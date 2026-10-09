
无论使用哪种 ABI，您都必须能够访问该平台的用户空间（userland）。

如果您想使用 Ports 集合中可用的某个 Linux 软件，请安装该 port。这将自动安装任何用户空间依赖项。

如果您想运行任意的 Linux 软件，您必须先安装一个 Linux 用户空间。FreeBSD 通常提供几个不同的 Linux 用户空间作为软件包。要查看可用的内容，请在软件包数据库中搜索 `linux_base`。

```
# pkg search linux_base

linux_base-c6-6.9.2
Base set of packages needed in Linux mode (Linux CentOS 6.9)

linux_base-c7-7.3.1611.6
Base set of packages needed in Linux mode (Linux CentOS 7.3.1611)
```

此版本的 FreeBSD 拥有两个 Linux 用户空间：一个基于 CentOS 6.9，另一个基于 CentOS 7.3。Linux 发行版可能会在未来发生变化，具体取决于 Linux 的发展方向。

检查您的软件支持的 Linux 版本。为您的应用程序安装最合适的用户空间。FreeBSD 将 Linux 用户空间安装在 /usr/compat/linux 下。

该 port 还会加载 Linux 模式的内核模块。若要在启动时自动加载该模块，请使用此 rc.conf 条目：

```
linux_enable="YES"
```

就这样！Linux 模式不是一个正式的服务，因为您无法重启它或获取其状态，所以您不能使用 `service(8)` 来配置它。运行 `/etc/rc.d/abi start` 可在不重启的情况下激活 Linux 模式。

在我们深入运行 Linux 程序之前，让我们先探索一下用户空间。

## Linuxulator 用户空间

正如 linux.ko 内核模块提供 Linux ABI 一样，Linuxulator 需要一个非常基本的 Linux 用户空间。查看 /usr/compat/linux 下的内容，您会发现它类似于以下内容：

```
# ls
bin     etc     lib64    proc    selinux sys     var
dev     lib     opt      sbin    srv     usr
```

这看起来很像 FreeBSD 的 / 目录内容，不是吗？如果您稍微浏览一下，就会发现，一般来说，/usr/compat/linux 的内容与您的核心 FreeBSD 安装相当相似。您会在两者中找到许多相同的程序。

Linux 爱好者立即注意到的任何 `linux_base` port 的一个特点是，与其典型的 Linux 安装相比，其内容非常精简。这是因为每个基于 Linux 的软件包只安装其运行所需的组件。FreeBSD 的 Linux 软件包将极简主义的 BSD 哲学强加于 Linux 软件之上。

只要可能，Linux 模式下的程序会尝试保持在 /usr/compat/linux 之下，这在某种程度上类似于一个弱 jail（参见第 22 章）。当您执行一个调用其他程序的 Linux 二进制文件时，Linux ABI 会先在 /usr/compat/linux 下查找该程序。如果该程序不存在于那里，Linux 模式会在主系统中查找。例如，假设您有一个调用 `ping(8)` 的 Linux 二进制文件。ABI 首先会在 /usr/compat/linux/ 下搜索 ping 程序；截至撰写本文时，它找不到任何 ping 程序。然后 ABI 检查主要的 FreeBSD 系统，找到 /sbin/ping 并使用它。Linuxulator 大量利用这种回退行为来减少 Linux 模式用户空间的大小。

或者，假设一个 Linux 二进制文件想要调用 `sh(1)`。Linux ABI 会在 /usr/compat/linux 下检查，找到 /usr/compat/linux/bin/sh，并执行该程序，而不是 FreeBSD 原生的 /bin/sh。

### linprocs 和 tmpfs

Linux 使用进程文件系统，或称为 procs。FreeBSD 几十年前就出于安全考虑默认取消了 procs，但某些 Linux 程序可能仍然需要它。使用需要 procs 的 Linux 软件意味着接受其固有的风险。FreeBSD 将 Linux procs 作为 `linprocs(5)` 提供。

若要启用 `linprocs(5)`，请在安装 Linuxulator 之后，将以下内容添加到 /etc/fstab：

| linproc | /compat/linux/proc | linprocs | rw | 0 | 0 |
| :------ | :----------------- | :------- | :- | :- | :- |

FreeBSD 按需加载文件系统内核模块，因此输入 `mount /compat/linux/proc` 即可在不重启的情况下激活 `linprocs(5)`。

许多 Linux 程序还期望有 `/dev/shm` 用于共享内存。FreeBSD 可以使用 `tmpfs(5)` 来模拟这一点。

`tmpfs /compat/linux/dev/shm tmpfs rw, mode=1777 0 0`

输入 `mount /compat/linux/dev/shm`，共享内存设备即准备就绪。

## 测试 Linux 模式

现在您对 Linux 模式下安装的内容有了一些了解，测试 Linux 功能就变得很容易。运行 Linux shell 并询问它正在运行在哪个操作系统上：

