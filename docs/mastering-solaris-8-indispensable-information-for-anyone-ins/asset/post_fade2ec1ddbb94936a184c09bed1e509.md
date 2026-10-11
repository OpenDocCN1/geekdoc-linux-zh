
3. Decompress the archive and extract with the following commands (in the last line, <file_name> will no longer have the “gz” attached to it):
   - $ cd /var/tmp
   - $ umask 0
   - $ gunzip <file_name>
   - $ tar -xvf <file_name>

# Netscape Bookmarks

The bookmark feature enables you to save the names and URLs of Web pages that are of special interest to you. This feature saves you the task of trying to remember the long complicated URLs. There are several ways you can use the bookmark feature:

- To create a bookmark, click the Bookmarks button on the Location toolbar. A list of bookmarks is displayed; the first three items on the list are Bookmark menu options, as shown in Figure 14.3.
- Click a bookmark to go to the site it points to.
- Select Add Bookmark to add the URL you are currently viewing as a bookmark.
- Choose File Bookmark to file it in a folder.
- Choose Edit Bookmarks to change the properties of bookmarks or move or delete them.
- You can also choose Bookmarks from the Communicator menu on the menu bar to browse through the list of bookmarks.

The first component in the URL points to the type of resource the page contains, such as HTTP, FTP, or Gopher. The http, colon, and double slash that follow act as identifiers to the Web, but they may be omitted from a URL in print. You usually do not have to enter them to get to the site the URL points to; they are implied. The full name of the host acting as the server for the information follows this. The rest of the URL is a relative path name to the file that contains information you are looking for.

# Customizing Netscape

Netscape has a set of preferences that you can use to customize the program’s behavior. To open these preferences, select the Preferences command from the Edit menu.

Figure 14.4 shows the Navigator section of the Preferences dialog box. You can choose the home page, which is the page that appears when you first open Netscape, by choosing the Home Page radio button under the Browser Starts With area and entering the URL into the Location text box under Home Page.

**FIGURE 14.4**
The Navigator section of the Netscape Preferences dialog box

![](img/256e02a6afce528d264a8d911fa0ff20_599_0.png)

There are two additional pages that you will want to visit. The first is the Netscape Advanced Cache Preference page, on which you can set the size and behavior of the cache. The second important page is the Advanced Proxies page, shown in Figure 14.5. On that page, you can configure how Navigator connects to the Internet: directly, through a proxy server, or using a configuration script. Click the View button to manually set different protocols and their servers and ports, as shown in Figure 14.6, but only if recommended by the system’s administrator. Incorrect settings will cause the browser to stop working. It will load but you won’t be able to view any Web pages.

# Electronic Mail

Electronic mail (or e-mail, as it is commonly known) is probably the most popular feature of the Internet. It’s quick and you can use it to send invitations, memos, letters, pictures, and so on, and you never need a stamp! One advantage of e-mail is that you can attach other documents to it, like a resume, for example. Attachments are opened by programs or browsers that are called by your mail program.

E-mail can be used to communicate with users on a local system, with users on a wide area network system, and with other users on the Internet. On a LAN or WAN, you can send messages to users who are logged on and are willing to receive them. E-mail utilities, however, allow you to send messages to parties not logged on as well as those who are. You can also send a message to several parties at one time. You can reply to an incoming message instantaneously. You can also delete messages you do not want to read.

Solaris has several utilities for receiving and sending e-mail. The dmain1, mailtool, mail, and mail1x utilities are some of the many mail programs available for Solaris 8 users in addition to Netscape, pine, emacs, and xmh (xmh is a graphical interface to the MH Message Handling System).

![](img/256e02a6afce528d264a8d911fa0ff20_600_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_601_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_601_1.png)

In many ways, the dtnail and mailtool1 programs are similar. They are both graphical interfaces to mail programs. Although either program can be run from the Common Desktop Environment (CDE) or OpenWindows, each program runs better on the window manager it was designed for. If either program is represented by an icon, the icon will indicate whether or not you have mail waiting to be read (the program does not have to be open). The mailtool1 program icon will show you if you have new mail or mail that has already been read. Both programs open with a list of messages; new messages are marked, and you can read, reply to, and dispose of messages as you choose. The difference is that dtnail uses an N for new mail and mailtool1 uses a U for unread mail. Each program then allows you to sort messages and store them in folders for easy retrieval. You can compose and send new messages to users on your system or on any system on the network you are connected to.

### Using pine for Electronic Mail

There is a Unix mailer called pine (Program for Internet News & Email) that, at its inception, was particularly easy for beginners to learn. This mail utility is user friendly and has capabilities that attract many users. It now has advanced capabilities for accessing Internet newsgroups, as well as a mechanism for transmitting files containing any kind of data. There are ways to customize pine according to individual preferences. Sun does not supply *pine*, but it can be obtained by contacting ftp://ftp.cac.washington.edu/pine or www.cac.washington.edu/pine. As you will note from the URLs, it was designed by the University of Washington for Unix.

Again, you should experiment with the various features until you feel comfortable with them. There is help text available for every screen. To get started, type in the following command:

```
$ pine
```

You will see a *pine* main menu screen that has seven commands in the middle. Each command is represented by a letter on the left.

At the top of the screen is a status line with the version of *pine* you are using and the name of the active screen. The bottom two lines give all the commands for the main menu, each highlighted with a single character that is displayed to the left of the command name. Because there are so many commands, you must enter 0 (other) to view another two-line display. These two two-line displays comprise the full set of commands for the Main menu; another 0 command takes you back to the original two-line display.

To execute a *pine* command, you can do either of the following:

- Press the key that corresponds to the character to the left of the command you want to execute.
- Use the arrow keys for Next and Previous to position the cursor over the command you want and then press the Return key.

The main menu has additional commands that don't fit in the display at the bottom of the screen. With the 0 command, you can view other commands. There is also help text available. You can use the *M* command to get back to the main menu and the *Q* command to quit *pine*. Experimentation is the key to learning *pine* or any mail system.

If you want to send mail from *pine*, try sending it to yourself first by following these steps:

1. Type *pine* in a terminal window to bring up main menu.
2. Choose the command Compose Message (Figure 14.7 shows the *pine* Compose Message window).

![](img/256e02a6afce528d264a8d911fa0ff20_603_0.png)

3. In the To field, type in your own login name and then type your message. Use the Ctrl key to type in commands (the display commands at the bottom of the screen). You can use Enter or the arrow keys to move down through the fields.
4. Use the Cc portion of the header to send copies. (To find other users’ addresses, press Ctrl+G.)
5. Press Ctrl+X to transmit the message. You will be asked if you are ready to send it. Answer with a yes or a no.
6. Press the Q key to return to the shell.

The first time you use pine, it will create a link to the user’s mail spool called INBOX. Folders called sent-mail and saved-messages are created and are put in the $(HOME)/mail folder by default. The INBOX will link to your unread messages, and the sent-mail folder will hold copies of mail already sent out. The saved-messages folder will hold messages that you want to save. You can create more folders in pine; you can also delete messages or transfer them from one folder to another. You can organize folders into collections of topics as you prefer. When you receive a message, you will see codes listed on the left. A code + means that the message was sent directly
