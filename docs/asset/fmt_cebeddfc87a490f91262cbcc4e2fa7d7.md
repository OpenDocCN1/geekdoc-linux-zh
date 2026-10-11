
上游 Linux 源码包含了构建 Debian 内核包所需的内容，但你仍然需要安装 `build-essential` 包以确保拥有构建 Debian 包所需的工具。此外，内核的配置步骤需要 `libncurses5-dev` 包。最后，`fakeroot` 包将允许在不需要管理员权限的情况下创建 Debian 包。

```
# apt install build-essential libncurses5-dev fakeroot
```

## 9.2.2. 获取源码

由于 Linux 内核源码以包的形式提供，运行 `apt-cache search ^linux-source` 命令应该列出 Kali 封装的最新内核版本。注意，这些包中包含的源码与 Linux Torvalds 和内核开发者在 [https://kernel.org/] 上发布的代码并不精确对应；与所有发行版一样，Debian 和 Kali 应用了许多补丁，这些补丁可能（也可能）进入上游 Linux 版本。这些修改包括来自较新内核版本的修复/功能的回移植（backports）、尚未（完全）合并到上游 Linux 的新功能，甚至是 Debian 或 Kali 特有的更改。

本节其余部分关注 Linux 内核 4.9 版本，但当然，示例可以根据你需要的内核版本进行调整。

在示例中，我们假设已安装 `linux-source-4.9` 二进制包。注意，我们安装的是包含上游源码的二进制包，而没有获取名为 `linux` 的 Kali 包。

```
# apt install Linux-source-4.9
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed: readline7
Suggested packages:
libncurses-dev | curses-dev libqt4-dev
The following NEW packages will be installed: readline7 linux-source-4.9
0 upgraded, 3 newly installed, 0 to remove and not upgraded.
Need to get 95.4 MB of archives.
After this operation, 95.8 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
[...
# ls /usr/src/
linux-config-4.9 linux-patch-4.9-rt.patch.xz linux-source-4.9.tar.xz
```

注意该包包含了 `/usr/src/linux-source-4.9.tar.xz`，这是内核源码的压缩包。你必须在一个新的目录下提取这些文件（不要直接在 `/usr/src/` 下，因为编译 Linux 内核不需要特殊权限）。相反，`~/kernel/` 更合适。

```bash
$ mkdir ~/kernel; cd ~/kernel
$ tar -xaf /usr/src/linux-source-4.9.tar.xz
```

## 9.2.3. 配置内核

下一步根据你的需求配置内核。具体步骤取决于目标。

构建取决于内核配置文件。在大多数情况下，你可能会尽可能保留 Kali 建议的配置，它像所有 Linux 发行版一样被安装在 `/boot` 目录。与其从头开始配置，复制 `/boot/config-version` 文件就足够了（该版本应与当前使用的内核版本相同，可以通过 `uname -r` 命令找到）。将副本放置在包含内核源码的目录中的 `.config` 文件中。

```bash
$ cp /boot/config-4.9.0-kali1-amd64 ~/kernel/linux-source-4.9/.config
```

或者，由于内核在 `arch/configs/*-defconfig` 中提供了默认配置，你可以使用类似命令选择配置位置，例如 `x86_64_defconfig`（针对 64 位 PC）或 `i386_defconfig`（针对 32 位 PC）。

除非你需要更改配置，否则你可以在此停止并跳到 9.2.4 编译并构建软件包。如果你需要进行更改，或者决定从头重新配置，你将需要时间来配置内核。内核源码目录中有各种专用接口，可以通过调用 `make` 命令来使用，其中 target 是下面描述的值之一。

`make menuconfig` 会编译并启动一个文本模式内核配置界面（这需要 `libcurses-dev` 包），允许在分级结构中导航许多可用选项。按空格键更改所选选项的值，并验证屏幕底部选中的按钮；`Select` 进入选中的子菜单；`Exit` 关闭当前屏幕并返回层级上层；`Help` 将显示所选选项的详细信息。方向键允许在选项和按钮列表中移动。要退出配置程序，从主菜单选择 `Exit`。程序随后会提议保存你所做的更改；如果你对选择感到满意，请接受。

其他接口具有类似的功能，但在更现代的界面中工作，例如 `make xconfig`（使用 Qt 界面）和 `make gconfig`（使用 GTK+）。前者需要 `libqt4-dev`，后者依赖于 `libgtk2-dev`。

### 处理过时的 .config 文件

当你提供另一个（通常是旧版本）内核生成的 `.config` 文件时，必须更新它。你可以通过 `make oldconfig`，它将交互式地询问与新配置对应的问题。如果你想对所有问题使用默认答案，可以使用 `make oldconfig`。使用 `make nooldconfig`，它将对所有问题假设否定答案。

## 9.2.4. 编译并构建软件包

### 重建前的清理

如果你已经在目录中编译了内核并希望从头重新构建（例如你大幅更改了内核配置），你需要运行 `make clean` 来删除编译文件。`make distclean` 会删除更多文件，包括你的 `.config` 文件，因此请确保已备份了它。

一旦内核配置就绪，简单的 `make deb-pkg` 将生成五个 `.deb` 格式的 Debian 包：

- `linux-image`：包含内核镜像和相关模块；
- `linux-headers`：构建内核模块所需的头文件；
- `linux-firmware`：某些驱动程序所需的固件文件（当你从 Debian 或 Kali 提供的源码构建时，此包可能缺失）；
- `linux-image-dbg`：包含内核及其模块的调试符号；
- `linux-libdev`：包含某些用户空间库（如 GNU C 库）相关的头文件。

版本由上游版本（由 Makefile 中的 `VERSION`、`PATCHLEVEL`、`SUBLEVEL` 和 `EXTRAVERSION` 定义）、`LOCALVERSION` 配置参数以及 `LOCALVERSION` 环境变量拼接定义。包版本使用相同的字符串，并附加一个经常增加的修订版本（存储在 `.version` 中），除非你用 `PKGVERSION` 变量覆盖它。

```bash
$ make deb-pkg LOCALVERSION=$custom deb_PKGVERSION=$(make kernelversion)-1
[...
$ ls *.deb
../linux-headers-4.9.0-kali1-custom-4.9.2-1_amd64.deb
../linux-image-4.9.0-kali1-custom-4.9.2-1_amd64.deb
../linux-image-4.9.0-kali1-custom-dbg-4.9.2-1_amd64.deb
../linux-libdev-4.9.2-1_amd64.deb
```

要实际构建内核，最后一步是使用 `dpkg -i file*.deb` 安装所需的包。`linux-image` 包是必需的；只有当你需要构建外部内核模块时才需要安装 `linux-headers` 包，在你有某些模块时就是如此。

已安装 `*-dkms*` 软件包（通过 `dpkg -l "*-dkms*" | grep ii` 检查）。其他包通常不需要（除非你明确知道需要它们！）。

## 9.3. 构建自定义 Kali ISO 镜像

Kali Linux 开箱即用提供了极其丰富的功能和灵活性。一旦安装了 Kali，通过少量的引导、创意、耐心和练习，你就可以完成各种惊人的壮举。然而，你也可以创建一个包含特定文件或包的 Kali 构建（以扩展或缩小性能和功能），并能够自动执行某些功能的 Kali 版本。例如，Kali ISO of Doom 和 Kali Evil Wireless Access Point 都是依赖于 Kali Linux 自定义构建实现的优秀项目。让我们来看下制作自定义 Kali Linux ISO 镜像的过程吧。
