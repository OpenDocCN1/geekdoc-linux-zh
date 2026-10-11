editing the /etc/exports file. But, these will be lost if the server is rebooted. An example is as follows:

    exportfs -o no_root_squash norbert:/public

This command would share the /public directory to the host norbert with the no_root_squash option.

![](bbox=[0.13, 0.27, 0.19, 0.32])

> Any time a change is made to the /etc/exports file, the exportfs -a command should be run.

| Table 16-19 exportfs Options | | | | | | | | | | | | | | |
| Option | Function |
| -a | Alone this option causes the NFS server to export all directories in the /etc/exports file. With the -u option it causes the NFS server to stop exporting all directories. |
| -o | Specify a list of export options, as done in the /etc/exportfs file. |
| -i | Ignore the /etc/exports file. Use only commands given on the command-line of exportfs. |
| -r | Reexport all directories contained in /etc/exportfs. If any exports were manually created using exportfs, they are no longer shared. |
| -u | Unexport one or more directories. |
| -v | Verbose. |

# Mounting exported directories

Mounting exported directories from a client is very similar to mounting local file systems. The mount command is used with the following syntax:

mount host:/directory /mount_point

An example would be the following:

mount norbert:/home /mnt/norbert

This would mount the /home directory shared out from the system named norbert to the local directory named /mnt/norbert. Remote file systems can be mounted at boot with an entry in the /etc/fstab file, such as the following:

```
# filesystem mountpoint fstype flags dump fsck
norbert:/home /mnt/norbert nfs rw 0 0
```