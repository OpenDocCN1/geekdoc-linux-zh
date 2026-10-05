file for the Red Hat configuration is found in the /usr/lib/sendmail-cf/cf subdirectory. It is pretty easy to locate. Among the generic files is one file simply named redhat.mc. This is the file we are looking for. Change to /usr/lib/sendmail-cf/cf and cat that file.

```
[craig]$$ cd /usr/lib/sendmail-cf/cf
[craig]$$ cat redhat.mc
divert(-1)
```

dnl This is the macro config file used to generate the dnl /etc/ sendmail.cf file. If you modify the file you will have to dnl regenerate /etc/sendmail.cf by running this macro config dnl through the macro preprocessor:

```
dnl m4 /etc/sendmail.mc > /etc/sendmail.cf
```

```
dnl You will need to have the sendmail-cf package installed for this to work.
include(`usr/lib/sendmail-cf/m4/cf.m4`)
VERSIONID(`linux setup for Red Hat Linux`)dnl
OSTYPE(`linux`)
define(`CONFDEF_USER_ID`,`8:12`)dnl
undefined(`UUCP_RELAY`)dnl
undefined(`BITNET_RELAY`)dnl
define(`CONFAUTO_REBUILD`)dnl
define(`CONFTO_CONNECT`,`1m`)dnl
define(`CONFTRY_NULL_MX_LIST`,`true`)dnl
define(`CONFDONT_PROBE_INTERFACES`,`true`)dnl
define(`PROCMAIL_MAILER_PATH`,`/usr/bin/procmail`)dnl
define(`ALIAS_FILE`,`/etc/aliases`)dnl
define(`UUCP_MAILER_MAX`,`2000000`)dnl
define(`CONFUSERDB_SPEC`,`/etc/mail/userdb.db`)dnl
dnl define(`CONFPRIVACY_FLAGS`,`authwarnings,nofrry,noexpn`**)dnl
dnl define(`CONFTO_QUEUEWARN`,`4h`)dnl
dnl define(`CONFTO_QUEUERTURN`,`5d`)dnl
```