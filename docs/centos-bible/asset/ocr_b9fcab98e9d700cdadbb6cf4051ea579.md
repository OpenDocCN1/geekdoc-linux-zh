# Chapter 17

# Setting Up a File Server

When groups of people need to work together on projects, they usually need to share documents. Likewise, it can be efficient for groups of people on a computer network to share common applications and directories of information needed to do their jobs. A common way to store files centrally and share them on a network is by setting up a file server.

CentOS systems include support for each of the most common file server protocols in use today. The Network File System (NFS) has always been the file-sharing protocol of choice for Linux and other UNIX systems. Networks with many Windows computers tend to use Samba, or SMB/CIFS (Server Message Block/Common Internet File System) protocol. This chapter describes how to set up file servers and clients associated with NFS and Samba, and file servers set up in Linux.

> **CROSS-REF** Two other types of file servers are also described in this book: FTP (using vsFTP) and HTTP (using Apache). To set up public FTP file servers, refer to Chapter 19. Chapter 20 discusses how to set up a Web Server.

# Goals of Setting Up a File Server

+   By centralizing data and applications on a file server, you can accomplish several goals:
+   
+   *   **Centralized Distribution** — You can add documents or applications to one location and make them accessible to any authorized computer or user. In this way, you don't have to be responsible for placing necessary files on every computer.

**IN THIS CHAPTER**

Setting up an NFS file server in Linux
Setting up a Samba file server in Linux