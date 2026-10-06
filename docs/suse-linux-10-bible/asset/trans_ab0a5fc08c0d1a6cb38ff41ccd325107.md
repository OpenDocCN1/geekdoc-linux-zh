

# 第 29 章 ♦ 内核 731

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_775_0.png)

图 29-3：使用 xnconfig 配置内核

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_775_1.png)

图 29-4：在 xnconfig 界面中选择选项

## 编译内核

现在假设架构是 x86，你需要执行以下操作：

```
root@bible: /usr/src/linux-2.6.5-7.79/ # make bImage
```

从历史上看，“b” 代表 big（大），而 “z” 表示这是一个压缩后的镜像。在其他架构上，你需要的命令是不同的。关于 SUSE 的特定细节可以访问 www.suse.de/-agruen/kernel-doc 查看。

这是真正开展工作的地方。在 2.6 内核中，默认情况下你在离开之前会在屏幕上看到较输出（参见列表 29-2）。

## 列表 29-2：内核构建过程的输出

```
root@bible: /usr/src/linux-2.6.5-7.79/ # make bImage
SPLIT      include/linux/autoconf.h -> include/config/
make[1]:  arch/i386/kernel/asm-offsets.s is up to date.
CHR       include/linux/compile.h
include   include/linux/compile.h
UDO       init/version.o
CC        init/built-in.o
CC        init/kretypes.o
INCFG     kernel/config
ZIP       kernel/config_data.gz
INCRG     kernel/config.data
CC        kernel/config-in.o
ID        kernel/built-in.o
GEN       .version
CHR       include/linux/compile.h
UDO       include/linux/compile.h
CC        init/version.o
[ ]
```

当构建过程成功完成后，你将看到类似下面的消息：

Root device is (3, 1)
Root sector is 512 bytes.
Setup is 5039 bytes.
System is 1426 kB
Kernel: arch/i386/boot/bImage is ready

你可以导航到该目录并查看创建的文件。

```
root@bible: # cd /usr/src/linux/arch/i386/boot/
root@bible: /usr/src/linux-2.6.5-7.79/arch/i386/boot/ # ls -1 bImage
```

你应该看到一个全新的 bImage 文件，时间戳显示它刚刚被创建。

当你制作好 bImage 后，还有几个步骤需要执行：

- 1. 编译模块：

```
root@bz:~/usr/src/linux-2.6.5-79/ # make modules
```

注意，如果你简单地执行 `make` 或 `make all` 命令，bImage 和模块将一步到位完成构建。

- 2. 安装内核和模块：

```
root@bz:~/usr/src/linux-2.6.5-79/ # make install
```

这会将 bImage 文件复制到 /boot 目录。（在你在此之前，你可能想备份旧内核，特别是当它具有相同的版本号时。）

```
root@bz:~/usr/src/linux-2.6.5-79/ # make modules_install
```

- 3. 创建与新内核对应的新 initramdisk：

```
root@bz:~/usr/src/linux-2.6.5-79/ # mkinitrd
```

- 4. 检查 GRUB 菜单是否同时引用了旧、新内核，以便在需要时可以返回旧内核。编辑文件 /boot/grub/menu.1 来确认这一点。

如果你使用 LILO 启动，你需要编辑 /etc/lilo.conf 以确保新旧内核都包含在内，并运行 lilo 命令。

当你重启并选择新内核时。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_777_0.png)

如果你将之前作为模块加载的内容编译进了内核，那么在新内核启动时，这些模块本身不被加载是非常重要的；否则，可能会出现意外的问题。在这种情况下，你可能需要调整 /etc/modprobe.conf。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_777_1.png)

在 /usr/share/doc/packages/kernel-source/ 目录下有一份关于 SUSE 系统上处理 2.6 内核源码的文档（作者 Andreas Gruenbacher）。还有一个示例显示了创建和构建内核模块的原理。

## 重建 km-* 软件包

有很多以 km_ 开头的包。这些包包含了额外模块的源代码，你可能需要单独编译它们以添加对功能的支持。例如，km_ocfs 为 Oracle 集群文件系统 (OCFS) 添加了支持，而 km_smart 增加了某些功能的支持。如果你将之前作为模块加载的内容编译进了内核，那么在新内核启动时，这些模块本身不被加载是非常重要的；否则，可能会出现意外的问题。在这种情况下，你可能需要调整 /etc/modprobe.conf。（*注：原文此部分落似乎存在乱码或逻辑错误，此处根据上下文尽可能翻译*）

（注：由于原文从 "Rebuilding the km-* Packages" 之后开始出现大量重复和无意义的乱码字符，译文已尽可能根据其技术语境进行还原。）

