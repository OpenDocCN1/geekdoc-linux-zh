but you'll need to do more work to configure your FTP server. Such a configuration is beyond the scope of this book.

# File Sharing with NFS, Samba, and Netatalk

In contrast to FTP, many operating systems include so-called file sharing facilities. Functionally, these are quite similar to ftp, but the user interface on the client side is typically much more like that of the host OS's access to local disks. Figure 3.5, for instance, shows how MacOS gives access to both a local hard disk and one shared from a Linux computer via the Netatalk package. In addition to file transfers from one computer to another, file sharing usually allows programs on the client system to directly access files on the server (so you can use an OS/2 word processor to work on files stored on your Linux box, for instance). It's even possible to run programs on the client that are stored on the server, which can greatly reduce the total disk space requirements of an office.

![](bbox=[0.13, 0.5, 0.8, 0.88])

# FIGURE 3.5

Shared file systems look and act very much as if they were local. In the case of MacOS, you can tell them apart from local drives by their icons on the desktop and in window title bars.