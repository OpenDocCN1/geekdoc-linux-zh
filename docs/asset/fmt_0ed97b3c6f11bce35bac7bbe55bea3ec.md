
![](img/c6f4acfaca4829cadfb14f4d738cba2c_204_0.png)

# LF315 深入 Android：Android 内部介绍

![](img/c6f4acfaca4829cadfb14f4d738cba2c_205_0.png)

- 除了寻找 Android 支持外，你还需要获取一个支持你的 SoC 或设备的内核
- Linaro 提供了支持多个 ARM SoC 的 Android 内核
- 如今大多数硅厂商都提供 Linux 和 Android 支持（但通常比主线落后几个版本）
- 像三星、HTC 等设备制造商有义务根据 GPL 协议发布内核源码

![](img/c6f4acfaca4829cadfb14f4d738cba2c_205_1.png)
![](img/c6f4acfaca4829cadfb14f4d738cba2c_205_2.png)

Copyright © 2013 The Linux Foundation. 保留权利

## 第 9 节 Android 内核

![](img/c6f4acfaca4829cadfb14f4d738cba2c_206_0.png)

- 描述
- 基于事务的进程间通信（IPC）
- 驱动节点：`/dev/binder`
- 驱动信息：`/proc/binder`
- 配置
  - `CONFIG_ANDROID_BINDER_IPC`
- 文件
  - `drivers/staging/android/binder.c`
  - `drivers/staging/android/binder.h`
- 启动所需？是

## 偏态网络（Paranoid network）

- 描述
- 通过 GID 限制对网络字字的访问
- 只有属于特定组的应用程序创建网络连接（查看 `include/linux/android_uid.h`）
- 配置
  - `CONFIG_ANDROID_PARANOID_NETWORK`
- 文件
  - `include/linux/android_uid.h`
  - `net/` 下的各种
- 启动所需？否

## 第 9 节 Android 内核

![](img/c6f4acfaca4829cadfb14f4d738cba2c_208_0.png)

- 描述
- 匿名共享内存（ashmem）允许进程共享段。与 System V 和 POSIX 共享内存类似，不同在于发生 OOM（内存溢出）时可以回收内存。
- 配置
  - `CONFIG_ASHMEM`
- 文件
  - `drivers/staging/android/ashmem.c`
  - `drivers/staging/android/ashmem.h`
- 启动所需？是

## 第 9 节 Android 内核

- 传统上，应用程序通过系统日志 syslogd 将日志消息写入文件
- 这很慢——需要多次任务切换
- 并且向闪存写入日志也很慢且会损坏内存
- Android 日志器（logger）是一个简单的字符驱动程序，写入内存中的环形缓冲区
  - 无需任务切换
  - 无需写入闪存
- 使用 `logcat` 读取日志

LF315 深入 Android：Android 内部介绍

![](img/c6f4acfaca4829cadfb14f4d738cba2c_211_0.png)

- 描述
- 实现了 Android 日志。通过 `/dev/log` 下的设备节点访问
- 配置
  - `CONFIG_ANDROID_LOGGER`
- 文件
  - `drivers/staging/android/logger.c`
  - `drivers/staging/android/logger.h`
- 启动所需？是

## 低内存管理（Low memory）

- 描述
- 当空闲内存通过阈值时，通过杀死具有特定 `oom_adj` 值的进程来实现低内存处理。
- 控制于
  - `/sys/module/lowmemorykiller/parameters/adj`
  - `/sys/module/lowmemorykiller/parameters/minfree`
- 配置
  - `CONFIG_ANDROID_MEMORY_KILLER`
- 文件
  - `drivers/staging/android/memorykiller.c`
- 启动所需？否![](img/c6f4acfaca4829cadfb14f4d738cba2c_212.png)

## 闹钟定时器（Alarm timers）

- 描述
- 与 POSIX 定时器类似，但它们在设备挂起时继续运行
- 通过 `/dev/alarm` 访问
- 配置
  - `CONFIG_ANDROID_ALARM`
- 文件
  - `drivers/staging/android/alarm.c`
- 启动所需？否

## 第 9 节 Android 内核

![](img/c6f4acfaca4829cadfb14f4d738cba2c_214.png)

- 描述
- 在挂起时，在某个内存区域保存数据。通过 `/proc/kmesg` 访问
- 配置
  - `CONFIG_ANDROID_RAM`
- 文件
- `drivers/staging/android/ram_console.c`
- 启动所需？否

