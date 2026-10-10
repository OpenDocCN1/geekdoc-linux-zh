# Part II  Using CentOS

```
Name (sparky:mike): jake
331 Please specify the password.
Password: ********
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

In this example, ftp connects to a computer called sparky (ftp sparky). When I was prompted for a name, it assumed that I was going to use my current login name on sparky (sparky:mike). I could have pressed [Enter] to use the name mike, but instead I logged in as jake and typed the password when prompted. The password was accepted, and, after some information was printed, I was given an ftp> prompt.

Because FTP is used for public servers, you can often log in using the word anonymous as your username. By entering a valid e-mail address as your password, you can enter the anonymous FTP site and download files that the server makes available to the public. Sometimes the username and password ftp is also reserved for anonymous logins.

Unlike Telnet, instead of being in a regular UNIX shell after I logged in with FTP, I was placed in FTP command mode. Command mode with FTP includes a whole lot of commands for moving around the remote file system and for copying files (which is its main job).

> **NOTE**  If you are behind a firewall and having trouble connecting to FTP servers, learn about active and passive FTP. Refer to the following: http://slacksite.com/other/ftp.html.

# *FTP Directory Commands*

To get your bearings and move around the remote file system, you could use some of the following commands from the ftp> prompt. The commands are used to work with both the remote and local directories associated with the FTP connection.

+   - **passive** — Turns passive data transfer mode on and off. Passive mode may be required from behind firewalls that don’t allow incoming connections.
+   - **pwd** — Shows the name of the current directory on the remote system.
+   - **ls** — Lists the contents of the current remote directory using the UNIX ls command. You can use any valid ls options with this command, provided that they are supported by the particular FTP server you are connected to
+   - **dir** — Same as ls
+   - **cd** — Use the cd command to move to the named directory on the remote system.
+   - **cdup** — Moves up one directory in the file system.
+   - **lcd** — Use the lcd command to move to the named directory on the local system.