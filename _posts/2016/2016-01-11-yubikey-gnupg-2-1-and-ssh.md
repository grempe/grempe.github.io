---
layout: post
title: "Yubikey, GnuPG 2.1 Modern, and SSH on OS X"
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
between the the Yubikey and the `gpg-agent` on OS X.

## GnuPG Install

I use [Homebrew](http://brew.sh){:target="_blank"} on OS X and installed the latest version (2.1.10) of GnuPG
Modern using [homebrew-versions](https://github.com/Homebrew/homebrew-versions/blob/master/README.md){:target="_blank"}:

{% highlight text %}
brew tap homebrew/versions
brew install gnupg21
brew install pinentry-mac
{% endhighlight %}

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

My primary key has key ID `0xA4A288A3BECCAE17`. I'll use that in my examples below.

Edit your key to identify which sub-key is used for authentication. If you don't
yet have an authentication sub-key I would refer you to the websites above.

{% highlight text %}
$ gpg2 --key-edit 0xA4A288A3BECCAE17
gpg (GnuPG) 2.1.10; Copyright (C) 2015 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Secret key is available.

gpg: TOFU: Ignoring revoked user id (Glenn Rempe <grempe@keybase.io>)
gpg: TOFU: Ignoring revoked user id (Glenn Rempe <grempe@keybase.io>)
sec  rsa4096/0xA4A288A3BECCAE17
     created: 2014-10-02  expires: 2019-10-01  usage: C
     validity: ultimate
The following key was revoked on 2015-06-04 by RSA key 0xA4A288A3BECCAE17 Glenn Rempe <glenn@rempe.us>
ssb  rsa4096/0xE7166A77CF97D091
     created: 2014-10-02  revoked: 2015-06-04  usage: S
The following key was revoked on 2015-06-04 by RSA key 0xA4A288A3BECCAE17 Glenn Rempe <glenn@rempe.us>
ssb  rsa4096/0xD1640B9CDB415269
     created: 2014-10-02  revoked: 2015-06-04  usage: E
The following key was revoked on 2015-06-04 by RSA key 0xA4A288A3BECCAE17 Glenn Rempe <glenn@rempe.us>
ssb  rsa4096/0x64360AFCB987E507
     created: 2014-10-02  revoked: 2015-06-04  usage: A
ssb  rsa2048/0x85C81023D9E3FC2F
     created: 2015-06-04  expires: 2019-09-11  usage: S
     card-no: 0006 00000000
ssb  rsa2048/0x2992317D667E3936
     created: 2015-06-04  expires: 2019-09-11  usage: E
     card-no: 0006 00000000
ssb  rsa2048/0x19EA4BEADCC31080
     created: 2015-06-04  expires: 2019-09-11  usage: A
     card-no: 0006 00000000
[ultimate] (1). Glenn Rempe <glenn@rempe.us>
[ revoked] (2)  Glenn Rempe <grempe@keybase.io>
[ultimate] (3)  [jpeg image of size 1740]
{% endhighlight %}

Find the sub-key with `usage: A` next to it. That is your Authentication sub-key
and is the one you will use for SSH. In my case it is `rsa2048/0x19EA4BEADCC31080`

Now, view your key with the additional Keygrip data you'll need for SSH.

{% highlight text %}
~$ gpg2 --with-keygrip -k 0xA4A288A3BECCAE17
pub   rsa4096/0xA4A288A3BECCAE17 2014-10-02 [expires: 2019-10-01]
      Key fingerprint = 497A 6138 963D 6C47 202B  238B A4A2 88A3 BECC AE17
      Keygrip = 5E485AA4FB7C25BE7F8FE3A095670CD7DE9164EE
uid                   [ultimate] Glenn Rempe <glenn@rempe.us>
uid                   [ultimate] [jpeg image of size 1740]
sub   rsa2048/0x85C81023D9E3FC2F 2015-06-04 [expires: 2019-09-11]
      Keygrip = 2CB90393A5D834F5B329C5EB55E0C6378ACAC003
sub   rsa2048/0x2992317D667E3936 2015-06-04 [expires: 2019-09-11]
      Keygrip = C5A98DAB4F5C1D355E05988BFA7449CCC75B5173
sub   rsa2048/0x19EA4BEADCC31080 2015-06-04 [expires: 2019-09-11]
      Keygrip = 12206385C2B0A6B8534ED6F0D235EC0C727E5146
{% endhighlight %}

In my case, since the authentication sub-key is `rsa2048/0x19EA4BEADCC31080` I
need Keygrip `12206385C2B0A6B8534ED6F0D235EC0C727E5146`.

Add the Keygrip for this auth sub-key to the file `~/.gnupg/sshcontrol`

{% highlight text %}
$ cat ~/.gnupg/sshcontrol
# List of allowed ssh keys.  Only keys present in this file are used
# in the SSH protocol.  The ssh-add tool may add new entries to this
# file to enable them; you may also add them manually.  Comment
# lines, like this one, as well as empty lines are ignored.  Lines do
# have a certain length limit but this is not serious limitation as
# the format of the entries is fixed and checked by gpg-agent. A
# non-comment line starts with optional white spaces, followed by the
# keygrip of the key given as 40 hex digits, optionally followed by a
# caching TTL in seconds, and another optional field for arbitrary
# flags.   Prepend the keygrip with an '!' mark to disable it.

# authentication sub-key keygrip for Yubikey KeyID 0xA4A288A3BECCAE17
12206385C2B0A6B8534ED6F0D235EC0C727E5146
{% endhighlight %}

Now, tell configure your `gpg-agent` to start with SSH support in
`~/.gnupg/gpg-agent.conf` by adding the `enable-ssh-support` entry. Here's
my config.

{% highlight text %}
default-cache-ttl 900
max-cache-ttl 999999
pinentry-program /usr/local/bin/pinentry-mac
enable-ssh-support
{% endhighlight %}

Lastly, configure all of your terminal shell environments to have an appropriate
`SSH_AUTH_SOCK` environment variable. Here are the relevant lines
from my `~/.zshrc`. You'll want to source your config file or close
and open a new terminal window after this change.

{% highlight text %}
...
# GPG 2.1.x SSH support
# See : http://incenp.org/notes/2015/gnupg-for-ssh-authentication.html
export SSH_AUTH_SOCK=$HOME/.gnupg/S.gpg-agent.ssh
...
{% endhighlight %}

Remove your Yubikey, and restart your `gpg-agent` process, and then re-insert your key.

{% highlight text %}
* remove key *
/usr/local/bin/gpgconf --kill gpg-agent && /usr/local/bin/gpgconf --launch gpg-agent
* insert key *
{% endhighlight %}

Running `gpg2 --card-status` should display all of the info for your Yubikey and
the keys you have installed on it.

If you have reached this point, you are almost ready to go. Your GPG keys are
on your Yubikey, the `gpg-agent` is running and ready to support your SSH client,
and all that you need to do is reveal your SSH public key so you can add it
to the `authorized_keys` file on your remote server you want to access with SSH.

{% highlight text %}
~$ ssh-add -L
error fetching identities for protocol 1: agent refused operation
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCms1sSkTyI6SUCPxMTiF8gr79+aKu7+eHHVl6fN36HACaTxSouTH3m4cfRc+tZUc3xBxMw5dIsHqD0dAahE/1uDlm+T9uxw9H+m5DpX3sZc/ZR9OYAtGmjpNp8Qa+dS1LnbuIDhF5WziFjekbXnp/WAGO+06sXw3Prelhk26RSEDInj2pGubzEFDqcr1YJHHa/9Ym9vQGboVGUnw9AaoG4GUOAJ1ZEG0S3tgqM8x4u90eynVd0T5e/SExX8zyvtivJWz6Pul84uVf7jcJJ7XGx6592alY4KmrhTauJeOB+YVmQdId7D/Iz9U1Kn45bQAtM4hTt6FPbU5MJmHK7YymF cardno:000600000000
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCms1sSkTyI6SUCPxMTiF8gr79+aKu7+eHHVl6fN36HACaTxSouTH3m4cfRc+tZUc3xBxMw5dIsHqD0dAahE/1uDlm+T9uxw9H+m5DpX3sZc/ZR9OYAtGmjpNp8Qa+dS1LnbuIDhF5WziFjekbXnp/WAGO+06sXw3Prelhk26RSEDInj2pGubzEFDqcr1YJHHa/9Ym9vQGboVGUnw9AaoG4GUOAJ1ZEG0S3tgqM8x4u90eynVd0T5e/SExX8zyvtivJWz6Pul84uVf7jcJJ7XGx6592alY4KmrhTauJeOB+YVmQdId7D/Iz9U1Kn45bQAtM4hTt6FPbU5MJmHK7YymF (none)
{% endhighlight %}

In this case, three lines are being printed. The first error line is something
I have not figured out how to remove yet but it does not seem to affect
functionality. The second and third lines in my case are both the same public
key and differ only in the comment field at the end.  I grabbed the last line
and pasted that into the `authorized_keys` file on my remote machine and changed
the comment field to indicate that this key was for my Yubikey.


{% highlight text %}
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCms1sSkTyI6SUCPxMTiF8gr79+aKu7+eHHVl6fN36HACaTxSouTH3m4cfRc+tZUc3xBxMw5dIsHqD0dAahE/1uDlm+T9uxw9H+m5DpX3sZc/ZR9OYAtGmjpNp8Qa+dS1LnbuIDhF5WziFjekbXnp/WAGO+06sXw3Prelhk26RSEDInj2pGubzEFDqcr1YJHHa/9Ym9vQGboVGUnw9AaoG4GUOAJ1ZEG0S3tgqM8x4u90eynVd0T5e/SExX8zyvtivJWz6Pul84uVf7jcJJ7XGx6592alY4KmrhTauJeOB+YVmQdId7D/Iz9U1Kn45bQAtM4hTt6FPbU5MJmHK7YymF (yubikey)
{% endhighlight %}

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

I ran into one major problem with this setup. It seems that if the `gpg-agent`
is running and you remove your Yubikey and re-insert it, the `gpg-agent` will
no longer recognize that your Yubikey is present and SSH logins won't work.

Normally this isn't a problem when just using the Yubikey for GPG keys since
GnuPG will take care of launching the agent as needed.  But in the SSH scenario
you want the `gpg-agent` to be ready to go for SSH whenever your Yubikey is
inserted.

The only way I could discover to fix this was to kill and restart `gpg-agent` after
each Yubikey insertion.

{% highlight text %}
gpgconf --kill gpg-agent && gpgconf --launch gpg-agent
{% endhighlight %}

Of course this is a PITA. There has to be a better way.

## Using controlPlane to restart GnuPG agent after Yubikey removal and insertion

What I wanted, as a workaround to the problem, was to re-start the agent after the
Yubikey is removed, and then once again whenever it is re-inserted. I think this may
be possible using `launchd` on OS X, but I settled on using ControlPlane which is
an OS X application that can apply system config, or run arbitrary shell scripts,
in reaction to designated system events. In our case it can be configured to run
a shell script that will re-start `gpg-agent` every time a Yubikey is inserted
or removed.

I added the following shell script (make sure it is `chmod 700`) to
`~/bin/gpg-agent-restart.sh`.

{% highlight text %}
#!/bin/bash
/usr/local/bin/gpgconf --kill gpg-agent && /usr/local/bin/gpgconf --launch gpg-agent
{% endhighlight %}

You can test that this technique will work for you by running that script manually
after a removal and re-insertion of the Yubikey. If it does, then you can [install
ControlPlane](http://www.controlplaneapp.com){:target="_blank"} to automate it.

### ControlPlane Setup

Setup a 'Yubikey' context. This may not be strictly necessary.

![ControlPlane - Contexts](/images/2016-01-11-control-plane/1-contexts.png){:width="300px"}

Make sure the 'Attached USB Device' checkbox is checked on the Evidence Sources tab.

![ControlPlane - Evidence Sources](/images/2016-01-11-control-plane/2-evidence-sources.png){:width="300px"}

On the Rules tab click the **+** to add a rule which is based on the presence
of the Yubikey. Make sure the Yubikey is plugged in when you select this tab
so its available in the drop-down.

![ControlPlane - Rules Yubikey](/images/2016-01-11-control-plane/3a-rules-yubikey.png){:width="300px"}

![ControlPlane - Rules](/images/2016-01-11-control-plane/3b-rules.png){:width="300px"}

On the Actions tab click the **+** to add a new Action. Provide the full path to
your shell script and be sure to set the context to the name of the context
you chose in the first step, no delay, and choose to execute on **both** arrival
and departure of the Yubikey.

![ControlPlane - Actions](/images/2016-01-11-control-plane/4-actions.png){:width="300px"}

And that should do it! When you insert or remove the Yubikey you should see
a notification (and a log entry in the advanced tab of ControlPlane) showing
that the script is getting run. Your `gpg-agent` should be getting a new PID
every time you insert the Yubikey.

## Know a better way?

Please do [let me know](https://github.com/grempe/grempe.github.io/issues) and
I'll be sure to try out your ideas and document them here if they improve things.

Now all thats left is to migrate that collection of SSH
public keys you have over to your new GPG/SSH key to rule them all. Enjoy!
