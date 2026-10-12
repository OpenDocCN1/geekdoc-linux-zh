The same approach of accessing anonymous FTP sites works if you type the hostname of some other anonymous FTP server. For example, try typing the following URL:

```
ftp://ftp.netscape.com
```

You get the directory of the `ftp.netscape.com` server.

# # Using the Command-Line FTP Client

Knowing how to use FTP from the command line is a good idea — just in case. For example, your GUI desktop may not be working and to fix the problem, you may have to download some files. If you know how to use the command-line FTP client, you can download the files and take care of the problem. It’s not that hard.

The best way to learn the command-line FTP client is to try it out. The command is called `ftp`, and you can try out the `ftp` commands from your Fedora Core system. You don’t even need any Internet connection because you can use the `ftp` command to connect to your own system — I show you how.

In the following sample FTP session, I use the command-line FTP client to log in using my username (*naba*) and browse the directories on my system. When you try a similar operation, replace the name with your username and provide your password. Here’s the listing showing the commands (my comments appear in *italics*):

```
```
ftp localhost
Connected to localhost (127.0.0.1).
220 (vsFTpd 1.2.1)
Name (localhost:naba):    (I press Enter.)
331 Please specify the password.
Password:             (I type my password.)
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> help             (I type help to see a list of FTP commands.)
Commands may be abbreviated.  Commands are:
```

```

+   * !, debug, mdir, sendport, site
+   * $, dir, mget, put, size
+   * account, disconnect, mkdir, pwd, status
+   * append, exit, mls, quit, struct
+   * ascii, form, mode, quote, system
+   * bell, get, mtime, recv, unique