# Chapter 20

# Electronic Mail

We recommend sanitization; in your .mc file, use

```
define(PRIVACY_OPTIONS, "goaway, warnings, restrictmail,
restrictqr")
```

sendmail's default value for the privacy options is warnings; the line above will respect that. Notice the double sets of quotes; some versions of m4 require them to protect the commas in the list of privacy option values. Red Hat, Solaris, and AIX default to warnings; SUSE and Ubuntu to warnings, needmailhe, norfry, noexpn, noverb; and HP-UX defaults to restrictqrun, goaway, and warnings, the most secure—go, HP!

# Running a chrooted sendmail (for the truly paranoid)

If you are worried about the access that sendmail has to your filesystem, you can start it in a chrooted jail.(See page 913 in Chapter 22, Security, for more information about chroot.) Create a minimal filesystem in your jail, including things like /dev/null, /etc essentials (passwd, group, resolv.conf, sendmail.cf), any map files/, shared libraries that sendmail needs, the sendmail binary, the mail queue directory, and any log files. You will probably have to fiddle with the list to get it right. Use the chroot command to start a sendmail. For example:

```
$ sudo chrootjail /usr/sbin/sendmail -bd -q30m
```

# Denial of service attacks

Denial of service attacks are difficult to prevent because there is no priori to determine that an attack is rather than a valid piece of email. Attackers can try various nasty things, flooding the SMTP server with bogus connections, filling disk partitions with messages, clogging outgoing connections, and mail bombing. sendmail has some configuration parameters that can slow down or limit the impact of a denial of service attack, these parameters can also interfere with legitimate mail. Milters can help sysadmins thwart a prolonged denial of service attack.

The MaxDaemonChildren option limits the number of sendmail processes. It prevents the system from being overwhelmed with sendmail, but it also allows an attacker to easily shut down SMTP service. The MaxMessageSize option can prevent the mail queue directory from filling, but if you set it too low, legitimate mail will bounce. (You might mention your limit to users so that they aren't surprised when their mail bounces. We recommend a fairly high limit anyway, since legitimate mail is huge.) The ConnectionRateThrottle option, which limits the number of permitted connections per second, can slow down a bit. And finally, setting MaxRcptsPerMessage, controls the maximum number of recipients allowed on a single message, may help.

sendmail has always been able to refuse connections (option REFUSE_LA) or queue email (QUEUE_LA) according to the system load average. A variation,