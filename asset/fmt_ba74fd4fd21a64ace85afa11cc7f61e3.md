
# 第 3 章 模块 I：基础

列在 `/etc/modules` 中的模块将进行加载（仅给出模块名称）。在 GTO 系统中，`/etc/modules.autoload` 文件起到了这种作用。

对于基于 SUSE 的系统，需要修改的文件是 `/etc/sysconfig/kernel`。

```bash
depmod -a
```

为了让 `depmod` 和 `modprobe` 找到模块，它们必须位于指定的位置，即 `/lib/modules`。`/etc/modprobe.conf` 在每次加载模块或运行 `depmod` 时都会被查询。

当模块在外部目录构建并使用 `modules_install` 目标安装时，它们被放置在模块目录下。

### modprobe

`modprobe` 可以加载（或通过 `-r` 选项卸载）相互依赖的模块堆栈，它可以替代 `insmod`。

它也可以列出模块，这取决于 `/etc/modprobe.conf`。

当添加新模块时，应该运行 `depmod`。

模块包在使用 `insmod` 时使用 `.ko` 扩展，但 `modprobe` 和 `rm` 不需要扩展名。

### lsmod

`lsmod` 输出了所有已加载模块的列表。提供的信息包括名称、大小、计数和引用模块。内容与 `/proc/modules` 相同。

### insmod

`insmod` 将模块加载到运行内核中，并解析所有符号。`-f` 将在内核与模块版本不时不尝试强制加载。`mod` 可以将参数加载到模块。例如：

```bash
insmod my_net_driver.ko irq-10
```

不需要指定 `.ko` 扩展。

### rmmod

`rmmod` 从运行内核中卸载模块。可以像这样给出模块列表：

```bash
rmmod my_net_driver.char_driver
```

### depmod

`depmod` 创建一个类似于 `Makefile` 的依赖文件 `/lib/modules/KERNEL-VERSION-NUMBER`，基于注释行中显式提到的模块或默认路径中的符号。`mod` 允许使用 `modprobe`。它在启动期间一直运行。在某些情况下，它应该

## 3.4 传递参数

传递给模块的参数必须显式标记，并进行类型检查。例如：

```c
int irq = 12;
module_param(irq, int, 0);
```

有许多宏可以使用：

```c
#include <linux/modprobe.h>
```

```c
module_param(name, type, perm)
module_param_array(name, type, perm)
module_param_string(name, type, perm)
```

## 3.5 编译模块

```bash
31

T_S** # 使用线程的用户态程序 (c文件) 列表

T_XX** # 使用线程的用户态程序 (可执行文件) 列表

# 所有目标的列表

# 跳过空目录

if [ "$1" -maxdepth 1 -name *.c -ne "0" ]; then

  echo No such makefile: source exit

fi

CFLAGS="-WWall -Wpedantic" # 用户程序的编译标志

CFLAGS_X="-WWall -Wextra" # 线程用户态程序的的编译标志

fi

# 将默认内核设置为当前运行的内核；否则从

# 第一个命令行参数获取

for name in $*; do

if [ "$KNOOT" = "" ]; then
  KNOOT="/lib/modules/$(uname -r)/build"
  [ -d "$KNOOT" ] && KNOOT="/usr/src/kernels/$(uname -r)"
fi

# 排除带有 NOMAKE 或 .mod.c 文件的文件

if [ "$1" != "*NO*" ] && [ "$1" != "*.mod.c" ]; then

  echo "$1 is being skipped; it is not a module or program

# 如果中止不是源

else

if [ "$1" = "*module.h*" ]; then
  FILENAME="$(basename "$1").c"
fi

else 如果它是一个程序吗？

else

if [ "$1" = "*cpp.h*" ]; then

  FILENAME_EXE="$(basename "$1")"

  T_X_T="$(basename "$1").EXE"

  T_S_T="$(basename "$1").S"

# 如果中止不是源

if [ "$KNOOT" != "" ] && [ ! -f "Makefile" ]; then

  echo "The kernel source directory exists or has no makefile"

fi

# 额外的标志？

U_X_U="$(basename "$name")"
U_S_S="$(basename "$name")"

if [ "$KNOOT" != "" ]; then

  CFLAGS_U="$CFLAGS_U -I$KNOOT/include"

  CFLAGS_X_T="$CFLAGS_X_T -I$KNOOT/include"

fi

CLEANUFF="$U_X $U_S"

# 从 Makefile 中提取内核版本

# 也许没有内核模块

KV_gp=$(grep "VERSION" Makefile | awk '{print $3}');

KG_gp=$(grep "KERNELLEVEL" Makefile | awk '{print $3}');

GS_gp=$(grep "SUBLEVEL" Makefile | awk '{print $3}');

KERNEL_VER_T_X_T="$KV_gp-$KG_gp-$GS_gp"

if [ "$KNOOT" != "" ]; then

  CLEANUFF="$CLEANUFF Module.sys.modules.order"

fi

echo kernel-KERNEL,KERNEL-KV $KERNEL_VER_T_X_T&

if [ "$U_X" != "" ]; then ALL_TARGETS="userprogram"; fi

if [ "$T_X_T" != "" ]; then ALL_TARGETS="threaded"; fi

if [ "$KNOOT" != "" ]; then ALL_TARGETS="modules"; fi

# 检查主发布版本

# 如果你好奇请输出：

if [ "$KNOOT" = "" ]; then

  echo KNOOT is not set 2.6, exiting

fi

echo K_S_K_S ORBJIS_ORBJIS_U_S_U_S U_X_U_X_T_S_T_S T_X_T_X_T

###########################################################################################

我们准备工作完成了，最后构建 Makefile！

fi

# 移除旧内核，构建新内核

# 构建内核和用户态源码及目标列表
```

## 3.6 模块与热插拔

```bash
rm -f Makefile

echo "### Automatic Makefile generation by 'gemmake' script #### Makefile"
echo "### Copyright, Jerry Cooperstein, coop@coop.com/ 2003 - 1029 ######## Makefile"
echo "### License: GPLv2 ###"
################################################################

if [ "$KBUILDSRC" = "tree" ]; then
  echo "### BUILD MODULES" >> Makefile
  echo "### EXPORT KBUILDOUT" >> Makefile
  if [ "$ARCH" = "all" ]; then
    echo "ARCH=ARCH-\$ARCH" >> Makefile
  fi
fi

echo "-clean: ALL" >> Makefile
```
