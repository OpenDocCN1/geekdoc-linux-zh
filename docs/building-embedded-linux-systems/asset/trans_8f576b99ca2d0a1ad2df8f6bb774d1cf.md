
其主要方法是为每个命令提供一个小型二进制文件。embutil5 由 diet libc 的作者 Felix von Leitner 编写并维护，其目标与 diet libc 非常相似。embutil5 可在 http://www.fefe.de/embtils/ 获取。

尽管它支持许多最常见的 Unix 命令，但 embutil5 远不像 BusyBox 那样全面。例如，在本文撰写时，0.18 版本仍缺少 *fbset、find、grep、ifconfig、ps* 和 *route*。它也不提供任何 shell 命令。

与 BusyBox 一样，并非所有完整命令提供的选项都受支持，但提供的子集足以满足大多数系统操作需求。然而，与 BusyBox 不同的是，embutil5 必须与 diet libc 进行静态链接。它不能链接到其他任何库。由于 diet libc 本身已经非常小，因此生成的命令二进制文件也相对较小。当只需要少量二进制文件时，embutil5 比 BusyBox 可能是更好的选择，因为总体尺寸更小。

## 设置

在开始设置之前，你需要按照第 4 章的说明在主机系统上安装 diet libc。然后，下载 embutil5 并将其提取到 ${PROJECTROOT}/sysapps 目录中。在本示例中，我们使用 embutil5 0.18。你可以进入该包所在的目录以完成剩余的设置：

```
$ cd ${PROJECTROOT}/sysapps/embtils-0.18
```

embutil5 没有配置选项。因此，你可以直接构建该包：

```
$ make ARCH=ppc CROSS=powerpc-linux- all
```

然后可以安装 embutil5：

```
$ make ARCH=ppc DESTDIR=\$\${PROJECTROOT\}\}/rootfs prefix=\"\" install
```

构建和安装 embutil5 时使用的选项和变量与用于 diet libc 的选项和变量含义相同。

## 使用

embutil5 的安装过程会将许多静态链接的二进制文件复制到目标根文件系统的 /bin 目录中。与 BusyBox 不同，这是唯一安装二进制文件的目录。

类似 BusyBox 的全合一二进制文件 allinone 也已安装。当为它创建适当的符号链接时，该二进制文件的反应方式与 BusyBox 相同。请注意，与 BusyBox 不同，你需要手动创建这些符号链接，因为安装脚本不会自动创建它们。allinone.c 文件显示，allinone 支持以下命令：

- arch
- basename
- clear
- cht
- dirname
- dmesg
- domainname
- echo
- env
- false
- hostname
- pwd
- sleep
- sync
- tee
- true
- ty
- uname
- which
- whoami
- yes

与 diet libc 一样，末尾斜杠（`/`）很重要。

### 自定义应用程序

根据组件的数量和类型，根文件系统中有很多地方可以放置你自己的应用程序。通常，遵循 FHS（文件系统标准）的指南是可取的。

如果你的应用程序由相对较少数量的二进制文件组成，将其放置在 /bin 中可能是最佳选择。这是第 4 章中控制守护进程实际使用的安装路径。

如果你的应用程序由复杂的二进制文件集以及可能还有数据文件组成，请考虑在你的项目的根文件系统中添加一个条目。你可以将这个新目录称为 project，或者根据你的项目名称来命名。在我们的控制模块的情况下，这个目录可以是 control-module。

自定义目录可以包含其自身的层级结构，你可以自定义它以最好地满足你的需求。如果你的二进制文件放置在那里，你可能需要在目标上设置 PATH 环境变量以包含自定义目录。

请注意，在根文件系统中添加自定义条目是与 FHS 相悖的。然而，由于你的文件系统是专为你的目标定制的，不太可能成为独立的发行版，因此这种对标准的违反是可以被原谅的。

### 系统初始化

系统初始化是 Unix 系统的另一个特殊性。如第 2 章所述，内核在初始化过程中的最后一步是启动 init 程序。该程序负责通过生成各种应用程序和启动一些关键软件组件来完成系统启动。在大多数 Linux 系统中，init 模拟 System V init，并以类似的方式配置。在嵌入式 Linux 系统中，System V init 的灵活性是过度的，因为它们很少作为多服务器系统运行。

