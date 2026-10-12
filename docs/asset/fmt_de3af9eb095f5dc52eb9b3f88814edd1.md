
表 16-12 描述了此命令使用的选项。

## 表 16-12 `repquota` 命令的选项

| 选项 | 描述 |
| --- | --- |
| `-a` | 显示 `/etc/fstab` 文件中指定的所有文件系统的磁盘信息 |
| `-v` | 列出所有磁盘配额的信息 |
| `-t` | 截断超过九字符的用户名和组名 |
| `-n` | 跳过将用户和组 ID 解析为用户名和组名以加速显示 |
| `-s` | 以更易读的格式显示磁盘信息 |
| `-u` | 仅报告基于用户的磁盘配额 |
| `-g` | 仅报告基于组的磁盘配额 |
| `-F fmt` | 以指定的格式显示磁盘信息，包括 `vfsold` (version 1), `vf` (version 1) |

## 章节总结

- `X Window` 系统提供了一种编写与设备无关的图形窗口系统的方法，该系统可以轻松从一台计算机传输到另一台计算机。它的开发是为了释放 `Linux` 的图形能力，并提供一种用于创建和操作屏幕图形元素的协议。通过该系统，你可以同时运行多个图形应用程序。

- 最常见的开源 `X Window` 版本是 `XFree86` 和 `X.Org`（包含在 `openSUSE` 中）。`openSUSE` 使用 `GUI` 模块来配置 `X Window`。在更改配置后，你需要重启 `X Window`。

- 使用 `xdpyinfo` 命令显示有关 `X` 服务器的信息。使用 `startx` 命令从命令行启动 `X Window`。

- `X` 显示器管理器提供了一个图形化登录界面，在允许访问 `openSUSE Linux` 桌面之前提示你输入用户名和密码。此外，它允许你为 `X` 窗口系统选择不同的桌面。

- 启动 `Linux` 系统后 `X` 显示器管理器显示的方式取决于运行级别（`runlevel`）。运行级别定义为 `/etc/init` 文件中的系统状态项。

- `su`、`kdesu` 和 `sudo` 命令用于管理 `root` 账户。`su` 命令将用户凭据更改为 `root` 用户或由用户名指定的的用户。`kdesu` 是 `KDE` 中的 `GUI` 程序，允许你以 `root` 权限运行应用程序。系统管理员可以使用 `sudo` 命令允许一组用户以 `root` 或另一个用户的身份运行某些命令，同时记录这些命令及其参数。

- 磁盘配额（`Disk quotas`）用于指定分配给每个用户的最大磁盘空间。磁盘配额有两种：硬限制（`hard limits`）和软限制（`soft limits`）。硬限制是不灵活的，用于设置一个无法超过的特定限制；软限制是灵活的，允许用户在指定时间内超过限制。

- `/etc/fstab` 文件中的 `uquota` 和 `grquota` 用于启用用户和组的磁盘配额。`quotache` 命令用于扫描文件系统并为每个启用配额的文件系统构建当前使用表。`edquota` 命令用于编辑用户配额。`repquota` 命令显示指定文件系统的磁盘使用和配额摘要。

## 关键术语

`disk quotas`（磁盘配额）`Linux` 特性，用于指定分配给每个用户的最大磁盘空间。
`hard limits`（硬限制）不灵活的磁盘配额，不允许用户超过指定的限制。
`refresh rate`（刷新率）每秒刷新显示的次数。
`soft limits`（软限制）灵活的磁盘配额设置，当用户接近硬限制时会发出警告。**另参** `hard limits`。

`X Window System`（`X Window` 系统）提供了一种编写与设备无关的图形窗口软件的方法，该系统可以轻松从一台计算机传输到另一台计算机。

# 复习习题

1. 使用哪个 `Linux` 命令为系统上的每个用户设置配额？
   a. `edquota`
   b. `quotacheck`
   c. `repquota`
   d. `quotaon`

2. 使用哪个 `Linux` 命令启用磁盘配额？
   a. `edquota`
   b. `quotacheck`
   c. `repquota`
   d. `quotaon`

