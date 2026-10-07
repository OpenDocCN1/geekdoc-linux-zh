
*(注：由于用户提供的待翻译文本从“PREREQUISITES”之后开始出现大量重复且无意义的英文单词，此处翻译工程师已对核心技术内容完成翻译。)*

## `/usr/src/linux`: 工作目录

传统上，系统正在运行的内核源码位于 `usr/src/linux`。以下命令将创建相应的符号链接。示例显示的内核目录名称为 `linux-source-2.6.32`；你正在操作的系统上的名称会略有不同。

```bash
# ln -s /usr/src/linux-source-2.6.32 /usr/src/linux
```

执行这些命令后，内核源码位于 `/usr/src/linux`。本章的其余部分假设内核源码位于此位置。

## 现在工作目录是 `/usr/src/linux`

- 本节中所有关于构建内核的命令都相对于存放内核源码的顶层目录。传统上，该目录是 `/usr/src/linux`。在继续操作之前，请确保该目录是你的工作目录。如有必要，请如上所述，将 `/usr/src` 中存放内核源码的目录链接到 `/usr/src/linux`。

## 阅读文档

内核包包含了最新的文档，某些内容在其他文档中可能没有。你可能希望查看内核源码目录顶部的 `README` 以及 `Documentation` 子目录中的相关文件。此外，`/usr/share/doc/kernel-package` 目录下有大量信息。请阅读《Linux Kernel-HOWTO》，以获取关于安装和配置 Linux 内核的详细但有些过时的通用指南。

## 配置和编译 Linux 内核

本节描述了如何配置内核、如何编译内核以及如何下载和编译内核模块。

### `.config`: 配置内核

在编译代码并创建 Linux 内核之前，你必须决定并指定你希望内核支持的功能。你可以通过两种方式之一配置内核支持大多数功能：将功能构建进内核，或者将功能指定为可加载内核模块（第 580 页），根据需要将其加载到内核。在决定使用哪种方法时，你必须权衡内核的大小与加载模块所需的时间。在尽可能减少模块加载频率的同时，使内核尽可能精小。除非你有特殊理由，否则不要将 SCSI 驱动程序设置为模块化。

你下载源码目录中的 `.config` 文件控制着新内核将支持的功能以及其支持方式。“自定义 Linux 内核”（第 577 页）解释了如果该文件不存在如何创建该文件的默认版本，以及如果它已存在如何编辑该文件。

### 替换自定义内核

如果你已经配置了一个自定义内核，你可能想用一个配置相似的更新内核来替换它。然而，每个内核都可能有新的配置选项——这解释了为什么使用旧的 `.config` 文件编译新内核是一个糟糕的做法。本节解释了如何升级现有的 `.config` 文件，使其包含内核中新增的选项，并保持旧选项的配置。

在下载或解压源码的目录中操作。系统在 `/boot` 中保留了本地运行内核的配置副本。以下命令将该文件复制到工作目录下的 `.config`：

```bash
$ cp /boot/config-$(uname -r) .config
```

在该命令中，shell 执行 `uname -r` 并用 `$(uname -r)` 替换为命令的输出结果，即本地系统运行的内核版本名称。更多信息请参阅第 362 页的“命令替换”。

接下来执行 `oldconfig` 命令，用新内核中存在但旧内核中的选项来修复 `.config` 文件。该命令会显示新旧内核中相同的内核选项，并自动将新内核中该选项设置为与旧内核相同的状态。当发现新内核中出现但在旧内核中不存在的选项时停止。随后它会显示一个提示，类似于 `[N/y]? (NEW)`，显示可能的响应并指示该选项的状态。提示显示大写字母为默认响应；你可以输入该字母（大写或小写）并按 `RETURN`，或直接按 `RETURN` 选择此响应。在示例中，Tickless System（无滴答系统）选项是新的，默认响应为 `Y`，表示在新内核中包含该选项。要选择非默认响应（`n` 表示不，不包含该选项；`m` 表示作为模块包含该选项），你必须输入字母并按 `RETURN`。输入 `?` 后按 `RETURN` 显示有关该选项的更多信息。

