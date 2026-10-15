

```
-rw-r--r-- 1 other 1657 Oct 22 2002 .indexhead
-rw-r--r-- 1 other 510 Jul 27 1996 .message
-rw--- 1 other 1153 Nov 12 2003 Makefile
dr-sr-xr-x 7 other 1120 Jul 24 2014 admin
drwxr-xr-x 10 sys 192 Jun 03 2009 dos
lrwxrwxrwx 1 sys 12 Apr 13 2012 electronics -> user/rstevew
-rw-r--r-- 1 sys 40608 May 29 23:30 index
drwxr-xr-x 4 sys 64 Jun 03 2009 lib
dr-sr-xr-x 3 other 128 Jun 03 2009 linux
drwxrwxr-x 2 jons 176 Jun 03 2009 midnight_beach
drwxr-xr-x 2 other 96 Jun 03 2009 misc
dr-sr-xr-x 3 other 80 Jun 03 2009 osx
lrwxrwxrwx 1 sys 1 Apr 13 2012 pub -> .
drwxr-xr-x 5 other 976 Mar 22 2012 scobins
dr-sr-xr-x 6 other 2256 Jan 05 2012 scripts
dr-sr-xr-x 4 other 624 Jul 20 2011 source
drwxr-xr-x 3 other 112 Jun 03 2009 text
dr-sr-xr-x 3 other 96 Jun 03 2009 unixware
drwxr-xr-x 38 other 640 May 02 2014 user
dr-sr-xr-x 3 other 288 May 27 2011 www
226 Transfer complete.

ftp>
```

看起来 unixware 目录里可能有些有趣的东西，但在探索那个目录之前，我先查看一下 index 消息。

2. 要读取文本文件，我会获取它但复制到 /dev/tty。或者，如果我担心它比几行长，我会获取它然后使用 ! shell 转义在本地查看它，如下所示：

Click here to view code image

```
ftp> get index
local: index remote: index
227 Entering Passive Mode (192,122,209,23,43,229)
150 Opening BINARY mode data connection for index (40608 bytes).
100% |**************************************| 40608 39.73 KiB/s | 00:00 ETA
226 Transfer complete.
40608 bytes received in 00:01 (37.32 KiB/s)
ftp> !head index
Having <a href=ftpserve.html>problems connecting to the FTP server</a>?

deepthought’s archives are in the following directories:
#index
/*
admin ...... Administrative utilities (ksh and gawk programs)
dos ....... DOS utilities
misc ....... Miscellaneous archives
scobins .... Binary executables for SCO UNIX 3.2v5
scripts .... Interpreted programs, mostly ksh and gawk scripts
ftp>
```

啊，看起来也没那么有趣。 我将进入 unixware 看看里面有什么。

3. 我使用 cd 切换到该目录，然后使用 dir 查看那里有什么：

Click here to view code image

```
ftp> cd unixware
250 CWD command successful.
ftp> dir
```

```
227 Entering Passive Mode (192,122,209,23,105,229)
150 Opening ASCII mode data connection for /bin/ls.
total 80
-rw-r--r--   1 1042      18724 Jan 16  2003 cwtmp
drwxr-xr-x   2 sys           64 Jun 03  2009 help_pages
-rw-r--r--   1 sys         357 Jan 16  2003 index
-rw-r--r--   1 source     17236 Mar 19  2002 pcmd
226 Transfer complete.
ftp>
```

这次，我直接查看 index 文件：

Click here to view code image

```
ftp> get index /dev/tty
local: /dev/tty remote: index
227 Entering Passive Mode (192,122,209,23,11,86)
150 Opening BINARY mode data connection for index (357 bytes).
unixware/
Binary executables for SCO UnixWare. Tested only under UnixWare 7.
Source is in the source/ directory.
# HTML version at http://www.armory.com/~ftp/index.html#unixware/

Filename    Description
cwtmp       Remove useless entries from wtmp & fix wtmp & utmp corruption.
pcmd        Push characters into tty input buffer, as though typed at keyboard.

226 Transfer complete.
357 bytes received in 00:00 (4.20 KiB/s)
ftp>
```

正如你所见，这个归档服务器上有很多东西。我可以用 cd 和 dir 继续探索，直到找到感兴趣的东西，但我将改为使用 quit 断开连接，结束这次匿名 FTP 的快速游览！

## Note

随着像 SourceForge 这样的基于 Web 的归档库的兴起，FTP 归档就像恐龙一样，每年变得更加过时。如今很难找到有用的 FTP 归档，除非有令人信服的理由这样做，否则我建议通过 Firefox 或其他图形化工具来探索归档、获取源文件和复制文档会更好。

不过，如果你小心使用，FTP 仍然是获取互联网信息的合法方式。成千上万的系统通过匿名 FTP 提供各种服务：表 21.2 列出了其中一些最有趣的。

