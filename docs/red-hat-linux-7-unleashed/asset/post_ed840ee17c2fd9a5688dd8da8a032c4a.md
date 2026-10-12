
## Netgroup Information
Netgroup information is kept in the `/etc/netgroup` file and shared via NIS.

The format of a netgroups file is as follows:

groupname member-list

`groupname` is the name of the group being defined, and the `member-list` consists of other group names or tuples of specific data. Each entry in the `member-list` is separated by a whitespace.

A tuple containing specific data comes in this form:

(hostname, username, domain name)

`hostname` is the name of the machine for which that entry is valid, `username` is the login of the person being referenced, and `domain name` is the NIS domain name. Any entry left blank is considered a wildcard; for example, `(technics, , )` implies everybody on the host `technics`. An entry with a dash in it (`-`) means that there are no valid values for that entry. For example, `(-, ssshah, )` implies the user `ssshah` and nothing else. This is useful for generating a list of users or machine names for use in other netgroups.

In files where netgroups are supported (such as `/etc/passwd`), you reference them by placing an `@` sign in front of them. If you want to give the netgroup `sysadmins` consisting of `(-, ssshah, )` `(-, heidis, )` permission to log in to a server, you add this line to your `/etc/passwd` file:

`+@sysadmins`

An example of a full netgroups file follows:

```text
sysadmins (-,ssshah, ) (-,heidis, ) (-,njnguyen, ) (-,mphan, )
servers (numarK, , ) (vestax, , )
clients (demor, , ) (technics, , ) (mtx, , )
research-1 (-,bosen, ) (-,joym, ) (-,weals, ) (-,jaffe, )
research-2 (-,sanget, ) (-,mona, ) (-,pareskh, ) (-,manjari, ) (-,jagdish, )
consultants (-,arturo, )
allusers sysadmins research-1 research-2 consultants
allhosts servers clients
```

As a general rule, the line lengths should be no more than 1,024 characters. Although the system has no problems with the greater line lengths, it is difficult to edit the file because `vi`, `view`, and perhaps other editors have a 1,024-character line-length limitation.

## Some Troubleshooting Tips
If the NIS software isn't behaving as you think it should, you can check a few things:

- Make sure the processes are running. Use `ps aux` to list all the running processes. Make sure you see the appropriate processes running, regardless of whether the machine is a client, a server, or both.
- Check system logs (in `/var/log`) to see if there are any messages indicating peripheral problems that could be affecting your configuration.
- If the processes appear to be running but are not responsive, kill them and restart them. In some rare circumstances, the daemon may be misbehaving and may need to be restarted.
- Make sure `/etc/nsswitch.conf` is configured properly. This is a common problem.
- If you are trying to start the daemons by hand, make sure you are logged in as `root`.

When encountering problems, slow down, take a short break, and then retrace your steps. It's amazing how often simply slowing down helps you find problems.

## Summary
This chapter covered the installation and configuration of NIS master servers, secondary servers, and clients. In addition to the setup of NIS itself, common “NISisms” and netgroups were discussed. The lessons learned from these sections put a powerful tool in your hands.

Some key points to remember:

- Use `ypinit` to set up NIS master servers and secondary servers.
- The `/var/yp` directory contains the makefile necessary to update NIS information.
- Consider separating NIS files from your regular system files for clarity.
- NIS servers need the `ypserv` daemon.
- NIS clients need the `ypbind` daemon.
- `yppasswd` allows users on NIS clients to change their passwords.
- Schedule a reboot to test all your changes.

Although it isn’t the most exciting feature to come along in recent history, NIS is one of the most useful of the core network services. In conjunction with other services, NIS gives you the ability to create a seamless system for all of your users.

# Chapter 16
# NFS: Network Filesystem

## IN THIS CHAPTER
- Installing NFS 511
- Starting and Stopping the NFS Daemons 512
- Configuring NFS Servers and Clients 512
- Exporting Filesystems with linuxconf 519
- Complete Sample Configuration Files 521

The Network Filesystem, or NFS, is the means by which UNIX systems share their disk resources. What makes NFS really useful is its capability to function in a heterogeneous environment. Most UNIX variants, if not all, support NFS, and you can find NFS support for Microsoft Windows inexpensively, making it a good choice for sharing disks.

NFS was originally developed by Sun Microsystems during the 1980s. Sun shared its design and made the protocol a standard, which eliminated any interoperability conflicts with other operating systems. Linux supported NFS before version 1.0 was released.

A key feature of NFS is its robust nature. It is a *stateless protocol*, meaning that each request made between the client and server is complete in itself and does not require knowledge of prior transactions. Because of this, NFS cannot tell the difference between a very slow host and a host that has failed altogether. This allows servers to go down and come back up without having to reboot the clients. If this doesn’t make much sense, don’t worry about it. Understanding the underlying protocol isn’t necessary for you to set up and successfully run an NFS server.

### Note
> In Chapter 17, “Samba,” you’ll read about how Linux can share its disks with Windows machines. NFS and Samba are not the same. They are two different protocols with two fundamentally different views on how disks should be shared. One of the many things that makes Linux great is its capability to support both means of sharing disks at the same time. In fact, it’s common for Linux servers to share disks with each other through NFS and with Windows-based clients with Samba at the same time.

### Caution
Unfortunately, NFS’s design is insecure by nature. Although taking some steps to protect yourself from the evil hacker pretending to be a common user provides a moderate level of security, there is not much more you can do. Any time you share a disk with another machine via NFS, you need to give the users of that machine (especially the root user) a certain amount of trust. If you believe that the person you are sharing the disk with is untrustworthy, you need to explore alternatives to NFS for sharing data and disk space.

Keep up with security bulletins from both Red Hat and the Computer Emergency Response Team (CERT). You can find these bulletins on Red Hat’s site at www.redhat.com, CERT’s site at www.cert.org, or the moderated newsgroup comp.security.announce.

## Installing NFS
Before you begin installing NFS, make sure that your network setup is functioning correctly and that the server and clients can ping each other. Setting up your network is explained in Chapter 20, “TCP/IP Network Management.”

Although the NFS software comes preinstalled with Red Hat Linux, you need to be aware of what the software is and what each specific program does. This is important when you are troubleshooting problems and configuring NFS-related tools such as the automounter.

Three programs provide NFS server services:

- `rpc.portmapper`—This program does not directly provide NFS services itself; however, it maps calls made from other machines to the correct NFS daemons.
- `rpc.nfsd`—This daemon translates the NFS requests into actual requests on the local filesystem.
- `rpc.mountd`—This daemon services requests to mount and unmount filesystems.

### Note
The `rpc.nfsd` and `rpc.mountd` programs need only run on your NFS servers. In fact, you might find it prudent not to run them at all on your client machines, for security concerns and to free resources that might otherwise be consumed by them. NFS clients do not need any special NFS software to run. They should run the `rpc.portmapper` program, however, because it provides RPC functionality to programs other than NFS.

By default, these programs are installed and loaded at boot time. To check for this, use the `rpcinfo` command as follows:

```
rpcinfo -p
```

This will display all the registered RPC programs running on your system. To check which RPC programs are registered on a remote host, use

```
rpcinfo -p hostname
```

where `hostname` is the name of the remote host you want to check. The output for a Linux host running NFS looks something like the following:

```
[root@vexstar /root]# rpcinfo -p
program    vers   proto   port
100000      2    tcp  111  portmapper
100000      2    udp  111  portmapper
```
