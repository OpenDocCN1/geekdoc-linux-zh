# Windows 2000 NFS Server/HP-UX NFS Client

+   6. If the NFS client is not already enabled, you will get a message asking you if you wish to enable it. Select Yes to proceed.

+   7. Fill in the necessary information in the Add Remote File System dialog box. (See Figure 11–13.)

![](bbox=[0.076, 0.233, 0.758, 0.683])

**Figure 11–13** The Add Remote File System mount point on hpux called /pcmnt.

In my example, I created a mount point on hpux called /pcmnt. This is the value of the Local Directory Name box. Earlier, I had created an NFS share on w2kserv called music, whose path name was D:\music. Therefore, Remote Server Name is w2kserv.book.local and the remote directory name is /music. Actually, so what I supplied here is the share name preceded by a slash (/). Pressing OK will execute the mount w2kserv.book.local:/music command with the default option values and will ensure that the mount will also take place at system boot. The primary default mount options are listed in Table 11–1.