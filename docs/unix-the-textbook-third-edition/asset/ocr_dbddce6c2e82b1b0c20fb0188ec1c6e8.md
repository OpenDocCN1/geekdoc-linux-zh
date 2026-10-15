Notice that since this session is the first ssh connection from the local client to the remote server host, an exchange of authentication keys is necessary. On every subsequent connection, the key exchange is not necessary if the keys have not been changed.

Using the following command, you log in to a host 192.168.0.13 with username sarwar, use the uname -a command to display the machine information of the server-side machine, log out, and use the uname -a command on the client machine to display information of the client-side machine. Note that there is no exchange of authentication keys because this is not the first ssh connection between the client and server machines.

```
% ssh -l sarwar 192.168.0.13
Password:
Last login: Sun Oct 12 17:32:20 2014 from 202.147.169.196
Oracle Corporation    SunOS 5.11    11.2    June 2014
$ uname -a
SunOS solaris srv 5.11 11.2 i86pc i386 i86pc
$ logout
Connection to 202.147.169.197 closed.
% uname -a
FreeBSD pcbsd-srv 10.0-RELEASE-p6 FreeBSD 10.0-RELEASE-p6 #0
acf484b(releng/10.0) : Mon Feb 24 15:14:38 EST 2014    root@
avenger:/usr/obj/root/pcbsd-build-10.0-EDGE/git/freebsd/sys/
GENERIC    amd64
%
```

We now discuss remote execution of commands with ssh. All of the rsh commands discussed in Section 11.8.7 will work if you replace rsh with ssh. Here are some additional commands. The following command executes the ps -A | grep d$ command on the remote server host 192.168.0.13 (a Solaris machine) and displays (on the local client machine) the status of all the daemons on that remote host. As shown, you will be prompted for a password because of the default configuration of ssh.

```
% ssh 192.168.0.13 ps -A | grep d$
Password: xxxxxx
0 ?        0:00 sched
7 ?        0:03 intrd
47 ?       0:09 dimgmtd
304 ?      0:00 nwamd
535 ?      4:14 syslogd
39 ?       0:09 netcfd
66 ?       3:20 kcfd
518 ?      0:00 hald-add
76 ?       0:38 ipmgmtd
93 ?       0:00 pfexecd
478 ?      0:00 in.ndpd
16991 ?    0:00 sshd
```