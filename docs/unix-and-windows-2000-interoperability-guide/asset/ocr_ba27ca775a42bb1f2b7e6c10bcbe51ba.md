# Chapter 12 • CIFS File Sharing

However, in order to secure each user's home directories, we must ensure that those directories reside on NTFS volumes and then assign the appropriate NTFS permissions. Done properly, all CIFS/9000 clients will be able to access the home share, but each subdirectory within that share will be protected by NTFS permissions.

In our example, we secure the Dylan subfolder of the home directory by right-clicking on its icon, choosing Properties, and then clicking the Security tab (see Figure 12–6).

![](bbox=[0.105, 0.275, 0.675, 0.768])

Figure 12–6 Securing a folder with NTFS permissions.

Note that only Dylan has permissions to control this folder. This will keep others from messing with this folder despite the fact that Everyone has Full Control permission on the home share.