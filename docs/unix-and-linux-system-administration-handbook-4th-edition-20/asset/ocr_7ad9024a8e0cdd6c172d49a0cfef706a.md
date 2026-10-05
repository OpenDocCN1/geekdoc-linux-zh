# Direct maps

automated filesystems are handled (through autofofs) by a separate daemon process, **automount**. The daemon does its work silently and does not need additional configuration.

On Linux systems, the daemon is called **automount** and the setup function is performed by the **/etc/init.d/autofs** startup script. Linux details are given in the section *Specific for Linux* on page 717. In the following discussion, we refer to the setup command as **automount** and the daemon as **automount**.

If you change the master map or one of the direct maps that it references, you must rerun **automount** to pick up the changes. With the -v option, **automount** will show you the adjustments it's making to its configuration.

**automount** also accepts a -t argument that tells how long (in seconds) an automounted filesystem remains before being unmounted. The default is 10 minutes. Since an NFS mount whose server has crashed can cause programs that touch to it, it's good hygiene to clean up automounts that are no longer in use; don't raise the timeout too much.

# Indirect maps

Indirect maps mount several filesystems underneath a common directory. However, the path of the directory is specified in the master file, not in the map itself. For example, an indirect map for filesystems under **/chimchim devel** might look like this:

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

8. The other side of this issue is the fact that it takes a certain amount of time to mount a filesystem. System response will be faster and smoother if filesystems aren't being continually remounted.