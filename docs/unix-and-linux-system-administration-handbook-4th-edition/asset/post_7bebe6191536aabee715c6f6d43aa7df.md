
sendmail's SafeFileEnvironment option controls where files can be written when email is redirected to a file by aliases or a .forward file. It causes sendmail to execute a chroot system call, making the root of the filesystem no longer / but rather /safe or whatever path you specified in the SafeFileEnvironment option. An alias that directed mail to the /etc/passwd file, for example, would really be written to /safe/etc/passwd.

The SafeFileEnvironment option also protects device files, directories, and other special files by allowing writes only to regular files. Besides increasing security, this option ameliorates the effects of user mistakes. Some sites set the option to /home to allow access to home directories while keeping system files off-limits.

Mailers can also be run in a chrooted directory.

## Privacy options

sendmail also has privacy options that control

- What external folks can determine about your site through SMTP
- What you require of the host on the other end of an SMTP connection
- Whether your users can see or run the mail queue

Table 20.15 lists the possible values for the privacy options as of this writing; see the file doc/op/op.ps in the distribution for current information.

### Table 20.15 Values of the PrivacyOption variable

| Value | Meaning |
|---|---|
| public | Does no privacy/security checking |
| needmailhelo | Requires SMTP HELO (identifies remote host) |
| noexpn | Disallows the SMTP EXPN command |
| novrfy | Disallows the SMTP VRFY command |
| needexpnhelo | Does not expand addresses (EXPN) without a HELO |
| needvrfyhelo | Does not verify addresses (VRFY) without a HELO |
| noverb* | Disallows verbose mode for EXPN |
| restrictmailq | Allows only mqueue directory's group to see the queue |
| restrictqrun | Allows only mqueue directory's owner to run the queue |
| restrictexpand | Restricts info displayed by the -bv and -v flags* |
| noetrn* | Disallows asynchronous queue runs |
| authwarnings | Adds warning header if outgoing message seems forged |
| noreceipts | Turns off delivery status notification for success return receipts |
| nobodyreturn | Does not return message body in a DSN |
| goaway | Disables all SMTP status queries (EXPN, VRFY, etc.) |

a. Verbose mode follows .forward files when an EXPN command is given and reports more information on the whereabouts of a user's mail. Use noverb or, better yet, noexpn, on any machine exposed to the outside world.
b. Unless executed by root or the TrustedUser.
c. ETRN is an ESMTP command intended for use by dial-up hosts. It requests that the queue be run just for messages to that host.

## We recommend conservatism; in your `.mc` file, use

```
define(`confPRIVACY_OPTIONS', `goaway, authwarnings, restrictmailq,
    restrictrun')
```

**sendmail's** default value for the privacy options is `authwarnings`; the line above would reset that value. Notice the double sets of quotes; some versions of **m4** require them to protect the commas in the list of privacy option values. Red Hat, Solaris, and AIX default to authwarnings; SUSE and Ubuntu to authwarnings, needmailhelo, novrfy, noexpn, and noverb; and HP-UX defaults to restrictrun, goaway, and authwarnings, the most secure—go, HP!

## Running a chrooted sendmail (for the truly paranoid)

If you are worried about the access that **sendmail** has to your filesystem, you can start it in a **chrooted** jail. (See page 913 in Chapter 22, *Security*, for more information about **chroot**.) Create a minimal filesystem in your jail, including things like `/dev/null`, `/etc` essentials (`passwd`, `group`, `resolv.conf`, `sendmail.cf`, any map files, `mail/*`), the shared libraries that **sendmail** needs, the **sendmail** binary, the mail queue directory, and any log files. You will probably have to fiddle with the list to get it just right. Use the `chroot` command to start a jailed **sendmail**. For example:

```
$ sudo chroot /jail /usr/sbin/sendmail -bd -q30m
```

## Denial of service attacks

Denial of service attacks are difficult to prevent because there is no a priori way to determine that a message is an attack rather than a valid piece of email. Attackers can try various nasty things, including flooding the SMTP port with bogus connections, filling disk partitions with giant messages, clogging outgoing connections, and mail bombing. **sendmail** has some configuration parameters that can help slow down or limit the impact of a denial of service attack, but these parameters can also interfere with legitimate mail. Milters can help sysadmins thwart a prolonged denial of service attack.

The MaxDaemonChildren option limits the number of **sendmail** processes. It prevents the system from being overwhelmed with **sendmail** work, but it also allows an attacker to easily shut down SMTP service. The MaxMessageSize option can help prevent the mail queue directory from filling, but if you set it too low, legitimate mail will bounce. (You might mention your limit to users so that they aren’t surprised when their mail bounces. We recommend a fairly high limit anyway, since some legitimate mail is huge.) The ConnectionRateThrottle option, which limits the number of permitted connections per second, can slow things down a bit. And finally, setting MaxRcptsPerMessage, which controls the maximum number of recipients allowed on a single message, might help.

**sendmail** has always been able to refuse connections (option REFUSE_LA) or queue email (QUEUE_LA) according to the system load average. A variation,
