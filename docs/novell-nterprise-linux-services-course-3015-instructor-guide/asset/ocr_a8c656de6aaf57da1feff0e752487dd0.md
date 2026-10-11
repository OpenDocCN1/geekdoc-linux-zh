If you are placing the iFolder server behind a firewall, you need to remember that iFolder uses both 80 and 443 for both client and server access. The administration page and the iFolder client authentication will be over 443.

# iFolder Architecture

To understand how the iFolder components and architecture work to synchronize and provide access to personal files, you need to know the following:

+   ■ Web Servers and iFolder
+   ■ LDAP and iFolder
+   ■ Authentication and Synchronization
+   ■ How iFolder Synchronizes Files

# Web Servers and iFolder

The iFolder server software uses Apache as its default Web server for NetWare and Linux server operating systems. On Windows 2000, iFolder uses the IIS Web server.

When iFolder is active on NetWare servers with Apache-based solutions, it can run in the operating system space or in protected memory space.

Because iFolder requires some configuration changes to Apache-specific files, we recommend that you install iFolder on a server that does not have other applications that rely on Apache.

If you do have other applications that use Apache, these applications might not work when you install iFolder.