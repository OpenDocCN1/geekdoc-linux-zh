
## /etc/hosts.allow and /etc/hosts.deny

To help prevent unauthorized intrusions into your system, you should configure the file called `/etc/hosts.allow` so that only the hosts connected to your internal network, if any, are allowed to access TCP/IP services on your computer. You can do so by modifying `/etc/hosts.allow` and `/etc/hosts.deny` as explained in this chapter.

The file called `/etc/hosts.allow` lists the names of hosts that are allowed to access TCP/IP services on your computer. If you are connected to a local area network in which all the other users are trustworthy, you can make your computer available to all the hosts on the network by typing the first three values of the network's IP address, followed by a period, as in the following example:

```
192.168.100.
```

Any of the machines connected to this network can access TCP/IP services on your computer. When you define `/etc/hosts.allow`, don't forget to grant access to the local host. To do so, type a space after the abbreviated network address, a colon, another space, and 127, as in the following example:

```
192.168.100. : 127.
```

The file called `/etc/hosts.deny` lists the hosts that are specifically denied access to TCP/IP services running on your computer. The safest way to configure this file is to type the following:

```
ALL:ALL
```

This configuration denies access to all hosts, except those specifically granted permission in `/etc/hosts.allow`.

## Network File System (NFS) Configuration

The Network File System (NFS) is the native Linux networking system. NFS allows Linux systems to share directories and files over the network. The result, from the user's point of view, is a single, seamless file system, in which the remote directories seem like natural extensions of the filesystem that's physically present on the user's system. However, note that NFS has several disadvantages. Improperly configured, NFS can open security holes that a knowledgeable intruder could exploit. In addition, NFS does not provide a straightforward method to integrate Microsoft Windows 95/98/NT systems; if you would like to include Windows machines in your network, see the section “Configuring Samba Networking,” later in this chapter.

### Configuring NFS: An Overview

To get NFS working successfully, you must do the following:

- 1. Make sure that your user and group IDs match on the client and server systems.
- 2. On the server, modify `/etc/hosts.allow` and `/etc/hosts.deny` so that the server will accept portmap requests from clients on your network.
- 3. On the server, create or modify the file `/etc/exports` so that the server will make specified directories available to other machines on the network.
- 4. On the client, modify `/etc/fstab` so that the client will automatically load the exported directories when you start the client system.

### User and Group IDs

NFS won’t work smoothly (or at all) if the user and group names and numerical IDs aren’t the same on both systems. If there are discrepancies, you must fix them before proceeding. See `usermod` (Chapter 12) for information on changing the UID and GID of users. Also see `chmod` (Chapter 5) for information on changing the ownership of files recursively throughout the user’s directories.

> **TIP** If you change a user’s IDs, all of the user’s files must be modified (with **chmod**, discussed in Chapter 5) to match the new user and group IDs.

### Portmap Security Restrictions

To use NFS safely, you should modify the `/etc/hosts.allow` and `/etc/hosts.deny` files so that you gain some measure of protection while using NFS. Modify `/etc/hosts.deny` by adding the following line:

```
portmap: ALL
```

Now, modify `/etc/hosts.allow` by adding a line such as the following:

```
portmap: 192.168.100.10/255.255.255.0
```

This line specifies that the indicated client (192.168.100.10) has permission to access the portmap utility. Note that the slash mark and netmask (255.255.255.0) are required. If you are not sure what the IP address and netmask of the client are, go to the client, open a terminal window, type `ifconfig eth0`, and press Enter.

### Required Daemons for NFS Service

To work with NFS, you will need the following daemons (memory-resident programs) running on both servers and clients:

- 1. **portmap** Accepts remote requests for information and guides these requests to the appropriate port.
- 2. **rpc.mountd** This daemon enables the system to mount and unmount remote NFS directories.
- 3. **nfsd** This is the NFS daemon proper.

You should configure all the machines on your network so that they start these daemons at the beginning of each session. On Red Hat systems, you do this with the `/usr/sbin/setup` utility, a text-mode utility that enables you to specify which system services you want to run. Make sure that your system is running the following services: netfs, nfs, nfslock, portmap, rstatd, and ruserd. If any of these options aren't available on the Setup Program menu, you need to install the RPM packages for these services. Other distributions provide varying means to specify which services run automatically at startup; check your distribution's documentation to find out which utility to run.

To make sure you're running the needed utilities, you can run the startup scripts with the status option. Here's how to do this:

- Switch to the directory where network scripts are stored. On Red Hat and kindred systems, this directory is `/etc/rc.d/init.d`.
- Type `./portmap status` and press Enter. You should see a message stating that portmap is running. If not, type `./portmap start` and press Enter.
- Now, type `./nfs status` and press Enter. You should see a message informing you that rpc.mountd and nfsd are running. If not, type `./nfs start` and press Enter.
- Type `/usr/sbin/rpcinfo -p` and press Enter. You should see a list of all the running daemons, including their version numbers and the protocol they're using.

If you see an error message such as “Can't contact portmapper” or “Connection refused,” or “Prog not registered,” portmap isn't running, or your `/etc/hosts.deny` and `/etc/hosts.allow` files aren't properly configured. Check your configuration, then restart your system and try the previous steps again.

### Configuring /etc/exports

The next step involves modifying the file `/etc/exports` on the server so that NFS knows which directories to “export,” that is, make available to clients. To specify a directory to export, type the name of the directory you want to export, followed by a space, and the IP address of the client or clients to which you want to make the directory available. After the IP address, place the export options you want within parentheses. Here's an example:

```
/home/suzanne 192.168.100.33(rw)
/mnt/cdrom 192.168.100.*(ro)
```

This example exports `/home/suzanne`, a directory owned by the user named suzanne on the server, to Suzanne's computer (192.168.100.33), where it will be available to her through NFS. The option (rw) specifies that this directory should be exported with read and write permissions.

The second line exports the server's CD-ROM drive (`/mnt/cdrom`) to all the clients on my network, with read-only permission.

> **WARNING** Before NFS can make use of the modifications you've made, you must use the **exportfs** utility to update the exported directory database, `/var/lib/nfs/mtab` (or `/var/lib/nfs/xtab` depending on version). This database is needed by the remote mounting daemons; if it isn't accurate, clients won't be able to mount the exported directories. To synchronize `/etc/exports` with the database, type **exportfs -rv** and press Enter.

### Configuring /etc/fstab on the Client

Now you need to configure the clients so that they access the exported directories automatically. To do this, follow these steps:

- 1. On the client system, create the directories where you want to mount the remote directories. If you're creating mount points for a user's directories, be sure to do this from the user's account so that it will have the correct permissions.
- 2. Add mount information to `/etc/fstab` on the client system.

The following examples load the directories `/home/public` and `/home/suzanne`, which are physically present on the server named rivendell:

```
rivendell:/home/public /home/suzanne/public nfs rsize=8192,wsize=8192,user
rivendell:/home/suzanne /home/suzanne/rivendell nfs rsize=8192,wsize=8192,user
```

These lines mount the specified directories to local directories named, respectively, `/home/suzanne/public` and `/home/suzanne/rivendell`. The additional options specify the filesystem type (nfs), read and write block sizes that are larger (and faster) than the default, and the all-important user option that enables ordinary users to mount and unmount the remote directories without switching to superuser (which, as you've already learned, would transform them into nobodies).
