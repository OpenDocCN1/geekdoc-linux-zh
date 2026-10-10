• **bookmark** — If you are visiting a site that you want to return to, type the bookmark command and type a name to identify that site. The next time you start an ncftp session, type the bookmark name as an option. Not only are you logged into the FTP site you bookmarked; you are taken to the directory where you set the bookmark.

• **lls, lcd, lmkdir, lpwd** — There is a set of commands that enables you to move around the local file system. Just place a letter l in front of standard shell commands such as ls, cd, mkdir, pwd, rm, and rmdir and you can move around and work with your local file system while you are in ncftp.

• **rhelP** — Use rhelP to see commands that are recognized by the remote FTP server. To see commands that are specific to the FTP server, type help while you are in an ncftp session.

• **Auto-resume** — If you were disconnected in the middle of a large download, you will appreciate this new feature. After a connection is broken during a download, reconnect to the FTP site and begin downloading the file again in the same local directory. The ncftp command resumes downloading where it left off.

# Using ncftp for background transfers

If you are moving around to different parts of the FTP site, or jumping between different sites, you might not want to wait around for a file transfer to complete before you can go somewhere else. The ncftp command has an excellent feature for placing transfer commands in a spool file and then running them in the background immediately or later.

To select a file for background transfer, use the bgget command. Here is an example:

```
ncftp /pub > bgget wireless.doc
•Spooled: get wireless.doc
ncftp /pub > jobs
---Scheduled-For-----------Host-----------Command-----------
2007-06-01 18:38 maple GET wireless.doc
ncftp /pub > bgstart
Background process started.
Watch the "/home/br/.ncftp/spool/log" file to see how it is progressing
```

In this example, the bgget command spools the wireless.doc file from the remote current directory (/pub) and sets it to be copied to the local current directory. Typing the jobs command shows that the job (GET wireless.doc), from the host named maple, is scheduled to run immediately (6:38 p.m., June 1, 2007). By running the bgstart command this process, and any other spooled jobs, are run immediately.

Instead of starting the background transfers immediately you can do them later. For background jobs spooled for transfer, the transfer begins when you quit ncftp, leave your current FTP site, or go to another FTP site. In this way, the program that does the transfer (ncftpbatch) can take over your current login session to do the transfer.