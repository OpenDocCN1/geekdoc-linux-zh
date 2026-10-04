
# 656 Installing the Mail Server

```
dnl define('CONFDONT_BLAME_SENDMAIL'.groupreadablekeyfile)dnl
dnl define('confTO_QUEUEWARN', '4h')dnl
dnl define('confTO_QUEUERTURN', '5d')dnl
dnl define('confTO_QUEUE_LA', '12d')dnl
dnl define('confTO_REFUSE_LA', '18h')dnl
dnl define('confTO_IDENT', '0')dnl
dnl FEATURE(delay_checks)dnl
dnl FEATURE('no_default_mail_sender')dnl
dnl FEATURE('sendmail', '.hash -o /usr/bin/ash.d')dnl
dnl FEATURE('mailertable', '.hash -o /etc/mail/mailertable.db')dnl
dnl FEATURE('virtuosable', '.hash -o /etc/mail/virtuosable.db')dnl
dnl FEATURE(restriction)dnl
dnl FEATURE(always_add_domain)dnl
dnl FEATURE(use_cw_file)dnl
dnl FEATURE(use_ct_file)dnl
dnl #
dnl # The t option will retry delivery if e.g. the user runs over quota.
dnl FEATURE(local_procmail,'procmail -t -Y -a $h -d $u')dnl
dnl FEATURE('access_db','.hash -TCMFP) -o /etc/mail/access.db')dnl
dnl USER(root)dnl
dnl EXPOSED_USER(root)dnl
dnl #
dnl # The following causes sending to only listen on the IPv4 lookup address
dl # 127.0.0.1 and not on any other network devices. Remove the loopback
dl # address restriction to accept email from the internet or intranet.
dl #
DAEMON,OPTIONS('port=smtp,Addr=127.0.0.1,Name-TA')dnl
dl #
dnl # The following causes sending to additionally listen to port 587 for
dl # from mail MUAs that authenticate. Roaming users who can't reach
dl # preferred send daemon to port 25 being blocked or redirected if
dl # this is useful.
dl #
DAEMON,OPTIONS('port=submission,Name-MSA,M=E-a')dnl
dl #
dnl # The following causes sending to additionally listen to port 465, but
dl # starting immediately in TLS mode upon connecting. Port 25 or 587 followed
dl # by STARTTLS is enabled, from roaming clients using Outlook Express can
dl # do not support STARTTLS ports other than 25. Mozilla Mail can only use STARTTLS
dl # and doesn't support STARTTLS Evolution Cl.1.1 or later.
ndl # when SSL is enabled - STARTTLS is available in version 1.1.1.
dl #
dl #
dl # # For this work your OpenSSL certificates must be configured.
dl #
DAEMON,OPTIONS('port=smtp,Name-TLSMTA,M=s')dnl
dl #
dnl # The following causes sending to additionally listen on the IPv6 lookup
dl # device. Remove the loopback address restriction listen to the network.
dl #
dl #
DAEMON,OPTIONS('port=smtp,Addr=::,Name-MTA-v6,Family=inet6')dnl
dl #
dnl # enable both ipv4 and ipv6 in sendmail:
dl #
DAEMON,OPTIONS('Name-MTA-v4,Family=inet,Name-MTA-v6,Family=inet6')dnl
dl #
dnl # # We strongly recommend not accepting unresolvable domains if you want to
dl # protect yourself from spam. However, the laptop and users on computers
dl # that do not have 24x7 DNS do we need.
dl #
```

# Installing the Mail Server 657

```
FEATURE('accept_unresolvable_domains')dnl
dnl # FEATURE('relay_based_on_MX')dnl
dnl #
dnl # Also accept email to "localhost.locomain" as local email.
dnl #
dnl LOCAL_DOMAIN('localhost.locomain')dnl
dnl # The following example makes mail from this host and any additional
dnl # specified domains appear to be sent from mydomain.com
dnl #
dnl MASQUERADE_AS('mydomain.com')dnl
dnl # masquerade not just the headers, but the envelope as
dnl #
dnl FEATURE('masquerade_envelope')dnl
dnl #
dnl # masquerade not just @mydomainalias.com, but @*.mydomainalias.com as
dnl # FEATURE('masquerade_entire_domain')dnl
dnl #
dnl MASQUERADE_DOMAIN(localhost)dnl
dnl MASQUERADE_DOMAIN(localhost.locomain)dnl
dnl MASQUERADE_DOMAIN(mydomainalias.com)dnl
dnl MAILER(-cf)dnl
MAILER(procmail)dnl
```

![](img/d9230b719dc0efd80851f363d8c6f571_683_0.png)

If you change the set for /etc/mail/sendmail.cf file, you must change the /etc/mail/sendmail.cf file by running the sendmail.cf file through the m4 macro processor with the following command (you have to log in as root):

m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf

The comments also tell you that the sendmail-cf package to this file.

From the previous section's description of m4 macros, you can see that sendmail.cf file use define to create new macros. You can also see the literal use of dnl to avoid inserting too many lines into the output.

The other uppercase words (such as OTYPE, FEATURE, and MAILER) are sendmail macros. These are defined in the m4 files in the subdirectories of the /usr/share/sendmail-cf directory and are incorporated into sendmail.cf file with the following macro:

```
include('/usr/share/sendmail-cf/m4/cf.m4')dnl
```

The /usr/share/sendmail-cf/m4/cf.m4 file, in turn, includes the cfhead.m4 file, which includes other m4 files, and so on. The net effect is that the m4 processor processes the sendmail.cf file, the macro processor incorporates many m4 files from various subdirectories of /usr/share/sendmail-cf.

# 658 Installing the Mail Server

There are some key points to note about the /etc/mail/sendmail.mc file:

- VERSIONID('setup for Red Hat Linux') macro inserts the version information enclosed in quotes into the output.
- OTYPE('linux') specifies Linux as the operating system. You have to specify this macro early to ensure proper configuration.
- Placing this mailer right after the VERSIONID macro is custom.
- MAILER(smtp) describes the mailer. According to instructions in the /usr/share/sendmail-cf/README file, MAILER declarations are always placed at the end of the sendmail.mc file, and MAILER(smtp) precedes MAILER(procmail). The mailer smtp is the SMTP mailer.
- FEATURE requests various special features. For example, FEATURE('blacklist_recipients') turns on the capability to block incoming mail for certain usernames, hosts.
- FEATURE('access_db','.hash -TCMFP) -o /etc/mail/access.db')
- FEATURE('masquerade_envelope')
- FEATURE('masquerade_entire_domain')
- FEATURE('accept_unresolvable_domains')
- MAILER(procmail)
- The following causes sending to only listen on the IPv4 lookup address 127.0.0.1 and not on any other network devices. Remove the loopback address restriction to accept email from the internet or intranet.
- The following causes sending to additionally listen to port 587 for from mail MUAs that authenticate. Roaming users who can't reach preferred send daemon to port 25 being blocked or redirected if this is useful.
- The following causes sending to additionally listen to port 465, but starting immediately in TLS mode upon connecting. Port 25 or 587 followed by STARTTLS is enabled, from roaming clients using Outlook Express can do not support STARTTLS ports other than 25. Mozilla Mail can only use STARTTLS and doesn't support STARTTLS Evolution Cl.1.1 or later. when SSL is enabled - STARTTLS is available in version 1.1.1.
- The following causes sending to additionally listen on the IPv6 lookup device. Remove the loopback address restriction listen to the network.

# Installing the Mail Server 657

If you change the set for /etc/mail/sendmail.cf file, you must change the /etc/mail/sendmail.cf file by running the sendmail.cf file through the m4 macro processor with the following command (you have to log in as root):

m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf

The comments also tell you that the sendmail-cf package to this file.

From the previous section's description of m4 macros, you can see that sendmail.cf file use define to create new macros. You can also see the literal use of dnl to avoid inserting too many lines into the output.

The other uppercase words (such as OTYPE, FEATURE, and MAILER) are sendmail macros. These are defined in the m4 files in the subdirectories of the /usr/share/sendmail-cf directory and are incorporated into sendmail.cf file with the following macro:

```
include('/usr/share/sendmail-cf/m4/cf.m4')dnl
```

The /usr/share/sendmail-cf/m4/cf.m4 file, in turn, includes the cfhead.m4 file, which includes other m4 files, and so on. The net effect is that the m4 processor processes the sendmail.cf file, the macro processor incorporates many m4 files from various subdirectories of /usr/share/sendmail-cf.

# Installing the Mail Server 658

There are some key points to note about the /etc/mail/sendmail.mc file:

