
## MySQL 工具

MySQL 提供了多种工具（如表 29-6 所示），包括服务器、客户端和管理工具。可以使用 `mysqldump` 命令处理备份。`mysqlshow` 命令将使用 SQL 命令 `SELECT *` 显示数据库，而 `mysqldimport` 可以导入文本文件，类似于 `LOAD INFILE`。

| 命令 | 描述 |
| --- | --- |
| mysqld | MySQL 服务器 |
| mysql | MySQL 客户端 |
| mysqladmin | 创建和管理数据库 |
| mysqldump | 数据库备份 |
| mysqldimport | 导入文本文件 |
| mysqlshow | 显示数据库 |

表 29-6 MySQL 命令

# 第 29 章：打印、新闻和数据库服务 675

## 使用 mysql 和 mysqladmin 管理 MySQL

要管理你的 MySQL 数据库，你使用 root 用户身份运行 `mysql`。`mysql` 客户端会启动 MySQL 监器。作为 root 用户，你可以输入管理命令来创建数据库和数据库表，或者删除条目，并执行显示数据等标准客户端任务。

以 root 用户身份登录并打开终端窗口。然后输入 `mysql` 命令。这将启动一个带有 `mysql>` 提示符的 MySQL 监器 shell。请确保你的命令以分号结束；否则，监器将提供一个缩进的箭头提示符等待添加参数。在监器中，结束命令的是分号而不是回车键。

```
mysql -u root -p

mysql>
```

如果你设置了 MySQL root 用户，可以使用 `-u root` 配合 `-p` 选项，如下所示。系统将提示你输入密码。

```
mysql -u root -p
```

一旦 `mysql` 客户端启动，你可以使用 `status` 命令检查服务器状态，并使用 `show databases` 列出当前数据库：

```
mysql status;

mysql show databases;
```

最初，MySQL 会为其自身管理设置并显示两个数据库：`mysql` 和 `test`。`mysql` 数据库存储了 MySQL 用户信息，`test` 数据库用于测试服务器。

## PostgreSQL

PostgreSQL 基于 POSTGRES 数据库管理系统，尽管它使用 SQL 作为查询语言。POSTGRES 是在加利福尼亚大学伯尔克利分校开发的下一代原型。你可以在 `www.postgresql.org` 网站上了解更多关于 PostgreSQL 的信息。PostgreSQL 是一个根据 GPL 许可证开发的开源项目。

PostgreSQL 常用于为高需求的 Internet Web 服务器提供数据库支持。通过几个命令，你可以创建关系数据库表。使用 `createuser` 命令创建一个 PostgreSQL 用户，可以使用该用户登录服务器。然后可以使用 `createddb` 命令创建数据库，并使用 `create table` 指令构建关系表。通过 `insert` 命令，你可以添加记录并使用 `select` 命令查看它们。远程用户对服务器的访问由 PostgreSQL 目录下的 `pg_hba.conf` 文件控制。

**注意** 搜索和索引服务器 `htiddig` 允许对 Web 和 FTP 站点进行文档搜索（`http://htiddig.org`）。通过它，你可以索引文档并执行复杂的搜索请求。

# 第 30 章

## 共享资源：Samba 和 NFS

Linux 提供了若干工具用于访问连接到网络的远程文件。网络文件系统（NFS）允许你连接并直接访问...（注：原文在此部分包含重复/乱码片段；根据指令保留提供的内容）。

## 第 30 章：共享资源：Samba 和 NFS 679

| 应用 | 描述 |
|--- | :--- |
| system-config-samba | Ubuntu Samba 管理工具，用于 GNOME GUI 配置 smb.conf |
| SWAT | Samba Web 管理工具，通过 Web 浏览器配置 smb.conf |
| smbd | Samba 服务器守护进程，为 SMB 客户端提供文件和打印机服务 |
| nmbd | Samba 守护进程，提供 NetBIOS 名称解析和服务浏览支持 |
| winbind | 使用 Windows 域提供的身份验证服务 |
| smbclient | 为 Linux 客户端对 Samba 服务提供类似 FTP 的访问 |
| mount.cifs | 在 Linux 客户端上挂载 Samba 共享目录（用于带有 -t cifs 选项的 mount 命令） |
| smbpasswd | 更改 Samba 服务器上的 SMB 加密密码 |
| smbtatus | 显示 SMB 网络连接当前状态 |
| smbrun | smbd 与外部程序之间的接口程序 |
| testpart | 测试 Samba 配置文件 smb.conf |
| smbtar | 直接将 SMB/CIFS 共享资源备份到 Unix 磁带机 |
| nmblookup | 将 Windows PC 的 NetBIOS 名称映射到其 IP 地址 |
| /etc/init.d/samba | 用于启动、停止和重启 Samba 服务器的 Samba 初始化脚本 |

**表 30-2** Samba 应用

