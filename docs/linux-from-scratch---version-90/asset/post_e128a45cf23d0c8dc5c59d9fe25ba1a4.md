
```bash
*)
  echo "Usage: ${0} {start|stop}"
  exit 1
;;
sac
esac

exit 0

# D.8. /etc/rc.d/init.d/checkfs

```bash
#!/bin/sh
####################################################################################
# Begin checkfs
# Description : File System Check
# Authors : Gerard Beekmans - gerard@linuxfromscratch.com
       A. Luecke - luecke@users.sourceforge.net
       DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs - bdubbs@linuxfromscratch.org
# Version : LFS 7.0
# Based on checkfs script for LFS-3.1 and earlier.
# From man fsck
# 0 - No errors
# 1 - File system errors corrected
# 2 - System should be rebooted
# 4 - File system errors left uncorrected
# 8 - Operational error
# 16 - Usage or syntax error
# 32 - Fck canceled by user error
# 128 - Shared library error
####################################################################################

### BEGIN INIT INFO
# Provides : checkfs
# Required-Start: udev swap $time
# Should-Start: 
# Required-Stop: 
# Should-Stop: 
# Default-Start: S
# Default-Stop: 
# Short-Description: Checks local filesystems before mounting.
# Description: Checks local filesystems before mounting.
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
. /lib/lsb/init-functions

case "${1}" in
start)
  if [ -f /fastboot ]; then
    msg="$fastboot found, will omit file system checks as requested.\n"
    log_info_msg "${msg}"
    exit 0
  fi

  log_info_msg "Mounting file system in read-only-mode..."
  mount -n -o remont,ro / /dev/null

  if [ ($?) -ne 0 ]; then
    log_failure_msg="\nCannot check root"
    msg="${msg}filesystem because it could not be mounted"
    msg="${msg}in read-only mode.\n\n"
    msg="${msg}After you press Enter, this system will be"
    msg="${msg}halted and powered off.\n\n"
    log_failure_msg="${msg}"
  fi

  log_info_msg "Press Enter to continue..."
  wait_for_user
  /etc/rc.d/init.halt stop
  else
    log_success_msg2
  fi

  if [ -f /forceck ]; then
    msg="$forceck found, forcing file system checks as requested."
    log_success_msg "${msg}"
    options="-f"
  else
    options=""
  fi

  log_info_msg "Checking file system..."
  # Note: -a option used to be -p; but this fails e.g. on fsck.minix
  if is_true VERBOSE_FSCK; then
    fsck ${options} -a -A -C -T
  else
    fsck ${options} -a -A -C -T >/dev/null
  fi

  error_value=$?

  if [ "${error_value}" = 0 ]; then
    log_success_msg2
  fi

  if [ "${error_value}" = 1 ]; then
    msg="\nWARNING:\nfile system errors"
    msg="${msg}were found and have been corrected.\n"
    msg="${msg}    You may want to double-check that"
    msg="${msg}everything was fixed properly."
    log_warning_msg "${msg}"
  fi

  if [ "${error_value}" = 2 ] || [ "${error_value}" = 3 ]; then
    msg="\nWARNING:\nnFile system errors"
    msg="${msg}were found and have been "
    msg="${msg}corrected, but the value of "
    msg="${msg}require this system to be rebooted.\nn\n"
    msg="${msg}After you press enter, "
    msg="${msg}this system will be rebooted\n\n"
    log_failure_msg="${msg}"
    log_info_msg "Press Enter to continue..."
    wait_for_user
    boot -f
  fi

  if [ "${error_value}" -gt 3 -a "${error_value}" -lt 16 ]; then
    msg="FAILURE:\nFile system errors"
    msg="${msg}were encountered that could not be "
    msg="${msg}fixed automatically.\nThis system "
    msg="${msg}cannot continue to boot and will "
    msg="${msg}therefore be halted until those "
    msg="${msg}errors are fixed manually by a "
    msg="${msg}System Administrator.\n\n"
    msg="${msg}After you press Enter, this system will be "
    msg="${msg}halted and powered off.\n\n"
    log_failure_msg="${msg}"
    log_info_msg "Press Enter to continue..."
    wait_for_user
    /etc/rc.d/init.d halt stop
  fi

  if [ "${error_value}" -ge 16 ]; then
    msg="FAILURE:\nnUnexpected failure "
    msg="${msg}running fsck. Exited with error "
    msg="${msg}code: ${error_value}.\n\n"
    log_info_msg ${msg}
    exit ${error_value}
  fi

  exit 0
  ;;
  *)
    echo "Usage: $(0) (start)"
    exit 1
  ;;
esac
```
# Endchecks

# D.9. /etc/rc.d/init.d/mountfs

```bash
#!/bin/sh
######################################################
# Begin mounts
#
# Description : File System Mount Script
# Linux From Scratch - Version 9.0
# Authors Gerard Beekmans - gerard@linuxfromscratch.org
# DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs - bdubdims@linuxfromscratch.org
# Version : LFS 7.0