- VERSIONID('setup for Red Hat Linux') macro inserts the version information enclosed in quotes into the output.
- OTYPE('linux') specifies Linux as the operating system. You have to specify this macro early to ensure proper configuration.
- Placing this mailer right after the VERSIONID macro is custom.
- MAILER(smtp) describes the mailer. According to instructions in the /usr/share/sendmail-cf/README file, MAILER declarations are always placed at the end of the sendmail.mc file, and MAILER(smtp) precedes MAILER(procmail). The mailer smtp is the SMTP mailer.
- FEATURE requests various special features. For example, FEATURE('blacklist_recipients') turns on the capability to block incoming mail for certain usernames, hosts.
- FEATURE('access_db','.hash -TCMFP) -o /etc/mail/access.db')
- FEATURE('masquerade_envelope')
- FEATURE('masquerade_entire_domain')
- FEATURE('accept_unresolvable_domains')
- MAILER(procmail)
- The following causes sending to only listen on the IPv4 lookup address 127.0.0.1 and not on any other network devices. Remove the loopback address restriction to accept email from the internet or intranet.
- The following causes sending to additionally listen to port 587 for from mail MUAs that authenticate. Roaming users who can't reach preferred send daemon to port 25 being blocked or redirected if this is useful.
- The following causes sending to additionally listen to port 465, but starting immediately in TLS mode upon connecting. Port 25 or 587 followed by STARTTLS is enabled, from roaming clients using Outlook Express can do not support STARTTLS ports other than 25. Mozilla Mail can only use STARTTLS and doesn't support STARTTLS Evolution Cl.1.1 or later. when SSL is enabled - STARTTLS is available in version 1.1.1.

# Installing the Mail Server 657

If you change the set for /etc/mail/sendmail.cf file, you must change the /etc/mail/sendmail.cf file by running the sendmail.cf file through the m4 macro processor with the following command (you have to log in as root):

m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf

The comments also tell you that the sendmail-cf package to this file.

From the previous section's description of m4 macros, you can see that sendmail.cf file use define to create new macros. You can also see the literal use of dnl to avoid inserting too many lines into the output.

The other uppercase words (such as OTYPE, FEATURE, and MAILER) are sendmail macros. These are defined in the m4 files in the subdirectories of the /usr/share/sendmail-cf directory and are incorporated into sendmail.cf file with the following macro:

```
include('/usr/share/sendmail-cf/m4/cf.m4')dnl
```

The /usr/share/sendmail-cf/m4/cf.m4 file, in turn, includes the cfhead.m4 file, which includes other m4 files, and so on. The net effect is that the m4 processor processes the sendmail.cf file, the macro processor incorporates many m4 files from various subdirectories of /usr/share/sendmail-cf.

# Installing the Mail Server 658

There are some key points to note about the /etc/mail/sendmail.mc file:

- VERSIONID('setup for Red Hat Linux') macro inserts the version information enclosed in quotes into the output.
- OTYPE('linux') specifies Linux as the operating system. You have to specify this macro early to ensure proper configuration.
- Placing this mailer right after the VERSIONID macro is custom.
- MAILER(smtp) describes the mailer. According to instructions in the /usr/share/sendmail-cf/README file, MAILER declarations are always placed at the end of the sendmail.mc file, and MAILER(smtp) precedes MAILER(procmail). The mailer smtp is the SMTP mailer.
- FEATURE requests various special features. For example, FEATURE('blacklist_recipients') turns on the capability to block incoming mail for certain usernames, hosts.
- FEATURE('access_db','.hash -TCMFP) -o /etc/mail/access.db')
- FEATURE('masquerade_envelope')
- FEATURE('masquerade_entire_domain')
- FEATURE('accept_unresolvable_domains')
- MAILER(procmail)

# sendmail.cf syntax

sendmail.cf file's syntax is designed to be easy to parse by the sendmail program because sendmail reads it whenever it starts. Human readability was not a primary consideration when the file's syntax was designed. Still, with a little explanation, you can understand the meaning of the control lines in sendmail.cf.

Each sendmail control line begins with a single-letter operator that defines the rest of the line. A line that begins with a space or a tab is considered a continuation of the previous line. Blank lines and lines begin with a pound (#) are comments.

Often, no space is between the single-letter operator and the arguments makes the lines even harder to understand. For example, sendmail uses the concept of a class — essentially a collection of phrases. You can define a class named P and add the phrase REDRECT to that class with the following control line:

```
PREDIRECT
```

Because everything is jumbled together, the command is hard to decipher. On the other hand, to define a class named Accept and set it to the values OK and RELAY, write the following:

```
C(Accept)OK RELAY
```

This command may be slightly easier to understand because the delimiters (such as the class, Accept) are enclosed in braces.

Other — more recent — control lines are even easier to understand. For example, the line

```
0 HelpFile=/etc/mail/helpfile
```

defines the option HelpFile as the filename /etc/mail/helpfile. That line contains help information sendmail uses when it receives a HELP command.
