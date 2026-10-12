
with the .tar.gz or .tar.Z extension — often referred to as a compressed tarball. If you want the software, you have to download the compressed tarball and unpack it.

扩展名为 .tar.gz 或 .tar.Z —— 通常被称为压缩 tar 包。如果你想要该软件，你必须下载压缩的 tar 包并解包它。

You download the compressed tar file using anonymous FTP or the Web browser. Typically, this involves no more effort on your part than clicking a link and saving the file in an appropriate directory on your system.

你可以使用匿名 FTP 或 Web 浏览器下载压缩的 tar 文件。通常，这只需要你点击链接并将文件保存到系统中的适当目录即可，无需更多操作。

To try your hand at downloading and building a software package, you can practice on the X Multimedia System (XMMS) — a graphical X application for playing MP3 files and other multimedia files. XMMS is bundled with Red Hat Linux and is installed on your system when you select the Multimedia Support package group during Red Hat Linux installation. However, there is no harm in downloading and rebuilding the XMMS package again.

为了练习下载和构建软件包，你可以练习 X 多媒体系统（XMMS）—— 一个用于播放 MP3 文件和其他多媒体文件的图形化 X 应用。XMMS 与 Red Hat Linux 捆绑在一起，当你在 Red Hat Linux 安装期间选择多媒体支持软件包组时，它会被安装到你的系统上。然而，再次下载并重新构建 XMMS 软件包也无妨。

You can access the source files for XMMS from http://www.xmms.org/download.html in the form of a compressed tar archive. You can also download the files from the xmms/1.0 directory of the anonymous FTP server (ftp.xmms.org). You should try downloading from the anonymous FTP server so you know how to manually download files.

你可以通过 http://www.xmms.org/download.html 以压缩 tar 归档的形式访问 XMMS 的源文件。你也可以从匿名 FTP 服务器（ftp.xmms.org）的 xmms/1.0 目录下载文件。你应该尝试从匿名 FTP 服务器下载，以便了解如何手动下载文件。

Before attempting to download a file from an FTP server, make sure that your Linux system is connected to the Internet. You should also change the directory to the location where you want to store the downloaded file (although you can always move the file after downloading). I typically log in as root and change the directory to /usr/local before typing the ftp command. If you use the GNOME or KDE desktop, you type these commands from a terminal window.

在尝试从 FTP 服务器下载文件之前，请确保你的 Linux 系统已连接到互联网。你还应将目录更改为想要存储下载文件的位置（尽管下载后也可以随时移动文件）。我通常以 root 身份登录，并在输入 ftp 命令前将目录更改为 /usr/local。如果你使用 GNOME 或 KDE 桌面，则从终端窗口输入这些命令。

## Downloading the software

## 下载软件

Here is a sample session that you can use as a guideline when you download the compressed tar file for XMMS from the anonymous FTP server. The lines I typed appear in boldface.

以下是一个示例会话，可作为你从匿名 FTP 服务器下载 XMMS 压缩 tar 文件时的参考。我输入的行以粗体显示。

