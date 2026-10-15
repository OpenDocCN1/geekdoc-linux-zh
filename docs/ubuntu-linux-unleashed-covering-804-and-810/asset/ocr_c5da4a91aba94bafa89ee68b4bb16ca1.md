# NFS Server Configuration

You can configure the NFS server by editing the /etc/exports file. This file is similar to the /etc/fstab file in that it is used to set the permissions for the file systems being exported. The entries look like this:

```
/file/system yourhost(options) *.yourdomain.com(options) 192.168.0.0/24(options)
```

This shows three common clients to which to share /file/system. The first, yourhost, shares /file/system to just one host. The second, .yourdomain.com, uses the asterisk (*) as a wildcard to enable all hosts in yourdomain.com to access /file/system. The third share enables all hosts of the Class C network, 192.168.0.0, to access /file/share. For security, it is best not to use shares like the last two across the Internet because all data will be readable by any network the data passes by.

Table 16.1 shows some common options.

# TABLE 16.1 /etc/fstab Options

| Option | Purpose |
| --- | --- |
| rw | Gives read and write access |
| ro | Gives read-only access |
| async | Writes data when the server, not the client, feels the need |
| sync | Writes data as it is received |

The following is an example of an /etc/exports file:

```
# /etc/exports: the access control list for filesystems which may be exported
#               to NFS clients.  See exports(5).
/home/andrew 192.168.0.0/24(rw,no_root_squash)
```

This file exports (makes available) /home/ahudson to any host in 192.168.0.* and allows users to read from and write to /home/andrew.

After you have finished with the /etc/exports file, the following command

```
$ sudo exportfs -a
```

exports all the file systems in the /etc/exports file to a list named xtab under the /var/lib/nfs directory, which is used as a guide for mounting when a remote computer asks for a directory to be exported. The -r option to the command reads the entire /etc/exports file and mounts all the entries. You can also use the exportfs command to export specific files temporarily. Here's an example using exportfs to export a file system:

```
/usr/sbin/exportfs -o async yourhost:/usr/tmp
```

This command exports /usr/tmp to yourhost with the async option.