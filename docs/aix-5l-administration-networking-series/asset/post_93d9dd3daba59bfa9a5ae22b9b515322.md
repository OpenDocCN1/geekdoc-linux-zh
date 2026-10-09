
To enable the quota systems, execute the **quotaon** command. As part of the nightly system housekeeping, update the information in the quota files by running the **quotacheck** command. You can use the -a flag to indicate *all* quota filesystems. The following are quota update commands:

```bash
# quotaoff -a      <---- Turn quotas off for all filesystems
# quotacheck -a    <---- Updates quota information for all filesystems
# quotaon -a       <---- Turns quotas on for all filesystems
```

The quota limits for a user or a summary can be displayed using the **quota** and **repquota** commands, respectively, as shown here:

```bash
# quota ren
Disk quotas for user ren (uid 4084):
Filesystem blocks quota limit grace files quota limit grace
/home1 11836* 5120 6144 none 363 1000 2000
```

```bash
# repquota -u -a
User Block limits File limits
used soft hard grace used soft hard grace
root -- 31448 0 0 0 700 0 0
bin -- 57700 0 0 0 2037 0 0
sys -- 4 0 0 0 1 0 0
bi1bro -- 16 0 0 0 4 0 0
```

## USER ACCOUNT ACCESS RIGHTS

Who gets an account and how long can they keep it? Access and expiration policies might not seem like a big deal for small workgroups; however, the less ambiguity, the better. There are also legal implications that can be avoided if these policies are formalized and made public. Expiring and cleaning up accounts on large user base systems can be automated easily if expiration policies are clearly defined. AIX provides a mechanism for expiring accounts and performing the cleanup housekeeping. By providing both facilities, AIX allows you to implement grace periods between when an account expires and when it is actually removed from the system. This can be incorporated into a last-use policy.

## USER ACCOUNT ENVIRONMENT

What face will the system present to new users? As a Systems Administrator, you are charged with setting up the default environment for each new account. You want to maintain some level of control over environment parameters, yet you want to allow users the freedom of tailoring their own work space. Shells, editors, terminal definitions, and the like are religious issues best left to the faithful! You can't keep everyone from shooting themselves in the foot. You also don't want to open the floodgates to more shell environments than can support. You can provide a simple, modular login environment that simplifies recovery for the adventurous user when shell experimentation goes awry.

Begin by defining the default environment variables that will be set for all users. Environment variables are `name=value` pairs that are read by shells and commands to set values or determine behavior. For example, the environment variable EDITOR indicates what editor is to be invoked by applications. Environment variables may be command or shell specific, and they may be modified by the end user. See Table 20-1 for a list of some common environment variables.

To view the current values of environment variables, use echo or print and precede the variable name with a dollar sign, as shown here:

```bash
# echo $MANPATH
# print $MANPATH
```

### The /etc/environment and /etc/profile Files

AIX provides two files that are used to set default environment variables for the system. The /etc/environment file contains default variables set for each process by the `exec()` system call. The /etc/profile file contains the set of environment variables and commands that will be invoked when a user logs into the system. The contents of these files are read before local shell start-up files, and they are best kept non-shell-specific. The AIX-supplied /etc/environment and /etc/profile files provide a good base for tailoring your own defaults. See the default /etc/environment file here.

| Variable | Use |
| :--- | :--- |
| `PATH` | List of directory paths to search for commands and files |
| `LIBPATH` | List of library paths to search for binding |
| `MANPATH` | List of directory paths to search for man page files |
| `PAGER` | Default full-screen pager |
| `EDITOR` | Default editor |
| `TZ` | Time zone |
| `TERM` | Terminal type |
| `MAIL` | Incoming mail path |
| `MAILMSG` | Message text prompt when new mail arrives |
| `LANG` | Locale name in effect for NLS |
| `LOCPATH` | Directory containing locale file |
| `NLSPATH` | Full path to NLS catalogs |
| `USER` | User name |
| `LOGNAME` | User name |
| `HOME` | Home directory path |

Table 20-1. Common Environment Variables

### The Default System /etc/environment File

