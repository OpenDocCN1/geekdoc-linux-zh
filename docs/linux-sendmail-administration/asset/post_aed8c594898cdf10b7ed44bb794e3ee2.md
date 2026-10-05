
# Table 5.1 Mailer Configuration Variables (continued)

| Variable | Purpose |
|---|---|
| LOCAL_MAILER_PATH | Local mail delivery program. |
| LOCAL_SHELL_ARGS | Arguments for prog mail. |
| LOCAL_SHELL_DIR | Directory in which the shell should run. |
| LOCAL_SHELL_FLAGS | Flags added to IsDFM for the mailer. |
| LOCAL_SHELL_PATH | Shell used to deliver e-mail. |
| RELAY_MAILER_ARGS | Relay mailer arguments. |
| RELAY_MAILER_FLAGS | Flags added to “nDFMuX” for the relay mailer. |
| RELAY_MAILER_MAXMSG | Maximum number of messages for the relay delivered by a single connection. |
| SMTP8_MAILER_ARGS | smtp mailer arguments. |
| SMTP_MAILER_ARGS | smtp mailer arguments. |
| SMTP_MAILER_CHARSET | Character set for SMTP 8-bit MIME mail. |
| SMTP_MAILER_FLAGS | Flags added to “nDFMuX” for all SMTP mailers. |
| SMTP_MAILER_MAX | Maximum size of messages for all SMTP mailers. |
| SMTP_MAILIL_MAXMSG | Maximum number of SMTP messages delivered by a single connection. |

It is very unlikely that you will need to change a mailer setting. But if you do, use the appropriate variable. Don't directly edit the MAILER source files. For example, if you want to limit the size of messages handled by the SMTP mailers to 2,000,000 bytes, you could add the following define to your configuration:

```
define(`SMTP_MAILER_MAX`, `2000000`)
```

Variable definitions, like those shown in Table 5.1, are available for all mailers. See the “OSTYPE” section of Appendix A for a complete list of these variables.

## Chapter 5 Understanding a Vendor's Configuration

> **NOTE** Appendix A lists these variables in the discussion of the OSTYPE file that is where mailer and path information is supposed to be stored. However, most Sendmail administrators don't want to take it upon themselves to create their own OSTYPE file. Most administrators add commands like these directly to the macro configuration file.

The linux.m4 OSTYPE file shown in Listing 5.2 tweaked the macro path setting for PROCMAIL_MAILER_PATH. That is the only mailer setting touched by the generic-linux.mc configuration, and it is indicative of how rarely mailer settings need to be changed.

The analysis of the generic-linux.mc has shown several things. We have discovered the interrelationships of the various m4 source files and we have learned the purpose and syntax of several different configuration commands. Also, we discovered that the generic-linux.cf file developed with the Sendmail 8.11 source distribution works fine for our sample Linux system once the various files required by Sendmail are placed in the correct directories under the correct names.

Next we analyze the Sendmail configuration that was installed as part of the RPM package on our sample Red Hat system. That configuration worked fine from the start. The analysis of the Red Hat configuration is not to debug a problem: it is to learn about the configuration provided by the vendor and to see what we can do to improve it.

## The Red Hat Configuration

In Chapter 3, “Running Sendmail,” 8.11 was installed on a sample Red Hat system using the rpm command. Three RPM packages were installed in this way: the documentation, the configuration files, and the Sendmail program. The Sendmail configuration file examined in this section is the file that was installed as part of sendmail-cf-8.11.0-1386.rpm.

The RPM package creates a directory structure in /usr/lib/sendmail-cf that is very similar to the cf directory structure from the Sendmail source distribution. An ls of /usr/lib/sendmail-cf shows the following directories:

```
$craig]$ ls /usr/lib/sendmail-cf
```

README cf feature hack m4 mailer ostype sh siteconfig

