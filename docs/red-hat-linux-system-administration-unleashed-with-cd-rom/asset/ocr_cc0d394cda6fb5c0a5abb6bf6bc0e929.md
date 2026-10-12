If you later wanted to make the shared filesystem unavailable, you would use the smbumount command. This command has a syntax much like that of the normal mount command. Here is the example to unmount the previously mounted share:

```
smbumount /windows
```

In addition to the Samba suite, there is another part of Linux that enables clients running Linux to access filesystem shares on Windows networks. This part is the smbfs support, which you can compile into your kernel. The smbfs is an implementation of the SMB protocols that is based on Samba code. It allows you to mount SMB shares in a manner similar to NFS exported filesystems. To use this feature of the Linux kernel you must install the smbmount command from the Samba package; however, you are not required to run the smbd or the nmbd daemons. Red Hat goes one step further in that it provides a shell script wrapper to the smbmount program called /sbin/mount.smb that translates mount commands given in the standard mount syntax into the appropriate smbmount commands. Here is a sample of this functionality in action:

```
[root@nomad /root]# mount -t smbfs //quicksilver/public /mnt2
[root@nomad /root]# Added interface ip=192.168.50.25
bcast=192.168.50.255 netmask=255.255.255.0
Server time is Wed Jul 14 23:35:57 1999
Timezone is UTC-5.0
Password:
Domain=[ALCHEMY] OS=[Unix] Server=[Samba 2.0.3]
connected as guest security=user
```

```
[root@nomad /root]# df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda2 1478572 1133273 268893 81% /
//QUICKSILVER/PUBLIC 1072672 214176 658496 20% /mnt2
```

```
[root@nomad /root]# ls -l /mnt2
total 3
-rwxr-xr-x 1 root root 261 Jul 14 00:00 README
drwxr-xr-x 1 root root 512 Jul 13 23:57 accounting
drwxr-xr-x 1 root root 512 Jul 13 23:57 development
drwxr-xr-x 1 root root 512 Jul 13 23:57 humanresources
drwxr-xr-x 1 root root 512 Jul 14 00:00 miscellaneous
drwxr-xr-x 1 root root 512 Jul 13 23:57 techops
```