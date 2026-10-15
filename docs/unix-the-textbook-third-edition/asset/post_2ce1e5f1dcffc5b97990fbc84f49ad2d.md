
```
[bob@pcbsd-1233] /usr/home/bob# iocage list
JID UUID BOOT STATE TAG
- 44599667-9574-11e5-9cc9-08002738ba74 off down bobsecond
- 527c21ff-9573-11e5-9cc9-08002738ba74 off down
2015-11-27@17:57:04
```

The name of the new jail is bobsecond, with a reference UUID (44599667-9574-11e5-9cc9-08002738ba74).

## EXERCISE 25.2

Similar to the steps shown in Example 25.1, create a lightweight jail on your system. Name or tag the jail with your own unique name. Then use the zfs list command to display the ZFS file system for this jail, and its mount point. How large is the jail in bytes?

### Example 25.2: Listing Jails and Starting Them Automatically at System Boot

As shown in Example 25.1, the following command lists information about the current jails:

```
# iocage list
JID UUID BOOT STATE TAG
- 44599667-9574-11e5-9cc9-08002738ba74 off down bobsecond
```

You can see that the boot flag is off. This means the jail will not be started at boot time. The STATE identifier means that the jail has not been started, or is inactive.

Starting jails automatically at system boot: To allow iocage to start your jails at boot time, add the following line to /etc/rc.conf:

```
iocage_enable="YES"
```

Individual jails can be marked for starting at system boot by using this command:

```
# iocage set boot=on bobsecond
```

You can specify the order for jails to start by setting their priority:

```
# iocage set priority=20 bobsecond
```

A lower value means a higher boot priority (i.e., boot the jail earlier).

## EXERCISE 25.3

For the jail you created in in-chapter Exercise 25.2, change its properties so that it autostarts at system boot. Then reboot the system to see that the jail starts automatically.

### Example 25.3: Looking Into, Starting, Stopping, and Destroying a Jail

You can chroot into your jail without starting or running the jail:

```
# iocage chroot bobsecond
root@pcbsd-1233: / #
```

This can be useful for modifying the jail. Explore the jail with the ls command:

```
root@pcbsd-1233:/ # ls
.cshrc  bin   etc   media  rescue  sys   var
.profile boot  lib   mnt    root    tmp
COPYRIGHT dev libexec proc  sbin    usr
root@pcbsd-1233:/ #
```

See how the network connection is configured:

```
root@pcbsd-1233:/ # ifconfig
em0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> metric 0 options=9b<RXCSUM,TXCSUM,VLAN_MTU,VLAN_HWTAGGING,VLAN_HWCSUM>
ether 08:00:27:38:ba:74
inet6 fe80::a00:27ff:fe38:ba74%em0 prefixlen 64 scopeid 0x1
inet 192.168.0.16 netmask 0xffffffff broadcast 192.168.0.255
nd6 options=23<PERFORMNUD,ACCEPT_RTADV,AUTO_LINKLOCAL>
media: Ethernet autoselect (1000baseT <full-duplex>)
status: active
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> metric 0 mtu 16384
options=600003<RXCSUM,TXCSUM,RXCSUM_IPV6,TXCSUM_IPV6>
inet6 ::1 prefixlen 128
inet6 fe80::1%lo0 prefixlen 64 scopeid 0x2
inet 127.0.0.1 netmask 0xff000000
nd6 options=21<PERFORMNUD,AUTO_LINKLOCAL>
root@pcbsd-1233:/ #
```

To get out of the chroot, press <CTRL-D> or type exit.

Starting a jail

```
[bob@pcbsd-1233] /usr/home/bob# iocage start bobsecond
* Starting 44599667-9574-11e5-9cc9-08002738ba74 (bobsecond)
+ Started (shared IP mode) OK
+ Starting services OK
[bob@pcbsd-1233] /usr/home/bob#
[bob@pcbsd-1233] /usr/home/bob# iocage list
JID          UUID                                 BOOT  STATE TAG
```

```
1 44599667-9574-11e5-9cc9-08002738ba74  off  up    bobsecond
- 527c21ff-9573-11e5-9cc9-08002738ba74  off  down
2015-11-27@17:57:04
[bob@pcbsd-1233] /usr/home/bob#
```

The jail named bobsecond is up.

Accessing a jail console: This command allows you access to the jail without logging into it:

```
[bob@pcbsd-1233] /usr/home/bob# iocage console bobsecond
FreeBSD 10.2-RELEASE-p4 (GENERIC) #0: Tue Aug 18 15:15:36 UTC 2015
Welcome to FreeBSD!
Release Notes, Errata: https://www.FreeBSD.org/releases/
...
root@44599667-9574-11e5-9cc9-08002738ba74:~ #
```

You are now in the jail as if you had logged in at the console. For example, we can now start sshd manually. Watch as it creates missing keys automatically:

```
root@44599667-9574-11e5-9cc9-08002738ba74:~ # service sshd onestart
Generating RSA1 host key.
2048 09:c9:e8:a8:b3:dc:5b:e6:22:9c:a8:f4:6b:76:da:c7:10
root@44599667-9574-11e5-9cc9-08002738ba74 (RSA1)
Generating RSA host key.
2048 a4:03:c5:76:ed:41:80:77:20:3f:d6:99:89:37:4d
root@44599667-9574-11e5-9cc9-08002738ba74 (RSA)
Generating DSA host key.
1024 78:4b:04:4b:e8:f5:09:a5:5f:0e:71:02:b4:c6:b2:7b
root@44599667-9574-11e5-9cc9-08002738ba74 (DSA)
Generating ECDSA host key.
256 c7:98:87:dc:16:37:df:95:21:d0:24:04:75:a8:50:c3
root@44599667-9574-11e5-9cc9-08002738ba74 (ECDSA)
Generating ED25519 host key.
256 53:08:ac:52:d3:3e:ba:53:9e:ec:0b:c6:42:22:bc:c8
root@44599667-9574-11e5-9cc9-08002738ba74 (ED25519)
Performing sanity check on sshd configuration.
Starting sshd.
root@44599667-9574-11e5-9cc9-08002738ba74:~ #
```

Check the network configuration:

```
root@44599667-9574-11e5-9cc9-08002738ba74:~ # ifconfig
em0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> metric 0 mtu 1500
```
