# 384 Using Graphical FTP Clients

For uploading files, you want to use gFTP because you typically have to provide a username and password for such transfers. Web browsers work fine for anonymous downloads, which is how you typically download software from the Internet.

I briefly describe both GUI clients in the next two sections.

# Using gFTP

GNOME comes with gFTP, a graphical FTP client. gFTP is not installed by default, but you can easily install it from the companion DVD by following these steps while you are logged in root:

+   1. Mount this book's companion DVD.

Insert the DVD into the DVD drive and type mount /mnt/cdrom in a terminal window (you may have to change cdrom to cdrom1, if the drive is the CD/DVD drive on your system).

+   2. Install the gFTP RPM.

Type the following commands from a terminal window (these commands assume that the DVD is mounted on /mnt/cdrom):

```
cd /mnt/cdrom/RPMS
rm -ivh gftp*
```

To start gFTP, choose from the GNOME or KDE desktop Menu Internet->gFTP. The gFTP window appears (as shown in Figure 4-1).

> Figure 4-1: The gFTP window just before opening a connection to a remote FTP server.

![](bbox=[0.262, 0.597, 0.693, 0.893])