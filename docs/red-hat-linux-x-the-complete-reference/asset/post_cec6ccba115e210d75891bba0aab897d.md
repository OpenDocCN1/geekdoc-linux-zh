
## GNOME Mail Clients: Evolution, Balsa, and Others

Several GNOME-based mail clients are under development, many of which you can currently use (see Table 13-2). These include Evolution, Balsa, Mahogany, Althea, MMC, SMAN, Pygmy, Spruce, and Sylpheed (Balsa, Evolution, and Sylpheed are included with Red Hat). Check the GNOME Web site for more mail clients as they come out. Many are based on the GNOME mail client libraries (camel) currently under development, which provides support for standard mail operations. Balsa is a GNOME mail client with extensive features, though it can operate under any window manager, including KDE, as long as GNOME is installed on your system. Evolution is an integrated mail client, calendar, and contact manager from Ximian. The Mahogany mail client is a GNOME mail client that also has versions for other platforms. Althea is a stable IMAP mail client. The SMAN simple mail client is used to access POP3 servers. Pygmy is a simple GNOME mail client written in the Python programming language that supports attachments and MIME messages. Sylpheed is a mail and news client with an interface similar to Windows mail clients. Spruce is a GNOME e-mail client with support for multiple accounts. Several support tools are also available like mail checkers and notifiers, including RePopApp and Flink mail checkers, along with Sonicmail and gpostman mail notifiers.

Table 13-2: GNOME Mail Clients

| Application | Description |
|---|---|
| Balsa | E-mail client for GNOME that supports POP3, IMAP, local folders, and multithreading |
| Evolution | Ximian integrated mail client, calendar, and contact manager |
| Sylpheed | Mail and news client similar to Windows clients |
| Althea | Stable IMAP mail client |
| SQmail | A folder-based e-mail system (using mysql) |
| SMAN | Simple mail user agent that accesses POP3 servers |
| RePopApp | GNOME mail checker with support for multiple accounts |
| Mahogany | Cross-platform e-mail application |
| Flink | GNOME mail checker with IMAP, POP3, and mbox support |
| Pygmy | GNOME mail client written in the Python programming language |
| Spruce | E-mail client with support for multiple accounts |
| gpostman | Basic GNOME mail notifier |
| MMC | GNOME mail client |
| Sonicmail | GNOME POP3 mail notifier applet |

Balsa provides a full-featured GUI interface for composing, sending, and receiving mail messages. The Balsa window displays three panes for folders, headers, and messages. The left pane displays your mail folders. You initially have three folders: an inbox folder for received mail, an outbox folder for mail you have composed but have not sent yet, and a trash folder for messages you have deleted. You can also create your own mail folders in which you can store particular messages. To place a message in a folder you have created, click and drag the message header for that message to the folder.

## The K Desktop Mail Client: KMail

The K Desktop mail client, KMail, provides a full-featured GUI interface for composing, sending, and receiving mail messages. KMail is now part of the KContact package, which also includes an address book (KAddressBook), an organizer and scheduler (KOrganizer), and a note writer (KNotes). To start up KMail, you start the KContact application. The KMail window displays three panes for folders, headers, and messages. The upper-left pane displays your mail folders. You have an inbox folder for received mail, an outbox folder for mail you have composed but have not sent yet, and a sent-mail folder for messages you have previously sent. You can create your own mail folders and save selected messages in them, if you wish. The top-right pane displays mail headers for the currently selected mail folder. To display a message, click its header. The message is then displayed in the large pane below the header list. You can also send and receive attachments, including binary files. Pictures and movies that are received are displayed using the appropriate K Desktop utility. If you right-click the message, a pop-up menu displays options for actions you may want to perform on it. You can move or copy it to another folder, or simply delete it. You can also compose a reply or forward the message.

To set up KMail for use with your mail accounts, you must enter account information. Select the Configure entry in the Settings menu. Several panels are available on the Settings window, which you can display by clicking their icons in the left column. For accounts, you select the Network panel. You may have more than one mail account on mail servers maintained by your ISP or LAN. A configure window is displayed where you can enter login, password, and host information. For secure access, KMail now supports SSL, provided OpenSSL is installed. Messages can now be encrypted and decoded by users. It also supports IMAP in addition to POP and SMTP protocols.

## X Mail Clients: Mozilla and Emacs

Although many of the newer mail clients are being designed for either GNOME or the K Desktop, several mail clients were developed for use on the X Window System and operate under any window manager or desktop. They do not require either GNOME or the K Desktop. Mozilla mail and Emacs are two of the more popular mail clients. The Emacs mail clients are integrated into the Emacs environment, of which the Emacs editor is the primary application. They are, however, fully functional mail clients.

Mozilla is an Open Source version of Netscape based on Netscape 5.0. It has replaced Netscape as the primary Web browser on Red Hat distributions. To use the Mozilla mail client, you have simply to select it in the Tasks menu of the Mozilla Web browser or from the Internet menu on the GNOME program menu. When you first start Mozilla, you are prompted to enter new account information. You can add and edit accounts later by selecting the Mail/News Account Settings entry in the Edit menu. This opens a dialog box with a button for adding new accounts if you wish.

Note Netscape Communicator includes a mail client called Messenger. Account information, such as your mail server, username, and password, must be entered in the Mail panel in the Pro

The GNU version of Emacs includes a mail client along with other components, such as a newsreader and editor. GNU Emacs is included on Red Hat distributions. Check the Emacs Web site at www.gnu.org/software/emacs for more information. When you start up GNU Emacs, menu buttons are displayed across the top of the screen. If you are running Emacs in an X Window System environment, you have full GUI capabilities and can select menus using your mouse. To access the Emacs mail client, select from the mail entries in the Tools menu. To compose and send messages, just select the Send Mail item in the Tools menu. This opens a screen with prompts for To and Subject header entries. You then type the message below them, using any of the Emacs editing capabilities. GNU Emacs is a working environment within which you can perform a variety of tasks, with each task having its own buffer. When you read mail, a buffer is opened to hold the header list, and when you read a message, another buffer will hold the contents. When you compose a message, yet another buffer holds the text you wrote. The buffers you have opened for mail, news, or editing notes or files are listed in the Buffers menu. You can use this menu to switch among them.

XEmacs is another version of Emacs designed to operate solely with a GUI interface. The Internet applications, which you can easily access from the main XEmacs button bar, include a Web browser, a mail utility, and a newsreader. When composing a message, you have full use of the Emacs editor with all its features, including the spell-checker and search/replace.

## Command Line Mail Clients

Several mail clients use a simple command line interface. They can be run without any other kind of support, such as the X Window System, desktops, or cursor support. They are simple and easy to use but include an extensive set of features and options. Three of the more widely used mail clients of this type are Mail, New Message Handler (nmh), and Mutt. Mail is the mailx mail client that was developed for the Unix system. It is considered a kind of default mail client that can be found on all Unix and Linux systems. The nmh is a collection of mail access tools designed to be integrated into your shell easily. Mutt is a cursor-based client that can be run from the command line.
