```
```text
eric       pts/1    192.168.1.100   Sat Feb 26 09:55 - 09:55  (00:00)
belandja   pts/4    192.168.1.100   Sat Feb 26 09:54 - down     (14:02)
hart       pts/1    192.168.1.100   Sat Feb 26 09:53 - 09:54  (00:01)
root       pts/3    :0.0             Sat Feb 26 09:46 - down     (14:11)
belandja   pts/2    192.168.1.100   Sat Feb 26 09:12 - 10:14  (01:01)
hart       pts/1    192.168.1.100   Sat Feb 26 08:44 - 09:53  (01:08)
root       pts/0    0                Sat Feb 26 08:44 - down     (15:12)

wtmp begins Mon Feb 14 19:00:40 2005
```
```

You can use a separate command to quickly extract the last login times of certain accounts. This can be a quick way to check for unused accounts or accounts that are being used but shouldn't be. Here's an example of the lastlog command:

```
```text
Athena:~ # lastlog
Username         Port     From               Latest
root             pts/2    athena.universal   Sun Feb 27 12:30:43 -0500 2005
bin                       **Never logged in**
daemon                    **Never logged in**
lp                        **Never logged in**
games                     **Never logged in**
man                       **Never logged in**
.                         **Never logged in**
.                         **Never logged in**
ldap                      **Never logged in**
dhcpd                     **Never logged in**
belandja  1      192.168.1.100   Sun Feb 27 12:29:40 -0500 2005
eric      2      192.168.1.100   Sun Feb 27 12:23:43 -0500 2005
hart      1      192.168.1.100   Sat Feb 26 10:08:46 -0500 2005
peter                     **Never logged in**
pol       pts/3  192.168.1.240   Sun Feb 27 14:25:20 -0500 2005
mark      pts/4  hermes.universal Sun Feb 27 14:31:03 -0500 2005
ted       tty5                   Sun Feb 27 14:29:25 -0500 2005
```
```

This command provides a listing of all the accounts on the system as well as the times they were last logged in to the system and the source of the login. Because of the large number of system accounts, the list can grow quite large. You might be tempted to parse the output of this command using grep to remove all accounts that have never been used:

```
```text
Athena:~ # lastlog | grep -v -e "**Never"

Username   Port      From              Latest
root       pts/2     athena.universal  Sun Feb 27 12:30:43 -0500 2005
belandja   1         192.168.1.100     Sun Feb 27 12:29:40 -0500 2005
eric       2         192.168.1.100     Sun Feb 27 02:23:43 -0500 2005
```
```