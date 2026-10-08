
```bash
# block creates a block device
# char creates a character device
# pipe creates a pipe, this will ignore the <major> and
# <minor> fields
# <major> and <minor> are the major and minor numbers used for
# the device.
###############################################################################

# End /etc/sysconfig/createfiles
```

## D.23. /etc/sysconfig/udev-retry

```
###############################################################################
# Begin /etc/sysconfig/udev-retry
# Description : udev_retry script configuration
# Authors :
# Version : 00.00
# Notes : Each subsystem that may need to be re-triggered after mountfs
runs should be listed in this file. Probable subsystems to be
listed here are rtc (to /var/lib/hwclock/adjime) and sound
(due to both /var/lib/alsa/asound.state and /usr/sbin/lsactl).
Entries are whitespace-separated.
###############################################################################
```

rtc

```
# End /etc/sysconfig/udev-retry
```

# D.24. /sbin/ifup

```bash
#!/bin/sh
###############################################################################
# Begin /sbin/ifup
# Description : Interface Up
# Authors : Nathan Coulson - nathan@linuxfromscratch.org
# Kevin P. Fleming - kfleming@linuxfromscratch.org
# Update : Bruce Dubces - dbubds@linuxfromscratch.org
# DJ Lucas - dj@linuxfromscratch.org
# Version : LFS 7.7
# Notes : The IFONFIG variable is passed to the SERVICE script
in the /lib/services directory, to indicate what file the
service should source to get interface specifications.
##############################################################################################
```

```bash
up()
{
log_info_msg "Bringing up the ${1} interface..."

if ip link show $1 > /dev/null 2>&1; then
  link_status=`ip link show $1`

  if [ -n ${link_status} ]; then
    if echo "${link_status}" | grep -q UP; then
      ip link set $1 up
    fi
  fi
else
  log_failure_msg "Interface ${INTERFACE} doesn't exist."
  exit 1
fi

evaluate_retrieval
}

RELEASE="7.7"

USAGE="Usage: $0 [-h -V] [--help] [--version] interface"
STR="IFS ifup, version ${RELEASE}"

while [ \$# -gt 0 ]; do
  case "$1" in
    --help | -h)
      help="y"; break; 
    --version | -V)
      echo "ifup: ${1}: invalid option" >&2
      echo "${USAGE}" >&2
      exit 2; 
    -*)
      break; 
  esac
done

if [ -n "$help" ]; then
  echo "${VERSTR}"
  echo "${USAGE}"
  echo
  cat << HERE_EOF
ifup is used to bring up a network interface. The interface parameter, e.g. eth0 or eth0:2, must match the trailing part of the interface specifications file, e.g. /etc/sysconfig/ifconfig.eth0:2.
HERE_EOF
  exit 0
fi

file=/etc/sysconfig/ifconfig.${1}
# Skip backup files
[ "${file}" = "${file}"-"" ] || exit 0

./lib/lsb/init-functions

if [ -r "${file}" ]; then
  log_failure_msg "Unable to bring up ${file} interface! ${file} is missing or cannot be accessed."
  exit 1

$file

if [ "${INTERFACE}" = "" ]; then
  log_failure_msg "Unable to bring up ${file} interface! ${file} does not define an interface ${INTERFACE}"
  exit 1
fi

# Do not process this service if started by boot, and ONBOOT
# is not set to yes
if [ "${IN_BOOT}" = "1" -a "${ONBOOT}" != "yes" ]; then
  exit 0
fi

# Bring up the interface
if [ "${VIRTINT}" != "yes" ]; then
  up ${INTERFACE}
fi

for S in ${SERVICE}; do
  if [ ! -x "/lib/services/${S}" ]; then
    MSG="Unable to process \${file}."
    MSG="${MSG}THE SERVICE '${S}' was not present"
    MSG="${MSG}or cannot be executed."
    log_failure_msg "$MSG"
    exit 1
  fi
done

if [ "${SERVICE}" = "wpa" ]; then log_success_msg; fi

# Create/configure the interface
for S in ${SERVICE}; do
  IFCONFIG=${file} /lib/services/${S} ${INTERFACE}

  # Set up virtual interfaces
  if [ "${VIRTINT}" = "yes" ]; then
    up ${INTERFACE}
  fi

  # Bring up any additional interface components
  for I in ${INTERFACE_COMPONENTS}; do up ${I}; done

  # Set MTU if requested. Check if MTU has a "good" value.
  if test -n "\${MTU}"; then
    if [[ \${MTU} =~ ^[0-9]+$ ]] && [[ \${MTU} -ge 68 ]]; then
      for I in ${INTERFACE_COMPONENTS}; do
        ip link set dev ${I} mtu ${MTU}
      done
    fi
  else
    log_info_msg2 "Invalid MTU \${MTU}"
  fi
done

# Set the route default gateway if requested
if -n "${GATEWAY}"; then
  if ip route | grep -q already setup; then
    log_warning_msg "Gateway already setup, skipping."
  else
    log_info_msg "Adding default gateway \${GATEWAY} to the \${IFACE} interface"
    ip route add default via \${GATEWAY} dev \${IFACE}"
    evaluate_retrieval
  fi
fi

# End /sbin/ifup

# D.25. /sbin/ifdown

```bash
#!/bin/bash
##################################################################
# Begin /sbin/ifdown
#
# Description : Interface Down
# Authors      : Nathan Coulson nathan@linuxfromscratch.org
               Kevin P. Fleming kpflemming@linuxfromscratch.org
