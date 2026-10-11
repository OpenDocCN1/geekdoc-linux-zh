
# Linux 管理手册

### 应该在 /Build 中执行，必须在 `divert(0)` 之后执行
`include(/usr/share/sendmail/m4/cf.m4')`
`divert(0)`

`VERSIONID(@#)Setup for SuSE Linux 8.11.0-4 (SuSE Linux) 04/09/2000)`
`OSTYPE(su-linux)`
`FEATURE(always_add_domain)`
`MAILER(local)`
`MAILER(smtp)`
`MAILER(procmail)`
`MAILER(uuc)`
`MAILER(bsmtp)`
`MAILER(fido)`
`DOMAIN(generic)`
`LOCAL_CONFIG` ### 无用，无任何作用

这里是 `linux.nullclient.mc`；你必须将 `mailhub.domain.notused` 替换为实际邮件枢纽机器的名称。我们删除了行末的 `dnl` 以使示例更易读。

`divert(-1)`
# Copyright (c) 1999 SuSE GmbH Nuernberg, Germany.
# Author: Werner Fink <werner@suse.de>

# 这是一个特殊情况——它创建了一个精简的配置文件
# 该文件仅包含支持通过本地基于 SMTP 的网络
# 将所有邮件转发到中心枢纽的功能。参数是
# 该枢纽的名称。

### 应该在 /Build 中执行，必须在 `divert(0)` 之后执行
`include(/usr/share/sendmail/m4/cf.m4')`
`divert(0)`

`VERSIONID(@#)Setup for SuSE Linux 8.11.0-2 (SuSE Linux) 28/03/2000)`
`OSTYPE(su-linux)`
`FEATURE(nullclient, 'mailhub.domain.notused')`
`FEATURE(noconifying)`
`LOCAL_CONFIG` ### 无用

`OSTYPE` 文件通常大约 10 行，并包含各种程序的路径，这些位置取决于操作系统。SuSE Linux 做得有些过头；我们再次对不寻常的行添加了以 ### 开头的注释。单行 `OSTYPE('su-linux')` 会导致以下文件被包含在这些简单配置中：

`divert(-1)`
# Copyright (c) 1999, 2000 SuSE GmbH Nuernberg, Germany.
# Author: Werner Fink <werner@suse.de>

`VERSIONID(@#) suse-linux.m4 8.11.1-0 (SuSE Linux) 22/11/2000)`
`define(confCF_VERSION, 'SuSE Linux 8.11.1-0.5')`

```
define(confDEF_USER_ID, 'daemon:daemon')
```

else 使用 daemon 的 uid/gid

# 第 19 章

# 电子邮件

# 585

```
define(confCOPY_ERRORS_TO, 'Postmaster')
define(UUCP_MAILER_MAX, '200000')
define(confMAX_MIME_HEADER_LENGTH, '356/128')
define(confMAX_HEADERS_LA, '32768') ### 默认
define(confQUEUE_LA, '12')
define(confREFUSE_LA, '18')
define(MAX_DAEMON_CHILDREN, '30')
define(confTOCONNECT, '30s')
dnl 许多系统管理员禁用了 IDENT
define(confTO_IDENT, 'us')
dnl 我们是否应该将 accepts 设置为 as dsn?
define(confPRIVACY_FLAGS, 'warnings,needmailhe,novfry,noexpn,noverb')
define(confTRUSTED_USERS, 'mdm wroot ucp daemon)
define(confN0_RCP_ACTION, 'add-to-undisclosed')
dnl 注意：RFC1891 虽然是这么说的，但经常被误用
define(confFRRT_IMPLIES_DSN, 'True')
FEATURE('allows_add_domain')
```

```
define(PROCMAL_MAILER_PATH, '/usr/bin/procmail')
define(PROCMAL_MAILER_ARGS, 'procmail -m $h $f $')
FEATURE('local,procmail')
define(local_SHELL_FLAGS, 'u09')
define(local_MAILER_ARGS, 'procmail -a $h $d')
define(local_MAILER_FLAGS, 'Spfhn09')
define(USENET_MAILER_PATH, '/usr/bin/inews')
```

```
define(DATABASE_MAP_TYPE, '/usr/lib/sendmail') ### 默认
define(confSETTINGS_DIR, '/etc/mail/') ### 默认
define(confDEADLETTER_DROP, '/var/log/dead.letter')
```

```
syscmd(test -f /etc/SUSE-release)
elife(sysval, 0)
define(STATUS_FILE, '/var/var/log/sendmail.st') ### 默认
define(QUEUE_DIR, '/var/spool/mqueue')
define(STATUS_FILE, '/etc/mail/sendmail.st') ### 文件的旧名
define(QUEUE_DIR, '/var/mqueue')
```

```
define(confHOST_STATUS_DIRECTORY, 'hotstat')
- define(HELP_FILE, SMILIBDIR/helpfile)
- define(ALIAS_FILE, '/etc/aliases') ### 默认
define(confHOSTS_FILE, '/etc/hosts') ### ###
define(confCT_FILE, '/etc/mail/sendmail.st') ### ###
```

# Linux 管理手册

```
divert(0)
VERSIONID(@)#sendmail.mc    8.9.3-21 (Debian) 20000309')
OSTYPE(debian)
LOCAL_CONFIG                   ### doesn't belong in the middle of an mc file
FEATURE(masquerade_envelope)
FEATURE(always_add_domain)      ### should be at the end under LOCAL_CONFIG
Cwappie toadbranch.com
FEATURE(cw_file)
FEATURE(use_ct_file)
FEATURE(noucp)
FEATURE(smrsh, /usr/lib/sm.bin/smrsh')### doesn't belong
MAILER_DEFINITIONS
MAILER(local)
MAILER(smtp)
LOCAL_CONFIG
MASQUERADE_AS(lappie.toadranch.com) ### should be above MAILERS
```

## 下方为自定义配置（将保留）
