
包管理器是一种工具，允许您搜索软件包并升级或移除它们。它跟踪随每个软件包提供的文件。包管理器还提供查询选项，以列出已安装的软件包及其特性。包管理器遵循的软件包文件命名约定是 `name-version-release.architecture.rpm`。`RPM` 包管理器和 `YUM`（`Yellow dog Updater, Modified`）包管理器是包管理器的示例。

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_273_1.png)

### 记录已安装软件包的变更

建议您记录对已安装软件包所做的任何更改。这将有助于您排除故障并跟踪先前安装的版本。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_273_2.png)

### 依赖项

依赖项是指目标软件包实现其功能所依赖的软件包。依赖链可以延续很多层级。例如，只有在安装软件包 `B` 之后才会安装软件包 `A`。同样，只有在安装软件包 `C` 之后才会安装软件包 `B`。安装五个具有各自依赖项的软件包可能是一项繁琐的任务。包管理器可以自动获取所需的软件包，从而节省时间和精力。`RPM` 拥有诸如 `up2date` 和 `yum` 等互补实用工具来管理依赖项。依赖项管理是包管理器的主要功能之一。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_274_0.png)

图 7-3：由于依赖项软件包不可用，软件包安装失败。

### RPM 包管理器

`RPM` 包管理器（`RPM`）由 `Red Hat` 开发，是一种用于维护软件包的工具。

通过提供标准的软件打包格式，`RPM` 便于 `Linux` 系统和服务器管理和维护。`RPM` 提供标准的安装机制、关于已安装软件包的信息以及卸载和升级现有软件包的方法。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_274_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_274_2.png)

图 7-4：显示 `rpm` 工具的各种选项。

### RPMS 目录

`Red Hat` 发行版包含一个 `RPMS` 目录，其中存放着软件包。您还可以在互联网和 `FTP` 站点找到软件包。您可以在 `http://rpmfind.net` 网站找到软件包。

### 安装软件包

安装 `Linux` 时，您可以安装随附的所有软件包。然而，最好只安装您需要的软件包。稍后，当您还需要安装额外的软件包时，您可以使用 `CD`（或您使用的任何源）来获取额外的软件包。您可以检查是否已发布软件包的新版本，并安装最新版本。

### /usr/lib/rpm/ 目录

`/usr/lib/rpm/` 目录包含管理 `RPM` 软件包所需的 `RPM` 工具。`/var/lib/rpm/` 目录包含已安装软件包的 `RPM` 数据库。默认情况下，`rpmrc` 文件（全局 `RPM` 配置文件）位于 `/usr/lib/rpm` 目录中。`rpmrc` 文件包含 `RPM` 架构兼容性的信息。如果您希望 `RPM` 设置适用于系统范围的配置，请将 `rpmrc` 文件放在 `/etc` 目录中。如果将 `rpmrc` 文件作为 `.rpmrc` 放在任何用户的主目录中，那么 `rpm` 设置将仅适用于该特定用户。

### RPM 命令

![](img/477ccb2f05b6ba1b2d563ea74f18c197_275_0.png)

常见的 `RPM` 包管理命令使您可以执行包管理任务。

常用的 `RPM` 包管理命令在下表中给出。

| 命令 | 允许您 |
| :--- | :--- |
| `rpm -i {RPM 软件包_文件}` | 安装软件包。 |
| `rpm -F {RPM 软件包_文件}` | 重新安装软件包。 |
| `rpm -U {RPM 软件包_文件}` | 升级软件包。 |
| `rpm -e {RPM 软件包_名称}` | 移除软件包。 |

### RPM 组件

`RPM` 包管理器包含许多组件。使用这些组件，您可以维护系统上已安装软件包的列表。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_276_0.png)

| 组件 | 描述 |
| :--- | :--- |
| `RPM` 本地数据库 | 跟踪系统上已安装的软件包。 |
| `RPM` 软件包 | 包含安装软件包所需的大量可执行文件和脚本。 |
| `YUM` | 充当 `RPM` 的前端软件包安装器。 |
| `RPM` 软件包文件 | 包含软件包的源代码。 |

### RPM 查询

`RPM` 查询是一个用于查询 `RPM` 关于已安装和未安装软件包信息的函数。`rpm -q` 命令有各种选项，它们提供不同的输出。

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

图 7-5：使用 `rpm` 查询获得的 `samba` 软件包基本详细信息。

`RPM` 查询命令的选项如下列出。

| 选项 | 允许您 |
| :--- | :--- |
| `rpm -qa` | 列出系统上已安装的所有软件包。 |
| `rpm -qc 软件包_名称` | 列出指定软件包的配置文件。 |
| `rpm -qi 软件包_名称` | 提供软件包的基本详细信息，例如安装日期、大小和摘要。 |

