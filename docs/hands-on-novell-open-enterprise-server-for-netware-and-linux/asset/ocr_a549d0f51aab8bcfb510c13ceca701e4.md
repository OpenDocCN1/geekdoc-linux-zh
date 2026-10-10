# **NetWare File System Components**

The NetWare file system offers many benefits for making information available on a network. These benefits can be classified into the following categories:

+   - **Centralized management of data and backups**—When data is stored on a server, many users can have access to centralized database files that contain current and accurate information. In addition, centralizing data enables critical files to be backed up regularly and makes it easier to recover from lost data or a file server failure.

+   - **Improved security**—Prevents users from modifying or accessing data that they aren’t responsible for maintaining or aren’t authorized to use.

+   - **Improved reliability and fault tolerance**—NetWare’s disk-mirroring and duplexing features can be used to ensure that duplicate copies of data are automatically available for users in the event of hardware failures. NetWare 6.5 includes disk clustering technology that allows multiple servers to share access to the same networked disk system. In this chapter, you learn how disk clustering can be used to increase reliability and fault tolerance.

+   - **Shared and private storage areas**—Shared storage areas enable users to share files or transfer files to other users without having to carry disks between machines. With private storage areas, users can save their own work in a secure area of the file server.

+   - **Access to data**—An important part of Novell’s Open Enterprise vision is giving users access to the data and documents they need from a computer attached to any interconnected network by using common clients and operating systems (OS). In this chapter, you learn how Novell’s Native File Access Pack (NFAP) allows the NetWare file system to support Apple, Linux, and Windows clients, which reduces hardware costs because there’s no need for separate servers to support each OS. As more users and applications are added to the network, it becomes more important for a CNA to know how to give users secure access to the data they need, both inside and outside the corporate network.

Because of the importance of organizing and securing the information stored on the network, a good file system design is necessary to facilitate your network’s setup, use, and growth. Starting with NetWare 6.0, Novell improved the network file system by implementing **Novell Storage Services (NSS)** version 3. Earlier versions of NSS included with NetWare 5.0 were more complex to implement and didn’t support the SYS volume. As a result, on NetWare 5.0 servers NSS was typically used only with very large data volumes. Because of the advanced features of NSS, Novell has made NSS version 3.2 the primary file system on all NetWare 6.5 volumes, including the SYS volume. As you learned in Chapter 2, an NSS SYS volume of at least 4 GB is required during NetWare 6.5 installation.

As shown in Figure 3-1, the main components of the NetWare 6.5 file system are disk partitions, storage pools, and volumes.

![](bbox=[0.11, 0.7, 0.45, 0.85])

**Figure 3-1** NetWare 6.5 NSS file system components

The disk drive is first divided into one or more partitions. The partition space from one or more drives is then combined to form storage pools. A single storage pool can contain space from one or more disk partitions. After a storage pool is created, volumes can be defined within that storage pool. Figure 3-2 shows an example