```bash
@(#)18                1.21 src/bos/etc/environment/environment, cmdsh, bos430, 9737A,430 5/13/94 15:09:03
# IBM_PROLOG_BEGIN_TAG
# This is an automatically generated prolog.
# bos430 src/bos/etc/environment/environment 1.21
# Licensed Materials - Property of IBM
# (C) COPYRIGHT International Business Machines Corp. 1989,1994
# All Rights Reserved
# US Government Users Restricted Rights - Use, duplication or
# disclosure restricted by GSA ADP Schedule Contract with IBM Corp.
# IBM_PROLOG_END_TAG
# COMPONENT_NAME: (CMDSH) Shell related commands
# ORIGINS: 27
# (C) COPYRIGHT International Business Machines Corp. 1989, 1994
# All Rights Reserved
# Licensed Materials - Property of IBM
# US Government Users Restricted Rights - Use, duplication or
# disclosure restricted by GSA ADP Schedule Contract with IBM Corp.
############################################################
# System wide environment file. This file should only contain
# 1. comment lines which have a # in the first column,
# 2. blank lines, and
# 3. Lines in the form name=value.
#
# WARNING: This file is only for establishing environment variables.
# Execution of commands from this file or any lines other than
# specified above may cause failure of the initialization process.
#
# Searching the current directory last is usually a BIG time saver.

# If /usr/ucb is at the beginning of the PATH the BSD version of
# commands will be found.

PATH=/usr/bin:/etc:/usr/sbin:/usr/ucb:/usr/bin/X11:/sbin:/usr/local/bin
TZ=EST5EDT
LANG=en_US
LOCPATH=/usr/lib/locale
NLSPATH=/usr/lib/locale/msg/$l:$N:/usr/lib/locale/msg/$l:AN.cat
LC_FASTMSG=true
MANPATH=/opt/freeware/man

# ODM routines use ODMDIR to determine which objects to operate on
# the default is /etc/objrepos - this is where the device objects
# reside, which are required for hardware configuration.
ODMDIR=/etc/objrepos
DOCUMENT_SERVER_MACHINE_NAME=saptst1
DOCUMENT_SERVER_PORT=80
CSI_DIRECTORY=/usr/HTTPServer/cgi-bin
DOCUMENT_DIRECTORY=/usr/HTTPServer/htdocs
DEFAULT_BROWSER=netscape
# IMNSearch DBCS environment variables
IMQCONFIGSV=/etc/IMNSearch
IMQCONFIGCLI=/etc/IMNSearch/dbcs/help
ITECONFIGSV=/etc/IMNSearch/clients
ITECONFIGCLI=/etc/IMNSearch/clients
ITE_DOC_SEARCH_INSTANCE=search
```

### The Default /etc/profile File

```bash
# @(#)27  1.20 src/bos/etc/profile/profile, cmdsh, bos430, 977A4_A30 8/9/94
# 12:01:38
# IBM_PROLOG_BEGIN_TAG
# This is an automatically generated prolog.
#
# bos430 src/bos/etc/profile/profile 1.20
#
# Licensed Materials - Property of IBM
#
# (C) COPYRIGHT International Business Machines Corp. 1989,1994
# All Rights Reserved
#
# US Government Users Restricted Rights - Use, duplication or
# disclosure restricted by GSA ADP Schedule Contract with IBM Corp.
#
# IBM_PROLOG_END_TAG
# COMPONENT_NAME: (CMDSH) Shell related commands
#
# FUNCTIONS:
#
# ORIGINS: 3, 26, 27
#
# (C) COPYRIGHT International Business Machines Corp. 1989, 1994
# All Rights Reserved
# Licensed Materials - Property of IBM
#
# US Government Users Restricted Rights - Use, duplication or
# disclosure restricted by GSA ADP Schedule Contract with IBM Corp.
#
###############################################################
#
# System wide profile. All variables set here may be overridden by
# a user's personal .profile file in their HOME directory. However,
# all commands here will be executed at login regardless.

trap "" 1 2 3
readonly LOGNAME

# Automatic logout, include in export line if uncommented
# TMOUT=120

# System Added Path
PATH=$PATH:/usr/local/sbin:/usr/local/netscape

# The MAILMSG will be printed by the shell every MAILCHECK seconds
# (default 600) if there is mail in the MAIL system mailbox.
MAIL=/usr/spool/mail/$LOGNAME
MAILMSG="YOU HAVE NEW MAIL"

# If termdef command returns terminal type (i.e. a non NULL value),
# set TERM to the returned value, else set TERM to default lft.
TERM_DEFAULT=lft
TERM=`termdef`
TERM=${TERM:-$TERM_DEFAULT}

# If LC_MESSAGES is set to "C$lft" and TERM is not set to "lft",
# unset LC_MESSAGES.
if [ "$LC_MESSAGES" = "C$lft" -a "$TERM" != "lft" ] then
        unset LC_MESSAGES
fi

export LOGNAME MAIL MAILMSG TERM
trap 1 2 3
```

### The /etc/security/environment File

Individual user environment variables may also be defined in the /etc/security/environment file. This file contains a stanza for each user in the system, identified by user
