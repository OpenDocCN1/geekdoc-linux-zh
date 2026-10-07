

# 第 3 章  Sendmail

220 pub2-pa.vix FTP server ready.
Name (ftp.sendmail.org:craig): anonymous
331 Guest login ok, send your e-mail address as password.
Password:
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd pub/sendmail
ftp> get sendmail.8.11.0.tar.gz
local: sendmail.8.11.0.tar.gz remote: sendmail.8.11.0.tar.gz
200 PORT BINARY command successful.
150 Opening BINARY mode data connection for sendmail.8.11.0.tar.gz
(130785 bytes).
226 Transfer complete.
130785 bytes received in 26 secs (50 Kbytes)
ftp> quit
221-You have transferred 130785 bytes in 1 files.
221-Thank you for using the FTP service pub2.pa.vix.com.
221 Goodbye.
[craig]$ cd /usr/local/src
[craig]$ tar -zxvf /home/craig/sendmail.8.11.0 directory created by the tar file,

接下来，进入 tar 文件创建的 sendmail-8.11.0 目录，并使用脚本编译新的 Sendmail 程序，如列表 3.11 所示。

## 列表 3.11 使用 Build 命令编译 Sendmail

```
[craig]$ cd sendmail-8.11.0
[craig]$ ./Build
Making all:
/usr/local/src/sendmail-8.11.0/libsmsutil
Configuration: pfx=, os=linux, rel=2.2.10, rbase=2, root=2.2,arch=i586, sfx, variant=optimized
Using M4=/usr/bin/m4
Creating ../obj.Linux.2.2.10.i586/libsmsutil using ../devtools/OS/Linux
Making dependencies in ../obj.Linux.2.2.10.i586/libsmsutil
make[1]: Entering directory
/usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/libsmsutil
cc -M -I. -I..../sendmail -I..../include -DNEWDB
-DNOT_SENDMAIL debug.
-erring string lockfile.c safefile.c snprintf strl.c >> Makefile
make[1]: Leaving directory
/usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/libsmsutil
```

## 下载并编译 Sendmail

```
Making in ..obj.Linux.2.2.10.i586/libsmutil
make[1]: Entering directory
'/usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/libsmutil'
cc -O -I../../sendmail -I../include -DNEWWEDB
-DNOT_SENDMAIL -c ..//debug.c -o debug.c
cc -O -I../../sendmail -I../include -DNEWWEDB
-DNOT_SENDMAIL -c ..//errstring.c -o errstring.o
- Many, many, many lines deleted...
cc -O -I../../sendmail -I../include -DNEWWEDB
-DNOT_SENDMAIL -c vacation.c -o vacation.o
cc -o vacation.o ../libmsdb/libsmdb.a
/libsmutil/libsmutil.a -ldb -lresolv -lcrypt -lnsl -lndl -Tascii -man vacation.1 > vacation.0 ||
cp vacation.0 dist.vacation
make[1]: Leaving directory

```/sendmail-8.11.0/obj.Linux.2.2.10.i586/vacation
Build 检测到系统架构并为系统构建正确的 Makefile。然后使用新创建的 Makefile 编译 Sendmail。
根据文档，在大多数系统中，你只需要运行 Build 即可编译 Sendmail。如示例所示，它在 Calder Linux 系统上运行良好。然而，安装过程中在某些 Linux 系统可能会出现一些问题，这些将在下一节“已知问题”中描述。
一旦 Sendmail 编译完成，使用带有 install 参数的 Build 命令进行安装（参见列表 3.12）。

## 列表 3.12 安装新的 Sendmail 二进制文件

```
# ./build install
Making all in:
/usr/local/src/sendmail-8.11.0/libsmutil
Configuration: pfx=, os=linux, rel=2.2.10, rbase=2, root=2.2, arch=i586, sfx, variant=optimized
Making in ..obj.Linux.2.2.10.i586/libsmutil
make[1]: Entering directory
'/usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/libsmutil'
cc -O -I../../sendmail -I../include -DNEWWEDB
-DNOT_SENDMAIL -c ..//debug.c -o debug.c
cc -O -I../../sendmail -I../include -DNEWWEDB
-DNOT_SENDMAIL -c ..//errstring.c -o errstring.o
- Many, many, many lines deleted...
cc -O -I../../sendmail -I../include -DNEWWEDB
-DNOT_SENDMAIL -c vacation.c -o vacation.o
cc -o vacation.o ../libmsdb/libsmdb.a
/libsmutil/libsmutil.a -ldb -lresolv -lcrypt -lnsl -lndl -Tascii -man vacation.1 > vacation.0 ||
cp vacation.0 dist.vacation
make[1]: Leaving directory
/usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/vacation
Build 检测到系统架构并为系统构建正确的 Makefile。然后使用新创建的 Makefile 编译 Sendmail。
根据文档，在大多数系统中，你只需要运行 Build 即可编译 Sendmail。如示例所示，它在 Calder Linux 系统上运行良好。然而，安装过程中在某些 Linux 系统可能会出现一些问题，这些将在下一节“已知问题”中描述。
一旦 Sendmail 编译完成，使用带有 install 参数的 Build 命令进行安装（参见列表 3.12）。

（此处重复的段落已根据指令要求不再重复输出原文/译文，保持逻辑一致）

## 已知问题

Sendmail 文档列了一些影响 Linux 的问题。这些问题分为几类：

一种是 Sendmail 与内核之间的不兼容。另一个是

这需要修复，你可以通过使用命令行选项 `-C` 为 sendmail 命令提供配置文件的正确路径，例如 `sendmail -C/etc/sendmail.cf`。还需要编辑 Sendmail 的启动脚本以插入此命令行选项，以便在每次系统启动时都使用正确的配置文件。坦率地说，这麻烦得不偿手。只需将 sendmail.cf 文件移动到 /etc 即可。

无论你做什么，文件的物理位置和配置中定义的文件位置必须一致。

## 配置兼容性

Sendmail 8.11 还更改了 Sendmail 配置文件（sendmail.cf）的位置。该文件原本位于 /etc 目录，这也是大多数 Linux 系统中找到它的地方。Sendmail 8.11 使用新的 /etc/mail 目录存放 sendmail.cf 文件。在系统上运行新编译的 Sendmail 将失败，因为系统将 sendmail.cf 文件保留在 /etc 目录，而 Sendmail 8.11 在 /etc/mail 目录中查找它。一个简单的测试显示：

```
[root]# sendmail -v -t
line 0: cannot open: No such file or directory
/etc/sendmail.cf
```

这需要修复，你可以通过使用命令行选项 `-C` 为 sendmail 命令提供配置文件的正确路径，例如 `sendmail -C/etc/sendmail.cf`。还需要编辑 Sendmail 的启动脚本以插入此命令行选项，以便在每次系统启动时都使用正确的配置文件。坦率地说，这麻烦得不偿手。只需将 sendmail.cf 文件移动到 /etc 即可。

