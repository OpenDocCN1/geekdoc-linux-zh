
```
rights -f /var/nss/ifolder -r rwcemf trustee kthorn.slc.da.da-tree
```

# 为服务代理分配权限

可以由 OES NetWare 或 OES Linux 服务器托管的 Novell 服务通常使用 eDirectory 用户对象作为代理，用于访问访问托管该服务的平台的文件系统。这些 eDirectory 用户对象被称为服务代理（Service Agents）。

iFolder 是使用服务代理的一个良好示例。当 iFolder 由 OES Linux 服务器托管时，`novlif` 用户对象就是用于访问 Linux 文件系统并管理 iFolder 数据文件的代理。

`novlifdr` 属于 `ifdrwww` 组。`ifdrwww` 和 `novlifdr` 都启用了 LUM。

iFolder 设计为能够使用原生 Linux 文件系统或 NSS 卷来存储数据。如果在安装期间，您配置 iFolder 将数据存储在原生 Linux 中，iFolder 安装程序会自动将 `novlifdr` 和 `ifdrwww` 分配为该目录的所有者和组。

然而，如果您选择将 iFolder 数据存储在 NSS 卷上，必须手动将 `novlifdr` 分配为 NSS 卷的文件系统信任人，并赋予 `novlifdr` 所有文件系统权限。

例如，假设 NSS 卷 iFolder 配置为挂载在 `/var/nss/iffolder`，则执行此信任人分配的命令为：

```
rights -f /var/nss/iffolder -r all trustee novlifdr.slc
```

由于 NSS 文件系统权限与原生 Linux 文件系统权限不相关，因此为 NSS 卷分配什么所有者或组并不重要。在 NSS 卷上唯一重要的文件系统权限是通过通过 `rights` 工具分配的权限。

# 练习 5-2 在 DA1 Linux 服务器上安装和配置 NSS

现在您已经复习了 OES 文件系统、NCP 服务器和 NSS，准备好开始练习 5-2 了。

NCP 服务器和 SMS 备份服务默认在 Novell OES for Linux 安装中安装。然而，为了本次练习的目的，NCP 和 SMS 在安装时被取消勾选。

Novell OES for Linux 安装默认不安装 NSS。

当您在练习的 DA1 Linux 服务器上安装 NSS 时，也选择了 NCP 包进行安装。此外，当您安装 NSS 时，SMS 备份服务包会被为您选中，因为 NSS 依赖于 SMS。

请参阅《Integrating Open Enterprise Server for Linux 工作手册》第 5-17 页的练习 5-2：在 DA1 Linux 服务器上安装和配置 NSS。

## 目标 7 使用服务器合并工具迁移 NSS 卷

Novell OES Support Pack 2 提供了一个用于迁移 NSS 卷的工具。在开始开始迁移之前，您应该考虑以下内容：

- 满足系统和软件需求
- 理解 NetWare 到 Linux 的迁移问题
- 准备源和目标服务器
- 创建并运行合并项目

### 满足系统和软件需求

在执行合并项目时，Linux 目标服务器必须安装并运行以下组件：

- Novell eDirectory
- Novell NCP Server（如果从 NetWare 源服务器复制数据）
- Novell Storage Services (NSS)（如果从 NetWare 源服务器复制数据）
- Novell User Management (LUM)

如果您从 NetWare 源服务器复制数据，必须在 Linux 目标服务器上创建并配置 NSS 卷。

### 理解 NetWare 到 Linux 的迁移问题

在运行服务器合并工具从 NetWare 服务器复制数据到 OES Linux 服务器之前，应该意识到以下问题：

- 打开的文件无法复制。服务器合并工具无法复制正在打开并使用的文件。

该规则有一个例外。NSS 有一个名为“写入复制”（Copy on Write）的功能。这允许对正在更改的文件进行访问。

该功能通过输入以下命令在 NSS 卷上启用：

```
nss /filewrite=volname
```
