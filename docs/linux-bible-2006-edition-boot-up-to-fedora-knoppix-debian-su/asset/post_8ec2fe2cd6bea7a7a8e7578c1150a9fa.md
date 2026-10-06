
# Chapter 27 ♦ Running a File Servers 717

/etc/exports File
/apps/bin pine(rw), maple(rw), spruce(rw)

# mount oak:/apps/bin/oak/apps

![](img/a2d958d7eab32ca5b89b2b8af808aa70_748_0.png)

![](img/a2d958d7eab32ca5b89b2b8af808aa70_748_1.png)

/apps/
bin/file2file3
/oak/
apps/

**Figure 27-1:** NFS can make selected file systems available to other computers.

In this example, a computer named oak makes its /apps/bin directory available to clients on the network (pine, maple, and spruce) by adding an entry to the /etc/exports file. The client computer (pine) sees that the resource is available and mounts the resource on its local file system at the mount point /oak/apps, after which any files, directories, or subdirectories of /apps/bin on oak are available to users on pine (given proper permissions).

Although often used as a file server (or other type of service), Linux is a general-purpose operating system, any Linux system can share file systems (export) as a server or use another computer's file systems (mount) as a client. Contrast with dedicated file servers, such as NetWare, which can only share files with client computers (such as Windows workstations) and never act as a client.

> A file system is usually a structure of files and directories that exists on a single device (such as a hard disk partition or CD-ROM). A Linux file system refers to the entire directory system (which may include file systems from several disks or NFS resources), beginning from root (/) on a single computer. A shared directory in NFS may represent all or part of a computer's file system, which can be attached (from the shared directory down the directory tree) to another computer's file system.

# Getting NFS

While nearly every Linux system supports NFS client and server features, NFS is not installed by default. You'll need different packages for different Linux systems to install NFS. Here are some examples:

- **Fedora Core and other Red Linux systems** — You need to install the nfs-utils package to use Fedora as an NFS server. There is also a graphical Configuration tool that requires you to install the system-config package. NFS client features are in the base operating system. To turn on the NFS server, type the following:
```
# service nfs start
# chkconfig nfs
```

- **Debian** — To act as an NFS client, the nfs-common and portmap packages are required; for an server the nfs-kernel-server package must be added. Using the apt-get command line (if you are connected to the Internet) installs all. Then, if you have exported an NFS file to the /etc/exports file (as described later), you can start the nfs-common and nfs-kernel-server scripts, as shown here:
```
# apt-get install nfs-common portmap nfs-kernel-server
# /etc/init.d/nfs nfs-kernel-server start
# /etc/init.d/nfs common start
```

- **Gentoo** — With Gentoo, NFS file system and NFS server support must be configured into the kernel to use NFS server features. Installing the n-utils package (emer nfs-utils) should get the required packages. To start the service, run rc-update and start the service immediately:
```
# emerge nfs-utils
# rc-update add portmap default
# rc-update add nfs default
# /etc/init.d/nfs start
```

The commands (mount, exportfs, and so on) and files (/etc/exports, /etc/fstab, and so) for actually configuring NFS are the same on every Linux system I've encountered. So once you have NFS installed and running, just follow the instructions in this chart to using NFS.

# Sharing NFS File Systems

To share an NFS file system from your Linux system, you need to export it to the server system. Exporting is done in Linux by adding entries into the /etc/exports file. Each entry identifies a directory in your local file system that you want to share with other computers. The entry also identifies the other computers that can share the resource (or opens it to all computers) and includes other options that reflect permissions associated with the directory.

Remember when you share a directory, you are sharing all files and subdirectories below that directory as well (by default). So, you need to be sure that you want to share everything in that directory structure. There are still ways to restrict access within that directory structure, and those are discussed later in this chapter.

# Configuring the /etc/exports File

To make a directory from your Linux system available to other systems, you need to export it. Exporting is on a permanent basis by adding information about an exported directory to the /etc/exports file.

The format of the /etc/exports file is

```
Directory Host(Options) # Comments
```

where Directory is the name of the directory that you want to share, and Host indicates the computer to which the sharing of this directory is restricted. Options can include a variety of options to define the security measures attached to the shared directory for the host. (You can repeat Host/Option pairs.) Comments are any optional comments you want to add (following the #).

As root user, you can use any editor to configure /etc/exports to modify shared entries or add new entries. Here's an example of an /etc/exports file:

```
/cal *.linuxtoys.net(rw) # Company events
/pub (ro,insecure,all_squash) # Public dir
/home maple(rw,squash uids=0-99) spruce(rw,squash uids=0-99)
```

The cal entry represents a directory that contains information about events related to the company. It is made accessible to everyone with any computers in the company's domain (*.linuxtoys.net). Users can write to the directory as well as read them (indicated by the rw option). The (# Company events) simply serves to remind you of the directory contents.

The /pub entry allows any company and user to read files from the directory (indicated by the ro option) but not to write files. The insecure port enables any computer, even one that does not use a secure NFS port, to access the directory. The all_squash option uses all users (UIDs) and groups (GIDs) to be mapped to the nobody.

The /home entry allows specific users to access the directory. The squash option maps client UIDs to nobody, but the uids option limits this to UIDs between 0 and 99.

# Part V ♦ Running Servers

These are just examples; you can share any parts of /etc.

# Host Names in /etc/exports

You can indicate in /etc/exports file which computers can have access. If you want to associate multiple host names or IP addresses, be sure to have a space before each host. For example:

```
/usr/local maple(rw) spruce(ro,root_squash)
```

Notice that there is a space after maple. Here are ways to identify:

- **Individual host**—Enter host names or IP addresses. The host is in your local domain, you can simply indicate the host name. Otherwise, use the full host.domain format. These are valid ways to indicate individual computers:
* maple.handsonhistory.com
* 10.0.0.11
- **IP network**—Allow access to all hosts from a particular network by indicating a network number and its netmask, separated by a slash (/). Here are valid ways to designate network numbers:
* 10.0.0.0/255.255.0.0
* 172.16.0.0/255.255.255.0
* 192.168.0.0/255.255.255.0
- **IP domain**—Using wildcards, you can include all or some host computers from a particular domain. Here are some valid uses of the asterisk and question mark wildcards:
* *.handsonhistory.com
* *craft.handsonhistory.com
* ***handsonhistory.com

Using an asterisk doesn't match subdomains. For example, *.handsonhistory.com would not cause the host name mallard.duck.handsonhistory.com to be included in the access list.

- **NIS groups**—You can allow access to hosts contained in an NIS group. To indicate it, precede the group name with an at @ sign (for example, @group).

![](img/a2d958d7eab32ca5b89b2b8af808aa70_751_0.png)
