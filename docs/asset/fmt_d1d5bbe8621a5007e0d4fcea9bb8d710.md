
当许多平台相似时，重新编译效果最好。例如，FreeBSD 和 Linux 有许多相似的系统函数；它们都基于标准 C 函数构建，使用相似的工具；都使用 GCC 编译器，等等。多年来，各种 Unix 类操作系统已经发生了分化。每个 Unix 版本都实现了新功能、新库和新函数，当某个软件需要这些函数时，它将无法在其他平台上构建。POSIX 定义了最小可接受的 Unix 系统调用，它的引入部分原因是为了缓解这个问题。使用仅符合 POSIX 标准的系统调用和库编写的软件应该能够立即移植到任何其他符合 POSIX 标准的操作系统，且大多数 Unix 供应商都符合 POSIX。问题在于确保开发者可以在 POSIX 环境下运行。许多开源开发者只关心他们的软件是否运行在偏好的平台上。例如，现有的 Linux 特有软件并不符合 POSIX 标准。而仅符合 POSIX 的代码则没有利用操作系统提供的任何特殊功能。

例如，FreeBSD 拥有极高效的数据读取系统 `kqueue(2)`。其他 Unix 类操作系统使用 `select(2)` 和 `poll(2)` 代替。应用开发者问自己的问题是，他们是否应该使用 `kqueue(2)`，这会让他们的软件在 FreeBSD 上快得惊人但在其他地方毫无用处，还是他们应该选择 `select(2)` 和 `poll(2)` 以允许他们的软件在处处运行，尽管速度较慢。开发者可以投入更多时间平均支持 `kqueue(2)`、`select(2)` 和 `poll(2)`，虽然这让用户满意，但从开发者的角度来看这很糟糕。

FreeBSD 采取了折中之道。如果一个软件可以在 FreeBSD 上正确重新编译，ports 团队通常会实现它。如果软件需要细微补丁，ports 团队会将补丁包含在移植中，并将其发送给软件开发者。大多数开发者乐意接受允许他们支持另一个操作系统的补丁，即使他们可能没有该 OS 可供测试，或者他们可能并不熟悉它。

如果这不可行，你可以在 Wine 这样的模拟器下运行非原生软件，或者通过重新实现软件原生平台的应用程序二进制接口 (ABI) 来运行。

# 模拟

传统软件是为特定的 OS 编写的，且仅在该 OS 上运行。许多人通过修改软件使其在另一个系统上运行，这一过程被称为移植。作为管理员，你有方法可以使用为 FreeBSD 以外平台编写的软件。最有效的方法是重新编译源代码以在 FreeBSD 上原生运行。

如果这不可行，你可以在 Wine 这样的模拟器下运行非原生软件，或者通过重新实现软件原生平台的应用程序二进制接口 (ABI) 来运行。

## 外部软件库

虽然 ABI 重实现解决了一个主要问题，但程序需要的不仅仅是 ABI。没有共享库、支持程序以及其他用户态（userland），大多数程序将无法正常运行。无论你使用哪种 ABI，你都必须访问该平台的用户态。

要使用 SVR4 模式，你需要一张 Sun Solaris 2.5.1 的 CD。旧版本的 Solaris 不再免费提供，因此 FreeBSD 项目无法为你提供这些。这并非不可逾越，但它让使用 SVR4 模式变得稍微困难了一些，而且昂贵得多。如果你有那张 CD，请查看 `/usr/ports/emulators/svr4_base`。

Linux 用户态是免费获取的。由于准入门槛非常低，我们将详细讨论 Linux 模式。一旦你彻底理解了它的原理，就可以将这些知识应用到任何你想要使用的 ABI 兼容模式上。

## 使用 Linux 模式

要安装 Linuxator，请选择一个需要 Linux 模式的软件并安装它。端口集合（Ports Collection）足够智能，能够识别出某个软件需要 Linux 模式，并选择合适的 Linux 组件进行安装。例如，我使用 Adobe Acrobat Reader (`/usr/ports/print/acreader7`)，这会触发 Linux 模式的安装。

该端口下载大量的 Linux 系统文件并将它们安装在 `/usr/compat/linux` 下。Linux 程序使用这个用户态，而不是 FreeBSD 用户态。

该端口还会加载 Linux 模式内核模块。要让 FreeBSD 在启动时自动加载该模块，请使用此 `rc.conf` 条目：

```
linux_enable="YES"
```

