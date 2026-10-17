
### 步骤 3：创建构建目录

`buildtoolchain-step03-makebuilddirectories` 脚本为 `binutils`、`gcc`、`glibc` 和 `gdb` 创建构建目录（见列表 3.5）。这些目录将包含编译过程中产生的中间对象文件。当 `buildtoolchain` 执行完成后，你可以删除这些构建目录。

## 列表 3.5 `buildtoolchain-step03-makebuilddirectories` 脚本

```bash
#!/bin/bash
# buildtoolchain-step03-makebuild v0.1 8/16/01
### www.embeddedlinuxinterfacing.com
#
# 此脚本原始位置是
### http://www.embeddedlinuxinterfacing.com/chapters/03/buildtoolchain

### 版所有 (C) 2001 Craig Hollabaugh
# 参见我们 buildtoolchain 脚本中的通用公共许可证声明

if [ ! $BUILDTOOLCHAINENV ]
then
    ./buildtoolchain-environment $1
fi

### 步骤 3 - 创建构建目录
#
echo 步骤 3 - 创建构建目录
echo Making build directories in $BUILDLOC

if [ ! -e $BUILDLOC ];
then
    mkdir $BUILDLOC
fi

mkdir $BUILDLOC/$TARGET-binutils
mkdir $BUILDLOC/$TARGET-gcc
mkdir $BUILDLOC/$TARGET-glibc
mkdir $BUILDLOC/$TARGET-gdb

echo 步骤 3 - 完成
echo
```

## 第 3 章 选择平台并安装工具集

### 第 4：构建 binutils

`buildtoolchain-step04-binutils` 脚本构建二进制工具的交叉编译版本（参见列表 3.6）。这些程序在交叉编译过程中用于创建可执行文件。`buildtoolchain-step04-binutils` 脚本执行以下操作：

- 1. 它从构建目录中的 tar 文件提取 `binutils` 源码。
- 2. 它从构建目录运行配置（configuration）。
- 3. 它制作二进制工具。
- 4. 它安装 `binutils` 工具。这些 `binutils` 是用于处理 PowerPC 二进制文件的 x86 可执行文件。它们安装在 `/usr/bin` 中，但带有前缀 `powerpc-linux`。
- 5. 它清理构建目录。
- 6. 它列出在 `/usr/bin` 目录中已构建和安装的内容。

### 列表 3.6 `buildtoolchain-step04-binutils` 脚本

```bash
#!/bin/bash
### buildtoolchain-step04-binutils v0.1 8/16/01
### www.embeddedlinuxinterfacing.com

# 此脚本的原始位置
### http://www.embeddedlinuxinterfacing.com/chapters/03/buildtoolchain

# Copyright (C) 2001 by Craig Hollabaugh
# See buildtoolchain script for General Public License statement

if [ ! $BUILDTOOLCHAINENV ]; then
then
  ./buildtoolchain-environment $1
fi

#
### Step 4 - Build binutils
#
echo Step 4 - Build binutils
echo Building $BINUTILSVERSION for $TARGET
cd $BUILDLOC
tar zxf $SRCFILE/$BINUTILSVERSION.tar.gz
```

# 列表 3.6 继续

```bash
cd $TARGET-binutils
../$BINUTILSVERSION/configure --target=$TARGET --prefix=$PREFIX -v
make
make install
```

```bash
cd $BUILDLOC
rm -rf $TARGET-binutils
rm -rf $BINUTILSVERSION/bin/$TARGET-*
```

`echo -1 Step 4 - Complete`

`echo`

以下是 `buildtoolchain-step04-binutils` 的输出，它列出了 `powerpc-linux` `binutils`：

```
/usr/bin/powerpc-linux-addr2line
/usr/bin/powerpc-linux-ar
/usr/bin/powerpc-linux-as
/usr/bin/powerpc-linux-c++c
/usr/bin/powerpc-linux-gdb
/usr/bin/powerpc-linux-ld
/usr/bin/powerpc-linux-nm
/usr/bin/powerpc-linux-objcopy
/usr/bin/powerpc-linux-objdump
/usr/bin/powerpc-linux-ranlib
/usr/bin/powerpc-linux-readelf
/usr/bin/powerpc-linux-size
/usr/bin/powerpc-linux-strings
/usr/bin/powerpc-linux-strip
```

