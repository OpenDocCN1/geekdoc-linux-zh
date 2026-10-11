
### 图 4-21 设置 Stunnel.PEM 文件的保护。

```
$ set security/protection=(G,W) stunnel.pem
```

`root@lnxone~~`

文件 编辑 设置 帮助

### 图 4-22 将 Stunnel.EXE 文件和服务器启动脚本文件拷贝到 Stunnel 目录。

```
$ set def ssl$root:[stunnel]

$ dir

Directory SSL$ROOT:[STUNNEL]

STUNNEL-3.22,DIR:1 STUNNEL.PEM:1

Total of 2 files.

$ copy ssl$root:[stunnel-3.22.vms] stunnel.exe ssl$root:[stunnel]*,* 

$ copy ssl$root:[stunnel-3.22.vms] stunnel_startup_server.com ssl$root:[stunnel]*,* 

$ dir

Directory SSL$ROOT:[STUNNEL]

STUNNEL-3.22,DIR:1 STUNNEL_EXE:1

STUNNEL_STARTUP_SERVER.COM:1

Total of 4 files.
```

`root@lnxone:~`

文件 编辑 设置 帮助

### 图 4-23 编辑 `stunnel_startup.server.com` 文件并定位到 "stunnel =" 行；然后用 "#" 注释掉它。

```
$! 编辑此命令过程文件以在你的环境中运行 Stunnel

$! 作者: Taka Shinagawa, OpenVMS 安全

$! (takaaki.shinagawa@hp.com)

$! 日期: 2002年6月2日

######################################################################

$! 定义一个 Stunnel 命令 /* 为你的本地主机编辑此命令：Stunnel 命令 */

$! Telnet

$ stunnel_command = "STUNNEL -d 992 -r localhost:23 -p -stunnel,pem -o stunnel+

######################################################################

$! 询问私钥是否加密

$ question:

$ inquire encrypted = "私钥（PEM 文件中的）是否已加密？[Y/N]"

$ if encrypted .eqs

$ then

$ goto question

$ else
```

`root@lnxone:~`

文件 编辑 设置 帮助

### 图 4-24 如高亮显示所示，添加 Stunnel 命令，并将第二行作为单行命令包含，在 -p 处隔一个空格（删除多余的 "-"）。将其保存为 DCL 脚本的新版本。

```
$! 编辑此命令过程文件以在你的环境中运行 Stunnel

$! 作者: Taka Shinagawa, OpenVMS 安全

$! (takaaki.shinagawa@hp.com)

$! 日期: 2002年6月2日

######################################################################

$! 定义一个 Stunnel 命令 /* 为你的本地主机编辑此命令 */

$! Telnet

$ stunnel_command = "STUNNEL -d 992 -r localhost:23 -p -stunnel,pem -o stunnel+

$ stunnel_command = "STUNNEL -d 992 -r localhost:23 -p -

$slroot:[stunnel,stunnel,pem -o stunnel.log"

$! 询问私钥是否加密

$ question:

$ inquire encrypted = "私钥（PEM 文件中的）是否已加密？[Y/N]"

$ if encrypted .eqs

$ then

$ goto question

$ else

$ if encrypted .eqs = "Y" then goto encrypted
```

第 4 章 – OpenVMS 和 Linux 的安全工具 49

### 图 4-25 验证现在是否有两个版本的 `stunnel_server_startup.com` 文件。

```
$ dir

目录 SSL@ROOT:[STUNNEL]

STUNNEL-3.22,DIR:1 STUNNEL.EXE:1 STUNNEL.PEM:1

STUNNEL_STARTUP_SERVER,COM:2 STUNNEL_STARTUP_SERVER.COM:1

共 5 个文件。
```

### 图 4-26 运行 `stunnel_server_startup.com` 脚本。使用与你加密 PEM 证书时相同的密码，注意区分大小写（记住在密码周围始终使用双引号——务必如此）。

```
$ dir

目录 SSL@ROOT:[STUNNEL]

STUNNEL-3.22,DIR:1 STUNNEL.EXE:1 STUNNEL.PEM:1

STUNNEL_STARTUP_SERVER,COM:2 STUNNEL_STARTUP_SERVER.COM:1

共 5 个文件。

$ @stunnel_startup_server

私钥（PEM 文件中的）是否已加密？[Y/n]: y

输入解密密钥的密码（请在使用时带双引号）：

"welcome"

正在启动在端口 992 运行的隧道

RUN-S-PROC_ID, 创建的进程标识为 20200435

Stunnel 成功启动！
```

50 Linux 与 OpenVMS 互操作性

## Linux 上安装 Stunnel 客户端

图 4-27 至 4-34 展示了在 Linux 上安装 Stunnel 客户端。

### 图 4-27 执行一个进程以确保 Stunnel 进程正在运行。

```
root@lnxone:~

文件 编辑 设置 帮助

私钥（PEM 文件中的）是否已加密？[Y/N]: y

输入解密密钥的密码（请在使用时带成对的双引号）：

"welcome"

正在启动在端口 992 运行的 Stunnel

IRULN-S-PROC_ID, 创建的进程标识为 20200437

Stunnel 成功：启动！

$ show system:process=stunnel_992

OpenVMS 7.3-1 运行于节点 VMSNODE 2002-AUG-26 20:16:53.37 运行时间 0 01:51:06

PID Name State Pri I/O CPU Page lists Pages

20200437 STUNNEL992 LE 5 659 0:00:00.19 369 481
```

### 图 4-28 解压 `stunnel-22.tar.gz`：`gzip -dc stunnel-22.tar.gz | tar -x`

```
root@lnxone:~/Stunnel

文件 编辑 设置 帮助

root@lnxone:~/Stunnel

[root@lnxone:~/Stunnel]#

[root@lnxone:~/Stunnel]# ls -al

total 2128

dr-xr-x 2 root root 25 44

stunnel-22.tar.gz
```
