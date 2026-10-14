
- Change the configuration files as needed. This can be done using an editor of your choice.
- Execute `/sbin/SuSEconfig` to make the changes take effect. If you have changed `/etc/rc.config` via YaST2, this is done automatically.
- Bring your system back to the previous runlevel.

```
root@earth:   > init 3
```

This procedure is mainly relevant if you have changed system-wide settings (such as network configuration). It is not necessary to go into single user mode for small changes, but it ensures all relevant programs are correctly restarted.

> **Tip**
> 
> To disable the automatic configuration of SuSEconfig, set the variable `{ENABLE_SUSECONFIG}` in `/etc/sysconfig/suseconfig` to no. Do not disable SuSEConfig if you want to use the SuSE installation support. It is also possible to disable the autoconfiguration partially.

## System Configuration: Scripts and Variables

In this section, we describe a selection of system parameters, including their default settings. If you do not use YaST2 to change `/etc/rc.config` or the configuration files in `/etc/sysconfig`, make sure you set empty parameters as two quotation marks (e.g. `KEYTABLES=""`) and that you surround parameters that contain a blank with quotation marks. Parameters consisting of only one word do not have to be quoted.

### Basic Settings in /etc/rc.config

```
PATH="/sbin:/bin:/usr/sbin:/usr/bin"
```

This variable is only used internally. Do not change it.

```
CHECK_PERMISSIONS="set"
```

defines whether file permissions will be checked against the `/etc/permissions` file. With set, wrong settings will be corrected. With warn, only “warnings” will be issued. With no, the feature is disabled.

```
PERMISSION_SECURITY="easy local"
```

In /etc/permissions.paranoid, /etc/permissions.secure, and /etc/permissions.easy, three security levels are predefined. Enter easy, secure or paranoid. If you select paranoid, some system services might not be available anymore. Explicitly enable them if needed.

To define your own settings, create, for example, a file /etc/permissions.local then set the variable to local.

> **Note**
> 
> If you define your own /etc/permissions.local, make sure your settings do not conflict with the rotation mechanism (package logrotate). logrotate overwrites the settings in /etc/permissions.local. See Section *Log Files — the Package logrotate* on page 273.

```
HALT_SOUND="no"
```

Set to yes or quint to play a quint tone sequence at system halt or reboot or set to octave to play octave sound.

```
CHECK_INITTAB="yes"
```

SuSEconfig can do some modifications to /etc/inittab. If you do not want this, set this variable to no.

```
CONSOLE_SHUTDOWN="reboot"
```

This variable determines how [Ctrl] + [Alt] + [Del] is handled by the init process. CHECK_INITTAB has to be set to yes to activate this feature. Possible settings are ignore, reboot, or halt. Default is reboot.

```
DVB_SOUND_CHIP="ti"
```

Choose the sound chip on DVB card — ti or crystal

```
START_FRONTBASE="no"
```

Start the FrontBase and the FrontBase web service?

```
IRCSERVER="sun.cosmos.com"
```

Specify a space-separated list of IRC servers (*Internet Relay Chat*).

```
SECCHK_USER="root"
```

This variable determines to which e-mail address the reports from the security check scripts are sent. Default is root.

```
START_SECCHK="yes"
```

This variable controls whether the security check scripts should be run automatically every night, week, or month. Set to no to disable.

```
KERNEL_LOGLEVEL="1"
```

Default log level for klogd.

```
SYSLOGD_PARAMS=""
```

Parameters for syslogd, e.g., "-r = my.dom.ain".

```
LOAD_MEMSTAT_MODULE="no"
```

Enable this to load the memstat kernel module for xosview automatically at boot time.

### Settings for the files in /etc/sysconfig

**suseconfig** – Settings for SuSEconfig.

```
ENABLE_SUSECONFIG="yes"
```

Decide whether SuSEconfig should take care of updating the configurations. Do not disable SuSEconfig if you want to consult our Installation Support.

```
MAIL_REPORTS_TO="root"
```

Select the user to which SuSEconfig should send e-mail reports created during the automatic system administration.

```
MAIL_LEVEL="warn"
```

Set the variable to warn if only important messages should be sent. Set it to all if the log files should be mailed, too.

```
CREATE_INFO_DIR="yes"
```

Set the variable to yes if a perl script should be used to generate the file /usr/share/info/dir automatically. This file is the index for all info pages.