通过 Linux 访问 Samba 服务。`mount.cifs` 和 `umount.cifs` 允许 Linux 客户端挂载和卸载 Samba 共享目录（使用带有 `-t samba` 选项的 `mount` 实用程序）。`smbtatus` 显示 SMB 服务器的当前状态以及是否正在被使用。你使用 `testpart` 来测试你的 Samba 配置。`smbtar` 是一个 shell 脚本，可直接将 SMB/CIFS 共享资源备份到 Unix 磁带驱动器。你使用 `nmblookup` 将 Windows PC 的 NetBIOS 名称映射到其 IP 地址。Ubuntu 默认的 Samba way配置工具是 `system-config-samba`，它允许你使用 GUI 创建并维护 Samba 配置文件 `/etc/samba/smb.conf`。或者，你也可以使用 Web 管理工具 (`SWAT`) 来配置 Samba。配置文件保存在 `/etc/samba` 目录中。

Samba 为文件和打印机服务、身份验证与授权、名称解析以及服务公告提供了四种服务。SMB 守护进程 `smbd` 提供文件和打印机服务，以及这些服务的身份验证和授权。这意味着网络上的用户可以共享文件和打印机。你可以通过要求用户提供密码来访问这些服务。当用户尝试访问共享目录时，系统会提示密码。控制可以在共享模式（share mode）或用户模式（user mode）下实现。共享模式为共享资源设置一个密码，然后允许任何拥有密码的用户访问。用户模式则为每个用户提供不同的密码。为了此目的，Samba 维护了自己的密码文件：`/etc/samba/smbpasswd`。

名称解析和服务公告由 `nmbd` 服务器处理。名称解析本质上是将 NetBIOS 名称解析为 IP 地址。服务公告（也称为浏览）是网络上可用服务的列表，连接的 Windows PC（以及通过 Samba 连接的 Linux PC）已知这些服务。

Samba 还包含了 `winbind` 守护进程，它允许 Samba 服务器使用 Windows 域提供的身份验证服务。与其让 Samba 服务器维护自己的用户列表来允许访问，它可以使用 Windows 域身份验证服务来验证用户。

## 启动 Samba

为了允许访问 Linux 系统并反之亦然，请使用 Samba 服务器。首先确保已安装 Samba 以及 `system-config-samba` 或 `SWAT` 工具。打开 Synaptic 软件包管理器，对 `samba` 并进行搜索。确保同时安装了 `samba` 和 `system-config-samba` 包。

> 注意：可以使用 GNOME 的 `nautilus-share` 和 `shares-admin`（第 4 章）设置 Samba 共享目录。然而，该工具不提供用户级安全防护，该功能现已被废弃。它为任何用户提供非常基础的共享访问权限。

安装完成后，Samba 通常配置为自动启动。你可以使用 GNOME 服务管理器（系统 | 管理 | 服务）开启或关闭此选项。确保勾选了带有 Samba 名称的 Windows 文件条目以启动 Samba。

对于简单设置，你可以使用 Ubuntu 版本的 `system-config-samba` 或 `SWAT` 来配置 `/etc/samba/smb.conf` 文件。如果你进行了更改，必须重启 Samba 服务器才能使更改生效。要使用新配置重启，请使用带有 `restart` 选项的 `samba` 初始化脚本 `/etc/init.d/samba`。`start`、`stop` 和 `restart` 选项将分别启动、停止和重启服务器。在终端运行以下命令来重启 Samba：

```
sudo /etc/init.d/samba restart
```

> 提示：Samba 服务器需要运行 `nmbd` 和 `smbd` 两个服务器。没有 `nmbd` 服务器，Windows 将无法检测到你的 Samba 服务器。这两个都由 `samba` 初始化脚本 `/etc/init.d/samba` 启动。

## 防火墙访问

`iptables` 防火墙阻止从 Linux 桌面浏览 Samba 和 Windows 共享。要绕过此限制，请确保防火墙将 Samba 视为信任服务。要允许防火墙访问 Samba 端口（通常为端口 137-139 和 445），对于 Firewalld，在 Policy 面板上选择 Inbound（入站）菜单，然后右键点击 Services 添加规则。添加新的入站绑定规则，在 Name 弹出菜单中选择 Samba (SMB)，系统将为你选中 137–139 和 445 端口。

## 使用配置工具设置 Samba

要设置 Linux 系统，可以使用 Ubuntu 上的 `system-config-samba` 工具配置 `/etc/samba/smb.conf` 文件。

1. 通过选择系统 | 管理 | Samba 打开 `system-config-samba` 工具。
2. 然后选择偏好 | 服务器设置。
3. 在 Basic 选项卡上，输入你的 Windows 工作组名称（见图 30-2）。Windows 给出的默认名为 WORKHOME 或 WORKGROUP。使用已赋予你的 Windows 网络名称。对于家庭网络，确保所有计算机使用相同的名称。
4. 在 Security 选项卡上，你可以选择所需的身份验证类型。默认选择了 User。你也可以使用 share 或 server；这些更开放，但在后期版本中可能删除。

### 用户

对于身份验证，你需要将 Windows 用户与特定的 Linux 用户关联。在偏好窗口中选择 Samba Users。然后选择一个 Linux 用户。如果你想添加新的 Samba 用户，选择 Add User。
你应该编辑选定的用户，输入相应的 Windows 用户以及用户用于访问 Linux 的密码。这就是用户的 Samba 密码。Samba 维护一组供访问 Samba 共享的用户密码。当 Windows 用户想要访问 Samba 共享时，需要输入密码。

