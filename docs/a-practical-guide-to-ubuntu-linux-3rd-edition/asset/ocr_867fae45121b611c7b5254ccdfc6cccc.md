+   * **-b (broadcast)** Makes an RPC broadcast to *version of program* and lists those hosts that respond.
+   * **-d (delete)** Removes local RPC registration for *version of program*. Available to a user running with root privileges only.
+   * **-n (port number)** With `\-t` or `\-u`, uses the port numbered *port* instead of the port number specified by **portmap**.
+   * **-p (probe)** Lists all RPC programs registered, with **portmap** on *host* or on the local system when you do not specify *host*.
+   * **-t (TCP)** Makes a TCP RPC call to *version* (if specified) of *program* on *host* and reports whether it receives a response.
+   * **-u (UDP)** Makes a UDP RPC call to *version* (if specified) of *program* on *host* and reports whether it receives a response.

For example, the following command displays the RPC programs registered with the **portmap** daemon on the system named *plum*:

```
$ rpcinfo -p plum

program      vers  proto  port
100000       2     tcp    111 portmapper
100000       2     udp    111 portmapper
100003       2     udp    2049 nfs
100003       3     udp    2049 nfs
100003       4     udp    2049 nfs
100021       1     udp    32768 lockmgr
...
```

Use the `\-u` option to display a list of versions of a daemon, such as *nfs*, registered on a remote system (*plum*):

```
$ rpcinfo -u plum nfs
program 100003 version 2 ready and waiting
program 100003 version 3 ready and waiting
program 100003 version 4 ready and waiting
```

Specify *localhost* to display a list of versions of a daemon registered on the local system:

```
$ rpcinfo -u localhost ypbind
program 100007 version 1 ready and waiting
program 100007 version 2 ready and waiting
```

Because the **portmap** daemon holds information about which servers are running on the local system and which port each server is running on, only trusted systems should have access to this information. One way to ensure only selected systems have access to **portmap** is to lock it down in the */etc/hosts.allow* and */etc/hosts.deny* files (page 465). Put the following line in *hosts.deny* to prevent all systems from using portmap on the local (server) system:

```
portmap: ALL
```