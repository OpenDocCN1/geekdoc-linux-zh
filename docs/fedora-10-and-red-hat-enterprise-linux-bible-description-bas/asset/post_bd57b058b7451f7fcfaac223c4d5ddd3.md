
# Chapter 9: Using the Internet and the Web 395

system. If your current local directory were /home/jake, ftp would try to copy the file to /home/jake/tmp/sting.

- put-file — Copies a file from the current local directory to the remote directory. The usage of this command is essentially the same as the get command, except that files are copied from the remote system.

> NOTE: Anonymous FTP sites (described) usually let you copy files from them, but not to them. If they do not allow you to put files on their servers, it will usually be in a restricted area.

- mget-file… This command lets you download multiple files at once. You can specify multiple files individually or by using metacharacters (such as the asterisk). If you run the prompt command (see below), FTP prompts you for each file to make sure you want to copy it.

- mput-file… This command lets you put multiple files on the remote computer. Like mget, mput can prompt you before transferring each file.

Another useful ftp command is the prompt command. After prompt is, mget and mput commands will offer a prompt to ask if you want to download each file in the list requested as it is ready to download.

# FTP exiting commands

While a connection is open to a remote computer from an FTP client in Fedora, you can use several commands to temporarily or permanently exit from that connection. Here are some useful commands:

- ! This command temporarily exits you to the local shell. After you have done what you need to do, type exit to return to your FTP session. You can also use this command to run other commands. For example, you can type pwd to see the current directory is on the local system, uname -a to remind yourself of your local system name, or ls - to see the contents of your current directory.

- close Closes the connection.

- bye Closes the connection and exits the ftp command. You can also use quit or by.

# Using the nctftp command

By virtue of being an FTP program, nctftp command supports all the standard commands you would expect to find in an FTP client (get, put, ls, cd, and so on). However, nctftp has added features that make it more efficient and friendlier than some other FTP clients.

> NOTE: You can install the nctftp package by typing yum install nctftp.

# Part II: Using Fedora RHEL

nctftp, you can connect to an FTP server in the same way you did with ftp. One convenience is that if you enter no user name, nctftp assumes you want to use the anonymous user name and logs you in. Here is an example:

```
$ nctftp ftp.mozilla.org
nctftp 3.2.2 (Aug 18, 2008) by Mike Gleason
(http://www.nctftp.com/contact/)
Connecting to ftp.mozilla.org...
(vsFTP 2.0.9)
Logging in...
Login successful.
Logged in to ftp.mozilla.org.
nctftp / ~
```

To log in as a user other than anonymous, a -u user option, where user is replaced by the name you want to log in. Enter the password as prompted to continue.

# Using nctftp

After you are logged in with the nctftp session running, there are a few features you can use that are not available with other FTP clients. Here are some examples:

- bookmark — If you are visiting a site that you want to return to, type the bookmark command and a name to identify that site. The next time you start nctftp session, type the bookmark name as an option. You are only logged into the FTP site you bookmarked; you are taken to the directory where you set the bookmark.

- ls, lmkdir, lpwd — There is a series of commands that enable you to move around the local file system. Place a letter l in front of standard shell commands such as ls, cd, mkdir, pwd, rm, and rdir and you can move around and work with your local file system while you are in nctftp.

- help — Use rhelp to see commands that are recognized by the FTP server. To see commands that are specific to the FTP server, type help while you are in an nctftp session.

- Auto-resume — If you were disconnected in the middle of a large download, you will appreciate this feature. After a connection is broken during a download, reconnect to the FTP site and begin downloading the file in the same local directory. The nctftp command resumes where it left off.

- Tab completion — Press the Tab key to have nctftp complete file names and paths.

Using nctftp for background transfers

If you are moving around different parts of the FTP site, or jumping between different sites, you might not want to wait for a file transfer to complete before you go somewhere else. The nctftp command has an excellent feature for placing transfers in a spool file and then running them in the background immediately or later.

# Chapter 9: Using the Internet and the Web 397

To select a file for background transfer, use the bgget command. Here is an example:

```
ncftp /pub > bgget_wireless.doc
Spooled: get wireless.doc
ncftp /pub > jobs
---Scheduled-For---Host---------Command-----------------------
2008-06-01  18:38 maple      GET wireless.doc
ncftp /pub > bgstart
Background process started.
Watch the "/home/./ncftp/log" file to see how it progressing
```

