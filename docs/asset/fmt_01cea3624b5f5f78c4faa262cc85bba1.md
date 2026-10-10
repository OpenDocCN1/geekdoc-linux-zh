
你在一台 Linux 系统上安装了 PDF 软件，以便用户能够查看电子书。部分用户在尝试打开最新电子书时遇到错误。检查错误后，你决定将 PDF 软件升级到最新版本。

| 你要做什么 | 怎么做 |
| :--- | :--- |
| 1. 安装较新版本的 Adobe Reader 软件包。 | a. 输入 `rpm -Uvh AdobeRdr9.1.0-1_i486linux_enu.rpm` 以升级 Acrobat Reader 软件包。 |
| | b. 观察进度条达到 `100%`，对应于 `AdobeReader_eni`，表明软件包已成功安装。 |

- 2. 验证 Adobe Reader 软件包已升级。

  - a. 输入 `rpm -qi AdobeReader_enu` 以查看软件包信息。

  - b. 观察 `Version`（版本）为 `9.1.0`，`Release`（发布版）为 `1`。

  - c. 输入 `cd /opt/Adobe/Reader9/bin` 以切换到 `bin` 目录。

  - d. 输入 `./acroread` 以启动应用程序。

  - e. 在 `Adobe Reader - License Agreement`（Adobe Reader - 许可协议）对话框中，点击 `Accept`（接受）以接受协议条款。

  - f. 观察 `Acrobat Reader` 窗口已显示。

  - g. 关闭 `Acrobat Reader` 窗口。

  - h. 输入 `clear` 以清除终端窗口。

## 主题 D

### 配置软件源

你已升级并刷新了已安装的软件包。在管理网络时，你可能需要用最新的软件包更新系统。你需要知道从哪里获取这些软件包。在本主题中，你将了解软件源及其如何用于更新系统。

使用最新软件包更新系统是系统管理员最重要的职责之一。为此，你必须知道软件包在哪里可用以及如何下载它们。

## 软件源

**定义：**

*软件源*（`repository`）是一个保存源代码和编译结果的数据库。有两种类型的软件源：本地和在线。只有当系统上存在软件的软件源时，才能在该系统上安装软件。软件的软件包在其各自的软件源中找到，并直接从其中安装。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_288_0.png)

软件源

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_288_1.png)

*图 7-7：一个本地软件源。*

## 软件源类型

有两种类型的软件源：*在线软件源*和*本地或私有软件源*。在线软件源位于互联网上。软件包可以直接从互联网下载并安装到系统上。本地或私有软件源存储在你的系统上。由于源文件随时可用，软件源极大地促进了系统更新过程。软件源使系统管理员更容易同时更新多个系统。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_288_2.png)

软件源类型

![](img/477ccb2f05b6ba1b2d563ea74f18c197_289_0.png)

## createrepo 命令

`createrepo` 命令用于创建 `yum` 软件源。它生成称为 `repomd` 的 XML 元数据，并基于现有的 `rpm` 软件包创建软件源。`createrepo` 命令有许多选项，以促进软件源创建过程。

`createrepo` 命令的各种选项如下所示。

| 选项 | 功能 |
| :--- | :--- |
| `-p` | 以 XML 格式生成输出。 |
| `-s` | 选择用于创建软件源的校验和。 |
| `-c` | 将软件源与校验和进行比较，并检查软件包完整性。为软件包校验和创建缓存目录。 |
| `-x` | 从软件源中排除指定的文件。 |
| `-h` | 显示帮助菜单。 |
| `-v` | 详细运行命令。 |

## 语法

`createrepo` 命令的语法为 `createrepo [选项] <目录>`。

## 如何配置软件源

### 操作参考：创建私有软件源

要创建私有软件源：

- 1. 以 `root` 身份登录。

- 2. 输入 `mkdir /(<目录名>)` 以创建目录。

- 3. 在目录中填充软件包。

