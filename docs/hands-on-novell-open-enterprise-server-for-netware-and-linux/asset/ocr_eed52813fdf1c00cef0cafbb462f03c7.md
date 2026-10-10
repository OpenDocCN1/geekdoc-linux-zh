# Using the Network File System (NFS) Client

Although NFS support is installed and started as part of the NetWare 6.5 installation, accessing the NetWare file system from Linux requires a few more steps than Windows or Macintosh. An important component of the NFS file system is the NFS server, which makes directories on the local system available to the network. NFS running on the NetWare server can be stopped and started from the NetWare server console with the NFSTOP and NFSTART commands. Before a NetWare directory can be accessed from Linux clients, it needs to be exported to the NFS server software running on your NetWare 6.5 server. You can use iManager to export a NetWare volume to the NFS server by performing the following steps:

+   1. Start iManager and log in with a user name that has administrative rights.
+   2. Expand the File Protocols heading and click NFS.
+   3. Click the Export button to open the Export Options window.
+   4. In the Path text box, enter the path to be exported, using forward slashes to separate directory names. (For example, to export the shared directory in the IT structure, enter `/Data/IT/Shared`.)
+   5. In the Access Control text box, specify Independent or NetWare mode. Independent mode means that NetWare and NFS rights are managed separately. NetWare mode means that rights are managed from NetWare and mapped to NFS accordingly. You learn about NetWare file access rights in Chapter 6 and NFS permissions in Chapter 13.
+   6. Use the Global permissions field to specify what permissions will be granted to all trusted computers by default.
+   7. In the Trusted Host and Access Permissions table, specify the NFS host you want to make a trusted host for the exported path and the rights to be granted to the export host.

After a directory has been exported, it can be mounted on the Linux computer by following these steps from the Linux system:

+   1. Use the mkdir command to create a directory for storing the NetWare 6.5 NFS export.
+   2. Use the mount command to link the new directory to the NetWare 6.5 Open Enterprise Server export.
+   3. Access the NetWare exported directory from Linux with standard Linux commands (described in Chapter 13).

> In Chapter 13, you export and mount a NetWare directory on a Linux system.

# Web Browser Clients

Web browsers are clients that use the HTTP and WebDAV protocols to make requests to Web servers. Today many Internet applications are written to provide access to data and services from Web browsers. As you have learned, an important part of Novell’s OneNet strategy is to allow administrators and users to use their Web browsers as clients to manage the network and access file and print services. In addition to Remote Manager, you learn about a number of Web-enabled applications, including iManager, iFolder, NetStorage, and iPrint, that are included with NetWare 6.5. In the following section, you learn how to use iManager to enable Novell NFAP passwords. In Chapters 4 and 5, you use iManager to help set up and manage the eDirectory tree for your version of the UAS network. In Chapter 10, you learn how to configure iFolder so that users can access their files from any location by using Web browsers.