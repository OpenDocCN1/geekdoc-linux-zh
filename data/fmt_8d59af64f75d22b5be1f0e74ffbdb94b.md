
# service inetd restart

Debian、Slackware 和 Gentoo 等 Linux 发行版通过 `inetd` 超守护进程开启 SWAT 服务。在安装 SWAT 后，你只需从 `/etc/inetd.conf` 文件中删除 `swat` 行前的注释字符（以 root 用户身份使用任何文本编辑器）并重启守护进程即可。以下是 Ubuntu 和 Debian 中 `swat` 行的目示例：

```
swat stream tcp nowait.400 root /usr/sbin/tcpd /usr/sbin/swat
```

当 SWAT 服务准备好被激活后，重启 `inetd` 守护进程使其重新读取 `inetd.conf` 文件。在 Debian 中执行此操作，以 root 用户身份输入以下命令：

```
# /etc/init.d/inetd restart
```

`inetd.script` 和 `xinetd` 服务是 Linux 中启动 SWAT 服务的两种方式。因此，如果你使用的是 Fedora 或 Debian 以外的 Linux 发行版，请在 `/etc/inetd.conf` 文件或 `/etc/xinetd.d` 目录（Fedora 中自动使用）查找你的 SWAT 服务所在位置。

完成此步骤后，一个守护进程将会在你的网络接口上监听连接到你 SWAT 服务的请求。你现在可以使用下一节描述的 SWAT 程序来配置 Samba。

## 开始使用 SWAT

你可以通过在本地浏览器中输入以下 URL 来运行 SWAT 程序：

```
http://localhost:901/
```