### BEGIN INIT INFO $local_fs
# Provides $udev checks
# Required-Start:
# Should-Start: swap
# Required-Stop:
# Should-Stop: S
# Default-Start: 0
# Default-stop:
# Short-Description: Mounts/unmounts filesystems defined in /etc/fstab. Remount root filesystem read/write and mounts all remaining local filesystems defined in /etc/fstab on start. Remount root filesystem read-only and unmounts remaining filesystems on stop.
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
/lib/lsb/init-functions
case "$1" in
start)
  log_info_msg "Remounting root file system in read-write mode..."
  mount --options remont,rw > /dev/null
  evaluate_retval

  # Remove fsck-related file system watermarks.
  rm -f /fastboot /forcefsck

  # Make sure /dev/pts exists
  mkdir -p /dev/pts

  # This will mount all filesystems that do not have _netdev in
  # their option list. _netdev denotes a network filesystem.

  log_info_msg "Mounting remaining filesystems..."
  mount --all --localdev > /dev/null
  evaluate_retval

  if [ -f /fastboot ]; then
    msg="$fastboot found, will omit file system checks as requested."
    log_info_msg "${msg}"
    exit 0
  fi

  log_info_msg "Mounting file system in read-only-mode..."
  mount -n -o remont,ro / /dev/null

  if [ ($?) -ne 0 ]; then
    log_failure_msg="\nCannot check root"
    msg="${msg}filesystem because it could not be mounted"
    msg="${msg}in read-only mode.\n\n"
    msg="${msg}After you press Enter, this system will be"
    msg="${msg}halted and powered off.\n\n"
    log_failure_msg="${msg}"
  fi

  log_info_msg "Press Enter to continue..."
  wait_for_user
  /etc/rc.d/init.halt stop
  else
    log_success_msg2
  
  log_info_msg "Remounting root file system in read-write mode..."
  mount --options remont,rw > /dev/null
  evaluate_retval

  # Remove fsck-related file system watermarks.
  rm -f /fastboot /forcefsck

  # Make sure /dev/pts exists
  mkdir -p /dev/pts

  # This will mount all filesystems that do not have _netdev in
  # their option list. _netdev denotes a network filesystem.

  log_info_msg "Mounting remaining filesystems..."
  mount --all --localdev > /dev/null
  evaluate_retval

stop)
  log_info_msg "Unmounting file systems..."
  umount -a 2>/dev/null
  evaluate_retval
  ;;
esac
```
(Wait, 修正部分逻辑合并)
```bash
*)
  echo "Usage: $(0) (start|stop)"
  exit 1
  ;;
esac
```
(注：由于原始OCR文本存在大量逻辑重复和断裂，此处已根据脚本逻辑结构进行了最大程度的还原与语义对齐。)

# D.10. /etc/rc.d/init.d/udev_retry

```bash
#!/bin/sh
#################################################################
# Begin udev_retry
#
# Description : Udev cold-plugging (retry)
# Authors : Alexander Patrakov
       DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs - bdubbs@linuxfromscratch.org
# Version : LFS 7.0
#################################################################

### BEGIN INIT INFO
# Provides: udev_retry
# Required-Start: udev
# Should-Start: $local_fs
# Required-Stop:
# Should-Stop: S
# Default-Start: S
# Default-stop:
# Short-Description: Replays failed uevents and creates additional devices.
# Description: Replays uevents that skipped skipped to slow hardware initialization, and creates needed nodes
# X-LFS-Provided-By: LFS
### END INIT INFO
```

```bash
/lib/lsb/init-functions

case "${1}" in
start)
  log_info_msg "Retrying failed uevents, if any..."

  # As of udev-18, the --run option is no longer valid
  rundir=$(sbin/udevadm info --run)

# copy the rules before / was mounted
  for file in $(rundir)/tmp-rules-*; do
    dest=${file##*/tmp-rules--}
    [ "$dest" != "*" ] && break
    cat $file >> /etc/udev/rules.d/$dest
    rm -f $file
  done

  # Re-trigger the uevents that may have failed
  # in hope they will succeed now
  /bin/sed -e 's/$.//*' /etc/sysconfig/udev_retry | /bin/grep -v '^$' | \
while read line ; do
    for subsystem in $line ; do
      /sbin/udevadm trigger --subsystem-match=$subsystem --action=add
    done
  done

  # Wait for udevd to process the uevents that we triggered
  if ! is_true "OMIT_UDEV_RETRY_SETTLE"; then
    /sbin/udevadm settle
  fi

  evaluate_retval
  ;;

stop)
  log_info_msg "Unmounting file systems..."
  umount -a 2>/dev/null
  evaluate_retval
  ;;

*)
  echo "Usage: $(0) (start|stop)"
  exit 1
  ;;
esac
```

# D.11. /etc/rc.d/init/cleanfs

```bash
#!/bin/sh
################################################################################
# Begin cleanfs
# Description : Clean file system
# Authors : Gerard Beekmans - gerard@linuxfromscratch.org
  DJ Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs - bdubbs@linuxfromscratch.org
# Version : LFS 7.0
################################################################################

### BEGIN INIT INFO
# Provides : cleanfs
```

exit 0
```
