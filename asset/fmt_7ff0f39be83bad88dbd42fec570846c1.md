
虽然在 `Domino Server` 上使用备份软件进行备份是可能的，但主要的缺点是您必须在备份期间关闭 `Domino`。如果你不需要不间断运行，可以考虑使用某种第三方备份产品之一。

适用于 `Linux` 操作系统的备用第三方备份方案包括：

- `IBM Tivoli Storage Manager`

`IBM Tivoli Storage Manager` 是一种用于备份任何数据的可扩展客户端/服务器软件。服务器软件和客户端软件均适用于 `Linux` 平台。通过管理客户端，你可以轻松地检索和访问已备份的数据。

要了解更多关于该软件及其可用性的信息，请访问 `IBM Tivoli` 网站：`http://www.ibm.com/tivoli`

- `VERITAS NetBackup BusinessServer`

`NetBackup 4.5` 也是一种客户端/服务器软件。客户端和服务器均适用于 `Red Hat`；`SuSE` 仅支持客户端。

访问 `VERITAS` 网站了解更多关于该软件的信息：`http://www.veritas.com`

- `BrightStor ARCserve for Linux`

`CA` 专门为 `Linux` 创建了备份软件。它具有基于 `Web` 的用户界面，内置了病毒扫描器，并提供灾难恢复服务。根据 `CA` 网站，该产品的当前版本 `BrightStor ARCserve Backup for Linux 7 Advanced Edition` 支持 `Red Hat Linux 6.x`、`7.0`、`7.1` 以及 `SuSE 7.2` 和 `7.3`：

`http://www.ca.com`

- `Galaxy ImageDataAgent for RedHat Linux`

这是由 `Commvault` 提供的适用于 `RedHat Linux` 的备份软件。访问以下地址查看更多信息：

`http://www.commvault.com`

### 适用于 Linux 版 Domino Server 的备份软件

由于大多数 `Domino` 服务器预计要提供不间断的服务，因此你不能关闭服务器来执行备份。唯一的选择是执行在线备份。这是可能的，因为 `Domino 备份/恢复 API`，并且有利用这些 `API` 的第三方产品，为执行 `Domino` 服务器的在线备份提供了可能。

### Lotus Notes 的 NetWorker 模块

在编写时，我们只知道一种适用于 `Linux` 版 `Domino` 的备份产品：由 `Legato` 提供的 `NetWorker Module for Lotus for Linux`。你可以在 `Legato` 网站找到详细信息：

```
http://www.legato.com
```

在编写时，`Legato` 软件仅适用于旧版本的 `Linux` 发行版和旧版本的 `Domino for Linux`。对于 `Linux`，支持的平台有：

- `RedHat 6.1, 6.2, 7.0, 7.1`
- `SuSE 6.4, 7.0, 7.1`

支持的 `Domino` 版本为：

- `Domino Server 5.04` 或 `5.06`

`NetWorker` 提供的关键功能包括：

- 在线、非中断性备份
- 全量或增量备份
- 文档级备份和恢复（阶段 2）
- 点还原和定向（到另一个目录）恢复
- 自动库库支持
- 介质管理（磁带跟踪、标记和条形码支持）
- 通过电子邮件和日志文件通知用户
- 图形调度界面
- `Notes` 备份与文件系统备份的无缝集成，用于企业级存储管理
- 本地或远程备份与恢复
- 可选的数据压缩和加密

> 注意：请检查 `Legato` 网站获取更新版本。

### 其他解决方案

第三方供应商为 `Domino` 服务器提供了许多备份产品，但在本文编写时，它们不支持 `Linux` 操作系统。

此处列出了某些产品；请检查它们的网站以查看是否已添加支持：

- `IBM Tivoli Storage Manager for Mail`（原名为 `IBM Tivoli Data Protection for Lotus Domino`）

```
http://www.ibm.com/tivoli
```

- `VERITAS Netbackup`

`http://www.veritas.com`

- `CA Brightstar`

`http://www.ca.com`

- `Commvault Galaxy for Notes R5`

`http://www.commvault.com`

## 从 Windows 版 Domino 迁移到 Linux 版 Domino

本附录描述了如何从 `Windows Intel` 平台上的 `Domino Server` 迁移到 `Linux Intel` 上的 `Domino Server`。

