# Chapter 26: File Transfer and Sharing

| Server | Comment |
| --- | --- |
| Workgroup | Master |
| WVH | HD-HTGLOB5 YM901252 |

You can use the information from either of these examples to identify the name of the share that you want to mount and the server from which that directory is shared. You will need this information to mount share on your Ubuntu system using any of the mechanisms described in the next few sections.

# Mounting Windows Shares at Boot Time

If you know that you will frequently need to access files and directories in a Windows share, the easiest way to make that permanently available is to add it to the list of filesystems that your Ubuntu system mounts when system boots. Of Chapter 4, "Basic Linux Systems Concepts," entitled "Automatically Mounting Filesystems at Boot Time" explains the file text that contains the list of filesystems your system knows about and that can be mounted at boot time. This section explains the specific entries that are necessary when mounting a networked Windows shared directory at boot time.

If you know the name and associated server for the Windows share that you want to mount, you have all of the information that you need to mount on your Ubuntu system. If not, you can use the information from either of the examples in the previous section to get the share and server name. To mount share on your system each time you start your system, add an entry for the Windows share that you want to mount to the file /etc/fstab. For example, to mount the office share shown in the previous example on the directory /mnt/office (which must already exist), you would create anetc/fstab entry like the following:

```
//192.168.6.2 /mnt/office cifs \
auto.credentials=/etc/cifs.login,uid=0,gid=users 0 0
```

(This entry would appear on a single line in the /etc/fstab file — the backslash is only present for formatting purposes.)

The only unique portions of this entry are the mount options, which have the following meanings:

+   - Auto: Automatically the filesystem when the system boots.
- credentials=/etc/cifs.login: Identifies the name of a file that contains the username and password to authenticate when mounting the filesystem. Because the /etc/fstab file is usually publicly readable, you do not want to embed this information in that file for security reasons. You should put this information in a separate file and change that so that it can only be read by root (sudo chmod g-r,o-r /etc/cifs.login). This file should contain two lines of the following form:

```
username=USERNAME
password=PASSWORD
```