/etc/rsyslog.conf. If you are not already root, boot root and then open the /etc/rsyslog.conf file in a text editor (such as vi). You should see something similar to this:

```
#rsyslog v3 config file

# if you experience problems, check
# http://www.rsyslog.com/troubleshoot ####

#### MODULES ####

$ModLoad inuxsock.so # provides support for local system logging (e.g. via logger command)
$ModLoad inklog.so # provides kernel logging support (previously done by rklogd)
##ModLoad innark.so # provides --MARK-- message capability

# Provides UDP syslog reception
$ModLoad impd.so
$UDPServerRun 514

# Provides TCP syslog reception
$ModLoad itcp.so
$InputTCPServerRun 514
```

```
#### GLOBAL DIRECTIVES ####

# Use default timestamp format
$ActionFileDefault RSYSLOG_TraditionalFile

# File syncing capability is disabled by default.
# This feature is usually not required,
# not useful and an extreme performance hit
$ActionFileEnableSync on
```

```
#### RULES ####

# Log all kernel messages to the console.
# Logging much else clutters the screen.
#kern.* /dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info:mail.none:authpriv.none:cron.none /var/log/messages
```

```
# The authpriv file has restricted access.
authpriv.* /var/log/secure
```