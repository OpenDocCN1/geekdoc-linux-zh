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
cctftp / ~
```

To log in as a user other than anonymous, a -u user option, where user is replaced by the name you want to log in. Enter the password as prompted to continue.

# Using nctftp

After you are logged in with the nctftp session running, there are a few features you can use that are not available with other FTP clients. Here are some examples:

+   - bookmark — If you are visiting a site that you want to return to, type the bookmark command and a name to identify that site. The next time you start nctftp session, type the bookmark name as an option. You are only logged into the FTP site you bookmarked; you are taken to the directory where you set the bookmark.

+   - ls, lmkdir, lpwd — There is a series of commands that enable you to move around the local file system. Place a letter l1 in front of standard shell commands such as ls, cd, mkdir, pwd, rm, and rdir and you can move around and work with your local file system while you are in nctftp.

+   - help — Use rhelp to see commands that are recognized by the FTP server. To see commands that are specific to the FTP server, type help while you are in an nctftp session.

+   - Auto-resume — If you were disconnected in the middle of a large download, you will appreciate this feature. After a connection is broken during a download, reconnect to the FTP site and begin downloading the file in the same local directory. The nctftp command resumes where it left off.

+   - Tab completion — Press the Tab key to have nctftp complete file names and paths.

Using nctftp for background transfers

If you are moving around different parts of the FTP site, or jumping between different sites, you might not want to wait for a file transfer to complete before you go somewhere else. The nctftp command has an excellent feature for placing transfers in a spool file and then running them in the background immediately or later.