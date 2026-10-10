Table 3-2 System-created directories (continued)

| Directory Name | Purpose |
| :--- | :--- |
| Nss | Contains files used by Web Services |
| Odbc | Contains database and configuration files for Web Services |
| Perl | Contains programming software used by Web Services |
| Public | Contains files and software available to all users after logging in |
| Pvsw | Contains license file information |
| Queues | Used for backward compatibility with legacy NetWare print queues, described in Chapter 8 |
| System | Contains files and software used by the NetWare operating system |
| Tmp | Used to store temporary files |
| Ucs | Contains NetWare modules used by the operating system |
| Webapps | Contains Web application software for NetStorage, Web Manager, and WebAccess |
| XTier | Contains NetWare Loadable Modules used by the operating system |
| Zenworks | Contains applications and configuration files for the Z.E.N.works application management system, described in Chapter 9 |

# Login

The **Login** directory contains files and programs that can be accessed before logging in. In the past, DOS clients used the Login directory to access commands needed to log in to the network. NetWare 6.5 makes use of the Login directory to find commands needed to access or start network services from a Web browser. Three important DOS programs in the Login directory are Cx.exe, Map.exe, and Login.exe. These utilities are mostly used when logging in from or working on DOS-based computers. In addition to storing DOS commands, many network administrators like to use the Login directory to store files and programs that users often use during the startup process. When these programs release a new version, you can update them easily by simply copying the new software into the Login directory, instead of having to copy them to each computer's hard disk drive.

# Public

The **Public** directory contains utility programs and files, such as the CX, MAP, and RIGHTS commands, that are available to all users after they have logged in. You use these commands in later chapters. ConsoleOne and NetWare Administrator are also stored in the Public directory.

# System

The **System** directory contains NetWare OS files and utilities that are accessible only to the network administrator. Many of these system files are flagged as Hidden and System to protect them from accidental access. Only the Admin user should be given rights to the System directory to avoid the possibility of users erasing or modifying system files and using commands that affect the file server's functioning. Some network administrators move program files they don't want users to run, such as NetWare Administrator, from the Public directory to the System directory. This improves security by preventing users from using that utility to browse the eDirectory database.

# Other System Directories

In addition to the three major system directories, you also find the Etc and Deleted.sav directories on the SYS volume. NetWare 6.5 creates the Etc directory to store sample files that help configure the server for the TCP/IP network protocol. To help users recover lost files, the Deleted.sav directory is created automatically on each volume and is part of NetWare's file recovery system that enables you to salvage a file even after the