```
CREATE_JAVALINK="yes"
```

SuSEconfig can automatically create the links /usr/lib/java and /usr/lib/jre that point to a suitable JDK or JRE respectively if you set this variable to yes.

```
CREATE_PERLLOCAL_POD="yes"
```

May SuSEconfig modify your perllocal.pod?

```
UPDATE_GROFF_CONF="yes"
```

Update DESC to get page sizes correct?

```
GROFF_PAGESIZE=""
```

If the correct page size cannot be found in your printcap this variable can be set to the following values: letter, legal, a4, or b5, supported by both groff and ghostscript.

**CHECK_ETC_HOSTS="yes"**  
Defines whether SuSEconfig should check and modify `/etc/hosts`.

**BEAUTIFY_ETC_HOSTS="no"**  
Should `/etc/hosts` be sorted by SuSEconfig?

**SORT_PASSWD_BY_UID="no"**  
If this variable is set to yes, SuSEConfig sorts your `/etc/passwd` and `/etc/group` by “uid” and “gid”.

**CWD_IN_ROOT_PATH="no"**  
Should the current working directory (“.”) be in the path of user root?  
For security reasons, this setting is not recommended. This setting is valid for all users with a “UID” below 100 (system users).

**CWD_IN_USER_PATH="yes"**  
Should the current working directory (“.”) be in the path for normal users?

**onlineupdate** – Settings for YaST2 Online Update.

**YAST2_LOADFTPSERVER="yes"**  
When starting you (YaST2 Online Update), should the default FTP server list be updated via a call from wget to `www.suse.de`? This list is stored under `/etc/suseservers`. Set the variable to no if you do not want to reload the FTP server list.

**autoinstall** – AutoInst of YaST2.

**REPOSITORY="/var/lib/autoinstall/repository"**  
Repository with all profiles

**SuSEDir=""**  
SuSE Directory

**CLASS_DIR="/var/lib/autoinstall/classes"**  
Classes

**USE_CLASSES="no"**  
Use classes?

**autofs** – With this daemon, it is possible to mount directories accessible via NFS or local directories (CD-ROM drives, disk drives, etc.) automatically. The package `nfs` or `series n` must be installed and configured.

**AUTOFS_OPTIONS=""**  
autofs daemon options, e.g. `"--timeout 60"`.

**susehelp** – SuSE help system.

```
DOC_HOST=""
```

If a global documentation server should be used for the SuSE help system, enter the name of the server here, for example, "sun.cosmos.com".

```
DOC_SERVER="no"
```

On the documentation server, this variable must be set to yes so, depending on the settings in DOC_ALLOW, access will be granted to http-man and the index files for the HTTP server will be modified accordingly. They will point to the documentation server instead of http://localhost.

```
DOC_ALLOW="LOCAL"
```

List of hosts and domains as a pattern for /etc/hosts.allow, which should have access to the documentation server. This variable will only be read if DOC_SERVER is set to yes. A subdomain can also be listed here (e.g., with "*.cosmos.com").

### language — Settings for language and locale

```
DEFAULT_LANGUAGE="english"
```

This variable is set by YaST automatically if you change the language settings in the control center. This value is used as a fallback if RC_LANG is not set. The value is passed on through the file /usr/share/locale/locale.alias.

```
RC_LANG="en_US"
```

Sets variable LANG for locale. This is the default for local users, as long as no RC_LC_* variables are used. The respective sysconfig variables are: RC_LC_ALL (overwrites LC_* and LANG!), RC_LC_MESSAGES, RC_LC_CTYPE, RC_LC_MONETARY, RC_LC_NUMERIC, RC_LC_TIME, and RC_LC_COLLATE.

See Section *Local Adjustments — I18N/L10N* on page 292.

```
ROOT_USES_LANG="no"
```

Should locale settings be used for root?

### mail — Settings for e-mail.

```
FROM_HEADER=""
```

From: line defined for the whole system. If empty "", FQDN is used. See Section *Domain Name System* on page 330.

```
MAIL_CREATE_CONFIG="yes"
```

Set this to no if SuSEconfig should not generate the configuration files (e.g., you want to generate your /etc/sendmail.cf yourself). If you want to generate a sendmail configuration /etc/sendmail.cf from parameters given in /etc/sysconfig/sendmail, use yes.
