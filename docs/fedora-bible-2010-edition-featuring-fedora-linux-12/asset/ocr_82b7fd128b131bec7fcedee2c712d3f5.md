# ### Getting files with FTP

FTP is a protocol that is available on many different operating systems. Archives of files on the Internet are stored on what are called **FTP servers**. To connect to those servers from Fedora, you can either type the URL of that server into a Web browser or you can use the `lftp` command or graphical FTP windows such as **gFTP**. Of the other FTP client programs available for Fedora, my favorite is the `ncftp` command.

# ### Using the lftp command

The `lftp` command is available on Fedora for copying files to and from FTP servers. The `lftp` command has a command mode or you can use it to connect directly to a remote computer. For example:

```
```
$ lftp maple
lftp maple:~>
```
```

In this example, `lftp` connects to a computer called maple (`ft pmaple`). Unless you use the `-u username` option, you are automatically logged in using the anonymous user account. See Chapter 19 for how to set up your own FTP server.

Unlike ssh, instead of being in a regular Linux shell after you log in with an FTP client, you are placed in FTP command mode. Command mode with FTP includes a whole lot of commands for moving around the remote file system and for copying files (which is the main job of an FTP client).

> **NOTE:** If you are behind a firewall and having trouble connecting to FTP servers, learn about **active and passive FTP**. Refer to the following: <http://slacksite.com/other/ftp.html>.

# ### FTP directory commands

To get your bearings and move around the remote file system, you could use some of the following commands from the `lftp host:->` prompt. The commands are used to work with both the remote and local directories associated with the FTP connection.

+   - `pwd` — Shows the name of the current directory on the remote system.
+   - `ls` — Lists the contents of the current remote directory using the Linux `ls` command. You can use any valid `ls` options with this command, provided that they are supported by the particular FTP server you are connected to.
+   - `dir` — Same as `ls`.
+   - `cd` — Use the `cd` command to move to the named directory on the remote system.
+   - `lpwd` — Shows the name of your current directory on your local system.
+   - `lcd` — Use the `lcd` command to move to the named directory on the local system.

If you want to make changes to any of the remote files or directories, use the following commands: