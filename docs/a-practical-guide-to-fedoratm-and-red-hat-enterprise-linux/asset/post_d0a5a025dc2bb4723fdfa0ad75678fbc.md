
acregmax=n (attribute cache regular file maximum) The n is the number of seconds, at a maximum, that NFS waits before refreshing regular file attributes. Default is 60 seconds.

acregmin=n (attribute cache regular file minimum) The n is the number of seconds, at a minimum, that NFS waits before refreshing regular file attributes. Default is 3 seconds.

actimeo=n (attribute cache timeout) Sets acregmin, acregmax, acdirmin, and acdirmax to n seconds. Without this option, each individual option takes on its assigned or default value.

# ERROR HANDLING

The following options control what NFS does when the server does not respond or when an I/O error occurs. To allow for a mount point located on a mounted device, a missing mount point is treated as a timeout.

- fg (bg) (foreground) Exits with an error status if a foreground NFS mount fails. The bg (background) option retries failed NFS mount attempts in the background. Default is fg.
- hard (soft) With the hard option, NFS retries indefinitely when an NFS request times out. With the soft option, NFS retries the connection retrans times and then reports an I/O error to the calling program. In general, it is not advisable to use soft. As the mount man page says of soft, “Usually it just causes lots of trouble.” For more information refer to “Improving Performance” on page 810. Default is hard.
- retrans=n (retransmission value) NFS generates a server not responding message after n timeouts. NFS continues trying after n timeouts if hard is set and fails if soft is set. Default is 3.
- retry=n (retry value) The number of minutes that NFS retries a mount operation before giving up. Set to 0 to cause mount to exit immediately if it fails. Default is 2 minutes for foreground mounts (fg) and 10,000 minutes for background mounts (bg).
- timeo=n (timeout value) The n is the number of tenths of a second NFS waits for a response before retransmitting. For NFS over TCP, the default is 600 (60 seconds). See the nfs man page for information about the defaults used by NFS over UDP. On a busy network, in case of a slow server, or when the request passes through multiple routers, increasing this value might improve performance. See “Timeouts” on the next page for more information.

# MISCELLANEOUS OPTIONS

Following are additional useful options:

- lock (nolock) Permits NFS locking. The nolock option disables NFS locking and is useful with older servers that do not support NFS locking. Default is lock.
- nfsvers=n The n specifies the NFS version number used to contact the NFS server (2, 3, or 4). The mount fails if the server does not support the specified version. By default, the client negotiates the version number, starting with 4, followed by 3 and then 2.
- port=n The n specifies the number of the port used to connect to the NFS server. A 0 causes NFS to query rpcbind on the server to determine the port number. When this option is not specified, NFS uses port 2049.
- size=n (read block size) The n specifies the maximum number of bytes read at one time from an NFS server. Refer to “Improving Performance.” Default is negotiated by the client and server and is the largest both can support.
- wsize=n (write block size) The n specifies the maximum number of bytes written at one time to an NFS server. Refer to “Improving Performance.” Default is negotiated by the client and server and is the largest both can support.
- udp Uses UDP for an NFS mount. Default is tcp.
- tcp Uses TCP for an NFS mount. Default is tcp.

## Improving Performance

- hard/soft Several parameters can affect the performance of NFS, especially over slow connections such as a line with a lot of traffic or a line controlled by a modem. If you have a slow connection, make sure **hard** (default; page 809) is set so timeouts do not abort program execution.
- Block size One of the easiest ways to improve NFS performance is to increase the block size—that is, the number of bytes NFS transfers at a time. Try to specifying **size** and **wsize** (previous) so the client and server set these options to their maximum values. Experiment until you find the optimal block size. Unmount and mount the directory hierarchy each time you change an option. See the *Linux NFS-HOWTO* at nfs.sourceforge.net/nfshowto for more information on testing different block sizes.
- Timeouts NFS waits the amount of time specified by the **timeo** (timeout; page 809) option for a response to a transmission. If it does not receive a response in this amount of time, NFS sends another transmission. The second transmission uses bandwidth that, over a slow connection, might slow things down even more. You might be able to increase performance by increasing **timeo**.

You can test the speed of a connection with the size of packets you are sending (**size** and **wsize**, both above) by using **ping** with the -s (*size*) option. The -c (*count*) option specifies the number of transmissions **ping** sends.

```
$ ping -s 4096 -c 4 plum
PING plum (192.168.206.181) 4096(4124) bytes of data.
4104 bytes from plum (192.168.206.181): icmp_seq=1 ttl=64 time=0.460 ms
4104 bytes from plum (192.168.206.181): icmp_seq=2 ttl=64 time=0.319 ms
4104 bytes from plum (192.168.206.181): icmp_seq=3 ttl=64 time=0.372 ms
4104 bytes from plum (192.168.206.181): icmp_seq=4 ttl=64 time=0.347 ms
--- plum ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3000ms
rtt min/avg/max/mdev = 0.319/0.374/0.460/0.056 ms
```

