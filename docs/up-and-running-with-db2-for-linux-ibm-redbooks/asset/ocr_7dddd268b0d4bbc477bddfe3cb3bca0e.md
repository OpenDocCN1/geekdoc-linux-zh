```
#   consequently, for the rsh(1) program. The server provides \
#   remote execution facilities with authentication based on \
#   privileged port numbers from trusted hosts.
service shell
{
    socket_type      = stream
    wait             = no
    user             = root
    log_on_success   += USERID
    log_on_failure   += USERID
    server           = /usr/sbin/in.rshd
    disable          = no
}
```

Alternatively, you can use the ntsysv command to launch Red Hat's ntsysv tool. This application allows you to configure which services are started at boot time for each runlevel. Please note that the changes that you make will not take effect immediately and that ntsysv cannot be used to stop, start or re-start services.

# Network troubleshooting on Red Hat

If you are having problems getting network communications set up on Red Hat, you should look at the following network configuration files.

+   - /etc/hosts - This is the hostname resolution file (resolves a hostname to an IP address). This file must contain the localhost entry 127.0.0.1. Our /etc/hosts file looks like this:
+   ```
+   # /etc/hosts file on host "udblnx03"
+   # Do not remove the following line, or various programs
+   # that require network functionality will fail.
+   127.0.0.1   localhost
+   9.1.38.63   udblnx01
+   9.1.38.64   udblnx02
+   9.1.38.65   udblnx03 udblnx03.local
+   9.1.38.66   udblnx04
+   9.1.38.67   udblnx05
+   ```

+   - /etc/sysconfig/network - This file specifies routing and host information for all network interfaces. It should look something like this:
+   ```
+   # our /etc/sysconfig/network file on host "udblnx03"
+   NETWORKING=yes
+   HOSTNAME=udblnx03
+   ```

+   - /etc/sysconfig/network-scripts/ifcfg-eth0 - This contains an interface configuration script that controls the first network interface card in the system. For example, our ifcfg-eth0 file contains the following data:
+   ```
+   DEVICE=eth0
+   BOOTPROTO=none
+   ```