# Backing Up and Restoring Files

# Mounting an NFS file system

To access an exported NFS file system on a client system, you have to mount that file on a mount point — which is, in practical terms, more than a local directory. For example, suppose you want to access the /home directory exported from the server named LNBP200 at the local directory /mnt/lnbp200 on the client system. To do so, follow these steps:

+   1. Log in as root, and create the directory with the following command:
mkdir /mnt/lnbp200

+   2. Type the following command to perform the mount operation:
mount lnbp200:/mnt/lnbp200

+   3. Change the directory to /mnt/lnbp200 with the command cd /mnt/lnbp200.

Now you can view and access exported files from this directory.

To confirm that the NFS file system is mounted, log in as root on the client system and type mount in a terminal window. You see a line similar to the one about the NFS file system:

```
lnbp200:/home/public /mnt/lnbp200 type nfs (rw,addr=192.168.1.200)
```

# Backing Up and Restoring Files

Backing up and restoring files is a crucial system-administration task. If something happens to your system's hard drive, you have to rely on the backups to recover important files. Here I present backup strategies, describe several backup media, and explain how to back up and restore files using the tape archive (tar) program that comes with Fedora Core. Also, you find out how to perform incremental and automatic backups on tapes.

If you have a CD burner, you can also back up files by recording them on a CD-R. Consult Book II, Chapter 4 for information on how to burn a data.

# Selecting a backup strategy and media

Your Fedora Core system drive contains everything you need to keep the system running — as well as other files (such as documents and databases) that you have to back up these files so you can recover quickly and bring the system back to normal in case the hard drive crashes. Typically, you have to follow a strict regimen of regular backups because you can never tell when the hard drive may fail or the file system may corrupt. To implement such a regimen, first decide which files you want to back up, how often, and what storage media to use. This process is what I mean by selecting a backup strategy and backup media.

![](bbox=[0.131, 0.423, 0.178, 0.474])

![](bbox=[0.131, 0.686, 0.198, 0.755])