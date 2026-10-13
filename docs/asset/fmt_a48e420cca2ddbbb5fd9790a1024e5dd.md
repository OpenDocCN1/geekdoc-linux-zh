
要为所有其他用户永久更改显示管理器，请编辑或创建 `/etc/sysconfig/desktop` 文件并定义变量 `DISPLAYMANAGER`。有效值包括 `GNOME`、`KDE` 和 `XDM`。例如，若要将其设置为 `KDE`，请执行以下操作：

```bash
# vi /etc/sysconfig/desktop
DISPLAYMANAGER=KDE
```

当 X 重启时，它将使用 `/etc/X11/predm` 文件并检查 `/etc/sysconfig/desktop` 文件中的 `DISPLAYMANAGER` 指令，然后启动定义的显示管理器。

## 配置用户默认桌面

使用 `switchdesk` 命令或其 GUI 版本 `switchdesk-gui`（桌面切换工具）来设置默认桌面。你需要加载 `switchdesk` 软件包才能使其生效，因为该包默认情况下是不安装的。请使用第 11 章“软件包管理”中概述的适当软件包安装方法。假设你当前正在运行 `KDE`，以下是切换到 `GNOME` 的方法：

```bash
$ switchdesk gnome
Red Hat Linux switchdesk 4.0
Copyright (C) 1999-2004 Red Hat, Inc
Redistributable under the terms of the GNU General Public License
Desktop now set up to run GNOME.
```

此命令会在你的主目录下创建两个文件——`Clients` 和 `.Clients-default`，在后续登录时，该桌面被定义为默认。系统上的每个用户都可以运行此命令并为自己设置不同的窗口管理器。如果你想切换到替代桌面管理器（如 `KDE`），请编辑 `.Clients-default` 文件并将 `WM` 指令值修改为 `KDE`，然后注销并登录。

通过菜单执行此操作，请选择 (GNOME) 系统 -> 偏选项 -> 更多选项 -> 桌面切换工具，或 (KDE) 主菜单 -> 设置 -> 桌面设置。

## 配置系统级默认桌面管理器

要为新用户设置默认桌面管理器，请编辑或创建 `/etc/sysconfig/desktop` 文件并定义变量 `DESKTOP`。有效值包括 `GNOME` 和 `KDE`。例如，若要将其设置为 `GNOME`，请执行以下操作：

```bash
# vi /etc/sysconfig/desktop
DESKTOP=GNOME
```

## 远程运行 X

如你所知，X 是一种客户端/服务器应用程序，能够在环境中运行。这允许你在无需连接到系统控制台的情况下，在远程 RHEL 系统或你的桌面电脑上运行图形化管理工具。以下是如何从 `rhel01` 在 `rhel02` 上启动 X 会话的方法。此过程假设你的系统中已运行了 X。

- 1. 确保 `rhel02` 上的 `ssh` 守护正在运行：

```bash
# ps -ef | grep sshd | grep -v grep
root 4545 1 0 09:17? 00:00:00 /usr/sbin/sshd
```

- 2. 在 `rhel01` 上，打开一个 `xterm` 并在命令行提示符处运行该函数以 `root` 身份在 `rhel02` 上启动 X 会话：

```bash
# ssh -X root@rhel02
```

- 3. 如果提示设置加密密钥，请确认是。

- 4. 输入 `root` 密码进行登录。

- 5. 运行图形化应用程序，例如 `system-config-display` 或 `system-config-selinux`。显示将出现在 `rhel01` 上。

如果发生任何问题，请切换到虚拟控制并登录。检查 `~/.session-errors`、`/var/log/messages` 和 `/var/log/Xorg.0.log` 文件中的错误日志、X 服务器的状态以及 `DISPLAY` 变量的设置（本地为 `DISPLAY=localhost:0.0` 或 `DISPLAY=:0.0`）。

## 总结

本章详细介绍了 X Window 系统和图形桌面管理器。你概述了 X 系统、X 服务器以及相关的配置文件。介绍了如何配置 X 服务器。

接下来，你学习了如何管理 X 服务器的启动和停止。学习了 X 应用程序和图形桌面管理器。最后，你了解如何配置默认桌面管理器以及通过网络运行 X 客户端应用程序。

## 软件包管理

本章涵盖了以下主要主题：