### 从 Windows 迁移到 Linux

在这种场景下，我们假设你正在使用两台物理机器，一台运行当前的 `Domino` 服务器，另一台用于新的 `Domino for Linux` 服务器。

### 升级当前服务器

应首先将当前的 `Windows` 服务器升级到你将在 `Domino for Linux` 服务器上运行的 `Domino` 版本。

### 构建 Linux 版 Domino

按照本红皮书所述构建 `Domino for Linux` 服务器。将服务器添加到现有的 `Domino` 域，并复制从当前服务器的所有数据。

### 从 Windows NT 或 Windows 2000 迁移你的应用程序

如果你的应用程序现在在运行 `Windows NT` 或 `Windows 2000` 的 `Domino` 服务器上运行，它们在 `Domino for Linux` 服务器上也能正常工作。

`Domino` 数据库与平台无关的，这意味着你可以从 `NT` 复制文件到 `UNIX`，并在不对文件格式进行任何更改的情况下打开数据库。然而，由于环境差异，有几点需要注意。

为了确保你的应用程序兼容性，请考虑以下问题：

- 你的应用程序是“自包含的”吗？
- 你是否使用了 `CASE`（计算机辅助工程）工具？
- 它是否使用了操作系统特性？

#### 你的应用程序是“自包含的”吗？

自包含应用程序完全运行在 `Domino` 服务器内部，不进行外部调用，也不导入或导出数据。显式引用文件例如 `c:\domino\data\NAMES.NSF` 在 `Linux` 上无法运行，需要替换为 `/domino/data/names.nsf`。`Linux` 对大小敏感，当使用外部脚本、链接或热点时，大小写也会成为一个问题。

#### 你使用了 CASE 工具？

`CASE` 工具可能有用，但许多工具是为非 `UNIX` 操作系统创建的，它们的输出代码可能与 `Linux` 不兼容。在使用这些工具之前，务必向制造商确认兼容性。

#### 你的应用程序使用了操作系统特性？

应用程序中任何特定平台的特性在 `Linux` 环境中可能失败。特定的 `NT` 服务、用于用户注册的 `NT Registry`、`Active-X` 控制以及依赖特定库来编译应用程序的编译器在应用程序移动到 `Linux` 时会产生问题。

#### 将应用程序移动到 Linux 服务器

从 `Windows NT` 或 `Windows 2000` 将文件传输到 `UNIX` 有许多方法。`FTP`、通过 `CDRW`、`Iomega` 磁带或其他介质以及 `PCNFS` 都是获取数据的好方法。在示例中，我们使用了 `FTP`，因为它是领域内常用的工具。

由于 `FTP` 服务器在 `UNIX` 侧默认安装，而在 `NT` 端没有，因此通常从 `NT` 端开启 `FTP` 会话并连接到 `UNIX` 端更为方便。这里我们使用的是 `NT 4.0`。

1. 从 `NT` 框，通过选择“开始 -> 程序 -> `MSDOS`”使用 `MSDOS` 命令提示符。

   a. 使用命令切换目录到服务器数据目录：

   ```
   cd \Lotus\notes\data
   ```

   b. 使用命令启动 `FTP` 会话：

   ```
   ftp servername
   ```

2. 在 `UNIX` 框使用命令切换目录到数据目录：

   ```
   cd /local/notes/data
   ```

3. 通过发布命令切换到二进制传输模式：

   ```
   bin
   ```

4. 使用命令传输数据库：

   ```
   put names.nsf
   ```

   或者使用通配符配合 `mput` 命令一次传输多个文件：

   ```
   mput *.nsf
   ```

`重要：` 在 `Domino` 服务器运行期间，切勿在操作系统（`OS`）层级添加或删除数据库。`Domino` 会缓存数据目录的列表，如果您在服务器运行时修改了数据目录，可能会发生不可预知的行为。这可能导致服务器崩溃或挂起。

## 确保权限正确

传输完成后，请确保 `UNIX` 机器上的权限正确。登录到 `UNIX` 机器并切换到数据目录（`cd /local/nodesata`），并使用以下命令检查传输文件的权限：

```
ls -l *.nsf
```

权限行的示例为：

```
-rw-rwx 1 nadmsup notes 1589248 Feb 22 09:34 log.nsf
```

按如下方式解释此记录：