This directory contains the same cf, m4, ostype, feature, mailer, and domain subdirectories we saw in Chapter 4, and they perform the same functions. The macro control file for the Red Hat configuration is found in the /usr/lib/sendmail-cf/cf subdirectory. It is pretty easy to locate. Among the generic files is one file simply named redhat.mc. This is the file we are looking for. Change to /usr/lib/sendmail-cf/cf and cat that file.

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
define(`CONFTRY_NULL_LIST`,`true`)dnl
define(`CONFONT_PROBE_INTERFACES`,`true`)dnl
define(`PROCMAIL_MAILER_PATH`,`/usr/bin/procmail`)dnl
define(`ALIAS_FILE`,`/etc/aliases`)dnl
define(`UUCP_MAILER_MAX`,`2000000`)dnl
define(`CONFUSERDB_SPEC`,`/etc/mail/userdb.db`)dnl
define(`CONFPRIVACY_FLAGS`,`authwarnings,noexpn`)dnl
define(`CONFTO_QUEUE`,`4h`)dnl
define(`CONFTO_QUEUE`,`5d`)dnl
```

## Chapter 5 Understanding's Configuration

```
dnl define(`CONFQUEUE_LA`, `2`)dnl
dnl define(`CONFUSE_LA`, `8`)dnl
FEATURE(`smush`,`usr/sbin/smush`)dnl
FEATURE(`mailertable`,`hash -o /etc/mail/mailertable`)dnl
FEATURE(`virtertable`,`hash -o /etc/mail/virtertable`)dnl
FEATURE(`redirect`)dnl
FEATURE(`always_domain`)dnl
FEATURE(`cw_file`)dnl
FEATURE(`local_db`)dnl
FEATURE(`access_db`)dnl
FEATURE(`blacklist_recipients`)dnl
dnl We strongly recommend to comment this out if you want to protect yourself from spam. However, the laptop and users on do not have DNS need this.
FEATURE(`accept_unresolvable_domains`)dnl
dnl FEATURE(`relay_based_MX`)dnl
MAILER(smtp)dnl
MAILER(procmail)dnl
```

Wow! This is one of the largest files I have ever seen! The first thing we need to cut this monster down to size and attack it piecemeal. One thing we can do eliminate the comments. Every line that begins with dnl is a comment that can be ignored for this.

```
[craig]$ grep -v '^' redhat.mc
divert(-1)
include(`../m4/cf.m4`)
VERSIONID(`linux setup for Red Hat Linux`)
OSTYPE(`linux`)
define(`confDEF_USER_ID`,`8:12`)dnl
undef(`_UCP_RELAY`)dnl
define(`BITNET_RELAY`)dnl
define(`confAUTO_REBUILD`)dnl
define(`confTO_CONNECT`,`1m`)dnl
define(`confTRY_NULL_LIST`,true)dnl
```

```
define(`PROCMAIL_MAILER_PATH`,`/usr/bin/procmail`)dnl
define(`ALIAS_FILE`,`/etc/aliases`)dnl
define(`STATUS_FILE`,`/var/log/sendmail.st`)dnl
define(`UOCP_MAILER_MAX`,`2000000`)dnl
define(`CONFUSERDB_SPEC`,`/etc/mail/userdb.db`)dnl
FEATURE(`smush`,`usr/bin/smush`)dnl
FEATURE(`mailertable`,`hash -o /etc/mail/mailertable`)dnl
FEATURE(`virtertable`,`hash -o /etc/mail/virtertable`)dnl
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

![](img/b8082498451dba2bf0cf2907c85c4c83_145_0.png)

Okay, it is surprisingly large, but it is not as bad as it looks. We have already covered many of the lines in this file and don't need to cover them again. divert were covered in Chapter 4. We know the VERSIONED mode and can ignore it. The OSTYPE(`linux`) marco is the same one covered earlier in this chapter, and during discussion of the linux.m4 file we covered PROCMAIL_PATH and FEATURE(local_procmail). We also covered FEATURE(`redirect`), FEATURE(use_cw_file), and MAILER(`smtp`) during discussion of the generic-linux.mc configuration. We've made a good start. Still, there are leafs of commands to discuss.

## Understanding Defines and Undefines

The first new command in this configuration is a command that overrides the default setting of confDEF_USER_ID, which holds the user ID and group ID used by Sendmail. By defaultDEF_USER_ID is set to 1:1, which on a Red Hat system is user bin and group bin. In the redhat.mc configuration file this is changed to 8:12, which is user mail and group mail. Having a specific user ID and group ID for Sendmail is a good idea. The bin user can be used for a variety of programs. Creating a specific mail user and group makes it easier to track actions back to Sendmail and to control the access Sendmail is given to the rest of the system.

The next two lines are undefined commands that clear the names of the relay servers from the UOCP_RELAY and the BITNET_RELAY variables. Clearing these variables means that all UOCP sites must be directly connected and that the .BITNET pseudo-domain will not
