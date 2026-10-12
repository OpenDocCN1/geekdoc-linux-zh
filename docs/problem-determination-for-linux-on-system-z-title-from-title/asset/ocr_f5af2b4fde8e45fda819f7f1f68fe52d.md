# Data for analysis

To troubleshoot the problem, we need to gather the following information and analyze it for correctness:

+   - /etc/sysconfig/hardware/hwcfg-qeth-bus-ccw-0.0.xxxx
+   - /etc/sysconfig/network/ifcfg-qeth-bus-ccw-0.0.xxxx
+   - dmesg command output
+   - ifconfig command output
+   - /etc/sysconfig/network/routes
+   - netstat -m command output

# Analysis and conclusion

Upon checking the configuration files, all looked correct. But from the routing table output given by the route -n command, we identify that the eth0 interface is configured as the routing interface (default gateway) for eth1. So, when the eth0 interface went down, the eth1 interface was not able to communicate because of the loss of the routing table entries. All communication was done via the eth0 interface.

If the above approach is not leading to a solution, then consider obtaining a packet trace.

# Case study 2 - connection lost after VSWITCH OSA takeover

Assume that we have a VSWITCH configured on a z/VM system with device 3700 as the active OSA and device 3800 as the backup OSA.

# Problem

When the cable connected to the active OSA (device 3700) was removed, the communication was lost even though switching to the backup OSA (device 3800) happened.

# Data for analysis

Analyze the following data:

+   - The status of devices 3700 and 3800
+   - ARP cache of z/VM TCP/IP and the workstation executing the ping command
+   - Routing z/VM Linux guest information for the z/VM Linux guest (route -n command output)
+   - Trace information for the VSWITCH
+   - OSA/SF query