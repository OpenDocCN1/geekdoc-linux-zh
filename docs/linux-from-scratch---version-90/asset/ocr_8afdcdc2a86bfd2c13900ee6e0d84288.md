# D26. .lib/services/ipv4-static

```
#!/bin/sh
############################################################
# Begin /lib/services/ipv4-static
#
# Description : IPv4 Static Boot Script
#
# Authors : Nathan Coulson - nathan@linuxfromscratch.org
# Kevin P. Fleming - kpfleming@linuxfromscratch.org
# Update : Bruce Dubbs - bdubbs@linuxfromscratch.org
#
# Version : LFS 7.0
############################################################
. /lib/lsb/init-functions
. ${CONFIG}

if [ -z "${IP}" ]; then
    log_failure_msg "\nIP variable missing from ${CONFIG}, cannot continue."
    exit 1
fi

if [ -z "${PREFIX}" -a -z "${PEER}" ]; then
    log_warning_msg "\nPREFIX variable missing from ${CONFIG}, assuming 24."
    PREFIX=24
fi
args="${args} \${IP}/${PREFIX}"
elif [ -n "${PREFIX}" -a -n "${PEER}" ]; then
    log_failure_msg "\nPREFIX and PEER both specified in ${CONFIG}, cannot continue."
    exit 1
fi
if [ -n "${PREFIX}" ]; then
    args="${args} \${IP}/${PREFIX}"
fi
if [ -n "${PEER}" ]; then
    args="${args} \${IP} peer \${PEER}"
fi

if [ -n "${LABEL}" ]; then
    args="${args} label \${LABEL}"
fi

if [ -n "${BROADCAST}" ]; then
    args="${args} broadcast \${BROADCAST}"
fi

case "$2" in
    up)
```