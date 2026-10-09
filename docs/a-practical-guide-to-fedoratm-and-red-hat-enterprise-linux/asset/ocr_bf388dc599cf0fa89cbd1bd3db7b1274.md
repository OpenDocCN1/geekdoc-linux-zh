port=\# The *n* specifies the number of the port used to connect to the NFS server. A 0 causes NFS to query rpcbind on the server to determine the port number. When this option is not specified, NFS uses port 2049.

size=\# (read block size) The *n* specifies the maximum number of bytes read at one time from an NFS server. Refer to “Improving Performance.” Default is negotiated by the client and server and is the largest both can support.

wsize=\# (write block size) The *n* specifies the maximum number of bytes written at one time to an NFS server. Refer to “Improving Performance.” Default is negotiated by the client and server and is the largest both can support.

udp Uses UDP for an NFS mount. Default is tcp.

tcp Uses TCP for an NFS mount. Default is tcp.

# # Improving Performance

hard/soft Several parameters can affect the performance of NFS, especially over slow connections such as a line with a lot of traffic or a line controlled by a modem. If you have a slow connection, make sure **hard** (default; page 809) is set so timeouts do not abort program execution.

Block size One of the easiest ways to improve NFS performance is to increase the block size—that is, the number of bytes NFS transfers at a time. Try to specifying **size** and **wsize** (previous) so the client and server set these options to their maximum values. Experiment until you find the optimal block size. Unmount and mount the directory hierarchy each time you change an option. See the *Linux NFS-HOWTO* at nfs.sourceforge.net/nfshowto for more information on testing different block sizes.

Timeouts NFS waits the amount of time specified by the **timeo** (timeout; page 809) option for a response to a transmission. If it does not receive a response in this amount of time, NFS sends another transmission. The second transmission uses bandwidth that, over a slow connection, might slow things down even more. You might be able to increase performance by increasing **timeo**.

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

The preceding example uses a packet size of 4096 bytes and shows a fast average packet round-trip time of about one-half of a millisecond. Over a modem line, you