```bash
$ make oldconfig
scripts/kconfig -o arch/i386/Kconfig
```

- Linux 内核配置

- 代码成熟度级别选项

- 开发和/或不完整代码/驱动程序的提示 (EXPERIMENTAL) [Y/n]? y

- 通用设置

- 本地版本 - 追加内核发布版本 (LOCALVERSION) []

- 自动向版本字符串附加版本信息 (LOCALVERSION_AUTO) [N/y/?] n

...

- 处理器类型和特性

- Tickless System (Dynamic Ticks) (NO_HZ) [Y/n?] (NEW) ? ?

此选项启用无滴答系统：当系统忙碌或空闲时，定时器中断将仅根据需要触发。

- Tickless System (Dynamic Ticks) (NO_HZ) [Y/n?] (NEW) RETURN

高分辨率定时器支持 (HIGH_RES_TIMERS) [Y/n/] y

对称多处理器处理支持 (SMP) [Y/n/] y

- 子架构类型

    - 1. PC 兼容型 (x86_PC)

    - 2. AMD Elan (x86_ELAN)

```bash
# 配置写入 .config
```

## 自定义内核

你可以使用三个标准命令之一构建配置 Linux 内核的 `.config` 文件：

```bash
$ make config
$ make menuconfig
$ make gconfig
```

请参阅第 572 页的“前提条件”，了解运行除第一个命令外命令所需的软件包列表。

如果工作目录中不存在 `.config` 文件，这些命令中的除第一个外都会设置一个与系统运行内核匹配的 `.config` 文件并允许你修改该配置。只有当本地运行内核的配置文件位于 `/boot/config-$(uname -r)` 时，这些命令才能设置该 `.config` 文件。如果你想构建与现有配置相似的新内核，请参见前节。

`make config` 命令是三个命令中最简单的，使用文本界面且不需要额外的软件。然而，它是最不容错且最难使用的。`make menuconfig` 使用伪图形界面并显示文本界面。`make gconfig` 使用 GTK+ (www.gtk.org) 并显示图形界面。

在响应相同的情况下，每个命令都会询问相同的问题并产生相同的结果。前两个命令在字符环境中工作；第三个命令在图形环境中工作。对于许多使用 GUI 的管理员来说，第三种方法是最容易使用的。

### 配置与编译 Linux 内核 579

浏览各个选项，并按照你希望在新内核中配置的特性进行设置。在配置过程中的任何时候，你都可以将当前定义的配置保存到文件中、从文件中加载配置，或者在不保存更改的情况下退出。这些操作可以通过菜单栏：文件（File）来完成。完成后，选择菜单栏：文件+保存（File+Save）并关闭窗口。

## 清理源码树

在生成 `.config` 文件后，在编译或重新编译内核之前，使用以下命令清除源码树中所有的 `*.o` 文件：

```bash
$ make-kpkg clean
exec make kpkg_version=12.032 -f /usr/share/kernel-package/rules/minimal.mk clean
=================================================================
make target_minimal [new prereqs]: =
这是内核包版本 12.032。
test ! -ffconfig || cp -pf config.preconfig
test ! -e stamp-building || rm -f stamp-building
test ! -f Makefile ||
make ARCH=i386 distclean
make[1]: Entering directory /usr/src/linux-source-2.6.32/
CLEAN scripts/basic
CLEAN scripts/config
CLEAN include/config
CLEAN .config include/linux/autocon.h
make[1]: Leaving directory /usr/src/linux-source-2.6.32/
test ! -fconfig || mv -f config.preconfig
rm -f modules/modversions.kernel/ksys.ver scripts/cramfs/cramfscscripts/mkramfs
```