你实际上并不需要在根文件系统中拥有标准的 init 程序，如 System V init。内核本身并不真的在意。它只需要一个在系统初始化完成后可以启动的应用程序。例如，你可以添加 init=path_to_your_init 启动参数，告诉内核使用你的主应用程序作为其 init。然而，这种方法有一些缺点，因为你的应用程序将成为内核唯一启动的应用程序。你的应用程序将负责启动系统中的其他应用程序。此外，如果你的应用程序意外终止，其退出将导致内核恐慌并随后进行系统重启，这与 System V init 意外退出的结果相同。虽然这在某些情况下可能是期望的行为，但通常会使嵌入式系统变得无用。因此，出于这些原因，通常在根文件系统中拥有真正的 init 是更安全且更有用的做法。

以下小节涵盖了大多数 Linux 发行版中找到的标准 init 包、BusyBox init 以及由 embutil5 和 diet libc 作者提供的微型 init——Minit。

与 Unix 中的其他问题一样，init 是一个广泛的主题。有许多文档详细讨论了 Linux init。《Running Linux》描述了主流工作站和服务器 init 设置。Alessandro Rubini 撰写了一篇关于 init 的非常有趣的文章，深入探讨了各种初始化方案的细微差别，可在 http://www.linux.it/kernel/docs/init 获取。

#### 标准 System V init

大多数 Linux 发行版中找到的标准 init 包由 Miquel van Smoorenburg 编写，可在 ftp://ftp.cistron.nl/pub/people/miquels/sysvinit 获取。使用该包可以为你提供与配置工作站或服务器启动相同的灵活性，用于配置目标的启动。然而，额外的功能和支持需要更多的空间。此外，它要求你跟踪另一个软件包的开发。该包的 2.86 版本包含以下命令：

- bootlogd
- poweroff
- halt
- reboot
- init
- runlevel
- killall5
- shutdown
- last
- sulogin
- mesg
- telinit
- mountpoint
- utmpdump
- pidof
- wall

该包可以很容易地交叉编译。首先，下载该包并将其解压缩到你的 ${PROJECTROOT}/sysapps 目录中。对于我们的控制模块，我们使用了 sysvinit 版本 2.86。然后，进入包的源代码目录并构建它：

```
$ cd ${PROJECTROOT}/sysapps/sysvinit-2.86/src
$ make CC=powerpc-linux-gcc
```

替换 CC 的值以匹配你目标的交叉编译器。构建完成后，你可以将其安装到目标的根文件系统中：

```
$ make BIN_OWNER="$$(id -un)" BIN_GROUP="$$(id -gn)" \
> ROOT=$$(PROJECTROOT)/rootfs install
```

此命令将安装目标根文件系统中的所有组件，除了二进制文件以外，但随后会失败，因为 Makefile 试图将 man 页也安装到根文件系统上。你可以修改 Makefile 以避免这种情况，但你也可以忽略错误消息。

前面的命令将 BIN_OWNER 和 BIN_GROUP 变量设置为当前用户的所有权。默认情况下，Makefile 试图安装组件并将其所有权设置为 root 用户。由于你不是以 root 身份登录的，Makefile 将失败。二进制文件在目标上的所有权并不重要，因为它通常不是多用户系统。但是，如果是多用户系统，你需要以 root 身份登录并运行 make install 命令。无论如何，都要非常小心地将 ROOT 的值设置为目标根文件系统的路径。否则，你可能会用目标二进制文件覆盖你工作站的 init。或者，为了避免以 root 身份登录，你可以使用正常用户权限运行安装命令，然后使用 chown 命令作为 root 更改每个已安装文件的权限。然而，这需要浏览 Makefile 以找到每个已安装文件及其目的地。

在将 init 安装到目标的根文件系统后，你需要添加适当的 /etc/inittab 文件，并用适当的文件填充 /etc/rc.d 目录。本质上，/etc/inittab 定义了系统的运行级别，而 /etc/rc.d 中的文件定义了每个运行级别上运行的服务。表 6-5 列出了 init 的七个运行级别及其在工作站和服务器发行版中的典型用途。

**表 6-5. System V init 运行级别**

| 运行级别 | 描述 |
| :------- | :---------- |
| 0 | 系统已停止。 |
| 1 | 系统中只有一个用户；无需登录。 |
| 2 | 多用户模式，无 NFS，命令行登录。 |
| 3 | 完全多用户模式，命令行登录。 |
| 4 | 未使用。 |
| 5 | X11，图形用户界面登录。 |
| 6 | 重启系统。 |

