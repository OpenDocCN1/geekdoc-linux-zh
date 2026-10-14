# Mounting Samba Shares

There are two ways to mount Samba shares to your Linux host. Mounting a share is the same as mounting an available media partition or remote NFS directory except that the Samba share is accessed using SMB. The first method uses the standard Linux mount command:

```
```bash
$ sudo mount -t smbfs //10.10.10.20/homes /mount/point -o username=ahudson,dmask=777,\
  fmask=777
```
```

> **NOTE**
> 
> You can substitute the IP address for hostname if your name service is running or the host is in your `/etc/hosts` file.

This command mounts ahudson’s home directory on your host and gives all users full permissions to the mount. The permissions are equal to the permissions on the chmod command.

The second method produces the same results using the smbmount command, as follows:

```
```bash
$ sudo smbmount //10.10.10.20/homes /mount/point -o username=ahudson,dmask=777,\
  fmask=777
```
```

To unmount the share, use the following standard command:

```
```bash
$ sudo umount /mount/point
```
```

You can also use these mount commands to mount true Windows client shares to your Ubuntu host. Using Samba, you can configure your server to provide any service Windows can serve, and no one but you will ever know.

# Configuring Samba Using SWAT

The Samba team of developers has made administering Samba much easier with the *Samba Web Administration Tool (SWAT).* SWAT is a web-based configuration and maintenance interface that gets as close to a point-and-click Samba environment as possible. This section provides a simple example of how to use SWAT to set up SMB access to a user’s home directory and how to share a directory.

> **NOTE**
> 
> Using SWAT requires you to install the `openbsd_inetd` and `swat` packages, so make sure you have these before proceeding.
> 
> Also you need to enable the root account by giving it a password by using the command `sudo passwd root`. Not enabling the root account prevents you from using SWAT effectively.

You need to perform a few steps before you can start using SWAT. First, make sure you have the Samba and the swat packages installed. You then enable SWAT access to your