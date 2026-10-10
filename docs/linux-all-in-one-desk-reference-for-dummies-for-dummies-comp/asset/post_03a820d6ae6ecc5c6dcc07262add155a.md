
## When Akregator First Runs

When Akregator first runs, it displays its main window without any RSS feeds. To subscribe to a feed, choose Feed▸Add Feed from the menu or right-click All Feeds in the left pane of the window (see Figure 3-8) and select Add Feed from the pop-up menu. Then type the URL for the feed in the Add Feed dialog box and click OK. For example, to read Slashdot's RSS feed, I type http://slashdot.org/index.rss. The feed's title appears in the left pane of the window. Click the feed title to view the items in this feed. Then you can click an item in the upper-right pane, and that item appears in the lower-right pane, as shown in Figure 3-8. You can add many different RSS feeds, organize them into folders, and browse them in Akregator.

![](img/11709a8f88c8cd03868a929dc94c0e2b_385_0.png)

## Chapter 4: Using FTP

### In This Chapter

- Using the GNOME FTP client
- Using any Web browser as an FTP client
- Getting to know the FTP commands

Just as the name implies, *File Transfer Protocol* (FTP) is used to transfer files between computers. For example, if your Internet Service Provider (ISP) gives you space for a personal Web site, you may have already used FTP to upload the files making up the Web site. Using an FTP client on your computer, you log in to your ISP account, provide your password, and then copy the files from your home system to the ISP’s server.

You can also use FTP to download other files anonymously, such as open source software from other computers on the Internet — in which case, you don’t need an account on the remote system to download files. You can simply log in using the word *anonymous* as the username and provide your e-mail address as the password. (In fact, your Web browser can do this on your behalf, so you may not even know this process is happening.) This type of anonymous FTP is great for distributing files to anyone who wants them. For example, a hardware vendor might use anonymous FTP to provide updated device drivers to anyone who needs them.

Linux comes with several FTP clients, both command-line ones and GUI ones. In this chapter, I introduce you to a few GUI FTP clients and for the command-line FTP client, describe the commands you use to work with remote directories.

### Using Graphical FTP Clients

You can use one of the following GUI FTP clients in Linux:

