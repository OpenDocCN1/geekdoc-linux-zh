
# Chapter 18 The Network File System

Second, if filesystems are mounted from many different hosts, clients become dependent on many different servers. Chaos ensues when one of those servers crashes. Every command that accesses the mount points will hang.

Third, when an important server crashes, it may cripple users by making filesystems like /usr/share unavailable. In this situation, it's best to have a copy of the partition be mounted temporarily from a backup server. However, NFS has no built-in provision for backup servers.

You can moderate all these problems by using an automount daemon to manage filesystems when they are referenced and unmount them when they are no longer used. An automounter limits the number of active mount points and is largely transparent to users. Most automounters accept a list of “replicated” (identical) filesystems so that the network can continue to function when a primary server becomes unavailable.

To implement behind-the-scenes mounting and unmounting, the automount mounts a virtual filesystem driver on the directories you designated as locations for automatic mounting to occur. In the past, the automounter did this by posing as an NFS server, but this scheme suffers from significant limitations and is rarely found on contemporary systems. A kernel-resident filesystem driver called autofs is used.

Instead of mirroring an actual filesystem, the automounter “makes up” a virtual filesystem hierarchy according to the specifications in its configuration file. When a user references a directory within the automounter’s virtual filesystem, the automounter intercepts the reference and mounts the actual filesystem the user is trying to reach. On systems that support autofs, the NFS filesystem is mounted beneath the autofs filesystem in UNIX fashion. Other systems may require mounting to occur in a separate directory that is pointed to by symbolic links.

The idea of an automounter originates from Sun, now part of Oracle. Sun’s implementation, automount, is shipped with most Sun-derived NFS clients. Linux distributions provide a version that functionally mimics that of Sun, though it is an independent implementation. Similarly, AIX provides its own independent automount daemon that IBM calls an administration tool for AutoFS.

The various automount implementations understand three kinds of configuration files (referred to as “maps”): direct, indirect, and master maps. Direct and indirect maps provide information about the filesystems to be automounted. A master list provides the direct and indirect maps that automount should pay attention to. Only one master map can be active at once; the default master map is kept in /etc/auto_master (/etc/auto.master under Linux).

On systems, automount is a stand-alone command that reads its configuration, sets any necessary autofs mounts, and exits. Actual references to automated filesystems are handled (through autofofs) by a separate daemon process, **automount**. The daemon does its work silently and does not need additional configuration.

On Linux systems, the daemon is called **automount** and the setup function is performed by the **/etc/init.d/autofs** startup script. Linux details are given in the section *Specific for Linux* on page 717. In the following discussion, we refer to the setup command as **automount** and the daemon as **automount**.

If you change the master map or one of the direct maps that it references, you must rerun **automount** to pick up the changes. With the -v option, **automount** will show you the adjustments it's making to its configuration.

**automount** also accepts a -t argument that tells how long (in seconds) an automounted filesystem remains before being unmounted. The default is 10 minutes. Since an NFS mount whose server has crashed can cause programs that touch to it, it's good hygiene to clean up automounts that are no longer in use; don't raise the timeout too much.

# Indirect maps

Indirect maps mount several filesystems underneath a common directory. However, the path of the directory is specified in the master file, not in the map itself. For example, an indirect map for filesystems under **/chimchim** might look like this:

```
users harp/harp/users
devel -soft harp/harp/devel
info -ro harp/harp/info
```

The first column names the subdirectory in which each automount should be installed, and subsequent items list the mount options and the NFS path of the filesystem. This example (perhaps stored in **/etc/auto.harp**) tells **automount** that it can mount the directories **/harp/users**, **/harp/devel**, and **/harp/info** from the server harp, with **info** being read-only and **devel** being mounted soft.

In this configuration the paths on chimchim and the local host are the same. However, this correspondence is not required.

# Direct maps

Direct maps list filesystems that do not share a common prefix, as **/usr/src** and **/cs/tools**. A direct map entry **/etc/auto.direct**) that described both of these filesystems to **automount** might look something like this:

```
/usr/src harp/usr/src
/cs/tools -ro monk:/cs/tools
```

Because they do not share a common parent directory, these automounts must each be implemented with a separate autofs mount. This configuration requires more overhead, but it has the added advantage that the mount point and directory structure are always accessible to commands such as ls. Using ls on a directory of indirect mounts can be confusing to users because automount doesn't show the subdirectories until.

# Master maps

A master map lists the direct and indirect maps that automount should pay attention to. For each indirect map, it also specifies the root directory used by the maps.

A master map that use the direct and indirect maps shown in the examples would look something like this:

```
# Directory Map
/harp /etc/auto.harp -proto=tcp
/- /etc/auto.direct
```

The first column is a directory name for an indirect map or the special token /- for a direct map. The second column identifies the file in which the map is stored. You can have several maps of each type. When you mount options at the end of a line, they sets the defaults for all mounts within the map. Linux administrators should always specify the -fstype=nfs4 flag for NFS version 4.

> On many systems, the default options set on a map entry do not blend with the options specified in the direct or indirect map to points. If a map entry has its own list of options, the defaults are ignored. Linux merges the two sets, however the same option is specified in both places, the map entry's value overrides the default.

The master map can usually be replaced or augmented by a version shared through NIS. See your documentation for details.

# Executable maps

If a map is executable, it's assumed to be a script or program that dynamically generates automounting information. Instead of reading the map as a text file, the automunter executes it with an argument (the "key") that indicates subdirectory a user has attempted to access. The script is responsible for printing an appropriate map entry; if the specified key is not valid, the script can simply exit without printing anything.

This powerful feature makes up for many of the deficiencies in automounter's strange configuration system. In effect, it allows you to define a site-wide automount configuration file in a format of your choice. You can write a simple script to decode the global configuration on each machine. Some systems
