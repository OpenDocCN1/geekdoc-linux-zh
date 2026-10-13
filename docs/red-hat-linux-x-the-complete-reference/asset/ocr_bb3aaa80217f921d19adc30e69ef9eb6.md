# Network File Systems: NFS and /etc/exports

NFS enables you to mount a file system on a remote computer as if it were local to your own system. You can then directly access any of the files on that remote file system. This has the advantage of allowing different systems on a network to access the same files directly, without each having to keep its own copy. Only one copy would be on a remote file system, which each computer could then access. You can find out more about NFS at its Web site at nfs.sourceforge.net.

Note Mac OS X for Macintosh computers, which is based on BSD Unix, now supports NFS for file sharing. To access Apple file systems and printers using older Apple operating systems, you can use Netatalk. Netatalk implements the classic AppleTalk and AppleShare IP network protocol on Unix and Linux systems. The current Netatalk Web site is netatalk.sourceforge.net, with links to the FAQ and the HOW-TO sections.

# NFS Daemons

NFS operates over a TCP/IP network. The remote computer that holds the file system makes it available to other computers on the network. It does so by exporting the file system, which entails making entries in an NFS configuration file called /etc/exports, as well as by running several daemons to support access by other systems. These include rpc.mountd, rpc.nfsd, and rpc.portmapper. Access to your NFS server can be controlled by the /etc/hosts.allow and /etc/hosts.deny files. The NFS daemons are listed here:

+   - **rpc.nfsd** Receives NFS requests from remote systems and translates them into requests for the local system.
+   - **rpc.mountd** Performs requested mount and unmount operations.
+   - **rpc.portmapper** Maps remote requests to the appropriate NFS daemon.
+   - **rpc.quotad** Provides user disk quote management.
+   - **rpc.statd** Provides locking services when a remote host reboots.
+   - **rpc.lockd** Handles lock recovery for systems that have gone down.

Note It is advisable to use NFS on a local secure network only. If used over the Internet, NFS would open your system up to nonsecure access.

# Starting and Stopping NFS

On Red Hat, you can start up and shut down the NFS daemons using the /etc/rc.d/init.d/nfs service, which you can invoke with the service command, service nfs start. To have NFS started automatically, you can use chkconfig or the redhat-config-services tool to specify the runlevels at which it will operate. The following example will have NFS start up automatically at runlevels 3 and 5 on Red Hat:

```
chkconfig --level 35 nfs on
```

# NFS Analytical Tools

# Configuring NFS with the Red Hat NFS Configuration Tool