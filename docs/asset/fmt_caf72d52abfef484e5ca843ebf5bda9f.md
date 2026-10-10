
- i. 按`Esc`键退回到命令模式。
- j. 保存并关闭文件。
- 4. 禁用`yum`配置文件中的`gpgcheck`。
  - a. 输入`vi /etc/yum.conf`以打开`yum.conf`文件。
  - b. 输入`/gpg`以定位到`gpgcheck=1`行。
  - c. 切换到插入模式。
  - d. 将`gpgcheck=1`更改为`gpgcheck=0`以禁用`gpgcheck`。
  - e. 按`Esc`键退出到命令模式。
  - f. 保存并关闭文件。
  - g. 输入`clear`以清除终端窗口。

## 主题 E

### 使用 YUM 管理软件包

你之前已经使用`RPM`在单台计算机上管理了软件包安装。作为系统管理员，你的任务是在短时间内同时在多台系统上安装软件。在本主题中，你将学习如何使用`YUM`管理软件包安装。

作为系统管理员，你需要同时处理多台系统。你需要尽可能快速地同时在所有系统上安装软件包。了解`YUM`软件包管理器的知识将帮助你同时在多台系统上安装和管理软件包。

### YUM 软件包管理器

`Yellow dog Updater, Modified`（`YUM`）是一个用于更新、安装和管理软件包的软件包管理器。`YUM`会自动检测并配置软件包的依赖关系，并维护一个已安装软件的数据库。由于易于操作，`YUM`被系统管理员广泛使用。它支持本地和在线软件仓库。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_294_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_294_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_295_0.png)

### YUM 命令

`YUM`提供了各种可用于维护软件包的命令。

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

`YUM`命令的语法为`yum [options] {command} {package name}`。

### 如何使用 YUM 管理软件包

操作参考：使用`YUM`管理软件包

要使用`yum`管理软件包：

- 1. 以`root`身份登录。
- 2. 使用`yum`管理软件包。
  - 输入`yum install {package name}`使用`YUM`安装软件包。
  - 输入`yum remove {package name}`使用`YUM`删除软件包。
  - 输入`yum info {package name}`显示软件包描述。
  - 输入`yum update {package name}`使用指定的软件包更新系统。

### 活动 7-5

#### 使用 YUM 管理软件包

开始之前：

- 1. 你已在`GUI`中以`root`身份登录。
- 2. 已显示终端窗口。
- 3. 输入`cd /root`切换到`root`目录。
- 4. 输入`clear`清除终端窗口。

场景：

贵公司安排了一次会议。你需要在会议室的系统上安装`ypbind`服务，以启用网络通信。你还被要求向用户介绍已安装的`ypbind`软件包。你决定安装这些软件包，并利用`YUM`输出中显示的详细信息生成描述。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_296_0.png)

> 第 12 课中的活动`Configuring NIS Services`（配置 NIS 服务）依赖于本活动。因此，请务必与学生一起执行此活动。

| 执行的操作 | 执行方法 |
| :--- | :--- |
| 1. 使用`yum`安装`ypbind`软件包。 | a. 输入`yum localinstall /rhelsource/Server/yp*`安装软件包。<br>b. 在`Is this ok [y/N]:`提示下，输入`y`确认下载。<br>c. 观察依赖关系已更新，并显示`Complete!`消息。<br>d. 输入`clear`清除终端窗口。 |
| 2. 检查软件包的状态。 | a. 输入`yum list ypbind`查看`ypbind`软件包的状态。<br>b. 观察`ypbind.i386`列在`Installed Packages`（已安装软件包）下。<br>c. 输入`yum info ypbind`查看`ypbind`软件包的描述。<br>d. 观察软件包版本为`1.19`，发行版为`11.el5`。<br>e. 输入`clear`清除终端窗口。 |

## 主题 F

### 使用 Debian 软件包管理器管理软件包

在上一主题中，你使用`YUM`软件包管理器管理软件包。你可能还需要在其他`Linux`发行版中管理软件包。在本主题中，你将学习如何使用`Debian`软件包管理器管理软件包。

作为`Linux+`管理员，你可能需要删除过时软件包以释放硬盘空间。如果你知道软件包安装在哪里，删除不需要的软件包会更容易。你需要跟踪安装软件包时添加的所有文件。这可以通过`Debian`软件包管理器完成。

### Debian 归档软件包安装过程

`Debian`归档软件包安装过程包括三个阶段：检查依赖、解包和配置。

- 在`check for dependency`（检查依赖）阶段，软件包管理器检查指定的`Debian`归档软件包所需的众多依赖关系。
- 在`unpack`（解包）阶段，`Debian`归档软件包及其依赖软件包被解包到硬盘的文件系统中。
- 在最终的`configure`（配置）阶段，解包的文件可以使用默认值进行配置，或根据需求进行定制。除此之外，你还可以选择稍后重新配置该软件包及其依赖项。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_297_0.png)

图 7-9：`Debian`归档软件包安装过程中的阶段。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_297_1.png)

### DEB 工具

`DEB`工具是一套用于基于`Debian`的`Linux`发行版软件包管理的工具。`DEB`工具用于安装、列出和删除符合`DEB`打包标准的软件包。高级软件包工具（`APT`）是`DEB`工具套件的`front end`（前端），旨在使其更易于使用。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_298_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_298_1.png)

`DEB`套件中包含的工具如下表所示。

| 工具 | 描述 |
|---|---|
| `dpkg` | 它是主要的软件包管理程序。其主要目的是安装和删除`DEB`软件包。 |
| `dpkg-deb` | 它是`Debian`软件包的归档操作工具。用于从目录中提取`DEB`软件包内容并显示软件包信息。还用于收集和删除关于`Debian`归档的信息。 |
| `dpkg-split` | 它将软件包拆分成更小的部分。它用于将软件包拆分为`1.44 MB`的大小，以便可以装在一组软盘中。 |
| `dselect` | 它是`dpkg`软件包的菜单驱动前端界面。通过此实用程序，你可以安装和删除软件包。 |

### Debian 归档软件包管理命令

`Debian`软件包管理命令可用于获取`Debian`归档软件包的信息。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_298_2.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_298_3.png)

一些`Debian`归档软件包管理命令选项描述如下表所示。

| 选项 | 用途 |
|---|---|
| `dpkg -p [Debian package name]` | 查看软件包的版本、依赖关系和完整性。 |
| `dpkg -L [Debian package name]` | 列出软件包的内容。 |
| `dpkg -l [Debian package name]` | 查看安装状态。 |
| `dpkg --yet-to-unpack` | 查找尚未安装的软件包。 |
| `dpkg -S [File or package name]` | 查找包含特定文件或软件的软件包。 |

### apt-get 命令