In this example, the bgget command pools the wireless.doc file from the remote directory (/pub) and sets it to the local directory. Typing the command that shows the job (GET wireless.doc), from the host name, is scheduled to run immediately (6:38 p.m., June 1, 2008). By running the bgget command, this process, and any other pooled jobs, are run immediately.

Instead of starting background transfers immediately you can do them later. For background jobs spooled for transfer, the transfer begins when you quit ncftp, leave your current site, or go to another FTP site. In this way, the program that does catch your current login session to the transfer.

If you want to wait longer to do the transfers, you can pass an option to the bgget command to start the transfer at a particular time. Here is an example:

```
ncftp /pub > bgget -e 2008-10-04 10:00 wireless.doc
```

With this command, the transfer is set to run at October 4 to transfer the file called wireless.doc. Again, you can check .ncftp/log file in your home directory to see if the transfer completed. The transfer is completed by background process.

# Using the gFTP window

If you prefer a more graphical interface for accessing FTP servers, you can use gFTP window. Install gFTP by typing yum gftp. You can open gFTP window by typing gftp. Figure 9-9 shows an example of gFTP window.

Unlike the ftp command, gFTP window lets you see the contents of the remote and local directories. To transfer a file from one site to the other, simply double-click it or drag drop it to the other pane. (Normally, you will just be copying files from FTP sites, unless a site provides you with permission to write to it.)

# Using Fedora RHEL 398

![](img/63c8e1d25a0e2be7e9f6de6f02530)

Figure 9-9: View local and remote files simultaneously with gFTP.

Follow this procedure to connect to an FTP site:

1. Type the name of the FTP server where you want to connect (for example, ftp.duke.edu) into the Host box.
2. Type the port number on the FTP server (you can leave this blank to use the default port 21).
3. Type the user name used to log in to the FTP server. Use the default anonymous if you do not have a specific user name and the server is publicly accessible.
4. Type the password for the user name you entered. The convention with anonymous servers is to use your e-mail address as the password.
5. Click the icon displaying two monitors to connect to the FTP site.
6. If you entered the information correctly, the bottom pane on the window should show that the transfer was complete and the right pane should show the current directory of the FTP site. Here are some actions you can take once you are connected:

# Chapter 9: Using the Internet and the Web 399

- Move around — Double-click a directory to move to that directory or double-click on the two dots ( ) to move up a level. You can do this on both the remote and local directories.

- Drag and drop files — You can drag and drop files from the FTP site to the left pane (representing your current directory).

- Save this site — If you want to return to this site later, choose Bookmarks → Add Bookmark. A pop-up window lets you name this site for the bookmarks list. After, you can select it from the list at a later date to connect to the site. gFTP window will have stored only the name, but port, user name, and password. You are just one click away from connecting. This is one of the best features of graphical FTP programs as gFTP.

A nice feature of gFTP is that it stores log information. Logging View Log. A window appears showing the conversations that have taken place between your computer and each FTP site. You can look at these messages to see what you are unable to connect to a site or remember where you have been and what you have done on an FTP site.

> NOTE: The Bookmarks list comes with several entries under the Red Hat Sites menu that let you connect directly to FTP sites that have software packages as RPMs. While these sites were useful at one time, it is better to use yum or PackageKit to get software packages. Many of the sites in Bookmarks list contain out-of-date RPMs and won't automatically take care of dependency issues.

# Getting files with wget

If you already know where a file is on the network, there are more efficient ways of downloading that file than opening an FTP session, moving around the FTP server, and running the get command. The wget command is a simple, efficient tool for doing interactive downloads of files over the Internet.

> NOTE: Another great command for copying files over the network is the rsync command. I often use rsync to do backups over the network. See Chapter 13 for descriptions on using rsync to do backups.

If there is a file you want to download from an FTP site or Web server (HTTP), and you know exactly where the file is, wget is a good way to download. The wget command is very useful if you want to copy a whole site, recursively, from one computer to another (for example, containing user directories). When downloading from FTP sites, wget can let you just download as the anonymous user or add your user name and password to the command line.

# Downloading a single file

Here is an example of wget to get a file from a Web server:
