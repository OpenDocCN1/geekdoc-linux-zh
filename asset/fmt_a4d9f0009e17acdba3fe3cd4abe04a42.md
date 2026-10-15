
```
lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 base64 -> busybox

-lrwrxwrfwx 1 qemu qemu 1023344 Nov 9 17:43 busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 cat -> busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 chattr -> busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 chgrp -> busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 chnod -> busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 chown -> busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 conspy -> busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 cp -> busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 ctyhtack -> busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 date -> busybox

-rwxr-xr-x 1 qemu qemu 207552 Nov 10 09:47 dbclient

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 dd -> busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 df -> busybox

-lrwrxwrfwx 1 qemu qemu 7 Dec 19 09:41 dmesg -> busybox
```

我们将在实践课程中看到如何制作任何命令。但现在，只需要理解所有这些东西都是派生自`busybox`。现在我们回到原始幻灯片。`busybox`中的工具提供的选项通常比其功能完整的GNU兄弟版本少。这意味着如果我们在使用`busybox`中的某些工具，同时直接使用某些工具（或者说功能性工具），它们将是类似的，但对于高级用户，你可能会看到一些差异。不过对于普通用户来说没关系。这就是为什么它被称为选项比功能完整的GNU兄弟版本少。对于小型系统，或者你可以说是空间受限的嵌入式平台，`Busy Box`提供了几乎所有我们需要的环境，我们可以说一个`Busybox`就足以满足我们嵌入式平台的大部分需求。`Busybox`基本上在编写时考虑了尺寸和有限的资源。它具有极强的模块化方法。你可以轻松地包含或排除其中的一个包。我们将查看如何创建一个可以运行的系统。对于运行系统，我们需要`bin`文件夹、`sbin`文件夹、`dev`文件夹等。

这些内容可以创建，但`busybox`提供了我们的`bin`文件夹、`sbin`文件夹和配置文件。除此之外，我们需要创建设备节点、`proc`、`sys`，就可以了。只需在启动时包含Linux内核和引导程序，你的系统就准备好部署了。在`busybox`中，你将获得像`menuconfig`这样的功能（我们在Linux内核中见过它），它可以让我们灵活地包含或排除特定的包。默认情况下，大多数常用工具都会被包含。

- `BusyBox`的编写考虑了尺寸优化和有限的资源。
- 它也具有极强的模块化特征，因此你可以在编译时轻松地包含或排除命令（或功能）。
- 这使得自定义你的嵌入式系统变得简单。
- 要创建一个运行的系统，需要在`/dev`中添加一些设备节点，在`/etc`中添加一些配置文件，以及Linux内核和引导程序 (`u-boot`)。
- `Busybox`提供类似`menuconfig`的功能来包含或排除特定包。
- `Busybox`存在于所有的Linux发行版中。大多数基础命令都来自`busybox`。

我们不需要担心包含什么和不包含什么。对于高级用户，我们需要包含它，它默认不会被包含。`Busybox`几乎出现在所有的Linux发行版中。大多数基础命令都来自`busybox`。

你会看到它已经将目标位置更改为`busybox`的上一个文件夹。现在我很了。现在我们的配置文件已经创建了，如果你想看的话，这就是我们的配置文件，正如我们已经看到的在Linux构建中创建了`.config`文件。所以这种方法是类似的吗？现在我们可以编译了。要进行编译只需去掉`menuconfig`和`option`，它将并行编译并安装。按回车，它会做什么呢？它将在目标文件夹中编译并安装。现在`busybox`已经完全编译并安装到`rootfs`目录。进入`rootfs`目录查看它是否安装正确。等一下，进入`rootfs`目录查看它是否安装正确。记得我们选择了`.`，这意味着`rootfs`的上级目录，查看它是否已构建，这样我们就能看到`bin`、`sbin`和`usr`文件夹被创建。这些都是`rootfs`的主要文件夹。这个项目就此结束，在下一个项目中我们将学习如何使用`dropbear`作为`ssh`工具，因为`dropbear`是轻量级的。

## DROPBEAR 轻量级 SSH 客户端工具

在今天的项目中，我们将学习`dropbear`。`dropbear`基本上是一个轻量级的`ssh`客户端和服务器工具，它是`openssh`服务器的替代品之一。让我们从基础开始。`dropbear`是一个相对较小的`ssh`服务器和客户端。它运行在多种基于`posix`的平台上，基本上适用于大多数嵌入式平台，如无线路由器等许多平台。它具有与`openssh`服务器类似的认证过程。它支持`X11`转发，并具有与`openssh`服务器相似的功能。现在我们将进入实操阶段。在实操阶段中，首先我们需要满足前提条件，即设置工具链并获取`dropbear`的`tar`包。现在我将复制前三行。这是设置工具链所需的命令，你已经知道了。只需复制并输入到这里。只需检查一下你的工具链是否设置正确，输入`arm`并按补全键。所以我们的交叉工具链已设置正确。现在是下载`tar`包的时间。我已经下载好了，我不再重复下载。这就是那个文件。

### 教程文档 - 第 1 页

```bash
export ARCH=arm
export PATH=$PATH:/home/qemu/ripi/demo/tools-master/arm-bcm2708/arm-linux-gnueabihf/bin
export CROSS_COMPILE=arm-linux-gnueabihf/
```

```bash
wget http://matt.ucc.sn.au/dropbear/releases/dropbear_0.53.1.tar.gz
tar -xvf dropbear-0.53.1.tar.gz
cd dropbear-0.53.1
```

```bash
## 配置
./configure --prefix=$SPWD/../rootfs/ --host=arm-linux-gnueabihf --disable-lib CC=arm-linux-gnueabihf-gcc LDFLAGS=-Wl,--gc-sections -ffunction-sections -fdata-sections -O2
```

```bash
## 编译
make PROGRAMS="dropbear dbclient dropkey dropbearconvtt" -j1
```

```bash
## 安装
make install
```

只需复制并粘贴到你的终端。`wget`是一个让我们能够直接从互联网获取包的命令。无需访问浏览器，我们可以使用`wget`工具进行下载。只需将其复制并粘贴到你的终端，你就准备好了，按回车执行即可。由于我已经下载过了，我将不再重复下载。下载完成后，我们需要解压它。只需输入`ls`查看是否下载正确。现在我们需要解压它。正如我们所知，解压`tar`包文件需要提供`tar -x vf 文件名`。它会进行解压。现在解压完成。现在我们将进入`dropbear`目录完成其余工作。

```bash
qemu@genu-Virtuali:~/rpi/rpl/denmo/rootfs$ ls busybox
qemu@genu-Virtuali:~/rpi/rpl/denmo/rootfs$ export ARCH=arm
qemu@genu-Virtuali:~/rpi/rpl/denmo/rootfs$ export PATH=$PATH:/home/qemu/rpl/denmo/tools-master/
qemu@genu-Virtuali:~/rpi/rpl/denmo/rootfs$ export CROSS_COMPILE=arm-linux-gnueabihf/
qemu@genu-Virtuali:~/rpi/rpl/denmo/rootfs$ ls
arm2hdl
arm-linux-gnueabihf-gcov      arm-linux-gnueabihf-ld
arm-linux-gnueabihf-as       arm-linux-gnueabihf-prof
arm-linux-gnueabihf-ld      arm-linux-gnueabihf-strip
arm-linux-gnueabihf-cc       arm-linux-gnueabihf-ldd
arm-linux-gnueabihf-cstrip  arm-linux-gnueabihf-nm
arm-linux-gnueabihf-fstrip arm-linux-gnueabihf-objcopy
arm-linux-gnueabihf-ct-ng.config arm-linux-gnueabihf-objdump
arm-linux-gnueabihf-static  arm-linux-gnueabihf-pickle
arm-linux-gnueabihf-gcc-4.9  arm-linux-gnueabihf-readelf
arm-linux-gnueabihf-ar       arm-linux-gnueabihf-size
arm-linux-gnueabihf-strip  arm-linux-gnueabihf-strings
arm-linux-gnueabihf-gcc-arlib arm-linux-gnueabihf-strip
qemu@genu-Virtuali:~/rpi/rpl/denmo/rootfs$ tar -xvf dropbear-0.53.1.tar.gz -C rootfs busybox
```

首先我们需要在这里进行配置。我们唯一需要正确设置的是`rootfs`路径，即`pwd`，然后是我们已经为`busybox`设置的`rootfs`。进入`dropbear`文件夹后，只需复制并运行配置。现在检查所有前提条件是否已设置好。如果未设置，在需要安装特定包时它会报错。由于它没有给我返回任何错误，这意味着配置已经完成。现在是编译它了，只需运行`make`命令即可。由于我们指定了只编译`dropbear`、`dbclient`、`dropkey` `dropbearconvert`，这就是为什么我们在程序中指定了要构建的内容。
