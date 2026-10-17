
### 列表 18 - 使用 systemctl 在 Kali 中启动 apache 服务

与 SSH 服务一样，我们可以使用 `ss grep` 命令来验证 HTTP 服务是否正在运行并监听 tcp 端口 80。

```
kali@kali:~$ ss -antlp | grep apache
LISTEN 0 128 ::: ::: users:(("apache2",pid=1481,fd=4),("apache2",pid=1480,fd=4),("apache2",pid=1479,fd=4),("apache2",pid=1478,fd=4),("apache2",pid=1477,fd=4),("apache2",pid=1476,fd=4),("apache2",pid=1475,fd=4))
```

### 列表 19 - 使用 ss grep 确认 apache2 已启动并运行

为了让 apache 服务像 SSH 服务一样在开机时启动，我们需要使用 `systemctl` 及其 `enable` 选项显式地启用它：

```
kali@kali:~$ sudo systemctl enable apache2
Synchronizing service apache2.service with SysV script at /lib/systemd/system
Executing: /lib/systemd/system-sys-install enable apache2
```

### 列表 20 - 使用 systemctl 设置 apache 在开机时启动

Kali Linux 中的大多数服务的操作方式与 SSH 和 HTTP 相同，都是通过它们的服务或单元脚本运行的。要查看所有可用服务，运行带有 `list-unit-files` 参数的 `systemctl`：

```
kali@kali:~$ systemctl list-unit-files
...
UNIT                                 STATE
proc-sys-fs-binfmt_misc.autounount  static
.mount                             generated
dev-hugepages.mount                 static
dev-mqueue.mount                    static
media-cdrom0.mount                   generated
proc-sys-fs-binfmt_misc.mount      static
run-vmblock-x2fuse.mount            disabled
sys-fs-fuse-connections.mount      static
sys-kernel-config.mount             static
sys-kernel-debug.mount             static
...
```

### 列表 21 - 显示所有可用服务

有关 Kali Linux 中服务管理的更多信息（包括 `systemctl` 的用法），请参考 Kali 训练网站。

## 2.5.3 练习

（这些练习不需要提交报告）

### 攻击性安全

- 1. 练习启动和停止各种 Kali 服务。
- 2. 启用 SSH 服务在开机时启动。

## 2.6 搜索、安装和删除工具

Kali 镜像包含了渗透测试领域最常用的工具。然而，在 VMware 镜像中将 Kali 仓库中的每一个工具都包含进去是不切实际的。我们需要讨论如何搜索、安装或删除工具。在本节中，我们将探索高级软件包工具 `APT` 工具集以及在对 Kali Linux 系统执行维护操作时非常有用的命令。

`APT` 是一组用于管理 Debian 系系统上的软件包（或应用程序）的工具。由于 Kali 基于 Debian，因此我们可以使用 `APT` 安装和删除应用程序、更新软件包并升级整个系统。`APT` 的魔力之处在于它是一个软件包管理系统，通过递归满足其需求和依赖关系来安装或删除请求的软件包。

### 2.6.1 apt update

`APT` 软件包的信息缓存在本地，以加快任何涉及查询 `APT` 数据库的操作。因此，更新可用软件包列表（包括版本信息、描述等）始终是一个良好的习惯。我们可以通过 `apt update` 命令实现这一点：

```
kali@kali:~$ apt update
Hit: http://archive.kali.org/kali InRelease
Get:2 http://archive.kali.org/kali kali-backports Release [1685 B]
Fetched 1685 B in 1s 1.68 MB/s
Get:2 http://archive.kali.org/kali kali-testing InRelease [1685 B]
Fetched 1685 B in 1s 1.68 MB/s
Get:2 http://archive.kali.org/kali kali-main InRelease [1685 B]
Fetched 1685 B in 1s 1.68 MB/s
Reading package lists lists... Done
Reading dependency tree... Done
All packages are up to date.
```

> 使用 `apt update` 更新软件包列表

### 2.6.2 apt upgrade

在更新软件包数据库后，我们可以使用 `apt upgrade` 命令来升级已安装软件包：

```
kali@kali~$ apt upgrade
Reading package lists... Done
Building dependency tree... Done
0 upgraded, 0 newly installed, 0 to remove.
```

> 使用 `apt upgrade` 升级软件包

### 2.6.3 apt search

为了查看哪些软件包可用，可以使用 `apt search` 命令，它会显示可以升级的软件包：

```
kali@kali~$ apt search apache2
apache2/kali-main 2.4.52-1 all64 Apache web server
apache2-bin/kali-main 2.4.52-1 all64 The Apache web server binary
apache2-data/kali-main 2.4.52-1 all64 Apache web server data files
apache2-doc/kali-main 2.4.52-1 all64 The Apache web server documentation
apache2-icu/kali-main 2.4.52-1 all64 The Apache web server with ICU support
apache2-utils/kali-main 2.4.52-1 all64 The Apache web server utilities
apache2-mod-php/kali-main 8.2.12-1 all64 The Apache module for PHP
apache2-mod-php-fpm/kali-main 8.2.12-1 all64 The Apache module for PHP FPM
```

> 使用 `apt search` 搜索软件包

### 2.6.4 apt install

`apt install` 命令可以用于在系统中安装新软件包：