## 定时 GPIO（Timed GPIO）

- 描述
- 在某个时间调度特定的 GPIO 设置。即使应用程序被杀死也能确保其关闭
- 配置
  - `CONFIG_ANDROID_TIMED_GPIO`
  - `CONFIG_TIMED_OUTPUT`
- 文件
  - `drivers/staging/android/timed_gpio.c`
  - `drivers/staging/android/timed_output.h`
  - `drivers/staging/android/timed_output.c`
- 启动所需？否

## 唤醒锁（Wake locks）

- 桌面操作系统根据需要（例如关闭笔记本盖子时）挂起
- 手持设备在空闲一段时间后需要更激进的挂起
- 但当应用程序播放音乐或视频时，内核驱动程序需要防止挂起
- 当多个唤醒锁被锁定时，允许进入睡眠状态

![](img/c6f4acfaca4829cadfb14f4d738cba2c_216.png)
![](img/c6f4acfaca4829cadfb14f4d738cba2c_216.1.png)

## 唤醒锁

- 描述
- 持有唤醒锁防止内核进入睡眠状态
- 配置
  - `CONFIG_WAKELOCK`
  - `CONFIG_WAKELOCK_STAT`
  - `CONFIG_USER_WAKELOCK`
- 文件
  - `include/linux/waklock.h`
  - `kernel/power/userlock.c`
  - `kernel/power/welock.c`
  - 需要持有唤醒锁的驱动
- 启动所需？否

## 第 9 节 Android 内核

## 使用 git 查找差异

- 这种技术将显示你的内核与主线稳定树之间的差异
- `git format-patch` 为每个 commit 创建补丁文件

```
$ git clone https://android.googlesource.com/
kernel/goldfish
$ cd goldfish
$ git checkout origin/android-goldfish-2.6.29
$ git remote add stable git://git.kernel.org/pub/scm/
linux/kernel/git/stable/linux-stable.git
$ git fetch stable
$ git format-patch v<kernel-version>..HEAD
```

## 准备编译

- 内核交叉编译需要两个信息
- CPU 架构：`ARCH`
  * `arch/` 目录下的子目录
  * 对于 ARM 处理器
  * `$ export ARCH=arm`
- 交叉编译器前缀：`CROSS_COMPILE`
  * 取决于工具链
  * 对于预编译 Android ARM 工具链：
  * `$ export CROSS_COMPILE=arm-eabi-`

## 编译内核

- 通常内核有超过 1000 个配置选项
- 目标板的默认配置通常存储在 `arch/$ARCH/configs`
  - 例如 Beaglebone Android 的 `am335x_evm_android_defconfig`
- 使用以下设置配置
  - `$ make <config file>`
- 使用这些命令调整配置
  - `make menuconfig`（ncurses 文本菜单）
  - `make xconfig`（使用 Qt 的图形界面）
  - `make gconfig`（使用 Gtk+ 的图形界面）
- 生成的文件
  - `.config`
  - `include/generated/autoconf.h`

# LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_221_0.png)

- 大多数嵌入式设备需要一个纯压缩内核镜像：
  - `$ make zImage`
  - 或者一个压缩的内核镜像加上 U-Boot 头部文件
  - `$ make uImage` (*)
- 对于大多数 x86 系统：
  - `$ make bzImage`
- 内核镜像在 `arch/$ARCH/boot` 中生成

(*) 要创建一个 uimage，你需要 U-Boot `mkimage` 工具，该工具可以通过 Ubuntu 软件包 `u-boot-tools` 获取，或者从 U-Boot 源码编译。

![](img/c6f4acfaca4829cadfb14f4d738cba2c_221_1.png)

# 第 9 节：Android 内核

![](img/c6f4acfaca4829cadfb14f4d738cba2c_222_0.png)

- 内核模块包含可以在启动后加载到内核空间的代码
- 模块的许可协议是模糊的
  - 对 GPL 的严格解读表明，模块应该受相同许可证的
  - 然而，模块包含专有代码是种接受的惯常做法
  - 通常用于 GPU 和 WiFi 适配器的仅二进制驱动程序
- 模块和内核必须使用相同的工具链进行编译，且运行时使用的内核必须与编译时相同，否则模块将无法加载

# 内核模块命令

- `insmod <module file>`: 加载模块
  - 需要 root 权限
- `lsmod`: 列出已加载的模块
- `rmmod <module name>`: 移除（卸载）模块

![](img/c6f4acfaca4829cadfb14f4d738cba2c_223_0.png)

