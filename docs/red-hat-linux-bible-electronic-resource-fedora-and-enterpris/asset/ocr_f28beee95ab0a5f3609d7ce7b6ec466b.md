# # Chapter 18

# # Setting Up a File Server

## In This Chapter

+   - Setting up an NFS file server in Red Hat Linux
+   - Setting up a Samba file server in Red Hat Linux
+   - Setting up a NetWare file server in Red Hat Linux

When groups of people need to work together on projects, they usually need to share documents. Likewise, it can be efficient for groups of people on a computer network to share common applications and directories of information needed to do their jobs. A common way to centrally store and share files on a network is by setting up a file server.

Red Hat Linux includes support for each of the most common file server protocols in use today. The Network File System (NFS) has always been the file-sharing protocol of choice for Linux and other UNIX systems. Networks with many Windows and OS/2 computers tend to use Samba (SMB protocol). Prior to SMB, NetWare was the most prominent file-server software used on local area networks (LANs).

This chapter describes how to set up file servers and clients associated with NFS, Samba, and NetWare file servers set up in Linux.

> **CROSS-REFERENCE:** Two other types of file servers are also described in this book: FTP (using vsftpd) and AppleTalk (using netatalk). To set up public FTP file servers, refer to Chapter 20. Chapter 26 describes how to set up a netatalk server for file sharing with Apple computers.

# ## Goals of Setting Up a File Server

By centralizing data and applications on a *file server*, you can accomplish several goals:

+   - **Centralized distribution** — You can add documents or applications to one location and make them accessible to any computer or user that is granted permission. In this way, you don’t have to be responsible for placing necessary files on every computer.
+   - **Transparency** — Using protocols such as NFS, clients of your file server (Windows, Linux, or UNIX systems) can connect your file systems to their local file systems as if