
## 第 6 课 后续

在本课中，您学习了 Linux 打印服务。您配置了本地和远程打印机，使用各种打印机命令打印文件，并管理打印作业和队列。现在，您将能够设置打印机连接并打印文件的备份记录。

- **管理打印队列有什么好处？**
  *答案因情况而异，但可能包括：打印队列允许用户优先处理文件的打印，并自定义待打印文件的顺序。这有助于更快地打印那些急需打印的文件。*

- **本地打印机和网络打印机有什么区别？**
  *答案因情况而异，但可能包括：本地打印机只能从连接到它的单个系统访问，而网络打印机由打印服务器管理，可以被网络上的许多系统访问。*

## 软件包管理

课程时长：2 小时

### 学习目标：

在本课中，您将学习管理软件包。

您将：

- 使用 RPM 包管理器管理软件包。
- 验证软件包。
- 升级和刷新软件包。
- 配置软件仓库。
- 使用 YUM 包管理器安装软件包。
- 使用 Debian 包管理器管理软件包。
- 处理源文件。

### 介绍

您已探索了基本的 Linux 环境，操作了文件并进行了打印。现在，您已准备好在系统上安装软件。软件包促进了软件的运行。在本课中，您将管理软件包。

您需要有效地执行所需任务，因此必须在系统上安装软件。为此，您需要了解软件包、包管理器以及如何将它们安装到系统上。除非软件包完全安装，否则软件将无法运行。

本课涵盖以下 CompTIA Linux+ (2009) 认证目标的全部或部分：

- 主题 A
  - 目标 1.8
- 主题 B
  - 目标 1.8
- 主题 C
  - 目标 1.8
- 主题 D
  - 目标 1.8
- 主题 E
  - 目标 1.8
- 主题 F
  - 目标 1.8
- 主题 G
  - 目标 1.8

## 主题 A
### 使用 RPM 管理软件包

在系统上安装软件将增强计算机的功能，并使您能够更快地完成任务。在安装软件之前，您需要了解如何管理软件包。在本主题中，您将使用 RPM 包管理器管理软件包。

作为一名 Linux+ 专业人员，您需要安装系统上的软件。软件是一组软件包。只有当您知道如何在系统上添加这些软件包时，才能安装软件。即使只有一个软件包未正确安装，软件也无法工作。包管理器促进了这些软件包的安装。因此，有必要了解软件包和包管理器。

### 软件包

**定义：**

一个*软件包*是可以作为单个单元导入的类、函数或过程集合。软件包包括运行应用程序所需的所有文件。每个软件包都是针对特定的 Linux 发行版和系统类型专门编译的。根据使用的不同，存在许多类型的软件包。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_272_0.png)

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_272_1.png)

**图 7-1**：Linux 系统中的软件包。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_273_0.png)

### 包管理器

**定义：**
包管理器是一种工具，允许您搜索软件包并升级或移除它们。它跟踪随每个软件包提供的文件。包管理器还提供查询选项，以列出已安装的软件包及其特性。包管理器遵循的软件包文件命名约定是 name-version-release.architecture.rpm。RPM 包管理器和 YUM (Yellow dog Updater, Modified) 包管理器是包管理器的示例。

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_273_1.png)

### 记录已安装软件包的变更

建议您记录对已安装软件包所做的任何更改。这将有助于您排除故障并跟踪先前安装的版本。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_273_2.png)

### 依赖项

依赖项是指目标软件包实现其功能所依赖的软件包。依赖链可以延续很多层级。例如，只有在安装软件包 B 之后才会安装软件包 A。同样，只有在安装软件包 C 之后才会安装软件包 B。安装五个具有各自依赖项的软件包可能是一项繁琐的任务。包管理器可以自动获取所需的软件包，从而节省时间和精力。RPM 拥有诸如 up2date 和 yum 等互补实用工具来管理依赖项。依赖项管理是包管理器的主要功能之一。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_274_0.png)

图 7-3：由于依赖项软件包不可用，软件包安装失败。

### RPM 包管理器

RPM 包管理器（RPM）由 Red Hat 开发，是一种用于维护软件包的工具。

通过提供标准的软件打包格式，RPM 便于 Linux 系统和服务器管理和维护。RPM 提供标准的安装机制、关于已安装软件包的信息以及卸载和升级现有软件包的方法。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_274_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_274_2.png)

