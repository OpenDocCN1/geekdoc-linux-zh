# Linux From Scratch - Version 9.0

```
if [ "${ip addr} show ${1} 2>/dev/null | grep ${$IP}" != " " ]; then
  log_info_msg "Adding IPv4 address ${$IP} to the interface..."
  ip addr add ${$args} dev ${1}
  evaluate_retval
else
  log_warning_msg "Cannot add IPv4 address ${$1}. Already present."
fi
```

```
if [ "${ip addr} show ${1} 2>/dev/null | grep ${$IP}" != " " ]; then
  log_info_msg "Removing IPv4 address ${$IP} from the interface..."
  ip addr del ${$args} dev ${1}
  evaluate_retval
fi
```

```
if [ -n "${GATEWAY}" ]; then
  # Only remove the gateway if there are no remaining ipv4 addresses
  if [ "${ip addr} show ${1} 2>/dev/null | grep 'inet '" != " " ]; then
    log_info_msg "Removing default gateway..."
    ip route del default
    evaluate_retval
  fi
fi
```

```
echo "Usage: $0 [interface] (up|down)"
exit 1
```

# End /lib/services/ipv4-static

# D27. /lib/services/ipv4-static-route

```
#!/bin/sh
######################################################################
# Begin /lib/services/ipv4-static-route
# Description : IPv4 Static Route Script
# Authors      : Kevin P. Fleming - kefleman@linuxfromscratch.org
#               DJ Lucas - dj@linuxfromscratch.org
# Update      : Bruce Dubbs - bdubbs@linuxfromscratch.org
# Version      : LFS 7.0
######################################################################
```

```
. /lib/sb/init-functions
. ${IFONFIG}
```

```
case "${TYPE}" in
  ("" | "network")
    need_ip=1
```