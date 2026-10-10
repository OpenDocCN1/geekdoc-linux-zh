```
```
/usr/sbin/makemap hash access.db < access
chmod 0640 access.db
# make restart
Restarting: sendmail sendmail-clinetmqueue.
```
```

An excellent and complete discussion of virtual hosting and the use of the `virtusertable` file can be found at the Sendmail Consortium information site (`http://www.sendmail.org/virtual-hosting.html`).

# NOTE

By the way, `/etc/mail/Makefile` and all these convenient targets for rebuilding the various configuration databases are additions to FreeBSD and are not part of Sendmail as released by its developers. Other operating systems don’t provide these conveniences. If you’re going to be maintaining a Sendmail installation on a Linux system or some other platform, you’ll want to know the underlying commands beneath each of the build targets in the Makefile so that you can accomplish the same tasks. The documentation at `http://www.sendmail.org` is very helpful in this regard.

# DNS Resolution Issues

Running a successful Sendmail server really requires that you have accurate DNS information set up for your machine. If you simply install FreeBSD, assign an available IP address to it, and attempt to send mail, it might bounce back to you complaining that the remote server “could not resolve your hostname.” Many SMTP servers, including Sendmail in its default configuration, do not accept mail from senders without fully qualified domains in their addresses or resolvable DNS names.

Before you try to put Sendmail to full use on your machine, you’ll need to make sure you have reverse DNS lookups correctly set up. You can check this with the `nslookup` command, giving it your machine’s IP address as an argument:

```
```
# nslookup stripes.somewhere.com
Server:		lion.somewhere.com
Address:		64.41.131.132

Name:		stripes.somewhere.com
Address:	64.41.131.102
```
```

This output shows a correctly resolving reverse DNS setup, one in which Sendmail will work just fine. However, you may get something like the following: