
## Table 15.2 /etc/exports Options

| Option | Description |
|---|---|
| ro | Allows read-only access to the filesystem. |
| rw | Allows read-write access to the filesystem. |
| noaccess | Disallows access to a particular branch of an exported tree. |
| secure | Requires that requests originate on a secure port (one in the < 1024) range. This is the default. To disable this option, specify insecure. |
| map_daemon | Maps differing ids between client and server systems by using the ugid mapping daemon. |
| map_static=file | Maps differing ids between client and server systems by using a text file specified as an option argument. |
| map_nis=nisdomain | Maps differing ids between client and server systems by doing NIS lookups. |
| no_root_squash | Allows root on the client system access to the filesystem with root privileges. Default is root_squash. |
| all_squash | Maps all ids to the anonymous user. This is opposite of the default action. |
| anonuid=uid | The id that user accounts are mapped to if either the root_squash or all_squash options are specified. The default is user nobody (65534). |
| anongid=gid | The group id that user accounts are mapped to if either the root_squash or all_squash options are set. The default is group nogroup (65534). |

Now that you have an example of the format of the /etc/exports file and have a list of the available options, we can look at the syntax rules for the remainder of the file. Each entry of the file consists of three parts: the host specification, the filesystem specification, and the options list. The host specification can take one of several forms. The first form is a single hostname. This is fine for exceptions to general rules, but can become quite tedious if you need to specify every host of a large network. Another method of specifying hosts is to use NIS network group specification, given in the form @group. In this case, the host part of netgroup members is extracted and added to the access list, unless the host part consists of a single hyphen. This form can save you a lot of typing if you are running NIS. The next form is the wildcard form, in which you could specify an entire domain using an entry such as *.dejanews.com to specify all hosts in the dejanews.com domain consisting of the form host.dejanews.com. Please note that this will not include hosts in the form host.subdomain.dejanews.com. Yet another form that is accepted by the exports file is the IP network form, in which you can specify an IP/netmask pair to grant access to all systems matching that specification; for example, 192.168.50.0/255.255.255.0 to match all addresses on the class C network 192.168.50.0. These several forms are shown in the following example /etc/exports file:

```
/etc/exports

#
# /etc/exports
#
/home @workstations(rw) @admins(rw,no_root_squash)
/opt *.dejanews.com(ro) admin(rw,no_root_squash)
/opt/private (noaccess)
/vol/00 192.168.50.0/255.255.255.0(rw) 10.16.0.0/255.255.0.0(rw)
```

Now that you have ensured that the appropriate network daemons have been installed, decided which filesystem to export and with what options, and have constructed the /etc/exports file, you are ready to actually make the filesystems available on the network. This can be done with the exportfs command. This command has just a few options, as defined in Table 15.3.

## TABLE 15.3 exportfs Options

| Option | Description |
|---|---|
| -a | Exports or unexports all directories. |
| -o options | Specifies a list of export options like those in the /etc/exports file. |
| -r | Re-exports all directories and synchronizes /etc/exports with /var/lib/nfs/xtab. |
| -u | Unexports one or more directories. |
| -v | Verbose flag. |

This command is new to Linux and was first included with the kernel NFS daemon implementation. Prior to this, filesystems were exported or re-exported by manually killing off and restarting the mount daemon and nfs daemon, such as happens when you run the /etc/rc.d/init.d/nfs script with the restart option. If you want, you can still do this, but using the exportfs command is much easier and less disruptive to attached clients, since it does not stop the NFS daemons like the script does. Here is an example showing the transition from a server with an exports file to a Linux NFS server:

```
[root@quicksilver /etc]# showmount -e
Export list for quicksilver.alchemy.net:

[root@quicksilver /etc]# cat /etc/exports
/mnt/cdrom 192.168.50.0/255.255.255.0(ro,root_squash)
/home wizard(rw,no_root_squash)
/usr/local *.alchemy.net(ro,root_squash)
```

```
[root@quicksilver /etc]# exportfs -a
```

```
[root@quicksilver /etc]# showmount -e
Export list for quicksilver.alchemy.net:
/usr/local *.alchemy.net
/mnt/cdrom 192.168.50.0/255.255.255.0
/home wizard.alchemy.net
```

As you can see, the server quicksilver is now exporting the filesystems /mnt/cdrom, /home, and /usr/local. The following section looks at setting up an NFS client system.

## NFS Client Configuration

Having set up the server, you are now ready to look at what is required to set up a client to the NFS server. This is actually quite easy. The first thing that you must do is to verify that you have support for NFS built in to your kernel. This can be accomplished by examining the /proc/filesystems file and finding an entry for NFS or by verifying the existence of the nfs.o module in the modules directory for your kernel. Assuming that you have included support for the NFS filesystem type in your kernel, you must do three things in order to access a filesystem shared via NFS. These things are

- Ensure that you have access to the resource and request it if you do not.
- Modify the /etc/fstab file to include the information about the filesystems you want to mount.
- Create the appropriate mount points and mount the filesystems.

You can ensure that you have access to the resource using the same command used to verify that the filesystems were exported in the first place—showmount. The difference this time is that you will be passing the name of the NFS server as an argument to the showmount command. This will look something like this:

```
[root@wizard /etc]# showmount -e quicksilver
Export list for quicksilver.alchemy.net:
/usr/local *.alchemy.net
/mnt/cdrom 192.168.50.0/255.255.255.0
/home wizard.alchemy.net
```

From the showmount output, you can see that the client machine you are setting up, wizard, which has an IP address of 192.168.50.20 and is part of the alchemy.net domain, should be able to access all of the exported filesystems from quicksilver. That being the case, you can now proceed to step two. If this had not been the case, you would have requested access from the administrator of quicksilver, or if you administer it yourself,

simply modify the /etc/exports file on quicksilver to add wizard and re-export all of the filesystems with the command

```
exportfs -r -a
```

Step two is to modify your /etc/fstab file on wizard. The decisions you made earlier on what characteristics the mounted filesystem should have again come into play here, specifically the question regarding setuid binaries and execution of programs. The answers to these questions are used when setting the options field in the /etc/fstab file. Some of the most common options applicable to NFS filesystems are shown in Table 15.4.

## Table 15.4 NFS mount Options

| Options | Description |
|---|---|
| bg | If an initial attempt at mounting an NFS filesystem fails, retries in the background. |
| fg | If an initial attempt at mounting an NFS filesystem fails, continues to retry in the foreground. (default) |
| soft | A major timeout on an NFS operation results in an I/O error being returned to the application. |
| hard | A major timeout results in continuous retries. |
| rsize=n | Sets the number of bytes for NFS read operations. The default is 1024. |
| wsize=n | Sets the number of bytes for NFS write operations. The default is 1024. |
| intr | Allows file operations to be interrupted by signals. This is not the default. |
| nosuid | Does not allow setuid or setgid bits to take effect for binaries located on the filesystem. |
| noexec | Does not allow the execution of programs or scripts on the mounted filesystem. |

To continue with the example, you will modify the /etc/fstab file on wizard and mount the /home and /usr/local filesystems. The /home filesystem will be mounted read-write, with setuid and setgid binaries disallowed, and root on the client system mapped to root on the server. The /usr/local filesystem will be mounted read-write, with root on the client system mapped to root on the server. These options allow wizard to act as an administrative client for these filesystems. If you wanted to make wizard a simple client, you would remove the no_root_squash options from the mount options for /home and the no_root_squash and read-write options from the mount options for /usr/local. To implement this, here are the entries from /etc/fstab for these two filesystems:
