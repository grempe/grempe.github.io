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
fact control them. You can find all of my PGP public keys and all of my claimed
properties at [https://keybase.io/grempe](https://keybase.io/grempe).


## OpenPGP / GnuPG Keys

I use [GnuPG](https://gnupg.org/) for email encryption and signing. I also use
it to sign various other things, such as documents, code, and this blog. I have
transitioned fully to `GnuPG 'Modern' version > 2.1.9`.

I use different keys for different things. There are specialized keys for
email, code signing, and for signing the Git repository I manage this blog with.

Since this repository is signed, either at commit time or with a signed tag, any
content that is found within this repo can probably be implicitly be trusted as coming
from me.

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

The following key is used to sign this blog repository:

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

You can find some additional info on this email key at the following links:

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

*This page and my key management technique was inspired by
[Joanna Rutkowska's key page](http://blog.invisiblethings.org/keys/){:target="_blank"}.*
