
## ERROR HANDLING

The following options control what NFS does when the server does not respond or when an I/O error occurs. To allow for a mount point located on a mounted device, a missing mount point is treated as a timeout.

- **fg** (**bg**) (foreground) Retries failed NFS mount attempts in the foreground (default). The **bg** (background) option retries failed NFS mount attempts in the background.
- **hard** (**soft**) Displays **NFS server not responding** on the console on a major timeout and keeps retrying (default). The **soft** option reports an I/O error to the calling program on a major timeout. In general, it is not advisable to use **soft**. As the mount man page says of **soft**, "Usually it just causes lots of trouble." For more information refer to "Improving Performance" on page 780.
- **nointr** (**intr**) (**no** interrupt) Does not allow a signal to interrupt a file operation on a hard-mounted directory hierarchy when a major timeout (see retrans) occurs (default). The **intr** option allows this type of interrupt.
- **retrans**=n (**retransmission value**) After n minor timeouts, NFS generates a major timeout (default is 3). A major timeout aborts the operation or displays **server not responding** on the console, depending on whether **hard** or **soft** is set.
- **retry**=n (**retry value**) The number of minutes that NFS retries a mount operation before giving up (default is 10,000).
- **timeo**=n (**timeout value**) The n is the number of tenths of a second that NFS waits before retransmitting following an RPC, or minor, timeout (default is 7). The value is increased at each timeout to a maximum of 60 seconds or until a major timeout occurs (see retrans). On a busy network, in case of a slow server, or when the request passes through multiple routers, increasing this value may improve performance. See “Timeouts” below for more information.

## MISCELLANEOUS OPTIONS

Following are additional useful options:

- **lock** (**no**lock) Permits NFS locking (default). The **no**lock option disables NFS locking (does not start the **lockd** daemon) and is useful with older servers that do not support NFS locking.
- **nodev** (no device) Causes mounted device files not to function as devices (page 777).
- **port**=n The port used to connect to the NFS server (defaults to 2049 if the NFS daemon is not registered with portmap). When n is set to 0 (default), NFS queries **portmap** on the server to determine the port.
- **rsize**=n (read block size) The number of bytes read at one time from an NFS server. The default block size is 4096. Refer to “Improving Performance.”
- **wsize**=n (write block size) The number of bytes written at one time to an NFS server. The default block size is 4096. Refer to “Improving Performance.”
- **tcp** Uses TCP in place of the default UDP protocol for an NFS mount. This option may improve performance on a congested network; however, some NFS servers support UDP only.
- **udp** Uses the default UDP protocol for an NFS mount.

## IMPROVING PERFORMANCE

- **hard/soft** Several parameters can affect the performance of NFS, especially over slow connections such as a line with a lot of traffic or a line controlled by a modem. If you have a slow connection, make sure **hard** (page 779) is set (this setting is the default) so that timeouts do not abort program execution.
- **Block size** One of the easiest ways to improve NFS performance is to increase the block size—that is, the number of bytes NFS transfers at a time. The default of 4096 is low for a fast connection using modern hardware. Try increasing **rsize** and **wsize** (both above) to 8192 or higher. Experiment until you find the optimal block size. Unmount and mount the directory hierarchy each time you change an option. See the *Linux NFS-HOWTO* for more information on testing different block sizes.
- **Timeouts** NFS waits the amount of time specified by the **timeo** (timeout, page 779) option for a response to a transmission. If it does not receive a response in this amount of time, NFS sends another transmission. The second transmission uses bandwidth that, over a slow connection, may slow things down even more. You may be able to increase performance by increasing **timeo**.

The default value of **timeo** is seven-tenths of a second (700 milliseconds). After a timeout, NFS doubles the time it waits to 1400 milliseconds. On each timeout it doubles the amount of time it waits to a maximum of 60 seconds. You can test the speed of a connection with the size of packets you are sending (rsize and wsize; both on page 780) by using ping with the -s (size) option:

```bash
$ ping -s 4096 dog
PING dog (192.168.0.12) 4096(4124) bytes of data.
4104 bytes from dog (192.168.0.12): icmp_seq=1 ttl=64 time=0.823 ms
4104 bytes from dog (192.168.0.12): icmp_seq=2 ttl=64 time=0.814 ms
4104 bytes from dog (192.168.0.12): icmp_seq=3 ttl=64 time=0.810 ms
...
4104 bytes from dog (192.168.0.12): icmp_seq=28 ttl=64 time=0.802 ms
4104 bytes from dog (192.168.0.12): icmp_seq=29 ttl=64 time=0.802 ms
4104 bytes from dog (192.168.0.12): icmp_seq=30 ttl=64 time=0.801 ms
--- dog.bogus.com ping statistics ---
30 packets transmitted, 30 received, 0% packet loss, time 28999ms
rtt min/avg/max/mdev = 0.797/0.803/0.823/0.020 ms
```

The preceding example uses Ubuntu Linux’s default packet size of 4096 bytes and shows a fast average packet round-trip time of slightly less than 1 millisecond. Over a modem line, you can expect times of several seconds. If the connection is dealing with other traffic, the time will be even longer. Run the test during a period of heavy traffic. Try increasing **timeo** to three or four times the average round-trip time (to allow for unusually bad network conditions, such as when the connection is made) and see whether performance improves. Remember that the **timeo** value is given in tenths of a second (100 milliseconds = one-tenth of a second).

## /etc/fstab: MOUNTS DIRECTORY HIERARCHIES AUTOMATICALLY

The /etc/fstab file (page 510) lists directory hierarchies that the system mounts automatically as it comes up. You can use the options discussed in the preceding sections on the command line or in the fstab file.

The following line from **fstab** mounts **grape’s /gc1** filesystem on the **/grape.gc1** mount point:

```bash
grape:/gc1 /grape.gc1 nfs rsize=8192,wsize=8192 0 0
```

A mount point should be an empty, local directory. (Files in a mount point are hidden when a directory hierarchy is mounted on it.) The type of a filesystem mounted using NFS is always nfs, regardless of its type on its local system. You can increase the rsize and wsize options to improve performance. Refer to “Improving Performance” on page 780.

The next example from **fstab** mounts a filesystem from **dog**:

```bash
dog:/export /dog.export nfs timeo=50,hard 0 0
```

Because the local system connects to **dog** over a slow connection, **timeo** is increased to 5 seconds (50-tenths of a second). Refer to “Timeouts” on page 780. In addition, **hard** is set to make sure NFS keeps trying to communicate with the server after a major timeout. Refer to “hard/soft” on page 780.
