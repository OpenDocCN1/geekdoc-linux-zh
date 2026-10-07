
`$ PATH=/usr/local/oorece-i686/sysroots/i686-angstromdk-linux/usr/bin/armv7a-android-linux-gnueababi:$PATH`

`$ export ARCH=arm`

`$ export CROSS_COMPILE=arm-angstrom-linux-gnueababi-`

`$ make defconfig`

`$ make`

`$ make install`

注意，在最后阶段 busybox 被安装到了 `_install` 目录中。接下来，你需要将这些文件拷贝到 SD 卡中。你将在 Android 安装之后作为一个独立的阶段进行此。Busybox 将位于 `/system/gnu`，并且 `/bin`, `/sbin`, `/usr/bin`, `/usr/sbin` 和 `lib` 会指向该目录的符号链接。

将 SD 卡插入读取器。在系统分区中创建一个名为 'gnu' 的子目录。

```
$ sudo cp -a _install/* /media/system/gnu
$ cp -a /usr/local/oorece-i686/sysroots/armv7a-angstrom-linux-gnueababi/lib /media/system/gnu
```

## LF315 深入 Android：Android 内部原理

向 `init.am335xvm.rc` 添加以下行以创建符号链接并将 busybox 添加到路径

on init

```
symlink /system/gnu/bin /bin
symlink /system/gnu/usr /usr/bin
symlink /system/gnu/usr/sbin /usr/sbin
symlink /system/gnu/lib /lib
export PATH /sbin:/vendor/bin:/system/sbin:/system/bin:/system/xbin:/bin:/usr/bin:/usr/bin
```

编译 Android 并像以前一样将新的 ramdisk 拷贝到启动分区。

启动 Beaglebone 并验证你是否可以使用 `grep`, `cp`, `vi` 等 busybox 命令。

## 第 12 节 图形与 OpenGL

![](img/c6f4acfaca4829cadfb14f4d738cba2c_292_0.png)

## 第 12 节：图形与 OpenGL

- Android 和 OpenGL
- EGL
- 图形栈
- 图形驱动
- 设备配置

Copyright © 2013 The Linux Foundation. All rights reserved

## LF315 深入 Android：Android 内部原理

## OpenGL 和 OpenGL ES

- OpenGL 是用于 2D 和 3D 图形的跨平台 API
- 由 Khronos Group 发布的规范
  - http://www.khronos.org/
- OpenGL ES 是为嵌入式设备设计的 OpenGL 子集
- 例如，OpenGL ES 具有：
  - 没有双精度浮点或长整数数据类型
  - 没有四边形或多边形图元：使用三角形代替

![](img/c6f4acfaca4829cadfb14f4d738cba2c_293_0.png)

284

![](img/c6f4acfaca4829cadfb14f4d738cba2c_293_1.png)

## 第 12 节 图形与 OpenGL

![](img/c6f4acfaca4829cadfb14f4d738cba2c_294_0.png)

Copyright © 2013 The Linux Foundation. All rights reserved.

![](img/c6f4acfaca4829cadfb14f4d738cba2c_295_0.png)

- 所有版本的 Android 都支持 OpenGL ES
- 从开始就支持 OpenGL ES 1.0/1.1 Common profile
- 从 API level 8 (Froyo) 开始支持 OpenGL ES 2.0
- 你会在两个地方遇到 OpenGL：
  - 在栈顶端作为 Java API，它们松基于 Java JSR 239（但并非 100% 兼容）
  - 在栈底部作为渲染图形的要手段

## 第 12 节 图形与 OpenGL

## EGL

- EGL 是 Khronos 原生平台图形接口
- 描述 OpenGL ES（以及 OpenVG）如何与底层窗口系统交互
  - 将表面映射到显示器
  - 分配缓冲区
  - 双缓冲和单缓冲表面
  - 显示尺寸、色彩深度等

## EGL 示例 (1)

应用程序使用 EGL 分配窗口缓冲区，然后使用 OpenGL ES 在后缓冲区中绘制一帧

![](img/c6f4acfaca4829cadfb14f4d738cba2c_297_0.png)

## 第 12 节 图形与 OpenGL

![](img/c6f4acfaca4829cadfb14f4d738cba2c_298_0.png)

## LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_299_0.png)

Copyright © 2013 The Linux Foundation.
All rights reserved. DO NOT DISTRIBUTE.

## 第 12 节 图形与 OpenGL

![](img/c6f4acfaca4829cadfb14f4d738cba2c_300_0.png)

## LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_301_0.png)

Copyright © 2013 Linux Foundation. All rights reserved. DO NOT DISTRIBUTE.

## UI 组件

- 典型的 UI 由按钮、菜单等组成
- 这些每一个渲染到 Canvas 并成为应用程序的 Surface
- 有两条渲染路径：
  - Skia - 软件渲染器
  - HWUI - 硬件渲染器
- 使用的是 View 的一个属性
  - `android.view.setLayerType` 设置 `LAYER_TYPE_NONE`、`LAYER_TYPE_SOFTWARE`、`LAYER_TYPE_HARDWARE`

## LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_303_0.png)

## 第 12 节 图形与 OpenGL

![](img/c6f4acfaca4829cadfb14f4d738cba2c_304_0.png)

- JSR 239 是 Java 绑定 OpenGL ES 的 API
  - http://docs.oracle.com/javame/config/cldc/opt-pkgs/api/jb/jsr239/index.html
- EGL
  - `javax.microedition.khronos.egl`
  - EGL
  - EGL0
  - EGL1
- OpenGL
  - `javax.microedition.khronos`
  - GL
  - GL10
  - GL11

## LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_305_0.png)

Copyright © 2013 Linux Foundation.
All rights reserved.

## 第 12 节 图形与 OpenGL

## 图形加速

- 大多数平台都有图形处理器 (GPU)
- 驱动程序通常是厂商特定的
- 大多数平台都有帧缓冲区 (framebuffer)
- EGL 和 OpenGL ES 层
- 首先尝试编号最高的
  - EGL/libELES1/libGLES1
  - /lib/LES2/libGLES2

![](img/c6f4acfaca4829cadfb14f4d738cba2c_306_0.png)

## LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_307_0.png)

## 第 12 节 图形与 OpenGL

![](img/c6f4acfaca4829cadfb14f4d738cba2c_308_0.png)

- `egl.cfg` 文件包含：
  - <显示器编号> <实现>
- 库文件为：

```
0 0
```
- 例如，TI AM335 SoC 有一个 PowerVR SG530 GPU
- `egl.cfg` 将包含：

```
0 0
```
- 所需要的库：
`/system/lib/egl/libEGL.so`
`/system/lib/egl/libGLES1.so`
`/system/lib/egl/libGLES2.so`
（根据 OCR 上文修正）

## LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_309.png)

## 设备配置

- 添加到 `BoardConfig.mk`

```
BOARD_EGL_CFG := device/ti/bebone/egl.cfg
USE_OPENGL_RENDERER := true
```
- 将库拷贝到正确的目录
- 将驱动程序添加到内核配置，或编译为模块并添加到系统镜像

## LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_311_0.png)

- 低级图形缓冲区处理由硬件模块 **gralloc** 执行
- gralloc 实现了两个接口
- framebuffer
  - 映射显示位图内存
  - 见 `hardware/libhardware/include/hardware/fb.h`
- gralloc
  - 分配并管理适用于 2D 和 3D 图形使用的内存
  - 见 `hardware/libhardware/include/hardware/gralloc`

## 内核 framebuffer驱动

- Linux framebuffer 驱动提供了显示位图的标准接口
- 设备 `/dev/fb0` (Android 上的 `/dev/graphics/fb0`)
- 用于读取固定参数的 ioctl 函数
  - 屏幕和缓冲区尺寸等
- 用于读写变量参数的 ioctl 函数
  - 例如用于“平移”显示（确定缓冲区的可见部分）
- `mmap` 函数将缓冲区映射到应用程序地址

![](img/c6f4acfaca4829cadfb14f4d738cba2c_312_0.png)

# LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_313_0.png)

## 第12 节：图形与 OpenGL

### 使用 fbset 进行测试

- 使用 Busybox 中的 fbset 实用
- 注意：帧缓冲区高度为 1600，显示高度为 800
- 像素格式为 RGB 565

```
# fbset -fb /dev/graphics/fb0
mode "480x800-260"
# D: 100.000 MHz, H: 208.333
geometry 480 800 480 1600 16
timeings 10000 0 0 0 0 0
accel false
endmode rgba 5/11,6/5,5/0,0/0
```

![](img/c6f4acfaca4829cadfb14f4d738cba2c_314_0.png)

## LF315 深入 Android：Android 内部原理

## 缓冲区格式

Android 识别以下格式：
- 32 位/像素：
    - `HAL_PIXEL_FORMAT_RGBA_8888`
    - `HAL_PIXEL_FORMAT_RGB_8888`
    - `HAL_PIXEL_FORMAT_BGRA_8888`
- 24 位/像素：
    - `HAL_PIXEL_FORMAT_RGB_888`
- 16 位/像素：
    - `HAL_PIXEL_FORMAT_RGB_565`
    - `HAL_PIXEL_FORMAT_RGBA_4444`

![](img/c6f4acfaca4829cadfb14f4d738cba2c_315_0.png)
![](img/c6f4acfaca4829cadfb14f4d738cba2c_315_1.png)

## 第12 节：图形与 OpenGL

```
gralloc.default
```
- 一个与硬件无关的版本 (`gralloc.default`) 实现在 `hardware/lib/modules` 中
- 典型的厂商实现会提供一个优化的版本，以利用硬件特性

![](img/c6f4acfaca4829cadfb14f4d738cba2c_316_0.png)
![](img/c6f4acfaca4829cadfb14f4d738cba2c_316_1.png)

## 实验 12

## 练习 12.1 旋转立方体

在 `$HOME/embedded-android/resources/lab12/OpenGL-cube` 中有一个旋转立方体演示。将其拷贝到 `aosp/external/OpenGL-cube`，在目标机上编译并安装：

```
cd external/OpenGL-cube
mm
adb remount
adb sync
```

重启目标板并运行演示。

### 练习 12.2 添加 GPU 驱动程序

目前目标机正在使用软件渲染（SurfaceFlinger）。现在你将配置对 PowerVR GPU 的支持。将 `$HOME/embedded-android/resources/lab12/sgx` 拷贝到你的设备目录（即 `/dev/sgx`）。按照幻灯片上的示例创建 `egl.cfg`。

## 第12 节：图形与 OpenGL

在 `BoardConfig.mk` 中添加 `BOARD_EGL_CONFIG` 规则，并将 `USE_OPENGL_RENDER` 设置为 true。

```
service pvr /system/bin/sgx.rc start
```