### 共享

要设置一个简单的共享，在偏好窗口中点击 Add Share，这将打开 Create Samba Share 窗口（见图 30-3）。在 Basic 选项卡上，选择要共享的 Linux 目录（点击 Browse 查找），然后指定其是否可写且可见。
在 Access 选项卡上，你可以选择将共享开放给所有人或针对特定用户。你的新共享将显示在 Samba 服务器配置窗口中。

## SWAT

`SWAT` 是一种基于网络的 Samba 配置工具，通过 Web 页面界面允许你配置 `smb.conf` 文件。确保你已从 Ubuntu 主仓库安装了 `swat` 包。`SWAT` 是配置 Samba 服务器的一种简便方法，提供了

## 第 30 章：共享资源：Samba 和 NFS

图 30-3
新的 Samba，
基本选项卡

![](img/adea7e6d6a518dc3f4c5cea295c9d747_713_0.png)

完整的配置选项。`SWAT` 提供了一个易于使用的 Web 界面，带有按钮、菜单和用于输入值的文本框。顶部简单的按钮栏允许您选择想要配置的部分。密码部分也可以添加按钮栏。点击 View（查看）可以查看 `SWAT` 变化时 `smb.conf` 的内容。初始页面（HOME）显示 Samba 文档的索引。`SWAT` 最用的功能之一是它的上下文相关帮助。对于 `SWAT` 显示的每个参数和选项，您都可以点击 Help（帮助）来显示该操作的详细说明和示例。

### 激活 SWAT

`SWAT` 作为简单的软件包安装在 inetd/Ubuntu 的 xinetd 服务上。您还必须安装 `inetld` 软件包来运行 `SWAT`。如果你已经安装了 xinetd（xinetd 的增强版本），则会移除 xinetd 以允许 inetd 运行。作为 inetd 服务，它将列在 `/etc/services` 和 `/etc/inetd.conf` 文件中。`SWAT` 程序使用端口 901，该端口在 `/etc/services` 文件中指定并此处所示：

```
swat 901/tcp # Samba Web 管理工具
```

在使用 `SWAT` 之前，请备份您的 `smb.conf` 文件。`SWAT` 会覆盖原始文件，并用一个更短、更简洁的版本来替换它。原始安装的 `smb.conf` 列出了大量的选项并附有详细的说明。这是一个很好的学习工具，并提供了创建各种类型打印机和目录部分的极佳示例。只需创建一个备份副本：

```
cp /etc/samba/smb.conf /etc/samba/smb.bk
```

### 访问 SWAT

您可以通过打开浏览器并输入 IP 地址 127.0.0.1 以及端口 901 来启动 `SWAT`：

```
http://127.0.0.1:901
```

与其使用 127.0.0.1，您可以使用 localhost：

```
http://localhost:901
```

您可以在 Web 浏览器中输入运行 `SWAT` 的 Samba 服务器地址及其端口（901），从远程位置启动 `SWAT`。要配置 Samba，您需要输入您的用户名和密码。只有赋予了管理权限的用户才能获得访问。

## 第八部分：本地服务

`SWAT` 页面带有一个按钮栏，其中包含 HOME、GLOBALS、SHARES、PRINTERS、WIZARD、STATUS、VIEW 和 PASSWORD 页面的链接按钮（见表 30-3）。您可以使用 STATUS 页面列出您的 SMB 网络连接。对于不同的部分，`SWAT` 可以显示基本版本或高级版本。当您完成某个部分的工作时，点击该页面上的 Commit Changes（提交更改）以保存您的更改。对于您操作的每个独立页面，点击 GLOBALS 页面的 Commit Changes 会生成新版本的 `smb.conf` 文件。要让 Samba 服务器读取这些更改，您必须重启它。您可以通过点击 Status 页面上的 Restart SMB（重启 SMB）按钮来实现。

### 从 Windows 配置 Samba 访问

为 Windows 客户端设置连接，您需要指定 Windows 工作组名称并配置密码。工作组名称出现在 Windows 2000、NT 和 XP 的“我的网络位置”中（或早期版本中“网络邻域”下的“整个网络”）。在 Vista 上，它简单称为“网络”。要在 Windows XP 上设置工作组名称，打开控制面板并点击“系统”，在“计算机计算机”选项卡上点击“更改”按钮。这将打开一个带有工作组设置的对话框，您可以在此处输入工作组名称。默认值可能是 WORKGROUP 或 MSHOME。您可以设置自己的工作组名称，但所有计算机都将配置为使用该名称。

在您的 Ubuntu Samba 服务器上，您可以在 `system-config-samba` 的服务器设置中指定网络名称。或者，您也可以在 `smb.conf` 文件中手动输入网络名称，在全局部分的 `workgroup=` 条目中指定工作组名称。工作组名称应大大写且不包含空格。Windows XP 系统使用的默认名称是简单的 WORKGROUP。此时 `smb.conf` 的 `workgroup` 条目看起来如下：

```
workgroup = WORKGROUP
```
