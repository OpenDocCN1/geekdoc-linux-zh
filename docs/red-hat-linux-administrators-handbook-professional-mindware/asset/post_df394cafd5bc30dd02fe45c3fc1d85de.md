
To make sure both rpc.mountd and rpc.nfsd are running properly, run a program called rpcinfo, as follows:

```
rpcinfo -p
```

The output looks like this:

| program | vers | proto | port | service    |
|---------|------|-------|------|------------|
| 100000  | 2    | tcp   | 111  | portmapper |
| 100000  | 2    | udp   | 111  | portmapper |
| 100021  | 1    | udp   | 1024 | nlockmgr   |
| 100021  | 3    | udp   | 1024 | nlockmgr   |
| 100024  | 1    | udp   | 1025 | status     |
| 100024  | 1    | tcp   | 1024 | status     |
| 100011  | 1    | udp   | 728  | rquotad    |
| 100011  | 2    | udp   | 728  | rquotad    |
| 100005  | 1    | tcp   | 1026 | mountd     |
| 100005  | 1    | tcp   | 1025 | mountd     |
| 100005  | 2    | udp   | 1026 | mountd     |
| 100005  | 2    | tcp   | 1025 | mountd     |
| 100003  | 2    | udp   | 2049 | nfs        |

This shows that mountd and nfsd have announced their services and are working fine. At this point, the NFS server is set up, so the NFS client hosts now can be configured.

## Installing an NFS Client

If you are also using Red Hat Linux systems as NFS clients, you need to install the NFS client software on them. The NFS client software also comes in an RPM package. You should install it from your Red Hat CD-ROM. For example, to install the NFS client package for an x86 Red Hat Linux system, I can run the following command from the /RedHat/RPMS directory of the CD-ROM:

```
rpm -ivh nfs-client-version.i386.rpm
```

After you install the NFS client package, you are ready to configure the clients.

## Configuring an NFS Client

This section assumes that you are configuring Red Hat Linux-based NFS clients. If you are configuring an NFS client on a different platform, read the proper documentation if you need any help. The NFS client package comes with a program called showmount that gives you information on exported file systems or directories on an NFS server. You can run this command with the NFS server's host name or IP address as the argument to see what hosts are allowed to access the exported file systems or directories. For example,

```
showmount nfs-server.nitec.com
```

shows the list of NFS clients that are allowed to import files from `nfs-server.nitec.com`. To see the NFS server's export list, run this command with the `-e` option. To see which client is allowed to import what file systems or directories, run the command with the `-a` option.

If the showmount command indicates that the NFS client you are configuring is allowed to import a file system or directory, you are ready to continue with client configuration. If it does not show the host name or IP address of your current NFS client, you must reconfigure the `/etc/exports` file on the NFS server to allow this client access to whatever directory or file system you want to import.

To import a directory or file system from an NFS server, you need to mount it using the standard mount command. For example, to mount a directory called `/www` from an NFS server called `nfs-server.nitec.com`, use the following mount command:

```
mount nfs-server.nitec.com:/www /www -t nfs
```

This command mounts the `/www` directory from the `nfs-server.nitec.com` system as an NFS file system that is specified using the `-t` option. However, if you plan to mount an NFS file system or directory on a regular basis and on boot, you have to add a new line in the `/etc/fstab` file of your client system. For example, to mount the /www directory from nfs-server.nitec.com at boot, add the following line in the /etc/fstab file:

```
nfs-server.nitec.com:/www /www nfs
```

To make sure that your NFS client will automatically mount NFS file systems and directories at boot, check whether you have a symbolic link (starting with Sxx, where xx is a two-digit number) to the /etc/rc.d/init.d/nfs init script in your default run level rc directory. Unmounting an NFS file system is exactly the same as unmounting the local file system.

After you mount the NFS server-exported files on your NFS client system, your users can start using the mounted file systems or directories immediately. Before you allow users access to your NFS exports, consider the following security issues.

## Securing Your NFS Server

The portmap program, in combination with rpc.nfsd, can be fooled, making it possible for unauthorized persons to get to files on NFS servers without having any privileges. Fortunately, the portmap program that Linux uses is relatively secure against attack and can be made more secure by adding the following line in the /etc/hosts.deny file:

```
portmap: ALL
```

The system will deny portmap access for everyone. Next, the /etc/hosts.allow file needs to be modified as follows:

```
portmap: 192.168.1.0/255.255.255.0
```

This allows all hosts from the 192.168.1.0 network to have access to portmap-administered programs, such as nfsd and mountd.

> **Caution**
> Never use host names in the portmap line in /etc/hosts.allow, because use of host name lookups can indirectly cause portmap activity, which will trigger host name lookups in a loop.

One other security issue on the server side is whether to allow the root account on a client to be treated as root on the server. By default, Linux prohibits root on the client side of the NFS to be treated as root on the server side. In other words, an exported file owned by root on the server cannot be modified by the client root user. To explicitly enforce this rule, modify the `/etc/exports` file as follows:

```
/www nitec.com(rw, root_squash)
```

Now, if a user with UID 0 (the root user) on the client attempts to access (read, write, or delete) the file system, the server substitutes the UID of the server’s nobody user. This means the root user on the client can’t access or change files that only the root on the server can access or change. To grant root access to an NFS file system, use the `no_root_squash` option instead.

Note that it is also possible to enhance NFS client security by not trusting the NFS server too much. For example, you can use the `nosuid` option to disable suid programs from working off the NFS file system. This means that the server’s root user cannot make a suid-root program on the file system, log in to the client as a normal user, and then use the suid-root program to become the root on the client, too.

You also can forbid execution of files on the mounted file system altogether with the `noexec` option. Enter these options in the options column of the line that describes your NFS mount point in the `/etc/fstab` file.

## Distributing Files Using rdist

The rdist program enables you to maintain identical copies of files over multiple hosts. It uses either the rcmd function calls or the remote shell (rsh) to access each of the target host computers.

The easiest way to get rdist working is to create a common account on all the machines involved and create `.rhosts` files for each target (that is, client) system so that the common user on the master host is allowed to run rsh sessions. Because an example will make this easy to understand, suppose that you want to create a file distribution environment in which a master computer called `master.an-university.edu` contains the master copy of the file, and two hosts called `student1.an-university.edu` and `student2.an-university.edu` need to get fresh copies of the files on the master computer on a daily basis. Also assume that each of these three computers shares a common user account called updater. Here is how to set up such an environment.

On each of the student computers, add an .rhosts file in the home directory of the updater user. This file contains a single line, such as the following:

```
master.an-university.edu
```

This file must be owned by the root user and must be read-only for everyone else. This allows a user called updater on master.an-university.edu to run remote shell sessions on each student system.

The next step is to create a file distribution configuration file for rdist. This file is often called the distfile. A distfile is a text file that contains instructions for rdist on how to perform the file distribution task. Listing 13-1 shows one such distfile, rdist_distfile.

### Listing 13-1: The rdist_distfile File

```
# 
# Distfile for rdist
# 
# This is used to distribute files from 
# master.an-university.edu to student[12].an-
# university.edu 
# systems
# 
# $Author$ (kabir@nitec.com)
# $Version$
# $Date$
# $Id$

# List all the hosts that need to be updated.
# The list is created using user@hostname entries where 
# each 
# entry is separated by a whitespace character.
```
