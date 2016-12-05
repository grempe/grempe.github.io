# OpenPGP Key Transition Statement

Glenn Rempe

December 4, 2016

Canonical location for this statement and its detached signature:

[https://www.rempe.us/downloads/keys/20161204-key-transition-statement.md](https://www.rempe.us/downloads/keys/20161204-key-transition-statement.md)

[https://www.rempe.us/downloads/keys/20161204-key-transition-statement.md.sig](https://www.rempe.us/downloads/keys/20161204-key-transition-statement.md.sig)

## Intro

I have created a new OpenPGP key `0x7FFCB72A6522542E` and will be
transitioning away from my old key `0xA4A288A3BECCAE17`. The old
key **has not been compromised** and will continue to be valid for some
time, but I prefer all future correspondence to be encrypted to the
new key, and I will be creating signatures with the new key going forward.

I would like this new key to be re-integrated into the web of trust.
This message is signed by both keys to certify the transition. My new
and old keys are signed by each other. If you have signed my old key,
I would appreciate signatures on my new key as well, provided that
your signing policy permits that without re-authenticating me.

In addition to cross-signing the new key, like the old one, is also
signed by my master signing key `0x63608B66C0929A67`, which is a
long term `sign` and `certify` only key which I use to sign all
other keys I directly control.

## Keys

These are the relevant keys for this transition statement.

### Master Signing Key

``` text
pub   rsa4096/0x63608B66C0929A67 2015-12-27 [SC]
      Key fingerprint = 1C01 711C 3A0F 691D 11A9  D8BE 6360 8B66 C092 9A67
uid                   [ultimate] Glenn Rempe (Master Signing Key) <glenn@rempe.us>
```

### Blog Signing Key

``` text
pub   rsa4096/0x37B8284B4B3EBE74 2015-12-27 [SC]
      Key fingerprint = A866 1C60 4BFD 85DE 26B7  80E5 37B8 284B 4B3E BE74
uid                   [ultimate] Glenn Rempe (Blog Signing Key) <glenn@rempe.us>
```

Also signed with my master signing key `0x63608B66C0929A67`

### Old Key `0xA4A288A3BECCAE17`

``` text
pub   rsa4096/0xA4A288A3BECCAE17 2014-10-02 [C] [expires: 2019-10-01]
      Key fingerprint = 497A 6138 963D 6C47 202B  238B A4A2 88A3 BECC AE17
uid                   [ultimate] Glenn Rempe <glenn@rempe.us>
uid                   [  never ] [jpeg image of size 1740]
uid                   [ revoked] Glenn Rempe <grempe@keybase.io>
sub   rsa4096/0xE7166A77CF97D091 2014-10-02 [S] [revoked: 2015-06-04]
sub   rsa4096/0xD1640B9CDB415269 2014-10-02 [E] [revoked: 2015-06-04]
sub   rsa4096/0x64360AFCB987E507 2014-10-02 [A] [revoked: 2015-06-04]
sub   rsa2048/0x85C81023D9E3FC2F 2015-06-04 [S] [expires: 2019-09-11]
sub   rsa2048/0x2992317D667E3936 2015-06-04 [E] [expires: 2019-09-11]
sub   rsa2048/0x19EA4BEADCC31080 2015-06-04 [A] [expires: 2019-09-11]
```

Also signed with my master signing key `0x63608B66C0929A67`

### New Key `0x7FFCB72A6522542E`

``` text
pub   rsa4096/0x7FFCB72A6522542E 2016-11-30 [C] [expires: 2021-11-29]
      Key fingerprint = 8AE2 2920 FF71 1A64 8FDC  6786 7FFC B72A 6522 542E
uid                   [ultimate] Glenn Rempe <glenn@rempe.us>
sub   rsa4096/0x0A25436DD4439C6C 2016-12-01 [S] [expires: 2021-11-30]
sub   rsa4096/0xB5FB54504E609461 2016-12-01 [E] [expires: 2021-11-30]
sub   rsa4096/0xB31F795B60C3AE12 2016-12-01 [A] [expires: 2021-11-30]
```

Also signed with my master signing key `0x63608B66C0929A67`

### Cross Key Signatures

I have cross-signed the old and new keys and signed each with my
master signing key. The cross signatures were created with the following
commands:

``` text
# new key signs old
gpg2 --default-key 0x7FFCB72A6522542E --sign-key 0xA4A288A3BECCAE17

# old key signs new
gpg2 --default-key 0xA4A288A3BECCAE17 --sign-key 0x7FFCB72A6522542E

# master signing key signs new
gpg2 --default-key 0x63608B66C0929A67 --sign-key 0x7FFCB72A6522542E
```

## The Signing Process For You

Fetch and import the old key from a public key server. If you have previously
signed this key you can check for your own signature on this key:

``` text
gpg2 --keyserver pgp.mit.edu --recv-key 0xA4A288A3BECCAE17
```

Fetch and import the new key from a public key server:

``` text
gpg2 --keyserver pgp.mit.edu --recv-key 0x7FFCB72A6522542E
```

Verify that the new key is signed by the old one:

``` text
gpg2 --check-sigs 7FFCB72A6522542E
```

If you are satisfied that you've got the right key, and the User IDs
match what you expect, I would appreciate it if you would sign my new key:

``` text
gpg2 --sign-key 7FFCB72A6522542E
```

Once signed, please upload your signatures to a public keyserver directly:

``` text
gpg2 --keyserver pgp.mit.edu --send-key 7FFCB72A6522542E
```

Or email `glenn@rempe.us` (optionally encrypted with the same key) the output from:

``` text
gpg2 --armor --export 7FFCB72A6522542E
```

Note: The old and new keys are also available directly from my website.

[https://www.rempe.us/downloads/keys/0xA4A288A3BECCAE17.asc](https://www.rempe.us/downloads/keys/0xA4A288A3BECCAE17.asc)

[https://www.rempe.us/downloads/keys/0x7FFCB72A6522542E.asc](https://www.rempe.us/downloads/keys/0x7FFCB72A6522542E.asc)

If you'd like any further verification or have any questions about the
transition please [contact me directly](https://www.rempe.us/contact/).

### Verifying This Transition Statement

#### Using Detached Signature

You can verify that this file was signed by me with both the old
and new keys using the commands:

``` text
# import old public key if you don't have it
gpg2 --keyserver pgp.mit.edu --recv-key A4A288A3BECCAE17

# import new public key if you don't have it
gpg2 --keyserver pgp.mit.edu --recv-key 7FFCB72A6522542E

# download this statement and review it
wget https://www.rempe.us/downloads/keys/20161204-key-transition-statement.md

# download the detached signature for this statement
wget https://www.rempe.us/downloads/keys/20161204-key-transition-statement.md.sig

# verify the detached signature
gpg2 --verify 20161204-key-transition-statement.md.sig
```

Note: The command used to sign this file with both old and new keys:

``` text
gpg2 --local-user 0x7FFCB72A6522542E --local-user 0xA4A288A3BECCAE17 --output 20161204-key-transition-statement.md.sig --detach-sig 20161204-key-transition-statement.md
```

#### Using Github Signed Commits

All commits in the Git repository
[grempe/grempe.github.io](https://github.com/grempe/grempe.github.io/commits/master),
where this transition statement is found, are signed with my
Blog Signing Key `0x37B8284B4B3EBE74`.
