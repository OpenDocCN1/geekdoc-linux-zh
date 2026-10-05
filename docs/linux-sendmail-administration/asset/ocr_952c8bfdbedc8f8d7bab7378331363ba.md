# The Red Hat Configuration

# 125

```
define(`PROCMAIL_MAILER_PATH`, `/usr/bin/procmail`)dnl
define(`ALIAS_FILE`, `/etc/aliases`)`)
define(`STATUS_FILE`, `/var/log/sendmail.st`)dnl
define(`UOCP_MAILER_MAX`, `2000000`)dnl
define(`CONFUSERDB_SPEC`, `/etc/mail/userdb.db`)dnl
FEATURE(`smsh`, `/usr/bin/smsh`)dnl
FEATURE(`mailertable`, `-hash -o /etc/mail/mailertable`)dnl
FEATURE(`virtertable`, `-hash -o /etc/mail/virtertable`)dnl
FEATURE(`redirect`)dnl
FEATURE(`always_domain`)dnl
FEATURE(`use_cw_file`)dnl
FEATURE(`local_procmail`)dnl
FEATURE(`access_db`)dnl
FEATURE(`blacklist_recipients`)dnl
FEATURE(`accept_unresolvable_domains`)dnl
MAILER(`smtp`)dnl
MAILER(`procmail`)dnl
```

![](bbox=[0.913, 0.298, 0.977, 0.355])

Okay, it is surprisingly large, but it is not as bad as it looks. We have already covered many of the lines in this file and don't need to cover them again. divert and were covered in Chapter 4. We know the VERSIONED mode and can ignore it. The OSTYPE(`linux`) marco is the same one covered earlier in this chapter, and during discussion of the linux.m4 file we covered PROCMAIL_PATH and FEATURE(local_procmail). We also covered FEATURE(`redirect`), FEATURE(use_cw_file), and MAILER(`smtp`) during discussion of the generic-linux.mc configuration. We've made a good start. Still, there are leafs of commands to discuss.

# Understanding Defines and Undefines

The first new command in this configuration is a command that overrides the default setting of confDEF_USER_ID, which holds the user ID and group ID used by Sendmail. By defaultDEF_USER_ID is set to 1:1, which on a Red Hat system is user bin and group bin. In the redhat.mc configuration file this is changed to 8:12, which is user mail and group mail. Having a specific user ID and group ID for Sendmail is a good idea. The bin user can be used for a variety of programs. Creating a specific mail user and group makes it easier to track actions back to Sendmail and to control the access Sendmail is given to the rest of the system.

The next two lines are undefined commands that clear the names of the relay servers from the UOCP_RELAY and the BITNET_RELAY variables. Clearing these variables means that all UOCP sites must be directly connected and that the .BITNET pseudo-domain will not

PART 2