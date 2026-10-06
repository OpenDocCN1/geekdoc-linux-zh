# Chapter 18 ✦ Setting Up Windows Interoperability with Samba 503

![](bbox=[0.181, 0.137, 0.616, 0.429])

Figure 18-7: Browsing SMB resources using LinNeighborhood

# # Mounting a Shared Windows Drive

There are many ways to mount a shared Windows drive on your SUSE system, the easiest of which is to use the standard Linux mount command. For example, to mount an SMB share named vwh that is available on an SMB server named home, mount that on the directory /mnt/smb, and access those files as the Windows user vwh, you would execute a command as the following with the root user:

```
# mount -t smbfs -o username=vwh //home/vwh /mnt/smb
```

The previous command line can be broken down as follows:

+   - t smbfs-vwh—Identifies the type of filesystem that you are mounting as smbfs filesystem (SMB filesystem).
- o username=vwh—Passes the username to the mount command, which identifies your Windows user login as vwh.
- /home/vwh—The name of the Windows directory that you want to mount on your SUSE system. In this example, this is a directory named vwh on your Windows server named home.
- /mnt/smb—The directory on your SUSE system where you want to mount the specified Windows directory.