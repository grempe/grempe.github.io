---
layout: page
title: My Keys
permalink: /keys/
redirect_from:
  - /pgp/
---

## Keybase

[Keybase](https://keybase.io){:target="_blank"} provides a way to claim
ownership of OpenPGP keys and uses those keys to sign proofs
that claim ownership of other Internet properties. You can independently verify
the cryptographic proofs on each of those properties to see if I do in
fact control them. You can find my PGP public email key and all of my claimed
properties at [https://keybase.io/grempe](https://keybase.io/grempe){:target="_blank"}.


## OpenPGP / GnuPG

I use [GnuPG](https://gnupg.org/){:target="_blank"} 'Modern' v2.1.x for email
encryption and digital signatures. I use it to sign things like documents, code,
and the source code for this blog.

There is a single `Master Signing Key`, which acts as a kind of trust root, with which
I sign all of my other valid keys. In addition to the master, I currently have
a specialized `Blog Signing Key` and a `Code Signing Key`.  These signing keys
can only be used to certify other keys or for digital signatures. They cannot
be used for encryption.

I also maintain one or more traditional GnuPG email keys which can be used for signing,
key certification, or encryption. These keys will also be signed by the `Master Signing Key`.
For GnuPG Web of Trust (WOT) requests, I will sign your email keys with one of my email keys
and you are invited to sign my email key and any of my signing keys.

This hierarchy can help you determine which keys really belong to me. If a
currently valid key claiming to be mine is not also signed by the `Master Signing Key`
then you should not consider it valid without consulting with me first over a trusted
channel.

{% highlight text %}
|                          Master Signing Key
|                                  +
|           +----------------------------------------------+
|           +                      +                       +
|   Email Key (1..n)        Blog Signing Key       Code Signing Key
{% endhighlight %}

Since this entire repository is signed, either at commit time or with a signed tag, any
content that is found within can be implicitly trusted if the signatures are valid.

### Install All Keys

You can install all of my current signing and email keys by running the following command.
You should then verify the fingerprint for each key with the key data I have enclosed below.

{% highlight text %}
gpg2 --keyserver pgp.mit.edu --recv-keys 0x63608B66C0929A67 0x37B8284B4B3EBE74 0x2C4C3C144301224F 0xA4A288A3BECCAE17
{% endhighlight %}

You will then also need to run `gpg2 --edit-key KEYID` for each key and choose the `trust`
option which will allow you to specify the `ownertrust` level you want to assign to each of
my keys. Hopefully you will feel comfortable choosing `I trust fully`. Here is an example
session for a single key.

{% highlight text %}
$ gpg2 --edit-key C0929A67
gpg (GnuPG) 2.1.9; Copyright (C) 2015 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.


pub  rsa4096/C0929A67
     created: 2015-12-27  expires: never       usage: SC
     trust: unknown       validity: unknown
[ unknown] (1). Glenn Rempe (Master Signing Key) <glenn@rempe.us>

gpg> trust
pub  rsa4096/C0929A67
     created: 2015-12-27  expires: never       usage: SC
     trust: unknown       validity: unknown
[ unknown] (1). Glenn Rempe (Master Signing Key) <glenn@rempe.us>

Please decide how far you trust this user to correctly verify other users' keys
(by looking at passports, checking fingerprints from different sources, etc.)

  1 = I don't know or won't say
  2 = I do NOT trust
  3 = I trust marginally
  4 = I trust fully
  5 = I trust ultimately
  m = back to the main menu

Your decision? 4

pub  rsa4096/C0929A67
     created: 2015-12-27  expires: never       usage: SC
     trust: full          validity: unknown
[ unknown] (1). Glenn Rempe (Master Signing Key) <glenn@rempe.us>
Please note that the shown key validity is not necessarily correct
unless you restart the program.

gpg> quit
{% endhighlight %}


### Master Signing Key

The 'Trust Root'. All my intermediate signing keys (blog, code), and my email keys
are signed by this master key. The master key is kept offline and is never used for
anything but signing my other keys. Verifying the presence of this key signature is the
strongest way to determine if a key is indeed mine.

{% highlight text %}
pub   rsa4096/0x63608B66C0929A67 2015-12-27
      Key fingerprint = 1C01 711C 3A0F 691D 11A9  D8BE 6360 8B66 C092 9A67
uid                   [ultimate] Glenn Rempe (Master Signing Key) <glenn@rempe.us>

gpg> check
uid  Glenn Rempe (Master Signing Key) <glenn@rempe.us>
sig!3        0x63608B66C0929A67 2015-12-27  [self-signature]
{% endhighlight %}

#### Install Key [0x63608B66C0929A67.asc](/downloads/keys/0x63608B66C0929A67.asc)

from keyserver (w/ any third party signatures):

{% highlight text %}
gpg2 --keyserver pgp.mit.edu --recv-key 0x63608B66C0929A67
{% endhighlight %}

from this server:

{% highlight text %}
gpg2 --fetch-keys http://www.rempe.us/downloads/keys/0x63608B66C0929A67.asc
{% endhighlight %}

manually:

{% highlight text %}
wget https://www.rempe.us/downloads/keys/0x63608B66C0929A67.asc
gpg2 --import 0x63608B66C0929A67.asc
{% endhighlight %}


### Blog Signing Key

The following key is used to sign this blog repository. Signatures applied to
commits or tags can be cryptographically verified using the [GPG signing functionality
built into Git](http://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work){:target="_blank"}.

{% highlight text %}
pub   rsa4096/0x37B8284B4B3EBE74 2015-12-27
      Key fingerprint = A866 1C60 4BFD 85DE 26B7  80E5 37B8 284B 4B3E BE74
uid                   [ultimate] Glenn Rempe (Blog Signing Key) <glenn@rempe.us>

gpg> check
uid  Glenn Rempe (Blog Signing Key) <glenn@rempe.us>
sig!3        0x37B8284B4B3EBE74 2015-12-27  [self-signature]
sig!         0x63608B66C0929A67 2015-12-27  Glenn Rempe (Master Signing Key)
{% endhighlight %}

#### Install Key [0x37B8284B4B3EBE74.asc](/downloads/keys/0x37B8284B4B3EBE74.asc)

from keyserver (w/ any third party signatures):

{% highlight text %}
gpg2 --keyserver pgp.mit.edu --recv-key 0x37B8284B4B3EBE74
{% endhighlight %}

from this server:

{% highlight text %}
gpg2 --fetch-keys http://www.rempe.us/downloads/keys/0x37B8284B4B3EBE74.asc
{% endhighlight %}

manually:

{% highlight text %}
wget https://www.rempe.us/downloads/keys/0x37B8284B4B3EBE74.asc
gpg2 --import 0x37B8284B4B3EBE74.asc
{% endhighlight %}


### Code Signing Key

The following key is used to sign code and general Git commits:

{% highlight text %}
pub   rsa4096/0x2C4C3C144301224F 2015-12-27
      Key fingerprint = FCDD 20FD D083 C84A 5C64  0405 2C4C 3C14 4301 224F
uid                   [ultimate] Glenn Rempe (Code Signing Key) <glenn@rempe.us>

gpg> check
uid  Glenn Rempe (Code Signing Key) <glenn@rempe.us>
sig!3        0x2C4C3C144301224F 2015-12-27  [self-signature]
sig!         0x63608B66C0929A67 2015-12-27  Glenn Rempe (Master Signing Key)
{% endhighlight %}

#### Install Key [0x2C4C3C144301224F.asc](/downloads/keys/0x2C4C3C144301224F.asc)

from keyserver (w/ any third party signatures):

{% highlight text %}
gpg2 --keyserver pgp.mit.edu --recv-key 0x2C4C3C144301224F
{% endhighlight %}

from this server:

{% highlight text %}
gpg2 --fetch-keys http://www.rempe.us/downloads/keys/0x2C4C3C144301224F.asc
{% endhighlight %}

manually:

{% highlight text %}
wget https://www.rempe.us/downloads/keys/0x2C4C3C144301224F.asc
gpg2 --import 0x2C4C3C144301224F.asc
{% endhighlight %}


### Email Key

The following key is used for encryption and digital signatures of email or files.
It is also the key I use for signing other people's keys in the Web of Trust (WOT):

{% highlight text %}
pub   rsa4096/0xA4A288A3BECCAE17 2014-10-02 [expires: 2019-10-01]
      Key fingerprint = 497A 6138 963D 6C47 202B  238B A4A2 88A3 BECC AE17
uid                   [  full  ] Glenn Rempe <glenn@rempe.us>
uid                   [  full  ] [jpeg image of size 1740]
sub   rsa2048/0x85C81023D9E3FC2F 2015-06-04 [expires: 2019-09-11]
sub   rsa2048/0x2992317D667E3936 2015-06-04 [expires: 2019-09-11]
sub   rsa2048/0x19EA4BEADCC31080 2015-06-04 [expires: 2019-09-11]

gpg> check
uid  Glenn Rempe <glenn@rempe.us>
sig!3        0xA4A288A3BECCAE17 2014-10-02  [self-signature]
sig!3        0xA4A288A3BECCAE17 2014-11-06  [self-signature]
sig!         0x63608B66C0929A67 2015-12-27  Glenn Rempe (Master Signing Key)
uid  Glenn Rempe <grempe@keybase.io>
rev!         0xA4A288A3BECCAE17 2015-12-27  [revocation]
sig!3        0xA4A288A3BECCAE17 2014-11-06  [self-signature]
sig!         0x63608B66C0929A67 2015-12-27  Glenn Rempe (Master Signing Key)
uid  [jpeg image of size 1740]
sig!3        0xA4A288A3BECCAE17 2014-10-02  [self-signature]
sig!         0x63608B66C0929A67 2015-12-27  Glenn Rempe (Master Signing Key)
{% endhighlight %}

#### Install Key [0xA4A288A3BECCAE17.asc](/downloads/keys/0xA4A288A3BECCAE17.asc)

from keyserver (w/ any third party signatures):

{% highlight text %}
gpg2 --keyserver pgp.mit.edu --recv-key 0xA4A288A3BECCAE17
{% endhighlight %}

from this server:

{% highlight text %}
gpg2 --fetch-keys http://www.rempe.us/downloads/keys/0xA4A288A3BECCAE17.asc
{% endhighlight %}

manually:

{% highlight text %}
wget https://www.rempe.us/downloads/keys/0xA4A288A3BECCAE17.asc
gpg2 --import 0xA4A288A3BECCAE17.asc
{% endhighlight %}

Find some additional info on this email key and its position in the Web of Trust:

* [http://biglumber.com/x/web?sn=Glenn+Rempe](http://biglumber.com/x/web?sn=Glenn+Rempe){:target="_blank"}
* [http://biglumber.com/x/web?qs=0xA4A288A3BECCAE17](http://biglumber.com/x/web?qs=0xA4A288A3BECCAE17){:target="_blank"}
* [http://keyserver.cns.vt.edu/pks/lookup?search=0xA4A288A3BECCAE17&op=vindex](http://keyserver.cns.vt.edu/pks/lookup?search=0xA4A288A3BECCAE17&op=vindex){:target="_blank"}
* [http://pgp.cs.uu.nl/mk_path.cgi?STAT=0xBECCAE17&STATS=statistics](http://pgp.cs.uu.nl/mk_path.cgi?STAT=0xBECCAE17&STATS=statistics){:target="_blank"}


### Verifying code signatures

#### Signed Commits

You can verify git commit signatures on this blog, or other code I may have signed,
by first installing the appropriate signing key in your local GnuPG keyring. Once
that step is done you can make a local clone of a signed repository, and view the
commit log to verify signatures.

{% highlight text %}
# download and install a signing key to your local system
# (see instructions above)

# make a local git clone of this blog (or other signed repo)
$ git clone https://github.com/grempe/grempe.github.io.git
$ cd grempe.github.io

# view the log showing any signatures associated with commits
$ git log --show-signature
{% endhighlight %}

A good signature on a commit looks like this example. A signature on a commit
secures the chain of all previous commits reachable by that commit.

{% highlight text %}
commit 29c1b16c4397cda5d6cd03401052300752197eb8
gpg: Signature made Mon Dec 28 11:25:00 2015 PST
gpg:                using RSA key 0x37B8284B4B3EBE74
gpg: Good signature from "Glenn Rempe (Blog Signing Key) <glenn@rempe.us>" [ultimate]
Primary key fingerprint: A866 1C60 4BFD 85DE 26B7  80E5 37B8 284B 4B3E BE74
Author: Glenn Rempe <glenn@rempe.us>
Date:   Mon Dec 28 11:24:59 2015 -0800

    Change title to rempe.us
{% endhighlight %}

#### Signed Tags

Similar to signed git commits, git tags can also be signed and verified. Signed
tags also secure all commits reachable by that tag.

Install a signing key as shown above, list all tags with `git tag --list` and
verify any individual tag with `git tag -v TAGNAME` where `TAGNAME` is one of the
listed tags. Here is an example:

{% highlight text %}
# view all tags
$ git tag -l
v1.0.0-beta

# verify an individual tag
$ git tag -v v1.0.0-beta
object 29c1b16c4397cda5d6cd03401052300752197eb8
type commit
tag v1.0.0-beta
tagger Glenn Rempe <glenn@rempe.us> 1451332998 -0800

Beta release of the new site
gpg: Signature made Mon Dec 28 12:03:18 2015 PST
gpg:                using RSA key 0x37B8284B4B3EBE74
gpg: Good signature from "Glenn Rempe (Blog Signing Key) <glenn@rempe.us>" [ultimate]
Primary key fingerprint: A866 1C60 4BFD 85DE 26B7  80E5 37B8 284B 4B3E BE74
{% endhighlight %}


### Note : my signing keys do not expire

You may have noted my signing keys do not have expiration dates. This is
intentional. There is a fundamental problem with using an expiration date on
keys used for code signing. If a signing key expires it is unclear what
the outcome should be when someone verifies code which was written and
signed while the key was still valid. Has the code that was signed
become untrustworthy?

It is likely that we would like the old code, written and signed when the key was
still valid, to continue to verify cleanly long into the future. The only way
I am currently aware of accomplishing this is with signing keys that never expire.

## Alternatives

### miniLock

[miniLock](https://minilock.io/){:target="_blank"} is a Chrome browser extension
that uses your email and a secret passphrase to generate a miniLock ID. miniLock IDs
are small and easy to share online — anyone can use your ID to encrypt files to you, and
you can encrypt files to friends using their miniLock IDs. miniLock is a pretty
simple way to encrypt any document and can be used by almost anyone. Your miniLock
public key is small enough to fit in a Tweet. Here is mine.

{% highlight text %}
2Gas5UUw2piLwcHYcmmnRqJnCXADvnRBVT8TEAeVrfPZHw
{% endhighlight %}


### Minisign

[Minisign](https://jedisct1.github.io/minisign/){:target="_blank"} is a 'dead
simple tool to sign files and verify signatures'.

Any files I may sign with Minisign with be accompanied by a corresponding `*.minisig` file.

You can verify the signature using my Minisign public key:

{% highlight text %}
RWQoTKyaaWHgW90HtwGvvCCTqmTGcUTiEeW+YHxdE4t+ijBEONfEPlpO
{% endhighlight %}

{% highlight text %}
# example usage to verify a file
minisign -Vm <file> -P RWQoTKyaaWHgW90HtwGvvCCTqmTGcUTiEeW+YHxdE4t+ijBEONfEPlpO
{% endhighlight %}


*This page and my key management techniques were inspired by
[Joanna Rutkowska's key page](http://blog.invisiblethings.org/keys/){:target="_blank"}.*