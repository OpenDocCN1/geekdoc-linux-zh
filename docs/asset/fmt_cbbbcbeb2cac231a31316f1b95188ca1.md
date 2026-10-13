
- 4. 给 `lidia` 设置密码。

```
passwd lidia
```

- 5. 按照顺序安装 NFS 和 `portmap` 软件包：

```
rpm -ivh /mnt/cdrom/RedHat/RPMS/portmap*
```

```
rpm -ivh /mnt/cdrom/RedHat/RPMS/knfs*
```

- 6. 启动 `portmap` 程序。

```
/etc/rc.d/init.d/portmap start
```

- 7. 启动 NFS 服务器。

```
/etc/rc.d/init.d/nfs start
```

- 8. 编辑 `/etc/exports` 文件包含以下行。该文件被 NFS 用于将系统导出到网络。在这种情况下，用户 `lidia` 被导出到本地网络——星号被用作通配符，且挂载将是可读可写的。

```
/home/lidia 192.168.1.*(rw)
```

有很多导出选项。最常用的是读/写 `rw` 和只读 `ro`。详细描述导出项已超出本书的范围。请查阅 `exports` 手页以获取更多信息。

- 9. 按照如下方式激活 NFS 导出。

```
exportfs -a
```

你可以使用 `exportfs` 的 `-u` 选项来导出 NFS 共享。例如，要导出 `lidia` 用户，使用命令 `exportfs -u /home/lidia`。所有的共享都可以通过 `exportfs -a` 命令导出。

- 10. 你可以通过运行不带任何选项的 `exportfs` 来检查你刚刚创建的导出。你应该能看到以下输出。

- 11. 接下来，挂载主目录。

```
mount chivas:/home/lidia /mnt
```

- 12. 运行 `df` 命令查看你的新挂载。

| Filesystem | 1k-blocks | Used | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | 54416 | 33367 | 18240 | 65% | |
| /dev/hda8 | 995115 | 317206 | 626503 | 34% | /home |
| /dev/hda7 | 1856990 | 13857 | 174147 | 1% | /opt |
| /dev/hda5 | 1011928 | 611008 | 349516 | 64% | /usr |
| /dev/hda6 | 1856990 | 176081 | 158423 | 10% | /usr/local |
| /dev/hda9 | 202220 | 9965 | 181815 | 5% | /var |
| chivas:/home/lidia | 995115 | 317206 | 626503 | 34% | /mnt |

你已经有了一个 NFS 服务器。目前它是一个自给自足的服务器，下一步是让它更有用。下一节描述了在你的 Linux 节点配置 NFS 客户端的过程。你可以通过运行 `/etc/rc.d/init.d/nfs stop` 脚本来停止所有 NFS 服务。

## 配置示例 NFS 客户端

本节描述了如何配置 Linux 节点作为 NFS 客户端。首先，你需要构建另一台 Linux 计算机。使用第 1 章中描述的过程构建一台红帽 Linux 计算机。本章的第一节“创建新的红帽 Linux 计算机”描述了你需要使用的网络参数。你需要先配置 NFS 服务器。该过程在上一节“配置你的 NFS 服务器”中已有描述。

以下指令描述了如何跨网络挂载 NFS 共享。

- 1. 以 `root` 身份登录到 `chivas`。
- 2. 挂载红帽发行版 CD-ROM。

```
mount -r -t iso9660 /dev/cdrom /mnt/cdrom
```

- 3. 安装 NFS 客户端软件包。

```
rpm -ivh /mnt/cdrom/RedHat/RPMS/knfs-clients
```

- 4. 挂载 `lidia` 用户。

```
mount chivas:/home/lidia /mnt
```

- 5. 运行 `df` 命令，你应该能看到新的挂载。

你现在可以从 `/mnt` 挂载点访问用户文件。然而，与 Samba 一样，Linux 文件权限优先于你通过 NFS 声明的权限。

## 创建简单的 NIS (yp) 服务器

