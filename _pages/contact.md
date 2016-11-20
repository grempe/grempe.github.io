---
layout: page
title: Contact
permalink: /contact/
---

Something I am passionate about is the ability for each of us to communicate freely
while maintaining the confidentiality of our communications. The right to privacy
is a [fundamental human right](http://motherboard.vice.com/read/united-nations-encryption-and-online-anonymity-are-basic-human-rights){:target="_blank"}.

Privacy and security are not at odds with each other, and are essential to the
freedoms and liberties we enjoy. Strong encryption, used liberally, gives us
many of the tools we need to ensure we maintain these freedoms.

I would encourage you to learn more, and to make use of the tools at hand to
communicate with me. The [EFF Surveillance Self-Defense](https://ssd.eff.org){:target="_blank"}
site is a great starting point.

Here are some good ways to contact me, with varying security properties.

## Email

### Standard Security

My primary email address is hosted by Google. Unless you send encrypted email,
the expectation of privacy is pretty low.

* [glenn@rempe.us](mailto:glenn@rempe.us)

Please feel free to encrypt sensitive messages to me using PGP.

You can find [my PGP public key for email with ID 0xA4A288A3BECCAE17]({{ "/keys/" | relative_url }}) here.

*Supports : Plain Text / Encrypted Text / Attached Photos / Attached Documents*


### High Security

* [grempe@protonmail.com](mailto:grempe@protonmail.com)

Sensitive emails should be sent to my [ProtonMail](https://protonmail.com){:target="_blank"}
account. It is best if you also use ProtonMail to send the message to me, as that
way the message will be encrypted end-to-end. Read more about [ProtonMail Security](https://protonmail.com/security-details){:target="_blank"}.

If you don't also use ProtonMail please feel free to encrypt sensitive messages
to me at this address using PGP.

You can find [my PGP public key for email with ID 0xA4A288A3BECCAE17]({{ "/keys/" | relative_url }}) here.

*Supports : Plain Text / Encrypted Text / Attached Photos / Attached Documents*

## Instant Messaging

### Signal (Strongly Preferred)

Open Whisper Systems [Signal](https://whispersystems.org) is currently thought
to be very secure by people that I respect in the security and cryptography field.
Researchers have prepared [A Formal Security Analysis of the Signal Messaging Protocol (PDF)](https://eprint.iacr.org/2016/1013.pdf) and found it to be without any major
flaws.

Signal [has also demonstrated that they have extremely little metadata](https://whispersystems.org/bigbrother/eastern-virginia-grand-jury/){:target="_blank"} that
they can make available, even to governments even with lawful orders. Signal
is my preferred method of secure contact. If you have my mobile number
in your phone's contact list then you can reach me with Signal.

[How do I verify your safety numbers?](https://whispersystems.org/blog/safety-number-updates/){:target="_blank"}
Within a Signal conversation, touch my name at the top of the window and select
'Verify Safety Numbers' from the menu. Safety Numbers (also known as a fingerprint)
are unique 60 digit long numbers, unique to you and I alone. If we verify that we
have the same safety numbers when on a call, or in person, we gain some assurance
that our conversation cannot be intercepted by a man-in-the-middle attacker.

Only 30 digits of the safety number belong to you alone. The tricky part is
that the two halves are sorted and sometimes your portion will be first and sometimes
it will be last. If you change phones, or uninstall and re-install Signal our
safety numbers will change. Do not share the QR code for your safety numbers
publicly. The QR code contains safety numbers that are only valid for a single
contact pair.

My current Signal fingerprint is `58147 38090 62031 74518 07815 07777`

*Supports : Text Messaging / Voice Calls / Attached Photos / Attached Videos*


### Apple Messages

You can contact me using [Apple Messages](https://support.apple.com/explore/messages)
by adding my contact email address [glenn@rempe.us](mailto:glenn@rempe.us)
to your macOS/iOS device.

Unfortunately, Apple does not provide any way to view or verify key fingerprints
and your conversations are backed up to iCloud if you have automatic backups to
iCloud turned on. These backups are available to governments with a valid warrant.

*Supports : Text Messaging / Voice Calls / Video Calls / Attached Photos / Attached Videos*


### WhatsApp

WhatsApp can be used semi-securely, but it requires some config changes
to do so properly. Take a look at [this article from @thegrugq](https://medium.com/@thegrugq/operational-whatsapp-on-ios-ce9a4231a034#.6k0pzq7xr){:target="_blank"} for more info.

There are some serious security concerns with WhatsApp though due to their
insistance on pressuring users to backup all messages to their servers where
they will be available to WhatsApp and Facebook (or three letter agencies) on
request. It is not enough for you to refuse these backups, everyone else you
communicate with has to also. There are also concerns about WhatsApp now
sharing data with parent company Facebook which they initially promised would
not be done.

An additional security step you can take is to publish your WhatsApp fingerprint
publicly, for example on your facebook or twitter bio. WhatsApp does allow you
to publish your fingerprint, or verify the published fingerprint for another
user, but they don't make it particularly easy to do so. You can learn more about
it on their [End-to-End Encryption FAQ](https://www.whatsapp.com/faq/en/general/28030015){:target="_blank"} page.
The first step is to determine your own fingerprint.

1. Open the chat.
2. Tap on the name of the contact to open the contact info screen.
3. Tap Encryption to view the QR code and 60-digit number.

The fingerprint block you'll see, 12 groups of five numbers, is actually
the concatenation of your fingerprint, and the other person's fingerprint.
Each fingerprint is made up of six number blocks, so the first half
belongs to one of you, and the second half to the other. The tricky part is that
the two show no visible separation, and [are sorted by their value](https://twitter.com/dchest/status/717492356849803265). This means
that for any given chat partner, sometimes your fingerprint block comes first
and sometimes it comes last.

For example, if you're connected with me on WhatsApp and you view the 'Verify
Security Code' page, my portion of the fingerprint may be the first six blocks,
or the last six blocks of that verifier. It depends on how you would sort them.
So for me you will always see one of the following patterns, where
your fingerprint would be where the zeros are and mine is as shown.

``` text
56143 41025 77814 55362
45113 58854 00000 00000
00000 00000 00000 00000
```

``` text
00000 00000 00000 00000
00000 00000 56143 41025
77814 55362 45113 58854
```

So the easiest way to find out what your fingerprint is, is to look at the
verification page for two different chat connections you have, and find the
six number block that is the same between the two. The one that is the same,
which may come first or last in the sequence, is yours.

The easier way is to meet me in person and we can exchange and verify fingerprints
by scanning the QR code in the app, or by reading the fingerprint to each other
on a voice call, but only if we recognize each others voices.

*Supports : Text Messaging / Voice Calls / Attached Photos / Attached Videos*


### XMPP + OTR Chat

Learn more about [using XMPP+OTR+TOR in a great article](https://theintercept.com/2015/07/14/communicating-secret-watched/){:target="_blank"} by Micah Lee. Please contact me in advance if you wish to chat via XMPP + OTR.

``` text
XMPP/Jabber Address: grempe@xmpp-hosting.de
XMPP Provider:       https://jabber.hot-chilli.net/
OTR Fingerprint:     C30A3B09 C7C0240A 5A0033CA B99267F1 642354B0
```

``` text
XMPP/Jabber Address: glenn@rempe.us
XMPP Provider:       Google Talk (Not federated XMPP)
OTR Fingerprint:     3A93A6EF 7A8A8850 52525538 09BDBBB9 76E93502
```

*Supports : Text Messaging*

## Live Video Calls

Please use, in order of preference:

* Apple Facetime (end-to-end encrypted)
* Google Duo (end-to-end encrypted)
* Google Hangouts (end-to-end encrypted for [voice and video only](https://support.google.com/hangouts/answer/6046115?hl=en))
* Skype (nominally encrypted, but [considered unsafe](https://en.wikipedia.org/wiki/Skype_security))