- 4. 输入 `createrepo -v /(<目录名>)` 以创建私有软件源。

- 5. 如果你从目录中添加或删除任何软件包，请再次运行 `createrepo` 命令。

### 操作参考：配置额外软件源

要配置额外软件源：

- 1. 以 `root` 身份登录。

- 2. 输入 `cd /etc/yum.repos.d` 以导航至 `/etc/yum.repos.d` 目录。

- 3. 输入 `vi (<文件名>)` 以创建一个文件。

- 4. 切换到插入模式。

- 5. 输入所需信息。

  - 输入 `name = 软件源名称` 以设置软件源名称。

  - 输入 `软件源描述` 以提供软件源描述。

  - 输入 `baseurl = {软件源URL}` 以设置软件源的 `baseurl`。

  - 输入 `enabled = {0 | 1}` 以控制软件源状态。

  - 输入 `gpgcheck = {0 | 1}` 以控制 GPG 签名验证。

- 6. 保存并关闭文件。

## GPG

`GnuPG` (`GPG`) 是一种用于加密和签署软件包或文件的自由软件。加密或签名用于验证网络上共享的任何文件的真实性。

## 活动 7-4

### 配置软件源

**开始之前：**

- 1. 你已在图形界面中以 `root` 身份登录。

- 2. 终端窗口已显示。

- 3. 输入 `cd /rhelsource/Server` 以切换到 `Server` 目录。

- 4. 输入 `clear` 以清除终端窗口。

**场景：**

你被分配了使用 `kickstart` 应用程序更新网络上几台系统的任务。在安装过程中，你发现安装文件夹中有数百个软件包，每次你都必须查找 `kickstart` 软件包。因此，你决定通过创建一个包含特定软件包的 `kickstart` 软件源来简化工作，这样你就可以调用该软件源，而无需逐一查找软件包。

| 你要做什么 | 怎么做 |
| :--- | :--- |
| 1. 安装 `createrepo` 软件包。 | a. 输入 `rpm -ivh createrepo-0.4.11-3.el5.noarch.rpm` 以安装 `createrepo` 软件包。 |
| | b. 观察进度条达到 `100%`，表明软件包已成功安装。 |
| | c. 输入 `rpm -q createrepo` 以验证软件包已安装。 |
| | d. 观察显示了 `createrepo-0.4.11-3.el5` 软件包。 |
| | e. 输入 `rpm -qi createrepo` 以查看软件包信息。 |
| | f. 观察 `Version`（版本）为 `0.4.11`，`Release`（发布版）为 `3.el5`。 |

- 2. 创建私有软件源。

  - a. 输入 `cd /` 以导航至 `/` 目录。

  - b. 输入 `createrepo -v /rhelsource` 以创建私有软件源。

  - c. 观察来自 `/rhelsource/Server` 目录的 `2255` 个软件包已录入软件源。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_292_0.png)

- 3. 配置新软件源。

  - a. 输入 `cd /etc/yum.repos.d` 以导航至 `/etc/yum.repos.d` 目录。

  - b. 输入 `vi rhelsource` 以创建 `rhelsource` 文件。

  - c. 切换到插入模式。

  - d. 输入 `name = rhelsource` 以指定软件源名称。

  - e. 输入 `My Local Repository` 以指定软件源描述。

  - f. 输入 `baseurl=file://rhelsource/Server/` 以指定基础 URL。

  - g. 输入 `enabled = 1` 以启用软件源。

  - h. 输入 `gpgcheck = 0` 以禁用 `gpgcheck`。

  - i. 按 `Esc` 键退回到命令模式。

  - j. 保存并关闭文件。

