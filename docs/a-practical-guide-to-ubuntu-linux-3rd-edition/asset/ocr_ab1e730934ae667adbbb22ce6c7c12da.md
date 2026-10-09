The A resource record for `localhost` is followed by two CNAME resource records that specify `www(sam.net.)` and `ftp(sam.net.)` as aliases for the nameserver `ns.sam.net.`. For example, a user connecting to `ftp.sam.net` will connect to `192.168.0.6`. The resource records named `gw`, `ns`, `mark`, and `mail` are resource records for domains within the `sam.net` zone.

Before restarting `named`, create the directory for the log files and give it permissions and ownership as shown below. If you are running `named` in a chroot jail, create the `bind` directory in `/var/lib/named/var/log`.

```
$ sudo mkdir /var/log/bind
$ sudo chown bind:bind /var/log/bind
$ ls -ld /var/log/bind
drwxr-xr-x 2 bind bind 4096 2010-04-26 17:43 /var/log/bind
```

With the log directory in place, and the `named.conf`, `db.root`, `named.conf.local`, and `sam.net` zone files in `/etc/bind` (or in `/var/lib/named/etc/bind` if you are running `named` in a chroot jail), restart `named` and check the log files. The file `/var/log/syslog` should show something like the following (the example shows `named` started in a chroot jail):

```
# cat /var/log/syslog
***
Apr 26 18:05:19 plum named[22119]:  9.7.0-P1 -u bind -t /var/lib/named
Apr 26 18:05:19 plum named[22119]:  found 1 CPU, using 1 worker thread
Apr 26 18:05:19 plum named[22119]:  loading configuration from '/etc/bind/named.conf'
Apr 26 18:05:19 plum named[22119]:  listening on IPv4 interface lo, 127.0.0.1#53
Apr 26 18:05:19 plum named[22119]:  listening on IPv4 interface eth0, 192.168.0.10#53
Apr 26 18:05:19 plum named[22119]:  command channel listening on 127.0.0.1#953
Apr 26 18:05:19 plum named[22119]:  command channel listening on ::1#953
***
```

The `misc.log` file may show errors that do not appear in the syslog file:

```
# cat /var/log/bind/misc.log
... 01:05:19.932 general:  info:  zone 0.168.192.in-addr.arpa./IN:  loaded serial 1010110501
... 01:05:19.933 general:  info:  zone sam.net./IN:  loaded serial 1010110501
... 01:05:19.933 general:  notice:  running
```

# A SLAVE SERVER

To set up a slave server, copy the `/etc/bind/named.conf` file from the master server to the slave server, replacing the **type master** statement with **type slave** and adding a **masters ( 1.2.3.4; );** directive. Remove any zones the slave server will not be acting as a slave for, including the root (.) zone, if the slave server will not respond to recursive queries. If necessary, create the `/var/log/bind` directory for log files as explained at the end of the previous section.

Slave servers copy zone information from the primary master server or another slave server. The **notify** statement specifies whether you want a master server to notify slave servers when information on the master server changes. Set the (global)