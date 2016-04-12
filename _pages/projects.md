---
layout: page
title: Projects
permalink: /projects/
---

Here are a few of the Open Source projects I either created,
maintain, or contribute to. There are *many* more, but these are
active.

#### [grempe/grempe.github.io](https://github.com/grempe/grempe.github.io){:target="_blank"} (HTML/Markdown/CSS)

The source code for this website.

#### [grempe/tss](https://github.com/grempe/tss){:target="_blank"} (Ruby)

Threshold Secret Sharing (TSS) provides a way to generate N shares
from a value, so that any M of those shares can be used to
reconstruct the original value, but any M-1 shares provide no
information about that value. This method can provide shared access
control on key material and other secrets that must be strongly
protected.

This gem implements a Threshold Secret Sharing method based on
polynomial interpolation in GF(256) and a format for the storage and
transmission of shares.

This implementation follows the
[draft-mcgrew-tss-03](http://tools.ietf.org/html/draft-mcgrew-tss-03) specification.

#### [grempe/ex_rated](https://github.com/grempe/ex_rated){:target="_blank"} (Elixir)

ExRated, the Elixir OTP GenServer with the naughty name that allows you
to rate-limit calls to any service that requires it.

#### [grempe/diceware](https://github.com/grempe/diceware){:target="_blank"} (HTML/JavaScript/CSS)

Diceware is used to create cryptographically strong passphrases. It is based
on the principle that the truly random selection, based on rolls of dice, of
words in a word list can result in easily memorable passwords that are also
extremely resistant to attack by even the most powerful adversaries. Passwords
that are six words or longer are thought to be safe for high security applications.

A live version of this tool can be found at
[https://grempe.github.io/diceware/](https://grempe.github.io/diceware/){:target="_blank"}

#### [grempe/strongpass](https://github.com/grempe/strongpass){:target="_blank"} (HTML/JavaScript/CSS)

A deterministic, cryptographically strong, password and bitcoin wallet generator.

We all need passwords that are strong and easy to remember. If you can remember
one strong passphrase you can generate a password for any number of websites,
local applications, or even Bitcoin wallets. The same passphrase and options
will always result in the same output being generated. You can rest assured
that all cryptographic operations are done in your browser and no information
is sent elsewhere or shared with anyone.

A live version of this tool can be found at
[https://grempe.github.io/strongpass/](https://grempe.github.io/strongpass/){:target="_blank"}

#### [grempe/secrets.js](https://github.com/grempe/secrets.js){:target="_blank"} (JavaScript)

Another implementation of Shamir's Secret Sharing in JavaScript.

#### [jo/session25519](https://github.com/jo/session25519){:target="_blank"} (JavaScript)

session25519 is a public key cryptography library for the generation of
Curve25519 encryption and ed25519 digital signature keys.

#### [SpiderOak/crypton](https://github.com/SpiderOak/crypton){:target="_blank"} (JavaScript)

A framework for creating zero-knowledge mobile & desktop applications. You can
learn more about [crypton.io](https://crypton.io/). I have been an active contributor
to this project and support its goals of making the use of end-to-end encrypted
zero-knowledge back ends easier for developers to utilize.

### Archived Projects

#### [grempe/secretsharing](https://github.com/grempe/secretsharing){:target="_blank"} (Ruby)

Shamir's Secret Sharing is an algorithm in cryptography. It is a form of secret
sharing, where a secret is divided into parts, giving each participant its own
unique part, where some of the parts or all of them are needed in order to
reconstruct the secret. Holders of a share gain no knowledge of the larger secret.

This gem was dowloaded >6,000 times and was replaced by an improved
implementation : [grempe/tss](https://github.com/grempe/tss).

#### [grempe/amazon-ec2](https://github.com/grempe/amazon-ec2){:target="_blank"} (Ruby)

A Ruby Gem that gives you full access to several of the Amazon Web Services
API from Ruby. This was very popular when Amazon didn't provide their own Ruby
SDK. Since they now release and maintain their own this is no longer maintained.

### Other Projects

Over on Github You can see a variety of other
[projects I have toyed with over the years](https://github.com/grempe?tab=repositories){:target="_blank"}.
