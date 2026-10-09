
## Sharing drive space with NFS server

Although you can share static content via a network file system (NFS), earlier I recommended using local copies of the static files instead. Files stored on a local drive will yield a much faster access time than any network storage solution unless you choose a high-end SAN solution.

I highly recommend that you put only files that need to be shared, that change frequently, or that must use the same data across all Web nodes, on an NFS partition. For example, your Web applications can be shared over all nodes so that you have a single copy of all the software. However, more importantly, the data that these applications create should be shared. For example, if you have a CGI script that writes disk-session data for a shopping cart, when the user makes the next request the load-balancing scheme that you use might direct the user to a different Web server on your network, which means that the session data has to be available to the other Web server or else the user will have to restart her shopping cart.

Create a single directory in which you keep all your must-share data. For example, create `/www/cgi-data` as your CGI script data directory on the NFS server. You can create subdirectories for each CGI application and configure each application to write to its own directory within `/www/cgi-data`. Then, mounting this directory via NFS will make it available to all Web servers in the network. The following sections show you how.

### Setting up an NFS server

An NFS server needs to run a program called portmapper (also called portmap or rpc.portmap), which is usually started by an rc script. To check whether portmapper is already running, use the following command:

```
ps auxw | grep portmap
```

It turns out that under RedHat Linux, portmapper is automatically started by the `/etc/rc.d/rc3.d/S4/portmap` script (that is, the `/etc/rc.d/init.d/portmap` init script) so there is no need to manually start it.

The next step is to modify the `/etc/exports` file to tell the system what file systems or directories need to be exported to NFS clients. Because XC News only needs the `/www/cgi-data` directory exported to the Web servers, the export file on the `ns.xcnews-lan.com` host looks like this:

```
/www/cgi-data www1.xcnews-lan.com(rw) www2.xcnews-lan.com(rw)
```

This line tells the NFS server to allow both `www1.xcnews-lan.com` and `www2.xcnews-lan.com` read and write access to the `/www/cgi-data` directory.

> The syntax for the exports file may not be the same for all brands of Unix.

The next programs that must run are mountd (rpc.mountd) and nfsd (rpc.nfsd). These two programs are also started automatically from rc scripts in /etc/rc.d/rc3.d. Whenever a change is made to the /etc/exports file, however, these two programs need to be told about this change. A script called exportfs can restart these two programs, as follows:

```
exportfs
```

If exportfs is missing on a system, then a script such as the following can be used instead:

```
#!/bin/sh
killall -HUP /usr/sbin/rpc.mountd
killall -HUP /usr/sbin/rpc.nfsd
echo re-exported file systems
```

This script uses the killall program found on most Linux systems; if it is not available, you can always run a ps command, find the PID for these processes, and manually perform a kill -HUP for each process. Now to make sure both mountd and nfsd are running properly, run a program called rpcinfo, as follows:

```
rpcinfo -p
```

The output looks like this:

| program | vers | proto | port | service |
|---------|------|-------|------|---------|
| 100000  | 2    | tcp   | 111  | rpcbind |
| 100000  | 2    | udp   | 111  | rpcbind |
| 100005  | 1    | udp   | 635  | mountd  |
| 100005  | 2    | udp   | 635  | mountd  |
| 100005  | 1    | tcp   | 635  | mountd  |
| 100005  | 2    | tcp   | 635  | mountd  |
| 100003  | 2    | udp   | 2049 | nfs     |
| 100003  | 2    | tcp   | 2049 | nfs     |

This shows that portmapper, mountd, and nfsd have announced their services and are working fine. Before setting up the client side of NFS on the Web servers, it is important to make sure security issues are addressed, as I discuss in the next section.

### Server security issues

The portmapper, in combination with `nfsd`, can be fooled, making it possible to get to files on NFS servers without any privileges. Fortunately, the portmapper Linux uses is relatively secure against attack, and can be made more secure by adding the following line in the `/etc/hosts.deny` file:

```
portmap: ALL
```

The system will deny portmapper access for everyone. Now the `/etc/hosts.allow` file needs to be modified as follows:

```
portmap: 192.168.1.0/255.255.255.0
```

This enables all hosts from the `192.168.1.0` network to have access to portmapper-administered programs such as `nfsd` and `mountd`.

> **Caution** Never use host names in the `portmap` line in `/etc/hosts.allow` because use of host name lookups can indirectly cause `portmap` activity, which will trigger host name lookups in a loop.

Another security issue on the server side is whether to allow the root account on a client to be treated as root on the server. By default, Linux prohibits root on the client side of the NFS to be treated as root on the server side. In other words, an exported file owned by root on the server cannot be modified by the client root user. To explicitly enforce this rule, the `/etc/exports` file can be modified as follows:

```
/www/cgi-data www1.xcnews-lan.com(rw, root_squash) www2.xcnews-lan.com(rw, root_squash)
```

Now, if a user with UID 0 (the root user) on the client attempts to access (read, write, or delete) the file system, the server substitutes the UID of the server’s “nobody” account. This means that the client root user can’t access or change files that only the server root can access or change.

> **Tip** To grant root access to an NFS file system, use the `no_root_squash` option instead.

At this point the NFS server is set up and secure, so now let’s set up the NFS client hosts.

### Setting up an NFS client

By default, Red Hat Linux supports NFS file systems, so there is no need to mess around with the kernel. To mount the `/www/cgi-data` directory exported by the `ns.xcnews-lan.com` host, add the following line to the `/etc/fstab` file for both of the Web servers:

```
ns.xcnews-lan.com:/www/cgi-data /www/cgi-data nfs
```

This line automatically mounts the /www/cgi-data directory when any of the Web servers is rebooted.

Next, create the /www/cgi-bin directory on both systems and manually mount the directory using the mount command, as follows:

```
ns.xcnews-lan.com:/www/cgi-data nfs
```

> **Caution**
>
> One typical NFS mounting problem occurs because many developers forget to run **exportfs** (that is, **restart rpc.mountd and rpc.nfsd**) after they modify the /etc/exports file on the NFS server.

Unmounting an NFS file system is exactly the same as unmounting the local file system. Note that it is also possible to enhance NFS client security by not trusting the NFS server too much. For example, you can disable suid programs to work off of the NFS file system with a **nosuid** option. This means that the server's root user cannot make a suid-root program on the file system, log in to the client as a normal user, and then use the suid-root program to become the root on the client, too. It is also possible to forbid execution of files on the mounted file system altogether with the **noexec** option. You can enter these options in the options column of the line that describes your NFS mount point in the /etc/fstab file.

At this point, the file distribution scheme and the NFS-based CGI data directory are both ready. It is time to configure Apache and to make sure it is secured.

The primary bottleneck in an NFS environment is the disk I/O speed of the NFS server. The disk I/O speed is dependent on what kind of disk subsystem you use with your NFS server. For much, running a NFS server using IDE disks will not yield great performance versus running a server with ultra-wide SCSI drives that have high RPM rates. The maximum number of I/O operations per second will dictate how well your NFS server performs. I have used an Intel Xeon 500 system with 10 ultrawide SCSI disks in RAID 5 as a NFS server for approximately 50 users with great success.

After you have decided on a good disk subsystem such as a RAID 5 using an array of 10K RPM ultra-wide SCSI disks with a disk controller that has a large built-in disk cache, your next hardware bottleneck is the network itself. Isolating high-bandwidth traffic into its own network is a good way to reduce performance loss. So, I recommend that you connect your NFS server(s) to your NFS clients by using a dedicated 100Mbits Ethernet of its own. In other words, create a NFS backbone that only moves NFS packets. This will result in a high-performance NFS network.

The software configuration options that can help you to tune your NFS server are addressed in the following sections.

### Optimizing read/write block size

The default read and write block size for NFS is 4096 bytes (4K), which might not be optimal for all situations. You can perform a test to determine whether changing the block size will improve performance. Here is how you perform such a test.
