Total space:

Free space:

+   7. Click the **Exit** button to return to the Login window, and leave your Web browser open for the next activity.

![](bbox=[0.1, 0.19, 0.16, 0.25])

NOTE: On some OSs, clicking the **Exit** button might automatically close the Web browser. If this happens, you'll need to restart your Web browser.

# Directories and Subdirectories

Just as file cabinet drawers are organized by using hanging folders, NetWare volumes are divided into multiple directories and subdirectories, which enable you to keep files in a volume separated. You can also place space restrictions on directories and subdirectories to prevent certain applications or users from occupying too much of a volume's disk space. As a CNA, you must know which directories NetWare 6.5 needs and how to create directories for organizing data. In the following sections, you learn about the NetWare required directories along with suggested directory structures that you can use to meet your organization's data and software storage needs.

As shown in Table 3-2, the NetWare OS stores its required system files and utilities on the SYS volume under several directories. The most common directories administrators use include Login, Public, and System. The following sections explain how NetWare uses these three directories and where certain types of files are stored.

# Table 3-2 System-created directories

| Directory Name | Purpose |
| :--- | :--- |
| Apache | Contains the Apache Web Server files |
| Audit | Contains files for auditing system activity and Web server access |
| Etc | Contains configuration files for TCP/IP and the certificate server |
| iFolder | Contains configuration files for iFolder, covered in Chapter 10 |
| Java | Contains Java language files |
| Login | Files and software available to clients before logging in to the network |
| Mail | Contains no files and is used for backward compatibility with earlier versions of NetWare |
| Ndfs | Contains files used with Novell Distributed Print Services, covered in Chapter 8 |
| Netbasic | Contains files needed to run the NETBASIC language used with certain Web applications |
| NetStorage | Configuration files and software for NetStorage, covered in Chapter 10 |
| Ni | Contains configuration and software used by Certificate Services security |
| Novonyx | Contains Web server files for the Novonyx Web server |