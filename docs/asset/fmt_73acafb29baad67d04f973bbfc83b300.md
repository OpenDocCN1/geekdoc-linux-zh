
如果你未运行 X，可以使用 `config` 或 `menuconfig`。使用 `make config` 会以纯文本问答方式重建内核。从 `/usr/src/linux-2.4*` 输入 `make menuconfig` 可提供菜单驱动界面（在字符终端中运行）。

除了看起来更美观之外，`menuconfig` 和 `xconfig` 内核配置工具还能让你只选择想要更改的内核区域。使用 `make config` 时，你必须逐步浏览每个类别。使用 `xconfig` 工具时，你可以看到类别中所有可用的选择。要注意的是，如果某个类别被关闭，该类别内的选择会被灰显。此外，如果你犯了错误，只需重新选择该类别即可。

> **注意：** 你可能想在此处编辑 Makefile 文件并更改 `EXTRAVERSION` 的值。这可以防止你意外覆盖原始内核文件。新的内核启动后，你可以输入 `uname -a` 查看 `EXTRAVERSION` 的值附加在正在运行的内核名称之后。

### 检查依赖关系

配置内核后，保存更改。在你完成想要的内核配置更改后，必须返回到 `/usr/src/linux*` 目录并输入以下命令：

```
# make dep
```

`make dep` 命令检查软件包的依赖关系是否满足。接下来，你必须准备源树。

### 准备源树

要为新的内核构建准备源树，请按如下方式运行 `make clean` 命令：

```
# make clean
```

### 编译新内核

编译新内核有几种选择。你可以创建新的内核引导映像使其存储在硬盘上，或将其副本放在软盘上。后者适用于测试新内核。你可以在安装前从软盘启动映像，因此如果新内核无法工作，你可以避免安装它。

要编译内核并将其保存到软盘（以及硬盘），请将软盘放入磁盘驱动器并运行：`make zdisk`。要仅将新映像保存到硬盘，请输入 `make zImage` 编译内核。如果 `make zImage` 创建的映像过大，输入以下命令创建更压缩的映像：

```
# make bzImage
```

此过程需要一段时间，请耐心等待。无论如何，映像都放在 `arch/i386/boot` 目录中。生成的文件是一个压缩的引导映像。

### 制作模块

未编译到内核中的模块可使用 modules 选项编译为可加载模块。模块编译完成后，你可以使用 `modules_install` 选项将它们安装到 `/lib/modules/kernel`（其中 `kernel` 替换为代表当前内核的数字）中。输入以下命令：

```
# make modules
# make modules_install
```

要在系统运行时添加模块，可以使用 `modprobe` 或 `insmod` 命令。

### 创建 initrd 映像

如果你的计算机没有 SCSI 适配器，请跳过此步骤。但是，如果你的计算机有 SCSI 适配器并且需要在启动时加载 SCSI 模块，则必须创建 initrd 映像。首先，检查你的 `/etc/modules.conf` 文件是否包含 SCSI 适配器的行。例如：

```
alias scsi_hostadapter aic7xxx
```

接下来，使用 `mkinitrd` 命令构建新映像。`mkinitrd` 命令接受两个选项。第一个指示新映像的名称。第二个指示模块取自的内核（如 `/lib/modules/2.4.18-11`）。例如：

```
# mkinitrd /boot/newinitrd-image 2.4.18-11
```

当你在 `/etc/lilo.conf` 中为此新内核创建条目时，确保向该条目添加新的 initrd 映像。例如：

```
initrd=/boot/newinitrd-image
```
