On a remote DHCP server, enter the following:

`# Display=localhost; export display`

`# /usr/sbin/dhcpmgr &`

+   2. Make your changes in the DHCP Manager window.
+   3. Select the Exit command from the File menu.

Here are the four DHCP command-line utilities (each of these four commands is documented in the man pages):

in.dhcpd This command lets you control the DHCP daemon.

dhcpconfig This is a shell script that lets you configure the DHCP server using commands presented in a text-based menu system.

dhtadm This command allows you to change the configuration options and macros for DHCP clients.

pntadm This command allows you to modify DHCP network tables.

The Solaris DHCP client is the system that accepts the IP address from the server. On Solaris, it is a software program run as a daemon (dhcpagent). Solaris automatically installs the DHCP client as part of the installation of the operating system. You do not need to enable this client because it is already enabled.

# ## The Network File System

The Network File System (NFS) allows you to work locally with files that are stored on a remote computer disk but appear as if they are present on you own computer. The remote system acts as a file server, and the local system acts as the client and queries the file server.

**NOTE File** systems were covered extensively in Chapter 5. You may want to refer back to that chapter for a more detailed discussion of NFS.

The system administrator configures the NFS just as they do the NIS. If you are working with a file, you will probably not be aware of where the file is physically stored. This is another perfect example of distributed computing. Because most central file servers are equipped with large-capacity disk drives and devices that make backup copies of data, some Solaris systems may be diskless. A floppy disk can be used to start Solaris and load the system software from another machine on the network. Solaris also produces a dataless system that stores only the system software and the operating system, and the applications are kept on the disk.