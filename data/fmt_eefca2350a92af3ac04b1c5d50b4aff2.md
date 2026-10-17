
`ipfwadm -F -a m -S ipaddress/32 -D 0.0.0.0/0`

其中 `ipaddress` 是你接入网络的 Windows 95 电脑的 IP 地址（点点表示法）。你还应该 `su` 切换到超级用户 `root`，并从命令行执行此命令。你只需要执行一次；此后，每当你重启 Linux 系统时，该命令都会自动执行。

# 配置 POP3 服务

如果你希望你的 Windows 95 用户从 Linux 服务器下载邮件，你必须在你的 Linux 机器上启用 POP3 服务。POP（邮局传输协议）从单个用户的邮箱中读取邮件并将其转发给她。Linux 自带了一个名为 `in.pop3d` 的 POP3 守护进程。

POP3 守护进程的配置非常简单：只需将其开启即可。要执行此操作，请 `su` 切换到超级用户 `root` 并执行以下操作：

- 确保文件 `/etc/services` 中的以下行未被注释：

| Service | Port | Description |
| :--- | :--- | :--- |
| pop3 | 110/tcp | POP version 3 |
| pop3 | 110/udp | |

- 确保文件 `/etc/inetd.conf` 中的以下行未被注释：

```
pop3 stream tcp nowait root /usr/sbin/tcpd /usr/sbin/in.pop3d
```

按照我们在第 3 章描述的方法重启 `inetd` 守护进程。

## 影子密码

你应该注意的一个“坑”是，在 Slackware 环境下编译的 POP3 守护进程假设你安装了影子密码支持。如果你在安装 Slackware 时选择不使用影子密码，POP3 守护进程将无法正常工作——当用户输入密码时，它将始终失败，因为它会在 `/etc/shadow` 文件中查找密码，而不是 `/etc/passwd`。

解决此问题的唯一方法是获取 POP3 守护进程的源码并重新编译程序。如果你不熟悉 C 语言编程，请让当地的“大神”为你完成此工作。

程序员 Katie Stevens 提供的常用发行实现位于 `archive pop3d-1.00.44.tar` 中。这应该可以开箱即正确编译；只需确保 `Makefile` 中的 `CFLAGS` 设置如下：

```
CFLAGS = -O6 -DEFINUS
```