- 4. 禁用 `yum` 配置文件中的 `gpgcheck`。

    - a. 输入 `vi /etc/yum.conf` 以打开 `yum.conf` 文件。

    - b. 输入 `/gpg` 以定位到 `gpgcheck=1` 行。

    - c. 切换到插入模式。

    - d. 将 `gpgcheck=1` 更改为 `gpgcheck=0` 以禁用 `gpgcheck`。

    - e. 按 `Esc` 键退出到命令模式。

    - f. 保存并关闭文件。

    - g. 输入 `clear` 以清除终端窗口。

## 主题 E

### 使用 YUM 管理软件包

你之前已经使用 `RPM` 在单台计算机上管理了软件包安装。作为系统管理员，你的任务是在短时间内同时在多台系统上安装软件。在本主题中，你将学习如何使用 `YUM` 管理软件包安装。

作为系统管理员，你需要同时处理多台系统。你需要尽可能快速地同时在所有系统上安装软件包。了解 `YUM` 软件包管理器的知识将帮助你同时在多台系统上安装和管理软件包。

### YUM 软件包管理器

*Yellow dog Updater, Modified*（`YUM`）是一个用于更新、安装和管理软件包的软件包管理器。`YUM` 会自动检测并配置软件包的依赖关系，并维护一个已安装软件的数据库。由于易于操作，`YUM` 被系统管理员广泛使用。它支持本地和在线软件仓库。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_294_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_294_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_295_0.png)

### YUM 命令

`YUM` 提供了各种可用于维护软件包的命令。

| 命令 | 功能 |
|:---|:---|
| `install` | 安装软件包。 |
| `update` | 更新软件包。如果未指定软件包，该命令将更新所有软件包。 |
| `check-update` | 检查可用的更新。 |
| `remove` | 删除指定的软件包。 |
| `list` | 显示指定软件包的详细信息。如果未指定软件包，则列出系统中所有软件包的状态。 |
| `info` | 显示指定软件包的简要描述。 |
| `localinstall` | 从本地仓库安装软件包。 |

### 语法

`YUM` 命令的语法为 `yum [options] {command} {package name}`。

### 如何使用 YUM 管理软件包

操作参考：使用 `YUM` 管理软件包

要使用 `yum` 管理软件包：

- 1. 以 `root` 身份登录。

- 2. 使用 `yum` 管理软件包。

    - 输入 `yum install {package name}` 使用 `YUM` 安装软件包。

    - 输入 `yum remove {package name}` 使用 `YUM` 删除软件包。

    - 输入 `yum info {package name}` 显示软件包描述。

    - 输入 `yum update {package name}` 使用指定的软件包更新系统。

### 活动 7-5

#### 使用 YUM 管理软件包

**开始之前：**

- 1. 你已在 `GUI` 中以 `root` 身份登录。

- 2. 已显示终端窗口。

- 3. 输入 `cd /root` 切换到 `root` 目录。

- 4. 输入 `clear` 清除终端窗口。

**场景：**

贵公司安排了一次会议。你需要在会议室的系统上安装 `ypbind` 服务，以启用网络通信。你还被要求向用户介绍已安装的 `ypbind` 软件包。你决定安装这些软件包，并利用 `YUM` 输出中显示的详细信息生成描述。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_296_0.png)

> 第 12 课中的活动 `Configuring NIS Services`（配置 NIS 服务）依赖于本活动。因此，请务必与学生一起执行此活动。

| 执行的操作 | 执行方法 |
| :--- | :--- |
| 1. 使用 `yum` 安装 `ypbind` 软件包。 | a. 输入 `yum localinstall /rhelsource/Server/yp*` 安装软件包。<br>b. 在 `Is this ok [y/N]:` 提示下，输入 `y` 确认下载。<br>c. 观察依赖关系已更新，并显示 `Complete!` 消息。<br>d. 输入 `clear` 清除终端窗口。 |
| 2. 检查软件包的状态。 | a. 输入 `yum list ypbind` 查看 `ypbind` 软件包的状态。<br>b. 观察 `ypbind.i386` 列在 `Installed Packages`（已安装软件包）下。<br>c. 输入 `yum info ypbind` 查看 `ypbind` 软件包的描述。<br>d. 观察软件包版本为 `1.19`，发行版为 `11.el5`。<br>e. 输入 `clear` 清除终端窗口。 |

