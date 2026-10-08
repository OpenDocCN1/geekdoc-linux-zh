# 190

# crontab

# Files

/var/ld/ld.config
Default configuration file for 32-bit applications.

/var/ld/64/ld.config
Default configuration file for 64-bit applications.

/var/tmp
Default location for temporary configuration file (see tempnam(3C)).

/usr/lib/ldstub
Stub application employed by ldd(3DL) 32-bit objects.

/usr/lib/64/ldstub
Stub application employed by ldd(3DL) 64-bit objects.

/usr/lib/libcrl.so.1
Audit library employed by ldd(3DL) 32-bit objects.

/usr/lib/64/libcle.so.1
Audit library employed by ldd(3DL) 64-bit objects.

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWfoo |

# See Also

ld(1), ld.so.1(1), ldd(3DL), tempnam(3C), threads(3THR), attributes(5).

# crontab — User Chronological Table File

# Synopsis

/usr/bin/crontab [filename]
/usr/bin/crontab [-elr] username

# Description

Use the crontab command to manage a user's access with cron by copying, creating, listing, and removing crontab files. If invoked without options, crontab copies the specified file, or the standard input if no file is specified, into a directory that holds all users' crontabs.

# crontab Access Control

User access to cron is allowed:

+   * If the user's name appears in /etc/cron.d/cron.allow.