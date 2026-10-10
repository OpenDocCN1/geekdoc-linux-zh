# Listing 12-9
**Booting with NFS Root Mount**

```
Uncompressing Kernel Image . . . OK
Linux version 2.6.14 (chris@pluto) (gcc version 3.3.3
L(DENX ELDK 3.1.1 3.3.3-10)) #1 Mon Jan 2 11:58:48 EST 2006
.
Kernel command line: console=ttyS0,115200 root=/dev/nfs rw
\_nfsroot=192.168.1.9:/home/chris/sandbox/pd\na-target ip=dhcp

Sending DHCP requests . . . OK
IP-Config: Got DHCP answer from 192.168.1.9, my address is 192.168.1.68
IP-Config: Complete:
	device=eth0, addr=192.168.1.68, mask=255.255.255.0,
	gw=255.255.255.255, host=192.168.1.68, domain=
	mis-domain=(none), bootserver=192.168.1.9,
	rootserver=192.168.1.9,
	rootpath=/home/chris/sandbox/pd\na-target
.
.
Looking up port of RPC 100003/2 on 192.168.1.9
Looking up port of RPC 100005/1 on 192.168.1.9
VFS: Mounted root (nfs filesystem).

BusyBox v0.60.5 (2005.06.07-07:03+0000) Built-in shell (msh)
Enter 'help' for a list of built-in commands.
#
```

From Listing 12-9, first we see the kernel banner followed by the kernel com- mand line. We specified four items in this kernel command line:

+   - Console device (/dev/console)
+   - Root device (/dev/nfs)
+   - NFS root path (/home/chris/sandbox/pd\na-target)
+   - IP kernel-level autoconfiguration method (dhcp)

Shortly thereafter, we see the kernel attempting kernel-level autoconfiguration via DHCP. When the server responds and the DHCP exchange completes, the ker- nel displays the detected configuration in the following lines. You can see from this