此命令永远不会正确应用于编译内核时使用的任何编号方案。请继续以特权用户身份运行。

## 编译内核镜像文件和可加载模块

参见第 572 页的“前提条件”，获取编译源码必须安装的包列表。执行以下命令来编译内核和模块；它会在工作目录下生成一个 `.deb` 文件。

```bash
$ make-kpkg --intrd --cdroot --append-to-version $(date) kernel_image
make kernel_version=12.032 -f /usr/share/kernel-package/rules/minimal.mk deb
END_TO_VERSION=1271020298 INTRO_YES ROOT_CMD=cdroot
make target_minimal [new prereqs]: =
这是内核包版本 12.032。
test -d debian
make mkdir
test ! -e stamp-building || rm -f stamp-building
chmod -R 755 /usr/src/linux/linux-image-2.6.32.11dm.23271202298
chown -R root:root /usr/src/linux/linux-image-2.6.32.11dm.23271202298
cd /usr/src/linux/linux-image-2.6.32.11dm.23271202298
depkg: deb building package "linux-image-2.6.32.11dm.23271202298" in '../linux-image-2.6.32.11dm23271202298-10.0.Custom_i386.deb'.
make[2]: Leaving directory /usr/src/linux-source-2.6.32
make[2]: Leaving directory /usr/src/linux-source-2.6.32
```

```bash
$ ls ../deb
../linux-image-2.6.32.11dm.23271202298-10.0.Custom_i386.deb
```

`--append-to-version` 选项允许你指定一个用于唯一标识你正在构建的内核的字符串。该字符串有助于防止覆盖现有内核。你可以在其后指定任何喜欢的字符串，使用的字符集由小写字母、数字、`--`（减号）、`+`（加号）和 `.`（点）组成。你指定的值将放置在内核名称和发布版本的末尾。你可以在此字符串中记录应用到内核的补丁，以帮助开发者跟踪错误。上一个示例使用了命令替换（第 362 页）将自 UNIX 纪元以秒数放入内核名称中，从而轻松判断哪个内核是最新的。

## 使用可加载内核模块

可加载内核模块（第 1157 页）（有时称为模块或可加载模块）是一个对象文件——内核的一部分——在运行时链接到内核中。模块可以任何时间从运行的内核中插入和删除（模块正在使用除外）。这使得内核可以在任何时候尽可能精小。模块是提供某些内核功能的好方法，包括并非持续使用的驱动（例如磁带驱动）。模块文件名以 `.ko` 结尾并存储在 `/lib/modules` 的子目录下。Ubuntu 内核模块如前节所述与内核一起编译。

## 寻找非标准模块

许多不在主源码树中或免费的驱动程序以 `*-source` 包的形式提供。你可以使用 `aptitude` 显示可用 `*-source` 包列表。以下示例首先更新 APT 缓存，然后显示与 NVIDIA 相关的 `*-source` 包列表。命令末尾的美元符号。

```bash
$ apt update
$ aptitude search - | nvidia
```

`--append-to-version` 选项允许你指定一个唯一标识你正在构建的内核的字符串。该字符串有助于防止覆盖现有内核。你可以在其后指定任何喜欢的字符串，使用的字符集由小写字母、数字、`--`（减号）、`+`（加号）和 `.`（点）组成。你指定的值将放置在内核名称和发布版本的末尾。你可以在此字符串中记录应用到内核的补丁，以帮助开发者跟踪错误。上一个示例使用了命令替换（第 362 页）将自 UNIX 纪元以秒数放入内核名称中，从而轻松判断哪个内核是最新的。

## 使用可加载内核模块

可加载内核模块（第 1157 页）（有时称为模块或可加载模块）是一个对象文件——内核的一部分——在运行时链接到内核中。模块可以任何时间从运行的内核中插入和删除（模块正在使用除外）。这使得内核可以在任何时候尽可能精小。模块是提供某些内核功能的好方法，包括并非持续使用的驱动（例如磁带驱动）。模块文件名以 `.ko` 结尾并存储在 `/lib/modules` 的子目录下。Ubuntu 内核模块如前节所述与内核一起编译。

