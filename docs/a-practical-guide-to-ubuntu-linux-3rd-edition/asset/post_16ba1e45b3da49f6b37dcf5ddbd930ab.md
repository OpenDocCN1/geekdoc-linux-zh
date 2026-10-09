
When you install the **autofs** package, the **dpkg** postinit script starts the **automount** daemon. After you configure **automount**, call the **autofs** init script to restart the **automount** daemon:

```
$ sudo service autofs restart
```

After changing the **automount** configuration on an active server, use **reload** in place of **restart** to reload **automount** configuration files without disturbing automatically mounted file systems.

# autofs: Automatically Mounted Directory Hierarchies

An **autofs** directory hierarchy is like any other directory hierarchy but remains unmounted until it is needed, at which time the system mounts it automatically (demand mounting). The system unmounts an **autofs** directory hierarchy when it is no longer needed—by default, after 5 minutes of inactivity. Automatically mounted directory hierarchies are an important part of managing a large collection of systems in a consistent way. The **automount** daemon is particularly useful when an installation includes a large number of servers or a large number of directory hierarchies. It also helps to remove server-server dependencies (discussed next).

When you boot a system that uses traditional **fstab**-based mounts and an NFS server is down, the system can take a long time to come up as it waits for the server to time out. Similarly, when you have two servers, each mounting directory hierarchies from the other, and both systems are down, both may hang as they are brought up while each tries to mount a directory hierarchy from the other. This situation is called a *server-server dependency*. The **automount** facility gets around these issues by mounting a directory hierarchy from another system only when a process tries to access it.

When a process attempts to access one of the directories within an unmounted **autofs** directory hierarchy, the kernel notifies the **automount** daemon, which mounts the directory hierarchy. You must give a command, such as `cd /home/zach`, that accesses the **autofs** mount point (in this case `/home/zach`) to create the demand that causes **automount** to mount the **autofs** directory hierarchy; only then can the system display or use the **autofs** directory hierarchy. Before you issue this `cd` command, `zach` does not appear in `/home`.

The main file that controls the behavior of **automount** is `/etc/auto.master`. A simple example follows:

```
$ cat /etc/auto.master
/free1        /etc/auto.misc        -timeout=60
/plum         /etc/auto.plum
```

The **auto.master** file has three columns. The first column names the parent of the **autofs** mount point—the location where the **autofs** directory hierarchy is to be mounted. (The `/free1` and `/plum` directories in the example are not mount points but will hold the mount points when the directory hierarchies are mounted.) The second column names the files, called *map files*, that store supplemental configuration information. The optional third column holds mount options for map entries. In the preceding example, the first line sets the timeout (the length of time a directory stays mounted when it is not in use) to 60 seconds; the default timeout value is 300 seconds. You can change *auto* defaults values in `/etc/default/autofs`.

Although the map files can have any names, one is traditionally named **auto.misc**. Following are the two map files specified in *auto.master*:

```
$ cat /etc/auto.misc
music		-fstype=ext4		:/dev/sdb7

$ cat /etc/auto.plum
pl6		-fstype=nfs		plum:pl6
```

The first column of a map file holds the relative *autofs* mount point (**music** and **pl6** in the preceding files). This mount point is appended to the corresponding *autofs* mount point from column 1 of the *auto.master* file to create the absolute *autofs* mount point. In this example, **music** (from *auto.misc*) is appended to **/free1** (from *auto.master*) to make **/free1/music**; **pl6** is appended to **/plum** to make **/plum/pl6**.

The second column holds options, and the third column shows the server and directory hierarchy to be mounted. The first example shows a local drive (**/dev/sdb7**). You can tell it is local because its filesystem type is specified as **ext4** and no system name appears before the colon. The second example shows a filesystem on a remote system. It has a filesystem type of **nfs** and specifies the name of the remote system, a colon, and the name the filesystem is mounted under on the remote system.

Before the new setup can work, you must reload the **automount** daemon using the *autofs* init script (page 793). This script creates the directories that hold the mount points (**/free1** and **/plum** in the example) when you start, restart, or reload *autofs* and removes those directories when you stop it.

In the following example, the first ls command shows that the **/free1** and **/plum** directories do not exist. The next command, running with **root** privileges, runs the *autofs* init script to reload *autofs*. Now the directories exist but do not hold any files. When the user lists the contents of **/plum/pl6**, *autofs* mounts **pl6** and ls displays its contents:

```
$ ls /free1 /plum
ls: /free1: No such file or directory
ls: /plum: No such file or directory

$ sudo service autofs reload
Reloading automounter: checking for changes ...
Reloading automounter map for: /free1
Reloading automounter map for: /plum

$ ls /free1 /plum
/free1:
/plum:

$ ls /plum/pl6
lost+found memo
```

## Chapter Summary

NFS allows a server to share selected local directory hierarchies with client systems on a heterogeneous network, thereby reducing storage needs and administrative overhead. NFS defines a client/server relationship in which a server provides directory hierarchies that clients can mount.

On the server, the **/etc/exports** file typically lists the directory hierarchies that the system exports. Each line in **exports** specifies a directory hierarchy and the client systems that are allowed to mount it, including options for each client (readonly, read-write, and so on). An **exportfs -r** command causes NFS to reread this file.

From a client, a **mount** command mounts an exported NFS directory hierarchy. Alternatively, you can put an entry in **/etc/fstab** to have the system automatically mount the directory hierarchy when it boots.

Automatically mounted directory hierarchies help manage large groups of systems containing many servers and file systems in a consistent way and can help remove server–server dependencies. The **automount** daemon automatically mounts **autofs** directory hierarchies when they are needed and unmounts them when they are no longer needed.

## Exercises

1.  What are three reasons to use NFS?
2.  Which command would you give to mount on the local system the **/home** directory hierarchy that resides on the file server named **plum**? Assume the mounted directory hierarchy will appear as **/plum.home** on the local system. How would you mount the same directory hierarchy if it resided on the file server at 192.168.1.1? How would you unmount **/home**?
3.  How would you list the mount points on the remote system named **plum** that the local system named **grape** can mount?
4.  Which command line lists the currently mounted NFS directory hierarchies?
5.  What does the **/etc/fstab** file do?
6.  From a server, how would you allow readonly access to **/opt** for any system in **example.com**?

## Advanced Exercises

7.  When is it a good idea to disable attribute caching?
8.  Describe the difference between the **root_squash** and **all_squash** options in /etc/exports.
9.  Why does the **secure** option in /etc/exports not really provide any security?
10. Some diskless workstations use NFS as swap space. Why is this approach useful? What is the downside?
11. NFS maps users on the client to users on the server. Explain why this mapping is a security risk.
12. What does the mount **nosuid** option do? Why would you want to use this option?
