
## U-Boot 网络启动配置

```
U-Boot > dhcp /* 使用 DHCP 获取 IP 地址 10.0.0.10 */
U-Boot > setenv serverip 10.0.0.1 /* 这是我们的主机 IP 地址 */
U-Boot > setenv image 'zImage' /* 我们的内核镜像名称 */
U-Boot > setenv fdt file 'imx6q-sabresd.dtb' /* 指定设备文件的文件名 */
U-Boot > setenv nfsroot /nfsroot /* nfsroot 是 NFS 服务器的根目录，我们在此解压目标的根文件系统 */
U-Boot > saveenv /* 保存环境变量 */
U-Boot > run netboot /* 启动网络启动 */
```

要在不使用 DHCP 服务器的情况下进行网络启动，请在 U-Boot 提示符设置以下环境变量：

```
U-Boot > setenv serverip 10.0.0.1
U-Boot > setenv ipaddr 10.0.0.1
U-Boot > setenv image 'zImage'
U-Boot > setenv fdt file 'imx6q-sabresd.dtb'
U-Boot > setenv nfsroot /nfsroot
U-Boot > setenv ip_dyn no /* 启动时禁用 DHCP */
U-Boot > setenv narget 'setenv bootargs \
console=console,$(baudrate) $(smp) root=/dev/nfs rootwait \
rw ip=10.0.0.10:10.0.0.1:255.255.255.0:eth0:off \
nfsroot=$(serverip):$(nfsroot),v3,tcp'
U-Boot > saveenv
U-Boot > run netboot
```

# 构建 Linux 内核

内核将在 Yocto 构建系统外部配置和构建。

从 Yocto `tmp` 目录（使用 `bitbake` 构建镜像后生成）中拷贝内核源码到你自己的内核目录：

```
$ mkdir my-linux-imx
$ cp -rpa /fsl-release-bsp/build imx6_qt5 x11/tmp/imx6sabresd-poky-linux-gnuabi/linux-imx/3.14.28-r0/git/* ~/my-linux-imx/
$ cd ~/my-linux-imx/
```

设置 Poky 工具链环境：

```
~/my-linux-imx$ source /opt/poky/1.7/environment-setup-cortex9hf-vfp-neon-poky-linux-gnuabi
```

在编译 Linux 内核之前，确保内核源码是干净的且没有上次构建留下的残留通常是一个好主意：

- `1. clean` - 移除大多数生成的文件，但保留配置和构建外部模块的支持。
- `2. mrproper` - 移除所有生成的文件 + 配置 + 各种备份文件。
- `3. distclean` - `mrproper` + 移除编辑器备份和补丁文件。

```
~/my-linux-imx$ make distclean
```

通常从基础默认配置开始，然后根据需要对其进行定制是最简单的。使用 `imx_v7_defconfig`（位于 `Linux/arch/arm/configs`）作为起点：

```
~/my-linux-imx$ make imx_v7_defconfig
```

当你想自定义内核配置时，最简单的方法是使用内核内置的配置系统。其中最流行的配置系统之一是 `menuconfig` 工具。使用一个未 `source` 过 `environment-cortex9hf-vfp-neon-poky-linux-gnuabi` 的终端。在 `menuconfig` 中使用 "`cd /`" 进行搜索：

```
~/my-linux-imx$ make menuconfig ARCH=arm
```

# Linux/arm 3.14.28 内核配置

```
config Linux/arm 3.14.28 Kernel Configuration
方向键导航菜单，<Enter> 选择子菜单 ---> (或空
子菜单 ----），高亮的字母是热键。按下 <Y>
包含，<N> 排除，<M> 将功能模块化。按下 <Esc><Esc> 
退出，</> 帮助，</> 搜索。图例：[*] 内置 [ ]

General setup
[*] enable module support --->
[*] enable the block layer --->
  System type --->
    us support --->
  Kernel Features --->
    Boot options --->
  FPU Power Management --->
    Floating point emulation --->
    Userspace Binary formats --->

<Select>  < Exit >  < Help >  < Save >  < Load >
```

配置内核设置：

- `1.` 设备树调试，你可以将 `/proc/device-tree` 填充到文件系统。
  - -> `Device Drivers`
  - -> `Device Tree and Open Firmware support`
    - `[*] Support for device tree in /proc`

- `2.` 禁用 `MMA8451` 驱动。你将在其中一个驱动实验中开发自己的 `MMA8451` 驱动。
  - -> `Device Drivers`
  - -> `Hardware monitoring support`
  - `<> MMA8451 device driver`

- `3.` 添加 SPI 设备支持。
  - -> `Device Drivers`
  - -> `SPI support`
  - `<*> User mode SPI device driver support`

- `4.` 检查内核配置中是否选择了输入设备支持。
  - -> `Device Drivers`
  - -> `Input device support`
  - `<*> Input layer (needed for keyboard, mouse)`

- `5.` 启用 I/O 支持。
  - -> `Device Drivers`
  - `<*> I/O support`

## 构建系统

内核编译，必须拷贝到目标文件系统。设备树也应该拷贝到目标文件系统。模块应该安装在目标文件系统中。

![](img/739a35b59067f8a55eff80a58765146f_63_0.png)

要安装模块，使用以下命令：

```
~/my-linux-imx$ source /opt/poky/1.7/environment-setup-cortex9hf-vfp-neon-poky-linux-gnuabi
~/my-linux-imx$ sudo make ARCH=arm INSTALL_MOD_PATH=/nfsroot
```

使用将设备树拷贝到目标文件系统：

```
~/my-linux-imx$ cp arch/arm/boot/imx6q-sabresd.dtb /nfsroot/
```

将内核镜像拷贝到目标文件系统：

```
~/my-linux-imx$ cp arch/arm/boot/zImage /nfsroot/
```

内核、设备树和模块拷贝到目标文件系统后，重启系统。

## 目标文件系统应用程序

开发过程中需要正确安装到 iMX6 文件系统的多个应用程序：

- `1.` `Dropbear` SSH 服务器：

小型 SSH 服务器和客户端。在多种 POSIX 平台上运行。`Dropbear` 是开源软件，采用 MIT 许可发布。它对于嵌入式 Linux（或 Unix）系统（如无线路由器）特别有用。`Dropbear` 软件包包含了安全拷贝 (`scp`) 和安全外壳 (`ssh`) 客户端。更多详情访问 https://matt.asn.au/dropbear/dropbear.html。

- `2.` `I2C-Tools`：

此包包含一组用于 Linux 内核的异构 I2C 工具。这些工具最初是 `lm-sensors` 项目的一部分，但为了方便被分成自己的包。它们在 GNU/Linux 上编译、运行并经过测试。

这些是 I2C 工具包的主要工具：

- `i2cdect`：扫描 I2C 总线设备的用户空间程序。它输出一个包含指定总线上检测到的设备的表格。
- `i2cget`：读取 I2C 总线（或 SMBus）可见寄存器的小型辅助程序。
- `i2cset`：设置 I2C 总线可见寄存器的小型辅助程序。

- `3.` `Evtest`：输入设备事件监控。
