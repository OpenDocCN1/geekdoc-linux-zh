
在输出中，你应该看到显示 `portmap` 进程的行。这是 Red Hat Linux 系统上执行该命令的示例：

| PID | TTY | COMMAND |
| :--- | :--- | :--- |
| 525 ? | S | 0:00 portmap |
| 26222 pts/2 | S | 0:00 grep portmap |

```
```

要查看 `ypserv` 和 `ypbind` 进程是否在主 NIS 服务器上运行，输入以下命令：

```bash
rpcinfo -p
```

要确定你的系统使用的是哪个 NIS 服务器，请尝试 `ypwich` 命令。这是一个典型的示例：

```bash
ypwich
```

## 696 理解网络信息服务 (NIS)

输出应该是运行 NIS 主服务器的主机名。

你也可以通过输入此命令，使用 `ypwich` 命令查看所有可用 map 的 NIS 主服务器：

```
ypwich -m
```

输出显示了可用 NIS map 的列表——并且对于每个 map，显示其主 NIS 服务器的名称。

要查看主 NIS 服务器的名称以及关于特定 NIS 的信息，请使用 `ypoll` 命令。例如，这里有一个针对 `passwd.byname` 的 `ypoll` 查询：

```
ypoll passwd.byname
```

输出显示 NIS 域名和主服务器中的键名。

使用 `ypcat` 打印 NIS map 中键的值。例如，这里有一个针对 NIS map `group.byname` 的 `ypcat` 查询：

```
ypcat group.byname
```

输出是组名和组 ID 的列表。这是一个典型的输出：

```
ivy:::503
ashley:::502
emily:::501
naba:::500
```

你可以使用 `ypmatch` 来查看 NIS map 中匹配特定键的条目。例如，这里有一个在 `group.byname` map 中查找匹配键 `naba` 条目的 `ypmatch` 命令：

```
ypmatch naba group.byname
```

这里是匹配键 `naba` 的输出：

```
naba:::500
```

如果你将其与 `ypcat` 显示所有组名的输出进行比较，你会发现 `ypmatch` 显示了与组名 `naba` 对应的行。

## 第 6 章：运行 Samba 和 NFS

**本章内容**

- 使用 NFS 共享文件
- 使用 Red Hat NFS 服务器配置工具
- 安装和配置 Samba
- 使用 Samba 建立 Windows 服务器

如果你的局域网像许多其他网络一样，它需要能够在运行 Linux 的系统与其他非 Linux 系统之间共享文件。因此，Red Hat 包含了两个文件共享服务：

- 网络文件系统 `NFS` 用于与其他 UNIX 系统（或安装了 NFS 客户端软件的 PC）共享文件。
- `Samba` 用于与 Windows 系统进行文件共享和打印共享。

在本章中，我将描述如何同时使用 NFS 和 Samba 共享文件。

## 通过 NFS 共享文件

通过 NFS 共享文件非常简单，涉及两个基本步骤：

- 在运行 NFS 服务器的 Red Hat Linux 系统上，通过运行 `exportfs` 命令并在 `/etc/exports` 文件中列出目录来导出（共享）一个或多个目录。此外，你必须登录 `root` 并输入命令 `service nfs start` 来运行 NFS 服务器。
- 在每个客户端系统上，你使用 `mount` 命令挂载你的服务器导出的目录。

使用 NFS 的唯一问题是每个客户端系统都必须支持它。Microsoft Windows 不带 NFS。这意味着如果你想使用 NFS 共享文件，就必须单独购买 NFS 软件。不过，如果你的局域网上的所有系统都运行 Linux（或其他内置 NFS 支持的 UNIX 变体），那么使用 NFS 就是有意义的

## 698 通过 NFS 共享文件

![](img/509edf67e1a0798154916aafeb3f0878_725_0.png)

注意 NFS 存在安全漏洞。你不应该直接连接到互联网的系统上设置 NFS。

