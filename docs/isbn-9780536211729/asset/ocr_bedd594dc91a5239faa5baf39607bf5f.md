# 2.13.3 Upgrade sendmail

# DANGER LEVEL

The sendmail program is very complex, with all but the latest versions offering many well-known security holes. Upgrading is essential to security. The latest ones also have anti-spam software. There are some alternatives to sendmail, such as small, that claim to be easier to configure and possibly more secure. Since sendmail is used in many places I would consider it a safer bet.

Many systems have been broken into the past via sendmail exploits. Many of these exploits have involved buffer overflow, tricking sendmail into invoking a program of the cracker’s building instead of the intended one, and in the distant past, offering an interloper root shell on. In its defense it was written around 1980 by Eric Allman at Berkeley when the Internet was vastly smaller and friendlier. It must move between different users, communicate with a TCP port that only root normally allowed to listen on, use privileges for certain operations, parse an unimaginable and bizarre set of addressing methods, and must accept e-mail from any system in the world. It must also fork a variety of programs and offer various debugging options.

Because sendmail is a favorite target of crackers and spammers, it is critical for you to always keep yours upgraded to a recent version. Besides fixing past exploits, you will enjoy the benefits of the improvements that are continually being made to it. Commercial versions of sendmail are available from Sendmail, Inc. that are quite reasonably priced.

There are ways to configure sendmail so that it does not require running as root. If the limitations of this configuration are acceptable, this certainly reduces the severity of any remaining exploits that are discovered.

If your version of sendmail is older than 8.9.3, there are known buffer overflow exploits that you are vulnerable to. Note that major anti-spam features were introduced in sendmail version 8.9 and it also contains anti-relating features. Presently I consider 8.12.4 to be the minimum acceptable version of sendmail.

Version 8.12 of sendmail is available and you are strongly encouraged to install it on your system right now now. It is available from the CD-ROM and Web site; it may be downloaded

```
ftp://sendmail.org/pub/sendmail/sendmail.8.12.4.tar.gz
```

Some of the recent features of 8.12 are SMTP authentication, LDAP support, and multiple queues for parallel processing for enhanced performance. The SMTP authentication includes an optional password to limit your server to accepting e-mail only from certain sending systems and more spam blocking capability than previous versions. The new authentication level allows adding a security layer for digital signing and encryption.