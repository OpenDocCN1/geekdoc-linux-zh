# **362 Using Graphical FTP Clients**

For uploading files, you may want to use gFTP because you typically have to provide a username and password for such transfers. Web browsers work fine for anonymous downloads, which is how you typically download software from the Internet.

I briefly describe all three GUI FTP clients in the next two sections.

# Using gFTP

GNOME comes with gFTP, a graphical FTP client. gFTP is not installed by default, but you can download it from [http://gftp.seul.org](http://gftp.seul.org) and install it easily. In some distributions, it may be in a package already, and all you have to do is install that package.

![](bbox=[0.15, 0.4, 0.25, 0.55])

In Debian, type `su -` in a terminal window and enter the root password, then type `apt-get install gftp`.

![](bbox=[0.15, 0.46, 0.25, 0.55])

In Fedora Core, install gFTP from this book’s companion DVD. Log in as *root*, insert the DVD into the DVD drive, and type `mount /mnt/cdrom` in a terminal window. (You may have to change `cdrom` to `cdrom1`, if the DVD drive is the second CD/DVD drive on your system.) Then type `cd /mnt/cdrom/Fedora/RPMS`, followed by `rpm -ihv gftp` *.

In Fedora Core, start gFTP by choosing Main Menu\Internet\gFTP (if you don’t see gFTP, log in as *root* and type `yum install gftp` and then look for it in the menu). In other distributions, you should be able to find it in the Main Menu. The gFTP window appears, as shown in Figure 4-1.

![](bbox=[0.25, 0.65, 0.75, 0.83])

+   **Figure 4-1:**  
+   The gFTP window just after opening a connection to an FTP server.

![](bbox=[0.25, 0.84, 0.75, 0.96])