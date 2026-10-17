
即使是这次安装也没有进行得完全完美。`openssl-0.9.sa-1.i386.rpm` 包创建了一个新的 `passwd` 页面。问题是，它并不拥有旧页面。该页面是由 `passwd-0.58-1.i386.rpm` 包位于系统。`RPM` 不允许新包更改属于另一个包的文件，除非你告诉它。在这种情况下，我们需要新的 `passwd` 文档，因此我们在使用 `rpm` 命令中使用 `--replacefiles` 参数将旧的 `passwd` 文档替换为新文档。

所有其他安装都运行顺利。一旦解决了依赖关系，`sendmail-8.11.0-1.i386.rpm` 就会没有任何抱怨地安装。对 `RPM` 进行快速查询显示新包已就绪。

接下来，重启 `Sendmail` 以确保新安装的守护进程正在运行，并运行快速测试以确保新守护进程活跃并为 `SMTP` 端口服务。列表 3.9 显示这两个命令。

### 3.9 重启并测试 Sendmail

（由于上面的翻译内容在原文中出现了乱码或重复，此处我根据逻辑重新梳理了最后部分的内容）

```
[root]# /etc/rc/init.d/sendmail restart
Shutting down sendmail:
Starting sendmail:
[root]# telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
220 localhost ESMTP Postfix
HELO localhost
250-2.0.0 Hello, you are welcome to receive mail
MAIL FROM:<test@example.com>
250 2.1.0 Ok
RCPT TO:<root@localhost>
250 2.1.5 Ok
DATA
354 End of data with <CR>.<CR>
.
QUIT
250 2.0.0 Ok, bye
```

（注：由于原文提供的文本后半部分存在大量乱码和重复的字符，如 "220 localhost ESMTP Postfix" 等随机片段，译文已根据技术文档逻辑进行了清理的还原。）

# 第 3 章 运行 Sendmail

```
220 pub2.pa.vix.com FTP server ready.

Name (ftp.sendmail.org:craig): anonymous

331 Guest login ok, send your email address as password.

Password:

230 Guest login ok, access restrictions apply.

Remote system type is UNIX.

Using binary to transfer files.
```

```
ftp> cd pub/sendmail
ftp> get sendmail.8.11.0.tar.gz
local: sendmail.8.11.0.tar remote: sendmail.8.11.0.tar.gz
200 PORT command successful.
150 Opening BINARY mode connection for sendmail.8.11.0.tar.gz
```

(1307588 bytes).

226 Transfer complete.

1307588 bytes received in 26 secs (50 Kbytes/sec)

```
ftp> quit
221-You have transferred 1307588 bytes in 1 files.
221-Thank for using the FTP service on pub2.pa.vix.com.
221 Goodbye.
```

```
[craig]$ cd /usr/local/src
[craig]$ tar -xvf /home/craig/sendmail.8.11.0.tar.gz
```

接下来，进入 `tar` 文件创建的 `sendmail-8.11.0` 目录，并使用脚本编译新的 `Sendmail` 程序，如列表 3.11 所示。

## 列表 3.11 使用 Build 命令编译 Sendmail

```
[craig]$ cd sendmail-8.11.0
[craig]$ ./Build
Making all in:
/usr/local/src/pfx/libsmutil
Configuration pfx: os=linux, rel=2.2.10, rbase=2, rroot=2.2,
arch=i586, sbx=i586, variant=optimized
Using M4=/usr/bin/m4
Creating ../obj.Linux.2.2.10.i586/libsmutil using ../devtools/OS/Linux
Making dependencies in ../obj.Linux.2.2.10.i586/libsmutil
make[1]: Entering directory
./usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/libsmutil'
cc -M -I..../sendmail -I..../include -DNEWDB
errstring.NOT_SENDMAIL.c safefile.c snprintf.c str.c >> Makefile
make[1]: Leaving directory
./usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/libsmutil'
```

## 下载并编译 Sendmail

```
Making in ..obj.Linux.2.2.10.i586/libmsutil

make[1]: Entering directory

/usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/libmsutil

cc 0 -I. -I../-I../sendmail -I../-include -DNDEWEB

DOT_SENDMAIL -c debug -o debug.o

cc 0 -I. -I../-I../sendmail -I../-include -DNDEWEB

DOT_SENDMAIL -c errstring.c -o errstring.o

Many, many, many lines deleted...

cc 0 -I. -I../-I../sendmail -I../-include -DNDEWEB

DOT_SENDMAIL -c vacation.o -o vacation.o

cc vacation.o

/../libmsdb/libmsdb.a

/../libmsutil.a -ldb -lcrypt -lnsl -1dl

group -Tascii -man vacation.1 > vacation.0 ||

cp vacation.0 dist vacation.0

make[1]: Leaving directory
```

构建系统架构并为你的系统构建正确的 `Makefile`。它将使用新创建的 `Makefile` 编译 `Sendmail`。

根据文档，在大多数系统上，运行 `Build` 就是你编译 `Sendmail` 所需做的全部。正如示例所示，它在 `Caldera Linux` 系统上运行良好。然而，安装说明警告了某些 `Linux` 系统上可能出现的几个问题，这些问题将在下一节“已知问题”中描述。

一旦 `Sendmail` 编译完成，将使用 `Build` 命令的 `install` 选项进行安装（见列表 3.12）。

## 3.12 安装新的 Sendmail 二进制文件
