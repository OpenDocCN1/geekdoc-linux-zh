

![](img/2344fc4a798f29dca9e8b5ed7288171a_262_0.png)

图 6-10 使用 mv 移动 names 和 temp

## mv, cp：移动或复制文件

第 5 章讨论了使用 mv 重命名文件。然而，mv 的用途更为广泛：您可以使用该实用程序将文件从一个目录移动到另一个目录（更改文件的路径名），也可以更改简单的文件名。当用于将一个或多个文件移动到新的目录时，mv 命令的语法如下：

```
mv existing-file-list directory
```

如果当前工作目录是 /home/max，Max 可以使用以下命令将 names 和 temp 文件从工作目录移动到 literature 目录：

```
$ mv names temp literature
```

此命令将 names 和 temp 文件的绝对路径名从 /home/max/names 和 /home/max/temp 分别更改为 /home/max/literature/names 和 /home/max/literature/temp（见图 6-10）。与大多数 Linux 命令一样，mv 接受绝对或相对路径名。

当您在 Linux 中工作并创建更多文件时，您需要使用 mkdir 创建新目录，以保持文件的有条理。mv 实用程序是扩展目录层次结构时，将文件从一个目录移动到另一个目录的有用工具。

cp 实用程序的工作方式与 mv 相同，不同之处在于它在指定目录中创建 existing-file-list 的副本。

## mv：移动目录

就像将普通文件从一个目录移动到另一个目录一样，mv 也可以移动目录。语法类似，除了您指定要移动的是一个或多个目录，而不是普通文件：

```
mv existing-directory-list new-directory
```

![](img/2344fc4a798f29dca9e8b5ed7288171a_263_0.png)

图 6-11 典型的基于 FHS 的 Linux 文件系统结构

如果 *new-directory* 不存在，则 *existing-directory-list* 必须只包含一个目录名，mv 会将其更改为 *new-directory*（即 mv 重命名该目录）。虽然您可以使用 mv 重命名目录，但除非使用 -r（递归）选项，否则您无法使用 cp 复制其内容。请参考 tar 和 cpio 的手册页以了解复制和移动目录的其他方法。

## 重要的标准目录和文件

最初，Linux 系统上的文件并未位于目录层次结构中的标准位置。分散的文件使得记录和维护 Linux 系统变得困难，几乎不可能发布一个能在所有 Linux 系统上编译和运行的软件包。第一个 Linux 文件系统标准，FSTND（Linux 文件系统标准），于 1994 年初发布。1995 年初，开始制定一个涵盖许多类 UNIX 系统的更广泛的标准：FHS（Linux 文件系统层次标准；proton.pathbase.com/fhs）。最近，FHS 已被纳入 LSB（Linux 标准基；www.linuxfoundation.org/collaborate/workgroups/lsb），这是 FSG（自由标准组）的一个工作组。最后，FSG 与开放源代码开发实验室（OSDL）合并，成立了 Linux 基金会（www.linuxfoundation.org）。图 6-11 显示了 FHS 规定的一些重要目录和文件的位置。随着阅读的深入，这些目录中的许多将变得更加清晰。

以下列表描述了图 6-11 中显示的目录，FHS 规定的一些目录以及其他一些目录。然而，Ubuntu Linux 并未使用 FHS 规定的目录。请注意，您不能总是通过目录的名称来确定其功能。例如，尽管 /opt 存储附加软件，但 /etc/opt 存储 /opt 中软件的配置文件。另见第 488 页的“重要文件和目录”。

