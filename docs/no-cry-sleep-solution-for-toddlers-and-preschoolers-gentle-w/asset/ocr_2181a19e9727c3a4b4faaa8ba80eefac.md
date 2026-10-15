# CHAPTER
NFS and NIS

Linux provides several tools for accessing files on remote systems connected to a network. The Network File System (NFS) enables you to connect to and directly access resources such as files or devices like CD-ROMs that reside on another machine. The Network Information Service (NIS) maintains configuration files for all systems on a network. With Samba, you can connect your Windows clients on a Microsoft Windows network to services such as shared files, systems, and printers controlled by the Linux Samba server (see Chapter 37).

# Network File Systems: NFS and /etc/exports

NFS enables you to mount a file system on a remote computer as if it were local to your own system. You can then directly access any of the files on that remote file system. This has the advantage of allowing different systems on a network to access the same files directly, without each having to keep its own copy. Only one copy would be on a remote file system, which each computer could then access. You can find out more about NFS at its Web site at nfs.sourceforge.net.

> NOTE Mac OS X for Macintosh computers, which is based on BSD Unix, now supports NFS for file sharing. To access Apple file systems and printers using older Apple operating systems, you can use Netatalk. Netatalk implements the classic AppleTalk and AppleShare IP network protocol on Unix and Linux systems. The current Netatalk Web site is netatalk.sourceforge.net, with links to the FAQ and the HOW-TO sections.

# NFS Daemons

NFS operates over a TCP/IP network. The remote computer that holds the file system makes it available to other computers on the network. It does so by exporting the file system, which entails making entries in an NFS configuration file called /etc/exports, as well as by running several daemons to support access by other systems. These include rpc.mountd, rpc.nfsd, and