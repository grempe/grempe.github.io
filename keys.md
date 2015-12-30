---
layout: page
title: My Keys
permalink: /keys/
---

## Keybase

[Keybase](https://keybase.io) provides a way to claim
ownership of certain OpenPGP keys uses those keys to sign proofs
that claim ownership of other Internet properties.You can independantly verify
the cryptographic proofs on each of those properties to see if I do in
fact control them. You can find my PGP public key and all of my claimed
properties at [https://keybase.io/grempe](https://keybase.io/grempe).


## OpenPGP / GnuPG Keys

I use [GnuPG](https://gnupg.org/) for email encryption and signing. I also use
it to sign various other things, such as documents, code, and this blog. I have
transitioned fully to `GnuPG 'Modern' version > 2.1.9`.

I use different keys for different things. There are specialized keys for
email, code signing, and for signing the Git repository I manage this blog with.

Since this repository is signed, either at commit time or with a signed tag, any
content that is found within can be implicitly trusted.

### Master Signing Key

All my keys are signed by the following Master Signing Key. Verifying the signature
of this key on any other key claiming to be mine is the strongest way to determine
if it is a key I claim ownership of.

{% highlight text %}
pub   rsa4096/0x63608B66C0929A67 2015-12-27
      Key fingerprint = 1C01 711C 3A0F 691D 11A9  D8BE 6360 8B66 C092 9A67
uid                   [ultimate] Glenn Rempe (Master Signing Key) <glenn@rempe.us>

gpg> check
uid  Glenn Rempe (Master Signing Key) <glenn@rempe.us>
sig!3        0x63608B66C0929A67 2015-12-27  [self-signature]
{% endhighlight %}

Download [0x63608B66C0929A67.asc](/downloads/keys/0x63608B66C0929A67.asc) from this signed repo.

This key is also attached to this repo in the downloads/keys/ directory. You should verify
the fingerprint of this master key using some other channel in addition to this blog
(e.g. my [https://keybase.io/grempe](https://keybase.io/grempe) account).

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

Download [0x37B8284B4B3EBE74.asc](/downloads/keys/0x37B8284B4B3EBE74.asc) from this signed repo.

#### Verifying Signed Commits

You can verify the commit or tag signatures on this blog by installing this signing
key in your local GPG, making a local clone of this repository, and viewing the commit
log with signatures.

{% highlight text %}
# download my blog signing key to your local system using the link above
# and change to your download directory (will vary by system)
$ cd ~/Downloads

# import the signing key
$ gpg2 --import 0x37B8284B4B3EBE74.asc

# verify the new public key is installed in GPG
$ gpg2 --list-keys 0x37B8284B4B3EBE74

# update the key from the keyserver
# (picking up new signatures or revocations)
$ gpg2 --keyserver http://keyserver.cns.vt.edu --recv-keys 0x37B8284B4B3EBE74

# make a local git clone of this blog repo
$ git clone https://github.com/grempe/grempe.github.io.git
$ cd grempe.github.io

# view the log showing any signatures associated with commits
$ git log --show-signature
{% endhighlight %}

A good signature on a commit looks like this example. A signature on a commit
or tag covers all previous commits reachable by that commit.

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

#### Verifying Signed Tags

Similar to signed git commits, git tags can also be signed and verified. Signed
tags also secure all commits reachable by that tag.

Install my blog signing key as shown above, list all tags with `git tag --list` and
verify any individual tag with `git tag -v TAGNAME` where `TAGNAME` is one of the tags
I have created. Here is an example:

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

Download [0x2C4C3C144301224F.asc](/downloads/keys/0x2C4C3C144301224F.asc) from this signed repo.

### Email Key

The following key is used for encryption, and signatures over, email communication:

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

Download [0xA4A288A3BECCAE17.asc](/downloads/keys/0xA4A288A3BECCAE17.asc) from this signed repo.

Find some additional info on this email key and its position in the Web of Trust:

* [http://biglumber.com/x/web?sn=Glenn+Rempe](http://biglumber.com/x/web?sn=Glenn+Rempe)
* [http://biglumber.com/x/web?qs=0xA4A288A3BECCAE17](http://biglumber.com/x/web?qs=0xA4A288A3BECCAE17)
* [http://keyserver.cns.vt.edu/pks/lookup?search=0xA4A288A3BECCAE17&op=vindex](http://keyserver.cns.vt.edu/pks/lookup?search=0xA4A288A3BECCAE17&op=vindex)
* [http://pgp.cs.uu.nl/mk_path.cgi?STAT=0xBECCAE17&STATS=statistics](http://pgp.cs.uu.nl/mk_path.cgi?STAT=0xBECCAE17&STATS=statistics)


### Note on the lack of expiration dates on signing keys

You may have noted my signing keys do not have expiration dates. This is
intentional. There is a fundamental problem with using an expiration date on
keys used for code signing (e.g. `git tag -s`). It is unclear what the
outcome should be when someone verifies code, which was written and
signed while the key was still valid, at some point in the future if the key has
been allowed to expire. Is the code untrustworthy?

Naturally we would like the old code, written and signed when the key was
still valid, to continue to verify cleanly long into the future. The only way
I am currently aware of accomplishing that is with keys that never expire.


### miniLock

[minilock](https://minilock.io/) is a Chrome browser extension that uses your email
and a secret passphrase to generate a miniLock ID. miniLock IDs are small and
easy to share online — anyone can use your ID to encrypt files to you, and
you can encrypt files to friends using their miniLock IDs. miniLock is a pretty
simple way to encrypt any document and can be used by almost anyone. Your miniLock
public key is small enough to fit in a Tweet.

{% highlight text %}
miniLock ID (glenn@rempe.us):
2Gas5UUw2piLwcHYcmmnRqJnCXADvnRBVT8TEAeVrfPZHw
{% endhighlight %}


## Minisign

[Minisign](https://jedisct1.github.io/minisign/){:target="_blank"} is a 'dead
simple tool to sign files and verify signatures'.

Any files I may sign with `minisign` with be accompanied by
a corresponding `*.minisig` file.

You can verify the signature using my `minisign` public key:

`RWQoTKyaaWHgW90HtwGvvCCTqmTGcUTiEeW+YHxdE4t+ijBEONfEPlpO`

{% highlight text %}
# example usage to verify a file
minisign -Vm <file> -P RWQoTKyaaWHgW90HtwGvvCCTqmTGcUTiEeW+YHxdE4t+ijBEONfEPlpO
{% endhighlight %}


*This page and my key management techniques were inspired by
[Joanna Rutkowska's key page](http://blog.invisiblethings.org/keys/){:target="_blank"}.*
