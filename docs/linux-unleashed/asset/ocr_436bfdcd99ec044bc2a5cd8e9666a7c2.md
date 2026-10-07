There is a simpler way to mount commonly used directories. Put the names of the directories and their mount points in the `/etc/fstab` or `/etc/vfstab` file (the file to use depends on the version of Linux). Then you can mount the files by simply issuing the mount point name. For example, this command mounts the proper filesystem as `/skunk`:

`mount /skunk`

# ## Summary

As you have seen in this chapter, NFS is not very complex to set up, either as a client or server. With a few minutes work you can start sharing your directories and accessing directories on other machines. NFS is a very fast and easy way to access applications and copy files on remote machines. Although the configuration is dependent on the operating system version, a quick check of help screens or man pages will show you the proper format of the commands used in this chapter.

From here you can find related information:

+   - NIS and YP, which let you manage passwords network-wide, are discussed in Chapter 44, “NIS and YP.”
- Automating processes on your system using the cron utility, very handy for system administrators, is discussed in Chapter 46, “cron and at.”
- Setting up an Internet server is discussed in Chapter 47, “Setting up an Internet Site.”

![](bbox=[0.81, 0.45, 0.98, 0.6])