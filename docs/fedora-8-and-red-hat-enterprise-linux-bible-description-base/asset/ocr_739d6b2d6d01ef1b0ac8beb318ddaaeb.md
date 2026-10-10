FTP exiting commands

While a connection is open to a remote computer from an FTP client in Fedora, you can use several commands to either temporarily or permanently exit from that connection. Here are some useful commands:

+   - ! — This command temporarily exits you to the local shell. After you have done what you need to do, type **exit** to return to your FTP session. You can also use this command to run other local commands. For example, you can type `pwd` to see what the current directory is on the local system, `1uname -a` to remind yourself of your local system name, or `1ls -l` to see the contents of your current directory.

+   - **close** — Closes the current connection.

+   - **bye** — Closes the connection and exits the `ftp` command. You can also use **quit** in place of **bye**.

Using the ncftp command

By virtue of being an FTP client program, the `ncftp` command supports all the standard commands you would expect to find in an FTP client (`get`, `put`, `ls`, `cd`, and so on). However, `ncftp` has added features that make it more efficient and friendlier than some other FTP clients.

> NOTE: You can install the ncftp package by typing `yum install ncftp`.

With `ncftp`, you can connect to an FTP server in the same way you did with `ftp`. One convenient difference is that if you enter no user name, `ncftp` assumes you want to use the anonymous user name and just logs you in. Here is an example:

```
$ ncftp ftp.mozilla.org

NcFTP 3.2.1 (Oct 05, 2007) by Mike Gleason
(http://www.NcFTP.com/contact/).
Connecting to ftp.mozilla.org...
(vrsFTpd 2.0.5).
Logging in...
Login successful.
Logged in to ftp.mozilla.org.
ncftp / >
```

To log in as a user name other than anonymous, add a `-u user` option, where user is replaced by the name you want to log in as. Enter the password as prompted to continue.

Using ncftp

After you are logged in with the `ncftp` session running, there are a few nice features you can use that aren't available with other FTP clients. Here are some examples: