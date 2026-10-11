
## 在 Yocto 之外操作 HummingBoard

有多种方法使用 Yocto 项目系统构建 SDK。`populate_sdk` 任务是构建匹配“iMX6 目标根文件”的“sysroot”工具链推荐方法。这些是构建 SDK 的步骤：

```bash
~/solidrun-release-bsp/poky$ source oe-init-build-env

~/solidrun-release-bsp/poky/build$ bitbake -c populate_sdk core-image-x11
```

你可以将 `core-image-x11` 替换为你想要 sysroot 的目标镜像：

这将产生一个匹配目标根文件系统的工具链安装程序。生成的工具链和匹配的 sysroot 可以如下安装：

```bash
$ cd ~/solidrun-release-bsp/poky/build/tmp/deploy/sdk/

~/solidrun-release-bsp/poky/build/tmp/deploy/sdk$ . ./poky-glibc-i686-core-image-x11-cortexa9hf-vfp-neon-toolchain-1.8.2.sh
```

注意：脚本在 32 位和 64 位架构中可能不同。

执行脚本：

输入 SDK 目标目录 (默认: `/opt/poky/1.8.2`):
你准备将 SDK 安装到 "/opt/poky/1.8.2"。继续[Y/n]?n
Extracting SDK...done
Setting it up...done
SDK 已成功设置并准备就绪。

## 安装 TFTP 服务器

如果你还没有运行 TFTP 服务器，请按照以下步骤在你的 Ubuntu 14.04 主机上安装并配置 TFTP 服务器：

```bash
~ sudo apt-get install tftpd-hpa
```

`tftpd-hpa` 配置文件安装在 `/etc/default/tftpd-hpa`。默认情况下，它使用 `/var/lib/tftp` 作为根 TFTP 文件夹。使用以下命令更改文件权限以便所有用户访问：

```bash
~$ sudo chmod 1777 /var/lib/tftp
```

## 安装 NFS 服务器

如果你还没有运行 NFS 服务器，请按照以下步骤在你的 Ubuntu 14.04 主机上安装并配置一个：

```bash
~$ sudo apt-get install nfs-kernel-server
```

`/nfssolidrun` 目录将作为 NFS 服务器的根，因此目标根文件系统将从 Yocto 构建目录解压到这里：

```bash
~$ sudo mkdir -m 777 /nfssolidrun

~$ cd /solidrun-release-bsp-poky/build/deploy/images/

solidrun-imx6/core-image-x11-solidrun-imx6.tar.bz2
```

，你将配置 NFS 服务器导出 `/nfssolidrun` 文件夹。编辑 `/etc/exports` 文件并添加下一行：

```
/nfssolidrun* (rw,no_root_squash,async,no_subtree_check)
```

然后重启 NFS 服务器使更改生效：

```bash
~$ sudo service nfs-kernel-server restart
```

## 构建 Linux 内核

从 Yocto tmp 文件夹拷贝到自己的内核文件夹：

```bash
~$ mkdir my-linux-solidrun

~$ cp -rpe ~/solidrun-release-bsp-poky/build/tmp/solidrun_imx6-poky-linux-gnuabi/linux-solidrun-imx6/3.14.1-0r0/git/* ~/my-linux-solidrun/

~$ cd ~/my-linux-solidrun/
```

设置 Poky 工具链环境（包含 `CROSS_COMPILE` 和 `ARCH`）：

```bash
~/my-linux-solidrun$ source /opt/poky/1.8.2/environment-setup-cortexa9hf-vfp-neon-poky-linux-gnu
```

在编译 Linux 内核之前，最好确保内核源码是干净的，并且没有从之前的构建留下的残留：

```bash
~/my-linux-solidrun$ make distclean
```

通常，从基础默认配置开始，然后根据需要为你的用例进行定制是最简单的。你将使用 `imx_v7_cbi_hb_defconfig`（位于 `Linux/arch/arm/configs`）作为起始点：

```bash
~my-linux-solidrun$ make imx_v7_cbi_hb_defconfig
```

当你想自定义内核配置时，最简单的方法是使用内置的内核配置系统。最流行的配置系统之一是 `menuconfig` 实用程序。请使用没有加载过 `environment-setup-cortexa9hf-vfp-neon-poky-linux-gnueabi` 脚本的终端。使用 "cd /" 在 menuconfig 中进行搜索：

```bash
~my-linux-solidrun$ make menuconfig ARCH=arm
```

![](img/739a35b59067f8a55eff80a58765146f_430_0.png)

配置以下内核设置：

1. 对于设备树（Device Tree）调试，你可以将 `/proc/device-tree` 填充到文件系统中。

-> Device Drivers (设备驱动)
-> Device Tree and Open Firmware support (设备树和开放固件支持)
[*] Support for device tree in /proc (支持 /proc 中的设备树)

# 将内核模块移植到 HummingBoard 平台

2. 添加用户 SPI 设备驱动支持。

+ --> Device Drivers
-> SPI support
<*> User mode SPI device driver support (用户模式 SPI 设备驱动支持)

3. 检查内核配置中是否已选择输入设备支持。

+ --> Device Drivers
-> Input device support (输入设备支持)
<*> Generic input layer (needed for keyboard, mouse, ...) (通用输入层（键盘、鼠标等需要))

4. 启用工业 I/O 支持。

+ --> Device Drivers
<*> Industrial I/O support

保存配置。

一旦完成内核配置，就必须对其进行编译，以生成可启动的内核镜像以及选中的任何动态内核模块。默认情况下，U-Boot 期望使用 `zimage` 作为内核镜像。在编译内核之前，确保在使用的终端已加载 `environment-setup-cortex9hf-vf-neon-poly-gnu` 脚本。要仅构建 zimage，使用此命令：

```bash
~my-linux-solidrun$ make zImage
```

从 Linux 内核 3.8 版本开始，每个 ARM* 板板都有一个内核内核所需的唯一设备树二进制文件。因此，你需要为目标设备构建并安装正确的 dtb。所有设备树文件都位于 `Linux/arch/arm/boot/dtts/`。要编译单个设备树，找到你正在使用的板板的 dts 名称，并将 `.dts` 扩展名替换为 `.dtb`。编译后的设备树文件将位于 `Linux/arch/arm/boot/`。然后运行以下命令：

```bash
~my-linux-solidrun$ make imx6q-hummingboard2.dtb
```

默认情况下，大多数 Linux 驱动并没有集成到内核中。这些驱动被编译为动态模块。这将导致 `.ko`（内核对象）文件放置在内核树中。这些 `.ko` 文件就是动态内核模块。每当你对内核进行更改时，通常建议重新构建模块并重新安装内核模块。否则，内核模块可能无法加载或运行。构建这些模块的命令是：

```bash
~my-linux-solidrun$ make modules
```

要一步到位编译内核镜像、模块和所有设备树文件：

```bash
~my-linux-solidrun$ make
```

一旦编译了 Linux 内核、dtb 文件和模块，就必须对其进行安装。对于内核镜像，将通过将 `zimage` 文件复制到读取的位置来安装。设备树二进制文件也应该复制到内核镜像所在的相同目录：

```bash
~my-linux-solidrun$ cp /arch/arm/boot/zImage /var/lib/tftboot
```