就这样！你现在应该可以在不进行任何进一步配置的情况下运行 Linux 程序了。剩下的只是 Linux 模式中一些细微的困扰和特殊之处。遗憾的是，这类问题确实有几个。

## 什么是 LINUX_BASE？

你会看到很多关于名为 `linux_base` 的内容的引用。在历史上，你通过一个名为 `linux_base` 的端口安装 Linux 用户态，然后在这些文件之上安装软件。现代 FreeBSD 使这一过程对用户透明化，允许你安装所需的软件，而无必担心相关要求。你在 `/usr/ports/emulators` 中看到的各种 `linux_base` 端口是为开发者使用和兼容性测试设计的，而不是供你安装的！

## Linuxulator 用户态

正如 `linux.ko` 内核模块提供 Linux ABI 一样，Linuxulator 需要一个极简的 Linux 用户态。查看 `/usr/compat/linux`，你会看到类似下面的内容：

```
# ls
bin etc lib media mnt opt proc sbin selinux srv
sys usr var
```

看起来像 FreeBSD 的根目录内容，不是吗？如果你稍微找一找，就会发现，通常情况下，`/compat/linux` 的内容与你的核心 FreeBSD 安装内容相当。你会在两者中找到许多相同的程序。

信徒们在安装完任何 `linux_base` 端口后立即发现的是，其内容与典型的 Linux 安装相比要简单得多。该基于 Linux 的端口只安装运行所需的组件。当安装一个新端口时，端口集合会根据需要扩展 Linux 用户态。

只要可能，Linux 程序都会尝试保持在 `/compat/linux` 下，这有点像一个弱监狱（weak jail，见第 9 章）。当你执行一个调用其他程序的 Linux 二进制文件时，Linux ABI 会首先检查 `/usr/compat/linux` 下是否存在该程序。如果程序不存在，Linux 会在主系统中查找。例如，假设你有一个调用 `ping(8)` 的 Linux 二进制文件。ABI 首先在 `/usr/compat/linux` 下搜索 `ping` 程序；截至本文撰写时，将一无所获。ABI 然后检查 FreeBSD 系统，找到了 `/bin/ping` 并使用它。Linuxulator 利用这种回退行为来减小 Linux 用户态的大小。

或者，假设一个 Linux 二进制文件想要调用 `sh(1)`。Linux ABI 检查 `/usr/compat/linux`，找到了 `/usr/compat/linux/bin/sh`，并执行该程序而不是 FreeBSD 原生的 `/bin/sh`。

## 测试 Linux 模式

现在你已经对 Linux 模式下安装了什么有了了解，测试功能就很简单。运行 shell 并询问它运行在什么操作系统上：

```
# /usr/compat/linux/bin/sh
sh-3.005 # uname -a
stretchclim.blackhelicopters.org 2.4.2 FreeBSD 7.0-CURRENT Wed Apr 23 21:47 EDT 2008 GNU/Linux
sh-3.005
```

当我们询问运行的是什么类型的内核时，shell 回答说它是运行在 FreeBSD 2.4.2 之上的 Linux 系统。很酷吧？

然而，请记住，Linux 模式并不是完整的 Linux 用户态。你不能在默认的 Linuxator 中交叉编译软件。你只能执行基础任务。

## 识别和设置标记（Brands）

软件的标记（Branding）比管理牲畜（cattle）要简单。大多数类 Unix 二进制文件都是 ELF 格式，其中包含一个注释空间。这就是标记所在的地方。FreeBSD 按标记分配每个二进制文件。如果二进制文件没有标记，则假设它是 FreeBSD 二进制文件。FreeBSD 识别三种标记：FreeBSD、Linux 和 SVR4。使用 `brandelf(1)` 查看：

```
# brandelf /bin/sh
File '/bin/sh' is of brand 'FreeBSD'.
```

没意外吧？这是一个 FreeBSD 二进制文件，所以它将在 FreeBSD ABI 下执行。让我们尝试一个 Linux 二进制文件：

```
# brandelf /usr/compat/linux/bin/sh
File '/usr/compat/linux/bin/sh' is of brand 'Linux'.
```

如果你有一个无法运行的外部程序，请检查它的标记。如果它没有标记或标记不正确，你可能发现了问题所在：FreeBSD 正在尝试在原生 ABI 下运行该程序。通过使用 `brandelf -t` 设置标记来解决此问题。例如，要将程序标记为 Linux，这样做：

```
# brandelf -t Linux /usr/local/bin/program
```

下次你尝试运行该程序时，FreeBSD 将在 Linux 用户态下运行它，程序应该就能工作。

## procfs

Linux 使用进程文件系统或 procfs。FreeBSD 很久以前就因为安全风险消除了 procfs，但如果你正在运行 Linux 模式，某些程序将需要它。FreeBSD 将 proc 作为 `procfs(5)` 提供。要启用 procfs，在安装 Linuxulator 后向 `/etc/fstab` 中添加以下内容：

```
/compat/linux/proc procfs rw 0 0
```

FreeBSD 按需加载文件系统模块，因此只需挂载 `/compat/linux/proc` 即可激活 procfs 而无需重启。

## 使用 truss(1) 调试 Linux 模式

现在你已经对 Linux 模式下安装了什么有了概念，测试功能轻而易举。运行 shell 并询问它运行在什么操作系统上：

（此处省略上文已出现的 shell 示例，以保持逻辑一致）

当我们询问运行的是什么类型的内核时，shell 回答说它是运行在 FreeBSD 2.4.2 之上的 Linux 系统。很酷吧？

然而，请记住，Linux 模式并不是完整的 Linux 用户态。你不能在默认的 Linuxator 中交叉编译软件。你只能执行基础任务。

## 识别和设置标记（Brands）

（此处省略上文已出现的 `brandelf` 示例）

## procfs

（此处省略上文已出现的 `fstab` 示例）

## 使用 truss(1) 调试 Linux 模式

（此处省略上文已翻译调试逻辑）

# 商业 Linux 软件与 Linux 模式

请记住，商业软件供应商不支持在 FreeBSD 的 Linux 模式下运行其 Linux 软件。如果你处于具有服务等级协议（S）且面临罚款风险的工业环境中，请务必仔细考虑使用 Linux 模式。商业软件的主要优势在于当它出现故障时有人可以负责，但 FreeBSD 的 Linux 模式消消了这一优势。

# 在错误的架构上运行软件

64 位计算正变得越来越流行，尤其是 AMD 创建了兼容 i386 的 64 位架构后。能够运行 32 位和 64 位操作系统对于硬件来说是一个几乎不可抵拒的卖点。软件必须为 64 位平台编写。虽然得益于 Sun Solaris，开源世界多年来一直处理 64 位计算，但我的程序仍然是为 32 位操作系统编写的。当你运行 FreeBSD/amd64 平台时，你最终会发现某些软件仅适用于 i386 硬件。该怎么办？

好消息是：如果你的内核开启了 `COMPAT_IA32` 选项（已包含在 `GENERIC` 中），FreeBSD/amd64 可以运行所有 FreeBSD/i386 软件，只要 FreeBSD/i386 软件不使用 FreeBSD/amd64 的共享库。这意味着如果你想在 64 位计算机上运行复杂的 32 位程序，你必须提供必要库的 32 位版本。这是支持的；如果你检查 `rc.conf`，你会发现 `ldconfig(8)` 选项 `ldconfig_i32 paths` 和 `ldconfig_local_i32 dirs`。这些专门用于告诉你的 amd64 系统寻找 32 位二进制文件。

更令人惊讶的是，FreeBSD/amd64 运行 Linux 32 位二进制文件比 64 位的常见得多，FreeBSD 的 Linux 模式支持 32 位软件。只需在内核中包含 `COMPAT_LINUX32` 选项即可。不需要额外的或特殊的配置；amd64 上的 Linux 模式与 i386 上的 Linux 模式完全相同。FreeBSD 目前不支持运行 64 位 Linux 软件，但所有专门为 64 位 Linux 编写的软件在 FreeBSD 中也同样可用。

虽然软件管理还有更多内容需要学习，但你现在已经知道如何应付了。让我们继续学习如何升级 FreeBSD。

# 13

# 升级 FreeBSD

![](img/c4666520b4ae55f258e16019fbd3316d_402_0.png)

升级网络服务器可能是系统管理员日常工作中最令人生恼的任务。我可以处理升级后桌面电脑上莫名其妙的行为，但当一整个公司或数百名客户依赖于一个系统时，即使是想到要动那个系统，都会让我心翻肉跳。任何操作系统的升级都会增加你日益增多的白发收藏。每一位经验丰富的系统管理员在面临“原地升级系统”和“向自己的眼睛上扎红热针”之间的选择时，经常不得不坐下来考虑自己的选择。虽然少数类 Unix 系统有简单直接的升级程序，但它们需要几个小时才能完成，并且需要一定的运气。

