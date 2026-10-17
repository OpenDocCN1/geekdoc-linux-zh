
### 列表 11-1 默认的 `/etc/smb.conf` 文件

```
# This is the main Samba configuration file.
# You should read the smb.conf(5) manual page
# in order to understand the options listed here.
# Samba has a huge number of configurable options
# (perhaps too many!) most of which are not shown
# in this example
#
# Any line which starts with a ; (semi-colon) or
# a # (hash) is a comment and is ignored. In this
# example we will use a '#' for commentary and a ';'
# for parts of the config file that you may wish to
# enable
#
# NOTE: Whenever you modify this file you should
# run the command "testparm" to check that you have
# not made any basic syntactical errors.
#
#====== Global Settings ==============

[global]

# workgroup = NT-Domain-Name or Workgroup-Name
workgroup = MYGROUP

# server string is the equivalent of the NT
# Description field
server string = Samba Server
```

```
# This option is important for security. It allows
# you to restrict connections to machines which are on
# your local network. The following example restricts
# access to two C class networks and the "loopback"
# interface. For more examples of the syntax see
# the smb.conf man page
; hosts allow = 192.168.1. 192.168.2. 127.

# If you want to automatically load your printer
# list rather than setting them up individually
# then you'll need this
printcap name = /etc/printcap
load printers = yes

# It should not be necessary to spell out the
# print system type unless yours is non-standard.
# Currently supported print systems include:
# bsd, sysv, plp, lprng, aix, hpux, qnx
; printing = bsd

# Uncomment this if you want a guest account, you
# must add this to /etc/passwd
# otherwise the user "nobody" is used
; guest account = pcguest

# This tells Samba to use a separate log file for
# each machine
# that connects
log file = /var/log/samba/log.%m

# Put a capping on the size of the log files (in Kb).
max log size = 50

# Security mode. Most people will want user
```

### 列表 11-1 继续

```
# level security. See
# security_level.txt for details.
    security = user
# Use password server option only with
# security = server
;   password server = <NT-Server-Name>

# Password Level allows matching of _n_
# characters of the password for
# all combinations of upper and lower case.
; password level = 8
; username level = 8

# You may wish to use password encryption. Please read
# ENCRYPTION.txt, Win95.txt and WinNT.txt
# in the Samba documentation.
# Do not enable this option unless you have
# read those documents
; encrypt passwords = yes
; smb passwd file = /etc/smbpasswd

# Unix users can map to different SMB User names
;   username map = /etc/smbusers

# Using the following line enables you to
# customize your configuration
# on a per machine basis. The %m gets replaced
# with the netbios name of the machine that is
# connecting
;   include = /etc/smb.conf.%m

# Most people will find that this option gives
# better performance. See speed.txt and the manual
# pages for details
```
