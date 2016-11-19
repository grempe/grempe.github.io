---
layout: post
title: "Yubikey, GnuPG 2.1 Modern, and SSH on macOS"
date: "2016-01-11 10:33"
tags: security cryptography gnupg ssh yubikey osx
categories: security
---

I have been using a Yubico
[Yubikey NEO](https://www.yubico.com/products/yubikey-hardware/yubikey-neo/){:target="_blank"}
security token to store my [GnuPG](https://www.gnupg.org/){:target="_blank"}
private keys for about a year now. The Yubikey is a powerful security token and
I wanted to make use of it to manage my SSH keys as well. I also recently transitioned
to the newer [GnuPG 'Modern' 2.1.x](https://gnupg.org/faq/whats-new-in-2.1.html){:target="_blank"}
release and there are significant changes to how you would go about using your
GPG keys for SSH.  Since I ran into a few issues, and the existing documentation
on the web is somewhat lacking, I thought I would write up some notes documenting
how I did it, and how I solved at least one issue I was having with the interaction
between the the Yubikey and the `gpg-agent` on macOS.

## GnuPG Install

I use [Homebrew](http://brew.sh){:target="_blank"} on macOS and installed the latest version (2.1.16) of GnuPG
Modern using [homebrew-versions](https://github.com/Homebrew/homebrew-versions/blob/master/README.md){:target="_blank"}:

``` text
# NOTE : Installation of 'pinentry-mac' requires a full Xcode installation.
# The command line tools are not sufficient.
brew tap homebrew/versions
brew install gnupg21
brew install pinentry-mac
```

## Installing GPG keys on Yubikey

Here is a useful site for learning how to add your SSH keys to your Yubikey.

* [https://blog.josefsson.org/2014/06/23/offline-gnupg-master-key-and-subkeys-on-yubikey-neo-smartcard/](https://blog.josefsson.org/2014/06/23/offline-gnupg-master-key-and-subkeys-on-yubikey-neo-smartcard/){:target="_blank"}

## Using GnuPG for SSH Authentication

The following websites offered some useful info when learning about using the
Yubikey for SSH.

* [http://incenp.org/notes/2015/gnupg-for-ssh-authentication.html](http://incenp.org/notes/2015/gnupg-for-ssh-authentication.html){:target="_blank"}
* [https://lists.gnupg.org/pipermail/gnupg-users/2012-July/045059.html](https://lists.gnupg.org/pipermail/gnupg-users/2012-July/045059.html){:target="_blank"}
* [http://budts.be/weblog/2012/08/ssh-authentication-with-your-pgp-key](http://budts.be/weblog/2012/08/ssh-authentication-with-your-pgp-key){:target="_blank"}
* [https://gnupg.org/faq/whats-new-in-2.1.html](https://gnupg.org/faq/whats-new-in-2.1.html){:target="_blank"}  (see 'Auto-start of the gpg-agent')


## Setup GnuPG Agent for SSH

**UPDATE** : January 15, 2016 : It has been brought to my attention that adding a
keygrip to the `sshcontrol` file is not strictly necessary when using a smart-card
like the Yubikey. It is apparently only needed when dealing with keys on disk and
also explains the double entry I was seeing with `ssh-add -l`. I have removed the
section about discovering your keygrip ID and adding it to `sshcontrol` which
simplifies this setup a bit.

Configure your `gpg-agent` to start with SSH support in
`~/.gnupg/gpg-agent.conf` by adding the `enable-ssh-support` entry. Here's
my config (which also makes use of the pinentry-mac package we installed earlier).

``` text
default-cache-ttl 900
max-cache-ttl 999999
pinentry-program /usr/local/bin/pinentry-mac
enable-ssh-support
```

Next, configure all of your shell environment to have an appropriate
`SSH_AUTH_SOCK` environment variable. Here are the relevant lines
from my `~/.zshrc`. You'll want to source your config file or close
and open a new terminal window after this change.

``` text
...
# GPG 2.1.x SSH support
# See : http://incenp.org/notes/2015/gnupg-for-ssh-authentication.html
export SSH_AUTH_SOCK=$HOME/.gnupg/S.gpg-agent.ssh
...
```

Ensure your Yubikey is removed and restart your `gpg-agent` process,
then re-insert your Yubikey. Alternatively, run `killall gpg-agent`.
You may want to also confirm that you no longer have any `ssh-agent` processes
running. `ssh-agent` is no longer used at all with this setup.

``` text
* remove key *
/usr/local/bin/gpgconf --kill gpg-agent && /usr/local/bin/gpgconf --launch gpg-agent
* insert key *
```

Running `gpg2 --card-status` should display a summary of your Yubikey config
including the keys you have installed on it.

Now you are almost ready to go. Your GPG keys are on your Yubikey, the `gpg-agent`
is running and ready to support your SSH client, and all that you need to do is
reveal your SSH public key so you can add it to the `authorized_keys` file on
your remote server you want to access with SSH.

``` text
$ ssh-add -L
ssh-rsa AAAAB3Nza+MY_LONG_SSH_PUB_KEY cardno:000600000000
```

Grab the last line starting with `ssh-rsa` and paste
that into the `authorized_keys` file on the remote machine you want to SSH to.
This should be one long line and should contain no line breaks.

[Here is what the docs say](https://gnupg.org/faq/whats-new-in-2.1.html){:target="_blank"}
about the behavior of `gpg-agent` in the context of SSH. This is important to understand.
The `gpg-agent` must be running for SSH using GnuPG + Yubikey to work.

> Auto-start of the gpg-agent : If the option --enable-ssh-support is used the auto-start mechanism does not work because ssh does not know about this mechanism. Instead it is required that the environment variable SSH_AUTH_SOCK is set to the S.gpg-agent.ssh socket in the GnuPG home directory. Further gpg-agent must be started: Either by using a GnuPG command which implicitly starts gpg-agent or by using gpgconf --launch gpg-agent to explicitly start it if not yet done.

## Done?

OK, you should be ready to `ssh you@remotehost.com` now! Make sure your Yubikey
is inserted and ssh to that host. If all is working right, you should be prompted
for the user PIN for your Yubikey to unlock it, and once you enter that PIN you
should succeed in your ssh login.

## Problems?

**UPDATE** : January 15, 2016 : I am working through this issue in the gnupg-users
mailing list. You can follow along with the discussion thread  [here](https://lists.gnupg.org/pipermail/gnupg-users/2016-January/054988.html){:target="_blank"}.
I'll update this post again if there is a resolution to this issue.

I ran into one major problem with this setup. It seems that if the `gpg-agent`
is running and you remove your Yubikey and re-insert it, the `gpg-agent` will
no longer recognize that your Yubikey is present and SSH logins won't work.

Normally this isn't a problem when just using the Yubikey for GPG keys since
GnuPG will take care of launching the agent as needed.  But in the SSH scenario
you want the `gpg-agent` to be ready to go for SSH whenever your Yubikey is
inserted.

The only way I could discover to fix this was to kill and restart `gpg-agent` after
each Yubikey insertion.

``` text
gpgconf --kill gpg-agent && gpgconf --launch gpg-agent
```

Of course this is a PITA. There has to be a better way.

## Using controlPlane to restart GnuPG agent after Yubikey removal and insertion

What I wanted, as a workaround to the problem, was to re-start the agent after the
Yubikey is removed, and then once again whenever it is re-inserted. I think this may
be possible using `launchd` on macOS, but I settled on using ControlPlane which is
an macOS application that can apply system config, or run arbitrary shell scripts,
in reaction to designated system events. In our case it can be configured to run
a shell script that will re-start `gpg-agent` every time a Yubikey is inserted
or removed.

I added the following shell script (make sure it is `chmod 700`) to
`~/bin/gpg-agent-restart.sh`.

``` text
#!/bin/bash
/usr/local/bin/gpgconf --kill gpg-agent && /usr/local/bin/gpgconf --launch gpg-agent
```

You can test that this technique will work for you by running that script manually
after a removal and re-insertion of the Yubikey. If it does, then you can [install
ControlPlane](http://www.controlplaneapp.com){:target="_blank"} to automate it.

### ControlPlane Setup

Setup a 'Yubikey' context. This may not be strictly necessary.

![ControlPlane - Contexts]({{ "/images/2016-01-11-control-plane/1-contexts.png" | relative_url }}){:width="300px"}

Make sure the 'Attached USB Device' checkbox is checked on the Evidence Sources tab.

![ControlPlane - Evidence Sources]({{ "/images/2016-01-11-control-plane/2-evidence-sources.png" | relative_url }}){:width="300px"}

On the Rules tab click the **+** to add a rule which is based on the presence
of the Yubikey. Make sure the Yubikey is plugged in when you select this tab
so its available in the drop-down.

![ControlPlane - Rules Yubikey]({{ "/images/2016-01-11-control-plane/3a-rules-yubikey.png" | relative_url }}){:width="300px"}

![ControlPlane - Rules]({{ "/images/2016-01-11-control-plane/3b-rules.png" | relative_url }}){:width="300px"}

On the Actions tab click the **+** to add a new Action. Provide the full path to
your shell script and be sure to set the context to the name of the context
you chose in the first step, no delay, and choose to execute on **both** arrival
and departure of the Yubikey.

![ControlPlane - Actions]({{ "/images/2016-01-11-control-plane/4-actions.png" | relative_url }}){:width="300px"}

And that should do it! When you insert or remove the Yubikey you should see
a notification (and a log entry in the advanced tab of ControlPlane) showing
that the script is getting run. Your `gpg-agent` should be getting a new PID
every time you insert the Yubikey.

## Know a better way?

Please do [let me know](https://github.com/grempe/grempe.github.io/issues) and
I'll be sure to try out your ideas and document them here if they improve things.

Now all that is remaining is to migrate that collection of SSH
public keys you have now over to your new GPG/SSH key to rule them all. Enjoy!
