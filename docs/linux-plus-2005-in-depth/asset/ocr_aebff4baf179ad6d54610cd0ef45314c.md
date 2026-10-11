receiving a new one, your password expires in 99999 days, and you are warned seven days in advance before your password needs to be changed.

When a password has expired, the user is still allowed to log in to the system for a certain period of time, after which the user is disabled from logging in. The number of days after a password expires that a user account is disabled is represented by the disable2 field in /etc/shadow. In addition, you can choose to disable a user from logging in at a certain date, such as the end of an employment contract. The disable2 field in /etc/shadow represents the number of days since January 1, 1970, that a user account will be disabled.

An example /etc/shadow file is shown next:

```
[root@server1 root]# cat /etc/shadow
root:$1$Py5hQF6$Fx9nLNB70kZ.Gm\6lR.F/:0:99999:7:::
bin:*:12617:0:99999:7:::
daemon:!!:12617:0:99999:7:::
adm:!!:12617:0:99999:7:::
lp:!!:12617:0:99999:7:::
sync:!!:12617:0:99999:7:::
shutdown:!!:12617:0:99999:7:::
halt:!!:12617:0:99999:7:::
mail:!!:12617:0:99999:7:::
news:!!:12617:0:99999:7:::
uucp:!!:12617:0:99999:7:::
operator:!!:12617:0:99999:7:::
games:!!:12617:0:99999:7:::
gopher:!!:12617:0:99999:7:::
ftp:!!:12617:0:99999:7:::
nobody:!!:12617:0:99999:7:::
rpm:!!:12617:0:99999:7:::
vcsa:!!:12617:0:99999:7:::
nsccd:!!:12617:0:99999:7:::
sshd:!!:12617:0:99999:7:::
idemnt:!!:12617:0:99999:7:::
rpc:!!:12617:0:99999:7:::
rpcuser:!!:12617:0:99999:7:::
nfsnobody:!!:12617:0:99999:7:::
pcap:!!:12617:0:99999:7:::
mailnull:!!:12617:0:99999:7:::
smsqp:!!:12617:0:99999:7:::
apache:!!:12617:0:99999:7:::
squid:!!:12617:0:99999:7:::
webalizer:!!:12617:0:99999:7:::
dbus:!!:12617:0:99999:7:::
xfs:!!:12617:0:99999:7:::
```