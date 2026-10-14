When removable media such as CD-ROMs are mounted, the Eject function of the drive is disabled until the device is unmounted. This is not true of removable disk drives, which means it is possible for a user to eject a removable disk while it is still mounted. This can cause minor problems, or even result in lost data. For example, files will still be marked as open even though they cannot be accessed.

# Using Networked File Systems

Although a complete discussion of networked file systems is beyond the scope of this book, you should be aware that many Linux networks use these file systems to share data transparently over the network. Additional information is provided in Chapter 15, "Advanced Topics and Troubleshooting."

> A more complete discussion of networked filed systems is included in Chapter 5 of Guide to Linux Networking and Security (Course Technology 2003, ISBN 0-619-00094-5).

You already know that you can use a Web browser, an FTP client, or various command-line utilities to access data located on another computer. You can also use the mount command to make a directory on another computer appear as part of your local file system. This is similar to the idea of "mapping a network drive" in Microsoft Windows, where you assign a Windows share to a drive letter. Because Linux doesn't use drive letters, you might guess that you mount a networked file system to a subdirectory where it can be accessed.

Networked file systems in Linux are normally accessed using either the Network File System (NFS) or Server Message Block (SMB) protocols. A system administrator might tell you, for example, that you have access to a networked file system via NFS that is located on the server named glasgow in the directory /doc_archive. You decide to mount that file system on your computer in the subdirectory /glasgow_docs, which you have already created using mkdir. You can then mount the networked file system using this command, entering the password given to you by the administrator if prompted (a password is usually not needed):

```
# mount -t nfs glasgow:/doc_archive /glasgow_docs
```

# Automating File System Mounting

As a system administrator, you want to automate everything that you can so that your time is free for tasks that require new analysis and problem-solving skills. As you saw earlier, several types of file systems are mounted automatically when you start Linux. New file systems that you create from additional hard disks or other devices can also be automatically mounted at boot time.

The key to automounting file systems is the /etc/fstab configuration file. This file contains one line for each file system that you want to have automounted when Linux boots. It also