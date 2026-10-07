# The Red Hat Hat Configuration 125

```
define('CONFDONT_PROBE_INTERFACES',true)dnl
define('PROCMAIL_MAIL_PATH', '/usr/bin/procmail')dnl
define('ALIAS_FILE', '/etc/aliases')dnl
define('STATUS_FILE', '/var/log/sendmail.st')dnl
define('UUOCCP_MAIL_MAX', '2000000')dnl
define('CONFUSERDB_SPEC', '/etc/mail/userdb.db')dnl
FEATURE('smارش', '/usr/sbin/smrs')dnl
FEATURE('mailertable', hash -o /etc/mail/mailertable)dnl
FEATURE('virtertable', hash -o /etc/mail/virtertable)dnl
FEATURE(redirect)dnl
FEATURE(always_add_domain)dnl
FEATURE(use_cw_file)dnl
FEATURE(local_procmail)dnl
FEATURE('access_db')dnl
FEATURE('blacklist_recipients')dnl
FEATURE('accept_unresolvable_domains')dnl
MAILER(smtp)dnl
MAILER(procmail)dnl
```

Okay, it is still surprisingly large, but it is not as bad as it looks. We have already covered many of the lines in this file and do not need to cover them. divert and include covered in Chapter 4. Now know what the VERSIONED macro can and ignore it. OSTYPE('linux') macro is the same one covered earlier in this chapter, and during discussion of the linux.m4 file we covered PROCMAIL_MAIL_PATH AND FEATURE(local_procmail). We also covered FEATURE(redirect), FEATURE(use_cw_file), and MAILER(smtp) during the discussion of the generic-linux.mc configuration. We've made a good start. Still, there are left of commands to discuss.

# Understanding the Defines and Undefines

The first command in this configuration is a define command that overrides the default setting of CONF_USER_ID, which is the variable that holds the user ID and group ID used by Sendmail. By default confDEF_USER_ID is set to 1:1, which on a Red Hat system is user bin and group bin. In the redhat.mc configuration file this is changed to 8:12, which is mail user and mail group. Having a specific user ID and group ID for Sendmail is a good idea. The bin user can be used for a wide variety of programs. Creating a specific mail user and group makes it easier to track actions back to Sendmail and to control the access Sendmail is given to the rest of the system.

The next two lines are undef that clear the names of the relay servers from the UUCP_RELAY and the BITNET_RELAY variables. Clearing these variables means that all UUCP sites may be directly connected and that the .BITNET pseudo-domain will not

![](bbox=[0.933, 0.085, 0.995, 0.365])