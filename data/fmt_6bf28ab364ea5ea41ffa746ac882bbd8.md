
列表 7-11 显示了`/proc/net/dev`的内容。你可以看到以太网适配器`eth0`和伪网络设备，但没有 SLIP 设备。或者，你可以通过`RPM`检查是否安装了 SLIP。为此，输入以下命令：

```bash
rpm -q -f slip
```

`RPM`告诉你没有安装`slip`包。

没有需要安装的`RPM` SLIP 包。红帽在其基础配置中安装`kernel-modules`包。输入以下命令定位：

```bash
rpm -q -f kernel-modules | grep slip
```

它返回的位置如下：

```
/lib/modules/2.0.31/net/slip.o
```

## 第 7 章：配置 Linux

### 列表 7-11：显示已安装的网络设备

| 接口- | 接收 | 发送 |
| :--- | :--- | :--- |
| 数据包 face errs drop fifo frame | 数据包 errs drop fifo cols carrier | |
| 10: | 561 0 0 0 0 | 561 0 0 0 0 0 |
| eth0: | 17684 12 0 0 12 | 13916 0 0 0 0 0 |

请使用以下命令安装 SLIP 模块：

```
/sbin/insmod /lib/modules/2.0.31/net/slip.o
```

该命令返回了列表 7-12 所示的消息，表明尚未安装所有必要的模块。

### 列表 7-12：insmod 失败，因为 slip.o 依赖于其他模块

```
slip.o: unresolved symbol slhc_free_R3787e5b9
slip.o: unresolved symbol slhc_remember_Rbc0f8a5e
slip.o: unresolved symbol slhc_uncompress_Ra2ca7e0e4
slip.o: unresolved symbol slhc_compress_R5d6838a9
slip.o: unresolved symbol slhc_init_R20741a64
```

没关系。`modprobe`实用程序查看要加载的模块并确定它是否依赖于其他模块。任何依赖模块都会先加载。输入以下命令：

```
/sbin/modprobe /lib/modules/2.0.31/net/slip.o
```

成功后，它不会返回任何消息。输入`insmod`命令以确保模块已加载：

```
/sbin/insmod
```

该命令返回了列表 7-13 所示的信息。

### 列表 7-13：insmod 显示 SLIP 模块已成功加载

| 模块: | #页数: | 使用者: |
| :--- | :--- | :--- |
| slip | 2 | 0 |
| slhc | 2 | [slip] 0 |
| 3c509 | 2 | 1 (autoclean) |

## 第三部分：重要的客户端-服务器网络

你可以使用`modprobe`的`-l`选项列出所有可用模块。
你可以通过使用`-t <module type>`选项来更具体地列出给定类型的模块。例如，要列出所有网络模块，请输入命令`modprobe -l -t net`。

## 静态内核

重新编译内核几乎。源代码存储在`/usr/src/linux`目录。该目录下的`README`文件对必要的步骤提供了良好的描述（在大约一半的位置，查找描述`mrproper`、`make depend`等内容的行）。
要重新编译内核，你必须确保以下条件已就绪：

- **`GNU` 编译器 (`gcc`) 必须准备就绪**。回想本章较早的“列出软件包文件”部分，为了让`gcc`运行，你必须安装以下软件包：
  - `/mnt/cdrom/RedHot/RPMS/binutils-2.7.0-2.i1386.rpm`
  - `/mnt/cdrom/RedHot/RPMS/gcc-2.7.2-1.i1386.rpm`
  - `/mnt/cdrom/RedHot/RPMS/libc-devel-5.3.12-i1386.rpm`

- **你还需要 `Make` 实用程序**，你可以在以下位置找到：
  `/mnt/cdrom/RedHot/RPM/make-3.75-1.i1386.rpm`

- **必须安装 Linux 内核源码目录**。回想本章较早的“列出软件包文件”，必须安装了软件包：
  - `/mnt/cdrom/RedHot/RPMS/kernel-headers-2.0.30-2.i1386.rpm`
  - `/mnt/cdrom/RedHot/RPMS/kernel-source-2.0.30-2.i1386.rpm`

为了避免混淆，`Red Hat` 内核包创建一个指向当前 Linux 源码目录的符号链接。然后，`/usr/src/linux-2.0.31`有一个指向`/usr/src/linux`的链接，便于记忆和使用。请记住，如果你手动升级了 Linux 版本，应该删除并重新链接到新目录。重新链接可以通过输入以下命令完成：

```bash
cd /usr/src

rm /usr/src/linux

ln -s /usr/src/linux-2.0.31 linux
```

- **复杂的源代码倾向于标准化常用函数的位置**。包含文件将常用变量和常量定义等内容存储在与源代码分离的文件中，因此许多不同的程序可以使用一组公共定义。Linux 内核源码使用这种方法，并在`/usr/include`目录中查找此类定义。因此，使用符号链接指向这些地方，你必须按照如下方式定义它们：

```bash
cd /usr/include

rm -rf asm linux scsi

ln -s /usr/src/linux/include/asm-i386 asm

ln -s /usr/src/linux/include/linux

ln -s /usr/src/linux/include/scsi
```

- **如果你需要重新编译内核，你还需要包含要编译的特定架构的头文件。这些文件通常位于内核源码目录。要包含它们，请使用以下命令：**

```bash
cd /usr/src/linux

make depend
```

- **在头文件准备好后，你可以运行 `make` 命令来编译内核。根据你的处理器速度，这将需要大量时间。**

```
make
```

编译完成后，你将在`/usr/src/linux`目录中获得一个新的内核镜像。然后，你可以使用此镜像启动系统，按照之前描述的步骤进行操作。

输入`new_linux`以加载你的新内核。否则，输入`vmlinuz`，或直接按回车键以获取旧版本。如果你等待超过五秒，旧内核将自动启动。你可以将该时间更改为任何想要的值。

这个过程涉及大量的指令，但只要稍微练习一下，其实非常简单。随着可加载模块（loadable modules）的出现，这种过程已不再那么必要，但在你建立稳定的内核模块设置后，它仍然很有用。当你的系统处于生产模式时，为了简单，你可能想要重新编译常用函数。

### 定制 Red Hat 启动过程

我在第 3 章中已经某种程度上提到了启动过程。回想一下`rc`脚本用于启动守护进程（daemons）和其他程序。`/etc/rc.d/rc.local`脚本供你添加指令来启动你自己的守护进程。在下一章中，我将用它启动几个守护进程，但我想在这里提到它，因为它是一个重要功能。

该脚本在所有其他启动脚本运行后最后执行。因此，当你的脚本启动时，系统应该已经功能完备。例如，网络已经启动，磁盘已经挂载。在你添加自己的函数之前，`rc.local`脚本只设置了你登录时看到的标准登录界面。列表 7-17 显示了该脚本。

#### 列表 7-17：/etc/rc.d/rc.local 文件

```sh
#!/bin/sh

# 此脚本将在所有其他 init 脚本*之后*执行。

# 如果你不想执行完整的 Sys V 风格初始化工作，

# 可以在这里放入你自己的初始化内容。

if [ -f /etc/redhat-release ]; then

    R=$(cat /etc/redhat-release)

else

    R="release 3.0.3"

fi

arch=$(uname -m)

a="_arch"

case "$arch" in

    a*) a="an":

    i*) a="an";
esac

# 这将在每次启动时覆盖 /etc/issue。因此，对 /etc/issue 进行的

# 任何更改都应在这里进行，否则在重启时它们将会丢失。

echo "" > /etc/issue

echo "Red Hat Linux $R" > /etc/issue

echo "Kernel $(uname -m)" > /etc/issue

cp -f /etc/issue /etc/issue.net

echo > /etc/issue
```