```
# /usr/compat/linux/bin/sh
sh-4.1$ uname -a
Linux storm 2.6.32 FreeBSD 12.0-CURRENT #0 r322672: Fri Aug 17 16:31:34 EDT
2018 x86_64 x86_64 x86_64 GNU/Linux
sh-4.1$
```

当我们询问这个命令提示符正在运行在什么类型的系统上时，该 shell 响应说它是一个运行在名为 *FreeBSD* 的 Linux 2.6.32 内核上的 Linux 系统。相当酷，对吧？

然而，请记住，Linux 模式并不是一个完整的 Linux 用户空间。您无法在默认的 Linuxulator 安装中交叉编译软件。您只能执行非常基本的任务。

## 识别和设置品牌（Brands）

为软件二进制文件设置品牌比给牛打品牌容易，但远没有那么冒险。大多数现代类 Unix 二进制文件采用 ELF 格式，其中包含注释空间。品牌就居住在那里。FreeBSD 通过二进制文件上的品牌为每个程序分配一个 ABI。如果二进制文件没有品牌，则假设它是 FreeBSD 二进制文件。

使用 `brandelf(1)` 查看和更改品牌：

```
# brandelf /bin/sh
File '/bin/sh' is of brand 'FreeBSD' (9).
```

这并不令人惊讶。这是一个 FreeBSD 二进制文件，因此将在 FreeBSD ABI 下执行。让我们尝试一个 Linux 二进制文件：

```
# brandelf /usr/compat/linux/bin/sh
File '/usr/compat/linux/bin/sh' is of brand 'Linux' (3).
```

使用 -1 标志查看 FreeBSD 支持的品牌。

```
# brandelf -1
known ELF types are: FreeBSD(9) Linux(3) Solaris(6) SVR4(0)
```

如果您有一个无法运行的外部程序，请检查其品牌。如果没有品牌或品牌不正确，您可能已经发现了问题所在：FreeBSD 正在尝试在原生 FreeBSD ABI 下运行该程序。使用 `brandelf -t` 手动设置品牌来更改此行为。例如，要为程序设置 Linux 品牌，请这样做：

```
# brandelf -t Linux /usr/local/bin/program
```

下次您尝试运行该程序时，FreeBSD 将在 Linux ABI 和 Linux 用户空间下运行它，程序应该会按预期工作。

您还可以使用 sysctls 来设置回退品牌。所有 FreeBSD 二进制文件都正确设置了品牌，但您复制到宿主机的随机程序可能没有。未设置品牌的二进制文件将按照选定的回退品牌进行处理。sysctl `kern.elf32.fallback_brand` 为 32 位主机提供回退品牌，而 `kern.elf64.fallback_brand` 为 64 位主机设置回退品牌。此 sysctl 接受品牌的数值标识符，对于 Linux 来说是 3。

```
# sysctl kern.elf64.fallback_brand=3
```

现在您应该能够运行 Linux 程序，而无需任何进一步的配置。剩下的只是 Linux 模式的一些小麻烦和缺点。遗憾的是，有一些这类问题，正如我们接下来要展示的那样。

## 使用 Linux 模式

许多 Linux 程序仅作为 port 提供。Ports 集合足够智能，能够意识到某软件需要 Linux 模式，并选择安装合适的 Linux 组件。一个流行的选择是 Skype。安装此 port 会触发安装合适的 Linux 用户空间。

拥有最小化 Linux 用户空间的缺点是，任何 port 都会有许多依赖项。其中一些是 FreeBSD 二进制文件，另一些是 Linux 的。建议使用该 port 的 `make missing` 命令来显示缺失的依赖项，甚至如第 16 章所述，从软件包自动安装依赖项。一旦所有必需的软件包都安装好，一旦您安装了 linprocs 和 Linux 共享内存设备，并且所有内核模块都已加载，安装 Skype 就和 `make install clean` 一样简单。

## 调试 Linux 模式

Linux 模式不是 Linux，当程序崩溃时，这一点尤为明显。许多程序有晦涩的错误信息，而 Linux 模式可能会进一步掩盖它们。您需要能够挖掘错误信息背后、查看真正错误所在工具。

## Linux 模式和 truss(1)

我发现调试 Linux 模式的最好工具是 `truss(1)`，即 FreeBSD 系统调用跟踪器。有人告诉我，用 `truss(1)` 做这件事就像把一辆 Mack 卡车的 12 缸发动机装到一辆大众甲壳虫上一样，但在深思熟虑并仔细考虑之后，我决定我根本不在乎。它起作用。一旦您了解了 `truss(1)`，您就会想知道自己以前是如何没有它而生活的。

`truss(1)` 程序准确识别程序执行了哪些系统调用以及每个调用的结果。请记住，系统调用是程序与内核的接口。当程序试图与网络通信、打开文件甚至分配内存时，它都会执行系统调用。这使得 `truss(1)` 成为查看程序为何失败的一个绝佳方式。