3. 你刚刚修改了 `/etc/fstab` 文件以添加配额选项，并需要为用户创建配额文件。你使用哪个 `Linux` 命令扫描已启用配额的文件系统并构建当前使用表？
   a. `edquota`
   b. `quotacheck`
   c. `repquota`
   d. `quotaon`

4. 使用哪个 `Linux` 命令来显示指定文件系统的磁盘使用摘要以及配额？
   a. `edquota`
   b. `quotacheck`
   c. `repquota`
   d. `quotaon`

5. 如果你在使用 `KDE` 并在使用 `GUI` 时需要临时 `root` 权限，你使用哪个命令？
   a. `su`
   b. `kdesu`
   c. `sudo`
   d. `sudo -user`

6. 使用哪个 `Linux` 命令将你的用户凭据更改为 `root` 用户的凭据？
   a. `su`
   b. `kdesu`
   c. `sudo`
   d. `sudo -user`

7. 你是一名 `Linux` 管理员，需要允许一组用户以 `root` 用户身份运行某些命令。你使用哪个命令？
   a. `su`
   b. `kdesu`
   c. `sudo`
   d. `sudo-user`

8. 使用哪个命令从终端窗口启动 `X Window` 会话？
   a. `xvidtune`
   b. `xdpyinfo`
   c. `startx`
   d. `quotaon`

9. 如果你打开了一个 `X Window` 会话并需要查看显示信息，你使用哪个命令？
   a. `xvidtune`
   b. `xdpyinfo`
   c. `startx`
   d. `quotaon`

10. 如果你打开了一个 `X Window` 会话并需要调整视频设置，你使用哪个命令？
    a. `xvidtune`
    b. `xdpyinfo`
    c. `startx`
    d. `quotaon`

11. 哪个运行级别（也称为 `halt`）关闭 `Linux` 机器？
    a. `5`
    b. `3`
    c. `1`
    d. `0`

12. 哪个运行级别（也称为单用户模式）与 `Windows` 中的安全模式相当？
    a. `5`
    b. `3`
    c. `1`
    d. `0`

13. 哪个运行级别（也称为 `X11`）让你访问所有服务（包括 `GUI`）？
   a. `5`
   b. `3`
   c. `1`
   d. `0`

14. 下面是广泛使用的 `X Window` 版本？（选择所有项）。
   a. `GNOME`
   b. `FreeBSD86`
   c. `KDE`
   d. `X.Org`

15. 给 `/etc/fstab` 文件的内容，哪些文件系统启用了磁盘配额？（选择所有项）。

```
/dev/sda swap swap defaults 0 0
/dev/sda2 / ext4 acl,user_xattr,usrquota,grpquota 1 1
/dev/sda3 /home ext4 acl,user_xattr,usrquota,grpquota 1 1
proc /proc proc defaults 0 0
sysfs /sys sysfs noauto 0 0
```

   a. `/dev/sda2`
   b. `/dev/sda1`
   c. `/dev/sda3`
   d. `/sys`

16. 关于配额的下列哪些描述正确？（选择所有项）。
   a. 硬限制无法超过。
   b. 默认情况下，用户可以超过硬限制。
   c. 默认情况下，用户可以超过软限制。
   d. 管理员使用配额限制磁盘空间。
   e. `NIS` 环境用于磁盘配额。
   f. 设置软限制和硬限制。

## 案例项目

### 案例项目 16-1：比较桌面环境和窗口管理器

### 案例项目 16-2：使用配额

### 网络信息服务

# 353

`NIS` 服务器
- 客户端请求
- 经网络传输
- 请求
- 服务端 `RPC`
- 客户端 `RPC`
- 对客户端请求的响应
- 经网络传输
- 请求结果
- `NIS` 客户端
- 数据库访问
- 查询结果

`![](img/b8a4c65ba2acb99909d8842055c0bdd7_374_0.png)`

**图 17-1** `NIS` 与 `RPC` 的通信

© `Cengage Learning` 2013

（在此情况下为 `portmapper`）。尝试访问 `RPC` 服务的客户端会首先连接端口映射器（`portmapper`），它返回 `RPC` 服务可以的端口号。

## 安装和配置 `NIS` 服务器

要安装 `NIS`，你需要同时拥有 `NIS` 服务器和客户端。在安装 `NIS` 之前，请决定该计算机将用作主服务器、从服务器还是客户端。如果 `Linux` 网络上已经安装了 `NIS` 服务器（主服务器或从服务器），你只需要安装 `NIS` 客户端。相反，如果网络上没有 `NIS` 服务器，你还需要安装服务器以及客户端。如果你为系统配置了 `NIS` 服务器或客户端，你必须为计算机提供一个域名，以确保同一域内的客户端和服务器可以相互通信。客户端无法访问不同域的服务器。

## 创建 `NIS` 域

要创建一个 `NIS` 域，请确定哪些 `Linux` 计算机将成为该域的一部分，并使用 `domainname` 命令为它们指定 `NIS` 域名。设置域名时，必须从 `root` 用户账户执行此命令。普通用户可以使用不带参数的此命令来显示域名。例如，`domainname example` 将域名设置为 `example`。然而，此命令不会永久保存 `Linux` 计算机的域名。重启计算机时，域名将会丢失。要永久保存 `NIS` 域名，请编辑运行脚本 `/etc/init.d/network`，并在脚本中指定 `NIS` 域名，如在脚本中添加的这一行所示：

```
# Set the NIS domain name
domainname example
```

`nisdomain` 和 `ypdomain` 命令的值可以通过 `domainname` 命令进行更改。`NIS` 曾经被称为“黄页”（`Yellow Pages`），某些命令中的“`yp`”就源于此。

`![](img/b8a4c65ba2acb99909d8842055c0bdd7_374_1.png)`

## 安装 `NIS` 主服务器

`NIS` 主服务器包含域内所有 `NIS` 映射的源文件。如果你想对 `NIS` 映射进行任何更改，必须在 `NIS` 主服务器上进行。该服务器为客户端提供其请求的信息，并为从服务器提供最新的映射副本。`openSUSE` 默认提供 `NIS` 客户端；但是，你需要安装 `NIS` 服务器。从 `root` 用户账户，使用 `yast2 -i yast2-nis-server` 命令下载并安装 `nis-server` `RPM` 软件包及其依赖项。

### 在 `YaST` 中配置 `NIS` 主服务器

要启动 `YaST NIS` 服务器模块，请使用 `yast2 nis-server` 命令。图 17-2 显示了打开的窗口。

`![](img/b8a4c65ba2acb99909d8842055c0bdd7_375_0.png)`

图 17-2 网络信息服务 (`NIS`) 服务器设置窗口
来源：`openSUSE`

此窗口显示 `NIS` 服务器的当前状态。如你所示，`NIS` 软件已安装，但服务器尚未配置。选择“`Create NIS Master Server`”（创建 `NIS` 主服务器）选项，然后点击“`Next`”（下一步）进入图 17-3 所示的窗口。

你可以在此窗口中配置以下设置：

- 如果尚未设置，请设置 `NIS` 域名。
- 配置 `NIS` 服务器兼任 `NIS` 客户端，以便用户可以访问 `NIS` 服务器的数据。
- 选择“`Active Slave NIS server exists`”（存在激活的 `NIS` 从服务器）选项，以便 `NIS` 主服务器能与网络中的 `NIS` 从服务器协作。
- 选择“`Fast Map distribution`”（快速映射分布）选项可以加速从主服务器到从服务器的映射传输。

### 主服务器设置 - `YaST`（超级用户权限）

`![](img/b8a4c65ba2acb99909d8842055c0bdd7_376_0.png)`

`NIS` 域名
- 也是 `NIS` 客户端
- 激活的 `NIS` 服务器授权
- 快速映射分布周期
更改密码
- 允许更改 (`i`) `GECOS` 信息
- 允许更改 (`i`) 登录 `shell`
- 在防火墙中打开端口：防火墙状态
防火墙已禁用

