# create mask= and create mode= (S)

These two are synonyms. They specify the maximum permissions for a newly created file. The DOS permissions (read-only, hidden, and so on) will further restrict it. The default is 744, meaning user gets all rights, but group and other get only read. If the owner later marks the file read-only from DOS, the file’s actual mode on the Linux box is changed to 544 to reflect the loss of write permissions.

# browseable= (S)

The `browseable` entry instructs the SMB client whether to list the share in an SMB client’s browser (such as Windows Explorer). It does not grant access to users not in the `valid users=` list, nor does `browseable=no` deny access to users in the `valid users=` list.

If set to `yes`, the existence of the share can be seen even by those without rights to the share. If set to `no`, it cannot be seen even by those in the `valid users=` list. However, in clients that allow a user to access a share not listed (`smbclient` and `net use`, for instance), `browseable=no` does not prevent a valid user from accessing the share, as long as the user enters the proper command with the proper share name. For instance, look at the following `smb.conf` share:

```
```
[valsdir]
comment = Valerie’s special directory
path = /home/everyone/valsdir
browseable = no
valid users = valerie
```
```

Execute the following command:

```
```$ smbclient -NL 192.168.100.1```
```

This is the yield:

| Sharename | Type | Comment |
| :--- | :--- | :--- |
| everyone | Disk | Accessible to everyone |
| IPC$ | IPC Service | (Jacks Samba Server) |
| jacksdir | Disk | Jack’s remote source code directory |
| lp | Printer | |
| myuidx | Disk | Myuid’s remote source code directory |
| spec_dir | Disk | Home Directories |
| valerie | Disk | |

Notice that share `valsdir` is not listed. That’s because it’s not browseable. However, access is not affected on SMB clients allowing a user to access an unlisted share by name. For instance, in SMB client `smbclient`, user `valerie` can issue the following command:

```
```$ smbclient //192.168.100.1/valsdir -U valerie```
```