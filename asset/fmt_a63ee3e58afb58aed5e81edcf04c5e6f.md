
<Select>  < Exit  < Help  < Save  < Load >

![](img/6f792577a28af84c82be0eef5006ef77_35_0.png)

## 5) 检查 Petalinux 包组 (Package Groups) -> `packagegroup-petalinux-qt`，配置 qt 库

```
/home/alinx2020/peta_prj/LinxPsBase/petalinux-sdk/project-spec/configs/rootfs_c
-o- Petalinux_Package_Groups +packagegroup-petalinux-qt
packagegroup-petalinux-qt
```

使用方向键导航菜单 --<Enter> 选择子菜单 ---> (或空子菜单 ---)。高亮的字母为热键。按 <Y> 包含，按 <N> 排除，按 <M> 模块化。按 <Esc><Esc> 退出，按 <?> 帮助。图例：[*] 内置 [ ]

```
[[*] packagegroup-petalinux-qt
[ ] packagegroup-petalinux-qt-dev
[ ] packagegroup-petalinux-qt-dbg
[+] populate_sdk_qt5
```

<Select>  < Exit  < Help  < Save >< Load >

![](img/6f792577a28af84c82be0eef5006ef77_35_1.png)

## 6) 检查 Petalinux 包组 (Package Groups) -> `packagegroup-petalinux-v4lutils` 以配置 v4l 工具。这主要是一个 Linux 上的视频配置工具，可用于视频开发。

36 / 91 Amazon Store: https://www.amazon.com/alinx

```
/home/alinx2020/peta_prj/linux.edb/petalinux/project-spec/configs/rootfs_conf-
petalux Package Groups -> packagegroup-petalinux-v4utils
packagegroup-petalinux-v4utils
```

使用方向键导航菜单。<Enter> 选择子菜单 --> (或空子菜单 .... 高亮的字母为热键。按 <Y> 包含，排除更多功能。按 <Esc> 退出，按 <?> 帮助，/ 搜索。图例：[*] 内置 []

```
[*] packagegroup-petalinux-v4utils
[] packagegroup-petalinux-v4utils-dbg
[] packagegroup-petalinux-v4utils-dev
```

<Select>          < Exit >< Help >< Save >< Load >

## 7) 检查 Petalinux 包组 (Package Groups) -> `packagegroup-petalinux-x11` 以配置 x11 库

```
/home/alinx2020/eta_prj/linux/petalinux_sdk/project-spec/configs/rootfs_config-
petalux Package Groups -> packagegroup-petalinux-x11
packagegroup-petalinux-x11
```

使用方向键导航菜单。<Enter> 选择子菜单 --> (或空子菜单 ....)。高亮的字母为热键。按 <Y> 包含，<N> 排除，<M> 模块化。按 <Esc> 退出，按 <?> 帮助，/ 搜索。图例：[*] 内置 [ ]

```
module
[*] packagegroup-petalinux-x11
[] packagegroup-petalinux-x11-dev
[] packagegroup-petalinux-x11-dbg
```

<Select>          < Exit >< Help >< Save >< Load >

## 8) 检查文件系统包 (Filesystem Packages) -> `libs-alinx` 以配置 GPU 库

37 / 91 Amazon Store: https://www.amazon.com/alinx

```
/home/alinx2020/petalinux_prj/linux_Base/petalinux_sdk/project-spec/configs/rootfs_config/
Filesystem Packages -> libs-alinx
```

使用方向键导航菜单。<Enter> 选择子菜单 ---> (或空子菜单 ...) 高亮的字母为热键。按 <Y> 包含，<X> 排除，<M> 模块化。按 <Esc><Esc> 退出，<?> 帮助， </> 搜索。图例：[*] 内置 [ ] 排除 <M> module

```
[*] alinx-linux
[*] alinx-linux-dbg
[*] alinx-linux-dev
[*]-defaults (x11)
```

<Select>          < Exit >< Help >< Save >< Load >

## 9) 编译 petalinux 项目

```bash
petalinux-build --sdk
```

### 第 6 部分：安装 SDK

你可以在 `images/linux` 目录下找到生成的 `sdk.sh` 文件。该文件较大且不是文本文件。它包含一个交叉编译器、各种库和头文件。它非常有用。如果你只需要做 Linux 应用，需要一个 `sdk.sh` 文件（注：原文为“如果你只需要做 Linux 应用，需要一个 sdk.sh 文件，这可以从 Petalinux 和 Vitis 分离”）。

![](img/6f792577a28af84c82be0eef5006ef77_38_0.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_1.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_2.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_3.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_4.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_5.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_6.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_7.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_8.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_9.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_10.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_11.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_12.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_13.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_14.png)
![](img/6f792577a28af84c82be0eef5006ef77_38_15.png)

```
petalinux.cfg
bl31.bin
bl31.elf
BOOT.BIN
rootfs.cpio
rootfs.cpio.gz
rootfs.cpio.gz-boot
rootfs.jff
sdk.sh
system.bit
system.dtb
System.map.linux
zynqmp_fsblelf
zynqmp-qemu-arm-dt
```

2) 安装 sdk，它提示默认安装在 `/opt/petalinux/2020.1`。按回车并输入 Y 安装到默认目录。安装完成后，它提示
`source /opt/petalinux/2020.1/environment-setup-arch64-xinx-linux`
你可以使用 SDK

```
alinx2020@ubuntu:~/peta_prj/linux_sdk/images/linux$ ./sdk.sh
Petalinux SDK installer version 2020.1
=====================
Enter SDK 的目标目录 (默认: /opt/petalinux/2020.1):
你想将 SDK 安装到 "/opt/petalinux/2020.1"吗？继续 [Y/n]? y
```
