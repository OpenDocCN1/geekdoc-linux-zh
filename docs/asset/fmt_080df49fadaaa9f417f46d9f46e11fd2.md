
Sendmail 以新设置重启。这完成了创建邮件服务器的过程。

## 邮件投递的工作原理

当用户发送邮件时，邮件服务器查看目标地址，决定是在在本域接收邮件还是发送到其他域。如果地址在本域内，邮件服务器将其存储在队列中等待用户检索。如果地址在其他域，邮件服务器确定将邮件转发。

### 向域内发送邮件

#### 互联网

- 1 检查邮件地址的域名。
- 2 将邮件转发到邮件地址所在的邮件服务器。
- 3 接收到的邮件存储在邮件服务器的每个账户中。
- 4 当用户访问邮件服务器获取邮件后，邮件从服务器上删除。

## 创建邮件服务器，第 2 部分

### 安装 qpopper

发往用户的入邮件由 SMTP 服务器存储在邮件服务器上。用户访问 POP 服务器请求投递并将其传输到用户的邮件客户端。随后 POP 服务器将删除此邮件，完成邮件投递。

本节描述了如何编译并安装 POP 服务器程序 `qpopper`，使 Linux 邮件服务器提供 POP 服务器功能。

![](img/17f0f03278f20a01f4254f91fb48b8_147_0)

- 1 切换到解文件的目录。

切换目录。

```
[root@server CF-3.7Wp12#] cd /usr/local/src
[root@server src]# -
```

- 2 解压源文件。

| 解压源文件 | 输入命令。 |

> 注意：如果索引 CD-ROM 未挂载，请参见第 7.2 节的第 1 步并挂载它。

```
[root@server CF-3.7Wp12#] cd /usr/local/src
[root@server src]# tar xvfz /mnt/cdrom/dekiru/src/qpopper3.0b18.tar.2
qpopper3.0/
qpopper3.0/INSTALL
```

```
qpopper3.0/test/tgen
qpopper3.0/test/tscript
[root@server src]# -
```

> 提示！
> 获取 `qpopper` 的地址
> 获取此类邮件服务器的 URL 为 `http://eudora.qualcomm.com/free/servers.html`。

## 7.4 创建邮件服务器，第 2 部分

> 提示！
> `Popper` 和 `popauth` 程序

在这里安装的 `popper` 包含两个程序。其中一个是 `popper`，它是 POP 服务器。另一个程序名为 `popauth`，它是一个允许用户设置 APOP 密码的实用程序（请参见第 7.6 节）。如果未使用 `popauth` 设置密码，将使用 Linux 用户密码。

## 为编译 qpopper 准备

配置 `qpopper` 以使其支持 APOP。

- 切换目录。
- 输入命令。

```
[root@server src]# cd qpopper3.0/
[root@server qpopper3.0]# ./config --enable-apop --with-popuid=mail --enable-specialauth
/creating cache /config.cache
checking whether make sets ${MAKE}... yes
```

```
creating mmangle/Makefile
creating config.h
[root@server qpopper3.0]# 
```

## 编译 qpopper。

- 输入命令。

```
[root@server qpopper3.0]# ./config --enable-apop --with-popuid=mail --enable-specialauth
[root@server qpopper3.0]# make
cd ./popper. && make all
make[1]: Entering directory '/usr/local/src/qpopper3.0/popper'
gcc -c -I.. -I. -I. -./mmangle -g -O2 -fstack-reduce -fpcc-struct-return
```

```
在最后一行出现之前需要很长一段时间。作者 Albert
gcc -o popauth flock.o base64.o scram md5.o hmac.o popauth.o -lresolv -lgdbm
make[1]: Leaving directory '/usr/local/src/qpopper3.0'
[root@server qpopper3.0]# 
```

## 安装 qpopper。

- 切换目录。

```
make[1]: Leaving directory '/usr/local/src/qpopper3.0/popper'
[root@server qpopper3.0]# cd ..
install -s -m 4755 -o mail -g mail popauth /usr/bin/
[root@server popper#]# install -s popauth /usr/sbin/
[root@server popper#]# 
```

- 输入命令。
- 输入命令。

## 第 7 章。创建邮件服务器

## 初始化 APOP 密码数据文件。

输入命令。

```
[root@server popper#] install -s -m 4755 -o mail -g mail popauth /usr/bin
[root@server popper#] popauth -init
[root@server popper#]# 
```

## 编辑配置文件。

输入命令。

```
[root@server popper#] popauth -init
[root@server popper#] vi /etc/inetd.conf
```

注意：`inetd.conf` 文件是 Linux 网络服务的配置文件。

打开配置文件。

注意：关于 `vi` 文本器的信息请参阅第 95 页。

```
#
# Pop and imap mail services et al
#pop-2 stream tcp nowait root /usr/sbin/tcpd ipop2d
#pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
#imap stream tcp nowait root /usr/sbin/tcpd imapd
# The Internet UUOCP service.
```

因为 `pop-3` 行被注释掉了，请取消注释使其生效。

将 `ipop3d` 守护进程改为 `popper`。

```
#
# Pop and imap mail services et al
#pop-2 stream tcp nowait root /usr/sbin/tcpd ipop2d
#pop-3 stream tcp nowait root /usr/sbin/tcpd popper -s
#imap stream tcp nowait root /usr/sbin/tcpd imapd
# The Internet UUOCP service.
```

输入 "`popper -s`"。

删除 `#` 以使设置生效。

保存修改后的文件并退出。

## 实现设置。

```
[root@server popper]# /etc/rc.d/init.d/inet reload
[root@server popper]# 
```

新的配置文件已加载。这标志完成了邮件服务器的安装。

## IMAP 可以替代 POP

可以使用互联网消息访问协议 `IMAP` 代替 `POP` 来读取邮件。`IMAP` 给人一种信箱存放在服务器上的印象。当使用 `POP` 时，邮件在被客户端获取后会从服务器上删除。因此，邮件只能从该客户端读取。如果使用 `IMAP`，则可以从另一个客户端或其他地方访问同一个信箱。

要让你的 Linux 邮件服务器支持 `IMAP`，使用 `rpm` 命令安装 `IMAP` 服务器，然后取消 `/etc/inetd.conf` 文件中 `imap` 行的注释。

- 输入命令。
- 输入命令。
- 删除 `#` 以使设置生效。

`#imap tcp nowait root /usr/sbin/tcpd imapd`
`imap tcp nowait root /usr/sbin/tcpd imapd`

- 保存修改后的文件并退出。
- 输入命令。

```
[root@server /root]# /etc/rc.d/init.d/inet reload
[root@server /root]# 
```