| 选项 | 功能 |
| :--- | :--- |
| `rpm -ql package_name` | 列出包中的文件。 |
| `rpm -qR package_name` | 列出包的依赖项。 |
| `rpm -qa \| grep package_name` | 将 `rpm` 查询命令的结果传递给 `grep` 命令，以在结果中搜索特定包。 |

## 语法

`RPM` 查询的语法为 `rpm -q {what_packages} {what_information}`。

## 如何使用 RPM 管理软件包

### 操作参考：安装包

要安装包：

1. 下载你想要安装的 `rpm` 文件。
2. 使用 `rpm -ivh [file name.rpm]` 命令安装包。
3. 如有必要，下载依赖包。

### 操作参考：卸载包

要卸载包：

1. 使用 `rpm -qi [package_name]` 命令搜索你想要卸载的 `rpm` 包。
2. 使用 `rpm -e [package_name]` 命令卸载 `rpm` 包。

## 活动 7-1

## 使用 RPM 管理软件包

**数据文件：**

- `AdobeReader_enu-8.1.4-1.i486.rpm`

**开始之前：**

1. 在 `srvA` 上，你已以 `root` 身份登录到图形界面。
2. 在终端中，在 `/` 目录下创建一个名为 `rpms` 的目录。
3. 导航到 `/085039Data/Managing_Packages` 目录。将 `AdobeReader_enu-8.1.4-1.i486.rpm` 复制到 `/rpms` 目录。
4. 切换到 `/rpms` 目录。
5. 输入 `clear` 以清除终端。

**场景：**

你在 `Linux` 中有大量以电子书形式提供的文档。你需要安装 `Adobe Reader` 应用程序，以便用户能够在 `Linux` 中查看电子书。

| 你做什么 | 如何做 |
| :--- | :--- |
| **1. 安装并检查 AdobeReader 包的版本。** | a. 输入 `rpm -ivh AdobeReader_enu-8.1.4-1.i486.rpm` 以安装 `AdobeReader` 包。<br>b. 观察进度条处于 **100%**，表示包已成功安装。<br>c. 输入 `rpm -qi AdobeReader_enu` 以查看包的版本号。<br>d. 观察 `Version`（版本）为 `8.1.4`，`Release`（发行版）为 `1`。 |
| **2. 列出 AdobeReader 包中的文件。** | a. 输入 `rpm -ql AdobeReader_en` 以查看包中的文件列表。<br>b. 观察应用程序文件安装在 `/opt/Adobe/Reader8/bin` 目录中。<br>c. 输入 `clear` 以清除终端窗口。 |
| **3. 检查 AdobeReader 包中文件的状态。** | a. 输入 `rpm -qs AdobeReader_en` 以查看包中所有文件的状态。<br>b. 观察第一列显示所有文件的状态均为 `normal`，表示文件已正确安装。<br>c. 最小化 `root@srvA:/rpms` 窗口。<br>d. 在桌面上，双击 **Adobe Reader 8** 图标。<br>e. 在 **Adobe Reader - License Agreement** 对话框中，点击 **Accept** 以接受协议条款。<br>f. 观察 **Adobe Reader** 窗口已显示，表示应用程序已成功安装。<br>g. 关闭 **Adobe Reader** 窗口。<br>h. 恢复 `root@srvA:/rpms` 窗口。<br>i. 在 `root@srvA:/rpms` 窗口中，输入 `clear` 以清除屏幕。 |

## 主题 B

## 验证包

在上一主题中，你使用 `RPM` 包管理器管理软件包。作为 `Linux+` 系统管理员，你可能需要验证和修复损坏的包。在本主题中，你将验证包。

如果你知道如何验证包，在排查包安装和软件问题时将节省时间。你还应能够验证系统中已安装包的完整性。

### RPM 验证

`RPM` 验证将现有包与 `RPM` 包数据库进行比较，并返回缺失或损坏的包。各种选项允许你验证包中的特定信息。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_280_0.png)

图 7-6：使用 `RPM` 验证 `Samba` 包的状态。

`RPM` 验证选项列于下方。

| 选项 | 功能 |
| :--- | :--- |
| `rpm -Va` | 验证所有已安装的包。 |
| `rpm -V package name` | 验证特定包。 |
| `rpm -V (file name) (package_name)` | 验证包中的特定文件。 |

### 语法

`RPM` 验证的语法为 `rpm -V package_name`。

## 验证包的重要性

也可以通过 `RPM` 系统验证包的完整性。此验证过程可用于确保包文件存在于正确的目录中且未经修改，并具有适当的权限。更具体地说，`RPM` 检查包中每个文件的大小、`MD5` 校验和、权限、类型、所有者和组。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_281_0.png)

