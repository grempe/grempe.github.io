---
layout: page
title: Projects
permalink: /projects/
---

Here is a sampling of the Open Source projects I have created,
maintain, or have contributed to. I have contributed thousands of commits,
pull requests, and issue reports to open source projects in the last
decade and I believe very strongly in the benefits of Open Source Software. You
can see a more detailed summary of my contributions on my [Github profile page](https://github.com/grempe){:target="_blank"}.

Some of the more recent interesting projects I have been working on include:

#### [Tierion](https://tierion.com){:target="_blank"} / [Chainpoint](https://chainpoint.org){:target="_blank"} (JavaScript / Node.js / Solidity / Bash / Docker / Kubernetes)

As Vice President of Engineering at [Tierion](https://tierion.com){:target="_blank"}, a blockchain technology provider, I was broadly responsible for all engineering efforts, DevOps, and the overall technical architecture. I designed and coded large portions of the codebase and I am a co-author of the [Chainpoint Proof](https://tokensale.tierion.com/TierionTokenSaleWhitePaper.pdf) standard. The vast majority of this code is available as Open Source code at:

* [https://github.com/tierion](https://github.com/tierion){:target="_blank"}
* [https://github.com/chainpoint](https://github.com/chainpoint){:target="_blank"}
* [https://chainpoint.org](https://chainpoint.org){:target="_blank"}
* [https://tokensale.tierion.com](https://tokensale.tierion.com){:target="_blank"}
* [Chainpoint Network Whitepaper](https://tokensale.tierion.com/TierionTokenSaleWhitePaper.pdf){:target="_blank"}

#### [grempe/grempe.github.io](https://github.com/grempe/grempe.github.io){:target="_blank"} (HTML / Markdown / CSS)

The source code for this website.

#### [grempe/sirp](https://github.com/grempe/sirp){:target="_blank"} (Ruby)

SiRP is a pure Ruby implementation of the Secure Remote Password
protocol (SRP-6a), which is a 'zero-knowledge' mutual authentication system.

SRP is a protocol that allows for mutual authentication of a client and
server over an insecure network connection without revealing the password
to the server or an eavesdropper.

There is a [live demo version](https://sirp-demo.herokuapp.com/index.html) you can try.

#### [grempe/tss-rb](https://github.com/grempe/tss-rb){:target="_blank"} (Ruby)

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

#### [grempe/rack-json_web_token_auth](https://github.com/grempe/rack-json_web_token_auth){:target="_blank"} (Ruby)

`Rack::JsonWebTokenAuth` is a Rack middleware that makes it easy for your Rack based application (Sinatra, Rails) to authenticate clients that present a valid `Authorization: Bearer [token]` header with a cryptographically signed [JSON Web Token (JWT)](https://jwt.io/).

#### [grempe/session-keys-rb](https://github.com/grempe/session-keys-rb){:target="_blank"} (Ruby)

SessionKeys is a cryptographic tool for the deterministic generation of NaCl
compatible Curve25519 encryption and Ed25519 digital signature keys.

Compatible with [grempe/session-keys-js](https://github.com/grempe/session-keys-js){:target="_blank"}

#### [grempe/session-keys-js](https://github.com/grempe/session-keys-js){:target="_blank"} (JavaScript)

SessionKeys is a cryptographic tool for the deterministic generation of NaCl
compatible Curve25519 encryption and Ed25519 digital signature keys.

Compatible with [grempe/session-keys-rb](https://github.com/grempe/session-keys-rb){:target="_blank"}

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
