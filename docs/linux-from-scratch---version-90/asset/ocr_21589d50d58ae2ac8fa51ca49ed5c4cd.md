```
;;

*)
echo "Usage: ${0} {start|stop|restart|status}"
  exit 1
  ;
esac

exit 0
```

# D.14./etc/rc.d/init.d/sysctl

```
#!/bin/sh
################################################################################
# Begin sysctl
#
# Description : File uses /etc/sysctl.conf to set kernel runtime parameters
# Authors : : Nathan Coulson (nathan@linuxfromscratch.org)
# Matthew Burgess (matthew@linuxfromscratch.org)
# DJ Lucas - dj@linuxfromscratch.org
# Update : : Bruce Dubbs - dbubbs@linuxfromscratch.org
# Version : LFS 7.0
################################################################################

### BEGIN INIT INFO
sysctl
# Provides:
# Required-Start: mountvirtfs
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start: S
# Default-Stop:
# Short-Description: Makes changes to the proc filesystem
# Description: Makes changes to the proc filesystem as defined in
etc/sysctl.conf. See 'man sysctl(8)'.
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```
. /lib/ls(l)/init-functions

case "$1" in
start)
  if [ -f "/etc/sysctl.conf" ]; then
    log_info_msg "Setting kernel runtime parameters..."
    sysctl -q p
    sysctl evaluate_retval
  fi
  ;;

status)
```