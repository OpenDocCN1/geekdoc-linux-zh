
# yum install vsftpd

一旦安装了 `vsftpd` 软件包，你可以运行以下命令来熟悉该软件包的内容。运行此命令获取有关该软件包的一般信息：

```bash
# rpm -qi vsftpd
```

| 软件包 | Fedora Project |
| :--- | :--- |
| 供应商 | Fedora Project |
| URL | https://security.appspot.com/vsftpd.html |
| 摘要 | Very FTP Daemon |
|or | `vsftpd` 是一个 Very FTP daemon。它完全从零开始编写。 |

如果你想获取更多关于 `vsftpd` 的信息，请访问列出的 URL 相关网站 (`https://security.appspot.com/vsftpd.html`)。你可以获取有关 `vsftpd` 最新版本的额外文档和信息。

你可以查看 `vsftpd` 软件包的完整内容 (`rpm -ql vsftpd`)。或者只查看文档 (`-qd`) 或配置文件 (`-qc`)。要查看 `vsftpd` 软件包中的文件，请使用以下：

```bash
# rpm -qd vsftpd
/usr/share/doc/vsftpd-2.3.4/EXAMPLE/INTERNET_SITE/README
/usr/share/doc/vsftpd-2.3.4/EXAMPLE/PER_IP_CONFIG/README
/usr/share/doc/vsftpd-2.3.4/EXAMPLE/VIRTUAL_HOSTS/README
/usr/share/doc/vsftpd-2.3.4/EXAMPLE/VIRTUAL_USERS/README
/usr/share/doc/vsftpd-2.3.4/FAQ
/usr/share/doc/vsftpd-2.3.4/vsftpd.xinetet
```

## 第四部分：成为 Linux 服务器管理员

```
/usr/share/man/man5/vsftpd.conf.5.gz
/usr/share/man/man8/vsftpd.8.gz
```

在 `/usr/share/doc/vsftpd-*/EXAMPLE` 目录结构中，包含了了一些示例配置文件，可以帮助你以适用于站点、多 IP 地址和虚拟主机的方式来配置 `vsftpd`。主 `/usr/share/doc/vsftpd-*` 目录包含 FAQ（常见问题解答）、安装提示和版本信息。

当你准备开始配置 `vsftpd` 服务器时，man 页面可能包含最有用的信息。输入 `man vsftpd.conf` 读取关于配置文件的内容，输入 `man vsftpd` 读取关于守护进程的内容。

要列出配置文件，请输入以下命令：

```bash
# rpm -qc vsftpd
/etc/logrotate.d/vsftpd
/etc/pam.d/vsftpd
/etc/vsftpd/ftusers
/etc/vsftpd/user_list
/etc/vsftpd/vsftpd.conf
```

主配置文件是 `/etc/vsftpd/vsftpd.conf`。`ftusers` 和 `user_list` 文件提供了关于限制访问服务器的用户账户的信息。`/etc/pam.d/vsftpd` 文件设置了 FTP 服务器身份验证的方式。`/etc/logrotate.d/vsftpd` 文件配置了日志如何轮转。

现在你已经安装了 `vsftpd` 并快速查看了它的内容。下一步是设置并测试 `vsftpd` 服务。

# 启动 vsftpd 服务

如果你想使用默认设置，则不需要任何配置即可启动 `vsftpd` 服务。如果你按照 Fedora 交付的状态启动 `vsftpd`，你将得到：

- `vsftpd` 启动 `vsftpd` 守护进程，该进程在后台运行。
- `vsftpd` 监听的标准端口是 TCP 端口 21。默认情况下，连接建立后，数据通过 TCP 端口 20 传输给用户。必须在防火墙中开放 TCP 端口 21 以允许新连接访问该服务。（请查看“保护你的 FTP 服务器”部分，有关开放端口、启用被动 FTP 所需的连接跟踪以及设置与 FTP 相关的其他防火墙规则的详情。）
- `vsftpd` 守护进程读取 `vsftpd.conf` 来确定服务允许哪些功能。

# 第 18 章：配置 FTP 服务器

- Linux 用户账户（排除管理用户）和匿名用户账户（无需密码）可以访问 FTP 服务器。如果 SELinux 处于强制执行（Enforcing）模式，你需要设置一个布尔值来允许普通用户登录 FTP 服务器。详情请查看“保护你的 FTP 服务器”部分。
- 匿名用户仅可以访问 `/var/vsftpd` 目录及其子目录。普通用户从家目录作为当前目录开始，可以访问该用户通过普通登录或 SSH 会话能够查看的任何目录 `/etc/vsftpd/user_list` 和 `/etc/vsftpd/ftpusers` 文件中的用户列表定义了没有访问 FTP 服务器权限但没有上传权限的管理员和特殊用户。
- 匿名用户可以从服务器下载文件，但不能上传。普通用户可以根据 Linux 权限下载或上传文件。
- 详细说明文件上传或下载的日志消息被写在 `/var/log/xferlogs` 文件中。这些消息以标准的 xfer 格式存储。

如果你准备好使用上述默认设置启动服务器，下面的示例将向你展示如何操作。如果你想更改某些设置，请先进入“配置你的 FTP 服务器”部分确定你的设置，然后返回这里查看有关如何启用和启动服务器的说明。

在启动 `vsftpd` 服务之前，你可以检查它是否已经在运行。在 Fedora 中，请使用以下命令：

```bash
# systemctl status vsftpd.service
vsftpd.service - vsftpd daemon
Loaded: loaded ( /lib/systemd/system/vsftpd.service; disabled)
Active: inactive (dead)
Group: systemd-system/vsftpd.service
```

在 Red Hat Enterprise Linux 6 中，你需要两个命令来查看信息：

```bash
# service vsftpd status
vsftpd
# chconfig --list vsftpd
vsftpd  0:off  1:off  2:off  3:off  4:off  5:off  6:off
```

在 Fedora 和 RHEL 的示例中，服务、chconfig 和 systemctl 命令显示状态为已停止。你还可以看到它在 Fedora 中是禁用的（disabled），在 RHEL 中在每个运行级别都是禁用的。禁用（off）意味着当启动系统时，该服务不会开启。

要在 Fedora 中启动并启用 `vsftpd`（检查状态），请输入以下内容：

```bash
# systemctl start vsftpd.service
# systemctl enable vsftpd.service
ln -s '/lib/systemd/system/vsftpd.service' /etc/systemd/system/multi-user.target.wants/vsftpd.service
```

![](img/47358dd1a47f0ba12c47c96b4fe178b7_512_0.png)

## 第四部分：成为 Linux 服务器管理员

```bash
# systemctl status vsftpd.service
vsftpd.service - vsftpd daemon
Loaded: loaded ( /lib/systemd/system/vsftpd.service; disabled)
Active: inactive (dead)
Group: systemd-system/vsftpd.service
```

在 Red Hat Enterprise Linux 6 中，你需要两个命令来查看信息：

```bash
# service vsftpd status
vsftpd
# chconfig --list vsftpd
vsftpd  0:off  1:off  2:off  3:off  4:off  5:off  6:off
```

在 Fedora 和 RHEL 的示例中，服务、chconfig 和 systemctl 命令显示状态为已停止。你还可以看到它在 Fedora 中是禁用的，在 RHEL 中在每个运行级别都是禁用的。禁用（off）意味着当启动系统时，该服务不会开启。

要在 Fedora 中启动并启用 `vsftpd`（检查状态），请输入内容：

```bash
# systemctl start vsftpd.service
# systemctl enable vsftpd.service
```
