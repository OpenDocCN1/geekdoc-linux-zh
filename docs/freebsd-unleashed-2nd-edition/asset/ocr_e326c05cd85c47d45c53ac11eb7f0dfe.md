Refer to “Using a Firewall,” in Chapter 29, for more information on how to configure firewall rules using IPFW.

# ## NFS Mount Daemon (mountd)

Whereas `nfsd` is the program that provides the connection end of each individual NFS mount, a second program is in charge of listening for new NFS client requests (on TCP port 2049). This program is mountd, the mount daemon. It is executed automatically along with the `nfsd` processes during the network setup procedure at boot time if `nfs_server_enable` is set to “YES”.

`mountd` takes incoming NFS connections and passes them to `nfsd` processes. It’s also in charge of keeping track of the NFS shares you have specified in `/etc/exports`. To restart NFS services after making changes to `/etc/exports`, you need to send an HUP signal to mountd, as you will see shortly.

There aren’t too many useful options for mountd. The default settings in `/etc/default/rc.conf`, which you can override in `/etc/rc.conf`, are as follows:

```
mountd_flags=“-r”
```

The -r flag allows mountd to serve regular files rather than only directories, to maintain compatibility with certain diskless workstations that boot via NFS. The -1 flag allows you to log all NFS mount requests, and the -n flag allows NFS shares to be mounted to remote systems such as Windows PCs that don’t share the same ownership and permissions model as Unix.

# ## Determining What to Share with the /etc/exports File

The `/etc/exports` file lists what directory trees should be shared via NFS as well as who should be allowed to share them. If `/etc/exports` does not exist or is not readable at the time the network is started, the `nfsd` and mountd processes are not started.

The full format of `/etc/exports` is defined in `man exports`. A basic export line specifies one or more directories that should be exported (shared), any of several options, and then an optional list of hosts (by IP address, network, netgroup, or hostname) allowed to share the specified directories. For example, the following line shares the `/home` directory and all its subdirectories to anybody who connects:

```
/home  -alldirs
```

Note that the -alldirs option can only be specified if the share is the mount point of a filesystem (for example, `/usr` or `/home`). If it isn’t, the share will not be made available. A share that can be accessed only by three specified hosts and is read-only would look like this:

```
/usr2 -ro -alldirs stripes.somewhere.com spots.somewhere.com 64.41.131.165
```