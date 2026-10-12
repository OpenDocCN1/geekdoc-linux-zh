compiled into the sendmail configuration, let’s first look at the sendmail.mc file that comes with Red Hat and which already has several options provided (see Listing 17.1).

# **Listing 17.1 A Generic sendmail.mc File with Several Options Provided for Generating a Secure sendmail.cf File**

```
```text
divert(-1)
include('/usr/lib/sendmail-cf/m4/cf.m4')
define('confDEF_USER_ID', "8:12")
OSTYPE('linux')

undefine(`UUCP_RELAY`)
undefine(`BITNET_RELAY`)
define(`confAUTO_REBUILD`)
define(`confTO_CONNECT', '1m')
define(`confTRY_NULL_MX_LIST',true)
define(`confDONT_PROBE_INTERFACES',true)
define(`PROCMAIL_MAILER_PATH', '/usr/bin/procmail')
FEATURE(`smrsh','/usr/sbin/smrsh')
FEATURE(mailertable)
FEATURE(`virtusertable',`hash -o /etc/mail/virtusertable')
FEATURE(redirct)
FEATURE(always_add_domain)
FEATURE(use_cw_file)
FEATURE(local_procmail)
MAILER(procmail)
MAILER(smtp)

FEATURE(`access_db')
FEATURE(`blacklist_recipients')
FEATURE(`accept_unresolvable_domains')
dnl FEATURE(`relay_based_on_MX')
```
```

You can use the configuration in Listing 17.1 to define a custom *.mc file that you can name whatever you want. Though the options defined in this listing might appear rather confusing, it is easier to edit the generic *.mc file than to change the options in the generated sendmail.cf file. Many of these features are buried deep within the sendmail configuration file.