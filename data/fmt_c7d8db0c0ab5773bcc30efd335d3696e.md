
该命令确保在你完成内核时，正确应用你使用的任何编号方案。继续以特权用户身份操作。

## 编译内核文件和可加载模块

参考第 572 页的“前提条件”（`Prerequisites`）获取必须安装源码的包列表。运行以下命令编译内核和模块，并在工作目录中生成 `.deb` 文件。

```bash
make -s kconfig --init -modules --append-to-version $(uname) kernel_image

make kernelversion12.032 -f /usr/src/linux-package/ruleset/minimal.mk debian APP_ENTRIES_VERSION=12.032-Y298_ROOT_clean
```

```
====== making target debian (new prereqs) =====

This is kernel package version 12.032

test debian

test ! -f stamp-building || rm -f stamp-building

chmod -R root:root /usr/src/linux/linux-image-2.6.32.i386.23712202298

chmod -R root:root /usr/src/linux/linux-image-2.6.32.i386.23712202298

chmod -R root:root /usr/src/linux/linux-image-2.6.32.i386.23712202298

dpkg --build

dpkg: Building package linux-image-2.6.32.i386.23712202298 in "../linux-image-2.6.32.i386.23712202298.deb"

make[1]: Leaving directory /usr/src/linux-source-2.6.32

make[1]: Entering directory /usr/src/linux-source-2.6.32
```

```
S 1 install
../linux-image-2.6.32.i386.23712202298_2.6.32.i386.23712202298-10.0.Custom_i386.deb
```

## 第 15 章构建 Linux 内核

`--append-to-version` 选项允许你指定一个唯一标识你正在构建的内核的字符串。该字符串还可以防止覆盖现有的内核。你可以按照此选项指定任何字符串，使用小写字母、数字、下划线、连字符和点集中的字符。你指定的值将放置在内核名称和发布版本的末尾。你可以在此字符串中记录应用于内核的补丁，以帮助开发者跟踪漏洞。前一个示例使用了命令替换（第 362 页）将自 UNIX 纪元以来的秒数放入内核名称中，从而轻松区分多个内核中最新的一个。

## 使用可加载内核模块

可加载内核模块（第 1157 页）（有时称为模块或可加载模块）是内核的组成部分——即在运行时链接到内核中。模块可以在运行时从运行的内核中插入和删除（模块正在使用时除外）。这使得内核在任何时刻保持尽可能小的灵活性。模块是添加内核功能的好方法，包括不需要的驱动程序（例如磁带驱动程序）。模块以 `.ko` 结尾并存储在 `/lib/modules` 的子目录下。Ubuntu 模块如后续节所述，与内核一起编译。

## 寻找非标准模块

许多驱动不在主源码树中，或者没有以 `--source` 包的形式提供。你可以使用 `module-assistant` 工具来管理这些模块。

`module-assistant` 是一个用于下载、编译和安装内核模块的命令行工具。它对于未包含在标准发行中的模块特别有用。

`module-assistant` 命令格式如下：

```
module-assistant [options] command [pkglist]
```

其中 `command` 是列出的命令之一，`pkglist` 是空格分隔的包列表。

- `auto-install pkglist`：结合 `prepare`、`get`、`build` 和 `install` 命令处理 `pkglist`。该命令简写为 `-i`。
- `build pkglist`：编译 `pkglist`。错误位于 `/var/cache/dpkg`。
- `get pkglist`：下载并安装 `pkglist` 的源码。
- `install pkglist`：安装 `pkglist`。如果没有 `pkglist`，则为本地运行内核构建的最后一个包。
- `list [pkglist]`：带参数时列出 `pkglist` 的详细信息。如果没有参数，列出所有已知包。该命令简写为 `-l`。
- `list-installed`：列出已安装包的详细信息。简写为 `li`。
- `prepare`：内核头包名称，根据需要安装其和 `build-essential` 包，并创建 `/usr/src/linux` 符号链接。使用 `-l` 选项，此命令使用你指定的内核版本。如果没有此选项，它使用本地运行内核的版本。在运行任何其他 `module-assistant` 命令之前必须运行此命令。

## 下载、编译和安装非标准模块

一旦确定了名称，你就需要下载、编译和安装模块源码。`module-assistant` 工具调用 `sudo` 来运行 `apt-get` 和 `dpkg`。如果你对 `/usr/src` 没有写入权限，它将失败；`sudo` 提示你输入密码。你必须是 `admin` 组的成员，以便 `module-assistant` 能成功调用 `sudo`。如果没有 `--text-mode` 选项，`module-assistant` 将呈现图形化界面。

如果你遇到问题，可能希望调用 `module-assistant` 执行每个步骤。以下命令使用 `-t` 代替 `--text-mode`：

```bash
module-assistant -t prepare

module-assistant -t get

module-assistant -t build

module-assistant -t install
```

# 加载模块

当你使用 `module-assistant` 安装模块后，必须加载该模块才能使其对运行中的内核可用。表 15-1 列出了某些可以帮助你处理模块的工具。请参考相应的帮助手册页以获取选项和更多信息。

表 15-1 处理模块的工具

| 工具/实用程序 | 功能 |
| --- | --- |
| depmod | 处理模块的依赖关系。 |
| insmod | 在运行的内核中加载模块。 |
| lsmod | 列出所有已加载模块的信息。 |
| modinfo | 列出模块的信息。 |
| modprobe | 加载、卸载并报告模块。当它加载一个模块时，它也会加载依赖项。 |
| rmod | 从运行的内核中卸载模块。 |

# 安装内核、模块和相关文件

下一步是将编译好的内核、模块和相关文件复制到相应的目录——通常是 `/boot`。如果你在 `/boot` 挂载了分区，则文件将保存在该分区的根目录下（即 `/boot`）。由于你创建了 deb 包，安装这些文件非常简单。以下命令将新内核文件安装到属性中：

```bash
$ cd

$ dpkg -i linux-image-2.6.32.11-drm33.212720298-2.6.32.11-drm33.212720298-00.Custom_i386.deb

Selecting previously selected package linux-image-2.6.32.11-drm33.212720298-

(Reading database ... 138002 files and directories currently installed.)

Unpacking linux-image-2.6.32.11-drm33.212720298 (from linux-image)

2.6.32.11-drm33.212720298-00.Custom_i386.deb

done.

Setting up linux-image-2.6.32.11-drm33.212720298-2.6.32.11-drm33.212720298-00.common

done.

Examining /etc/postinst/*

run-executing script /etc/postinst/linux-common/nvidia-common 2.6.32.11-drm33.212720298

/boot/vmlinuz-2.6.32.11-drm33.212720298

run-executing script /etc/postinst/linux-common/pm-utils 2.6.32.11-drm33.212720298

/boot/vmlinuz-2.6.32.11-drm33.212720298

Running postinst hook script update-grub

Generating grub.cfg
```
