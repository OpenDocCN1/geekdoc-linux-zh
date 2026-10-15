# 5.3.11 The CMS Shared File System

z/OS programmers might be familiar with the z/OS UNIX System Services (z/OS UNIX or UNIX System Services), which allows z/OS to access UNIX files. The most noticeable difference between the z/OS UNIX file system and z/OS data sets is that z/OS UNIX is a hierarchical file system when accessed from within UNIX System Services.

The z/VM file system, CMS Shared File System (SFS), allows you to view the system in a hierarchical fashion: z/OS programmers might be more accustomed to this type of hierarchical file system.

SFS is an additional file system that is shipped with z/VM, and it offers several advantages over the normal CMS file system. Table 5-6 lists and compares these file systems.

# Table 5-6 Compare and contrast SFS and normal CMS file system

| Shared File System | CMS file system |
|---|---|
| Sharing at file level | Sharing at minidisk level |
| Minimum allocation: zero 4096 byte blocks | Minimum allocation: 1 cylinder |
| Hierarchical file system | Flat file system |
| Allocation can be changed dynamically | Bigger minidisk required |
| Recovery at file level | Recovery at minidisk level |

SFS is essentially a collection of minidisk storage managed by a server. The following three main areas are shown in Figure 5-4 on page 273:

+   **Control data**
+   Holds the definitions of the file pool and its users.
+   
+   **Log data**
+   Holds the logs so that, in the event of interruption, files can be rolled back.
+   
+   **User data**
+   Holds the user data. The server allocates data from here to give to users.