# Update      : Bruce Dubbs bdubbs@linuxfromscratch.org
# Version      : LFS 7.0
# Notes       : the IFCONFIG variable is passed to the SERVICE
in the /lib/services directory, to indicate what file the
service should source to get interface specifications.
##################################################################

RELEASE="7.7"

USAGE="Usage: $0 [-h -V] [--help] [--version] interface"
STR="IFS ifdown, version ${RELEASE}"

while [ \$# -gt 0 ]; do
  case "$1" in
    --help | -h)
      help="y"; break; 
    --version | -V)
      echo "ifdown: ${1}: invalid option" >&2
      echo "${USAGE}" >&2
      exit 2; 
    -*)
      break; 
  esac
done

if [ -n "$help" ]; then
  echo "${VERSTR}"
  echo "${USAGE}"
  echo
  cat << HERE_EOF
ifdown is used to bring down a network interface. The interface parameter, e.g. eth0 or eth0:2, must match the trailing part of the interface specifications file, e.g. /etc/sysconfig/ifconfig.eth0:2.
HERE_EOF
  exit 0
fi

file=/etc/sysconfig/ifconfig.${1}
# Skip backup files
[ "${file}" = "${file}"-"" ] || exit 0

./lib/lsb/init-functions

if [ -r "${file}" ]; then
  log_failure_msg "Unable to bring down ${file} interface! ${file} is missing or cannot be accessed."
  exit 1

$file

if [ "${INTERFACE}" = "" ]; then
  log_failure_msg "Unable to bring down ${file} interface! ${file} does not define an interface ${INTERFACE}"
  exit 1
fi

# Do not process this service if started by boot, and ONBOOT
# is not set to yes
# (logic follows ifup)
if [ "${IN_BOOT}" = "1" -a "${ONBOOT}" != "yes" ]; then
  exit 0
fi

# Bring down the interface
if [ "${VIRTINT}" != "yes" ]; then
  down ${INTERFACE}
fi

for S in ${SERVICE}; do
  if [ ! -x "/lib/services/${S}" ]; then
    MSG="Unable to process \${file}."
    MSG="${MSG}THE SERVICE '${S}' was not present"
    MSG="${MSG}or cannot be executed."
    log_failure_msg "$MSG"
    exit 1
  fi
done

if [ "${SERVICE}" = "wpa" ]; then log_success_msg; fi

# De-configure the interface
for S in ${SERVICE}; do
  IFCONFIG=${file} /lib/services/${S} ${INTERFACE}

  # Set up virtual interfaces
  if [ "${VIRTINT}" = "yes" ]; then
    down ${INTERFACE}
  fi

  # Bring down any additional interface components
  for I in ${INTERFACE_COMPONENTS}; do down ${I}; done
done

# Set the route default gateway if requested
if -n "${GATEWAY}"; then
  if ip route | grep -q already setup; then
    log_warning_msg "Gateway already setup, skipping."
  else
    log_info_msg "Adding default gateway \${GATEWAY} to the \${IFACE} interface"
    ip route add default via \${GATEWAY} dev \${IFACE}"
    evaluate_retrieval
  fi
fi

# End /sbin/ifdown
```

## D.26. /lib/services/ipv4-static

```bash
#!/bin/sh
############################################################
# Begin /lib/services/ipv4-static
#
# Description : IPv4 Static Boot Script
#
# Authors : Nathan Coulson - nathan@linuxfromscratch.org
# Kevin P. Fleming - kfleming@linuxfromscratch.org
# Update : Bruce Dubbs - bdubbs@linuxfromscratch.org
#
# Version : LFS 7.0
############################################################

RELEASE="7.7"

USAGE="Usage: $0 [-h -V] [--help] [--version] interface"
STR="IFS ipv4-static, version ${RELEASE}"

while [ \$# -gt 0 ]; do
  case "$1" in
    --help | -h)
      help="y"; break; 
    --version | -V)
      echo "ipv4-static: ${1}: invalid option" >&2
      echo "${USAGE}" >&2
      exit 2; 
    -*)
      break; 
  esac
done

if [ -n "$help" ]; then
  echo "${VERSTR}"
  echo "${USAGE}"
  echo
  cat << HERE_EOF
ipv4-static is used to bring up a network interface. The interface parameter, e.g. eth0 or eth0:2, must match the trailing part of the interface specifications file, e.g. /etc/sysconfig/ifconfig.eth0:2.
HERE_EOF
  exit 0
fi

file=/etc/sysconfig/ifconfig.${1}
# Skip backup files
[ "${file}" = "${file}"-"" ] || exit 0

if [ -r "${file}" ]; then
  log_failure_msg "Unable to bring up ${file} interface! ${file} is missing or cannot be accessed."
  exit 1

fi

$file

if [ "${INTERFACE}" = "" ]; then
  log_failure_msg "Unable to bring up ${file} interface! ${file} does not define an interface ${INTERFACE}"
  exit 1
fi

# Do not process this service if started by boot, and ONBOOT
# is not set to yes
if [ "${IN_BOOT}" = "1" -a "${ONBOOT}" != "yes" ]; then
  exit 0
fi

# Bring up the interface
if [ "${VIRTINT}" != "yes" ]; then
  args=""
  ip addr show ${INTERFACE} 2>/dev/null | grep 'inet ' | awk '{print $2}' | cut -d/ -f1 | while read -r line; do
    if [ -z "$args" ]; then
      args="$line"
    else
      args="$args $line"
    fi
  )
  # This is a simplified representation of the actual script logic
  # In the real script, it iterates through the config
fi

# (The actual logic continues with parsing the config and calling ip addr)
```
