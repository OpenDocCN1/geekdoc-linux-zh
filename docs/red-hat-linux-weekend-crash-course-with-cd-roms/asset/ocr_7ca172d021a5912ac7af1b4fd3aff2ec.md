```
-rw-r--r--  1 xmms     xmms     700909 Jan 30 15:22 xmms-1.0.0.tar.gz
-rw-r--r--  1 xmms     xmms     715574 Jan 30 15:15 xmms-1.0.1.tar.gz
226 Transfer complete.
ftp> binary
200 Type set to I.
ftp> get xmms-1.0.1.tar.gz
200 PORT command successful.
150 Opening BINARY mode data connection for xmms-1.0.1.tar.gz (715574 bytes).
226 Transfer complete.
715574 bytes received in 383 secs (1.8 Kbytes/sec)
ftp> bye
```

Notice that you have to log in with the user name anonymous — that’s why the FTP server is called the anonymous FTP server. For the password, you should type your e-mail address and then press Enter. To change the directory, use the cd command. For a directory listing, use the ls command.

You need to type the binary command to make sure that the data transfer occurs in binary mode (because the .tar.gz file is a binary file). Then you can use the get command to download the file — in this case, xmms-1.0.1.tar.gz. As I mentioned earlier, the .tar.gz extension tells you that this is a compressed tar archive. After the download is complete, type bye to end the anonymous FTP session.

After downloading the compressed tar file, you should first examine the contents with this command:

```
tar ztf xmms*.gz | more
xmms-1.0.1/
xmms-1.0.1/Makefile.in
xmms-1.0.1/README
xmms-1.0.1/stamp-h.in
xmms-1.0.1/AUTHORS
xmms-1.0.1/COPYING
xmms-1.0.1/ChangeLog
xmms-1.0.1/INSTALL
xmms-1.0.1/Makefile.am
xmms-1.0.1/NEWS
xmms-1.0.1/TODO
xmms-1.0.1/acconfig.h
xmms-1.0.1/acinclude.m4
xmms-1.0.1/aclocal.m4
xmms-1.0.1/config.guess
xmms-1.0.1/config.h.in
xmms-1.0.1/config.sub
xmms-1.0.1/configure
... rest of the output not shown ...
```

![](bbox=[0.01, 0.32, 0.1, 0.45])