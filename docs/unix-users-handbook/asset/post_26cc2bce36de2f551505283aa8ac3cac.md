
netstat example provides network interface information every five seconds.

```
# netstat -I lan0 5
(lan0)-> input                 output            (Total)-> input          output
       packets errs  packets errs colls         packets errs  packets errs colls
      3590505   2  45714    0  104         3590737   2  45946    0  104
          134   0      5    0   0             134   0      5    0   0
          174   0      0    0   0             174   0      0    0   0
          210   0     13    0   0             210   0     13    0   0
          165   0      0    0   0             165   0      0    0   0
          169   0      0    0   0             169   0      0    0   0
          193   0      0    0   0             193   0      0    0   0
          261   0      7    0   0             261   0      7    0   0
          142   0      8    0   0             142   0      8    0   0
          118   0      0    0   0             118   0      0    0   0
          143   0      0    0   0             143   0      0    0   0
          149   0      0    0   0             149   0      0    0   0
```

With this example, you get multiple outputs of what is taking place on the LAN interface. As I mentioned earlier, you may want to ignore the first output, because it includes information over a long time period. This may include a time when your network was idle, and therefore the data is not important to you.

You can specify the network interface on which you want statistics reported by using **-I interface**; in the case of the example, it was **-I lan0**. An interval of five seconds was also used in this example.

Yet another use of netstat is to show the state of network sockets. netstat -a produces a list of protocols, queues, local and remote addresses, and protocol states. All this information is useful for showing active communications, as shown in the following example:

```
# netstat -a
Active Internet connections (including servers)
Proto Recv-Q Send-Q   Local Address           Foreign Address         (state)
tcp   0    0      2 system1.tenet.atlm0061.atl.hp..1319 ESTABLISHED
tcp   0    0      * *                       LISTEN
tcp   0    0   *.psmond   * *             LISTEN
tcp   0    0  *.mcsemon   * *             LISTEN
tcp   0    0  localhost.8886  localhost.1062 ESTABLISHED
tcp   0    0  localhost.8886  localhost.8886 ESTABLISHED
tcp   0    0     *.8886  * *             LISTEN
tcp   0    0     *.8887  * *             LISTEN
tcp   0    0     *.1006  * *             LISTEN
tcp   0    0     *.978   * *             LISTEN
tcp   0    0    *.22370  * *             LISTEN
tcp   0    0     *.389   * *             LISTEN
tcp   0    0     *.8181  * *             LISTEN
tcp   0    0     *.1054  * *             LISTEN
tcp   0    0     *.1053  * *             LISTEN
tcp   0    0 *.diagmond  * *             LISTEN
tcp   0    0     *.1045  * *             LISTEN
tcp   0    0     *.1038  * *             LISTEN
tcp   0    0     *.135   * *             LISTEN
tcp   0    0     *.smtp  * *             LISTEN
tcp        0      0  *.1036                 *.*                     LISTEN
tcp        0      0  *.appconn              *.*                     LISTEN
tcp        0      0  *.spc                  *.*                     LISTEN
tcp        0      0  *.dtsc                 *.*                     LISTEN
tcp        0      0  *.recserv              *.*                     LISTEN
tcp        0      0  *.klogin               *.*                     LISTEN
tcp        0      0  *.kshell               *.*                     LISTEN
tcp        0      0  *.chargen              *.*                     LISTEN
tcp        0      0  *.discard              *.*                     LISTEN
tcp        0      0  *.echo                 *.*                     LISTEN
tcp        0      0  *.time                 *.*                     LISTEN
tcp        0      0  *.daytime              *.*                     LISTEN
tcp        0      0  *.printer                *.*                     LISTEN
tcp        0      0  *.auth                 *.*                     LISTEN
tcp        0      0  *.exec                 *.*                     LISTEN
tcp        0      0  *.shell                *.*                     LISTEN
tcp        0      0  *.login                *.*                     LISTEN
tcp        0      0  *.telnet               *.*                     LISTEN
tcp        0      0  *.ftp                  *.*                     LISTEN
tcp        0      0  *.795                  *.*                     LISTEN
tcp        0      0  *.792                  *.*                     LISTEN
tcp        0      0  *.*                    *.*                     CLOSED
tcp        0      0  *.787                  *.*                     LISTEN
tcp        0      0  *.783                  *.*                     LISTEN
tcp        0      0  *.779                  *.*                     LISTEN
tcp        0      0  *.portmap              *.*                     LISTEN
tcp        0      0  *.2121                 *.*                     LISTEN
tcp        0      0  *.1121                 *.*                     LISTEN
udp        0      0  *.177                  *.*
udp        0      0  *.1003                 *.*
udp        0      0  *.*
udp        0      0  *.*
udp        0      0  *.*
udp        0      0  *.*
udp        0      0  *.nfsd                 *.*
udp        0      0  *.976                  *.*
udp        0      0  *.22370                *.*
udp        0      0  *.1097                 *.*
udp        0      0  *.1095                 *.*
udp        0      0  *.1079                 *.*
udp        0      0  *.135                  *.*
udp        0      0  *.*
udp        0      0  *.1045                 *.*
udp        0      0  *.snmp                 *.*
udp        0      0  *.1040                 *.*
udp        0      0  *.tftp                 *.*
udp        0      0  *.chargen              *.*
udp        0      0  *.discard              *.*
udp        0      0  *.echo                 *.*
udp        0      0  *.time                 *.*
udp        0      0  *.daytime              *.*
udp        0      0  *.ntalk                *.*
udp        0      0  *.bootps               *.*
udp        0      0  *.1023                 *.*
udp        0      0  *.787                  *.*
udp        0      0  *.798                  *.*
udp        0      0  *.797                  *.*
udp        0      0  *.1037                 *.*
udp        0      0  *.*
udp        0      0  *.1036                 *.*
udp        0      0  *.1035                 *.*
udp        0      0  *.777                  *.*
udp        0      0  *.portmap              *.*
udp        0      0  *.1034                 *.*
udp        0      0  *.syslog               *.*
udp        0      0  *.2121                 *.*
Active UNIX domain sockets
Address      Type    Recv-Q Send-Q Inode    Conn     Refs  Nextref Addr
bb9c00       stream  0      0      af9000   0        0     0     /tmp/.AgentSoA
ced700       dgram   0      0      c99400   0        0     0     /opt/dcelocalr
c000         dgram   0      0      d23000   0        0     0     /opt/dcelocalr
b04200       dgram   0      0      b87000   0        0     0     /opt/dcelocalr
997a00       stream  0      0      b84800   0        0     0     /opt/dcelocal1
b24e00       dgram   0      0      b84000   0        0     0     /opt/dcelocal1
d59400       dgram   0      0      b66400   0        0     0     /var/tmp/psb_t
d85c00 dgram 0 0 b67000 0 0 0 /var/tmp/psb_t
c88200 dgram 0 0 b12000 0 0 0 /opt/dclocal1r
c88400 stream 0 0 b78400 0 0 0 /opt/dclocal15
c8b300 dgram 0 0 b78000 0 0 0 /opt/dclocal15
c90900 dgram 0 0 d22400 0 0 0 /opt/dclocal1r
c78c00 dgram 0 0 ba1000 c4a180 0 0 /opt/dclocal10
b1e900 dgram 0 0 9a4400 0 c32e80 0 /opt/dclocald
d64100 stream 0 0 d24c00 0 0 0 /opt/dclocal15
9e1600 dgram 0 0 9a4000 d4d940 0 0 /opt/dclocal12
d64200 dgram 0 0 cfc800 0 c32c80 0 /opt/dclocal19
d12d00 dgram 0 0 cfc000 c32c00 0 0 /opt/dclocal11
c5ee00 stream 0 0 b1c000 0 0 0 /opt/dclocal14
d19d00 dgram 0 0 ce4800 0 0 0 /opt/dclocald
cf0c00 dgram 0 0 a92800 0 af15c0 0 /opt/dclocal17
d2d600 dgram 0 0 a93800 c32c00 0 d4db80 /opt/dclocal10
c9b900 dgram 0 0 a93c00 0 0 0 /opt/dclocald
d6c800 stream 0 0 ba3000 0 0 0 /var/opt/OV/st
# 
```

A lot of information is in this output. You can refer to the manual page at the end of this chapter if you want a detailed explanation of any of the fields.

The first line shows the Proto tcp to the Local Address system1.telnet as having a (state) of ESTABLISHED. This is the connection we have initiated to this system. We are sitting on system1 with a telnet session open to the system on which we ran netstat.

Most of the remaining tcp protocol entries are listening. This means that they are listening for incoming connections as indicated by the LISTEN. They have a wildcard in the Foreign Address field, which will contain the address when a connection has been established. We are one of the few connections that has been made, as indicated by the ESTABLISHED.

All the send and receive queues, shown as Recv-Q and Send-Q, are empty as indicated by the 0.

The UNIX domain sockets at the end of the output are stream and datagram connections for a variety of services such as NFS.

This output gives you an appreciation of the immense amount of activity taking place from a networking perspective on your UNIX system. Networking and connectivity have been among the most advanced aspects of UNIX since its inception.