一旦你在网络上使用超过两台 Linux（或 UNIX）计算机，管理用户及其文件的工作就会变得更加困难。当使用多一台计算机时，用户的生活也随会变得更加困难。一种解决方案是使用网络信息系统 `NIS`。

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_276_0.png)

请不要将 DNS 域名名与 NIS 域名名混淆。它们是不同的。NIS 域名名是你的网络名称。

## 引入 switch.conf

`/etc/switch.conf` 文件控制 NIS 如何运行以及何时使用它。它包含了服务列表以及配置的位置。例如，`passwd` 行在 2000 年之后才被使用。

`switch.conf` 控制的重要服务包括：

- 组名
- 自动挂载

NIS 使用域名的概念。域名名并不是网络名称；它指代映射的位置。随着 NIS 的增长，将映射合并到一个池中是一个问题。映射存储在 `/var/yp`。`ypserv` 守护进程会将这些映射分给所有的 NIS 客户端。

- 1. 以 `root` 身份登录到 `chivas`。
- 2. 挂载红帽 CD-ROM。

```
mount -r -t iso9660 /dev/cdrom /mnt/cdrom
```

- 3. 安装 NIS 软件包。

```
rpm -ivh /mnt/cdrom/RedHat/RPMS/yp*
```

- 3. 如果你还没有这样做，创建用户 `lidia`。这个示例用户将为本章中所有示例的测试提供平台。

```
useradd lidia
```

- 4. 给 `lidia` 设置密码。

```
passwd lidia
```

- 5. 你可以按照如下方式设置域名。

```
domainname tiburones
```

- 6. 确保 `portmap` 已经启动。

```
/etc/rc.d/init.d/portmap restart
```

- 7. 启动 NIS 服务器和客户端。

```
/etc/rc.d/init.d/ypserv start
```

- 8. 你需要创建 `/var/yp` 目录和 NIS 数据库以便服务器工作。运行以下命令。

```
/usr/lib/yp/ypinit -m
```

- 9. `yp` 会提示作为服务器的主机名。你正在工作的机器被用作默认，因此不需要输入任何主机名。按下 `Ctrl-D` 键然后按回车键完成该过程。数据库将被构建。

- 10. 启动 NIS 客户端。

```
/etc/rc.d/init.d/ypbind start
```

## 第三部分：扩展你的网络服务

11. NIS 现在已配置完成。你现在应该可以看到映射了。运行 `ypcat passwd` 命令，你应该能看到 `/etc/passwd` 文件的内容。

```
lidia:$1$V1Wbf0nkK$/r1KkG1ZE0:502::502::/nethome/lidia/:/bin/bash
```

12. 你可以从跟随它的服务器上测试你的 NIS 服务器。

```
su - lidia
```

13. 如果你运行 `whoami` 和 `pwd` 命令，你会发现你确实是以用户 `lidia` 的身份登录的，并且当前工作目录是 `/home/lidia`。

# 使用自动挂载 (automount)

`automount` 系统允许你从网络上的任何 Linux（或 UNIX）计算机访问资源，例如你的家目录。当与 NFS NIS 结合时，你可以使用 `automount` 指定在 Linux 计算机上自动挂载任何目录或文件系统。

# 在本地使用自动挂载

你需要告诉 `automount` 将使用哪个目录来挂载资源。例如，如果你想自动挂载家目录，通常的惯是使用 `/nethome` 目录。你声明为挂载点的任何目录将是虚拟的。也就是说，你不需要用 `mkdir` 命令物理地创建这样的目录。

你还需要给 `automount` 提供一个待挂载资源的映射（map）。映射包含待挂载资源的信息。例如，如果需要挂载用户的家目录，`automount` 必须知道该家目录的位置。映射可以是本地文件（多个）、NIS 数据库或一个命令。本地文件通常类似于 `/etc/auto.home`；NIS 映射将由 `ypserv` 和 `ybind` 分发并存在于内存中；程序映射将通过运行脚本或程序创建。

1. 以 `root` 身份登录 `chivas`。
2. 挂载 Red Hat CD-ROM。
3. 安装 `autofofs` (`automount`) 软件包。

```
mount /mnt/cdrom
```