- gFTP — a graphical FTP client for GNOME (http://gftp.seul.org)
- KBear — a graphical FTP client for KDE (http://kbear.sourceforge.net)
- Web browser, such as Firefox, for anonymous FTP downloads

For uploading files, you may want to use gFTP because you typically have to provide a username and password for such transfers. Web browsers work fine for anonymous downloads, which is how you typically download software from the Internet.

I briefly describe all three GUI FTP clients in the next two sections.

### Using gFTP

GNOME comes with gFTP, a graphical FTP client. gFTP is not installed by default, but you can download it from [http://gftp.seul.org](http://gftp.seul.org) and install it easily. In some distributions, it may be in a package already, and all you have to do is install that package.

![](img/11709a8f88c8cd03868a929dc94c0e2b_387_0.png)

In Debian, type `su -` in a terminal window and enter the root password, then type `apt-get install gftp`.

![](img/11709a8f88c8cd03868a929dc94c0e2b_387_1.png)

In Fedora Core, install gFTP from this book’s companion DVD. Log in as *root*, insert the DVD into the DVD drive, and type `mount /mnt/cdrom` in a terminal window. (You may have to change `cdrom` to `cdrom1`, if the DVD drive is the second CD/DVD drive on your system.) Then type `cd /mnt/cdrom/Fedora/RPMS`, followed by `rpm -ihv gftp`.

In Fedora Core, start gFTP by choosing Main Menu\Internet\gFTP (if you don’t see gFTP, log in as *root* and type `yum install gftp` and then look for it in the menu). In other distributions, you should be able to find it in the Main Menu. The gFTP window appears, as shown in Figure 4-1.

![](img/11709a8f88c8cd03868a929dc94c0e2b_387_2.png)

**Figure 4-1:** The gFTP window just after opening a connection to an FTP server.

![](img/11709a8f88c8cd03868a929dc94c0e2b_387_3.png)

The gFTP window has a menu bar with menus for performing various tasks. Just below the menu bar is a toolbar with a number of buttons and text fields. Here you can type the name or IP address of the remote host, the username, and the password needed to log in to the remote host. Figure 4-1 shows the gFTP window after you fill in this information and establish a connection with the remote host by clicking the button with the icon showing two computers (the leftmost one on the toolbar).

To upload or download files using gFTP, follow these steps:

1. **Fill in the hostname or the IP address of the remote system in the Host field.**
   If you have used that host before, you can select it from the drop-down list that appears when you click the downward-pointing arrow next to the Host field.
2. **Provide the username in the User field and the password in the Pass field and click the button with the icon showing two computers (to the left of the Host field).**
   This operation causes gFTP to connect to your chosen host and to log in with the username and password you provided. The lower part of the gFTP window shows the FTP protocol messages exchanged between the two systems.
3. **Observe this area for any indication of error messages.**
   The directory listing of the remote system appears in the right half of the gFTP window. The left half shows the current local directory.
4. **To upload one or more files from the current system to the remote system, select the files in the list on the left, and then click the right-arrow button.**
5. **To download files from the remote system, select the filenames in the list on the right, and click the left-arrow button.**
6. **When you’re done transferring files, choose FTP:: Quit from the menu.**

As these steps show, transferring files with a GUI FTP client, such as gFTP, is a simple task.

> Believe it or not, gFTP isn’t for FTP transfers alone. It can also transfer files using the HTTP protocol and secure file transfers using the Secure Shell (SSH) protocol.

### Introducing KBear

KBear is a GUI FTP client for KDE. You find it in the Main Menu (in the Internet category) on KDE desktops. In Debian, type `apt-get install kbear` to install KBear (after you type `su -` to become `root`).

When you first start KDE, it runs the KBear Wizard that enables you to configure KBear. This configuration step mostly involves the layout of the KBear window, so you can just accept the defaults.

When the main KBear window appears, it displays your home folder in a view similar to that in Windows Explorer. To connect to a FTP server, choose FTP Quick Connect. A dialog box (see Figure 4-2) prompts you for the hostname of the FTP server as well as the username and password.

![](img/11709a8f88c8cd03868a929dc94c0e2b_389_0.png)

After entering the requested information, click Connect. KBear establishes a connection to the remote FTP server. In the KBear main window, shown in Figure 4-3, you see both the local and remote directories side by side.

You can now transfer files by dragging them from one system's folder and dropping them on the other system's folder, so FTP transfers become just normal drag-and-drop file copying.

When you finish using KBear, choose FTP Quit or click the Power Off button (the leftmost one) on the toolbar.

### Using a Web Browser as an FTP Client

Any Web browser can act as an FTP client, but such programs are best for anonymous FTP downloads, where the Web browser can log in using the anonymous username and any password.

![](img/11709a8f88c8cd03868a929dc94c0e2b_390_0.png)

For example, you can use the Firefox Web browser as an FTP client. All you have to know is how to write the URL so that the Web browser can tell that you want to download a file using FTP. The syntax of the FTP URL is like this:

```
ftp://hostname/pathname
```

The first part (`ftp://`) indicates that you want an FTP transfer. The hostname part is the name of the FTP server (the name often starts with an ftp — for example, ftp.netscape.com). The pathname is the full directory path and filename of the file that you want to download.

If you simply provide the hostname for the FTP server, the Web browser displays the contents of the anonymous FTP directory. If you want to access anonymous FTP on your Linux system, start Firefox (click the Web browser icon on the GNOME panel), type the FTP URL in the Location text box, and press Enter. For example, on my system, I type ftp://localhost/pub/ to access the pub directory.

Figure 4-4 shows a typical appearance of an anonymous FTP directory in Firefox. You can click folders to see their contents and download any files. Although I show how you can access your local system by using Firefox’s FTP capabilities, the purpose of FTP is (of course) to download files from other systems to your system.
