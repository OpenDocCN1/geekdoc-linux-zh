
这将使 FreeBSD 假设未标记的 ELF 二进制文件使用 Linux ABI，因此你应该可以直接从 CDROM 运行安装程序。

现在，将 Math 文件复制到你的驱动器：

```bash
# mount /cdrom
# cp /cdrom/bin/MathInstaller /compat/linux/
```

等待，基于提供的 OCR 文本，让我们重新对齐碎片文本的逻辑流：

首先，你必须告诉 FreeBSD Mathematica 的 Linux 二进制文件使用的是 Linux ABI。最简单的方法是使用命令将所有未标记二进制文件的默认 ELF 二进制格式设为 Linux：

```bash
# sysctl kern.fallback_elf_brand=3
```

这将使 FreeBSD 假设未标记的 ELF 二进制文件使用 Linux ABI，因此你应该可以直接从 CDROM 运行安装程序。

现在，将 Math 文件复制到你的驱动器：（注意：这里的 OCR 文本非常混乱，我将根据提供的碎片重构可能的预期流）。

当没有安装 `/compat/linux/etc/host.conf` 时，Linux 应用程序会找到 FreeBSD 的 `/etc/host.conf`，并对不兼容的 FreeBSD 语法进行抱怨。如果你没有使用 `/etc/resolv.conf` 文件配置名称服务器，则应该移除 `bind`。

### 10.3.2 修改可执行文件

Mathematica 在安装期间创建的脚本在使用之前必须进行修改。在这些每一个文件中，请将以下内容的 Linux 替换为 FreeBSD：

```bash
cd /usr/local/bin
for i in math mathematica
do
  sed 's/Linux/FreeBSD/g' $i > $i.tmp
  mv $i.tmp $i
done
```

### 10.3.3 获取密码

首次启动 Mathematica 时，会提示密码。如果你没有从 Wolfram 获取，则需要注册。

### 10.3.4 通过网络运行 Mathematica 前端

Mathematica 使用了一些标准字体集中不存在的特殊字符。这些字体必须在本地安装。一种方法是将它们复制到 `/usr/local/share/X11/fonts`。有几种方法可以如下所示：

```bash
cd /usr/local/share/X11/fonts
mkdir Type1
cp /cdrom/Unix/SystemFiles/Fonts/* /usr/local/share/X11/fonts/Type1
mkfontdir
```

现在将新字体目录添加到你的字体路径：

```bash
xset fp+ /usr/local/share/X11/fonts/Type1
xset fp refresh
```
（注：此处原文应为 `xset fp` 逻辑）

如果你使用的是 Xorg 服务器，可以通过修改 `xorg.conf` 来自动加载这些字体。

> 注意：对于 XFree86 服务器，配置文件是 `X86Config`。

如果你没有 `/usr/local/share/X11/fonts/Type1` 目录，可以将上述示例中的目录名称改为 `TypeI`。

### 10.4 安装 Maple™

Aaron Kaplan 提供，感谢 Robert Getschmann。

Maple™ 是一种与 Mathematica 类似的商业数学程序。你必须从 `http://www.mapsoft.com/` 购买此软件并在那里注册许可证文件。要在 FreeBSD 上安装此软件，请遵循以下简单步骤：

- 执行产品发行包中的 `INSTALL` 脚本。在安装程序提示时选择 'RedHat' 选项。典型的安装目录可能是 `/usr/local/maple`。

- 如果你还没有，请从 Maple Waterloo Software (`http://register.mapsoft.com/`) 订购 Maple 许可证并复制到 `/usr/local/maple/license/license.dat`。

- 运行 Maple 自带的 `INSTALL_LIC` 脚本安装 FlexLM 管理器。为许可服务器指定你的主主机名。

- 使用以下内容补丁 `/usr/local/maple/bin/maple.system.type` 文件：

```
*** maple.system.type.orig Sun Jul 8 16:35:33 2001
--- maple.system.type Sun Jul 8 16:35:51 2001
****************
*** ****
 72,77 ****
--- 72,78 ---
```

# IBM RS/6000 AIX 案例

```
MAPLE_BIN=#bin.IBM_RISC_UNIX
;;
"FreeBSD"|\
"Linux"
```

# Linux/x86 案例

# 我们有两个 Linux 实现，一个针对 Red Hat 的，

---- 补丁结束

```

请注意，在对 FreeBSD 进行补丁将 FreeBSD 识别为 Linux 系统类型后，`bin/maple` shell 脚本会调用 `bin/system.type` shell 脚本，后者反过来调用 `uname -a` 来查找操作系统名称。根据操作系统名称，它将确定使用哪些二进制文件。

- 启动许可证服务器。

以下安装在 `/usr/local/etc/rc.d/lmgrd.sh` 的脚本是启动 `lmgrd` 的方便方法：

```
--- snip ---

#!/bin/sh

PATH=$usr/local/sbin:/usr/local/bin:/bin:/usr/bin:/usr/sbin:/usr/bin:/usr/X11R6/bin

PATH=${PATH}:/usr/local/maple/bin:/usr/local/maple/FLEX1m/usr/LINUX

export PATH

LICENSE_FILE=/usr/local/maple/license/license.dat

LOG=/var/log/lmgrd.log

```

```
case "$1" in

start)

lmgrd -c ${LICENSE_FILE} 2>> ${LOG} 1>&2

echo -n * " lmgrd"

;;

stop)

lmgrd -c ${LICENSE_FILE} -x lmdown 2>> ${LOG} 1>&2

;;

*)

echo "Usage: `basename $0` {start|stop}" 1>&2

exit 64

;;

esac

exit 0

--- snip ---
```

- 测试启动 Maple：

```
% cd /usr/local/maple/bin
./maple
```

你现在应该已经可以运行了。如果你想要原生的 FreeBSD 版本，请确保写入 Maples！

### 10.4.1 常见陷阱

- `FLEXim` 许可证管理器可能很难使用的工具。关于该主题的额外文档可以在此处找到：`http://www.globetrotter.com/`。

- `lmgrd` 对许可证文件非常挑剔，如果出现任何问题会导致核心转储（core dump）。正确的许可证文件看起来如下：

```
################
# License File for UNIX Installations ("Pointer File")
################
SERVER chilling any
#USE_SERVER
VENDOR mapleml \
FEATURE Map maple maplelm 2000.0831 permanent 1 XXXXXXXXXXX \
PLATFORMS=i86_r ISSUER="Waterloo Maple Inc." \\
ISSUED=11-may-2000 NOTICE="- Technische Universitat Wien" \\
SN=XXXXXXXXXX
```

**注意：** 序列号和密钥外的 `chilling` 是主机名。

只要你不触碰 `"FEATURE"` 行（该行受许可证密钥保护），编辑许可证文件就是有效的。

### 10.5 安装 MATLAB®

由 Dan Pelleg 贡献。

本文档描述了在 FreeBSD 系统上安装 Linux 版本的 MATLAB® 6.5 的过程。它运行良好，例外是 Java 虚拟机™（见第 10.5.3 节）。

可以直接从 MathWorks 官网 `http://www.mathworks.com` 订购 Linux 版本的 MATLAB。确保你也获取了许可证文件或创建该文件的说明。在联系时，告诉他们你想要该软件的原生 FreeBSD 版本。

### 10.5.1 安装 MATLAB

要安装 MATLAB，请执行以下操作：

- 1. 插入安装 CD 并进入。按照安装脚本的建议切换到 root 用户。要启动安装脚本，输入：
