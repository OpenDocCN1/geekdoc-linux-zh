

## 下载源代码

**rpmddev-setuptree** 在下载完所需的软件包（前一节）后，运行 **rpmddev-setuptree**。此实用工具会在你的主目录中设置一个 SRPM 构建环境，包括一个 **rpmbuild** 目录层次结构：

```
$ rpmddev-setuptree
$ ls rpmbuild
BUILD    RPMS    SOURCES    SPECS    SRPMS
```

编译内核后，**rpmddev-setuptree** 创建的五个目录将保存如下文件：**BUILD** 保存内核编译结果，**RPMS** 保存已编译的 RPM 文件，**SOURCES** 保存源代码和补丁文件，**SPECS** 保存内核规范文件，以及 **SRPMS** 保存源 RPM 文件（如果有）。

### 不要使用 root 权限操作

> **注意** 在配置或构建内核的任何环节中，除了安装软件包和安装内核（最后一步）之外，你都不需要——也不应该——使用 **root** 权限。内核 README 文件中指出：“不要滥用 **root** 之名。”

关于构建、自定义和安装内核的各节中，在需要使用 root 权限时使用 **su -c**。这种做法有助于防止你在无意中以 **root** 权限进行操作。如果出现问题，它还能提供一份更好的记录供你在 shell 历史中（第 376 页）查看。有关 **su -c** 的更多信息，请参考第 427 页的“执行单个命令”。

**yumdownloader** 对于最近发布的内核版本，下载更新的内核源代码最简单的方法是使用 **yumdownloader**。进入主目录并将内核源代码 RPM 文件下载到你的主目录：

```
$ cd
$ yumdownloader --source kernel
Loaded plugins: langpacks, refresh-packagekit
Enabling updates-source repository
Enabling fedora-source repository
...
kernel-3.9.8-300.fc19.src.rpm | 69 MB 00:27
```

### 关于本节中的示例

> **提示** 本节中的示例展示的是 Sam（其主目录为 /home/sam，即 ~sam）正在处理名为 **kernel-3.9.8-300.fc19** 的内核。当你构建内核时，你可能在自己的主目录中操作，而且你处理的内核名称可能与 Sam 的内核名称不同。在跟随示例操作时，请进行相应的替换。

## 安装源代码

**yum-builddep** 在内核源代码 RPM 包文件位于你的主目录中后，运行 **yum-builddep** 以下载并安装构建源代码包所需的软件包（依赖项）。由于你正在安装软件包，因此必须使用 **root** 权限。在下例中，请将 **sam** 和 3.9.8-300.fc19 替换为你的用户名和你正在使用的内核名称，以指定系统中 RPM 文件的位置。

```
$ su -c 'yum-builddep /home/sam/kernel-3.9.8-300.fc19.src.rpm'
Password:
Loaded plugins: langpacks, refresh-packagekit
Getting requirements for kernel-3.9.8-300.fc19.src
...
Install  15 Packages (+37 Dependent packages)

Total download size: 36 M
Installed size: 108 M
Is this ok [y/d/N]: y
...
Complete!
```

最后，作为非特权用户从你的主目录开始，使用 `rpm` 将内核源代码安装到你主目录中的 `rpmbuild` 目录层次结构：

```
$ rpm -Uvh kernel-3.9.8-300.fc19.src.rpm
  1:kernel    warning: user mockbuild does not exist -- using root
warning: group mockbuild does not exist -- using root
warning: user mockbuild does not exist -- using root
...
  1:kernel-3.9.8-300.fc19   ##################################################  [100%]
```

你可以忽略关于不存在的组和用户的错误（如上面所示）。

### 准备源代码

在你可以使用源代码之前，最后一步是进行预处理（prep）。预处理会解压缩文件并应用补丁。以下 `rpmbuild` 命令使用 `-bp` 选项来预处理源代码：

```
$ cd /home/sam/rpmbuild/SPECS
$ rpmbuild -bp --target {arch} kernel.spec
Building target platforms: x86_64
Building for target x86_64
Executing(%prep): /bin/sh -e /var/tmp/rpm-tmp.qGVQ0c
+ umask 022
+ cd /home/sam/rpmbuild/BUILD
...
```

如果 `rpmbuild` 找不到预处理代码所需的软件包，它会显示类似以下信息的消息：

```
error: Failed build dependencies:
  elfutils-libelf-devel is needed by kernel-3.9.8-300.fc19.x86_64
  zlib-devel is needed by kernel-3.9.8-300.fc19.x86_64
  binutils-devel is needed by kernel-3.9.8-300.fc19.x86_64
```

在这种情况下，安装所需的软件包（你可能需要安装与示例中不同的软件包）：

```
$ su -c 'yum install elfutils-libelf-devel zlib-devel binutils-devel'
```