## 寻找非标准模块

许多不在主源码树中或免费的驱动程序以 `*-source` 包的形式提供。你可以使用 `aptitude` 显示可用 `*-source` 包列表。以下示例首先更新 APT 缓存，然后显示与 NVIDIA 相关的 `*-source` 包列表。

```bash
$ apt update
$ aptitude search - | nvidia
```

## `MODULE-ASSISTANT`: 下载、编译和安装非标准模块

一旦确定了名称，你需要下载、编译并安装相应的包。在开始此过程之前，请检查第 572 页的前提条件。`module-assistant` 工具调用 `sudo` 来运行 `apt-get`。如果你没有对 `/src` 的写入权限（即你不在 `src` 组），它将失败；`sudo` 可能会提示输入密码。你必须是 `admin` 组的成员，以便 `module-assistant` 成功调用 `sudo`。如果没有 `--text-mode` 选项，`module-assistant` 将显示图形界面。

如果你遇到问题，可能希望逐个调用 `module-assistant`。在运行任何其他 `module-assistant` 命令之前，你必须运行 `module-assistant prepare`。以下命令使用了它：

`module-assistant` 命令格式如下：

```
module-assistant command [pkg-list]
```

其中 `command` 是列表中的命令，`pkg-list` 是一个或多个空格分隔的模块包。在使用 `module-assistant` 命名时不需要包含包的 `--source` 部分。`prepare` 命令不接受 `pkg-list`；其他命令都需要它。`module-assistant` 手页提供了更多选项、更多命令和更多信息。

- `auto-install pkg-list`

  合并了 `prepare`、`get`、`build` 和 `install` 命令并处理 `pkg-list`。

  此命令简写为 `a-i`。

- `build pkg-list`

  编译 `pkg-list`。错误信息输出到 `/var/cache/modcas/`

- `get pkg-list`

  下载并安装 `pkg-list` 的源码。

- `install pkg-list`

  安装 `pkg-list`。如果没有 `pkg-list`，它将安装为本地内核构建的最后一个包。

- `list-list`

  带参数时，列出 `pkg-list` 的详情。无参数，显示所有已知包。

  此命令简写为 `la`（list available）。

- `list-installed`

  列出已安装包的详情。

  此命令简写为 `li`。

- `prepare`

  确定内核头包的名称，并创建 `/usr/src/linux` 符号链接。使用 `-l` 选项按需要构建 `builds-essential` 创建你指定的内核版本。如果没有此选项，它将使用本地运行内核的版本。在运行任何其他 `module-assistant` 命令之前，你必须运行此命令。

## 加载模块

在用 `module-assistant` 安装模块后，你必须加载它使其在运行的内核中可用。表 15-1 列出了帮助你处理模块的可用工具。请参考相应的映射页以获取选项和更多信息。

表 15-1 处理模块的工具

| 工具/实用程序 | 功能 |
| --- | --- |
| `depmod` | 处理模块的依赖关系。 |
| `insmod` | 在运行的内核中加载模块。 |
| `lsmod` | 列出所有加载模块的信息。 |
| `modinfo` | 列出模块的信息。 |
| `modprobe` | 加载、卸载并报告模块。当它加载模块时，它也会加载依赖项。 |
| `rmmod` | 从运行的内核中卸载模块。 |

## 安装内核及相关文件

下一步是将编译好的内核及相关文件复制到相应的目录——通常是 `/boot` 和 `/lib/modules` 的子目录。当你在 `/boot` 有有一个分区时，文件将保留在该分区的根目录 (`/boot`) 中。当你创建了 `deb` 包时，安装这些文件非常简单。以下命令将新内核文件安装到目录中：