图 17-3 主服务器设置窗口

- “`Allow changes to passwords`”选项允许用户通过 `ypppasswd` 命令更改密码。通过选择此选项，“`Allow changes to GECOS field`”和“`Allow to login shell`”选项将被启用。`GECOS` 字段允许用户使用 `ypchfn` 命令更改其名称和地址设置，登录 `shell` 选项允许他们使用 `ypchsh` 命令更改默认 `shell`。

- 勾选“`Open Port in Firewall`”复选框以配置防火墙设置。点击“`Other global settings`”按钮允许用户更改 `NIS` 的源目录并定义可用的最小用户和组 ID（`UID` 和 `GID` 默认设置为 `500`）。在 `Linux` 发行版中，`500` 及以上的 `UID` 和 `GID` 分配给用户账户；低于 `500` 的保留给系统账户。`merge passwords` 默认开启，并应保持开启。此设置根据 `/etc/passwd`、`/etc/shadow` 和 `/etc/group` 认证文件创建用户数据库。

> 如果用户想要切换到另一个 `shell`，则该 `shell` 必须在 `/etc/shells` 文件中。

`![](img/b8a4c65ba2acb99909d8842055c0bdd7_376_1.png)`

如果你选择“`Active Slave NIS server exists`”选项，你看到的下一个窗口是 `NIS Master Slave Servers Setup`（见图 17-4）。只需添加主机名称即可来配置 `NIS` 从服务器。

# 356 第 17 章 `Linux` 环境下的网络

`![](img/b8a4c65ba2acb99909d8842055c0bdd7_377_0.png)`

**图 17-4** `NIS` 主服务器从服务器设置窗口
来源：`openSUSE`

如果你没有选择从服务器选项，你看到的下一个窗口是 `NIS Maps Setup`（见图 17-5）。默认映射对于大多数网络都是

`![](img/b8a4c65ba2acb99909d8842055c0bdd7_377_1.png)`

图 17-5 `NIS` 映射设置
来源：`openSUSE`

如果你没有选择从服务器选项，你看到的下一个窗口是 `NIS Maps Setup`（见图 17-5）。默认映射对于大多数网络都是。

`![](img/b8a4c65ba2acb99909d8842055c0bdd7_378_0.png)`

图 17-6 `NIS` 服务器查询窗口
来源：`openSUSE`

### 手动配置 `NIS` 服务器

使用之前 17-6 所示的 `YaST` 模块配置 `NIS` 服务器非常简单。在安装 `NIS` 服务器和客户端后，会创建 `/var/py` 目录。例如，在 `NIS` 域 `example.com` 中，有一个目录 `/var/py/example.com`，其中包含 `NIS` 映射的数据库。系统管理员应检查此目录下的 `NIS` 配置文件：

- `/var/py/Makefile`——你可以使用 `make` 命令运行此文件，该命令可以在 `/var/py` 目录下执行。它用于将更新的映射推送到 `NIS` 服务器。
- `/var/py/secclients`——此文件指定 `NIS` 客户端对 `NIS` 服务器的访问权限。你可以在此文件中输入 `IP` 地址；不能输入主机名，例如。文件中的数据是在 `YaST NIS` 服务器模块的最后阶段填充的。
- `/var/py/index`——包含按哈希排序的索引。此文件具有 `.dir` 扩展名。
- `/var/py/data`——包含与键相关的实际数据。此文件具有 `.pag` 扩展名。

`openSUSE` 有几个默认映射。表 17-1 描述了一些：

| `NIS` 映射 | 说明 |
|---|---|
| `/etc/group` | 包含组信息，如组 ID |
| `/etc/passwd` | 包含用户属性，如用户 ID |
| `/etc/shadow` | 包含用户的加密密码 |
| `/etc/aliases` | 包含别名名称；用于邮件服务 |
| `/etc/hosts` | 包含计算机的主机名和地址 |
| `/etc/networks` | 包含网络名称 |
| `/etc/protocols` | 标识分配给协议名称和地址 |

