
| 镜像名称 | 目标 | 提供的层 |
|---|---|---|
| `core-image-minimal` | 仅允许设备启动的小镜像 | `poky` |
| `core-image-base` | 完全支持目标的仅限控制台镜像 | `poky` |
| `core-image-sato` | 带有 Sato 的镜像，为移动设备提供移动环境和视觉样式。该镜像支持 Sato 主题的 X11，包含终端、编辑器和文件管理器 | `poky` |
| `fsi-image-machine-test` | FSI 社区核心镜像，带有控制台环境 - 无 GUI 界面 | `meta-fsl-bsp-release/imx/meta` |
| `fsi-image-gui` | 构建带 GUI 但无 QT 的 Freescale 镜像。此配方适用于 X11、Frame 和 Wayland 的所有后端 | `meta-fsl-bsp-release/imx/meta` |
| `fsi-image-qt5` | 为 X11、Frame Buffer 和 Wayland 后端构建 QT5 镜像 | `meta-fsl-bsp-release/imx/meta` |

在 `meta-fsl-bsp-release` 层中，NXP 提供了新的或更新的机器配置来覆盖 `meta-fsl-arm`。`fsl-setup-release.sh` 脚本将这些文件复制到 `meta-fsl-arm/conf/machine`。以下可以选择机器配置文件：

- `imx6dabsauto`
- `imx6dabsd`
- `imx6qsabsauto`
- `imx6qsabsd`
- `imx6slevk`
- `imx6solosabsauto`
- `imx6solosabsd`
- `imx6xsabsauto`
- `imx6xsabsd`

## 构建系统

`fsl-setup-release.sh` 脚本简化了机器设置。要使用该脚本，需要指定要构建的机器以及图形后端。后端可以是 `x11`、`fb`（帧）或 `Wayland`。

注意：如果你下载的是最后的 NXP BSP 版本，请在 Freescale Yocto Project User's Guide 中检查支持的后端，不再支持 DirectFB。访问 `nxp.com/imxtools` 查看 i.MX 软件和工具。

下面的命令用于为指定的板卡和后端设置目录和配置文件。完成此步骤后，构建环境将初始化并配置用于构建镜像：

```
$ MACHINE=<machine name> source fsl-setup-release.sh -b <build dir> -e <backend>
```

注意：此命令在最后的 BSP 版本中可能不同。请查看 "Freescale Yocto Project User's Guide"。`MACHINE` 机器配置指向 `meta-fsl-arm/conf/machine` 中的文件。设置脚本会检查有效的机器。如果没有设置 `MACHINE`，设置脚本默认认为 `imx6qabsred`。i-MX 机器文件由 `meta-fsl-arm` 目录 提供。`MACHINE` 配置也可以在 `<build dir>/conf/local.conf` 中更改。

以下代码显示了 `fsl-setup-release.sh` 脚本创建的 `local.conf` 文件部分：

```
MACHINE ?= 'imx6qabsred'
DISTRO ?= 'poky'
ACCEPT_FSL_EULA = "1"
```

如果在设置构建目录后打开新的终端窗口或重启机器，应使用环境脚本来设置环境变量并再次运行。不需要完整的 `fsl-setup-release.sh`。

```
~ source setup-environment <bitbake-dir>
```

# 第 1 章

## 构建镜像

`Bitbake` 为开发单个组件提供了多种实用的选项。要带有 `bitbake` 参数运行，命令格式如下：`bitbake <parameter> <component>`

每个组件的构建都包含多个任务，例如获取、配置、打包和部署到目标根目录。`Bitbake` 镜像会收集镜像所需的所有组件，并按照依赖任务的顺序进行构建。首次构建的是工具链以及构建组件所需的所需的工具。可以使用额外的参数执行下面描述的特定活动：

![](img/739a35b59067f8a55eff80a58765146f_48_0.png)

