
Trailblazer 的工程师正在使用 Embedded Planet RPX-CLLF（PowerPC MPC860）和 Brightstar MediaEngine（ARM SA-1110）。他们找到了两个解释 ARM 和 PowerPC 处理器 GNU 工具链的 HOWTO 文档：

- 针对 ARM 目标的 GNU 工具链 HOWTO：https://www.linux.org/docs/toolchain
- PowerPC 嵌入式系统 Linux HOWTO：http://penguinpc.org/usr/embedded/howto/PowerPC-Embedded-HOWTO.html

通过阅读这些 HOWTO，工程师发现构建一个交叉编译版本的 GNU 工具链是一项复杂的工程。他们首先手动构建了工具链。后来，他们切换了内核版本，发现他们必须重新构建工具链，因为 `gcc` 和 `glibc` 依赖于内核头文件。手动构建工具链既枯燥又容易出错，因此工程师们通过开发名为 `buildtoolchain` 的 `bash` 脚本实现了流程自动化。

`buildtoolchain` 可以构建 PowerPC 和 ARM 交叉编译版本的 `gcc`、`glibc`、`gb`、GNU 实用以及一个 `helloworld` 测试程序。`buildtoolchain` 脚本简化了 `powerpc-linux-gcc`、`arm-linux-gcc`、相应的 `glibc` 库文件以及 `gb` 的编译。`buildtoolchain` 并不是一个单一的脚本，而是简化编译 `powerpc-linux-gcc` 和 `arm-linux-gcc`、相应的 `glibc` 库文件和 `gb` 的集合。由于 `buildtoolchain` 被拆分为多个步骤，当构建失败时可以重新启动。`tbdev1`（一个 400MHz 的 Celeron）运行 `buildtoolchain` 需要超过一小时。

`buildtoolchain` 首先执行 `buildtoolchain-environment` 脚本，它设置了一系列环境变量。`buildtoolchain` 继续执行以下步骤：

- 1. 检查源文件：`buildtoolchain-step01-check`
- 2. 清理旧构建：`buildtoolchain-step02-clean`
- 3. 创建构建目录：`buildtoolchain-step03-makedirectories`
- 4. 构建 `binutils`：`buildtoolchain-step04-binutils`
- 5. 设置内核源和头文件：`buildtoolchain-step05-kernelsource`
- 6. 构建交叉编译版本的 `gcc`：`buildtoolchain-step06-gcc`
- 7. 构建交叉编译版本的 `glibc`：`buildtoolchain-step07-glibc`
- 8. 构建交叉编译版本的 `gdb`：`buildtoolchain-step08-gdb`
- 9. 检查 `gcc` 版本：`buildtoolchain-step09-gccversion`
- 10. 通过交叉编译检查 `helloworld`：`buildtoolchain-step10-helloworld`
- 11. 重新构建 `gcc`：`buildtoolchain-step11-rebuildgcc`
- 12. 重新构建 `glibc`：`buildtoolchain-step12-rebuildglibc`

下文将详细解释每个脚本。

让我们使用 `buildtoolchain` 为 PowerPC 构建工具链，`buildtoolchain` 版本 0.8 为 PowerPC 编译以下版本的 `binutils`、`gcc`、`glibc` 和 `gdb`：

```bash
BINUTILSVERSION=binutils-2.11.2
GCCVERSION=gcc-2.95.3
GLIBCVERSION=glibc-2.2.3
GLIBCCTREADSVERSION=glibc-linuxthreads-2.4.7
KERNELVERSION=linux-2.4.7
GDBVERSION=gdb-5.0
```

首先以 `root` 身份登录 `tbdevi`。创建一个名为 `/root/cross` 的目录并进入该目录。使用 `wget` 获取 `buildtoolchain` 并使用 `tar` 解压所有 `bash` 脚本。最后，带上 `powerpc` 参数运行 `buildtoolchain`。以下是开始所需的 `bash` 命令：

```bash
root@tbdev1[526]: mkdir /root/cross
root@tbdev1[527]: cd /root/cross
root@tbdev1[528]: wget http://www.embeddedlinux.com/chapters/03/buildtoolchain
root@tbdev1[529]: tar xvf buildtoolchain.tar
root@tbdev1[530]: ./buildtoolchain powerpc
```

命令 `buildtoolchain powerpc` 执行针对 PowerPC 的 `buildtoolchain-environment`。本章其余部分将产生超过 8MB 的输出。这时你可能想使用 `tail -f` 在输出文件创建时查看其内容。

### 列表 3.1 续

```bash
### 必须从头开始
### 在 step5 中添加了 targetboard，这可以防止你运行 make
### menuconfig
### 为 arm mediaengine 添加了 KERNELPATCH3，需要 3 个补丁
# d. 内核补丁现在在 linux 目录下通过 patch -p1 完成
### v0.8
### a. 在 step1 中添加了 wget 来获取源码（补丁除外）
### （取决于架构）
### b. 将行参数 ppc 改为 powerpc
```

```bash
set -e
```

```bash
./buildtoolchain-step01-check
buildtoolchain-step02-clean
buildtoolchain-step03-makebuildldirectories
buildtoolchain-step04-binutils
buildtoolchain-step05-kernelsourceheaders
buildtoolchain-step06-gcc
buildtoolchain-step07-glibc
buildtoolchain-step08-gdb
buildtoolchain-step09-gccversion
buildtoolchain-step10-helloworld
buildtoolchain-step11-rebuildgcc
buildtoolchain-step12-rebuildglibc
```

`buildtoolchain` 脚本非常简单；它仅仅调用了 `buildtoolchain` 脚本以及 12 步构建过程的各个脚本。

列表 3.2 的 `buildtoolchain-environment` 脚本要么为 PowerPC/ARM 构建设置环境变量，要么移除之前的安装。如果你想使用不同版本的 GNU 工具或内核，可以修改 `buildtoolchain-environment` 脚本然后运行 `buildtoolchain`。

### 列表 3.2 buildtoolchain-environment 脚本

```bash
#!/bin/bash
### buildtoolchain-environment 10/30/01
### www.embeddedlinuxinterfacing.com
```

### 列表 3.2 续

```bash
# 此脚本原始位置是
### http://www.embeddedlinuxinterfacing.com/chapters/03/buildtoolchain
#

### 版所有 (C) 2001 Craig Hollabaugh
### 参见 buildtoolchain 脚本中的通用公共许可证声明

export SRCIFILELOC=/root/cross
export BUILDLOC=/root/cross/builds
export PREFIX=/usr

case "$1" in
"powerpc" )
  export ARCH=ppc
export TARGET=powerpc-linux
export TARGETBOARD=rpxcliff
export BINUTILSVERSION=binutils-2.11.2
export GCCVERSION=gcc-2.95.3
export GCCPATCH=
export GLIBVERSION=glibc-2.2.3
export GLIBCTREADSVERSION=glibc-linuxthreads-2.4.3
export KERNELVERSION=linux-2.4.7
export KERNELPATCH1=
export KERNELPATCH2=
export KERNELPATCH3=
export GDBVERSION=gdb-5.0
  ;
"arm" )
  export ARCH=arm
export TARGET=arm-linux
export TARGETBOARD=mediaengine
export BINUTILSVERSION=binutils-2.11.2
export GCCVERSION=gcc-2.95.3
export GCCPATCH=gcc-2.95.3-diff-010218.bz
export GLIBVERSION=glibc-2.2.3
export GLIBCTREADSVERSION=glibc-linuxthreads-2.2.3
export KERNELVERSION=linux-2.4.2
export KERNELPATCH1=patch-2.4.2-rm1.kz
export KERNELPATCH2=diff-2.4.2-rm1-np2.gz
```

### 列表 3.2 续

```bash
export KERNELPATCH3=patch-2.4.2-rmk1-np2-bse.gz
export GDBVERSION=gdb-5.0
;

"remove-arm"
TARGET=arm-linux
echo Removing $TARGET 文件
rm -rf $BUILDLOC/$TARGET
rm -rf $PREFIX/bin/$TARGET*
rm -rf $PREFIX/$TARGET
rm -rf $PREFIX/src/$TARGET
rm -rf $PREFIX/lib/gcc-lib/$TARGET
rm -rf /usr/man/man1/$TARGET
exit 0

"remove-powerpc"
TARGET=powerpc-linux
echo Removing $BUILDLOC/$TARGET
rm -rf $BUILDLOC/$TARGET
rm -rf $PREFIX/bin/$TARGET*
rm -rf $PREFIX/$TARGET
rm -rf $PREFIX/src/$TARGET
rm -rf $PREFIX/lib/gcc-lib/$TARGET
rm -rf /usr/man/man1/$TARGET
exit 0
;
*)
  echo "用法 $0 arm|powerpc|remove-arm|remove-powerpc"
  exit 1
esac
```

echo buildtoolchain environment setup complete

echo

export BUILDTOOLCHAINENV=1

以下章节描述了构建工具链过程中的步骤。

### 步骤 1：检查所需的源文件

在开始构建工具链之前，你需要 `binutils`、`gcc`、`glibc`、`glibc-linuxthreads`、内核源码、`gdb` 以及任何补丁。你可以从以下位置下载，或者让 `buildtoolchain-step01` 为你完成：

| 需要的文件 | 路径 |
| :--- | :--- |
| binutils | ftp://ftp.gnu.org/gnu/binutils |
| 内核 | ftp://ftp.kernel.org/pub/linux |
| gcc | ftp://ftp.gnu.org/pub/gcc |
| glibc | ftp://ftp.gnu.org/pub/glibc |
| glibc-linuxthreads | ftp://ftp.gnu.org/pub/gnu/glibc |
| gdb | ftp://ftp.gnu.org/pub/gnu/gdb |

如果你为 ARM 处理器编译，还需要 ARM 专用的补丁：

| 补丁 | 路径 |
| :--- | :--- |
| 工具链 | ftp://ftp.armlinux.org/pub/toolchain |
| 内核 | ftp://ftp.arm.linux.org/pub/armlinux/source/kernel-patches |
| 内核 | ftp://ftp.netwider.org/ |

列表 3.3 显示的 `buildtoolchain-step01` 脚本会确定所需文件是否存在。如果缺失，该脚本将使用 `wget` 下载它们。

### 列表 3.3 buildtoolchain-step01 脚本

```bash
#!/bin/bash
### buildtoolchain-step01 v0.2 10/30/01
### www.embeddedlinuxinterfacing.com
#
# 此脚本原始位置是
### http://www.embeddedlinuxinterfacing.com/chapters/03/buildtoolchain
#
### 版所有 (C) 2001 Craig Hollabaugh
### 参见 buildtoolchain 脚本中的通用公共许可证声明

if [ ! $BUILDTOOLCHAINENV ];
then
  ./buildtoolchain-environment $1
fi
```

### 列表 3.3 续

```bash
#
### 步骤 1 - 检查源文件
#
echo 步骤 1 - 检查源文件
if [ ! -f $SRCFILELOC/$BINUTILSVERSION.tar.gz ]
then
    echo $BINUTILSVERSION.tar.gz
    wget ftp://ftp.gnu.org/gnu/binutils/$BINUTILSVERSION.tar.gz
fi

if [ ! -f $SRCFILELOC/$GCCVERSION.tar.gz ]
then
    echo $GCCVERSION.tar.gz
    wget ftp://ftp.gnu.org/gnu/gcc/$GCCVERSION.tar.gz
fi

if [ ! -f $SRCFILELOC/$GCCPATCH ]
then
    if [ ! -f $SRCFILELOC/$GCCPATCH ]
then
        echo $GCCPATCH
        exit 1
    fi
fi

if [ ! -f $SRCFILELOC/$GLIBVERSION.tar.gz ]
then
    echo $GLIBVERSION.tar.gz
    wget ftp://ftp.gnu.org/pub/glibc/$GLIBVERSION.tar.gz
fi

if [ ! -f $SRCFILELOC/$GLIBCTREADSVERSION.tar.gz ]
then
    echo $GLIBCTREADSVERSION.tar.gz
    wget ftp://ftp.gnu.org/pub/gnu/glibc/$GLIBCTREADSVERSION.tar.gz
fi

if [ ! -f $SRCFILELOC/$KERNELVERSION.tar.gz ]
then
    echo $KERNELVERSION.tar.gz
    wget ftp://ftp.kernel.org/pub/linux/$KERNELVERSION.tar.gz
fi
```

echo 步骤 1 - 完成

echo

### 步骤 2：清理

`buildtoolchain-step02-clean` 脚本移除旧版本的工具链二进制文件、库、临时内核文件以及任何帮助页（即手册）。列表 3.4 显示了 `buildtoolchain-step02-clean` 脚本。当该脚本完成后，工作站即可准备好构建工具链。

### 列表 3.4 buildtoolchain-step02-clean 脚本

```bash
#!/bin/bash
### buildtoolchain-step02-clean v0.1 8/16/01
### www.embeddedlinuxinterfacing.com
#
# 此脚本原始位置是
### http://www.embeddedlinuxinterfacing.com/chapters/03/buildtoolchain

### 版所有 (C) 2001 Craig Hollabaugh
### 参见 buildtoolchain 脚本中的通用公共许可证声明

if [ ! $BUILDTOOLCHAINENV ]
then
    ./buildtoolchain-environment $1
fi

### 步骤 2 - 清理
#
### 在我们开始之前清理，这只清理 TARGET
echo 步骤 2 - 清理
echo Removing $TARGET 文件
rm -rf $BUILDLOC/$TARGET
rm -rf $PREFIX/bin/$TARGET*
rm -rf $PREFIX/$TARGET
rm -rf $PREFIX/src/$TARGET
rm -rf $PREFIX/lib/gcc-lib/$TARGET
rm -rf /usr/man/man1/$TARGET
```

echo 步骤 2 - 完成
