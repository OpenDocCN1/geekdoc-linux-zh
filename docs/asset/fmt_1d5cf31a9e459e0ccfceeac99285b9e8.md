
total 8

r-- 1 joely_joely 35 Feb 22 20:31 homework.txt

r-- 1 joely_joely 422 Feb 22 20:31 notes.txt

226 Transfer complete.

ftp> quit

221 Goodbye.

506 book@mycomputer:"$

```
FIGURE 12.26 显示远程目录、列出发送的文件并退出 ftp。
```

# 使用 ftp 检索文件

`ftp` 提供了相应的 `get` 和 `mget` 命令分别检索单个或多个文件。图 12.27 展示了从示例账户检索单个 ascii 文件。在本例中，当前工作目录是 `/Intro_to_UNIX/chap12/work_files`，以便你可以将文件检索到该目录。

为了演示二进制传输模式以及多个文件的检索，图 12.28 从远程工作系统检索多个二进制文件到你示例路径 `/Intro_to_UNIX/chap12/work_files` 下的本地工作目录 `/project_files`。图 12.28 还禁用了提示，这样你就不会被提示确认每个文件的检索。

图 12.29 还展示了通过退出 `ftp` 并列出传输文件的当前工作目录来查看这些文件的效果。

# 基于网络的工具 415

```
506 book@computer:~$ ftp workcomputer.workdomain.org

Connected to workcomputer.

220 ftp server (Version 6.4/OpenBSD/Linux-ftpd-0,17) ready.

Name (workcomputer.workdomain.org:book): lisa

331 Password required for lisa

Password:

230 User logged in.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp> lcd -R Intro_to_UNIX/chap12/work_files

Local directory: /home/book/Intro_to_UNIX/chap12/work_files

ftp> asc

200 set to A.

ftp> get work_report.txt

local: work_report.txt remote: work_report.txt

200 PORT command successful.

150 Opening ASCII data connection for 'work_report.txt' (8072 bytes).

222 Transfer complete.

8184 bytes received in 0.05 secs (174,8 kB/s)

ftp>
```

> 12.27 在 ascii 模式下检索单个文件。

```
ftp> cd project_files

250 C command successful.

ftp> bin

200 Type set to 1.

ftp> prompt

Interactive mode off.

ftp> mget *

local: network-report.ps remote: network-report.ps

150 Opening BINARY data connection for 'network-report.ps' (11853 bytes).

222 Transfer complete.

11853 bytes received in 0.03 secs (4470,0 kB/s)

local: network-present.eps remote: network-present.eps

200 PORT command successful.

150 Opening BINARY data connection for 'network-present.eps' (5949 bytes).

222 Transfer complete.

5949 bytes received in 0.00 secs (1481,3 kB/s)

local: report_tar.gz remote: report_tar.gz

200 PORT command successful.

150 Opening BINARY data connection for 'report.tar.gz' (7613 bytes).

222 Transfer complete.

7613 bytes received in 0.00 secs (1756,3 kB/s)

ftp>
```

> 12.28 使用 `ftp` 在非交互式模式下检索多个文件。

```
ftp> quit

221 Goodbye.

510 book@mycomputer:~$ ls -l Intro_to_UNIX/chap12/work_files/

total 144

-trw--r-- 1 book 11853 Feb 22 22:20 network-report.ps

-trw--r-- 1 book 5949 Feb 22 22:20 network-present.eps

-trw--r-- 1 book 7613 Feb 22 22:20 report.tar.gz

-trw--r-- 1 book 8072 Feb 22 21:47 work_report.txt

511 book@mycomputer:~$
```

> 12.29 退出 `ftp` 并列出检索到的文件。

# 匿名或公共 ftp 登录

如果你不需要使用用户名或密码登录远程系统，那么一切还没有不可救。商业和公共系统通常提供匿名 `ftp` 访问，允许任何人登录到他们的系统来检索文件。如果允许这种类型的访问，可以通过用户名 `anonymous` 或 `ftp` 登录远程系统来获取，如果需要密码，你通常可以提供一个电子邮件地址。例如，图 12.30 展示了如何匿名登录到远程系统，以获取 `xv` 程序的 RPM 或源码，你可以利用它来查看和编辑图形，就像你在第 8 章“文本格式——创建和查看排版文档”中所做的那样。在图 12.30 中，你指定使用 `ftp` 作为匿名用户名，导航到预先学习的目录，列出其内容并检索感兴趣的文件。`ftp.org` 是另一个包含大量软件软件包的仓库，你可以下载并使用。

```
512 book@computer:~$ ftp ftp.trilon.com

Connected to ftp.trilon.com.

220-

--Welcome to trilon.com!

220-

220 trilon.com FTP server (Version wr-2,6,2(3)) Thu Apr 28 19:55:44 CDT 2005 ready

d.

Name (ftp,trilon,book):

331 login ok, send your complete e-mail address as password.

Password:

230 login ok, access restrictions apply.

Remote system is UNIX.

Using binary mode to transfer files.

ftp cd pub/binaries

250 CWD command successful.

ftp is

220 PORT command successful.

150 Opening ASCII mode data connection for /bin/ls.

drwxr-xr-x 2783 538 4096 Sep 16 2000 _ut_conf

trw-r--r 1783 538 1255 Sep 16 2000 solaris.install

trw-r--r 1783 538 108321 Sep 16 2000 xv-3.10a-1386.rpm

trw-r--r 1783 538 1326 Sep 16 2000 red-hat-readme.txt

trw-r--r 1783 538 12280 Sep 16 2000 xv-3.10a-Solaris.2.pkg.tgz

drwxr-xr-x 1783 538 585411 Sep 16 2000 xv310a.sgi.gz

228 Transfer complete.

ftp get xv-3.10a-1386.rpm

local: xv-3.10a-1386.rpm transferred from remote

200 PORT command successful.

150 Opening BINARY mode connection for xv-3.10a-1386.rpm (8219 bytes)

228 Transfer complete.
```
