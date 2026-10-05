# SETTING UP A SERVER 463

-b (broadcast) Makes an RPC broadcast to version of program and lists hosts that respond.

-d (delete) Removes RPC registration for version of program. Available to a user running with root privileges only.

-n (port number) With -t or -u, uses the port numbered port instead of the port number specified by portmap.

-p (probe) Lists all RPC programs registered, with portmap on host or on the local system when you do not specify host.

-t (TCP) Makes a TCP RPC call to version (if specified) of program and host reports whether it receives a response

-u (UDP) Makes a UDP RPC call to version (if specified) of program and host reports whether it receives a response

For example, the following command displays the RPC programs registered with the portmap daemon on the system plum:

```
$ rpcinfo -p plum
program vers proto port
100000 tcp 111 portmap
100000 udp 111 portmap
100003 udp 2049 nfs
100003 udp 2049 nfs
100004 udp 2049 nfs
100021 udp 32768 nockmanager
```

... Use the -option to display a list of versions of a daemon, such as nfs, registered on a remote system (plum):

```
$ rpcinfo -u plum nfs
program 100003 version 2 ready and waiting
program 100003 version 3 ready and waiting
program 100003 version 4 ready and waiting
```

Specify localhost to display a list of versions of a daemon registered on the local system:

```
$ rpcinfo -u localhost ybind
program 100007 version 1 ready and waiting
program 100007 version 2 ready and waiting
```

Locking down Because the portmap daemon holds information about which servers are running on the local system and which port each running on, only trusted systems should have access to this information. One way to ensure only selected systems have access to portmap is to lock it down in /etc/hosts.allow and /etc/hosts.deny files (page 465). Put the following line in hosts.deny to prevent all systems from using portmap on the local (server) system:

```
portmap: ALL
```