另一方面，FreeBSD 的最大优势之一就是它的升级程序。我曾让机器运行过三个不同的 FreeBSD 大版本以及其间无数个补丁版本，而无需重新安装系统。极少有 Windows 管理员会例行将服务器从 Windows 2000 升级到 Windows 2003，这仅仅是一个大升级。（顺便说一句，这些人对得上他们赚的每一分钱。）只有当 FreeBSD 系统老到硬件故障的风险让我整夜不安时，我才会将其淘汰。一个系统从 FreeBSD 2.2.5 开始，升级到 FreeBSD 3，最后升级到 FreeBSD 4。当 FreeBSD 4.8 出炉时，驱动程序开始发出奇怪的噪音，所以我选择在新系统上安装新版本。继任系统运行了 FreeBSD 5 和 6 直到最终崩溃。^1 我唯一遭受重大不便的时候是跨版本号跳转——即从 FreeBSD 5 跳跃到 6。我花了几个小时的时间在其他操作系统上模拟了这些操作。

# FreeBSD 版本

为什么升级 FreeBSD 是一件相对简单的事？关键在于 FreeBSD 的开发方法。FreeBSD 是一个不断进化的操作系统。如果你在下午下载当前版本的 FreeBSD，它与早晨的版本略有不同。来自各地的开发者不断添加更改和改进，这使得非开源软件使用的传统的发布版本编号变得不再实际。在任何时候，你都可以获得多个 FreeBSD 版本：发布版（releases）、错误修正分支（errata branches）——包括稳定版（stable）、-current 和快照（snapshots）。

# 发布版 (Releases)

如果你处于生产环境，你应该安装 FreeBSD 的发布版本，然后将系统补丁到正确的错误修正分支。

FreeBSD 发布版有一个传统的版本号，就像你在任何其他软件上看到一样：5.5、6.3、7.0 等。发布版仅仅是特定时间点 FreeBSD 最稳定版本的副本。每年三、四次，发布工程团队会要求开发者专注于解决更改。发布工程团队挑选候选版本；当团队对结果满意时，它就成为了发布版。

# 错误修正分支 (Errata Branches)

错误修正分支是一个特定的发布版本。虽然 FreeBSD 团队非常努力确保每个发布版本都没有漏洞，但这个目标并不现实。每个发布版本都有自己的错误修正分支。例如，FreeBSD 7.0-errata 与 FreeBSD 7.1-errata 不同，在它们之间进行升级很容易出错。错误修正分支中完全禁止任何 API 和 ABI 的更改。为了获得最大的稳定性，请留在你安装的版本。

截至写本文时，FreeBSD 项目支持发布后两年的错误修正分支，但可能会发生变化。请关注 `http://www.freebsd.org/security` 或 `FreeBSD-announce@FreeBSD.org` 邮件列表以获取有关计划寿命结束通知的更新。当然，由于源代码可用，只要你使用它，就可以继续支持旧发布版。你不能永远让 FreeBSD 团队为你做所有的工作！

# FreeBSD-current

FreeBSD-current，或简称 -current，是 FreeBSD 的最前沿、最新版本，包含了首次公开亮相的代码。虽然开发者在应用之前有测试服务器和补丁供评审，但与 FreeBSD-current 的广泛用户相比，这种暴露仍然少得多。初始的同伴评审会进行；有时,-current 会经历让经验丰富的系统迁移人员都感到剧烈的变化。

FreeBSD-current 提供给开发者、测试人员和相关方使用，但它并非用于通用。对 -current 问题的支持非常有限，因为开发者根本没有时间帮助你修复网络浏览器，同时有成千上万个关键问题需要处理。用户被期望修复这些问题，或者可能忍受直到有人修复它们。

更糟糕的是,-current 的默认设置包含了各种调试代码、特殊警告和相关的开发者功能。这些使得 -current 比 FreeBSD 的任何其他版本运行得慢。你可以禁用所有这些调试，但如果你这样做，那么当你遇到问题时就无法提交一份正确的报告。这意味着你更加孤立无援。查看你当前系统的 `/usr/src/UPDATING` 以获取调试详情。

如果你读不懂 C 语言和 Shell 代码，或者不想调试你的操作系统，或者不喜欢计算机功能任意失效，或者只是不喜欢被晾在那里直到有人能修复它，-current 并不适合你。勇者当然欢迎来到 -current，任何愿意投入大量时间学习和调试 FreeBSD 的人同样欢迎。
