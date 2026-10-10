# 434  Backing Up and Restoring Files

If you know only the IP address of the server, replace the host name (in this case, lnbp200) with the IP address.

+   3. Change the directory to /mnt/lnbp200 with the command cd /mnt/lnbp200.

Now you can view and access exported files from this directory.

To confirm that the NFS file system is indeed mounted, log in as root on the client system and type mount in a terminal window. You see a line similar to the following one about the NFS file system:

```
lnbp200:/home//public on /mnt/lnbp200 type nfs (rw,addr=192.168.1.200)
```

# Backing Up and Restoring Files

Backing up and restoring files is a crucial system administration task. If something happens to your system's hard drive, you have to rely on the backups to recover important files. Here I present some back up strategies, describe several back up media, and explain how to back up and restore files by using the tape archiver (tar) program that comes with Linux. Also, you find out how to perform incremental and automatic backups on tapes.

If you have a CD burner, you can also back up files by recording them on a CD-R. Consult Book II, Chapter 4, for information on what application you can use to burn a data CD.

# Selecting a back up strategy and media

Your Linux system's hard drive contains everything you need to keep the system running—as well as other files (such as documents and databases) that keep your business running. You have to back up these files so you can recover quickly and bring the system back to normal in case the hard drive crashes. Typically, you have to follow a strict regimen of regular backups because you can never tell when the hard drive may fail or the file system may get corrupted. To implement such a regimen, first decide which files you want to back up, how often, and what back up storage media to use. This process is what I mean by selecting a back up strategy and back up media.

Your choice of back up strategy and back up media depends on your assessment of the risk of business disruption due to hard drive failure. Depending on how you use your Linux system, a disk failure may or may not have much impact on you.