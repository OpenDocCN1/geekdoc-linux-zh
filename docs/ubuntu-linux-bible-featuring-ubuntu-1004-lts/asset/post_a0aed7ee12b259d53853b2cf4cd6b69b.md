
# Creating Permanent Desktop Icons for Services and Locations

The traditional way to connect to remote services in the graphical GNOME desktop environment used by Ubuntu Linux is to use the Nautilus File Manager. Using Nautilus to connect to FTP, SSH (Secure FTP), SMB/CIFS, and other servers creates a temporary icon for those that is automatically removed when you log out. You can also bookmark these servers, which is permanent but only visible from the Places menu or within Nautilus.

The easiest way to create a quick connection to a remote system from your Ubuntu system is to create a desktop shortcut to the remote location. You can create a Launcher for a remote location by right-clicking on the desktop, selecting Launcher from the context-sensitive menu, and selecting Location as the Type of that launcher. The dialog will now look like the one shown in Figure 26-1.

FIGURE 26-1

![](img/1a233c34336fbf5a85d6eb785e401709_966_0.png)

Enter some memorable text as the name of the location and identify the remote server by entering a URL of the form PROTOCOL://USER@HOST/SHARE/DIRECTORY. Replace PROTOCOL with ftp, smb, or ssh; replace USER with the name of the user that you want to connect as (you can leave out the USER@ portion of the URL if you are connecting to an anonymous FTP); and specify the hostname or IP address of the system you want to connect to. When connecting to a shared Windows directory, you must also specify the name of the SHARE that you want to connect to. Finally, you can specify a DIRECTORY path on the host or SHARE that you want to connect to, relative to the SHARE, directory, or anonymous FTP directory.

Click Save to save the new launcher. Double-clicking on the desktop icon for that launcher will display an authentication dialog for the remote service if authentication is required. Entering the correct password will now display the remote location in Nautilus. (SSH connections are displayed as Secure FTP connections).

If you're a fan of desktop icons for remote services, rather than selecting a menu item on Ubuntu systems, creating a desktop launcher/link is “the right thing to do” because these items persist after you log out and log back in again.

# Part II: Ubuntu for Desktop Users

# Using FTP

FTP in uppercase stands for "File Transfer Protocol," and is the oldest existing way of transferring files over a network, using the standard TCP/IP protocol that is the basis of the Internet. In lowercase letters, ftp is the name of a command-line program that you can run to connect to a remote FTP server so that you can transfer a file in either direction. If I'll explain in this section, Ubuntu makes it easy to transfer files using FTP in a variety of ways: The GNOME desktop provides built-in support for FTP connections, Ubuntu comes with the command-line FTP client, and the Ubuntu repositories provide stand-alone, graphical FTP applications if needed of the previous solutions meet your needs.

# Tip

If you need to access files from an FTP server and aren't interested in using a GNOME line FTP client approach, you can simply connect to the FTP server using your favorite Web browser. For example, if the files you're looking for are on an FTP server on a host named vhagen.org, you can try connecting to that host by specifying a URL of the form ftp://USERNAME@xen.vhagen.org., where USERNAME is the account that you want to connect to the FTP server. If the FTP server supports anonymous connections, you can connect anonymously using a URL of the form ftp://xen.vhagen.org.

FTP is an old protocol, and the commands that you need to know are simple, even from the line. You may not need to use FTP from the command line at all, because many equivalent command-line tools exist, such as wget and curl, which use newer protocols as HTTP to retrieve files by directly specifying their URLs. In general, I prefer to err on the side of caution in this book—if you don't need certain information, that's and you can skip over it. If you did to use FTP and information about it wasn't present in the book, both of us would be unhappy.

# Note

FTP is as old as TCP/IP networking. If you're wondering why I'm even bothering to talk about FTP, the reason is it may be the only mechanism that you can use to transfer relatively large files. Many mail servers enforce a size limit of 10 MB on attachments, a shared directory that contains the files that you need to download or upload and they aren't available for P2P download as a torrent, FTP is the tried-and-true solution that you'll probably need to use.

# Connecting to an FTP Server from the GNOME Desktop

Ubuntu's Places menu provides the Connect to Server command, which makes it easy to create an icon on your desktop for an FTP server, and then to connect to that share using the Nautilus File Manager. Selecting Places Connect to Server displays the dialog shown in Figure 26-2.

# Chapter 26: File Transfer and Sharing

![](img/1a233c34336fbf5a85d6eb785e401709_968_0.png)

The default selection, Public FTP, is not the one that you want to use if the FTP server that you want to connect to requires authentication (a specific username and password), which is usually the case. (I'll explain how to do later in this section.) As you might suspect, Public FTP servers are servers that do not require authentication and are traditionally known as anonymous FTP servers. If you are actually connecting to an anonymous FTP server, you must at least enter the name or IP address of the FTP server that you want to connect to. You need to specify a specific port only if the FTP server is running on a nonstandard TCP/IP port, and you need to specify the name of a remote directory only if you want to automatically connect to some directory other than the default one that the FTP server associates with the anonymous user. If you are, indeed, trying to connect to an anonymous FTP server, click Connect to create a desktop icon for FTP server and attempt to connect to it.

**Tip**: If you expect to connect to the same anonymous (or authenticated) FTP server multiple times, you can click the "Add bookmark" checkbox and enter the name of a bookmark that will be added to the Network section of your GNOME's Places menu after you successfully connect to the FTP server for the first time. ■

To specify you connect to an FTP server that requires authentication, click the Service menu at the top of this dialog and select the FTP (with login) entry to display the dialog shown in Figure 26-3.

As with an anonymous FTP server, you must at least enter the name or IP address of the FTP server that you want to connect to, but this is optional—if you do not specify one, you will be prompted for information when you actually connect. As with the Public server, you need to specify a specific port only if the FTP server is running on a nonstandard TCP/IP port, and you need to specify the name of a remote directory only if you want to automatically connect to some directory other than the default one that the FTP server associates with any user that you've specified. Click Connect to create a desktop icon for FTP server and attempt to connect to it.

# FIGURE 26-3

Defining a connection to an FTP server that requires authentication

![](img/1a233c34336fbf5a85d6eb785e401709_969_0.png)

When connecting to an authenticating FTP server, you will see a dialog that prompts for any required information that you have not yet, as shown in Figure 26-4. This figure shows the dialog in which you only specified the name of the FTP server that you want to connect to, and did not specify a user name.

# FIGURE 26-4

Completing the login information for an FTP server

![](img/1a233c34336fbf5a85d6eb785e401709_969_1.png)

If you are connecting to an FTP server that requires authentication and didn't specify the name of a user to connect as, the dialog shown in Figure 26-4 still gives you the opportunity to connect anonymously. However, to actually log, select the "Connect as user" radio button and enter the login name and password of the user that you want to connect as.

Once you enter the correct username and log in (or successfully connect to an anonymous FTP server), a Nautilus File Manager window appears, which displays the contents of the default directory with which you are logged in, as shown in Figure 26-5.

Once the Nautilus File Manager appears, you can copy files in either direction using the standard Nautilus and GNOME desktop conventions, as discussed in Chapter 5, "Using the GNOME Desktop."
