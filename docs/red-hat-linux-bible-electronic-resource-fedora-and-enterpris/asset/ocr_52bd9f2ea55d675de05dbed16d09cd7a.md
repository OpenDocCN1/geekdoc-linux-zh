# Rewriting rules

The Rewriting rules section of the sendmail.cf file contains a complex set of rules needed to handle your sendmail service. The rules cover such things as converting addresses and dealing with local host names. You should not change entries in this section arbitrarily.

# Mailer definitions

Mail Delivery Agents (MDAs) are described in the mailer definitions. Specifically, the section defines the Mlocal and Mprog MDAs used (procmail and smrsh), respectively:

```
Mlocal, P=/usr/bin/procmail, F=lsDFMAw5:|@qSPfhn9, S=EnvFromL/HdrFromL, R=EnvToL/HdrToL, T=DNS/RFC822/X-Unix, A=procmail -Y -a $h -d $u
Mprog, P=/usr/bin/smrsh, F=lsDFMOgoe9, S=EnvFromL/HdrFromL, R=EnvToL/HdrToL, D=$z::/, T=X-Unix/X-Unix/X-Unix, A=smrsh -C $u
```

In general, you shouldn’t need to modify the options specified in the mailer definitions.

However, the Mlocal and Mprog mailer definitions, shown previously, are worthy of note. The Mlocal definition is for delivering messages to a local account. The procmail MDA is used (rather than the old UNIX standard of /bin/mail) to place the mail in the local user’s mailbox.

The Mprog mailer definition is used when the recipient of a message is actually a program (as in the case of majordomo, described in the next section). To direct a message to a program, sendmail uses a program called smrsh (SendMail Restricted Shell). Allowing mail to be piped directly into a program is not a great idea from a security standpoint, but smrsh makes the process a bit safer. For the program to successfully execute, a link to the program must exist within the /etc/smrsh directory. This restriction ensures that only programs installed by the administrator can directly receive mail, and other random executable programs are denied.

# Redirecting mail

At times, you may want to redirect mail to some place other than the recipient’s mailbox on the local server. Each user can redirect his mail using the .forward file. System-wide, you can set aliases to redirect mail in the /etc/aliases file.

# The .forward file

One way for users to redirect their own mail is through the use of the .forward file, as described within the previously listed sendmail.cf file. The format of a plain-text .forward file is a comma-separated list of mail recipients. Common uses of the .forward file include: