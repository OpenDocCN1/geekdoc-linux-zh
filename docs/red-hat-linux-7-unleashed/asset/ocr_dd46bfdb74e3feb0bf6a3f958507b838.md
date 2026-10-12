# # Configuring the `/etc/fstab` File to Mount Filesystems Automatically

At boot time, the system will automatically mount the *root* filesystem with read-only privileges. This allows it to load the kernel and read critical startup files. However, after the system has bootstrapped itself, it will need guidance. Although it is possible for you to jump in and mount all the filesystems, it isn't realistic because you then have to finish bootstrapping the machine yourself. Even worse, the system might not come back online by itself.

To get around this, Linux uses a special file called `/etc/fstab`. This file lists all the partitions that need to be mounted at boot time and the directory where they need to be mounted. Along with that information, you can pass parameters to the *mount* command.

# ## Note

NFS servers can also be NFS clients. For example, a Web server that exports part of its archive to, say, an FTP server, can NFS mount from the server containing home directories at the same time.

Each filesystem to be mounted is listed in the `fstab` file in the following format:

```
``/dev/device      /dir/to/mount       fstype parameters fs_freq fs_passno``
```

An example would look like this:

```
``server:/usr/local/pub      /pub       nfs       rsize=8192,wsize=8192,timeo=14,intr``
```

# ## Note

There is a sample `/etc/fstab` at the end of the chapter.

The following items make up this line:

+   - **/dev/device**—The device to be mounted. In the case of mounting NFS filesystems, this comes in the form of `servername:/dir/exported`, where `servername` is the name of the NFS server and `/dir/exported` is the directory that is exported from the NFS server. For example, `demon:/export/home`, where `demon` is the hostname of your NFS server and `/export/home` is the directory that is specified in the `/etc/exports` directory as being shared.

+   - **/dir/to/mount**—The location at which the filesystem should be mounted on your directory tree.

![](bbox=[0.83, 0.09, 0.98, 0.34])