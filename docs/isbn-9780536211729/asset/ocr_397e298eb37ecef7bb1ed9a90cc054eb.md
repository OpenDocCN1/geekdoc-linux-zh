generating mailing list digests, operating X10 devices,¹ and updating the /etc/hosts files of neighboring systems when a system with dynamically changing IP address suffers a change.

Because the invoked program runs as root, using this feature creates security holes unless the program is written very carefully. The problems are very similar to those of CGI programs, except that CGI programs normally do not run as root.

Verify that your Sendmail version does not support the debug, wiz, or kill commands. This may be tested by connecting to your Sendmail and issuing these commands thusly.

```
telnet mail.pentacorp.com smtp
220-mail.pentacorp.com Sendmail 8.9.3/8.8.7 ready at 6 Sep 2000 22:20
220 SMTP spoken here
wiz
500 Command unrecognized
debug
500 Command unrecognized
kill
500 Command unrecognized
quit
221 mail.pentacorp.com closing connection
Connection closed by foreign host.
```

In this example, the Sendmail tested not support the insecure commands, so it is safe from these threats. If you get any other response than 500 Command unrecognized, you need to upgrade your version of Sendmail.

For older Sendmail installations, search the /etc/sendmail.cf file for a line starting

OW

The “o” command is enabling the “w” option. If the “w” option is enabled, the wizard’s password will be accepted; many crackers know what it is. The following command will be this:

```
grep '^OW' /etc/sendmail.cf
```

This would be the wizard's password. If it does not look like the following line, then it should be changed to look like it. This will disable the wizard's password. Failure to do so will offer a shell to anyone who knows the wizard's password.

OW*

+   1. X10 is a set of inexpensive remote control devices for controlling almost any electrical device for home and business use that are quite popular. They may be controlled by any computer with a serial connection and there is software available for Linux.