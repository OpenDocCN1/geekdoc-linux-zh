# Installing NFS

Before you begin installing NFS, make sure that your network setup is functioning correctly and that the server and clients can ping each other. Setting up your network is explained in Chapter 20, “TCP/IP Network Management.”

Although the NFS software comes preinstalled with Red Hat Linux, you need to be aware of what the software is and what each specific program does. This is important when you are troubleshooting problems and configuring NFS-related tools such as the automounter.

Three programs provide NFS server services:

+   • rpc.portmapper—This program does not directly provide NFS services itself; however, it maps calls made from other machines to the correct NFS daemons.

+   • rpc.nfsd—This daemon translates the NFS requests into actual requests on the local filesystem.

+   • rpc.mountd—This daemon services requests to mount and unmount filesystems.

# Note

The rpc.nfsd and rpc.mountd programs need only run on your NFS servers. In fact, you might find it prudent not to run them at all on your client machines, for security concerns and to free resources that might otherwise be consumed by them. NFS clients do not need any special NFS software to run. They should run the rpc.portmapper program, however, because it provides RPC functionality to programs other than NFS.

By default, these programs are installed and loaded at boot time. To check for this, use the rpcinfo command as follows:

```
rpcinfo -p
```

This will display all the registered RPC programs running on your system. To check which RPC programs are registered on a remote host, use

```
rpcinfo -p hostname
```

where hostname is the name of the remote host you want to check. The output for a Linux host running NFS looks something like the following:

```
[root@vexstar /root]# rpcinfo -p
program    vers   proto   port
100000      2    tcp  111  portmapper
100000      2    udp  111  portmapper
```