+   ■ File services—These services enable client computers to access and save data on a shared file system. In Chapters 3 and 6, you learn how to set up and secure the NetWare file system, and Chapter 13 explains how to implement file system security on a Linux server.

+   ■ Print services—These services allow printers to be attached to the network system and used by client computers. In Chapter 8, you learn how to set up, secure, and maintain a network printing system that supports both local and Internet printing.

+   ■ Application services—These services assist in running programs, such as spreadsheets, word processors, and database systems, by performing certain processing functions for client computers. Chapter 9 describes how to set up a client computer environment to support network applications.

# # INTRODUCTION TO NETWORK OPERATING SYSTEMS

The network operating system (NOS) is the software that controls network services and provides access to shared resources on the server computer. Historically, a major function of a network operating system has been to provide file and printer services to client computers. As a result, the server can be enhanced with specialized hardware and software to improve performance, security, and reliability beyond what can be expected from a desktop operating system, such as Windows 2000 Professional or Windows XP. The NOS is specialized to maximize use of the server’s hardware by including the following features and services:

+   ■ Performance—A server’s performance is determined by how fast it can respond to requests for data from client computers. Therefore, the main factors affecting a server’s performance are its capability to keep frequently used information in memory, the speed of its disk system, and the speed of its processor unit.

+   ■ Fault tolerance—Fault tolerance is the system’s capability to continue operating satisfactorily when there are errors or other problems. The server environment is designed with different levels of fault tolerance so that it can continue server operations despite physical errors on the disk drives or controller cards.

+   ■ Security—Security (preventing unauthorized access to information on the server) is one of the most important responsibilities of a network administrator. An NOS has features you can use to meet the security needs of your organization’s users and data. For example, login security requires all users of the system’s resources and services to supply a valid user name and optional password before being given access to the network. In addition, the option intrusion protection system, described in Chapter 5, can be used to lock out a user’s account if someone exceeds the number of login attempts you have set.

+   ■ Trustee assignments—Trustees are objects such as users and groups that are given permission to use or manage resources. You use trustee assignments to assign privileges, called trustee rights or permissions, to network users allowing them to access data and perform certain functions on the network.

+   ■ Client support—An NOS should be able to support many types of client computers so that a network can integrate diverse computing environments. For example, you learned how the NetWare operating system enables Apple Macintosh users to share files with Linux and Windows-based computers.

As shown in Figure 1-11, today’s NOSs can be defined as peer-to-peer or network-centric, depending on how they are designed.

Peer-to-peer systems enable client computers to communicate and share data with each other without the need for a dedicated server computer. In a peer-to-peer network, computers are organized into units called workgroups. Workgroups make it easier for users to find shared resources because administrators can group computers by department. Windows 98, Windows 2000 Professional, and Windows XP are designed as peer-to-peer operating systems. The main advantage of peer-to-peer systems is their capability to implement low-cost networks by saving the expense of dedicating a computer as a server. In addition, peer-to-peer systems let users in workgroups share data files and communicate easily with each other. In theory, this reduces the burden on the network administrator by placing more responsibility for data sharing in the hands of users.