### 第 5：设置内核源码和头文件

交叉编译 `gcc` 和 `glibc` 需要内核头文件。`buildtoolchain-step05-kernelsourceheaders` 执行以下步骤来准备内核头文件（参见列表 3.7）：

- 1. 它在构建目录中提取内核。
- 2. 它应用任何补丁（patches）。
- 3. 它保留预先存在的内核配置文件 `.config`。
- 4. 它删除预先内核源码目录。
- 5. 它将新创建的内核目录从构建目录移动到 `/usr/src`。
- 6. 它将保存的 `.config` 文件复制到新内核源码目录中的 `config.original`。
- 7. 它修改顶层内核 `Makefile`，为正在构建的架构更改 `ARCH` 和 `CROSS_COMPILE` 语句。
- 8. 它使用来自 `arch` 目录的默认目标板配置配置内核源码和头文件。
- 9. 它执行 `mrproper` 和 `dep`。
- 10. 它创建内核头文件，这些头文件包含了交叉编译过程所需的目录。

# 列表 3.7 `buildtoolchain-step05-kernelsourceheaders` 脚本

```bash
#!/bin/bash
# buildtoolchain-step05-kernelsourceheaders v0.1 8/16/01
### www.embeddedlinuxinterfacing.com

# 此脚本的原始位置
### http://www.embeddedlinuxinterfacing.com/chapters/03/buildtoolchain

# Copyright (C) 2001 by Craig Hollabaugh
# See buildtoolchain script for General Public License statement

if [ ! $BUILDTOOLCHAINENV ]
then
  ./buildtoolchain-environment $1
fi

## Step 5 - Setup Kernel Source and Headers
#
echo Step 5 - Setup Kernel Source and Headers
echo Setting up $KERNELVERSION source and headers for $TARGET
cd $SRCFILELOC

echo Removing $SRCFILELOC/linux
rm -rf $SRCFILELOC/linux
```

```bash
echo Extracting $KERNELVERSION.tar.gz

tar zxf $KERNELVERSION.tar.gz

cd linux

if [ $KERNELPATCH1 ]

then

    echo Patching with $KERNELPATCH1

gzip -cd ../$KERNELPATCH1 | patch -p1

fi

if [ $KERNELPATCH2 ]

then

    echo Patching with $KERNELPATCH2

gzip -cd ../$KERNELPATCH2 | patch -p1

fi

if [ $KERNELPATCH3 ]

then

    echo Patching with $KERNELPATCH3

gzip -cd ../$KERNELPATCH3 | patch -p1

fi
```

```bash
### save the existing kernel configuration if it exists

cd $SRCFILELOC

if [ -f $PREFIX/src/$TARGET/.config ]

then

    echo Saving $PREFIX/src/$TARGET/.config

    mv $PREFIX/src/$TARGET/.config /tmp/config.original
```

```bash
# remove all the exist kernel source code for this target

echo Removing $PREFIX/src/$TARGET

rm -rf $PREFIX/src/$TARGET
```

```bash
# Creating $PREFIX/src/$TARGET

mv linux $PREFIX/src/$TARGET
```

```bash
cd $PREFIX/src/$TARGET

if [ -f /tmp/config.original ]

then

    echo Saving $PREFIX/src/$TARGET/.config.original as $PREFIX/src/$TARGET/config.original

    mv /tmp/config.original $PREFIX/src/$TARGET/config.original
```

### 列表 3.8 续

```bash
ls -l $PREFIX/bin/$TARGET-

echo Step 6 - Complete

echo
```

这里是 `buildtoolchain-step06-gcc` 脚本的列表输出；注意 `/usr/bin/powerpc-linux-gcc` 现在已经存在：

- `/usr/bin/powerpc-linux-addr2line`
- `/usr/bin/powerpc-linux-ar`
- `/usr/bin/powerpc-linux-as`
- `/usr/bin/powerpc-linux-c++filt`
- `/usr/bin/powerpc-linux-gasp`
- `/usr/bin/powerpc-linux-gcc`
- `/usr/bin/powerpc-linux-ld`
- `/usr/bin/powerpc-linux-nm`
- `/usr/bin/powerpc-linux-objcopy`
- `/usr/bin/powerpc-linux-objdump`
- `/usr/bin/powerpc-linux-protoize`
- `/usr/bin/powerpc-linux-ranlib`
- `/usr/bin/powerpc-linux-readelf`
- `/usr/bin/powerpc-linux-size`
- `/usr/bin/powerpc-linux-strings`
- `/usr/bin/powerpc-linux-strip`
- `/usr/bin/powerpc-linux-protoize`

步骤 6 - 完成

## 步骤 7：构建交叉编译版本的 glibc

`buildtoolchain-step07-glibc` 脚本执行以下步骤来构建 `glibc`（参见列表 3.9）：

- 1. 它在构建目录中提取 `glibc` 源码。
- 2. 它在构建目录中提取 `glibc-threads`。
- 3. 它对构建进行配置。
- 4. 它制作一个交叉编译版本的 `glibc`。
- 5. 它安装交叉编译版本的 `glibc`。

### 列表 3.9 `buildtoolchain-step07-glibc` 脚本

```bash
#!/bin/bash

### buildtoolchain-step07-glibc v0.1 8/16/01

### www.embeddedlinuxinterfacing.com

#
# 该脚本的原位置是
### http://www.embeddedlinuxinterfacing.com/chapters/03/buildtoolchain

### 参见 buildtoolchain 脚本中的通用公共许可证声明

if [ ! $BUILDTOOLENV ]; then

  ./buildtoolchain-environment $1

fi

# 步骤 7 - 构建交叉编译版本的 glibc

echo Step 7 - Build a Cross-Compiled Version of glibc

echo Building $GLIBCVERSION for $ARCH

cd $BUILDDIR

tar zf $SRCFILE/$GLIBCVERSION.tar.gz

cd $GLIBCVERSION

tar zxf $SRCFILE/$GLIBC-THREADS.tar.gz

cd ../TARGET-glibc

if [ $ARCH = "arm" ]; then

  CC=$TARGET-gcc $GLIBCVERSION/configure $TARGET

  --build=i586-linux --prefix=$PREFIX/$TARGET --enable-addons

fi

if [ $ARCH = "ppc" ]; then

  # 需要为 powerpc 处理器移除 memset.S

  rm -rf $BUILDDIR/$GLIBCVERSION/sysdeps/powerpc/memset.S

  CC=$TARGET-gcc $GLIBCVERSION/configure $TARGET

  --build=i586-linux --prefix=$PREFIX/$TARGET --enable-addons

fi
```

构建嵌入式 Linux 工作站

```bash
make

make install

echo Step 7 - Complete

echo
```

## 步骤 8：构建交叉编译版本的 gdb

GNU 调试器 `gdb` 用于调试可执行文件。如果你正在调试 PowerPC 或 ARM，你需要一个交叉编译版本的 `gdb`。`buildtoolchain-step08-gdb` 脚本执行以下步骤来构建 `gdb`（参见列表 3.10）：

- 1. 它在构建目录中提取 `gdb` 源码。
- 2. 它对构建进行配置。
- 3. 它制作一个交叉编译版本的 `gdb`。
- 4. 它安装交叉编译版本的 `gdb`。
- 5. 它列出在 `/usr/bin` 目录中被构建和安装的内容。

### 列表 3.10 `buildtoolchain-step08-gdb` 脚本

```bash
#!/bin/bash

### buildtoolchain-step08-gdb v0.1 8/16/01

### www.embeddedlinuxinterfacing.com

#
# 该脚本的原位置是
### http://www.embeddedlinuxinterfacing.com/chapters/03/buildtoolchain

### 参见 buildtoolchain 脚本中的通用公共许可证声明

if [ ! $BUILDTOOLCHAINENV ]; then

  ./buildtoolchain-environment $1

fi

# 步骤 8 - 构建交叉编译版本的 gdb

echo Step 8 - Build Cross-Compiled Version of gdb

echo building $GDBVERSION

cd $GDBDIR

rm -rf $GDBVERSION

tar zxf $SRCFILEDIR/$GDBVERSION.tar.gz

cd $TARGET-gdb

../GDBVERSION/configure --target=$TARGET --prefix=$PREFIX -v

make

make install

ls -1 $PREFIX/bin/$TARGET-*

echo Step 8 - Complete

echo
```
