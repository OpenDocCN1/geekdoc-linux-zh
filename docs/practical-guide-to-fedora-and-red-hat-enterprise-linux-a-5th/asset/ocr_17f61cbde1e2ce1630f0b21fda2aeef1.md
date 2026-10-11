The A resource record for **localhost** is followed by two CNAME resource records that specify **www.sam.net.** and **ftp.sam.net.** as aliases for the nameserver **ns.sam.net.** For example, a user connecting to ftp.sam.net will connect to 192.168.0.6. The resource records named **gw**, **ns**, **mark**, and **mail** are resource records for domains within the sam.net zone.

**Log files** Before restarting **named**, create the directory for the log files and give it permissions and ownership as shown below. If you are running **named** in a chroot jail, create the **bind** directory in /var/named/chroot/var/log.

```
```
# mkdir /var/log/bind
# chmod 744 /var/log/bind
# chown named /var/log/bind
# ls -ld /var/log/bind
drwx--r-- 2 named root 4096 Nov 5 19:41 /var/log/bind
```
```

With the log directory in place, **named.conf** in /etc (or in /var/named/chroot/etc if you are running **named** in a chroot jail), the **named.ca**, **named.local**, and **sam.net** zone files in /var/named (or in /var/named/chroot/var/named if you are running **named** in a chroot jail), restart **named** and check the log files. The file /var/log/messages should show something like the following:

```
```
# cat /var/log/messages
--
19:25:48 peach named[22416]: starting BIND 9.3.2 -u named -t /var/named/chroot
19:25:48 peach named[22416]: found 1 CPU, using 1 worker thread
19:25:48 peach named[22416]: loading configuration from '/etc/named.conf'
19:25:48 peach named[22416]: listening on IPv4 interface lo, 127.0.0.1#53
19:25:48 peach named[22416]: listening on IPv4 interface eth0, 192.168.0.10#53
19:25:48 peach named[22416]: command channel listening on 127.0.0.1#953
19:25:48 peach named[22416]: command channel listening on ::1#953
```
```

The **misc.log** file may show errors that do not appear in the messages file:

```
```
# cat /var/log/bind/misc.log
19:25:48.077 general: info: zone 0.168.192.in-addr.arpa/IN: loaded serial 2005110501
19:25:48.079 general: info: zone sam.net/IN: loaded serial 200511051
19:25:48.097 general: notice: running
```
```

# # A SLAVE SERVER

To set up a slave server, copy the /etc/named.conf file from the master server to the slave server, replacing the **type master** statement with **type slave**. Remove any zones that the slave server will not be acting as a slave for, including the root (.) zone, if the slave server will not respond to recursive queries. Create the /var/log/bind directory for log files as explained at the end of the previous section.

**notify statement** Slave servers copy zone information from the primary master server or another slave server. The **notify** statement specifies whether you want a master server to notify slave servers when information on the master server changes. Set the (global)