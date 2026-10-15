```
```text
# CCW_CHAN_NUM set the number of channels for this device
# Always 3 for a qeth device
CCW_CHAN_NUM=3

# CCW_CHAN_MODE sets the port name for an OSA-Express device
# CCW_CHAN_MODE="LZ4LAN01"

# QETH_OPTIONS sets additional options for the OSA-Express or
# HiperSockets device. Valid parameters are:
# add_hhlen buffer_count broadcast_mode canonical_macaddr checksumming
# fake_broadcast fake_ll priority_queueing route4 route6
# QETH_OPTIONS="fake_ll=1"

# QETH_IPA_TAKEOVER enables IP address takeover for this device
# QETH_IPA_TAKEOVER=0
```
```

**Important:** Devices numbers must be lowercase.

+   4. Create the network configuration file in `/etc/sysconfig/network`  
+      (Example 6-10).

```
_Example 6-10  Creating the network configuration file_

```text
lnxgqill:/etc/sysconfig/network # cp -arv ifcfg-qeth-bus-ccw-0.0.0600 ifcfg-qeth-bus-ccw-0.0.0d20
ifcfg-qeth-bus-ccw-0.0.0d20
`ifcfg-qeth-bus-ccw-0.0.0d20' -> `ifcfg-qeth-bus-ccw-0.0.0d20'
```
```

+   5. Update the configuration file with your TCP/IP configuration (Example 6-11).

```
_Example 6-11  Updating TCP/IP configuration_

```text
lnxguill:/etc/sysconfig/network # cat ifcfg-qeth-bus-ccw-0.0.0d20
BOOTPROTO="static"
UNIQUE=""
STARTMODE="onboot"
IPADDR="172.0.0.1"
NETMASK="255.255.255.0"
NETWORK="172.0.0.0"
BROADCAST="172.0.0.255"
```
```

+   6. Enable the network interface in Linux (Example 6-12).

```
_Example 6-12  Enabling the network interface_

```text
lnxguill:/etc/sysconfig/hardware # echo '0.0.0d20,0.0.0d21,0.0.0d22' >
/sys/devices/qeth/0.0.0d20/portname
lnxguill:/etc/sysconfig/hardware # echo 1 >
/sys/devices/qeth/0.0.0d20/online
```
```