## 主题 F

### 使用 Debian 软件包管理器管理软件包

在上一主题中，你使用 `YUM` 软件包管理器管理软件包。你可能还需要在其他 Linux 发行版中管理软件包。在本主题中，你将学习如何使用 Debian 软件包管理器管理软件包。

作为 Linux+ 管理员，你可能需要删除过时软件包以释放硬盘空间。如果你知道软件包安装在哪里，删除不需要的软件包会更容易。你需要跟踪安装软件包时添加的所有文件。这可以通过 Debian 软件包管理器完成。

### Debian 归档软件包安装过程

Debian 归档软件包安装过程包括三个阶段：检查依赖、解包和配置。

- 在 `check for dependency`（检查依赖）阶段，软件包管理器检查指定的 Debian 归档软件包所需的众多依赖关系。

- 在 `unpack`（解包）阶段，Debian 归档软件包及其依赖软件包被解包到硬盘的文件系统中。

- 在最终的 `configure`（配置）阶段，解包的文件可以使用默认值进行配置，或根据需求进行定制。除此之外，你还可以选择稍后重新配置该软件包及其依赖项。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_297_0.png)

图 7-9：Debian 归档软件包安装过程中的阶段。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_297_1.png)

### DEB 工具

`DEB` 工具是一套用于基于 Debian 的 Linux 发行版软件包管理的工具。`DEB` 工具用于安装、列出和删除符合 `DEB` 打包标准的软件包。高级软件包工具（`APT`）是 `DEB` 工具套件的 `front end`（前端），旨在使其更易于使用。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_298_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_298_1.png)

`DEB` 套件中包含的工具如下表所示。

| 工具 | 描述 |
|---|---|
| `dpkg` | 它是主要的软件包管理程序。其主要目的是安装和删除 `DEB` 软件包。 |
| `dpkg-deb` | 它是 Debian 软件包的归档操作工具。用于从目录中提取 `DEB` 软件包内容并显示软件包信息。还用于收集和删除关于 Debian 归档的信息。 |
| `dpkg-split` | 它将软件包拆分成更小的部分。它用于将软件包拆分为 `1.44 MB` 的大小，以便可以装在一组软盘中。 |
| `dselect` | 它是 `dpkg` 软件包的菜单驱动前端界面。通过此实用程序，你可以安装和删除软件包。 |

### Debian 归档软件包管理命令

Debian 软件包管理命令可用于获取 Debian 归档软件包的信息。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_298_2.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_298_3.png)

一些 Debian 归档软件包管理命令选项描述如下表所示。

| 选项 | 用途 |
|---|---|
| `dpkg -p [Debian package name]` | 查看软件包的版本、依赖关系和完整性。 |
| `dpkg -L [Debian package name]` | 列出软件包的内容。 |
| `dpkg -l [Debian package name]` | 查看安装状态。 |
| `dpkg --yet-to-unpack` | 查找尚未安装的软件包。 |
| `dpkg -S [File or package name]` | 查找包含特定文件或软件的软件包。 |

### apt-get 命令

![](img/477ccb2f05b6ba1b2d563ea74f18c197_299_0.png)

`apt-get` 命令用于通过互联网或从分发光盘安装或升级软件包。在安装或升级软件包时，`apt-get` 命令会访问 `/etc/apt/sources.list` 文件中列出的网站或 `CD-ROM`。

`apt-get` 命令具有各种选项。

| **选项** | **用途** |
| :--- | :--- |
| `apt-get install [Debian package name]` | 安装软件包 |
| `apt-get remove [Debian package name]` | 卸载软件包 |
| `apt-get upgrade [Debian package name]` | 升级软件包 |

### 语法
