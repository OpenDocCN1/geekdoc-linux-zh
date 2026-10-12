```
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

In this example, ftp connects to a computer called maple (ftp maple). When I was prompted for a name, it assumed that I was going to use my current login name on maple (maple:mike). I could have pressed Enter to use the name mike, but instead I logged in as jake and typed the password when prompted. The password was accepted and, after some information was printed, I was given an ftp> prompt.

Because FTP is used for public servers, you can often log in using the word anonymous as your user name. By entering a valid e-mail address as your password, you can enter the anonymous FTP site and download files that the server makes available to the public.

Unlike telnet, instead of being in a regular UNIX shell after I logged in with FTP, I was placed in FTP command mode. Command mode with FTP includes a whole lot of commands for moving around the remote file system and for copying files (which is its main job).

# FTP directory commands

To get your bearings and move around the remote file system, you could use some of the following commands from the ftp> prompt. The commands are used to work with both the remote and local directories associated with the FTP connection.

+   - pwd — Shows the name of the current directory on the remote system.
+   - ls — Lists the contents of the current remote directory using the UNIX ls command. You can use any valid ls options with this command, provided that they are supported by the particular FTP server you are connected to.
+   - dir — Same as ls.
+   - cd — Use the cd command to move to the directory named.
+   - cdup — Moves up one directory in the file system.
+   - lcd — Lists the name of the current local directory.

If you want to make changes to any of the remote files or directories, use the following commands:

+   - mkdir — Creates a directory on the remote system.
+   - rename — Renames a file or directory on the remote system.
+   - rmdir — Removes a remote directory.
+   - delete — Removes a remote file.
+   - mdelete — Removes multiple remote files.