## 验证错误代码

如果包没有问题，不会显示任何消息，你将返回命令提示符。如果检测到问题，将显示一个八位字符字符串以提醒你发生了更改。根据此输出，你可以确定是否需要重新安装该包。验证错误代码列于下表。

| 错误代码 | 描述 |
| :--- | :--- |
| `c` | 配置文件错误。 |
| `S` | `MD5` 校验和测试失败。 |
| `S` | 安装后文件大小发生变化。 |
| `L` | 符号链接错误。 |
| `T` | 当前文件修改时间与原始文件修改时间不匹配。 |
| `D` | 设备属性错误。 |
| `U` | 用户设置与原始设置不同。 |
| `G` | 组设置与原始设置不同。 |
| `M` | 权限或文件类型模式不同。 |

## 如何验证包

### 操作参考：验证包

要验证包：

1. 以 `root` 身份登录。
2. 验证已安装的包。
   - 使用 `rpm -Va` 命令验证所有 `rpm` 包。
   - 使用 `rpm -Vv [package name]` 命令验证单个 `rpm` 包。
   - 使用 `rpm -V {file name} {package_name}` 命令验证包中的特定文件。

## 活动 7-2

## 验证包

### 开始之前：

1. 你已以 `root` 身份登录到图形界面。
2. 终端窗口已显示。

### 场景：

你的经理要求你将以前使用的 `DOS` 和 `Mac` 文件转换为 `UNIX` 格式，并确保客户能够访问 `Samba` 手册页。在确保应用程序已安装后，你决定验证包是否已准备就绪供使用。

| 你做什么 | 如何做 |
| :--- | :--- |
| 1. 检查是否已安装 dos2unix 和 samba-client 包。 | a. 输入 `rpm -q dos2unix` 以检查是否已安装 `dos2unix` 包。<br>b. 观察已安装 `dos2unix - 3.1 - 27.1` 包。<br>c. 输入 `rpm -q samba-client` 以检查是否已安装 `samba-client` 包。<br>d. 观察已安装 `samba - client - 3.0.33 - 3.7.el5` 包。 |
| 2. 验证 dos2unix 包。 | a. 输入 `rpm -Vv dos2unix`<br>b. 观察没有错误并显示六行内容。 |
| 3. 验证 samba-client 包。 | a. 输入 `rpm -Vv samba-client`<br>b. 观察没有错误，文件列表后跟随目录。<br>c. 输入 `rpm -Vv samba-client \| wc -1` 以统计行数。<br>d. 观察命令显示总共有 26 行。<br>e. 输入 `clear` 以清除终端屏幕。 |

## 主题 C

## 升级包

现在你已经了解了验证包的方法，你可以学习如何升级包。在本主题中，你将通过更新和刷新已安装的包来升级它们。

系统管理的一个方面是保持系统软件的最新状态。许多应用程序处于积极开发中，并且会定期发布新版本。这些新版本可能会添加功能、修复旧版本中的错误或提供重要的安全更新。`RPM` 能够快速轻松地升级软件包。这将避免你必须卸载并重新安装包以获得最新版本的情况。升级包使你能在最短时间内拥有应用程序的最新功能。

## 更新/刷新包

使用更新（`update`）或刷新（`freshen`）选项可以轻松地升级包。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_284_0.png)

| 选项 | 描述 |
| :--- | :--- |
| `Update`（更新） | 将包版本与已安装的包版本进行比较。如果找到该包，将更新该包。如果未找到该包，将安装该包。用于更新包的语法为 `rpm -U [file name].rpm`。 |
| `Freshen`（刷新） | 将包版本与已安装的包版本进行比较。如果找到该包，将更新该包。如果未找到该包，则不会安装该包。用于刷新包的语法为 `rpm -F [file name].rpm`。 |

## 刷新包

输入 `rpm -Fvh * .rpm` 会自动升级那些已经安装的包。

## 如何更新和刷新软件包

### 操作参考：更新软件包

要更新软件包：

1. 下载更新的软件包。
2. 使用 `rpm -Uvh [文件名.rpm]` 命令更新现有软件包。
3. 要验证软件包是否已更新，请使用 `rpm -qi [软件包名称]`。

## 活动 7-3

### 升级软件包

**数据文件：**

`AdobeRdr9.1.0-1_i486linux_enu.rpm`

**开始之前：**

1. 你已在图形界面中以 `root` 身份登录。
2. 导航至 `/085039Data/Managing_Packages` 目录。将 `AdobeRdr9.1.0-1_i486linux_enu.rpm` 复制到 `/rpms` 目录。
3. 输入 `clear` 以清除终端窗口。

**场景：**
