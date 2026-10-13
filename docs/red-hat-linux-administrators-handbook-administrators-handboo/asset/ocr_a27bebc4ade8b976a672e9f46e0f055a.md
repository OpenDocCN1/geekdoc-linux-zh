shows the following output:

```
Configuring for Apache, Version 1.3.91.3.9

Installation paths:
prefix: /usr/local/apache
exec_prefix: /usr/local/apache
bindir: /usr/local/apache/bin
sbindir: /usr/local/apache/bin
libexecdir: /usr/local/apache/libexec
mandir: /usr/local/apache/man
sysconfdir: /usr/local/apache/etc
datadir: /usr/local/apache/share
includedir: /usr/local/apache/include
localstatedir: /usr/local/apache/var
rundir: /usr/local/apache/var/run
logfiledir: /usr/local/apache/var/log
proxycachedir: /usr/local/apache/var/proxy

Compilation paths:
HTTPD_ROOT: /usr/local/apache
SUEEXEC_BIN: /usr/local/apache/sbin/suexec
SHARED_CORE_DIR: /usr/local/apache/libexec
DEFAULT_PIDLOG: var/run/httpd.pid
DEFAULT_SCOREBOARD: var/run/httpd.scoreboard
DEFAULT_LOCKFILE: var/run/httpd.lock
DEFAULT_XFERLOG: var/log/access_log
DEFAULT_ERRORLOG: var/log/error_log
TYPES_CONFIG_FILE: etc/mime.types
SERVER_CONFIG_FILE: etc/httpd.conf
ACCESS_CONFIG_FILE: etc/access.conf
RESOURCE_CONFIG_FILE: etc/srm.conf
```

The --layout option allows you to verify the directory structure before it is actually used. If you are upgrading Apache from 1.2 and want to keep the