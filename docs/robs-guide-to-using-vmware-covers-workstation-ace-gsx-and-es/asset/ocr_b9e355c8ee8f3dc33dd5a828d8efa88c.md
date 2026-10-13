# Samba

To create the Samba share, use the mount command following this syntax:

```
mount -t smbfs -o username=<user>,password=<pw>
    //<ip | host>/sharename <mount point>
```

To mount the share to /mnt/iso as a special user with read-only rights:

```
mount -t smbfs -o username=iso,password=secret
    //isosrv/isos hare /mnt/iso
```

Alternatively, when you want to set this up to be loaded automatically when your ESX Server boots, you want to add the following to your /etc/fstab file. As an example for the previous command line:

```
//isosrv/isos hare  /mnt/iso  smbfs
    ip=isosrv,username=iso,password=secret,noauto 0 0
```

# NFS

When your files are on another Linux host, or an ESX Server, you can set up an NFS export, to which your ESX Server can point to. On the host where the files reside, create the export manually with the following command:

```
exportfs <host>:/path
```

To share the /iso directory with the host called esx2:

```
exportfs esx2:/iso
```

To permanently add this NFS export to your host, add it to the /etc/exports file in the following, commonly used format:

```
/iso/  esx1(ro,root_squash,sync)
```

On the server, where you want to configure access to the files, you first have to make sure that the two necessary daemons are loaded. You can do this manually with the following commands:

```
/etc/init.d/netfs start
/etc/init.d/portmap start
```

When the daemons are loaded, use the following command to manually mount the NFS location to a directory:

```
mount -t nfs <ip | host>:/path <mount point>
```