图 7-4：显示 rpm 工具的各种选项。

### RPMS 目录

Red Hat 发行版包含一个 RPMS 目录，其中存放着软件包。您还可以在互联网和 FTP 站点找到软件包。您可以在 **http://rpmfind.net** 网站找到软件包。

### 安装软件包

安装 Linux 时，您可以安装随附的所有软件包。然而，最好只安装您需要的软件包。稍后，当您还需要安装额外的软件包时，您可以使用 CD（或您使用的任何源）来获取额外的软件包。您可以检查是否已发布软件包的新版本，并安装最新版本。

### /usr/lib/rpm/ 目录

*/usr/lib/rpm/* 目录包含管理 RPM 软件包所需的 RPM 工具。*/var/lib/rpm/* 目录包含已安装软件包的 RPM 数据库。默认情况下，rpmrc 文件（全局 RPM 配置文件）位于 */usr/lib/rpm* 目录中。rpmrc 文件包含 RPM 架构兼容性的信息。如果您希望 RPM 设置适用于系统范围的配置，请将 rpmrc 文件放在 /etc 目录中。如果将 rpmrc 文件作为 .rpmrc 放在任何用户的主目录中，那么 rpm 设置将仅适用于该特定用户。

### RPM 命令

![](img/477ccb2f05b6ba1b2d563ea74f18c197_275_0.png)

常见的 RPM 包管理命令使您可以执行包管理任务。

常用的 RPM 包管理命令在下表中给出。

| 命令 | 允许您 |
| :--- | :--- |
| `rpm -i {RPM 软件包_文件}` | 安装软件包。 |
| `rpm -F {RPM 软件包_文件}` | 重新安装软件包。 |
| `rpm -U {RPM 软件包_文件}` | 升级软件包。 |
| `rpm -e {RPM 软件包_名称}` | 移除软件包。 |

### RPM 组件

RPM 包管理器包含许多组件。使用这些组件，您可以维护系统上已安装软件包的列表。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_276_0.png)

| 组件 | 描述 |
| :--- | :--- |
| RPM 本地数据库 | 跟踪系统上已安装的软件包。 |
| RPM 软件包 | 包含安装软件包所需的大量可执行文件和脚本。 |
| YUM | 充当 RPM 的前端软件包安装器。 |
| RPM 软件包文件 | 包含软件包的源代码。 |

### RPM 查询

RPM 查询是一个用于查询 RPM 关于已安装和未安装软件包信息的函数。`rpm -q` 命令有各种选项，它们提供不同的输出。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_276_1.png)

```text
[root@localhost ~]# rpm -qi samba
Name        : samba
Version     : 3.0.33
Release     : 3.7.el5
Install Date: Thu 25 Jun 2009 11:37:44 AM EDT
Group       : System Environment/Daemons
Size        : 31830025
Signature   : DSA/SHA1, Mon 15 Dec 2008 06:05:28 PM EST, Key ID 53266010137017180
Packager    : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
URL         : http://www.samba.org/
Summary     : The Samba SMB server.
Description :
Samba is the suite of programs by which a lot of PC-related machines
share files, printers, and other information (such as lists of
available files and printers). The Windows NT, OS/2, and Linux
operating systems support this natively, and add-ons packages can
enable the same thing for DOS, Windows, WWS, UNIX of all kinds, MVS,
and more. This package provides an SMB server that can be used to
provide network services to SMB (sometimes called "Lan Manager")
clients. Samba uses NetBIOS over TCP/IP (NetBI) protocols and does NOT
Relocations: (not relocatable)
Vendor: Red Hat, Inc.
Build Date: Tue 09 Dec 2008 11:03:42
Build Host: hs20-bcl-7.build.
redhat.com
License: GNU GPL Version 2
```

*图 7-5：使用 rpm 查询获得的 samba 软件包基本详细信息。*

RPM 查询命令的选项如下列出。

| 选项 | 允许您 |
| :--- | :--- |
| `rpm -qa` | 列出系统上已安装的所有软件包。 |
| `rpm -qc 软件包_名称` | 列出指定软件包的配置文件。 |
| `rpm -qi 软件包_名称` | 提供软件包的基本详细信息，例如安装日期、大小和摘要。 |

