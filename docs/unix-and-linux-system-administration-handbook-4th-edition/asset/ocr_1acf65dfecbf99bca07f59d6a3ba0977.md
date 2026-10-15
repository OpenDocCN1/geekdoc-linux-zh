user’s acting on instructions from forged email that appears to emanate from this domain could have disastrous consequences, so it’s best if such email can be refused or discarded without reaching the addressee.

The ADSP TXT record can also include a t=y clause if you are just testing out DKIM and don’t want recipients to take your signatures too seriously.

During the development of the ADSP system, prior to RFC5617, a domain’s ADSP TXT record was kept in a different subdomain (_domainkey.domain, with no _adsp prefix) and had a slightly different syntax. o=~ meant that the domain signed some of its email, and o=- meant that it signed all email.

Since the two conventions use different subdomains, they can coexist. As of this writing, the original form remains predominant. If you are serious about getting recipients to scrutinize your signatures, it’s probably best to use both conventions for the next few years until everyone has become RFC5617-compliant.

Let’s look at an example. Gmail does not have an ADSP record, but Yahoo! does:

```
_domainkey.yahoo.com. 7200 IN TXT "t=y; O=~;" n=http://antispam.yahoo.com/domainkeys"
```

The n= clause is a comment that points a human user to more information about Yahoo!’s use of DKIM records.16 Some sites include an email address (without any @s, to avoid spam) instead. Here is yahoo.com’s DKIM TXT record for the key (selector) s1024:

```
s1024._domainkey.yahoo.com. 86400 IN TXT "k=rsa; t=y; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDRreeOi4juz+QfWYui /E9GXSXau/2PBLjNTD8V4UUnn+2FAZVG3L23BzeoULYY4PeeleB3gfm /JDJ0GX3N5L4KJA UUHfWwDeb0NPs+BK0VeKTATLY5/Y3SbT7xhy+1xtJ4Rk dV7V7xTn56Lb4udUnwuxK4V5b5PdOKj/XcwID4AQAB; n=A 1024 bit key,"
```

Here again, the n= clause is a comment, this time about the key itself.

The DKIM records shown in this section are all TXT records, but they will eventually migrate to the DKIM record type, which has the same format. In the interim, sites can use both record types to be sure there are no transition issues.

Chapter 20 covers the steps needed to implement DKIM within your mail system.

# SSHFP resource records

SSH, the secure shell, allows secure remote logins over an insecure network. It uses two authentication schemes, one for the host itself and one for the user attempting to log in. Unfortunately, users typically accept whatever host key ssh presents to them without verifying it. DNS’s SSHFP record type lets ssh verify the host key automatically, ensuring that the user has reached the intended machine and not an impostor.