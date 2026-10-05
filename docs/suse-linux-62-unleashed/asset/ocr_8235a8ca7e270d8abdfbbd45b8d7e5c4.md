# Networking and Internet Services
PART II

# Note

portmap is not started on NFS client machines at boot time unless you have set thenenvironment properly in /etc/rc.config. This can be set by editing the file directly
or by using yast.

Using your editor of choice, find the line

```
START_PORTMAP="no"
```

and change it to read

```
START_PORTMAP="yes"
```

For NFS servers, you can ignore the START_PORTMAP variable in /etc/rc.config and
instead set

```
NFS_SERVER="yes"
```

If the correct variable is set in /etc/rc.config (see the previous Note), these programs
start at boot time. To check for this, use the rpcinfo command as follows:

```
rpcinfo -p
```

This will display all the registered RPC programs running on your system:

```
[root@vestax /root]# rpcinfo -p
program vers proto port
100000 2 tcp 111 rpcbind
100000 2 udp 111 rpcbind
```

To check which RPC programs are registered on a remote host, use rpcinfo, such as
rpcinfo -p hostname

where hostname is the name of the remote host you want to check. The output for a Linux
host running NFS appears something like the following:

```
[root@vestax /root]# rpcinfo -p gentoo
program vers proto port
100000 2 tcp 111 portmapper
100000 2 udp 111 portmapper
100005 1 udp 821 mountd
100005 1 tcp 823 mountd
100003 2 udp 2049 nfs
100003 2 tcp 2049 nfs
```