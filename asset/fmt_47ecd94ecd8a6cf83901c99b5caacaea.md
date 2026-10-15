
# 加密数据流

在这种情况下，将 Window Maker 作为第一个客户端启动，几乎整个会话将通过 SSH 进行隧道化，无需任何进一步干预。

# 安装、配置和使用 OpenSSH

由于原始 SSH 协议实现的商业性质，一组程序员开始与 OpenBSD 项目合作开发 SSH 协议的开放实现版本。OpenSSH 完全兼容 SSH 2.x 版本协议，而除 OpenBSD 以外操作系统的版本（Portable OpenSSH，便 OpenSSH）在 Linux 上运行良好。可以在 `http://www.openssh.com` 找到 OpenSSH 的主页。

![](img/5b265b1d98ba2e1a657c3f9cdc5ce677_266_0.png)

> OpenSSH 有两种运行模式，其中一种与 ssh2 使用的新 SSH 版本 2.x 协议兼容。由于 OpenSSH 对 SSH 2.x 版本协议的实现尚未完成，本文将仅讨论 OpenSSH 和 1.x 版本的 SSH。

## 下载、编译和 OpenSSL

在下载、编译和安装 OpenSSL 之前，你需要下载、编译并安装 OpenSSL，这是一个 SSH 依赖的库。OpenSSL 主页可以在 `http://www.openssl` 找到。

Open源码下载页面可以在 `http://www.openssl` 找到。下载最新的源码包后，提取源码并进入新创建的目录：

```
$ tar -xzf openssl-0.9.6.tar.gz

$ cd openssl-0.9.6
```

现在配置、编译并安装 OpenSSL：

```
$ ./config

...[output of config]...

$ make

...[output of make]...

$ su

Password:

# make install

...[output of make install]...

$ exit

$
```

OpenSSL 的默认配置将其大部分文件安装在 `/usr/local`，库位于 `/usr/local/lib`。

## 下载和安装 OpenSSH

要下载 OpenSSH，访问 Portable OpenSSH 下载页面 `http://www.openssh.com/portable.html`。选择你附近的镜像站点并下载最新的 `.tar.gz` 源码包。提取源码并进入新创建的目录：

```
$ tar xzf openssh-2.3.0p1.tar.gz

$ cd openssh-2.3.0p1

$
```

在 `openssh-2.3.0p1` 目录下，使用 `configure` 命令为你的系统环境定制源码配置。你可能希望使用 `--with-tcp-wrappers` 选项允许 OpenSSH 与 TCP wrappers 工作：

```
$ ./configure --with-tcp-wrappers

...[/ output of configure ]...

$
```

如果你想更改最终 OpenSSH 安装的位置，使用 `--prefix` 选项更改安装路径：

```
./configure --with-tcp-wrappers --prefix=/opt/openssh2
```

记住，如果你在配置源码时调整了安装路径，以后配置和使用 OpenSSH 时需要考虑此差异。与 SSH 类似，可以使用额外的选项来更改最终 OpenSSH 安装的某些属性或行为；要查看这些选项的列表，请使用 `--help` 选项：

```
./configure --help
```

`configure` 在早期 Pentium 或旧系统上可能需要几分钟才能完成。如果没有返回错误，可以使用系统构建并安装 OpenSSH。不要忘记以超级用户安装，否则安装尝试将失败。

```
$ make

...[/ output of make ]...

$ su

Password:

# make install

...[/ output of make install ]...

# exit

$
```

### 加密数据流

安装 OpenSSH 文件后，需要对 `/etc/services` 和 `/etc/inetd.conf` 文件进行一些更改。这些更改将允许 `inetd` TCP 封装透明地管理入站的 SSH 请求，从而简化 SSH 的某些使用方面并节省资源。在 `/etc/services` 中添加以下行：

```
- ssh 22/tcp openssh

- ssh 22/udp openssh
```

这些行定义了一个名为 `ssh2` 的新服务，该服务将在端口 22 上监听以待的入站连接。如果你计划在另一个端口上运行 OpenSSH，请务必根据需要调整端口号。现在在 `/etc/inetd.conf` 中添加启动 OpenSSH 的行：

```
ssh stream tcp nowait /usr/sbin/tcpd /usr/local/sbin/sshd -i
```

此行允许 `inetd` 在需要使用 TCP 封装时启动 OpenSSH 守护进程。通过这种方式，你可以通过 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件使用 `sshd` 作为服务的名称来控制对 SSH 的访问。一旦对系统的网络配置文件完成了这些更改，你希望向系统的 `inetd` 进程发送挂断信号（HUP）：

```
killall -HUP inetd
```

这将重启 `inetd` 程序，并使你对 `/etc/inetd.conf` 文件所做的任何更改生效。

在 OpenSSH 能够使用密码认证之前，还必须为 `sshd` 守护进程创建 PAM 配置。实现此点的最简单方法是使用位于 OpenSSH 源码树中 `contrib` 目录下的通用 PAM 配置文件。只需将该文件复制到 `/etc/pam.d` 目录即可：

```
# cd openssh-2.3.01/contrib

# cp sshd.pam.generic /etc/pam.d/sshd
```
