image means that you should not blindly trust what you download. The mirror you were directed to may have been compromised, or you might be the victim of an attack yourself.
To alleviate this, the Kali project always provides checksums of the images it distributes. But to make such a check effective, you must be sure that the checkSum you grabbed is effectively the checkSum published by the Kali Linux developers. You have different ways to ascertain this.

# Relying on the TLS-Protected Website

When you retrieve the checkSum from the TLS-protected download webpage, its origin is indirectly guaranteed by the X.509 certificate security model: the content you see comes from a web site that is effectively under the control of the person who requested the TLS certificate.
Now you should generate the checkSum of your downloaded image and ensure that it matches what you recorded from the Kali website:

```
```
$ sha256sum kali-linux-2017.1-amd64.iso
49b1c576989b0922b066d0dc4c8e11a6909f7a270a80ad259e05773101df62e11e9d kali-linux-2016.2-amd64.iso
```
```

If your generated checkSum matches the one on the Kali Linux download page, you have the correct file. If the checkSums differ, there is a problem, although this does not indicate a compromise or an attack; downloads occasionally get corrupted as they traverse the Internet. Try your download again, from another official Kali mirror, if possible (see “cdimage.kali.org” [page 14] for more information about available mirrors).

# Relying on GPG’s Web of Trust

If you don’t trust HTTPS for authentication, you are a bit paranoid but rightfully so. There are many examples of badly managed certificate authorities that issued rogue certificates, which ended up being misused. You may also be the victim of a “friendly” man-in-the-middle attack implemented on many corporate networks, using a custom, browser-implanted trust store that presents fake certificates to encrypted websites, allowing corporate auditors to monitor encrypted traffic.
For cases like this, we also provide a GnuPG key that we use to sign the checksums of the images we provide. The key’s identifiers and its fingerprints are shown here:

```
```
pub rsa4096/0xED444FF07D8D0BF6 2012-03-05 [SC] [expires: 2018-02-02]
Key fingerprint = 44C6 513A 8E4F B303 0875 F758 ED44 4FF0 7D8D 0BF6
uid [full ] Kali Linux Repository <dev@kali.org>
sub rsa4096/0xA8373E18FC00D0CB 2012-03-05 [E] [expires: 2018-02-02]
```
```

This key is part of a global web of trust because it has been signed at least by me (Raphaël Hertzog) and I am part of the web of trust due to my heavy GnuPG usage as a Debian developer.