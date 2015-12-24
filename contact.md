---
layout: page
title: Contact
permalink: /contact/
---

As you will see I am interested in the ability for all of us to communicate
while maintaining the privacy of our communications. Privacy and security
are not just for those who have something to hide. It is something for all
of us to be mindful of in our everyday lives.

Privacy and security are essential to the freedoms and liberties we enjoy. Strong
encryption, used liberally, gives us the tools we need to ensure we keep these freedoms.

### Email

You can send email to me at the following addresses.

* [glenn@rempe.us](mailto:glenn@rempe.us)
* [grempe@protonmail.com](mailto:grempe@protonmail.com)

If your email is sensitive please use the [ProtonMail](https://protonmail.com)
account.  ProtonMail is a secure email service based in Switzerland and uses
[end-to-end encryption](https://en.wikipedia.org/wiki/End-to-end_encryption) when possible.

If you also have an account with ProtonMail (which is free and anonymous)
our emails will be end-to-end encrypted (a good thing). If you send email from
any other email account (e.g. you@gmail.com) your email will only be encrypted
once it finally reaches my ProtonMail Inbox. However, your original email and any replies
I send will still be stored on *your* server unencrypted which is [not as good thing](http://www.zdnet.com/article/fbi-says-it-doesnt-need-a-warrant-to-snoop-on-private-email-social-network-messages/).
Get a free account, its better for both of us.

### Open Whisper Systems - Signal

[Signal](https://whispersystems.org) is currently thought to be very secure by
people that I respect in the security industry.  Signal is my preferred method
of secure contact and supports voice, group text, private text, picture, and
video messages. If you have my mobile number in your phone's contact list then
you can reach me with Signal. If you need my phone number to contact me
via Signal please request it via email.

### OpenPGP/GnuPG

#### Master Key

* [0xA4A288A3BECCAE17.asc](/downloads/keys/0xA4A288A3BECCAE17.asc) (download directly)
* [http://biglumber.com/x/web?sn=Glenn+Rempe](http://biglumber.com/x/web?sn=Glenn+Rempe)
* [http://biglumber.com/x/web?qs=0xA4A288A3BECCAE17](http://biglumber.com/x/web?qs=0xA4A288A3BECCAE17)
* [http://keyserver.cns.vt.edu/pks/lookup?search=0xA4A288A3BECCAE17&op=vindex](http://keyserver.cns.vt.edu/pks/lookup?search=0xA4A288A3BECCAE17&op=vindex)
* [http://pgp.cs.uu.nl/mk_path.cgi?STAT=0xBECCAE17&STATS=statistics](http://pgp.cs.uu.nl/mk_path.cgi?STAT=0xBECCAE17&STATS=statistics)

**Key Fingerprint**

{% highlight text %}
497A 6138 963D 6C47 202B 238B A4A2 88A3 BECC AE17
{% endhighlight %}

**Key ID**

Using the 64 bit (0xlong) format to import my key is preferred
so as to avoid possible collisions with other keys with
the same shorter 32 bit ID.

{% highlight text %}
0xA4A288A3BECCAE17 (64 bit - last 16 digits of fingerprint)
0xBECCAE17         (32 bit - last 8 digits of fingerprint)
{% endhighlight %}

**Key Data**

{% highlight text %}
pub   4096R/0xA4A288A3BECCAE17 2014-10-02 [expires: 2019-10-01]
      Key fingerprint = 497A 6138 963D 6C47 202B  238B A4A2 88A3 BECC AE17
uid                 [ultimate] Glenn Rempe <glenn@rempe.us>
uid                 [ultimate] [jpeg image of size 1740]
uid                 [ultimate] Glenn Rempe <grempe@keybase.io>
sub   2048R/0x85C81023D9E3FC2F 2015-06-04 [expires: 2019-09-11]
sub   2048R/0x2992317D667E3936 2015-06-04 [expires: 2019-09-11]
sub   2048R/0x19EA4BEADCC31080 2015-06-04 [expires: 2019-09-11]
{% endhighlight %}

**Key Import and Verification from Keyserver**

To fetch my new key from a public key server, you can simply do:

{% highlight text %}
gpg --keyserver keyserver.cns.vt.edu --recv-key 0xA4A288A3BECCAE17
{% endhighlight %}

Verify the fingerprint of your imported key against my
published fingerprint.

{% highlight text %}
gpg --fingerprint 0xA4A288A3BECCAE17
{% endhighlight %}

**Key Import and Verification from DNS**

I have published a DNS TXT record that contains a pointer to my
public key as outlined [here](http://gushi.org/make-dns-cert/HOWTO.html):

You can view the DNS TXT record using the `dig` DNS command which will return
the key fingerprint and the URI that you can retrieve the key from.

{% highlight text %}
$ dig +short glenn._pka.rempe.us. TXT
"v=pka1\;fpr=497A6138963D6C47202B238BA4A288A3BECCAE17\;uri=https://www.rempe.us/pgp/0xA4A288A3BECCAE17.asc"
{% endhighlight %}

This allows you to import my public key automatically from this
trusted source (unless someone else now also controls my 'rempe.us' domain).
This bypasses any keyserver and can also be used as another data point
in verifying my key.

You can use this on the command line with the '--auto-key-locate pka'
command to GPG.

{% highlight text %}
# e.g. encrypt and armor a message for me
gpg --auto-key-locate pka -ea -r glenn@rempe.us
{% endhighlight %}


#### Blog/Code Signing Key

Coming soon. Soon I will create a non-expiring key that I will use solely for
signing this blog repository or for code signing. I will document that here
when it is fully operational.


### Keybase

[Keybase](https://keybase.io) is an up-and-coming alternative to prove
ownership of OpenPGP keys and control of other Internet properties.
Using this you can see the sites I claim as my own on the Internet, and then
verify the cryptographic proofs that show that I do in fact control them.

[https://keybase.io/grempe](https://keybase.io/grempe)


### miniLock

[minilock](https://minilock.io/) is a Chrome extension that uses your email
and a secret passphrase to generate a miniLock ID. miniLock IDs are small and
easy to share online — anyone can use your ID to encrypt files to you, and
you can encrypt files to friends using their miniLock IDs. miniLock is a much
simpler alternative to OpenPGP and can be used by almost anyone.

{% highlight text %}
miniLock ID (glenn@rempe.us):
2Gas5UUw2piLwcHYcmmnRqJnCXADvnRBVT8TEAeVrfPZHw
{% endhighlight %}

### XMPP + OTR Chat

Please contact me in advance if you wish to chat via XMPP + OTR.

{% highlight text %}
XMPP/Jabber Address: grempe@xmpp-hosting.de
XMPP Provider:       https://jabber.hot-chilli.net/
OTR Fingerprint:     C30A3B09 C7C0240A 5A0033CA B99267F1 642354B0
{% endhighlight %}

{% highlight text %}
XMPP/Jabber Address: glenn@rempe.us
XMPP Provider:       Google Talk (Not federated XMPP)
OTR Fingerprint:     3A93A6EF 7A8A8850 52525538 09BDBBB9 76E93502
{% endhighlight %}
