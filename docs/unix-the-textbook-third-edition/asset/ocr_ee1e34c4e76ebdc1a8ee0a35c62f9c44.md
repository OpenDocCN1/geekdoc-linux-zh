```
media 10baseT/UTP mediaopt full-duplex
media 10baseT/UTP
```

```
$
```

The ifconfig command can be used to change NIC settings as well as display them. A NIC is a Network Interface Card, what the system hardware uses to interface with a network. After executing each of the next series of ifconfig commands, view the changes in the NIC settings by using the ifconfig -l command.

To hard set the NIC bge0 to 100 MBps with full duplex, type this:

```
$ ifconfig bge0 media 100baseTX mediaopt full-duplex
```

To hard set the speed to 10 MBps, type this:

```
$ ifconfig bge0 media 10baseT/UTP
```

To change the IP address and netmask, type this:

```
$ ifconfig bge0 inet 10.0.0.208 netmask 255.0.0.0
```

The changes just made to your NIC settings are good for the current session. When you reboot, however, those settings will be lost.

# 23.3.8.3.2 ipadm in Solaris

The ipadm command administers the network IP interfaces and TCP/IP parameters.

To display information about the current IP interface configuration, use the following option:

```
$ ipadm show-if
IFNAME    STATE    CURRENT      PERSISTENT
lo0       ok       -m-v-----46  ---
bfe0      ok       bm--------46  ---
iwi0      ok       bm--------46  ---
$
```

To display the address associated with the IP interface, use the following option:

```
$ ipadm show-addr
ADDROBJ      TYPE    STATE    ADDR
lo0/v4       static  ok       127.0.0.0.1/8
bfe0/_b      dhcp    ok       ?
iwi0/_b      dhcp    ok       192.168.0.12/24
lo0/v6       static  ok       ::1/128
bfe0/_a      addrconf ok      fe80::212:3fff:fed1:8578/10
```