安装完软件包后，再次运行上述 `rpmbuild` 命令。一旦内核源代码在本地系统上安装并预处理完成，你就可以对其进行配置、编译和安装了。

## 配置和编译 Linux 内核

本节介绍如何配置和编译内核。

> **提示** **内核源代码和内核规范文件在哪里？** 按照前一节描述安装并预处理源代码后，Sam 的源代码位于 /home/sam/rpmbuild/BUILD/kernel-3.9.fc19/linux-3.9-300.fc19.x86_64/，而他的内核规范文件位于 /home/sam/rpmbuild/SPECS。你的源代码将位于名称相似的目录中（~rpmbuild/BUILD/kernel-*linux*），而你的内核规范文件将位于名为 ~rpmbuild/SPECS 的目录中。

本节的大部分工作是在源代码所在的目录（Linux*）中完成的。内核的标记和安装在 SPECS 目录中进行。

### 标记内核

为了防止覆盖现有的内核文件并识别内核的各种编译版本，你可以修改 *kernel.spec* 文件中的 **buildid** 变量。该变量初始设置为 .local。你分配给该变量的任何值都会放在内核名称和发行版号的末尾，以标识该内核。你可以在此字符串中记录应用于内核的补丁，以便人们后来追踪问题。使用 **cd** 更改目录到 ~rpmbuild/SPECS，编辑 kernel.spec，并修改该行中的 local：

```
# %define buildid .local
```

改为一个能标识你正在构建的内核的值。你还必须删除前导的井号（#）、井号后的空格以及 % 和 define 之间的空格：

```
%define buildid .sam1307021000
```

### .config：配置内核

在你编译代码并创建 Linux 内核之前，必须决定并指定你希望内核支持哪些功能。你可以通过两种方式之一来配置内核以支持大多数功能：将功能构建到内核中，或将该功能指定为可加载内核模块（第 589 页），该模块仅在需要时加载到内核中。在决定使用哪种方法时，你必须权衡内核的大小与加载模块所需的时间。尽量使内核尽可能小，同时最小化模块加载的频率。

~rpmbuild/BUILD/kernel-*linux* 目录中的 .config 文件控制新内核将支持哪些功能以及如何支持这些功能。下一节提供了替换现有自定义内核的说明。第 586 页的“自定义内核”解释了如果 .config 文件不存在，如何创建其默认版本；如果文件存在，如何编辑该文件。

### 替换自定义内核

如果你已经配置了一个自定义内核，你可能会想用配置类似但更新的内核来替换它。然而，每个内核都可能拥有新的配置选项——这就是为什么使用旧的 **.config** 文件来编译新内核是不好的做法。本节解释如何升级现有的 **.config** 文件，使其包含新内核的新选项，同时保留旧选项的现有配置。

在 `~/rpmbuild/BUILD/kernel*/linux*` 目录中工作。系统会在 `/boot` 中保留本地系统正在运行的内核的配置文件副本。以下命令将此文件复制到当前工作目录中的 **.config**：

```
$ pwd
/home/sam/rpmbuild/BUILD/kernel-3.9._fc19/linux-3.9._8-300._fc19.x86_64
$ cp /boot/config-$(uname -r) .config
```

在此命令中，shell 执行 `uname -r` 并使用命令替换（第 410 页）用该命令的输出替换 `$(uname -r)`，该输出是本地系统正在运行的内核发行版的名称。

接下来执行命令 `make oldconfig`，用新内核中不在旧内核中的选项来修补 **.config** 文件。此命令显示新内核和旧内核中相同的每个内核选项，并自动将新内核中该选项的状态设置为与旧内核中的设置方式相同。当它发现一个在新内核中出现但不在旧内核中的选项时停止。然后它显示一个提示，类似于 [N/y/?]（NEW），显示可能的响应并表明此选项是新的。提示会以大写字母显示默认响应；你可以输入该字母（大写或小写）并按 RETURN，或者直接按 RETURN 来选择此响应。在示例中，Tickless System 选项是新的，默认响应是 Y（表示是），*将选项包含在新内核中*。要选择非默认响应（**n** 表示*否，不包含该选项*，**m** 表示*将选项作为模块包含*），你必须输入该字母并按 RETURN。输入 ? 然后按 RETURN 以显示有关该选项的更多信息。

```
$ make oldconfig
scripts/kconfig/conf --oldconfig Kconfig

* Linux Kernel Configuration
*
* Code maturity level options
*
* Prompt for development and/or incomplete code/drivers (EXPERIMENTAL) [Y/n/?] y
*
* General setup
*
* Local version - append to kernel release (LOCALVERSION) []
* Automatically append version information to version string (LOCALVERSION_AUTO) [N/y/?] n
...
```

