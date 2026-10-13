
## gFTP

The gFTP program is a simpler GNOME FTP client designed to let you make standard FTP file transfers. It has an interface similar to WS_FTP used on Windows. The gFTP window consists of several panes. The top-left pane lists files in your local directory, and the top-right pane lists your remote directory. Subdirectories have folder icons preceding their names. The parent directory can be referenced by the double period entry (..) with an up arrow at the top of each list. Double-click a directory entry to access it. The pathnames for all directories are displayed in boxes above each pane. You can enter a new pathname for a different directory to change to it, if you want.

Two buttons between the panes are used for transferring files. The left arrow button, <-, downloads selected files in the remote directory, and the right arrow button, ->, uploads files from the local directory. To download a file, click it in the right-side pane and then click the left arrow button, <-. When the file is downloaded, its name appears in the left pane, your local directory. Menus across the top of the window can be used to manage your transfers. A connection manager enables you to enter login information about a specific site. You can specify whether to perform an anonymous login or to provide a username and password. Click the Connect button to connect to that site. A drop-down menu for sites enables you to choose the site you want.

## NcFTP

The NcFTP program has a screen-based interface that can be run from any shell command line. It does not use a desktop interface. FTP operations are executed using commands you enter at a prompt. Options and bookmarks can be selected using cursor-based menus. To start up NcFTP, you enter the ncftp command on the command line. If you are working in a window manager, such as KDE, GNOME, or FVWM, open a shell terminal window and enter the command at its prompt. The main NcFTP screen consists of an input line at the bottom of the screen with a status line above it. The remainder of the screen is used to display commands and responses from remote systems. For example, when you download files, a message specifying the files to be downloaded is displayed in the status line. NcFTP lets you set preferences for different features, such as anonymous login, progress meters, or a download directory. Enter the pref command to open the preferences screen. From there, you can select and modify the listed preferences.

To connect to an FTP site, you enter the open command on the input line, followed by the site's address. The address can be either an IP address or a domain name, such as ftp.gnome.org. If you don't supply an address, a list of your bookmarked sites is displayed, and you can choose one from there. By default, NcFTP attempts an anonymous login, using the term "anonymous" as your username and your e-mail address as the password. When you successfully connect, the status bar displays the remote site's name on the left and the remote directory name on the right.

```
open ftp.gnome.org
```

If you want to log into a specific account on a remote site, have yourself prompted for the username and password by using the -u option with the open command. The open command remembers the last kind of login you performed for a specific site and repeats it. If you want to change back to an anonymous login from a user login, you use the -a option with the open command. For busy sites, you may be unable to connect on the first try and you must repeat the open process. NcFTP has a redial capability you turn on with the -r option. The -d option sets the delay for the next attempt, and the -g option sets the maximum number of connection attempts. With the lookup command, you can obtain the IP and domain name addresses for an FTP site. The lookup command takes as an argument either the IP or domain name address and then displays both. This is useful for finding a site's IP address. With the -v option, more information, such as aliases, is retrieved. The NcFTP open options are shown in Table 14-5.

### Table 14-5: NcFTP Open Options

| Option | Description |
|---|---|
| -a | Connect anonymously |
| -u | Connect with username and password prompts |
| `-p num` | Use specified port number when connecting |
| `-r` | Redial until connected |
| `-d num` | Set delay (num) in number of seconds for redial option |
| `-g num` | Specify the maximum number of redials |

Once connected, you enter commands on the input line to perform FTP operations such as displaying file lists, changing directories, or downloading files. With the ls command, you can list the contents of the current remote directory. Use the cd command to change to another remote directory. The dir command displays a detailed listing of files. With the page command, you view the contents of a remote file, a screen at a time. To download files, you use the get command, and to upload files, you use the put command. During a download, a progress meter above the status bar displays how much of the file has been downloaded so far. The get command has several features described in more detail in the following section. When you finish, you can disconnect from the site with the close command. You can then use open to connect to another site, or quit the NcFTP program with the quit command. The help command lists all NcFTP commands. You can use the help command followed by the name of a command to display specific information on it.

The NcFTP program supports several commands that operate on your local system. These are usually standard FTP command names preceded by an l. lcd changes your local working directory, lls lists the contents of your local directory, lpage displays the contents of a local file a screen at a time, and lpwd displays the local directory's full pathname. For any other local commands or scripts you need to execute, use the shell escape command, !. Simply precede the shell command or script with a !. The NcFTP program also provides commands for managing files and directories on your remote site, provided you have the permission to do so. You can use mkdir to create a remote directory, and rmdir to remove one. Use the rm command to erase remote files. With the rename command, you can change their names. The NcFTP commands are listed in Table 14-6.

### Table 14-6: NcFTP Commands

| Command | Description |
|---|---|
| help [command] | Lists names of NcFTP commands |
| cd [directory] | Changes the working directory on the remote host |
| create [filename] | Creates an empty file on the remote host, enabling you to use the filename as a message |
| debug | Turns debugging on or off |
| version | Displays version information |
| dir | Displays a detailed directory listing |
| echo | Displays a string, useful for macros |
| get | Downloads files from a remote host to your working directory |
| lcd [directory] | Changes the local working directory |
| lls | Lists files in your local working directory |
| lookup host | Looks up entries for remote hosts |
| lpage filename | Displays contents of local file, a page at a time |
| lpwd | Displays the local current working directory |
| mkdir directory name | Creates a directory on the remote host |
| mode mode | Specifies transfer mode (b for block mode, s for stream mode) |
| open [option] hostname | Connects to a remote host. If no hostname is specified, the bookmark editor displays a host list from which you can choose one: -a forces anonymous login -u forces user login -r redials automatically -d specifies time delay before redial; used with -r -g specifies the maximum number of redials; used with -r |
| page filename | Displays the contents of a remote file |
| pdir | Same as dir, but outputs to your pager, enabling you to display a remote file list a page at a time. Used for command line interface |
| pls | Same as ls, but outputs to your pager. Used for command line interface |
| redir | Redisplays the last directory listing |
| predir | Redisplays the last directory listing and outputs to pager if working in command line interface |
| put filename | Uploads a file to a remote host |
| pwd | Displays the remote current working directory |
| rename orig-name new-name | Changes the name of a remote file |
| quit | Quits NcFTP |
| quote | Sends an FTP protocol command to the remote server |
| rhelp [command] | Sends a help request to the remote host |
| rm filenames | Erases remote files |
| rmdir directories | Removes remote directories |
| site command | Executes site-specific commands |
| type type | Changes transfer type (ASCII, binary, image) |
| ! command | Escapes to the shell and executes the following shell command or script |

The NcFTP program also has a colon mode of operation that enables you to issue a single ncftp command to download a file. Enter the ncftp command, followed by a URL, for the file you want. You can enter the command on the shell command line or place it within a script. For example, the following command downloads the readme file on the Red Hat FTP site:

$ ncftp ftp.redhat.com/pub/README

In the colon mode, the -c option sends the file to the standard output and the -m option pipes it to your
