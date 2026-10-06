# Getting NFS

While nearly every Linux system supports NFS client and server features, NFS is not installed by default. You'll need different packages for different Linux systems to install NFS. Here are some examples:

+   **Fedora Core and other Red Linux systems** — You need to install the nfs-utils package to use Fedora as an NFS server. There is also a graphical Configuration tool that requires you to install the system-config package. NFS client features are in the base operating system. To turn on the NFS server, type the following:
```
# service nfs start
# chkconfig nfs
```

+   **Debian** — To act as an NFS client, the nfs-common and portmap packages are required; for an server the nfs-kernel-server package must be added. Using the apt-get command line (if you are connected to the Internet) installs all. Then, if you have exported an NFS file to the /etc/exports file (as described later), you can start the nfs-common and nfs-kernel-server scripts, as shown here:
```
# apt-get install nfs-common portmap nfs-kernel-server
# /etc/init.d/nfs nfs-kernel-server start
# /etc/init.d/nfs common start
```

+   **Gentoo** — With Gentoo, NFS file system and NFS server support must be configured into the kernel to use NFS server features. Installing the n-utils package (emer nfs-utils) should get the required packages. To start the service, run rc-update and start the service immediately:
```
# emerge nfs-utils
# rc-update add portmap default
# rc-update add nfs default
# /etc/init.d/nfs start
```

The commands (mount, exportfs, and so on) and files (/etc/exports, /etc/fstab, and so) for actually configuring NFS are the same on every Linux system I've encountered. So once you have NFS installed and running, just follow the instructions in this chart to using NFS.

# Sharing NFS File Systems

To share an NFS file system from your Linux system, you need to export it to the server system. Exporting is done in Linux by adding entries into the /etc/exports file. Each entry identifies a directory in your local file system that you want to share with otheritither computers. The entry also identifies the other computers that can share the resource (or opens it to all computers) and includes other options that reflect permissions associated with the directory.