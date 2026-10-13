```
undefine('BITNET_RELAY')
FEATURE(redirect)
FEATURE(always_add_domain)
MAILER(local)
MAILER(smtp)
```

This m4 configuration produces a fairly standard sendmail.cf file that provides for delivery of incoming mail to local user mailboxes and delivery of outgoing mail through SMTP.

The directives in this file have the following effect:

+   - **include('../m4/cf.m4')**: This directive includes generic configuration directives necessary for all sendmail.cf files.
+   - **OSTYPE('linux')**: This directive indicates that you are building a sendmail.cf file for a Linux-based sendmail system and forces inclusion of the necessary Linux-specific configuration information.
+   - **undefine('UUCP_RELAY')**: This directive indicates that your sendmail system does not need to support UUCP routing of mail and, accordingly, the relevant sections of sendmail.cf are excluded.
+   - **undefine('BITNET_RELAY')**: This directive indicates that your sendmail system does not need to support BITNET routing of mail and, accordingly, the relevant sections of sendmail.cf are excluded.
+   - **FEATURE(redirect)**: This directive indicates that any mail of the form <address>.REDIRECT should be rejected with the reply message indicating the user’s new address. When users leave your organization their email addresses can be aliased to <address>.REDIRECT so that people who attempt to contact them can be informed of their new address.
+   - **FEATURE(always_add_domain)**: This directive indicates that the From line of all outgoing messages should contain the domain portion of the address and if a From line doesn’t have a domain portion the local domain should be appended.
+   - **FEATURE(local)**: This directive indicates that sendmail should allow delivery of messages to local Unix mailboxes through the standard sendmail local mailer.
+   - **FEATURE(smtp)**: This directive indicates that sendmail should allow delivery of messages to remote servers using SMTP.

As this example illustrates, using m4 greatly simplifies the generation of sendmail.cf files. m4 increases the clarity of the configuration process and leads to succinct configuration files. However, m4 also provides a great wealth of configuration directives that allow you to control the finer aspects of your sendmail configuration. The wealth of possibilities presented through m4 configurations is beyond the scope of this book. In fact, several chapters could be devoted to the numerous possibilities afforded by m4 configuration for sendmail.

An excellent discussion of how to configure sendmail with m4 can be found at the sendmail Web site at http://www.sendmail.org/m4/readme.html.