```
ftp ftp.xmms.org
Connected to ftp.xmms.org.
220 ProFTPD 1.2.0pre10 Server (FTP server for awpti.org) [awpti.org]
Name (ftp.xmms.org:naba): anonymous
331 Anonymous login ok, send your complete e-mail address as password.
Password: (Type your e-mail address and press Enter)
230 Anonymous access granted, restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd xmms/1.0
250 CWD command successful.
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for file list.
drwxr-xr-x 6 xmms xmms 4096 Jan 30 15:20 rpm
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

请注意，你必须使用用户名 anonymous 登录——这就是该 FTP 服务器被称为匿名 FTP 服务器的原因。对于密码，你应输入你的电子邮件地址然后按 Enter。要更改目录，请使用 cd 命令。要列出目录，请使用 ls 命令。

You need to type the binary command to make sure that the data transfer occurs in binary mode (because the .tar.gz file is a binary file). Then you can use the get command to download the file — in this case, xmms-1.0.1.tar.gz. As I mentioned earlier, the .tar.gz extension tells you that this is a compressed tar archive. After the download is complete, type bye to end the anonymous FTP session.

你需要输入 binary 命令以确保数据传输以二进制模式进行（因为 .tar.gz 文件是二进制文件）。然后你可以使用 get 命令下载文件——在本例中为 xmms-1.0.1.tar.gz。如前所述，.tar.gz 扩展名表示这是一个压缩的 tar 归档。下载完成后，输入 bye 以结束匿名 FTP 会话。

After downloading the compressed tar file, you should first examine the contents with this command:

下载压缩的 tar 文件后，你应首先使用以下命令检查其内容：

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

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_334_0.png)

The output of this command shows you the contents of the archive and gives you an idea of the directories that are created once you unpack the archive. In this case, a directory named xmms-1.0.1 is created in the current directory (which, in my case, is /usr/local). From the listing, you also learn the programming language used to write the package. If you see .c and .h files, that means the source files are in the C programming language used to write many open source software packages.

此命令的输出显示了归档的内容，并让你了解解包归档后创建的目录。在本例中，名为 xmms-1.0.1 的目录将在当前目录中创建（在我这里是 /usr/local）。从列表中，你还可以了解到用于编写该软件包的编程语言。如果看到 .c 和 .h 文件，则表示源文件使用 C 编程语言编写，而 C 语言被用于编写许多开源软件包。

## Unpacking the software

## 解包软件

To extract (or unpack) the contents of the tar archive, type the following tar command:

要提取（或解包）tar 归档的内容，请输入以下 tar 命令：

```
tar zxvf xmms*.gz
```

You again see the long list of files as they are extracted from the archive and copied to the appropriate directories on your hard disk.

你会再次看到长长的[content]
with the .tar.gz or .tar.Z extension — often referred to as a compressed tarball. If you want the software, you have to download the compressed tarball and unpack it.

扩展名为 .tar.gz 或 .tar.Z —— 通常被称为压缩 tar 包。如果你想要该软件，你必须下载压缩的 tar 包并解包它。

You download the compressed tar file using anonymous FTP or the Web browser. Typically, this involves no more effort on your part than clicking a link and saving the file in an appropriate directory on your system.

你可以使用匿名 FTP 或 Web 浏览器下载压缩的 tar 文件。通常，这只需要你点击链接并将文件保存到系统中的适当目录即可，无需更多操作。

To try your hand at downloading and building a software package, you can practice on the X Multimedia System (XMMS) — a graphical X application for playing MP3 files and other multimedia files. XMMS is bundled with Red Hat Linux and is installed on your system when you select the Multimedia Support package group during Red Hat Linux installation. However, there is no harm in downloading and rebuilding the XMMS package again.

为了练习下载和构建软件包，你可以练习 X 多媒体系统（XMMS）—— 一个用于播放 MP3 文件和其他多媒体文件的图形化 X 应用。XMMS 与 Red Hat Linux 捆绑在一起，当你在 Red Hat Linux 安装期间选择多媒体支持软件包组时，它会被安装到你的系统上。然而，再次下载并重新构建 XMMS 软件包也无妨。

You can access the source files for XMMS from http://www.xmms.org/download.html in the form of a compressed tar archive. You can also download the files from the xmms/1.0 directory of the anonymous FTP server (ftp.xmms.org). You should try downloading from the anonymous FTP server so you know how to manually download files.

你可以通过 http://www.xmms.org/download.html 以压缩 tar 归档的形式访问 XMMS 的源文件。你也可以从匿名 FTP 服务器（ftp.xmms.org）的 xmms/1.0 目录下载文件。你应该尝试从匿名 FTP 服务器下载，以便了解如何手动下载文件。

Before attempting to download a file from an FTP server, make sure that your Linux system is connected to the Internet. You should also change the directory to the location where you want to store the downloaded file (although you can always move the file after downloading). I typically log in as root and change the directory to /usr/local before typing the ftp command. If you use the GNOME or KDE desktop, you type these commands from a terminal window.

在尝试从 FTP 服务器下载文件之前，请确保你的 Linux 系统已连接到互联网。你还应将目录更改为想要存储下载文件的位置（尽管下载后也可以随时移动文件）。我通常以 root 身份登录，并在输入 ftp 命令前将目录更改为 /usr/local。如果你使用 GNOME 或 KDE 桌面，则从终端窗口输入这些命令。

## Downloading the software

## 下载软件

Here is a sample session that you can use as a guideline when you download the compressed tar file for XMMS from the anonymous FTP server. The lines I typed appear in boldface.

以下是一个示例会话，可作为你从匿名 FTP 服务器下载 XMMS 压缩 tar 文件时的参考。我输入的行以粗体显示。

```
ftp ftp.xmms.org
Connected to ftp.xmms.org.
220 ProFTPD 1.2.0pre10 Server (FTP server for awpti.org) [awpti.org]
Name (ftp.xmms.org:naba): anonymous
331 Anonymous login ok, send your complete e-mail address as password.
Password: (Type your e-mail address and press Enter)
230 Anonymous access granted, restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd xmms/1.0
250 CWD command successful.
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for file list.
drwxr-xr-x 6 xmms xmms 4096 Jan 30 15:20 rpm
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

请注意，你必须使用用户名 anonymous 登录——这就是该 FTP 服务器被称为匿名 FTP 服务器的原因。对于密码，你应输入你的电子邮件地址然后按 Enter。要更改目录，请使用 cd 命令。要列出目录，请使用 ls 命令。

You need to type the binary command to make sure that the data transfer occurs in binary mode (because the .tar.gz file is a binary file). Then you can use the get command to download the file — in this case, xmms-1.0.1.tar.gz. As I mentioned earlier, the .tar.gz extension tells you that this is a compressed tar archive. After the download is complete, type bye to end the anonymous FTP session.

你需要输入 binary 命令以确保数据传输以二进制模式进行（因为 .tar.gz 文件是二进制文件）。然后你可以使用 get 命令下载文件——在本例中为 xmms-1.0.1.tar.gz。如前所述，.tar.gz 扩展名表示这是一个压缩的 tar 归档。下载完成后，输入 bye 以结束匿名 FTP 会话。

After downloading the compressed tar file, you should first examine the contents with this command:

下载压缩的 tar 文件后，你应首先使用以下命令检查其内容：

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

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_334_0.png)

The output of this command shows you the contents of the archive and gives you an idea of the directories that are created once you unpack the archive. In this case, a directory named xmms-1.0.1 is created in the current directory (which, in my case, is /usr/local). From the listing, you also learn the programming language used to write the package. If you see .c and .h files, that means the source files are in the C programming language used to write many open source software packages.

此命令的输出显示了归档的内容，并让你了解解包归档后创建的目录。在本例中，名为 xmms-1.0.1 的目录将在当前目录中创建（在我这里是 /usr/local）。从列表中，你还可以了解到用于编写该软件包的编程语言。如果看到 .c 和 .h 文件，则表示源文件使用 C 编程语言编写，而 C 语言被用于编写许多开源软件包。

## Unpacking the software

## 解包软件

To extract (or unpack) the contents of the tar archive, type the following tar command:

要提取（或解包）tar 归档的内容，请输入以下 tar 命令：

```
tar zxvf xmms*.gz
```

You again see the long list of files as they are extracted from the archive and copied to the appropriate directories on your hard disk.

你会再次看到长长的
