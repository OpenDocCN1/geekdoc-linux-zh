filesystems are mounted on demand, and then unmounted after a specified period of inactivity. Automounting reduces the chance of NFS hangs, as only filesystems that are currently in use are mounted, thereby reducing the chance of an NFS problem.

Setup and use of the automounter are relatively simple operations, supported in most flavors of UNIX. In most cases the startup rc scripts of your client UNIX system will handle the start of the automount daemon. If you choose not to use the automounter, be sure to modify the rc script and comment out the automounter to reduce the number of processes running on your system.

> If you don't use the automounter, be sure to modify the operating system's rc script that starts the automounter. Commenting out the line in the startup script is sufficient, and will save resources on your client machine.

If you choose to use the automounter, you need to configure your `/etc/auto_master` file to define how the automounter should work. `auto_home` is the master map for the automounter. In our example below, we have two entries in our `auto_master` file, one for `/net` and one for `/home`. The entry for `/home` refers to another automount map file, `auto_home`, which for this example resides in `/etc/auto_home`.

Note that you can distribute your maps throughout the use of NIS. The master file consists of three entries. The first entry is the mount point where NFS will mount the server filesystem. The second entry defines the mount point, or the subsequent map to use. The third entry is for any special mount options, such as read-only. In our example, we are using `-nosuid`, which causes the client system not to execute setuid programs.

```
```text
#/etc/auto_master
#
# Master map for automounter
#
/net             -hosts             -nosuid
/home            auto_home
```
```

The first entry allows for mounting any NFS server that has granted the client system permission into the local directory. For example, to mount `earth:/usr/local` from mars, all we need to do is type:

```
```text
mars% cd /net/earth/usr/local
```
```

The automounter will take care of the rest, mounting `earth:/usr/local` onto `/net/<remote host name>/`. This is the behavior of the automounter—it allows us to quickly mount NFS directories. This is an espe-