- 软件包依赖
- 软件包数据库
- 软件包概述
- 软件包命名规范
- 软件包仓库
- 软件包仓库
- Red Hat Network (RHN)
- RHN 注册

以下是注册系统的步骤：

- 1. 在 X 终端窗口的命令行提示符运行 `rhn_register`，或者选择 (GNOME) 应用 / (KDE) 主菜单 -> 系统工具 -> 软件更新器。将出现如图 11-1 所示的“欢迎使用 Red Hat 更新代理”屏幕。点击下一步 (Forward)。

![](img/3f35ec29a294974bc1a4fdae3ae46652_219_0.png)

图11-1 RHN 注册 – 欢迎界面

- 2. 在后续屏幕上，如果您已经注册过，请输入用户名和密码；否则选择第二个选项“我没有 Red Hat 登录账号。我创建一个”，如图 11-2 所示，并点击下一步 (Forward)。

![](img/3f35ec29a294974bc1a4fdae3ae46652_219_1.png)

图 11-2 RHN 注册 – 登录界面

- 3. 按照图 11-3 所示填写表单并点击下一步 (Forward)。

## 创建登录账号

创建 Red Hat 登录账号可以让您访问订阅中包含的更新、源代码和管理工具。您还可以使用您的账户与我们就订阅服务和软件进行通信。

- Red Hat 登录

![](img/3f35ec29a294974bc1a4fdae3ae46652_220_0.png)

图 11-3 RHN 注册 – 用户账户创建

如果您已经订阅，请输入订阅编号或选择“使用我现有的、的订阅”。选择“发送基本硬件信息”和“发送包列表”，以允许 RHN 检查您的系统硬件类型是否需要软件和安全更新。在下方窗口中指定系统名称。完成后点击下一步 (Forward)。详见图 11-4。

![](img/3f35ec29a294974bc1a4fdae3ae46652_220_1.png)

图 11-4 RHN 注册 – 订阅激活

按照后续序列完成注册过程。

## 通过 RHN 管理软件

在创建用户账户并注册系统后，您可以登录 www.rhn.redhat.com 上的 Red Hat Network 网站远程管理系统，包括自动或手动在系统上安装、更新和删除包，以及查看待处理的操作，并执行其他管理任务。通过以下命令检查 `rhnsd` 守护进程在您的系统上运行：

```
# service rhnsd status
```

### 软件包管理

如果守护进程未运行，请执行以下步骤手动启动它，并确保它在每次系统重启时都会启动：

```
# service rhnsd start
# chkconfig rhnsd on
```

## 软件包管理工具

可以使用多个命令执行包管理功能。表 11-1 提供了列表及其简要描述。

| 命令 | 说明 |
| --- | --- |
| rpm | 安装、删除、更新和验证包。此命令不会自动满足包依赖。 |
| rpm2cpio | 提取包。 |
| rpmbuild | 根据自定义构建新的 RPM。 |
| rpmquery | 查询包。 |
| rpmverify | 验证包属性。 |
| yum | 包命令的前端。从一个或多个存储库安装、删除和更新包，并自动满足依赖。还允许搜索和列出包信息。支持通配符（globbing）。 |
| pup | 安装和更新包。 |
| pirat | 用于安装和更新包的图形化工具。 |

表 11-1 软件包管理命令

下面的章节介绍了如何使用表 11-1 列出的工具。

## 使用 rpm 管理包

本节讨论了使用 `rpm` 命令进行的包管理任务，包括列出、安装、升级、刷新、查询、删除、提取、验证和检查包。

在进入细节之前，让我们先看看表 11-2，它提供了常用 `rpm` 命令的选项列表。这些选项可以任一方式使用。

| 选项 | same |
| --- | --- |
| -a (--all) | 显示所有包。 |
| -c (--configfiles) | 显示配置文件。 |
| -d (--docfiles) | 显示文档文件。 |
| -e (--erase) | 删除包。 |
| -f (--file) | 显示有关指定文件的信息。 |
| -F (--freshen) | 升级现有包。必须存在旧版本才能进行升级。 |
| --force | 即使已存在相同版本也安装包。 |
| -h (--hash) | 显示包安装/升级的进度。 |
| -i (--info) | 显示包的基本信息。 |
| --import | 导入指定的公钥。 |
