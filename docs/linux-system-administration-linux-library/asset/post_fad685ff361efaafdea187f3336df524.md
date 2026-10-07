
# 118 Chapter 4 Tools of the Trade

## umount

```
umount [options] device|mount_point [-t vftype]
```

The umount command detaches the listed filesystem or the filesystem mounted on the specified mount point from the Linux tree. The filesystem cannot be unmounted when it contains open files, has a user currently located somewhere in its directory tree, or contains a swap file that is in use.

## showmount

```
showmount [options] [host]
```

The showmount command queries the mount daemon on a remote machine about the status of its NFS server. If no options are specified, the showmount command returns a list of all clients who are mounting from that host.

## ulimit

```
ulimit [options] [limit]
```

The ulimit command can be used to determine resource limits for a shell and the processes started by it. The arguments to ulimit include -a to report all current limits, -c for maximum core size, -f for maximum file size, -n for the number of open files, and -u for the number of processes per user. The ulimit may also also be used to adjust these limits by specifying the correct argument followed by the new numeric value. Preceding the options with a H sets hard limits, which cannot be increased once set. A soft limit, preceded by an S, can be increased until it reaches the hard limit. If neither H nor S is given, a soft limit is assumed.

To determine what the hard limit is on the maximum core size, use the ulimit command as listed below. The return value shows that on a Red Hat system, there is no hard limit to the size of a core file.

```
# ulimit -Hc
unlimited
```

To set the maximum core size to 1024, issue the following command:

```
# ulimit -c 1024
```

Now check your work by issuing the ulimit -c command without a value. The result should be the value you specified.

## mkswap

```bash
mkswap [options] device [size]
```

mkswap command creates a swap area on the specified device or file. A swap area is used to hold pages out from memory, making it possible to read them back into memory more quickly. In Linux, a swap space twice the size of the amount of memory in the system is usually sufficient. Most often, the device that contains the swap space is a disk partition, but a file created with a dd command can also be used, like this:

```bash
# dd if=/dev/zero of=/dev/swapfile bs=1024 count=65536
```

The copy command will not work to create a swap file. When the device or file is created, the swapon command must be used to activate the swap area.

A swap partition is typically created when the Linux system is first installed. Refer to Chapter 2 for more information on how to create swap space as a separate partition.

## swapoff

```bash
swapoff [-a]
swapoff specialfile(s)
```

The swapoff command disables swapping on the specified devices or files. If swapoff is called with an -a option, all swap entries in /etc/fstab will be disabled.

## swapon

```bash
swapon [-v] [-p priority] specialfile(s)
swapon [-a]
```

The swapon command enables swapping on the specified devices or files or on all devices listed in /etc/fstab if the -a option is given. This is usually done by the rc script when the run level is changed.

## sync

```bash
sync [options]
```

The sync command flushes the filesystem buffers, thereby forcing any data waiting there to be written to the disk. This command is necessary when you mount another filesystem and make changes to it to ensure that everything that was to be written to the mounted filesystem actually was.

## 120 Chapter 4 Tools of the Trade

## fuser

```bash
fuser [options] filesystem
```

The fuser (file command) determines which user is using a file from a given filesystem or is currently in a directory belonging to the given filesystem. This is important if you try to unmount a filesystem and are told it is busy. The -m option is necessary if the filesystem is mounted. Using the -u option gives both process and corresponding user information for the filesystem. The c after several process IDs in the following example indicates that those processes are running from the current directory.

```bash
# fuser -mu /home
```

```
/home:
1456(user) 4271(user) 4301(user) 4456(user) 5729(user)
```

## Network Commands

The commands in this section work with network connections and are used frequently. These commands allow you to determine whether a network interface is operational and to check its efficiency. Chapter 5 deals with TCP/IP connections and Chapter 7 deals with the security issues related to such connection.

## ifconfig

```bash
ifconfig [interface]
ifconfig interface [address] [options]
```

The ifconfig command displays the status of currently active interfaces. If an interface is listed as the only argument, ifconfig will return the status of that interface. The ifconfig command may also be used to configure network interfaces, although seldom used except in scripts. Listing 4.6 shows the output from this command.

### Listing 4.6 Sample Output from ifconfig

```
eth0 Link encap:Ethernet addr 00:55:A0:52:33 inet:192.168.1.1 Mask:255.255.255.0 UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1 RX packets:5861 errors:0 dropped:0 frame:0 TX packets:5051 errors:0 dropped:0 collisions:0 txqueen:100
lo Link encap:Loopback addr:127.0.0.1 Mask:255.0.0 UP LOOPBACK RUNNING MTU:3924 Metric:1 RX packets:4404 errors:0 dropped:0 frame:0 TX packets:4404 errors:0 dropped:0 collisions:0 txqueen:0
ppp Link encap:Point-to-Point inet addr:216.126.175.225:216.126.175.2 Mask:255.255.255 UP POINT RUNNING MULTICAST MTU:1500 Metric:1 RX packets:2191 errors:0 dropped:0 frame:0 TX packets:2125 errors:0 dropped:0 collisions:0 txqueen:10
```## Command-Line Tools

## netstat

```bash
netstat [options]
```

The netstat command displays network connections, routing tables, interface statistics, masquerade connections, and multicast memberships. The -n option forces the output to use numeric IP addresses rather than hostnames.

## ping

```bash
ping [options]
```

The ping command is used to test network connections. It sends a signal to the indicated host, waits to receive a reply packet, and reports the receipt or lack of response. The ping command is primarily used for troubleshooting network connections. Examples are given in Chapter 18.

## route

```bash
route [options] add [-net|-host] target [options]
route [options] del [-net|-host] target [options]
```

The route command is used to display and manipulate the IP routing table. It is primarily used to set up static routes to hosts or networks already configured by the ifconfig command.

## ftp

```bash
ftp [options] host
```

The ftp command starts the interface to the Internet's File Transfer Protocol, allowing users to transfer files to and from a remote site. It is typically run interactively, although this can be turned off with the -i option.

## telnet

```bash
telnet [options] [host|port]
```

The telnet command uses the Telnet protocol to communicate with the specified host or in command mode if no host is given. In command mode, telnet takes commands like OPEN (to open a host site), CLOSE (to close a host site), QUIT (exits the telnet session completely), STATUS, and a few others.

## traceroute

```bash
traceroute [options] destination_host
```

The traceroute command allows you to determine how long a packet takes to make each hop along the way to the destination host. This is very helpful information when a transmission to that host is significantly delayed or not received at all. Each intermediate host is listed with the time (in milliseconds) that the hop took. Listing 4.7 shows sample output.

### Listing 4.7 Sample Output from the traceroute command

```
traceroute 216.15.152.66 (216.15.152.66), 30 hops max, 38 bytes packets
1 lvhun1.popsite.net (216.126.175.4) 107.606 ms 98.544 ms 99.231 ms
2 bhm1-core1.popsite.net (216.126.175.1) 106.141 ms 109.084 ms 109.090 ms
3 atl-core1-s1-3.popsite.net (216.126.168.221) 116.211 ms 108.875 ms 109.361 ms
```
