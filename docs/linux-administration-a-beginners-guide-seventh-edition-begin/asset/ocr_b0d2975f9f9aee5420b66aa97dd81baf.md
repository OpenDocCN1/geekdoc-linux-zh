Notification to the server is unnecessary, because the server doesn't keep track of all clients that have mounted its file systems. Because the server doesn't maintain state information about clients and the clients don't maintain state information about the server, clients and servers can't tell the difference between a crashed system and a really slow system. Thus, if an NFS server is rebooted, ideally all clients should automatically resume their operations with the server as soon as the server is back online.

# Enabling NFS in Fedora, RHEL, and CentOS

Almost all the Linux distributions ship with support for NFS in one form or another. The only task left for the administrator is to configure and enable it. On our sample Fedora system, enabling NFS is easy.

Because NFS version 3 (and lower) and its ancillary programs are RPC-based, first need to make sure that the system rpcbind is installed and running.
First make sure that the rpcbind package is installed on the system. On a Fedora distro, try the following:

```
root@fedora-server ~]# rpm -q rpcbind
```

If the output indicates that the software is not installed, you can use dnf to install it by running this:

```
root@fedora-server ~]# dnf -y install rpcbind
```

To check the status of the rpcbind service installed on systemd-enabled Linux distros like Fedora, you can use the systemctl command:

```
root@fedora-server ~]# systemctl status rpcbind.service
```

If the rpcbind service is stopped, start it like so:

```
root@fedora-server ~]# systemctl start rpcbind.service
```

Before going any further, use the rpcinfo command to view the status of any RPC-based services that might have registered with portmap:

```
root@server ~]# rpcinfo -p
program vers proto service
100000 4 tcp 111 portmapper
100000 4 udp 111 portmapper
<OUTPUT TRUNCATED>...
```

Because we don't have an NFS server running on the sample system, the output may not show many RPC services.
To start the NFS service, you can use the systemctl command on systemd-enabled Linux distros like Fedora by typing

```
root@fedora-server ~]# systemctl start nfs.service
```