- / Root 根目录存在于所有 Linux 文件系统结构中，是文件系统中所有文件的祖先。
- /bin 基本命令二进制文件 包含系统在恢复模式（第 445 页）首次启动时启动和运行所需的文件。
- /boot 引导加载程序的静态文件 包含启动系统所需的所有文件。
- /dev 设备文件 包含所有代表外围设备的文件，如磁盘驱动器、终端和打印机。以前，此目录中充满了所有可能的设备。udev 实用程序（第 502 页）提供了一个动态设备目录，使 /dev 仅包含系统中存在的设备。
- /etc 本机系统配置文件 保存管理、配置和其他系统文件。其中最重要的是 /etc/passwd，它包含所有有权使用系统的用户列表。
- /etc/opt 存储在 /opt 中的附加软件包的配置文件
- /etc/X11 X 窗口系统的本机配置文件
- /home 用户主目录 每个用户的主目录通常是 /home 目录的许多子目录之一。例如，假设用户目录在 /home 下，Zach 的主目录的绝对路径名是 /home/zach。在某些系统中，用户目录可能不在 /home 下，而是分散在其他目录中，如 /inhouse 和 /clients。
- /lib 共享库
- /lib/modules 可加载的内核模块
- /mnt 用于临时挂载文件系统的挂载点
- /opt 附加（可选）软件包
- /proc 内核和进程信息虚拟文件系统
- /root 根账户的主目录
- /sbin 基本系统二进制文件 用于系统管理的实用程序存储在 /sbin 和 /usr/sbin 中。/sbin 目录包含在启动过程中所需的实用程序，而 /usr/sbin 包含系统在启动并运行后使用的实用程序。在旧版本的 Linux 中，许多系统管理实用程序分散在几个目录中，这些目录通常还包含其他系统文件（/etc、/usr/bin、/usr/adm、/usr/include）。
- /sys 设备伪文件系统 有关更多信息，请参见第 502 页的 udev。
- /tmp 临时文件
- /usr 第二大层次结构 传统上包含包含系统使用信息的子目录。/usr 子目录中的文件通常不会经常更改，并且可能由几个系统共享。
- /usr/bin 大多数用户命令 包含标准 Linux 实用程序——即不需要在恢复模式（第 445 页）中使用的二进制文件。
- /usr/games 游戏和教育程序
- /usr/include C 程序包含的头文件
- /usr/lib 库
- /usr/local 本地层次结构 保存添加到系统中的重要本地文件和目录。子目录可以包括 bin、games、include、lib、sbin、share 和 src。
- /usr/sbin 非关键系统管理二进制文件 参见 /sbin。
- /usr/share 架构无关的数据 子目录可以包括 dict、doc、games、info、locale、man、misc、terminfo 和 zoneinfo。
- /usr/share/doc 文档
- /usr/share/info GNU info 系统的主要目录
- /usr/share/man 在线手册
- /usr/src 源代码
- /var 可变数据 随着系统运行而变化的内容文件保存在 /var 下的子目录中。最常见的例子是临时文件、系统日志文件、排队的文件以及用户邮箱文件。子目录可以包括 cache、lib、lock、log、mail、opt、run、spool、tmp 和 yp。旧版本的 Linux 将此类文件分散在 /usr 的几个子目录中（/usr/adm、/usr/mail、/usr/spool、/usr/tmp）。
- /var/log 日志文件 包含 lastlog（每个用户最后登录的记录）、messages（来自 syslogd 的系统消息）和 wtmp（所有登录/注销的记录），以及其他日志文件。
- /var/spool 排队的应用程序数据 包含 anacron、at、cron、lpd、mail、mqueue、samba 和其他目录。文件 /var/spool/mail 通常是 /var/mail 的链接。

## 访问权限

Ubuntu Linux 支持两种控制谁可以访问文件以及他们如何访问文件的方法：传统的 Linux 访问权限和访问控制列表（ACL）。本节描述传统的 Linux 访问权限。有关 ACL 的讨论请参见第 221 页，ACL 提供了比传统访问权限更细粒度的访问权限控制。

三种类型的用户可以访问文件：文件的所有者（owner）、与文件关联的组的成员（group；有关组的更多信息请参见第 492 页）以及其他人（other）。用户可以尝试以三种方式访问普通文件：尝试从文件读取、写入文件或执行文件。

### ls -l：显示权限

当您使用 -l 选项和一个或多个普通文件的名称调用 ls 时，ls 会显示关于该文件的一行信息。以下示例显示两个文件的信息。文件 letter.0610 包含一封信的文本，

![](img/2344fc4a798f29dca9e8b5ed7288171a_265_0.png)

