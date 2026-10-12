
### 在 Debian 上安装 BIND

执行以下命令安装 `bind`：

```
debian:~# apt-get install bind
Reading Package Lists... Done
Building Dependency Tree... Done
The following NEW packages will be installed:
  bind
0 packages upgraded, 1 newly installed, 0 to remove and 1 not upgraded.
Need to get 571kB of archives. After unpacking 1323kB will be used.
Get:1 http://security.debian.org stable/updates/main bind
i:8.2.3-0_potato_1 [571kB]
Fetched 571kB in 10s (56.1kB/s)
Selecting previously deselected package bind.
(Reading database ... 9900 files and directories currently installed.)
Unpacking bind (from .../bind_1%3a8.2.3-0. potato.1_i386.deb)
Setting up bind (8.2.3-0.potato.1) ...

To be most effective, /etc/resolv.conf should list the IP address of your local machine (127.0.0.1) as a nameserver. It currently does not.

Would you like this to be added? [Y]
Starting domain name service: named.
```

### 在 Debian 上安装 DNS 工具

要使用 DNS 工具，你需要使用 `apt-get install dnsutils` 进行安装。

```
debian:~# apt-get install dnsutils
Reading Package Lists... Done
Building Dependency Tree... Done
The following NEW packages will be installed:
 dnsutils
0 packages upgraded, 1 newly installed, 0 to remove and 1 not upgraded.
Need to get 340kB of archives. After unpacking 778kB will be used.
Get:1 http://security.debian.org stable/updates/main dnsutils 1.8.2.3-0.potato.1 [340kB]
Fetched 340kB in 8s (38.0kB/s)
Selecting previously deselected package dnsutils.
(Reading database ... 9901 files and directories currently installed.)
Unpacking dnsutils (from .../dnsutils_1%3a8.2.3-0.potato.1_i386.deb) ...
Setting up dnsutils (8.2.3-0.potato.1) ...
```

### 在 Red Hat 系统上安装 BIND

要在 `Red Hat` 系统上安装 `BIND`，请遵循以下步骤。

1. 从 `Red Hat` 的 FTP 站点下载 `bind-8.2.2_P5-25.i386.rpm`、`caching-nameserver-7.0-6.noarch.rpm` 和 `bind-utils-8.2.2_P5-25.i386.rpm` 文件。

```
ftp> get bind-8.2.2_P5-25.i386.rpm
local: bind-8.2.2_P5-25.i386.rpm remote: bind-8.2.2_P5-25.i386.rpm
227 Entering Passive Mode (216,148,218,192,144,191).
150 Opening BINARY mode data connection for bind-8.2.2_P5-25.i386.rpm (1748960 bytes).
226 Transfer complete.
1748960 bytes received in 29.9 secs (57 Kbytes/sec)
ftp> get bind-utils-8.2.2_P5-25.i386.rpm
local: bind-utils-8.2.2_P5-25.i386.rpm remote: bind-utils-8.2.2_P5-25.i386.rpm
227 Entering Passive Mode (216,148,218,192,229,109)
150 Opening BINARY mode data connection for bind-utils-8.2.2_P5-25.i386.rpm (738549 bytes).
226 Transfer complete.
738549 bytes received in 12.1 secs (59 Kbytes/sec)
ftp> get caching-nameserver-7.0-6.noarch.rpm
local: caching-nameserver-7.0-6.noarch.rpm remote: caching-nameserver-7.0-6.noarch.rpm
227 Entering Passive Mode (216.148.218.192.117.151).
150 Opening BINARY mode data connection for caching-nameserver-7.0-6.noarch.rpm (5810 bytes).
226 Transfer complete.
5810 bytes received in 0.0976 secs (58 Kbytes/sec)
```

2. 安装新下载的 RPM 文件。`bind-utils` 软件包可能已经安装。也可以通过 `rpm` 进行检查。

```
[root@rh7 bind]# rpm -q bind-utils
bind-utils-8.2.2_P5-25
[root@rh7 bind]# rpm -qvh *.rpm
bind
###############################################
caching-nameserver
###############################################
```

3. 将 `/etc/resolv.conf` 中的 `nameserver` 条目更改为 `127.0.0.1`，使其使用新安装的本地名称服务器。

```
search the-nashes.net
nameserver 127.0.0.1
```

4. 运行 `/etc/init.d` 目录中的 `named` 脚本来启动 `named`。

```
[root@rh7 /root]# /etc/init.d/named start
Starting named:                                   [  OK  ]
```

### 配置路径与测试

`Debian` 将其 `BIND` 配置存储在 `/etc/bind` 中，而 `Red Hat` 将其 `named.conf` 存储在 `/etc` 中，其他文件存储在 `/var/named` 中。最后一步是通过解析名称来测试新安装的 DNS 服务器。例如：

```
debian:~# host www.hungryminds.com
www.hungryminds.com        A   38.170.216.15
debian:~# host www.linux.com
www.linux.com        CNAME   linux.com
linux.com        A   216.136.171.205
```

### 实验 16-2 NFS 服务器

本实验配置 NFS 服务器以导出一个目录。本实验适用于一台或两台工作站，因为你可以连接到本地共享的 NFS 导出。

要在 `Debian` 系统上安装 NFS 服务器，请以 `root` 身份登录并遵循以下步骤：

1. 通过运行 `apt-get update` 确保软件包列表已更新。
