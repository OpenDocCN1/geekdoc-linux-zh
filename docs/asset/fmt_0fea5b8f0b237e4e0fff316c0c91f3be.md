
### Automatically generated make config: don't edit
### Code maturity level options
`CONFIG_EXPERIMENTAL=y`

### Processor type and features

### `CONFIG_M386` is not set
### `CONFIG_M486` is not set
### `CONFIG_M586` is not set
### `CONFIG_M586TSC` is not set
`CONFIG_M586=y`
`CONFIG_X86_WP_WORKS_OK=y`
`CONFIG_X86_INVLPG=y`
`CONFIG_X86_BSWAP=y`
`CONFIG_X86_POPAD_OK=y`
`CONFIG_X86_TSC=y`
`CONFIG_X86_GOOD_APIC=y`
...

正如你所见，内容晦涩难懂，并没有描述 `CONFIG` 标签的含义。每条 `CONFIG` 行都指向一个特定的内核配置选项。值 `y` 将该选项编译进内核；值 `m` 则以可加载模块的形式启用该选项。

有些东西可以配置为模块，有些则不能。你只能靠知道哪些是哪些；从 `.config` 文件中看不出这一点。`CONFIG` 标签也很难映射到有意义的信息。

### Building the kernel binary

设置合适的 `.config` 文件是 Linux 内核配置过程中最重要的一部分，但你必须再跳过几个环节才能将该文件变成一个完成的内核。

以下是整个过程的大纲：

- 更改目录 `cd` 到内核源代码目录的顶层。
- 运行 `make xconfig`、`make gconfig` 或 `make menuconfig`。
- 运行 `make dep`（对于 2.6.x 及之后的内核不是必需的）。
- 运行 `make clean`。
- 运行 `make`。
- 运行 `make modules_install`。
- 将 `arch/i386/boot/bzImage` 复制到 `/boot/vmlinuz`。
- 将 `arch/i386/boot/System.map` 复制到 `/boot/System.map`。
- 在 `/boot/grub/grub.conf` 中添加新内核的配置行。

`make clean` 步骤并非总是严格必要，但通常最好从一个干净的构建环境开始。实际上，许多问题都可以追溯到跳过了这一步。

### Adding a Linux device driver

在 Linux 系统中，设备驱动程序通常以三种形式之一分发：

- 针对特定内核版本的补丁
- 可加载模块
- 安装脚本或安装驱动程序的软件包

最常见的是安装脚本或软件包。如果你很幸运地为你的新设备拥有其中之一，你应该能够按照安装新软件的标准流程进行操作。

在你拥有针对特定内核版本的补丁的情况下，在大多数情况下，你可以使用以下流程安装补丁：

```
linux# cd path_to_kernel_src ; patch -p1 < patch_file
```

如果以上两种情况都不适用，你很可能处于必须手动将新设备驱动程序集成到内核源代码树的情况。在接下来的页面中，我们演示如何手动添加一个假设的网络 “snarf” 驱动程序到内核。Linux 实际上让这个过程相当繁琐，尤其是与某些其他版本的 UNIX 相比。

在内核源代码树的 `drivers` 子目录中，找到与你处理的设备类型相对应的子目录。`drivers` 的目录列表如下所示：

```
linux$ ls -F path_to_kernel_src/drivers
acorn/    char/    i2c/     Makefile  net/     s390/    telephony/
acpi/     dio/     ide/     md/      nubus/   sbus/    usb/
atm/      fc4/     ieee1394/ media/   parport/ scsi/    video/
block/    gsc/     input/   message/ pci/     sgi/     zorro/
bluetooth/ hil/     isdn/    misc/    pcmcia/  sound/   
cdrom/    hotplug/ macintosh/ mtd/     pnp/     tc/      
```

最常见的添加驱动程序的目录是 `block`、`char`、`net`、`scsi`、`sound` 和 `usb`。这些目录分别包含块设备（如 IDE 磁盘驱动器）、字符设备（如串口）、网络设备、SCSI 卡、声卡和 USB 设备的驱动程序。其中一些其他目录包含总线本身的驱动程序（例如 `pci`、`nubus` 和 `zorro`）；你不太可能需要向这些目录添加驱动程序。一些目录包含特定平台的驱动程序，例如 `macintosh`、`s390` 和 `acorn`。

由于我们的示例设备是网络相关设备，我们将驱动程序添加到目录 `drivers/net`。我们修改以下文件：

- `drivers/net/Makefile` 以便编译我们的驱动程序
- `drivers/net/Kconfig` 以便我们的设备出现在配置选项中

将驱动程序的 `.c` 和 `.h` 文件放入 `drivers/net/snarf` 后，我们将驱动程序添加到 `drivers/net/Makefile`。我们添加的行（在文件末尾附近）是

```
obj-$(CONFIG_SNA RF_DEV) += snarf/
```

此配置将 `snarf` 驱动程序（存储在 `snarf/` 目录中）添加到构建过程。

在将设备添加到 `Makefile` 之后，我们必须确保在配置内核时可以配置该设备。所有网络设备都必须列在文件 `drivers/net/Kconfig` 中。为了添加设备使其可以作为模块或作为内核的一部分构建（与我们在 `Makefile` 中声明的一致），我们添加以下行：

```
config SNARF_DEV
tristate 'Snarf device support'
```

`config` 之后的第一個标记是配置宏，它必须与 `Makefile` 中 `CONFIG_` 之后的标记匹配。`tristate` 关键字意味着我们可以将设备构建为模块。如果设备不能作为模块构建，我们将使用 `bool` 而不是 `tristate`。下一个标记是字符串，用于

display on the configuration screen. It can be any arbitrary text, but it should identify the device that is being configured.

Having managed to link a new device driver into the kernel, how do you tell the kernel it needs to use the new driver? In kernel versions before 2.6, this was a tedious task that required programming knowledge. As part of the recent architectural changes made to the device driver model, there is now a standard way for drivers to associate themselves with the kernel.

It’s beyond the scope of this chapter to explain how that happens in detail, but the result is that device drivers written for version 2.6 (and later) register themselves with the macro `MODULE_DEVICE_TABLE`. This macro makes the appropriate behind-the-scenes connections so that other utilities such as `modprobe` (discussed in the Loadable kernel modules section starting on page 434) can enable new devices in the kernel.

## 13.4 SOLARIS KERNEL CONFIGURATION