`NIS` 服务器启动后，`NIS` 将数据导出到 `/var/py`。`/var/py` 下还会创建一个以域名命名的目录。例如，在 `NIS` 域 `example.com` 中，存在 `/var/py/example.com` 目录包含 `NIS` 映射的数据库。

`![](img/b8a4c65ba2acb99909d8842055c0bdd7_379_0.png)`

# 活动 17-1：安装和配置 `NIS` 服务器

所需时间：30 分钟

目标：在 `YaST` 中安装并配置 `NIS` 服务器。

要求：一个 `openSUSE` 虚拟机（`GOME` 或 `KDE`）和互联网连接
描述：在此活动中，你将安装 `YaST NIS` 服务器模块并使用它配置 `NIS` 服务器。

1. 启动 `VMware Player`，并登录 `openSUSE` 虚拟机。
2. 打开终端窗口，并切换到 `root` 用户。
3. 使用 `yast2 -i yast2-nis-server` 命令并按回车安装 `YaST NIS` 服务器模块。确保点击“同意”以确认所有软件包许可。
4. 在启动 `YaST NIS` 服务器模块之前，列出 `/var/py` 目录的内容，并注意该目录哪些文件。然后通过输入 `yast2 nis-server` 并按回车启动 `YaST NIS` 服务器模块。
5. 点击 `Install`（安装）并设置 `NIS Master Server` 选项按钮，然后点击 `Next`（下一步）。
6. 在 `NIS Domain` 框中输入 `example` 来设置 `NIS` 域名。勾选 `This host is also a NIS client` 复选框，将 `NIS` 服务器配置为 `NIS` 客户端。
7. 将没有 `NIS` 从属服务器，因此请确保 `Active NIS` 服务器存在，并且消选 `Fast Map distribution (rpc.pyxfrd)` 复选框。
8. 若要允许用户更改密码，勾选 `Allow changes to passwords` 复选框。然后勾选 `Allow changes to GECOS field` 和 `Allow changes to login` 复选框。
9. 通过勾选 `Open Port in Firewall` 复选框在你的防火墙中打开 `NIS` 端口，然后点击 `Next`（下一步）。
10. 在 `NIS Maps Setup` 窗口中，选中 `group`、`passwd`、`rpc` 和 `services` 复选框，然后点击 `Next`（下一步）。
11. 保留默认的网掩码 (`255.0.0.0`) 和网络 (`127.0.0.0`) 设置，然后点击 `Finish`（完成）。
12. 既然你已经安装并配置了 `NIS` 服务器，请列出 `/var/yp` 目录的内容，以查看 `NIS` 添加的新文件和目录。
13. 保持终端窗口打开并运行虚拟机，以便进行 Activity 17-2。

## 安装和配置 `NIS` 客户端

`YaST NIS` 模块随最新版本的 `openSUSE` 一起发布。要启动 `NIS` 客户端模块，请使用 `yast2 nis-client` 命令。图 17-7 显示了打开的窗口。

`![](img/b8a4c65ba2acb99909d8842055c0bdd7_380_0.png)`

图 17-7 配置 `NIS` 客户端

来源：`openSUSE`

# 第 17 章 `Linux` 环境中的网络

第一个任务是使用 `NIS` 选项按钮激活 `NIS`。接下来，你需要定义 `NIS` 策略以指定哪些 `NIS` 配置将被修改。默认情况下，它由 `netconfig` 脚本处理。此方法适用于大多数网络，但你可以通过选择这些选项之一来更改：

- `Only Manual Changes`（仅手动更改）——此选择确保 `netconfig` 脚本可以修改 `NIS` 配置。
- `Custom Policy`（自定义策略）——你使用此选项通过添加由分隔符的条目来自定义 `NIS` 策略。`netconfig` 中的条目由字段组成，例如指定网络 ID 和协议，如下例。要了解更多关于可能的值，请审阅 `netconfig` 页面。

```
