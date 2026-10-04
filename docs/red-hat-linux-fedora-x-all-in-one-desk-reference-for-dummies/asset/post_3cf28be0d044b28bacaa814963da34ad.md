
# 384 Using Graphical FTP Clients

For uploading files, you want to use gFTP because you typically have to provide a username and password for such transfers. Web browsers work fine for anonymous downloads, which is how you typically download software from the Internet.

I briefly describe both GUI clients in the next two sections.

# Using gFTP

GNOME comes with gFTP, a graphical FTP client. gFTP is not installed by default, but you can easily install it from the companion DVD by following these steps while you are logged in root:

- 1. Mount this book's companion DVD.

Insert the DVD into the DVD drive and type mount /mnt/cdrom in a terminal window (you may have to change cdrom to cdrom1, if the drive is the CD/DVD drive on your system).

- 2. Install the gFTP RPM.

Type the following commands from a terminal window (these commands assume that the DVD is mounted on /mnt/cdrom):

```
cd /mnt/cdrom/RPMS
rm -ivh gftp*
```

To start gFTP, choose from the GNOME or KDE desktop Menu Internet->gFTP. The gFTP window appears (as shown in Figure 4-1).

> Figure 4-1: The gFTP window just before opening a connection to a remote FTP server.

![](img/d9230b719dc0efd80851f363d8c6f571_410_0.png)

# Using Graphical FTP Clients 385

The gFTPC has a menu bar with menus for performing various tasks. Just below the menu bar is a toolbar with a number of buttons and text fields. Here you can type the name or IP address of the remote host, the username, and the password needed to log in to the remote host. Figure 4-1 shows the gFTPC window after you fill in this information.

To upload or download files using gFTPC, follow these steps:

- 1. Fill in the host name or the IP address of the remote system in the Host field.

If you have used that host before, you can select it from the drop-down list that appears when you click the downward-pointing arrow next to the Host field.

- 2. Provide the username in the User field and the password in the Pass field, and then click the button with the icon showing two computers (to the left of the Host field).

This operation causes gFTPC to connect to your host and log in with the username and password you provided. The lower part of the gFTPC window shows the FTP protocol messages exchanged between the two systems.

- 3. Observe any indication of error messages.

The directory listing of the remote system appears in the right half of the gFTPC window. The left half shows the current local directory.

- 4. To upload one or more files from the current system to the remote system, select the files in the left, and then click the right arrow button.

- 5. To download files from the remote system, select the filenames on the list, and then click the left arrow button.

- 6. When you are transferring files, choose FTPC: Quit from the menu.

As these steps, transferring files with a GUI FTP client, such as gFTPC, is a simple task.

Believe it or not, gFTPC isn't for FTP transfers. It can also transfer files using the HTTP protocol and secure file transfers using the Secure Shell (SSH) protocol.

![](img/d9230b719dc0efd80851f363d8c6f571_411_0.png)

# Using a Web browser as an FTP client

Any Web browser can act as an FTP client, but such programs are best for anonymous FTP downloads, where the Web browser can log in using the anonymous username and any password.

# Using Graphical FTP Clients

In Fedora Core, you can use the Mozilla Web browser as an FTP client. All you have to know is how to write the URL so the Web browser can tell that you want to download a file using FTP. The syntax of the FTP URL is like this:

```
ftp://hostname/pathname
```

The first part (ftp://) indicates that you want an FTP transfer. The hostname is part of the FTP server (the name often starts with an ftp — for example, ftp.netscape.com). The pathname is the full directory path and filename of you want to download.

If you provide the hostname for the FTP server, the Mozilla browser displays the contents of the anonymous FTP directory. If you want to find an anonymous FTP on your Fedora Core system, start Mozilla (click the Mozilla icon on the GNOME panel) and then type the following line in the Location box:

```
ftp://localhost
```

Then press Enter. Mozilla shows the contents of the anonymous FTP directory on your Fedora Core system. Figure 4-2 shows a typical appearance of an anonymous FTP directory in Mozilla. You can click folders to see their contents and download any files.

| Index of anonymous/ |
| --- |
| File Edit View Go Bookmarks Favorites Window Help |
| Back Forward Refresh ftp://localhost/ Search Print |
| Home Bookmarks Read Me In Network Support Shop Products Training |
| Index of ftp://localhost/ |
| To higher level Directory |
| 01/12/2004 06:00:00 |

Figure 4-2:
You can use Mozilla to download files from anonymous FTP servers.

![](img/d9230b719dc0efd80851f363d8c6f571_412_0.png)

When you use the ftp://localhost URL, you won't get a response from your system if you're not running an FTP server or if you have set your firewall so that no FTP connections are allowed. On your system, log in as root and type vsftpd start (in a terminal window) to start the FTP server.

# Using the Command-Line FTP Client 387

The same approach of accessing anonymous FTP sites works if you type the hostname of some other anonymous FTP server. For example, typing the following URL:

```
ftp://ftp.netscape.com
```

You get the directory of the ftp.netscape.com server.

# Using the Command-Line FTP Client

Knowing how to use FTP from the command line is a good idea — just in case. For example, your GUI desktop may not be working and to fix the problem, you may have to download some files. If you know how to use the command-line FTP client, you can download the files and take care of the problem. It's not hard.

The best way to learn the command-line FTP client is to try it out. The command is called ftp, and you can try out the ftp commands from Fedora Core system. You don't even need any Internet connection because you can use the ftp to connect to your system — I show you.

In the sample FTP session, use the command-line FTP client to log in using your username (n) and browse the directories on your system. When you try a similar operation, replace the name with your username and provide your password. Here is the listing showing the commands (commands appear in italics):

```
ftp localhost
Connected to localhost (127.0.0.1).
Name (localhost:naba): (I press Enter).
331 Specify the password.
Password: (I type my password).
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp help (I help to see a list of FTP commands).
Commands may be abbreviated. Commands are:
```

```
debug mdir sendport site
$ dir mget put size
disconnect mkdir pwd status
account mls struct
append exit quit struct
ascii form quote system
bell get mode unique
modtime recv unique
```

# 388 Using the Command-Line Client

```
binary mput
ascii mget
type get
cd /var/ftp (This changes to /var/ftp).
ls
 directory listing
250 Directory successfully changed.
mget filename (I get a specific file).
222 Entering Passive Mode
150 Here the directory listing.
226 Directory sent OK.
bye (This command ends the session).
221 Goodbye.
```

Table 4-1 describes some commonly used FTP commands. You don't have to type the entire FTP command. For a long command, you have to type the first few characters—enough to identify the command uniquely. For example, to delete a file, you can use delete and to change the file transfer to binary, you can type bin.

When downloading files from the Internet, you always want to transfer the files in binary mode because the software is usually archived and compressed in a binary form (files aren't plain text files). So always use the binary command to set the mode to binary. Then use the get command to download the files.
