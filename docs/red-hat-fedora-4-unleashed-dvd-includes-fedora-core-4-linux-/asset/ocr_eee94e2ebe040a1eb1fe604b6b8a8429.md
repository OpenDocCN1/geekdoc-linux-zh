This gives you the following prompt:

```
smb: <current directory on share>
```

From here, the commands are almost identical to the standard Unix/Linux FTP commands. Note that you can omit a password on the smbclient command line. You are then prompted to enter the Samba share password.

# Mounting Samba Shares

There are two ways to mount Samba shares to your Linux host. Mounting a share is the same as mounting an available media partition or remote NFS directory except that the Samba share is accessed using SMB. (See Chapter 37, “Managing the File System,” to see how to mount partitions.) The first method uses the standard Linux mount command:

```
mount -t smbfs //10.10.10.20/homes /mount/point -o username=jkennedy,dmask=777,\
fmask=777
```

> **NOTE**  
> The hostname can be substituted for an IP address if your name service is running or the host is in your /etc/hosts file.

This command mounts jkennedy’s home directory on your host and gives all users full permissions to the mount. The permissions are equal to the permissions on the chmod command.

The second method produces the same results using the smbmount command as follows:

```
# smbmount //10.10.10.20/homes /mount/point -o username=jkennedy,dmask-777,\
fmask=777
```

To unmount the share, use the standard

```
# umount /mount/point
```

These mount commands can also be used to mount true Windows client shares to your Fedora host. Using Samba, you can configure your server to provide any service Windows can serve, and no one but you will ever know.

# Configuring Samba Using SWAT

The Samba team of developers has made administering Samba a snap with the Samba Web Administration Tool (SWAT). SWAT is a web-based configuration and maintenance interface that gets as close to a point-and-click Samba environment as possible. This section provides a simple example of how to use SWAT to set up SMB access to a user’s home directory and how to share a directory.