- 如果下载状态未标记为完成，则进行获取。
- 清除整个组件的构建目录。构建目录中的所有更改将丢失。组件的根目录和状态（`state`）也将被清除。组件也会从下载目录中移除。
- 将镜像或组件部署到根目录。
- 即使构建中断也继续构建组件。
- 不建议直接修改 `tmp` 目录下的源代码，但如果确实修改，除非使用此选项，否则 Yocto 项目可能不会重新构建它。使用此选项在镜像部署后强制重新编译。
- 列出镜像或组件的依赖树。
- 开启 3 层深调试。每个 `D` 增加一个调试深度。

你将在 `x11` 后端进行构建。

```
$ MACHINE=imx6qsabred source fsl-setup-release.sh -b build_imx6_qt5_x11 -e x11
$ bitbake fsl-image-qt5
```

`Yocto` 项目在时间和磁盘占用上可能会消耗大量的构建资源，特别是当在多个构建目录中进行构建时。有方法可以优化这一点，例如使用共享 `sstate` 缓存（状态缓存）和共享下载目录（存放下载的包）。可以通过在 `local.conf` 文件中添加类似下方的语句将它们设置为任何位置：

```
DL_DIR="opt/freescale/yoct/imx/download"
SSTATE_DIR="opt/freescale/yoct/imx/sstate-cache"
```

## 构建系统优化

目录需要已经存在并具有适当的权限。当设置了多个构建目录时，共享的 `sstate` 很有帮助，每个目录都使用共享缓存来最小化构建时间。共享下载目录可以最小化获取时间。如果没有这些设置，`Yocto` 项目默认将构建目录作为 `sstate` 缓存和下载目录。当你想从干净状态开始构建时，需要删除 `sstate-cache` 和 `tmp` 目录。

镜像文件定义了放入文件系统中的包。根文件系统、内核、模块和 U-Boot 二进制文件位于 `build/tmp/deploy/images/`。

```
~ cd fsl-release-bsp/build_imx6_qt5_x11/tmp/deploy/images/imx6qsabres/
```

最后我们将镜像加载到内置的 SD 卡中。以下是使用笔记本电脑内置的指令：

```
~/fsl-release-bsp/build_imx6_qt5_x11/tmp/deploy/images/imx6qsabresd$
dmesq | tail
~/fsl-release-bsp/build_imx6_qt5_x11/tmp/deploy/images/imx6qsabresd$ sudo
mount /dev/mmcblk01
~/fsl-release-bsp/build_imx6_qt5_x11/tmp/deploy/images/imx6qsabresd$ sudo
diff if=fsl-image-qt5-imx6qsabresd.sdcard of=/dev/mmcblk0 bs=1M && sync
```

如果你使用外部 USB SD 读器，请使用以下命令：

```
~/fsl-release-bsp/build_imx6_qt5_x11/tmp/deploy/images/imx6qsabresd$ sudo
diff if=fsl-image-qt5-imx6qsabresd.sdcard of=/dev/sd bs=1M && sync
```

在这里，`/dev/sd` 对应于主机系统中分配给 SD 卡设备节点。

## 在 Yocto 之外工作

你可能会发现自己在 Yocto 项目构建系统之外内核内核以及驱动程序和应用程序更加方便。Yocto 项目 SDK 将协助完成这项任务。

什么是 Yocto 项目 SDK？

- 1. 一个交叉编译工具链。
- 2. 两个 `sysroots` 的组合：
    - 针对目标的：包含目标的头文件和库。与其派生的生成的镜像保持一致。
    - 针对主机的：包含主机特有的工具。这些工具在针对目标 `sysroot` 进行构建时能够保持一致性并按预期工作。
- 3. 一个环境脚本，用于设置必要的变量以使它们协同工作。

有几种方法可以使用 Yocto 项目构建系统构建 SDK。`populate_sdk` 任务是构建具有匹配“i.MX6 目标根文件系统”的 `sysroot` 工具链的推荐方法。构建 SDK 的步骤如下：

```
~/fsl-release-bsp/ source setup-environment build_imx6 qt5_x11
~fsl-release-bsp/build_imx6_qt5_x11$ bitbake -c populate_sdk fsl-image-qt5
```