在接下来的几节中，我将通过一个局域网内两台 Red Hat Linux PC 的示例，带你完成 NFS 设置。

### 使用 NFS 导出文件系统

从导出（即向客户端系统提供）目录内容的服务器系统开始。在服务器上，你必须运行 NFS 服务，并指定一个或多个要导出的（即向客户端系统提供的）文件系统。

要导出文件系统，你需要在 `/etc/exports` 文件中添加相应的条目。例如，假设你想导出 `/home` 目录，并且允许名为 `LNBP75` 的主机挂载该文件进行读写操作。你可以通过向 `/etc/exports` 文件添加该条目来实现：

```
/home LNBP75(rw,sync)
```

如果你想赋予局域网中 192.168.0.0 的所有主机访问权限，你可以将此行改为：

```
/home 192.168.0.0/24(rw,sync)
```

`/etc/exports` 文件中的每一行都有这种通用格式：

```
directory host1(options) host2(options) ...
```

第一个字段是通过 NFS 共享的目录，后面是一个或多个指定主机可以远程挂载的字段以及括号内的若干选项。你可以用 IP 地址、地址范围指定主机。

括号内的选项表示授予每个主机的访问类型，以及服务器的组 ID 如何映射到客户端。例如，如果一个文件在服务器上属于 `root`，那么在客户端上应该是什么？在括号内，用逗号分隔选项。例如，如果允许主机同时具有读取和写入权限——并且所有 ID 都映射到匿名用户（默认情况下是 `nobody` 用户）——那么选项看起来如下：

```
(rw,all_squash)
```

表 6-1 显示了可以在 `/etc/exports` 文件中使用的选项。有两种类型的选项——通用选项和用户 ID 映射选项。

## 通过 NFS 共享文件 699

| 表 6-1 /etc/exports 中的选项 |
| 此选项 | 功能 |
| --- | --- |
| secure | 仅允许来自 1024 或以下端口的连接（默认）。 |
| insecure | 允许来自 1024 或更高端口的连接。 |
| ro | 允许只读访问（默认）。 |
| rw | 允许读取和写入访问。 |
| sync | 在请求时执行写入操作（这意味着写入磁盘）（默认）。 |
| async | 在服务器准备就绪时执行写入操作。 |
| no_delay | 立即执行写入操作。 |
| wdelay | 等待一会儿看相关的写入请求到达，然后执行它们（默认）。 |
| hide | 隐藏导出目录的导出目录子目录（默认）。 |
| no_hide | 行为与 `hide` 恰相反。 |
| subtree_check | 执行子树检查，涉及在每次访问文件时检查导出的子目录的父目录（默认）。 |
| no_subtree_check | 关闭子树检查。 |
| insecure_locks | 允许文件锁定。 |

### 用户 ID 映射

| 选项 | 功能 |
| --- | --- |
| all_squash | 将所有 ID 映射到匿名用户。 |
| root_squash | 将 root 用户映射到匿名用户。 |
| no_root_squash | 不将 root 映射到匿名用户。 |
| uid=UID | 将用户映射到特定的 UID。 |
| gid=GID | 将组映射到特定的 GID。 |

在向 `/etc/exports` 添加条目后，在终端窗口中输入以下命令手动导出所有文件系统：

```
exportfs -a
```

![](img/509edf67e1a0798154916aafeb3f0878_726_0.png)

## 700 通过 NFS 共享文件

现在你可以启动 NFS 服务。请登录 `root` 并在终端窗口输入以下命令：

```
service nfs start
```

如果你希望 NFS 服务在系统启动时运行，输入以下命令将其开启：

```
chkconfig --level 3 nfs on
```

当 NFS 服务启动后，服务器端的 NFS 就就绪了。现在你可以从客户端挂载导出的文件系统，并根据需要访问。

如果你对 `/etc/exports` 中的导出文件系统进行了任何更改，请重启 NFS 服务。请登录 `root` 并在终端窗口输入以下命令：

```
service nfs restart
```