The preceding example uses a packet size of 4096 bytes and shows a fast average packet round-trip time of about one-half of a millisecond. Over a modem line, you can expect times of several seconds. If the connection is dealing with other traffic, the time will be even longer. Run the test during a period of heavy traffic. Try increasing timeo to three or four times the average round-trip time (to allow for unusually bad network conditions, such as when the connection is made) and see whether performance improves. Remember that the timeo value is given in tenths of a second (100 milliseconds = one-tenth of a second).

## /etc/fstab: MOUNTS DIRECTORY HIERARCHIES AUTOMATICALLY

The `/etc/fstab` file (page 524) lists directory hierarchies that the system might mount automatically as it comes up. You can use the options discussed in the preceding sections on the command line or in the fstab file.

The following line from the fstab file on guava mounts the `/home/public` directory from plumb on the `/plum.public` mount point on guava:

```
plumb:/home/public /plum.public nfs4 rsize=8192,wsize=819200
```

A mount point should be an empty, local directory. (Files in a mount point are hidden when a directory hierarchy is mounted on it.) The type of a filesystem mounted using NFS is always nfs4, regardless of its type on its local system. You can increase the rsize and wsize options to improve performance. Refer to “Improving Performance” on page 810.

The next example from fstab mounts a filesystem from dog:

```
dog:/export /dog.export nfs4 timeo=50,hard 0 0
```

Because the local system connects to dog over a slow connection, timeo is increased to 5 seconds (50-tenths of a second). Refer to “Timeouts” on page 810. In addition, hard is set to make sure NFS keeps trying to communicate with the server after a major timeout. Refer to hard/soft on page 810.

The final example from fstab shows a remote-mounted home directory. Because dog is a local server and is connected via a reliable, high-speed connection, timeo is decreased and rsize and wsize are increased substantially:

```
dog:/home /dog.home nfs4 timeo=4,rsize=16384,wsize=16384 0 0
```

## SETTING UP AN NFS SERVER

### PREREQUISITES

Install the following packages:

- nfs-utils (installed by default)
- rpcbind (installed by default; not needed for NFSv4)
- system-config-nfs (Fedora; optional)

Check rpcbind is running A new Fedora/RHEL system boots with **rpcbind** installed and running; For NFSv3 only (not NFSv4) **rpcbind** must be running before you can start the **nfs** service. Use the **systemctl** status command to make sure **rpcbind** is running.

```
$ systemctl status rpcbind.service
```

Enable and start nfs Run **systemctl** to cause the **nfs** service to start each time the system enters multiuser mode and then start the **nfs** service. Use the **systemctl** status command to make sure the service is running.

```
# systemctl enable nfs-server.service
# systemctl start nfs-server.service
```

After modifying nfs configuration files, give the second command again, replacing start with reload to cause nfs to reread those files.

### NOTES

**Troubleshooting** See page 819 for a list of error messages and troubleshooting tips.

**SELinux** When SELinux is set to use a targeted policy, NFS is protected by SELinux. You can disable this protection if necessary. For more information refer to “Setting the Targeted Policy with **system-config-selinux**” on page 476.

**Firewall** When NFSv4 is using AUTH_SYS authentication, as it does by default, it uses port 2049. When NFS is using **rpcbind** to assign a port, which NFSv4 does not do by default, it uses port 111. If the NFS server system is running a firewall or is behind a firewall, you must open one or both of these ports. Give the following commands to open the ports each time the system boots (permanently) and on the running system; see page 906 for information on **firewall-cmd**.

```
# firewall-cmd --add-port=2049/tcp
# firewall-cmd --permanent --add-port=2049/tcp
# firewall-cmd --add-port=2049/udp
# firewall-cmd --permanent --add-port=2049/udp
# firewall-cmd --add-port=111/tcp # not usually needed
# firewall-cmd --permanent --add-port=111/tcp # not usually needed
# firewall-cmd --add-port=111/udp # not usually needed
# firewall-cmd --permanent --add-port=111/udp # not usually needed
```

**Security** NFSv3 (and not NFSv4) uses TCP wrappers to control client access to the server. As explained on page 486, you can set up /etc/hosts.allow and /etc/hosts.deny files to specify which clients can contact rpc.mountd on the server and thereby use NFSv3. The name of the daemon to use in these files is **mountd**.

## JUMPSTART II: CONFIGURING AN NFS SERVER USING system-config-nfs (FEDORA)

Open the NFS Server Configuration window (Figure 22-2) by giving the command **system-config-nfs** from an Enter a Command window (**ALT**+**F2**) or a terminal emulator. From this window you can generate an /etc/exports file, which is almost all there is to setting up an NFS server. If the system is running a firewall, see “Firewall” in the
