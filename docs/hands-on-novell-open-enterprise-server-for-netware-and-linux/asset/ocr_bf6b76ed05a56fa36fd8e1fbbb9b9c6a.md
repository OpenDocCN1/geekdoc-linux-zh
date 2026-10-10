as Linux and Macintosh, can access and manage Active Directory information because it offers LDAP compatibility. In the following section, you learn how to plan for installing and implementing eDirectory on a NetWare server.

# ## Novell eDirectory Services

As you learned in Chapter 1, **eDirectory** is Novell’s directory service that runs on a variety of network OSs, including Novell NetWare, Windows Server 2003, and Linux. Novell eDirectory gives network administrators the capabilities and tools to manage network resources, such as servers, users, and printers, from an organizational perspective. eDirectory is an LDAP-compatible directory service and database that maintains information about all network resources. The database is properly referred to as the “Novell eDirectory database,” but it’s often shortened to “directory database” or just “eDirectory.” All three terms refer to the same part of the eDirectory service. Novell has been perfecting the use of directory services since the early 1990s, when Novell Directory Services (NDS) was introduced in NetWare 4.0.

![](bbox=[0.11, 0.35, 0.2, 0.42])

Novell eDirectory was called Novell Directory Services (NDS) in earlier versions of NetWare. As a result, you might see references to “NDS” in Novell manuals and software.

# ### eDirectory Architecture

Novell’s eDirectory service, based on X.500 standards, offers several additional features over NDS, including:

+   - Client libraries and LDAP tools for Linux, Solaris, and Tru64 UNIX
+   - An import/conversion export (ICE) engine to import or export LDIF files and perform server-to-server migration
+   - A merge utility for combining eDirectory trees
+   - The iManager utility to manage eDirectory objects
+   - The iMonitor utility to monitor and diagnose servers in the tree from a Web browser
+   - The Index Manager utility to create and manage eDirectory database indexes
+   - The capability to run on multiple platforms, including NetWare, Windows NT, Windows 2003/XP, Linux, Solaris, and Tru64 UNIX

Effectively managing and troubleshooting eDirectory is important to understanding how eDirectory works and how it’s different from earlier NDS implementations.

# ### eDirectory Operation

Instead of the fixed-length record files used in previous NDS versions, eDirectory uses Flexible and Adaptive Information Manager (FLAIM), a highly scalable, indexed database developed to store information for the GroupWise e-mail system. The structure and purpose of files in the FLAIM database are shown in Figure 4-8.

+   - The NDS.db file acts as the control file for the database and contains the rollback log used to abort incomplete transactions.
+   - The 00000001.log file in the SYS\NetWare\NDS.rf! directory tracks completed transactions and the current transaction. By default, the 00000001.log file is installed in No Keep mode, which means transactions are eventually overwritten and no additional log files are created. The log file can be changed to Keep mode if additional backup is required. In Keep mode, additional log files named 00000002.log, 00000003.log, and so on are created when specified log file conditions, such as maximum size, are met.