# 第 9 节：Android内核

## 总结

- Android 使用 Linux 内核，并针对移动操作系统的需求进行了少量修改
- 内核源码不是 AOSP 的一部分
- 内核必须与 AOSP 独立编译

![](img/c6f4acfaca4829cadfb14f4d738cba2c_224_0.png)

## 实验 9

### 练习 9.1：编译内核

目标：为 Beaglebone 构建内核

在这种情况下，你只需要从 rowboat 项目获取 Linux 3.2 内核，该内核支持 TI AM355 SoC 并带有 Android 补丁。

```bash
cd ~/embedded-android
git clone git://github.com/rowboat/kernel
cd kernel
git checkout rowboat-am35x-kernel
```

```bash
patch -p1 < ~/embedded-android/resources/lab9/change-default-kernel-to-boot.patch
```

现在进行编译。你需要先 source `envsetup.sh` 并运行 `lunch` 选择 Beaglebone 目标以选取 Android 工具链。然后回到 kernel 目录：

# 第 9 节：Android内核

```bash
export ARCH=arm
export CROSS_COMPILE=arm-linux-gnueabi-
make am335x_evm_android_config
make -j4 uImage
```

检查 `arch/arm/boot/uImage` 的大小：它应该是 4 MiB 左右。

# LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_227_0.png)

# 第 10 节大：启动

- 启动基础
- Fastboot
- U-Boot
- Android init 和 init.rc
- 系统属性

Copyright © 2013 Linux Foundation. 保留所有权利。请勿传播。

# 第 10 节：启动

![](img/c6f4acfaca4829cadfb14f4d738cba2c_228_0.png)

到 Jelly Bean 版本，可以在 `bootable/bootloader/legacy` 找到引导程序代码。某些 Android 设备使用 Little Kernel 引导程序，参见 https://codeaurora.org/tags/little-kernel。`fastboot` 协议定义位于 `bootable/bootloader/legacy/fastboot_protocol.txt`。目前还不确定规范存放在哪里。LINUX FOUNDATION Copyright © 2013 保留所有权利。

## 旧式启动方式

- 引导程序位于已知向量的 NOR flash
- 早期启动设置 SDRAM 并重定位到 RAM
- 主启动代码在 RAM 中运行

![](img/c6f4acfaca4829cadfb14f4d738cba2c_229_0.png)

由于 NOR flash 可以按字节访问并映射到处理器地址空间，代码可以立即执行。

# 第 10 节：启动

### 从 NAND flash 启动

- 不再使用 NOR flash - 太贵
- NAND flash 复杂得多，需要代码运行
- 代码必须存储在某处，通常在 SoC 内部
- 典型序列：
  - 启动代码从 NAND (或 MMC、USB...)加载预启动加载到内部 RAM (SRAM)
  - 预启动加载的大小受 SRAM 限制，通常为 16 KiB .. 128 KiB
  - 预启动加载初始化 SDRAM
  - 将主引导程序加载到 SDRAM 并启动

![](img/c6f4acfaca4829cadfb14f4d738cba2c_230_0.png)

NAND flash 内存只能一次访问一个页面，页面通常为 2048 字节。对 NAND flash 页面的访问是在程序控制下进行的，这在引导阶段会导致鸡生蛋问题。因此， SoC 内部必须有一些代码能够从 NAND flash 加载一个或多个页面。许多 扩展了此代码，能够从 MMC、UART 和 USB 等源加载。### 从 SD

- 在 TI OMAP 和 Sitara 芯片上，启动代码可以从 SDIO (SD 卡)接口加载镜像
- 文件必须命名为 `MLO`
- 它必须存储在卡的第一个分区
- 它必须使用 FAT32 格式

Beagleboard 拥有 Sitara 335x 芯片，其启动代码可以从 MMC（在我们的案例中连接到 SD 卡器）加载。代码非常有限，因此分区格式需要为 FAT32 名称固定为 "MLO"。MLO 二进制文件可以从 U-Boot 源码编译。

## Fastboot

- `fastboot` 可以指三个内容：
  - 一种用于向内存加载和编程镜像的 USB 协议
  - 一个命令行工具
  - 该协议的二进制实现
- 注意：`fastboot` 不是为了启动速度；而是为了加快开发过程

![](img/c6f4acfaca4829cadfb14f4d738cba2c_232_0.png)

## 进入 fastboot 模式

```bash
adb reboot bootloader
```
