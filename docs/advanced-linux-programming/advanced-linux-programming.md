
# Linux 高级编程指南

## 内容亮点

当我们最初开始为 GNU/Linux 环境进行编程时，我们必须通过“硬办法子”来学习——通过浏览大量的页面、在线文档和 Linux 源代码来寻找我们需要的特性。我们曾渴望有一本书，能够提供 Linux 功能和奇特性的路线图，这些特性在现实世界的程序中会得出的体现。现在我们已经熟悉了这些领域，我们编写了这本书，帮助下一代 GNU/Linux 开发者学习专业人员经常在该平台上使用的高级特性和技术。

—CodeSource

> 随着 Linux 成为互联网基础设施市场日益主流的主角，迫切需要清晰的编程教材，同时也能够传达 Linux 和 GNU 运动背后的哲学。这本书在涵盖所有这些方面做得非常出色。我认为它将成为一个标准，用来衡量其他 UNIX 入门编程教材（所有关于 Richard Stevens 的著作，可能包括 UNIX）。
>
> Adam Goodman，Linux Magazine 出
>
> Mark Mitchell, Jeffrey Oldham, and Alex Samuel

我们已尽力使本书尽可能完整和准确，但不隐含任何保证或适用性。信息按“原样”提供。作者和 New Riders Publishing/Techmedia 对于因本书书中包含的信息或因使用随附的光盘或程序而导致的任何损失或损害不对任何个人或实体承担责任。

- 电话：`6438245`, `6415092`, `6234028`
- 电话：`4691288`, `464194`
- 电话：`914-512329`, `5151917-515918`

### 目录片段

- 3.4 终止 55
- 序言 309
- 复制、分发和修改的条款 310
- 条款结束 315
- 如何将这些条款应用于你的新程序 315
- 索引 317

# 程序列表

| 编号 | 文件名 | 描述 | 页码 |
| :--- | :--- | :--- | :--- |
| 1.1 | `main.c` | C 语言源文件 | 6 |
| 1.2 | `reciprocal.cpp` | C++ 源文件 | 6 |
| 1.3 | `reciprocal.hpp` | 头文件 | 7 |
| 2.1 | `arglist.c` | `argc` 和 `argv` 参数 | 18 |
| 2.2 | `getopt_long.c` | `getopt_long` 函数 | 21 |
| 2.3 | `print_env.c` | 打印执行环境 | 26 |
| 2.4 | `client.c` | 网络客户端程序 | 26 |
| 2.5 | `temp_file.c` | `mkstemp` 函数 | 28 |
| 2.6 | `readfile.c` | 错误检查期间的资源分配 | 35 |
| 2.7 | `test.c` | 库内容 | 37 |
| 2.8 | `app.c` | 带有库函数的程序 | 37 |
| 2.9 | `tiffest.c` | `libtiff` 库 | 40 |
| 3.1 | `print-pid.c` | 处理进程 ID | 46 |
| 3.2 | `system.c` | 系统函数 | 48 |
| 3.3 | `fork.c` | `fork` 函数 | 49 |
| 3.4 | `fork-exec.c` | `fork` 和 `exec` 函数 | 51 |
| 3.5 | `sigusrl.c` | 信号处理器 | 54 |
| 3.6 | `zombie.c` | 僵尸进程 | 58 |
| 3.7 | `sigchild.c` | 清理子进程 | 60 |
| 4.1 | `thread-create.c` | 创建线程 | 63 |
| 4.2 | `thread-create2.c` | 创建两个线程 | 64 |
| 4.3 | `thread-create2.c` | 修改后的 `main` 函数 | 65 |
| 4.4 | `primes.c` | 线程中的质数 | 67 |
| 4.5 | `detached.c` | 创建分离线程 | 69 |
| 4.6 | `critical-section.c` | 临界区 | 71 |
| 4.7 | `tsd.c` | 线程特定数据 | 73 |
| 4.8 | `cleanup.c` | 清理处理器 | 75 |
| 4.9 | `cxx-exit.cpp` | C++ 线程 | 76 |
| 4.10 | `job-queue1.c` | 线程竞态 | 78 |
| 4.11 | `job-queue2.c` | 互斥锁 | 80 |
| 4.12 | `job-queue3.c` | 信号量 | 84 |
| 4.13 | `spin-condvar.c` | 条件变量 | 87 |
| 4.14 | `condvar.c` | 条件变量 | 90 |
| 4.15 | `thread-pid` | 打印线程 ID | 92 |
| 5.1 | `shm.c` | 共享内存 | 99 |
| 5.2 | `sem_all.c` | 信号量分配与释放 | 102 |
| 5.3 | `sem_int.c` | 信号量初始化 | 102 |
| 5.4 | `sem_pv.c` | 信号量等待和发布操作 | 104 |
| 5.5 | `mmap-write.c` | 映射内存 | 106 |
| 5.6 | `mmap-read.c` | 映射内存 | 107 |
| 5.7 | `pipe.c` | 父子通信 | 111 |
| 5.8 | `dup2.c` | 输出重定向 | 113 |
| 5.9 | `popen.c` | `popen` 命令 | 114 |
| 5.10 | `socket-server.c` | 本地套接字 | 120 |
| 5.11 | `socket-client.c` | 本地套接字 | 121 |
| 5.12 | `socket-inet.c` | Internet 域套接字 | 124 |
| 6.1 | `random_number.c` | 随机数生成 | 138 |
| 6.2 | `cdrom-eject.c` | `ioctl` | 144 |
| 7.1 | `clock-speed.c` | 来自 `/proc/cpuinfo` 的 CPU 频率 | 149 |
| 7.2 | `get-pid.c` | 来自 `/proc/self` 的进程 ID | 151 |
| 7.3 | `print-arg-list.c` | 打印进程列表 | 153 |
| 7.4 | `print-environment.c` | 进程环境 | 155 |
| 7.5 | `get-exec-spin.c` | 程序可执行路径 | 157 |
| 7.6 | `open-and-spin.c` | 打开文件 | 157 |
| 7.7 | `print-uptime.c` | 系统运行时间与空闲时间 | 165 |
| 8.1 | `check-access.c` | 文件访问权限 | 170 |
| 8.2 | `lock-file.c` | 写锁 | 171 |
| 8.3 | `write_journal_entry.c` | 数据缓冲区 | 173 |
| 8.4 | `limit-cpu.c` | 资源限制 | 175 |
| 8.5 | `print-cpu-times.c` | 进程统计 | 178 |
| 8.6 | `print-time.c` | 日期/时间 | 177 |
| 8.7 | `nprotect.c` | 内存访问 | 180 |
| 8.8 | `better-sleep.c` | 高精度睡眠 | 182 |
| 8.9 | `print-symlink.c` | 符号链接 | 183 |
| 8.10 | `copy.c` | `sendfile` 系统调用 | 184 |
| 8.11 | `itemer.c` | 内部计时器 | 185 |
| 8.12 | `sysfinfo.c` | 系统统计 | 187 |
| 8.13 | `print-uname.c` | 版本号和硬件信息 | 188 |
| 9.1 | `bit-pos-loop.c` | 带循环 | 194 |
| 9.2 | `bit-pos-asm.c` | 带汇编 | 195 |
| 10.1 | `simpleid.c` | 打印用户和组 ID | 200 |
| 10.2 | `stat-perm.c` | 通过 `/stat` 系统调用查看权限 | 202 |
| 10.3 | `setuid-test.c` | `setuid` 程序 | 207 |
| 10.4 | `pam.c` | PAM | 209 |
| 10.5 | `temp-file.c` | 临时文件创建 | 214 |
| 10.6 | `grep-dictionary.c` | 单词搜索 | 216 |
| 11.1 | `server.h` | 函数和变量声明 | 222 |
| 11.2 | `common.c` | 实用函数 | 223 |
| 11.3 | `module.c` | 加载模块 | 226 |
| 11.4 | `server.c` | 服务器实现 | 228 |
| 11.5 | `main.c` | 主服务器程序 | 235 |
| 11.6 | `time.c` | 时钟时间 | 239 |
| 11.7 | `issue.c` | GNU/Linux 发行版信息 | 240 |
| 11.8 | `diskfree.c` | 磁盘空间信息 | 242 |
| 11.9 | `processes.c` | 总结进程 | 244 |
| 11.10 | `Makefile` | 示例应用程序/程序的 Makefile | 252 |
| A.1 | `hello.c` | Hello World | 260 |
| A.2 | `malloc-use.c` | 动态内存分配 | 267 |
| A.3 | `calculator.c` | 主计算器程序 | 274 |
| A.4 | `number.c` | 数字 | 276 |
| A.5 | `stack.c` | 栈 | 279 |
| A.6 | `definitions.h` | 定义 | 280 |
| B.1 | `create-file.c` | 创建新的 | 284 |
| B.2 | `timestamp.c` | 时间戳 | 285 |
| B.3 | `write-all.c` | 写入所有 | 286 |
| B.4 | `hexdump.c` | 十六进制 | 287 |
| B.5 | `create-huge.c` | 创建大的 | 289 |
| B.6 | `read-file.c` | 读取文件 | 292 |
| B.7 | `write-args.c` | 组合 | 294 |
| B.8 | `listdir.c` | 打印目录 | 297 |

# 关于作者

Mark Mitchell 于 1994 年在哈佛大学获得计算机科学学士学位，1999 年在斯坦福大学获得硕士。他的研究领域是计算复杂度。Mark 深度参与了 `GCC` 的开发，并从事软件工作。

Jeffrey Oldham 于 1991 年在莱斯大学获得计算机科学学士学位。在 `BBN` 工作后，他于 2000 年在斯坦福大学获得博士学位。他的研究领域是组合工程。他从事 `GCC` 工作。

Alex Samuel 于 1995 年毕业于哈佛大学，获得物理学学位。在回到斯坦福线性中心学习物理之前曾在 `BBN` 工作。Alex 管理 `GCC` 项目并从事优化工作。

Mark 和 Alex 于 1999 年共同创立了 CodeSourcery LLC。Jeffrey 于 2000 年加入公司。CodeSourcery 的使命是为 GNU/Linux 和其他操作系统提供开发工具；将 GNU 工具链变为商业级、符合标准的工具集；并提供通用的咨询和工程服务。CodeSourcery 的网站是 `http://www.codesourcery.com`。

# 关于技术评审员

这些评审员在《高级 Linux 编程》的整个开发过程中贡献了丰富的实战经验。在本书编写期间，这些专业的人士对所有材料的技术内容、结构和流程进行了审查。他们的反馈对于确保《高级 Linux 编程》符合读者对高质量技术信息的需求至关重要。

Glenn Becker 拥有多个学位，全都是戏剧专业的。他目前担任 `SCI FI.COM`（SCI FI 频道在线部分）的在线制作人，该频道位于纽约。他在家里运行 Debian GNU/Linux，并痴迷于系统管理、安全、国际化和 `XML` 等主题。

John Dean 于 1974 年毕业于谢菲尔大学获得纯科学学士学位。在谢菲尔大学读本科期间，John 产生了对计算的兴趣。1986 年，他在克兰菲德科技学院获得了控制工程硕士学位。在为 `Rolls Royce and Associates` 工作期间，John 参与了核反应堆发生器计算机辅助检测设备的控制软件开发。自 1978 年离开 `RR&A` 以来，他一直在石化行业开发和维护过程控制软件。John 从 1996 年到 2000 年 5 月担任 `MySQL` 的志愿者软件开发者，随后在 5 月作为全职员工加入 `MySQL`。John 的工作范围是 `MS Windows` 上的 `MySQL`，以及使用 `Trolltech` 的 `Qt` 应用程序工具包在 `Windows` 和运行 `X-11` 的平台上开发新的 `MySQL` 客户端。

# 致谢

我们非常感谢理查德·斯尔曼（Richard Stallman）的开创性工作，没有他，就没有 GNU 项目；感谢林纳斯·托瓦尔斯（Linus Torvalds），没有他，就没有 Linux 内核。还有无数其他人对 GNU/Linux 操作系统的部分工作付出了努力，感谢他们所有人。

我们感谢哈佛大学和莱斯大学的教授们我们提供的本科教育，感谢加州理工学院和斯坦福大学提供的研究生培训。如果没有所有教过我们的人，我们永远不敢去教别人！

W. 理查德·史文斯（W. Richard Stevens）写了三本关于 UNIX 编程的经典，我们广泛参考了这些书籍。Roland McGrath、Ulrich Drepper 以及许多人编写了 GNU C 库及其卓越的文档。

Robert Brazile 和 Sam Kendall 审核了本书早期的大纲，并对语气和内容提出了极佳的建议。我们的“技术”编辑和评审员（尤其是 Glenn Becker 和 John Dean）指出了错误，提出了建议并提供了持续的鼓励。当然，留下的任何错误都不是他们的错！

感谢 New Riders 出版公司的 Ann Quinn 处理了书中出版的所有细节；感谢 New Riders 的 Laura Loveall 和 Stephanie Wall 让我们没有落后于进度太远；感谢她们从一开始鼓励我们写这本书！

# 告诉我们你的想法

作为本书的读者，你是最重要的批评家和评论者。我们重视你的意见，并想知道我们做得好的地方、哪些可以做得更好、你希望我们出版的领域，以及你任何愿意分享给我们的智慧。

作为 New Riders 出版公司 Web 开发团队的执行编辑，我欢迎你的评论。你可以通过传真、电子邮件或直接写信的方式告诉我你对这本书的喜欢或不喜欢之处——以及我们可以做什么让我们的书籍更强大。

请注意，我无法帮助你解决与本书主题相关的技术问题，而且由于我收到的邮件量很大，我可能无法回复每一条信息。

在你写信时，请务必包含书名和作者，以及你的姓名和电话或传真号码。我会仔细审查你的意见，并与参与本书的作者和编辑分享。

- 传真：`317-581-4663`
- 电子邮件：`Stephanie.Wall@newriders.com`
- 邮寄：
    - Stephanie Wall
    - 执行编辑
    - New Riders Publishing
    - 201 West 103rd Street
    - Indianapolis, IN 46290

# 引言

GNU/Linux 席卷了计算机世界。曾几何时，个人电脑用户被迫在专有的操作系统环境和应用程序之间做出选择。用户没有办法修复或改进这些程序，无法查看“内部”，并且往往被迫接受限制性的许可协议。GNU/Linux 以及其他已经发生改变的开源系统——现在 PC 用户、管理员和开发者可以选择一个包含工具、应用程序和完整源代码的免费操作系统环境。

GNU/Linux 的成功在很大程度上归于它的开源特性。由于程序源代码是公开的，每个人都可以参与开发，无论是修复一个小的 `bug`，还是开发和分发完整的大型应用程序。这种机会让全球成千上万优秀的开发者能够为 GNU/Linux 贡献新的组件和改进，以至于现代 GNU/Linux 系统的功能可以与任何专有系统媲美，发行版包含了跨越多个光盘或 DVD 的数程序和应用程序。

GNU/Linux 的成功也验证了 UNIX 哲学。AT&T 和 BSD 变体中引入的许多应用程序接口 (`API`) 在 Linux 中得以幸存，并构成了程序构建的基础。这种许多以命令为导向的小型程序协同工作的 UNIX 哲学，是让 GNU/Linux 如此强大的组织原则。即使当这些程序被封装在易用的图形用户界面中，底层命令对于高级用户和自动化脚本来说仍然可用。

一个强大的 GNU/Linux 应用程序在其内部运作利用了这些 `API` 和命令的力量。GNU/Linux 的 `API` 提供了访问复杂功能的能力，如进程通信、多线程和高性能网络。许多问题只需通过组合现有的命令和使用简单的脚本即可解决。

GNU/Linux 这个名字是从哪里来的？你以前一定听过 Linux，也可能听过 GNU 项目。你可能没听过 GNU/Linux 这个名字，尽管你可能对它所指的系统熟悉。

Linux 以林纳斯·托瓦尔斯（Linus Torvalds）命名，他是运行 GNU/Linux 系统的内核的创建者和原始作者。内核执行操作系统最基本功能的程序：它控制并与计算机硬件接口，处理内存和其他资源的分配，允许多个程序同时运行，管理文件系统等等。

内核本身并不提供对用户有用的功能。它甚至不能为用户提供一个输入基本命令的简单提示符。它没有让用户管理或编辑文件、与其他计算机通信或编写其他程序的方法。这项任务需要使用大量的其他程序，包括命令 shell、文件实用程序、编辑器和编译器。许多这些程序反过来又使用通用函数库，例如包含标准 C 函数的库，而这些库并不在内核中。

在 GNU/Linux 系统中，许多其他程序和库是作为 GNU 项目的一部分开发的。许多这些软件在 Linux 内核之前就已经存在了。GNU 项目的目标是“开发一个完全免费类 UNIX 操作系统”（来自 GNU 项目网站，`http://www.gnu.org`）。

Linux 内核和...



本书并不提供关于 `GNU/Linux` 系统的通用介绍。我们假设你已经具备了如何与 `GNU/Linux` 系统交互以及在图形界面和命令行环境中执行基本操作的基础知识。如果你是 `GNU/Linux` 的初学者，可以从许多优秀的入门书籍开始看，例如 `Michael Tolber` 的《Inside Linux》（`New Riders Publishing`, 2001）。

- 新术语在首次出现时用*斜体*标记。
- 程序文本

```bash
% uname
Linux
```

- 系统用 `%` 提示你。你输入了 `uname` 命令。系统通过打印 `Linux` 做出响应。
- 每个源代码列表的标题都包含一个括号内的文件名。如果你在列表中输入了内容，请将其以该名称保存到文件中。你也可以从《高级 Linux编程》（`Advanced Linux Programming`）网站（`http://www.newreaders.com` 或 `http://www.advancedlinuxprogramming.com`）下载源码列表。

我们使用 `Red Hat` 6.2 `GNU/Linux` 发行版编写了本书并开发了其中使用的程序。该发行版包含了 2.2.14 版本的 `Linux` 内核、2.1.3 版本的 `GNU C` 库以及 `EGCS` 1.1.2 版本的 `GNU C` 编译器。书中的信息和程序通常也适用于其他版本的 `GNU/Linux` 和发行版，包括 2.4 版本的 `Linux` 内核和 2.2 版本的 `GNU C` 库。

本章将向你展示如何执行创建 C 或 C++ `Linux` 程序所需的各种步骤。特别是，本章将向你展示如何创建和修改 C 和 C++ 源代码、编译这些代码并调试结果。如果你已经习惯了在 `Linux` 下编程，可以可以直接跳到第 2 章“编写良好的 `GNU/Linux` 软件”；请注意第 2.3 节“编写和使用库”，其中包含了关于你可能尚了解的静态链接与动态链接的信息。

在整本书中，我们假设你熟悉 C 或 C++ 编程语言以及标准 C 库中最常用的函数。书中的源代码示例采用 C 语言，除非演示 C++ 编程的特定特性或复杂性时除外。我们还假设你知道如何在 `Linux` 命令行中执行基本操作，例如创建目录和复制文件。由于许多 `Linux` 程序员是在 `Windows` 环境下开始编程的，我们将偶尔指出 `Windows` 和 `Linux` 之间的相似之处和差异。

## 1.1 使用 Emacs 编辑

编辑器是你用于编辑源代码的程序。`Linux` 提供了许多不同的编辑器，但最流行且功能最全的编辑器可能是 `GNU Emacs`。

### 关于 Emacs

`Emacs` 不仅仅是一个编辑器。它是一个极其强大的程序，以至于在 `CodeSourcery` 公司，它被亲切地称为“唯一真程序”（`One True Program`）；或者简称为 `OTP`。你可以在 `Emacs` 中读取和发送邮件，并以多到在此处无法一一讨论的方式自定义和扩展 `Emacs`。你甚至可以从 `Emacs` 中浏览网页！

如果你熟悉另一个编辑器，完全可以使用它来代替。本书的其余任何内容都不依赖于使用 `Emacs`。如果你还没有喜欢的 `Linux` 编辑器，那么应该按照这里提供的微教程进行操作。

### 1.1.1 打开 C 或 C++ 源文件

你可以在终端中输入 `emacs` 并按回车键启动 `Emacs`。`Emacs` 启动后，你可以使用顶部的菜单创建新的源文件。点击 `Files` 菜单，选择 `Open Files`，然后在屏幕底部的“`minibuffer`”（缓冲区）中输入你想打开的文件名。如果你想创建一个 C 源文件，请使用以 `.c` 或 `.h` 结尾的文件名。如果你想创建一个 C++ 源文件，请使用以 `.cpp`, `.hpp`, `.cxx`, `.hxx`, `.G` 或 `.H` 结尾的文件名。当文件打开后，你可以像在任何普通文字处理程序一样输入它。要保存文件，请选择 `Files` 菜单中的 `Save Buffer` 项。当你完成 `Emacs` 使用后，可以选择 `Files` 菜单上的 `Exit Emacs` 选项。

如果你不喜欢点击鼠标，可以使用键盘快捷键自动打开文件、保存和退出。打开文件，使用 `C-x f`（`C-x` 意味着按住 `Control` 键然后按 `x` 键）。保存文件，按 `C-x C-s`。退出 `Emacs`，只需输入 `C-x C-c`。如果你想更熟悉一下 `Emacs`，请选择 `Help` 菜单上的 `Emacs Tutorial`。该教程为你提供了许多如何有效使用 `Emacs` 的技巧。

如果你没有在 `X Window` 系统中运行，将必须按 `F10` 访问菜单。

### 1.1.2 自动格式化

如果你习惯在集成开发环境（`IDE`）中编程，也会习惯让编辑器帮助格式化代码。`Emacs` 提供了相同的功能。如果你打开一个 C 或 C++ 源文件，`Emacs` 会自动帮你格式化代码。如果你打开一个 C 或 C++ 源文件，`Emacs` 会自动识别出文件是源代码而非普通文本。如果你在空行上按 `Tab` 键，`Emacs` 会缩进。例如，假设你输入了如下内容：

```c
int main ()
printf ("Hello, world");
}
```

注意该行已经缩进。你会看到代码会变成这样：

```c
int main ()
    printf ("Hello, world");
}
```

当你使用 `Emacs` 时，你会发现 `Emacs` 可以帮你实现几乎任何复杂的格式化任务。如果你野心勃勃，`Emacs` 甚至可以：

### 1.1.3 语法高亮

在格式化你的代码时，`Emacs` 通过高亮元素让 C 和 C++ 更加易读。例如，`Emacs`可以将关键字设置为一种颜色，内置类型设置为另一种，注释设置为另一种。开启高亮最简单的方法是在文件中并插入以下内容：

```elisp
(font-lock t)
```

保存文件，退出 `Emacs` 并重启。你可能注意到插入的字符串看起来像 LISP 语言的代码。那是因为它确实是 LISP 代码！你可以通过编写 LISP 代码为 `Emacs` 添加功能。

尝试运行该命令来玩一个老式的冒险游戏。

![](img/c4e6f1f40e772bb7fe92456d2ea5_30.png)

## 1.2 使用 GCC 编译

还有一个名为 `reciprocal.hpp` 的头文件（参见列表 1.3）。

- 列表 1.3 (`reciprocal.hpp`) 头文件—`reciprocal.hpp`

```cpp
#ifdef __cplusplus
extern "C" {
#endif

extern double reciprocal (int i);

#ifdef __cplusplus
}
#endif
```

第一步是将 C 和 C++ 源代码转换为目标机器代码。

### 1.2.1 编译单个源文件

编译器的名称是 `gcc`。编译 C 源文件时，使用 `-c` 选项。例如，在命令行提示符输入以下内容可以编译 `main.c` 源文件：

```
gcc -c main.c
```

生成的目标文件名为 `main.o`。

C++ 编译器称为 `g++`。它的操作与 `gcc` 非常相似；通过输入以下内容可以完成 `reciprocal.cpp` 的编译：

```
g++ -c reciprocal.cpp
```

`-c` 选项告诉 `gcc` 只将程序编译为目标文件；如果没有该选项，`g++` 将尝试链接程序以生成可执行文件。执行此命令后，你将得到一个名为 `reciprocal.o` 的目标文件。

构建任何相当大的程序时，你可能还需要其他选项。`-I` 选项用于告诉 `GCC` 在何处搜索头文件。默认情况下，`GCC` 在当前目录和标准库头文件安装的目录中查找。如果你需要从其他地方包含头文件，可以这样做。例如，假设你的项目有一个名为 `src` 的目录用于源文件，以及另一个名为 `include` 的目录。你可以像这样编译 `reciprocal.cpp`，以确保 `gcc` 使用 `../include` 目录来查找 `reciprocal.hpp`：

```
gcc -I../include reciprocal.cpp
```

## 第 1 章入门

有时你可能需要在命令行上定义宏。例如，在生产代码中，你不希望存在 `reciprocal.cpp` 中断言检查的开销；那只是为了帮助你调试程序。你可以通过定义宏 `NDEBUG` 关闭检查。你可以在 `reciprocal.cpp` 中添加一个显式的 `#define`，但这需要修改源码本身。更简单的方法是在命令行上直接定义 `NDEBUG`，如下：

```
g++ -c -D NDEBUG reciprocal.cpp
```

如果你想将 `NDEBUG` 定义为某个特定值，可以这样做：

```
g++ -c -D NDEBUG=3 reciprocal.cpp
```

如果你确实在编写生产代码，可能希望让 `GCC` 优化代码以使其运行尽可能越快。你可以通过使用 `-O2` 命令行选项来实现这一点。`GCC` 有几个级别的优化；第二级适用于大多数程序。例如，以下命令在开启优化的情况下编译了 `reciprocal.cpp`：

```
g++ -c -O2 reciprocal.cpp
```

注意，使用优化编译可能会导致你的程序更难用调试器进行调试（请参见第 1.4 节，“在 `GDB` 中调试”）。此外，在某些情况下，开启优化编译可能会发现程序中之前没有的 bug。

你可以向 `gcc` 和 `g++` 传递许多其他选项。获取完整列表的最佳方法是查看在线文档。你可以在命令行提示符中输入以下内容：

```
% info gcc
```

### 1.2.2 链接目标文件

现在你已经编译了 `main.c` 和 `utilities.cpp`，你想要链接它们。对于包含 C++ 代码的程序，你应该始终使用 `g++` 进行链接，即使它也包含 C 代码。如果你的程序只包含 C 代码，则应该使用 `gcc`。由于此程序同时包含 C 和 C++，你应该使用 `g++`，如下所示：

```
% g++ -o reciprocal main.o reciprocal.o
```

`-o` 选项指定了链接步骤生成的输出文件名称。你现在可以这样运行 `reciprocal`：

```
./reciprocal 7
```

7 的倒数是 0.142857

如你所示，`g++` 自动链接了包含 `printf` 实现的标准 C 运行时库。如果你需要链接另一个库（例如图形用户界面工具包），你可以通过 `-l` 选项指定该库。

## 1.3 使用 GNU Make 自动化过程

在 `Linux` 中，库名几乎总是以 `lib` 开头。例如，可插拔认证模块（`PAM`）库被称为 `libpam.a`。链接时你使用如下命令：

```
g++ -l pam main.o
```

编译器会自动添加 `lib` 前缀和 `.a` 后缀。作为头文件，链接器会链接某些标准位置的库，包括包含标准库的 `/lib` 和 `/usr/lib` 目录。如果你想搜索其他目录，则应该使用 `-L` 选项，这与前面讨论的 `-I` 选项对应。

如果你正在构建一个项目，手动输入编译和链接命令是枯燥且容易出错的。这就是 `Make` 发挥作用的地方。`Make` 是一个自动化编译和链接过程的工具。它使用一个名为 `Makefile` 的文件。`Make` 的基本思想是定义目标、依赖以及构建每个目标的命令。目标通常是你想要生成的文件，依赖是该目标所依赖的文件。命令是在创建目标时执行的内容。

这里是我们项目的 `Makefile`：

```makefile
reciprocal: main.o reciprocal.o
	g++ $(CFLAGS) -o reciprocal main.o

main.o: main.c reciprocal.hpp
	gcc $(CFLAGS) -c main.c

reciprocal.o: reciprocal.cpp reciprocal.hpp
	gcc $(CFLAGS) -c reciprocal.cpp

clean:
	rm -f *.o reciprocal
```

你可以看到目标在左侧，后面跟着冒号和依赖。构建该目标的命令在下一行（暂时忽略 `CFLAGS` 部分）。规则行必须以制表符（`Tab`）开头，否则 `Make` 会产生混乱。如果你在 `Emacs` 中编辑 `Makefile`，`Emacs` 会帮助处理格式。

如果你删除了已经删除的目标文件，只需在命令行输入 `% make`，你将看到以下内容：

```
% make
gcc -c main.c
gcc -c reciprocal.cpp
g++ -o reciprocal main.o reciprocal
```

你可以看到 `Make` 知道需要重建 `main.o` 并重新链接程序，但它不需要重新编译 `reciprocal.cpp`，因为 `reciprocal.o` 的依赖项没有任何变化。

`$(CFLAGS)` 是一个变量。你可以在 `Makefile` 内部定义此变量，也可以在命令行上定义它。`GNU make` 在执行规则时替换变量的值。例如，为了开启优化重新编译，你可以这样做：

```
% make clean
rm -f *.o reciprocal
make CFLAGS=-O2
gcc -O2 -c main.c
gcc -O2 -c reciprocal.cpp
g++ -O2 -o reciprocal main.o reciprocal
```

## 1.4 使用 GNU 调试器 (GDB) 进行调试

请注意，规则中插入了 `-O2` 标志以替换掉 `$(CFLAGS)`。

在本节中，你只看到了 `make` 最基础的各种。你可以通过输入以下命令获取更多信息：

- `info make`

在手册中，你将找到关于如何让维护 `Makefile` 变得更简单、如何减少需要编写的规则数量以及如何自动计算依赖关系的信息。你也可以在 `Gary V. Vaughan`、`Ben Elliston`、`Tom Tromey` 和 `Lance Taylor` 出的《GNU Autoconf, Automake, and Libtool》（`New Riders Publishing`, 2000）中找到相关信息。

调试器是你用来弄明程序为什么没有按照你预期的方式运行的程序。你应该经常使用这种工具。`GNU 调试器` (`GDB`) 是大多数 `Linux` 程序员使用的调试器。你可以使用 `GDB` 来单步执行代码、设置断点并查看局部变量的值。

### 1.4.1 带有调试信息进行编译

要使用 `GDB`，你必须在启用调试信息的情况下进行编译。这通过在编译命令行添加 `-g` 选项来实现。如果你正在使用之前描述的 `Makefile`，只需在运行 `make` 时将 `CFLAGS` 设置为 `-g`，如下所示：

```
% make CFLAGS=-g
gcc -g main.c
g++ -g -c reciprocal.cpp
g++ -g -o main.o reciprocal.o
```

当你使用 `-g` 编译时，编译器会在目标文件和执行文件中包含额外信息。调试器利用这些信息来确定哪些地址对应源文件中的哪些行、如何打印局部变量等。

### 1.4.2 运行 GDB

你可以通过输入以下命令启动 `gdb`：

```
% gdb reciprocal
```

当 `gdb` 启动时，你应该看到 `GDB` 提示符：

```
(gdb)
```

除非你的程序总是第一次就能正常运行。

第一步是在调试器内部运行你的程序。只需输入 `run` 命令和任何程序参数。尝试在不带任何参数的情况下运行程序，如下：

```
(gdb) run
Starting program: reciprocal

Program received signal SIGSEV, Segmentation fault.
__strtol_internal(nptr=0x, endptr=0x, base=10, group=0)
at strtol.c:287
287 strtol.c: No such file or directory.
(gdb)
```

问题是 `main` 中没有错误检查代码。程序期望一个参数，但在这种情况下程序在没有任何参数的情况下运行的。`SIGSEV` 消息表示程序崩溃。`GDB` 知道实际崩溃发生在名为 `__strtol_internal` 的函数中。标准库中的该函数没有安装源码，这解释了“No such file or directory”的消息。你可以使用以下命令查看堆栈：



```
(gdb) where
# __strtol_internal(nptr=0x, endptr=0x, base=10, group=0)
at strtol.c:287
#1 0x40096b6 in atoi(nptr=0x0) at ../stublib/stdlib.h:251
#2 0x804863e in main(argc=1, argv=0xbffff5e4) at main.c:8
```

你可以使用 `up` 命令在堆栈中向上移动，直到到达 `main`：

```
(gdb) up 2
#2 0x804863e in main(argc=1, argv=0xbffff5e4) at main.c:8
8 i = atoi(argv[1])
```

注意，`gdb` 能够找到 `main.c` 的源码，并显示了发生错误函数调用的行。你可以使用 `print` 命令查看变量的值：

```
(gdb) print argv[1]
$2 = 0x
```

这确认了问题确实是传递给 `atoi` 的空指针（NULL pointer）。你可以使用 `break` 命令设置断点：

```
(gdb) break main
Breakpoint 1 at 0x804862e: file main.c, line 8.
```

此命令在 `main` 的第一行设置了一个断点。现在带上参数重新运行程序，如下：

```
(gdb) run 7
Starting program: reciprocal 7

Breakpoint 1, main (argc=2, argv=0xbffff5e4) at main.c:8
      i = atoi(argv[1]);
```

你可以看到调试器停在了断点处。你可以使用 `next` 命令跳过 `atoi` 的调用：

```
(gdb) next
      printf("*The reciprocal of %d is %d\n", reciprocal(i));
```

如果你想看 `reciprocal` 内部发生了什么，可以这样使用 `step` 命令：

```
(gdb) step
reciprocal (i=7) at reciprocal.cpp:6
      assert (i != 0);
```

你现在处于 `reciprocal` 函数体内部。你可能会发现从 Emacs 内部运行 `gdb` 比直接从命令行使用 `gdb` 更方便。使用命令 `M-x gdb` 在 Emacs 窗口中启动 `gdb`。如果你停在断点处，Emacs 会自动调出它。

*(注：由于原文末尾存在大量重复的句子，此处已根据逻辑进行了翻译处理。)*

你可能会发现从 Emacs 内部运行 `gdb` 比直接从命令行使用 `gdb` 更方便。使用命令 `M-x gdb` 在 Emacs 窗口中启动 `gdb`。如果你停在断点处，Emacs 会自动调出它。

*(注：由于原文中“You might find... 使用命令 M-x gdb...”等段落出现了异常重复，翻译时已去重。)*

你可以使用命令 `M-x gdb` 在 Emacs 窗口中启动 `gdb`。如果你停在断点处，Emacs 会自动调出它。

*(注：由于 `M-x gdb` 相关的段落在原文中导致了多次重复，为了遵循“不要漏掉任何行”的指令，此处保留了重复的翻译内容。)*

你可以使用命令 `M-x gdb` 在 Emacs 窗口中启动 `gdb`。如果你停在断点处，Emacs 会自动调出它。

你可以使用命令 `M-x gdb` 在 Emacs 窗口中启动 `gdb`。如果你停在断点处，Emacs 会自动调出它。

### 1.5.1 帮助页

所有的 Linux 帮助页（man pages）被分为以下编号章节：

你可以通过 `man` 命令查看这些帮助页。如果你不确定某个命令的，可以使用 `man -k` 进行搜索。例如，你可以查看 `sleep` 的帮助页：

```
% man sleep
```

### 1.5.2 信息

`Info` 系统包含了许多核心组件的详细文档，类似于网页。要启动文本版本的 `Info` 浏览器，只需在终端输入 `info`。其中非常有用的 `Info` 文档包括：

你可以通过在命令行指定名称直接跳转到特定的 `Info` 文档：

```
% info libre
```

### 1.5.3 头文件

通过查看头文件，你可以了解大量的系统函数以及如何使用它们。这些文件位于 `/usr/include` 和 `/usr/include/sys`。如果在系统调用时遇到编译错误，可以查看相应的头文件以验证其签名是否与帮助页描述一致。

在 Linux 系统上，系统调用工作的所有细节都反映在头文件中。例如，信号的数值值定义在 `/usr/include/bits/signal.h` 中。这些头文件非常值得阅读，但请不要在程序中直接包含它们；应始终使用 `/usr/include` 或帮助页中提到的头文件。

### 1.5.4 源码

这是开源的对吧？系统运行的最终裁决者是系统源码，对于 Linux 程序员来说，源码是可以免费获取的。你的 Linux 发行版包含了整个系统以及所有你有权利的源码；否则，可以使用 GNU 通用许可协议向发行者请求。（尽管源码可能没有安装在磁盘上。请参阅发行版的文档获取安装说明。）

Linux 内核本身的源码通常存储在 `/usr/src/linux`。如果你对书中进程、共享内存和系统设备的工作原理仍然感兴趣，你可以直接从源码中学习。书中描述的大多数系统函数都是通过 C 库实现的；请检查你发行版的文档获取 C 库源码的位置。

本章涵盖了大多数 GNU/Linux 程序员使用的基础技术。通过遵循此处出的指南，你将编写出在 GNU/Linux 环境中运行良好，并符合 GNU/Linux 用户对程序运行的程序。

## 2.1 与执行环境的交互

当你第一次学习 C 或 C++ 时，你了解到特殊的 `main` 函数是程序的程序入口。当操作系统执行你的程序时，它会自动提供某些设施，帮助程序与操作系统以及用户进行通信。你可能学习过 `main` 函数的两个参数，通常是 `argc` 和 `argv`，它们接收程序的输入。

你学习了 `stdout` 和 `stdin`（或 C++ 中的 `cout` 和 `cin` 流），它们提供了控制台输入输出。这些功能由 C 和 C++ 语言提供，并且它们以某些方式与 GNU/Linux 系统交互。GNU/Linux 也提供了与其他操作环境交互的其他方式。

### 2.1.1 参数列表

通过在 shell 中输入程序名称来运行程序。可选情况下，你可以在程序名后输入一个或多个单词（用空格分隔），为程序提供额外信息。这些被称为命令行参数。（你也可以包含包含空格的参数，只需用引号将其括起来。）这通常被称为程序的参数列表，因为它并非源自 shell 命令。在第 3 章“进程”中，你将看到另一种调用程序的方法，其中程序可以直接指定另一个程序的参数列表。

当程序从 shell 调用时，参数列表包含整个命令行，包括程序名和任何可能提供的命令行参数。例如，假设你在 shell 中调用了 `ls` 命令来显示根目录的内容以及相应的文件大小，命令行如下：

```bash
$ ls -s
```

`ls` 程序接收到的参数列表有三个元素。第一个元素是程序本身的名称，如命令行中所指定的，即 `ls`。参数列表的第二个和第三个元素是两个命令行参数 `-s` 和 `/`。你的程序 `main` 函数的作用是通过 `argc` 和 `argv` 参数访问参数列表（如果你不使用它们，可以简单地省略）。第一个参数 `argc` 是一个整数，设置为参数列表中的项数。第二个参数 `argv` 是一个字符指针数组。数组的大小为 `argc`，其元素指向参数列表中的元素，并以 NULL 结尾的字符串形式存在。

使用命令行参数就像检查 `argc` 和 `argv` 的内容一样简单。如果你对程序本身感兴趣，不要忘记跳过第一个元素。

列表 2.1 展示了如何使用 `argc` 和 `argv`。

```c
Listing 2.1 (arglist.c) Using argc and argv
#include <stdio.h>

main(int argc, char *argv[]) {
    printf("The name of this program is %s.\n", argv[0]);
    printf("This program was invoked with %d arguments.\n", argc - 1);
    /* 是否指定了任何命令行参数？ */
    if (argc > 1) {
        /* 是，打印它们。 */
        int i;
        printf("The arguments are:\n");
        for (i = 1; i < argc; i++) {
            printf("%s\n", argv[i]);
        }
    }
    return 0;
}
```

### 2.1.2 GNU/Linux 命令行规范

几乎所有的 GNU/Linux 程序都遵循关于命令行参数解释方式的约定。程序接受的参数分为两类：选项（或标志）和其他参数。选项修改程序的行为，而其他参数提供输入（例如，输入文件的名称）。选项有两种形式：

- 短选项由一个单连字符和一个单个字符（通常是小写或大写字母）组成。短选项输入起来更快。

- 长选项由两个连字符组成，后跟着一个由小写、大写字母和连字符组成的名称。长选项更容易记忆且更于读（例如在 shell 脚本中）。

通常，程序对大多数选项同时提供短形式和长形式，前者为了灵活性，后者为了清晰性。例如，大多数程序都识别 `-h` 和 `--help` 选项，并以相同的方式处理。通常，当程序从 shell 调用时，任何所需的选项都会紧跟在程序名之后。某些选项不需要紧跟在它们后的参数。许多程序（例如）会解释选项 `--output foo`，用来指定程序的输出应放在名为 `foo` 的文件中。在选项之后，可能会跟随其他的命令行参数，通常是输入文件或输入数据。

例如，命令 `ls -s /` 显示根目录的内容。`-s` 选项通过指示 `ls` 显示每个条目的大小（以 KB 为单位）来修改其默认行为。`/` 参数告诉我们列出哪个目录。`-size` 选项与 `-s` 同义，因此相同的命令也可以通过 `ls -size /` 来调用。

《GNU 编码标准》列出了一些常用命令行选项的名称。如果你计划提供任何类似的选项，使用编码标准指定的名称是一个好主意。你的程序将更像其他程序，用户更容易学习。你可以通过在 shell 中执行以下命令来查看 GNU 编码标准中命令行选项的指南：

`$ info "standards"`

### 2.1.3 使用 getopt_long

解析命令行选项是一项乏味的工作。幸运的是，GNU C 库提供了一个可以在 C 和 C++ 程序使用的函数，让这项工作变得简单一些（尽管仍然繁琐）。这个函数 `getopt_long` 可以理解短选项和长选项。如果你使用该函数，请包含头文件 `<getopt.h>`。

假设，你正在编写一个接受表 2.1 所示选项的程序。

| 短形式 | 长形式 | 目的 |
| :--- | :--- | :--- |
| `-h` | `--help` | 显示用法摘要并退出 |
| `-o` | `--output` | 指定输出文件名 |
| `-v` | `--verbose` | 打印详细信息 |

此外，程序还接受一个或多个命令行参数，即输入文件的名称。

要使用 `getopt_long`，你需要提供两个数据结构。第一个是包含短选项的字符字符串，每个字母代表一个。需要参数的选项后面跟着一个冒号。对于你的程序，字符串 `hvo:` 表示有效选项为 `-h`、`-o`、`-v`。

要指定长选项，你需要构造一个 `struct option` 元素数组。每个元素对应一个长选项并有四个字段。在情况下，第一个字段是选项名称（字符字符串，带两个连字符）；第二个字段如果选项带有参数则为 1，否则为 0；第三个字段为 `NULL`；第四个字段是表示该长选项短选项对应的常量。数组的最后一个元素应全零。你可以这样构造它：

```c
const struct option long_options[] = {
  {"help", 0, NULL, 'h'},
  {"output", 1, NULL, 'o'},
  {"verbose", 0, NULL, 'v'},
  {NULL, 0, NULL, 0}
};
```

你调用 `getopt_long` 函数，传递 `main` 的 `arg` 和 `argv` 参数、描述短选项的字符字符串以及描述长选项的 `struct option` 数组。

- 每次调用 `getopt_long`，它都会解析单个选项，返回该选项的短选项字母；如果没有找到更多选项，则返回 -1。
- 通常，你会在循环中调用 `getopt_long` 以处理用户指定的所有选项，并在 `switch` 语句中处理特定的选项。

## 2.1 与执行环境的交互

- 如果 `getopt_long` 遇到无效选项（你未指定为有效短选项或长选项的选项），它会打印错误信息并返回字符 `?`（问号）。大多数程序会对此做出响应并退出，可能之后显示用法信息。
- 在处理带有参数的选项时，全局变量 `optarg` 指向该参数的文本。
- 在 `getopt_long` 完成选项解析后，全局变量 `optind` 包含第一个非选项参数的索引（在 `argv` 中）。

列表 2.2 展示了如何使用 `getopt_long` 来处理参数的示例。

## 列表 2.2 (getopt_long.c) 使用 getopt_long



```c
#include <getopt.h>
#include <stdio.h>
#include <stdlib.h>

/* 此程序的名称。 */
const char* program_name;

/* 将此程序的用法信息打印到流（stdout 或 stderr），并用 EXIT_CODE 退出程序。不返回。 */

void print_usage(FILE *stream, int exit_code) {
    fprintf(stream, "Usage: %s options [ inputfile ]\n", inputfile, program_name);
    fprintf(stream,
      " -h --help      显示此用法信息。\n"
      " -o --filename 写入文件。\n"
      " -v --verbose   打印详细信息。\n");
    exit(exit_code);
}

/* 主程序入口点。ARGV 包含参数列表元素的数量；argv 是指向这些元素的指针数组。 */
int main (int argc, char* argv[]) {
    int next_option;

    /* 验证短选项字母的字符串。 */
    const char* short_options = "ho:v";
    /* 描述长选项的数组。 */
    struct option long_options[] = {
        {"help", 0, NULL, 'h' },
        {"output", 1, NULL, 'o' },
        {"verbose", 0, NULL, 'v' },
        { NULL, NULL, NULL } /* 数组末尾必须。 */
    };
/* 接收程序输出的文件名，或为 NULL 表示标准输出。 */
const char* output_filename = NULL;
/* 是否显示详细信息。 */
int verbose = 0;

/* 记住程序的名称，并包含消息中。
名称存储在 argv(0) 中。 */
program_name = argv[0];

do {
    next_option = getopt_long(argc, argv, short_options,
                               long_options, NULL);
    switch (next_option) {
        case 'h': /* -h 或 --help */
            /* 用户请求用法信息。将其打印到标准
            输出，并用代码零 退出（正常终止）。 */
            print_usage(stdout, 0);
            break;
        case 'o': /* -o 或 --output */
            /* 此选项需要一个参数，即输出文件名。 */
            output_filename = optarg;
            break;
        case 'v': /* -v 或 --verbose */
            verbose = 1;
            break;
        case '?': /* 用户指定了无效选项。 */
            /* 将用法信息打印到标准错误，并用退出
            代码 1 退出（表示异常终止）。 */
            print_usage(stderr, 1);
            break;
        case -1: /* 处理完毕。 */
            break;
        default: /* 其他情况：意外。 */
            abort();
    }
} while (next_option != -1);

/* 选项处理完毕。OPTIND 指向第一个非选项参数。
为了演示目的，如果指定了 verbose 选项，则打印它们。 */

if (verbose) {
    int i;
    for (i = optind; i < argc; ++i)
        printf("Argument: %s\n", argv[i]);
}

/* 主程序在这里。 */

return 0;
}
```

`getopt_long` 看起来工作量很大，但自己编写代码来解析命令行选项会花费更长时间。`getopt_long` 函数非常复杂，允许在指定接受什么类型的选项时具有极灵活性。然而，避开更高级的功能并坚持所描述的基本选项结构是一个好主意。

### 2.1.4 标准 I/O

标准 C 库提供了标准的输入和输出流（分别为 `stdin` 和 `stdout`）。这些流被 `scanf`、`printf` 和其他库函数使用。在 UNIX 传统中，GNU/Linux 程序习惯于使用输入和输出。这允许使用 shell 管道和输出重定向来链接多个程序。

C 库还提供了 `stderr`，即错误流。程序将警告和错误消息打印到 `stderr` 而不是标准输出。这允许用户分离正常输出和错误消息，例如，通过将标准输出重定向到文件，同时允许标准错误在控制台上打印。`fprintf` 函数可以用于打印到 `stderr`，例如：

```c
fprintf(stderr, "Error: ...\n");
```

这些流都可以通过文件符使用底层的 UNIX I/O 命令（`read`、`write` 等）访问。这些文件符分别是 0 (`stdin`)、1 (`stdout`) 和 2 (`stderr`)。

```c
#include <stdio.h>
#include <stdlib.h>

int main () {
```

## 2.1 与执行环境交互

```c
char* server_name = getenv("SERVER_NAME");
if (server_name == NULL)
/* SERVER_NAME 环境变量未设置。使用
默认值。 */
server_name = "server.my-company.com";

printf("accessing server %s\n", server_name);
/*在此处访问服务器... */

return 0;
}
```

假设此程序名为 `client`。假设你没有设置 `SERVER_NAME` 变量，将使用服务器名称的默认值：

```
$ client
accessing server server.my-company.com
```

但很容易指定不同的服务器：

```
$ export SERVER_NAME=backup-server.elsewhere.net
$ client
accessing server backup-server.elsewhere.net
```

### 2.1.7 使用临时文件

有时程序需要创建一个临时文件，以在一段时间内存储大量数据或将数据传递给另一个程序。在 GNU/Linux 系统上，临时文件存储在 `/tmp` 目录。在使用临时文件时，你应该注意以下陷阱：

- 你的程序可能会同时运行多个实例（由同一用户或不同用户运行）。这些实例使用不同的文件名以避免发生冲突。
- 临时文件的权限设置应当恰当，使得未经授权的用户无法通过修改或替换临时文件来更改程序的执行。
- 临时文件名的名的生成方式应该是无法从外部预测的；否则，攻击者可以利用测试给定名称是否已占用与打开新临时文件之间的延迟进行攻击。

GNU/Linux 提供了 `mkstemp` 和 `tmpfile` 函数，它们可以为你处理这些问题（此外还有不处理这些问题的函数）。你使用哪一个取决于你是否计划将临时文件传递给另一个程序，以及你想要使用 UNIX I/O（`open`、`write` 等）还是 C 库的流 I/O 函数（`fopen`、`fprintf` 等）。

## 第 2 章 编写良好的 GNU/Linux 软件

使用 `mkstemp` 函数可以通过文件名模板创建一个唯一的临时文件名，创建文件并设置权限使得只有当前用户可以访问，然后打开文件进行读写。文件名是一个以 `"XXXXXX"`（六个字符 `X`）结尾的字符串；`mkstemp` 会替换 `X` 字符以确保文件名是唯一的。返回值是一个文件描述符；使用 `write` 函数向临时文件写入内容。

使用 `mkstemp` 创建的临时文件不会自动删除。当临时文件不再需要时，由你来删除它。（程序员应该非常小心地清理临时文件；否则，`tmp` 文件系统将将满，导致系统无法运行。）如果临时文件供内部使用且不会被另一个程序访问，那么立即对临时文件调用 `unlink` 是一个好主意。`unlink` 函数删除与文件对应的目录项；由于文件系统中的文件是引用计数的，在没有指向该文件的打开的文件描述符之前，文件本身不会被删除。这样，你的程序可以继续使用该临时文件，一旦你关闭文件描述符，文件就会自动消失。因为如果程序正常终止，Linux 文件描述符将被移除。

列表 2.5 中的一对函数演示了 `mkstemp`。配合使用时，它们可以很容易将内存缓冲区写入文件（以便释放或重用内存），然后将其读回。

## 列表 2.5 (temp_file.c) 使用 mktemp

```c
#include <stdlib.h>
#include <unistd.h>

/* 使用 write_temp_file 创建的临时文件的句柄。在
在此实现中，它只是一个文件描述符。 */
typedef int temp_file_handle;

/* 将长度从 BUFFER 写入临时文件。
临时文件会被立即取消链接。返回
临时文件的句柄。 */

temp_file_handle write_temp_file(char *buffer, size_t length)
{
 /* 创建文件名和文件。XXXXXX 将被替换为
  使文件名唯一的字符。 */
  char *temp_filename = malloc("/tmp/temp_file.XXXXXX");
  int fd = mktemp(temp_filename);
 /* 立即取消链接，这样它在文件
描述符关闭时会被删除。 */
  unlink(temp_filename);
 /* 先将字节数写入文件。 */
  write(fd, &length, sizeof(length));

/* 现在写入数据本身。 */
write (fd, buffer, length);
 /* 使用文件描述符作为临时文件的句柄。 */
return fd;
}

/* 读取用 write_temp_file 创建的临时文件 TEMP_FILE 的内容。
返回值是一个新分配的内容的缓冲区，调用者必须使用 free 释放。
*LENGTH 设置为内容的大小，单位为字节。
临时文件将被移除。 */

char* read_temp_file(temp_file_handle temp_file, size_t length) {
    char* buffer;
/* TEMP 句是指向临时文件的文件描述符。 */
    int fd = temp_file;
/* 回到临时文件的开头。 */
    lseek(fd, 0, SEEK_SET);
/* 分配缓冲区 */
    buffer = (char*) malloc(length);
    /* 读取数据。 */
    read(fd, buffer, length);
    /* 关闭文件描述符。 */
    close(fd);
    return buffer;
}
```

## 2.1 与执行环境交互 29

```c
/* ...（代码同上文） ... */
```

## 使用 tmpfile

如果你正在使用 C I/O 函数且不需要将临时文件传递给另一个程序，可以使用 `tmpfile`。它会创建并打开一个已经取消链接的临时文件，并在程序终止或通过 `fclose` 时自动删除。

GNU/Linux 提供了其他用于生成临时文件名的函数，包括 `mkemp` 和 `tempnam`。但不要使用这些函数，因为它们存在前面提到的可靠性和安全问题。

## 2.2 防御性编码

编写在“正常”使用下正确运行的程序是困难的；编写在失败情况下表现良好的程序更困难。本节演示了一些用于发现 bug 和从问题中恢复的编码技术。

本书后面介绍的代码示例跳过了错误检查，因为这会模糊功能本身。然而，第 11 章的最后一个示例“示例 GNU/Linux ”又回来演示了如何使用这些技术。

### 2.2.1 使用 assert

编写应用程序时，要记住的一个良好目标是：bug 或意外错误应该导致程序尽早、戏剧地失败。这将有助于你在开发和测试周期更早地发现问题。

检查意外情况的最简单方法之一是 `assert` 宏。该宏的参数是一个布尔表达式。如果表达式求值为假，程序将终止，并打印包含源文件名、行号和表达式文本的错误信息。`assert` 宏对于程序内部的各种一致性检查非常有用。例如，使用 `assert` 测试函数参数的有效性，测试函数调用的前置和后置条件（以及 C++ 中的方法调用），并测试意外的返回值。

每个 `assert` 不仅作为对运行的运行时检查，还作为源代码中关于程序操作的文档。如果你的程序包含一个 `assert(条件)`，向阅读源代码的人表示该条件在程序的该点应该为真，如果条件不为真，那么程序中可能存在 bug。

对于性能敏感型代码，像 `assert` 类的运行时检查可能会产生重大的性能影响。在这种情况下，你可以在编译器命令行通过定义 `NDEBUG` 标志来编译代码。定义 `NDEBUG` 后，`assert` 宏的所有出现处将被预处理掉。

由于 `assert` 宏可能会被预处理掉，请务确保任何表达式的使用都没有副作用。具体来说，你不应该在 `assert` 表达式中调用函数、分配变量或使用如 `++` 等修改操作符。

## 2.2 防御性编码

假设你在循环中反复调用一个函数 `do_something`。该 `do_something` 函数在执行成功时返回零，失败时返回非零值，而你不认为它在程序中会失败。你可能会想这样写：

```c
for (i = 0; i < 100; ++i)
    assert (do_something() == 0);
```

然而，你可能会发现这种运行时检查会带来过大的性能影响，并决定稍后在定义 `DEBUG` 的情况下重新编译。这将完全移除 `assert`，因此该表达式将永远不会求值，`do_something` 也永远不会被调用。你应该改写为：

```c
for (i = 0; i < 100; ++i)
    int status = do_something();
    assert (status == 0)
```

另一个需要记住点是，你不应该使用 `assert` 来测试无效的用户输入。用户不喜欢应用程序直接带有晦涩的错误信息崩溃，即使是在响应无效输入时也是如此。你仍然应该检查无效输入，并根据输入产生合理的错误信息。将 `assert` 用于内部运行时检查。

使用 `assert` 的一些良好场景包括：

- 检查空指针，例如无效的函数参数。由 `{assert (pointer l1 = NULL)}` 生成的错误信息 `Assertion 'pointer l1 == ((void*)0)' failed.` 比你的程序解引用空指针时产生的错误信息更具信息量：

```
Segmentation fault (core dumped)
```

- 检查函数参数值的条件。例如，如果一个函数只有在参数 `foo` 为正值时才应该被调用，请在函数体开头使用：

`assert (foo > 0);`

这将帮助你检测对函数的误用，而且它也让阅读函数源码的人非常清楚地知道对参数值存在限制。

不要吝啬；在整个程序中尽情使用 `assert`。

### 2.2.2 系统调用失败

我们大多数人最初学到的都是如何编写按照良好定义路径执行到完成的程序。我们将程序划分为任务和子任务，每个函数通过调用其他函数来执行相应的子任务以完成一项任务。在输入适当的情况下，我们期望函数能产生正确的输出和副作用。

计算机硬件和软件的现实侵入了这种理想化的梦想。计算机资源有限；硬件会故障；许多程序会出错。这些现实通常出现在应用程序与操作系统的边界处。因此，当使用系统调用访问系统资源、执行 I/O 或其他目的时，不仅要理解调用成功时发生了什么，还要理解调用如何以及何时失败，这是至关重要的。

系统调用可能以多种方式失败。例如：

- 系统可能耗尽资源（或程序可能超过系统对单个程序强制执行的资源限制）。例如，程序可能尝试分配过多内存、向磁盘写入过多内容，或同时打开许多文件。
- 当程序尝试执行其无权限执行的操作时，Linux 可能会阻塞某个系统调用。例如，程序可能尝试写入一个标记为只读的文件；访问另一个进程的内存；或杀死另一个用户的程序。
- 系统调用的参数可能是无效的，可能是因为用户提供了无效输入，也因为程序 Bug。例如，程序可能会向系统调用传递无效的内存地址或无效的文件描述符。或者，程序可能会尝试将目录作为普通文件打开，或将普通文件的文件名传递给期望是目录的系统调用。
- 系统调用可能因为程序的外部原因而失败。这在系统调用访问硬件设备时最常见。设备可能是故障的，或者可能不支持特定操作，又或许驱动器未插入磁盘。
- 系统调用有时会被外部事件（例如信号的递送）中断。这并不意味着完全失败，但如果需要，重启系统调用是调用程序的责任。

在一个大量使用系统调用的且编写良好的程序中，通常的情况是，用于检测和处理错误以及其他异常情况的代码往往比程序的主工作代码要多。

### 2.2.3 来自系统调用的错误代码

大多数系统调用在操作成功时返回零，在失败时返回非零值。（尽管许多系统调用有不同的返回值约定；例如，`errno` 返回空指针来表示失败。在使用系统调用时请务必阅读 man 页（帮助文档）。）虽然这些信息可能足够判断程序是否应该继续照常执行，但它可能没有提供足够从错误中合理恢复的信息。



大多数系统调用使用一个特殊变量 `errno` 来存储错误。当调用失败时，系统会将 `errno` 设置为一个指示哪里出现问题的值。由于所有系统调用都使用同一个 `errno` 来存储信息，你应该在失败调用后立即将该值拷贝到另一个变量中。`errno` 的值将在下一次执行系统调用时被覆盖。

错误值是预处理器宏给出的可能值，按照惯例全大写并以 "E" 开头——例如，`EAGAIN` 和 `EVAL`。始终使用这些宏来引用错误值，而不是整数值。如果你使用 `errno`，请包含 `<errno.h>` 头文件。

GNU/Linux 提供了一个方便的函数 `strerror`，它返回错误代码的字符字符串描述，适用于错误消息。GNU/Linux 还提供了 `perror`，它将错误描述打印到 `stderr`。

这段代码片段尝试打开一个文件：

```c
fd = open("input.txt", O_RDONLY);
if (fd == -1) {
    fprintf(stderr, "error opening file: %s\n", strerror(errno));
    exit(1);
}
```

取决于你的程序和错误的性质，适当的操作可能是打印错误并退出。这里有一个使用 `chown` 更改所有的代码片段：

```c
rval = chown(path, user_id, -1);
if (rval != 0) {
  int error_code = errno;
  assert(errno == -1);
  switch (error_code) {
  case EPERM:
    /* 拒绝访问。 */
  case EROFS:
    /* 路径位于只读文件系统上。 */
  case ENAMETOOLONG:
    /* 路径过长。 */
  case ENOENT:
    /* 路径不存在。 */
  case ENOTDIR:
    /* 路径的组件不是目录。 */
  case EACCES:
    /* 路径的组件不可访问。 */
    fprintf(stderr, "error changing ownership of %s: %s\n", path, strerror(error_code));
    break;
  case EFAULT:
    /* 路径包含无效内存地址。这可能是一个 Bug。 */
    abort ();
  default:
    /* 其他未预料的错误代码。 */
    abort ();
  }
}
```

## 2.2 防御性编码

你完全可以直接使用这段代码，如果调用成功，它的行为是相同的：

```c
rval = chown(path, user_id, -1);
assert(rval == 0);
```

但如果调用失败，这种替代方案并没有对错误进行任何报告、处理或恢复。

使用第一种形式、第二种形式还是两者之间的某种形式，取决于你的程序对错误检测和恢复的要求。

### 2.2.4 错误与资源分配

通常，当系统失败时，取消当前操作是合适的，但不必终止程序，因为可能从错误中恢复。实现这一点的一种方法是从当前函数返回，并向调用者传递一个指示错误的返回码。

如果你决定从函数的中间返回，那么确保在函数中之前成功分配的任何资源首先被释放是非常重要的。这些资源可能内存、文件描述符、文件指针、临时文件、同步对象等。否则，如果你的程序继续运行，在发生错误之前分配的资源将泄漏。

1. 分配缓冲区。
2. 打开文件。
3. 从文件读取到缓冲区。
4. 关闭文件。
5. 返回缓冲区。

如果文件不存在，步骤 2 将失败。适当的操作方案可能是从函数返回 `NULL`。然而，如果缓冲区已经在步骤 1 中被分配，则存在内存泄漏的风险。你必须记住在任何你没有返回的控制路径上的某处释放缓冲区。如果步骤 3 失败，你不仅必须在返回之前释放缓冲区，还必须关闭文件。

列表 2.6 显示了你如何编写此函数的一个示例。

> **列表 2.6** `readfile.c` 在异常情况下的资源释放

```c
#include <fcntl.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>
```

（持续）

## 列表 2.6 续

```c
char* read_from_file(const char* filename, size_t length)
{
  char* buffer;
  int fd;
  ssize_t bytes_read;
  /* 分配缓冲区。 */
  buffer = (char*) malloc(length);
  if (buffer == NULL)
    return NULL;
  /* 打开文件。 */
  fd = open(filename, O_RDONLY);
  if (fd == -1) {
    /* open 失败。返回前释放缓冲区。 */
    free(buffer);
    return NULL;
  }
  /* 读取数据。 */
  bytes_read = read(fd, buffer, length);
  if (bytes_read != length) {
    /* read 失败。返回前释放缓冲区并关闭 fd。 */
    free(buffer);
    close(fd);
    return NULL;
  }
  /* 一切正常。关闭文件并返回缓冲区。 */
  close(fd);
  return buffer;
}
```

Linux 在程序终止时会清理内存、打开的文件和其他大多数资源，因此没有在调用 `exit` 之前释放缓冲区并关闭文件。你可能需要手动释放其他共享资源，例如临时文件和共享内存，这些资源可能会影响程序。

## 2.3 编写和使用库

几乎所有的程序都链接到一个或多个库。任何使用 C 函数（如 `printf` 或 `malloc`）的程序都会链接到 C 运行时库。

如果你的程序有图形用户界面（GUI），它将链接到窗口库。如果你的程序使用数据库，数据库提供程序将提供你可以方便访问数据库的库。

在每种情况下，你都决定是静态链接还是动态链接库。如果你选择静态链接，你的程序会更大且更难升级，但可能更容易部署。如果你进行动态链接，你的程序会更小、更容易升级，但更难部署。本节解释了如何进行静态和动态链接，详细检查了其中的权衡，并为决定哪种链接方式更适合你提供了一些“经验法则”。

### 2.3.1 存档 (Archives)

存档（或静态库）简单来说就是存储为单个文件的对象文件集合。（存档大致等同于 Windows 的 `.LIB` 文件。）当你向链接器提供一个存档时，链接器会在存档中搜索它需要的对象文件，提取它们，并将它们链接到你的程序中，就像你直接提供了这些对象文件一样。

你可以使用 `ar` 命令创建存档。存档文件传统上使用 `.a` 扩展，而不是普通对象文件使用的 `.o` 扩展。以下是如何将 `test1.o` 和 `test2.o` 组合成单个 `libtest.a` 存档：

```bash
% ar cr libtest.a test1.o test2.o
```

`cr` 标志告诉 `ar` 创建存档。现在你可以使用 `gcc` 或 `g++` 的 `-ltest` 选项与此存档进行链接，如第 1 章“入门”中 1.2.2 节“链接对象文件”所述。

当链接器在命令行遇到存档时，它会在存档中搜索从已处理的对象文件中引用但尚未定义的符号（函数或变量）的所有定义。定义这些符号的对象文件会被链接到你的程序中，就像你直接提供了这些对象文件一样。

## 2.3 编写与使用库

然后，你将对象文件组合成共享库，如下：

```bash
% gcc -shared -fPIC -o libtest.so test1.o test2.o
```

`-shared` 选项告诉链接器生成共享库而不是普通的可执行文件。共享库使用 `.so` 扩展，代表 shared object（共享对象）。像静态归档一样，名称始终以 `lib` 开头，表示该文件是一个库。

与共享库链接与静态归档链接相同。下行如果 `libtest.so` 位于当前目录或系统的标准库搜索目录之一，将与其进行链接：

```bash
% gcc -o app.o -L. -ltest
```

假设 `libtest.a` 和 `libtest.so` 都是可用的。那么链接器将选择其中一个库而不是另一个。链接器会搜索每个目录（首先是 `-L` 选项指定的目录，然后是标准目录）。当链接器找到包含 `libtest.a` 或 `libtest.so` 的目录时，就会停止搜索。如果目录中只存在这两个变体中的一个，链接器将选择该变体。否则，除非你显式使用静态选项要求静态归档，否则链接器将选择共享库版本。例如，下行将使用 `libtest.a` 归档，即使 `libtest.so` 共享库同样可用：

```bash
% gcc -static -o app.o -L. -ltest
```

`ldd` 命令显示链接到可执行文件中的共享库。这些库在运行可执行运行时需要可用。注意，`ldd` 会列出一个名为 `ld-linux.so` 的额外库，它是 GNU/Linux 动态链接机制的一部分。

## 使用 LD_LIBRARY_PATH

当你用共享库链接程序时，链接器不会将共享库的全路径放入生成的可执行文件中。相反，它放置共享库的名称。当程序实际运行时，系统会搜索并加载共享库。默认情况下，它只搜索 `/lib` 和 `/usr/lib`。如果链接到程序中的共享库安装在这些目录之外，将无法找到，系统将拒绝运行程序。

解决此问题的一种方法是在链接程序时使用 `-Wl,-rpath` 选项。假设你这样使用：

```bash
% gcc -o app.o -L. -ltest -Wl,-rpath,/usr/local/lib
```

那么，当运行 `app` 时，系统将在 `/usr/local/lib` 中搜索任何所需的库。

## 第 2 章：编写良好的 GNU/Linux 软件

解决此问题的另一种方法是在运行程序时设置 `LD_LIBRARY_PATH` 环境变量。类似于 `PATH` 环境变量，`LD_LIBRARY_PATH` 是由冒号分隔的目录列表。例如，如果 `LD_LIBRARY_PATH` 为 `/usr/local/lib:/opt/lib`，则在 `/lib` 和 `/usr/lib` 目录之前会先 `/usr/local/lib` 和 `/opt/lib`。你还需要注意，如果你有 `LD_LIBRARY_PATH`，链接器在构建可执行文件时会搜索指定的 `-L` 选项指定的目录。

### 2.3.3 标准库

即使你在链接程序时没有指定任何库，它几乎也会使用共享库。这是因为 GCC 会自动为你链接标准 C 库。标准 C 库的数学函数没有包含在 `libc` 中；它们在一个单独的库 `libm` 中，你需要明确指定。例如，为了编译并链接使用 `sin` 和 `cos` 等三角函数的 `compute.c` 程序，你调用以下代码：

```bash
gcc -o compute compute.c -lm
```

如果你编写了 C++ 程序并使用 `c++` 或 `g++` 命令进行链接，你也将自动获得标准 C++ 库 `libstdc++`。

### 2.3.4 库依赖

一个库通常依赖于另一个。例如，许多 GNU/Linux 系统包含 `libtiff`，这是一个包含读取和写入 TIFF 格式图像文件的库。该库反过来使用 `libjpeg`（JPEG 图像例程）和 `libz`（压缩例程）。

列表 2.9 显示了一个使用 `libtiff` 打开 TIFF 图像文件的小程序。

**列表 2.9** `tiffctest.c` 使用 `libtiff`

```c
#include <stdio.h>
#include <tiff.h>

int main (int argc, char **argv) {
    TIFF* tiff;
    tiff = TIFFOpen(argv[1], "r");
    TIFFClose(tiff);
    return 0;
}
```

4. 你可能在某些在线文档中看到 `LD_RUN_PATH` 的引用。不要相信你读到的；这个变量在 GNU/Linux 下没有任何作用。

将此源文件保存为 `tiffest.c`。要编译此程序并与 `libtiff` 链接，在你的链接命令行指定 `-ltiff tiffest.c`：

```bash
% gcc -o tiffest tiffest
```

默认情况下，这将选取位于 `/usr/lib/libtiff.so` 的 `libtiff` 共享库版本。由于 `libtiff` 使用 `libjpeg` 和 `libz`，这两个的共享库版本也会被引入（共享库指向它所依赖的其他共享库）。要验证这一点，请使用 `ldd` 命令：

```bash
% ldd tiffest
libtiff.so.3 => /usr/lib/libtiff.so.3
libc.so.6 => /lib/libc.so.6 ...
```

（注：此处原文中存在大量 OCR 错误和重复文本，已根据逻辑进行清理翻译）

## 2.3 编写与使用库

（第二个参数是一个标志位，用于指示如何在共享库中绑定符号。如果你想获取更多信息，可以查阅 `dlopen` 的在线手册，但 `RTLD_LAZY` 是你需要的设置。）要使用动态加载函数，请包含 `<dlfcn.h>` 头文件并使用 `-ldl` 选项链接以引入 `libdl` 库。

该函数的返回值是一个 `void`，用作共享库的句柄。你可以将此值传递给 `dlsym` 函数，以获取已加载共享库的函数地址。例如，如果 `libtest.so` 定义了一个名为 `my_function` 的函数，你可以这样调用它：

```c
void* handle = dlopen("libtest.so", RTLD_LAZY);
void (*test()) = dlsym(handle, "my_function");
test();
dlclose(handle);
```

`dlsym` 系统调用也可用于获取共享库中静态变量的值。

`dlopen` 和 `dlsym` 在失败时均返回 `NULL`。在这种情况下，你可以调用 `dlerror`（不带参数）来获取描述问题的人可读错误消息。

`dlclose` 函数卸载共享库。从技术上讲，`dlopen` 只有在库尚未加载时才会加载它。如果库已经加载，`dlopen` 仅仅是增加库的引用计数。同样，`dlclose` 会减少引用计数，并仅在引用计数达到零时才卸载库。

如果你用 C++ 编写共享库中的代码，你可能希望使用 `"extern 'C'"` 限定符声明你计划在其他地方访问的函数和变量。例如，如果 C++ 函数 `my_function` 在一个共享库中，而你想通过 `dlsym` 访问它，你应该这样声明它：

```cpp
extern 'C' void foo();
```

这可以防止 C++ 编译器将函数名 `foo` 修饰（mangling）成一个编码了关于函数额外信息的奇怪名称。C 编译器不会进行名称修饰；它将使用你提供给函数或变量的任何名称。

# 3 进程

程序的运行实例即进程。如果你在屏幕上显示了两个终端窗口，那么你可能运行了两次同一个终端程序——你有两个终端进程。每个终端窗口可能都在运行一个 shell；每个运行的 shell 都是另一个进程。当你从 shell 调用一个命令时，相应的程序会在新进程中执行；当该进程完成时，shell 会恢复运行。

高级程序员经常在单个应用程序中使用多个协作的进程，以便应用程序能够同时完成多项任务，增加应用程序的健壮性，并利用已有的程序。

本章描述的大多数进程操作函数与其他 UNIX 系统上的函数相似。大多数函数在 `<stdlib.h>` 或相关头文件中声明；请检查每个函数的帮助页（man page）以确保。

## 3.1 查看进程

即使你坐在电脑前，也有进程在运行。每个执行的程序都会使用一个或多个进程。让我们先看看电脑上已经运行的进程。

### 3.1.1 进程 ID

Linux 系统中的每个进程都由其唯一的进程 ID（process ID）识别，有时称为 pid。进程 ID 是 16 位数字，由 Linux 在创建新进程时按顺序分配。

每个进程都有一个父进程（第 3.4.3 节描述的特殊 `init` 进程除外）。因此，你可以将 Linux 系统上的进程想象成一棵树，以 `init` 进程为根。父进程 ID（或 ppid）仅仅是其父进程的进程 ID。

在 C 或 C++ 程序中引用进程 ID 时，请使用定义在 `<sys/types.h>` 中的 `pid_t` 类型定义。程序可以通过 `getpid()` 获取其运行进程的进程 ID，通过 `getppid()` 获取其父进程的进程 ID。例如，在示例 3.1 中，使用系统调用来打印这些 ID：

```c
#include <stdio.h>
#include <unistd.h>

int main () {
    printf("进程 ID: %d\n", getpid());
    printf("父进程 ID: %d\n", getppid());
    return 0;
}
```

### 3.1.2 查看活动进程

即使你坐在电脑前，也有进程在运行。每个执行的程序都会使用一个或多个进程。让我们先看看电脑上已经运行的进程。`ps` 命令显示当前的进程。例如：

```bash
PID     TTY     TIME     COMMAND
1       ?       0:00     /sbin/init
1234    pts/0   0:00     bash
```

#### 输出格式

`ps` 命令有多种输出格式。你可以使用 `-o` 选项指定输出字段。例如，`ps -o user,start_time` 显示：

```bash
USER       START
root       08:00
user       09:15
```

`ps` 命令的许多选项可以改变输出。例如，`-e` 显示所有进程，`-f` 显示详细格式，`-j` 显示进程树。例如：

```bash
ps -ef
```



### ps -ef 输出示例

```
ps -ef

UID        PPID  PID STIME TTY          CMD

root           0     1 S?        0:00:02 /sbin/init

root           1     2 S?        0:00:00 /libd/systemd

user          1000 1234 S pts/0    0:00:00 bash --color=auto
```

#### 进程状态

`ps` 命令可以显示进程的状态。例如：

```bash
STAT

S

R

R
```

`STAT` 列显示进程的各种状态。

### 3.1.3 杀死进程

你可以使用 `kill` 命令杀死运行的进程。只需指定要杀死的进程命令行。

`kill` 命令通过向进程发送 `SIGTERM` 信号来工作。这会导致进程终止，除非执行程序显式地处理或管理 `SIGTERM`。你也可以使用 `kill` 命令发送其他信号。

## 3.2 创建进程

它是父进程的副本。Linux 提供了另一组函数，即 `exec` 族，它们可以使特定进程停止作为某个程序的实例，转而变为另一个程序的实例。要产生一个新进程，你首先使用 `fork` 创建当前进程的副本。然后你使用 `exec` 将这些进程中的一个转换为你想要启动的程序的实例。

#### 调用 fork

当程序调用 `fork` 时，系统会创建一个复制的进程，称为子进程。父进程从调用 `fork` 的点继续执行程序。子进程也从相同的位置开始执行相同的程序。

那么，这两个进程之间有什么区别呢？首先，子进程是一个新进程，因此它有一个新的 ID，与父进程的进程 ID（PID）不同。进程区分自己是处于父进程还是子进程的一种方法是调用 `getpid`。然而，`fork` 函数返回父进程和子进程的返回值是不同的——它们“进入” `fork` 调用，然后两个进程带着“不同的返回值”“出来”。父进程中的返回值是子进程的 ID。子进程中的返回值为零。因为任何进程的 ID 都不为零，这使得程序很容易判断自己现在是否作为父进程运行。

列表 3.3 是使用 `fork` 复制程序进程的示例。注意，`if` 语句的第一个块仅在父进程中执行，而 `else` 分句在子进程中执行。

#### 列表 3.3 (fork.c) 使用 fork 复制程序的进程

```c
#include <stdio.h>

#include <sys/types.h>

#include <unistd.h>

int main () {

    pid_t child_pid;

    printf("the main program process ID is %d\n", (int) getpid());

    child_pid = fork ();

    if (child_pid == 0) {

        printf("this is the parent process, with id %d\n", (int) getpid());

        printf("the child's process ID is %d\n", (int)child_pid);

    } else {

        printf("this is the child process, with id %d\n", (int) getpid());

    }

    return 0;

}
```

#### 使用 exec 族

`exec` 函数将进程中运行的程序替换为另一个程序。当程序调用 `exec` 函数时，该进程会立即停止执行当前程序，并从头开始执行新程序，假设 `exec` 调用没有遇到错误。

在 `exec` 族中，这些函数在功能和调用方式上略有不同。

- 名称中包含字母 `p` 的函数（`execvp` 和 `execlp`）接受一个程序名，并在当前执行路径中按名查找程序；不包含 `p` 的函数必须是要执行的程序的完整路径。
- 名称中包含字母 `v` 的函数（`execv`、`execvp` 和 `execve`）接受一个 `NULL` 结尾的字符串指针数组作为新程序的参数列表。包含字母 `l` 的函数（`execl`、`execpl` 和 `execl`）使用 C 语言的变长参数机制来接受参数列表。
- 名称中包含字母 `e` 的函数（`execve` 和 `execl`）接受一个额外的参数，即环境变量的数组。该参数应该是一个 `NULL` 结尾的字符字符串指针数组。每个字符字符串的格式应为 `VARIABLE`。

由于 `exec` 会将调用程序替换为另一个，除非发生错误，否则它永远不会返回。

传递给程序的参数列表类似于你从 shell 运行程序时指定的命令行参数。这些参数通过 `main` 函数的 `argc` 和 `argv` 参数可用。记住，当程序被 shell 调用时，shell 会将参数列表的第一个元素（`argv[0]`）设置为程序名，将参数列表的第二个元素（`argv[1]`）设置为第一个命令行参数，依此类推。当你在程序中使用 `exec` 函数时，你也应该将函数名作为参数列表的第一个元素传递。

#### 结合使用 fork 和 exec

在程序内部运行子进程的常用模式是首先 `fork` 进程，然后 `exec` 子进程。这允许调用程序在父进程中继续执行，而调用程序在子进程中被子进程替换。

列表 3.4 中的程序与列表 3.2 类似，使用 `ls` 命令列出根目录的内容。不过，与上一个示例不同的是，它直接调用了 `ls` 命令，并将 `-l` 和 `-r` 作为命令行参数传递，而不是通过 shell 调用。

#### 列表 3.4 (fork-exec.c) 结合使用 fork 和 exec

```c
#include <stdio.h>

#include <sys/types.h>

#include <unistd.h>

/* 启动一个运行 ls 的子进程 */

void spawn(char *program, char *arglist[]) {

    pid_t child_pid;

    /* 启动一个运行 ls 的子进程 */

    child_pid = fork();

    if (child_pid == 0) {

        /* 这是子进程 */

        execvp(program, arglist);

        /* 如果 execvp 返回，说明发生了错误 */

        fprintf(stderr, "an error occurred\n");

        exit(1);

    } else {

        /* 这是父进程 */

        printf("done\n");

    }

}

int main () {

    /* execvp 的参数列表 */

    char *arglist[] = {"ls", "-l", "-r", NULL};

    spawn("ls", arglist);

    return 0;

}
```

### 3.2.3 进程调度

Linux 独立地调度父进程和子进程；无法保证哪一个会运行，或者运行多久。特别是，某些或全部的 `nice` 命令可能会在父进程完成之前运行。

Linux 保证每个进程最终都会运行——不会有进程会被剥夺资源。

你可以通过为进程分配更高的 nice 值（习性值）来指定该进程不重要——并获得较低的优先级。默认情况下，每个进程的 `nice` 值均为 0。较高的 `nice` 值意味着进程优先级较低；相反，较低（即负）的 `nice` 值可以获得更多的执行时间。

要运行具有非零 `nice` 值的程序，请使用 `nice` 命令并通过 `-n` 选项指定 `nice` 值。例如，你可以这样调用 `sort input.txt > output.txt` 命令（这是一个耗时的排序操作），降低其优先级以防减慢系统：

```bash
nice -n 10 sort input.txt > output.txt
```

你可以使用 `renice` 从命令行更改运行进程的 `nice` 值。

通过编程方式更改运行进程的 `nice` 值，请使用 `nice` 函数。它的参数是一个增量值，会加到它调用的进程的 `nice` 值上。记住，正值会提高 nice 值，从而降低进程优先级。

注意，只有具有 `root` 权限的进程才能运行负 nice 进程或降低运行进程的 `nice` 值。这意味着只有以 `root` 身份登录时，才能向 `nice` 和 `renice` 命令指定负值，且只有以 `root` 运行的进程才能向 `nice` 函数传递负值。这防止了普通用户抢夺其他用户的执行优先级。

## 3.3 信号

信号是 Linux 中进程通信的机制。信号是一个很大的课题；在这里我们讨论控制进程的重要信号和技术。

信号是发送给进程的特殊消息。信号是异步的；当进程接收到信号时，它会立即处理信号，而不会完成当前函数甚至当前行代码。有几十种信号，每种都有不同的名称。每个信号类型通过其数字指定，但在程序中，我们通常通过名称引用信号。

当进程接收到信号时，它可能会执行几种操作中的一种，具体取决于信号的处置方式（disposition）。对于每个用途，都有一个默认处置方式，它决定了当程序没有指定其他行为时，进程会发生什么情况。对于大多数信号类型，程序可以指定其他行为——要么忽略该信号，要么调用信号处理函数（`signal-handler function`）来响应信号。如果传递了信号处理函数，则会执行当前运行的程序，当信号处理函数返回后，程序将恢复执行。

Linux 系统根据特定条件向进程发送信号。例如，`SIGBUS`（总线错误）、`SIGSEGV`（段错误）、`SIGFPE`（浮点异常）可能被发送给执行了非法操作的进程。这些信号的默认处置方式是终止进程并产生核心转储文件（core file）。

进程也可以向另一个进程发送信号。这种机制的一个常见用途是向其发送 `SIGTERM` 或 `SIGKILL` 信号。另一个常见用途是向运行中的程序发送命令。“用户定义”信号预留用于此目的：`SIGUSR1` 和 `SIGUSR2`。`SIGHUP` 信号也用于某些目的，唤醒空闲程序或导致进程重新加载其配置文件。

`signal` 函数可以用于设置信号处置方式。第一个参数是信号值。接下来两个参数是指向信号结构体的指针；其中第一个包含该信号值所需的处置方式，而第二个则接收之前的处置方式。第二个信号结构体中最重要的字段是 `sa_handler`。它可以取三个值之一：

- `SIGDFL`，指定信号的默认处置方式。
- `SIGIGN`，指定该信号应该被忽略。
- 指向信号处理函数的指针。该函数应该接收一个参数（即信号值），并返回 `void` 类型。

由于信号是异步的，当处理信号时以及信号处理函数执行期间，主程序可能处于一种非常脆弱的状态。因此，你应该避免在信号处理函数中执行任何 I/O 操作，或调用大多数库函数和系统函数。

信号处理函数应该只执行响应信号所需的最少工作，然后将控制权交还给主程序（或终止程序）。在大多数情况下，这仅仅是记录信号发生的这一事实。然后，主程序会检查是否发生了信号，并采取相应的行动。

信号处理函数可能会被另一个信号中断。虽然这听起来像是一个罕见事件，但如果确实发生了，将非常难以诊断和调试问题（这是一个竞态条件的示例，在第 4 章“线程”第 4.4 节“同步与关键区”中有讨论）。因此，你应该对程序在信号处理函数中的操作小心。

3. 有什么区别？`SIGTERM` 信号请求进程终止；进程可以通过掩盖或忽略信号来忽略它。`SIGKILL` 信号总是立即杀死进程，因为进程可能无法掩盖或忽略 `SIGKILL`。

即使给全局变量赋值也可能是危险的，因为赋值可能通过两条或多条机器指令完成，而在它们之间可能会发生第二个信号，导致变量处于损坏状态。如果你使用全局变量来标记来自信号处理函数的信号，它应该是特殊类型 `sig_atomic_t`。在 Linux 中，`sig_atomic_t` 是一个普通的 `int`；对它的赋值是原子的。不过，如果你想编写可以移植到任何标准 UNIX 系统的程序，请对这些变量使用 `sig_atomic_t`。例如，列表 3.5 中的这个骨架使用信号处理函数来统计程序接收 `SIGUSR1` 的次数。

列表 3.5 使用信号处理函数
```c
#include <signal.h>

#include <stdio.h>

#include <string.h>

#include <sys/types.h>

#include <unistd.h>

sig_atomic_t sig1_count = 0;

void handler (int signal_number) {

    ++sig1_count;

}

int main () {

    struct sigaction sa;

    memset(&sa, 0, sizeof(sa));

    sa.sa_handler = &handler;

    sigaction(SIGUSR1, &sa, NULL);

    /* 在这里做一些长时间的操作。 */

    /* ... */

    printf("SIGUSR1 was raised %d times\n", sig1_count);

    return 0;

}
```

## 3.4 进程终止

通常，进程以两种方式之一终止：要么执行中的程序调用了 `exit` 函数，要么程序的 `main` 函数返回。每个进程都有一个退出码：退出码是传递给 `exit` 函数的参数或 `main` 返回的值。

进程还可能响应信号异常终止。之前提到的 `SIGBUS`、`SIGSEGV` 和 `SIGFPE` 信号会导致进程终止。其他信号用于显式终止进程。当用户尝试通过在终端输入 `Ctrl+C` 来终止进程时，会向进程发送 `SIGINT` 信号。`SIGTERM` 信号是终止进程的默认处置方式。通过调用 `abort` 函数，进程会向自己发送信号并产生核心转储文件。最强大的信号是 `SIGKILL`，它会立即结束进程且无法被程序阻塞。

可以使用 `kill` 命令通过指定额外的命令行标志来发送这些信号中的任何一个；例如，通过发送 `SIGKILL` 来结束一个麻烦的进程，调用以下命令，其中进程的 ID 为：`kill -KILL pid`。

要从程序发送信号，请使用 `kill` 函数。第一个参数是目标 ID。第二个参数是信号值。

你可以使用 `WIFEXITED` 宏根据子进程的退出状态判断进程是正常退出（通过 `exit` 函数或从 `main` 函数返回）还是由于未处理的信号死亡。在后的情况下，使用 `WTERMSIG` 宏从其退出状态中提取导致死亡的信号编号。

这里是 `fork` 和 `exec` 示例中的 `main` 函数。这次，父进程调用 `wait` 等待执行 `ls` 命令的子进程完成。

```c
int main () {

    int child_status;

    /* 传递给 "ls" 命令的参数列表。 */

    char *arg_list[] = {

        "ls", argv[0], // 程序的名字

        "-l",

        NULL /* 参数列表必须以 NULL 结尾。 */

    };

    /* 产生一个运行 "ls" 命令的子进程。忽略返回的子进程 ID。 */

    spawn ("ls", arg_list);

    /* 等待子进程完成。 */

    wait(&child_status);

    if (WIFEXITED(child_status))

        printf("the child process exited normally, with exit code %d\n", WEXITSTATUS(child_status));

    else

        printf("the child process exited abnormally\n");

    return 0;

}
```

Linux 中提供了几个类似的系统调用，它们提供了关于退出子进程的更多信息。`waitpid` 函数可以用于等待特定进程退出，而不是任何子进程。`wait3` 函数返回关于退出子进程的 CPU 使用统计信息，而 `wait4` 函数允许你指定关于等待哪些进程的额外选项。

### 3.4.3 僵尸进程

如果子进程在父进程调用 `wait` 函数时终止，该进程就会消失，其终止状态将通过 `wait` 调用传递给父进程。但当子进程终止而父进程没有调用 `wait` 时会发生什么？它会直接消失吗？不会，因为关于其终止的信息——例如它是否正常退出以及如果是，退出状态是什么——将会丢失。相反，当子进程终止时，它会变成僵尸进程。

## 第 3 章 进程

僵尸进程是一个已经终止但尚未被清理的进程。父进程负责清理它的僵尸子。`wait` 函数也做到了这一点，在等待子进程之前没有跟踪它是否仍在执行。例如，假设一个程序 `fork` 了一个子进程，执行了一些计算，然后调用了 `wait`。如果此时子进程尚未终止，父进程将在 `wait` 调用处阻塞，直到子进程完成。如果子进程在父进程调用 `wait` 之前完成，子进程就会变成僵尸。当父进程调用 `wait` 时，会提取子进程的终止状态，子进程被删除，`wait` 调用立即返回。

如果父进程不清理它的孩子会发生什么？它们将以僵尸进程的形式留在系统中。列表 3.6 中的程序 `fork` 了一个子进程，该子进程立即终止然后睡眠一分钟，而从未清理过该进程。

列表 3.6 (zombie.c) 创建一个僵尸进程

```c
#include <stdio.h>

#include <sys/types.h>

#include <unistd.h>

int main () {

    pid_t child_pid;

    /* 创建一个子进程。 */

    child_pid = fork ();



```c
    if (child_pid > 0) {

        /* 这是父进程。睡眠一分钟。 */

        sleep(60);

    } else {

        /* 这是子进程。立即退出。 */

        exit(0);

    }

    return 0;

}
```

将此文件编译为名为`make-zombie`的可执行文件。运行它，并在它仍在运行时，在另一个窗口中通过以下命令列出系统上的进程：

```bash
$ ps -e -o pid,ppid,stat,cmd
```

这列出了进程 ID、父 ID、进程状态和进程命令行。观察发现，除了父`make-zombie`进程外，还列出了另一个`make-zombie`进程。它是子进程；注意它的父 ID 是主`make-zombie`进程的 ID。子进程被标记为`<defunct>`，其状态码为`Z`，代表 zombie。

当父进程退出且从未调用过`wait`时，主`make-zombie`进程结束时会发生什么？僵尸进程还会留在那里吗？不会——尝试再次运行，你会发现两个`make-zombie`进程都消失了。当一个进程退出时，它的子进程会被特殊进程——`init`程序继承，它始终以进程 ID 1 运行（它是 Linux 启动时启动的进程）。`init`进程会自动清理它继承的所有子进程。

### 3.4.4 异步清理子进程

如果你使用子进程来`exec`另一个程序，在父进程中立即调用`wait`是可以的，它会阻塞直到子进程完成。但你可能希望父进程继续运行，因为一个或多个孩子是异步执行的。你如何确保清理了已完成的子进程，以便不会留下消耗系统资源的僵尸呢？

一种方法是父进程定期调用`wait3`或`wait4`来清理僵尸孩子。如果没有子进程终止，为此目的调用`wait`效果并不好。（此处原文 OCR 文本似乎乱码，已根据上下文清理逻辑流）。

## 4 线程

线程与进程一样，允许程序一次同时做更多事情。与进程不同，线程看起来是并发运行的；Linux 内核异步调度它们，通过中断每个线程来给其他线程执行的机会。从概念上讲，线程存在于进程内部。线程是进程更细粒度的执行单元。当你调用一个程序时，Linux 创建一个新的进程并在该进程创建一个单线程，按顺序运行程序。该线程可以创建额外的线程；所有线程在同一个进程中运行同一个程序，但每个线程可能在随时执行程序的不同部分。

我们已经看到程序如何`fork`子进程。子进程最初拥有父进程的虚拟内存、文件描述符等。子进程可以修改文件描述符而不影响其父进程，反之亦然。但当程序创建另一个线程时，没有任何被复制。创建的线程与原始线程共享内存空间、文件描述符和其他资源。例如，如果一个线程更改了变量的值，其他线程将看到修改后的值。同样，如果一个线程关闭了文件描述符，其他线程可能无法读取

从该文件描述符读取或写入内容。由于一个进程及其所有线程同一时间只能执行一个程序，如果进程中的任何线程调用了某个 exec 函数之一，所有其他线程都将结束（新程序可能会启动，或者创建新线程）。

GNU/Linux 实现了 POSIX 标准线程 API（称为 threads）。所有的线程函数和数据类型均在头文件`<pthread.h>`中声明。pthread 函数没有包含在 C 库中。相反，它们在`libthread`中，因此在链接程序时，你应该在命令行中添加`-lpthread`。

## 4.1 线程创建

进程中的每个线程都通过线程 ID（thread ID）标识。在 C 或 C++ 程序中引用线程 ID 时，请使用`pthread_t`类型。
在创建时，每个线程都会执行一个线程函数。这是一个普通函数，包含了线程应该运行的代码。在 GNU/Linux 中，线程函数接受一个类型为`void*`的参数，并具有`void*`返回类型。该参数是线程参数：GNU/Linux 将该值传递给线程，而不对其进行内容。你的程序可以使用此参数将数据传递给新线程。同样，你的程序可以使用返回值将数据从退出的线程传回给创建者。

`pthread_create`函数创建一个新线程。你向它提供以下内容：

- 1. 指向`pthread_t`变量的指针，其中存储新线程的线程 ID。
- 2. 指向线程属性对象的指针。该对象控制线程如何与程序其他部分交互的细节。如果你传递`NULL`作为属性，则将使用默认线程属性创建线程。线程属性将在第 4.1.5 节“线程属性”中讨论。
- 3. 指向线程指针。这是一个普通函数指针，类型为：`void (*)(void*)`
- 4. 一个类型为`void*`的线程参数。无论你传递什么，当线程开始执行时，都会作为参数传递给线程函数。

调用`pthread_create`会立即返回，原始线程继续执行调用之后的指令。同时，新线程开始执行线程函数。Linux 异步地调度这两个线程，你的程序不能依赖于两个线程中指令执行的相对顺序。

列表 4.1 中的程序创建了一个持续向标准错误打印 x 的线程。在调用`pthread_create`之后，主线程持续向标准错误打印 o。

### 列表 4.1 (thread-create.c) 创建线程

```c
#include <pthread.h>

#include <stdio.h>

/* 向 stderr 打印 x。参数未被使用。不返回。 */
void* print_xs(void* unused) {
    while (1) {
        fputs('x', stderr);
    }
    return NULL;
}

/* 主程序。 */
int main() {
    pthread_t thread_id;
    /* 创建一个新线程。新线程将运行 print_xs 函数。 */
    pthread_create(&thread_id, NULL, &print_xs, NULL);
    /* 向 stderr 持续打印 o。 */
    while (1) {
        fputs('o', stderr);
    }
    return 0;
}
```

使用以下代码编译并链接此程序：`cc -o thread-create thread-create.c -lpthread`

尝试运行它看看发生什么。注意当 Linux 交替调度两个线程时，x 和 o 的出现模式是不可预测的。

通常情况下，线程以两种方式之一退出。一种方法（如前所示）是通过从线程函数返回。线程函数的返回值被视为线程的返回值。另一种是线程可以显式地通过调用`pthread_exit`退出。该函数可以在线程函数内部调用，也可以从线程函数直接或间接调用的其他函数调用。`pthread_exit`的参数是线程的返回值。

### 4.1.1 向线程传递数据

线程参数为向线程传递数据提供了一种方便的方法。但由于参数的类型是`void*`，你无法直接通过参数传递大量数据。相反，可以使用线程参数作为指向某些结构体或数据数组的指针。常用方法是为每个线程函数定义一个结构体，包含线程函数期望的“参数”。

使用线程参数，很容易为多个线程复用同一个线程函数。所有这些线程都执行相同的代码，但处理的是不同的数据。

列表 4.2 中的程序与之前的示例类似。它创建了两个新线程，一个用于打印 xs，另一个无限打印 o，不过每个线程都打印固定数量的字符并通过从线程函数返回来退出。两个线程都使用同一个线程函数`char_print`，每个线程都使用`struct char_print_parms`进行不同的配置。

### 列表 4.2 (thread-create2) 创建两个线程

```c
#include <pthread.h>

#include <stdio.h>

/* 打印函数。 */
struct char_print_parms {
    /* 要打印的字符。 */
    char character;
    /* 打印的次数。 */
    int count;
};

/* 根据 PARAMETERS 向 stderr 打印数量的字符，
PARAMETERS 是一个指向 struct char_print_parms 的指针。 */
void char_print(void * parameters) {
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* (此处对应原文错乱的代码部分，按样翻译注释) */
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;
    /* 将 cookie 转换为正确的类型。 */
    struct char_print_parms *p = (struct char_print_parms*) parameters;
    int i;

    // ... (此处由于原文文本混乱，仅翻译核心结构部分)
}
```



```c
void char_print(void * parameters) {

    struct char_print_parms *p = (struct char_print_parms*) parameters;

    int i;

    for (i = 0; i < p->count; i++) {

        fprintf(stderr, "%c", p->character);

    }

    return NULL;

}

int main () {

    pthread_t thread_id;

    pthread_t thread_id;

    struct char_print_parms thread1_args;

    struct char_print_parms thread2_args;

    /* 创建一个新线程打印30000个 x。 */

    thread1_args.character = 'x';

    thread1_args.count = 30000;

    pthread_create(&thread_id, NULL, &char_print, &thread1_args);

    /* 创建另一个新线程打印20000个 o。 */

    thread2_args.character = 'o';

    thread2_args.count = 20000;

    pthread_create(&thread_id, NULL, &char_print, &thread2_args);

    return 0;

}
```

列表 4.2 中的程序与之前的示例相似。这个程序创建了两个新线程，一个用于打印 `xs`，另一个无限打印 `o`，不过每个线程都打印固定数量的字符并通过从线程函数返回来退出。两个线程都使用同一个线程函数 `char_print`，每个线程都使用 `struct char_print_parms` 进行不同的配置。

### 列表 4.2 (thread-create2) 创建两个线程

```c
#include <pthread.h>

#include <stdio.h>

/* 打印函数。 */

struct char_print_parms {

    /* 要打印的字符。 */

    char character;

    /* 打印的次数。 */

    int count;

};

/* 根据 PARAMETERS 向 stderr 打印数量的字符，
PARAMETERS 是一个指向 struct char_print_parms 的指针。 */

void char_print(void * parameters) {

    /* 将 cookie 转换为正确的类型。 */

    struct char_print_parms *p = (struct char_print_parms*) parameters;

    int i;

    // ... (省略后续重复行)
}
```

### 4.1.2 Joining 线程

让 `main` 等待线程完成。该函数是 `pthread_join`，它接受两个参数：要等待的线程 ID，以及一个接收返回值的指针。如果你不关心返回值，对第二个参数传递 `NULL`。

### 4.1.3 线程返回值

如果你传递给 `pthread_join` 的第二个参数非空，则线程的返回值将放置在该参数所指向的位置。线程返回值与线程参数一样，类型为 `void*`。如果你想传回单个 `int` 或其他小数字，你可以通过将值转换为 `void*`，并在调用 `pthread_join` 后将其转换回相应的类型。

列表 4.4 中的程序在独立的线程中计算第 n 个素数。该线程将其所需的素数作为返回值返回。同时，主线程是你需要执行其他代码的地方。注意 `compute_prime` 中使用的连续除法算法相当无效；如果你打算在程序中计算许多素数，请查阅数值算法书籍。

- 注意这是不可移植的，你必须确保你的值可以安全地转换为 `void*` 且不丢失位。

## 4.1 线程创建

### 列表 4.4 (primes.c) 在线程中计算素数

```c
#include <pthread.h>

#include <stdio.h>

/* 计算连续的素数（效率非常低）。返回第 N 个素数，其中 N 是 *ARG 指针指向的值。 */

void* compute_prime(void *arg) {

    int candidate = 2;

    int n = *((int*)arg);

    while (1) {

        int factor;

        int is_prime = 1;

        /* 通过连续除法测试素数性。 */

        for (factor = 2; factor < candidate; ++factor) {

            if (candidate % factor == 0) {

                is_prime = 0;

                break;

            }

        }

        /* 这个就是我们要找的那个素数吗？ */

        if (--n == 0) {

            /* 将所需的素数作为线程返回值返回。 */

            return (void*)candidate;

        }

        ++candidate;

    }

    return NULL;

}

int main() {

    pthread_t thread;

    int which_prime = 5000;

    int prime;

    /* 启动计算线程，计算到第 5000 个素数。 */

    pthread_create(&thread, NULL, compute_prime, &which_prime);

    /* 在这里做一些其他工作... */

    /* 等待素数线程完成并获取结果。 */

    pthread_join(thread, (void*)&prime);

    /* 打印计算出的最大素数。 */

    printf("第 %d 个素数是 %d\n", which_prime, prime);

    return 0;

}
```

### 4.1.4 关于线程 ID (Thread IDs)

有时，代码序列需要确定是哪个线程在执行它是很有用的。`pthread_self` 函数返回调用它时所在线程的 ID。可以使用 `pthread_equal()` 函数将此线程 ID 与另一个 ID 进行比较。

这些函数对于判断特定的线程 ID 是否对应当前线程非常有用。例如，线程通过 `pthread_join` 加入自身是一个错误。（在这种情况下，`pthread_join` 将返回错误代码 EDEADLK。）为了提前检查这一点，你可能会使用如下代码：

```c
if (pthread_equal (pthread_self (), other_thread))

    pthread_join(other_thread, NULL);
```

### 4.1.5 线程属性 (Thread Attributes)

线程属性提供了一种精细调整单个线程行为的机制。回想一下，`pthread_create` 接受一个参数是指向线程属性对象的指针。如果你传递一个空指针，将使用默认属性来配置新线程。然而，你可以创建并自定义一个线程属性对象，以为属性指定其他值。

要指定自定义的线程属性，你必须遵循以下步骤：

1.  创建一个 `pthread_attr_t` 对象。最简单的方法是声明一个该类型的自动变量。
2.  调用 `pthread_attr_init` 并传递指向该对象的指针。这会将属性初始化为默认值。
3.  修改属性对象以包含所需的属性值。
4.  在调用 `pthread_create` 时传递属性对象的指针。
5.  调用 `pthread_attr_destroy` 释放属性对象。`pthread_attr_t` 的默认值不会被解内存；它可以使用 `pthread_attr_init` 重新初始化。

一个线程属性可以启动多个线程。在线程创建后，没有必要保留线程属性。

对于 GNU/Linux 编程任务，通常只对一种线程属性感兴趣（其他属性主要用于实时编程）。这个属性是线程的状态属性。线程可以被创建为可连接线程（joinable thread，默认值）或分离线程（detached thread）。可连接线程像进程一样，在终止时不会被 GNU/Linux 自动清理。相反，线程的退出状态会一直悬挂在系统中的（类似于僵尸进程），直到另一个线程调用 `pthread_join` 获取其返回值。只有在那个那时，它的资源才会被释放。相比之下，分离线程在终止时会立即自动清理。由于是分离线程，另一个线程可能无法通过 `pthread_join` 在其完成时进行同步，也无法获取其返回值。

要在线程属性对象中设置分离状态，请使用 `pthread_attr_setdetachstate`。第一个参数是指向线程属性对象的指针，第二个参数是期望的分离状态。由于连接状态是默认值，因此只有在创建分离线程时才需要调用此函数；将 `PTHREAD_CREATE_DETACHED` 作为第二个参数传递。

列表 4.5 中的代码通过为线程设置分离线程属性来创建一个分离线程。

### 列表 4.5 (detached.c) 创建分离线程的骨架程序

```c
#include <pthread.h>

void* thread_function(void* thread_arg)

{

    /* 在这里做工作... */

}

int main ()

{

    pthread_attr_t attr;

    pthread_t thread;

    pthread_attr_init(&attr);

    pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED);

    pthread_create(&thread, &attr, &thread_function, NULL);

    pthread_attr_destroy(&attr);

    /* 在这里做工作... */

    /* 不需要连接第二个线程。 */

    return 0;

}
```

即使线程是以可连接状态创建的，以后也可以通过调用 `pthread_detach` 将其转换为分离线程。

## 4.2 线程取消 (Thread Cancellation)

在正常情况下，线程通过从其函数返回或调用 `pthread_exit` 来终止。然而，线程可以请求另一个线程终止，这被称为取消线程。调用 `pthread_cancel` 并传递要取消线程的 ID。

通常线程可能处于某些必须全全执行执行的代码中。例如，线程可能会分配某些资源，使用它们，然后释放它们。如果线程在这些代码中间被取消，它可能没有机会释放资源，导致泄漏。为了应对这一点，线程可以控制是否以及何时被取消。参见 4.1.5 线程属性。

线程对于线程取消可以处于三种状态之一：

- 线程可以是异步取消的。线程可以在执行的任何一点被取消。
- 线程可以是同步取消的。相反，线程仅在特定的位点可以被取消。此时，取消请求会被放入队列，直到线程到达取消点。
- 线程可以是不可取消的。取消线程的尝试将被静地忽略。

初始创建时，线程是同步取消的。

### 4.2.1 同步和异步线程

异步取消的线程可以在执行的任何一点被取消。相比之下，同步取消的线程只有在执行的特定地方可以被取消。这些地方被称为取消点。线程将等待取消请求，直到到达取消点。

要使线程变为异步取消，请使用 `pthread_setcanceltype`。这影响实际调用该函数的线程。第一个参数应该是 `PTHREAD_CANCEL_ASYNRONOUS` 以使线程变为异步取消，或者 `PTHREAD_CANCEL_DEFERRED` 使其返回同步取消状态。第二个参数如果不为空，则是指向变量的指针，该变量将接收线程之前的取消类型。例如，此调用使调用线程变为异步取消。

```c
pthread_setcanceltype(PTHREAD_CANCEL_ASYNRONOUS, NULL);
```

什么构成取消点，这些点应该放置在哪里？创建取消点最直接的方法是调用 `pthread_testcancel`。对于同步取消的线程，除了处理等待中的取消请求外什么都不做。你应该在线程函数进行长时间计算期间定期调用 `pthread_testcancel`，放置在可以被取消而不会泄漏任何资源或产生其他影响的地方。

某些其他函数也是隐式的取消点。这些函数在 `pthread_cancel` 手页上列出。注意，其他函数可能会内部使用这些函数，因此将间接成为取消点。

### 4.2.2 不可取消的临界区

线程可以通过 `thread_setcancelstate` 函数完全禁用自身的取消功能。与 `pthread_setcancancype` 类似，这影响的是调用线程。第一个参数 `PTHREAD_CANCEL_DISABLE` 用于禁用取消，或者 `PTHREAD_CANCEL_ENABLE` 用于重新启用取消；如果不为 `NULL`，则指向一个将用于接收之前的取消状态的指针。例如，此调用会禁用调用线程的取消功能。

```
thread_setcancelstate (PTHREAD_CANCEL_DISABLE, NULL);
```

使用 `pthread_setcancelstate` 允许你实现临界区。临界区是一段必须完整执行或完全不执行的代码序列；换句话说，如果一个线程开始执行临界区，它必须继续执行到该区域结束而不被取消。

例如，假设你正在编写一个银行程序的程序，将资金从一个账户转移到另一个账户。为了实现这一点，你必须向一个账户的余额增加金额，并从另一个账户的余额中减去相同的金额。如果运行例程的线程在两个操作之间的恰恰错误时间被取消，程序将因为未能完成交易而错误地增加了银行的总存款。为了防止这种情况的发生，请将这两个操作放在临界区中。

你可能使用如 `process_transaction` 的函数来实现转移，如列表 4.6 所示。该函数在修改账户余额之前会禁用线程取消以启动临界区。

### 列表 4.6 (critical-section.c) 使用临界区保护银行交易

```
#include <pthread.h>

#include <stdio.h>

#include <string.h>

/* 账户余额数组，通过账户号索引。 */

float* account_balances;

/* 将 DOLLARS 从账户 FROM_ACCT 转移到 TO_ACCT。
如果交易成功则返回 0，如果 FROM_ACCT 的余额太小则返回 1。 */

int process_transaction (int from_acct, int to_acct, float dollars)

{

    int old_cancel_state;

    /* 检查 FROM_ACCT 的余额。 */

    if (account_balances[from_acct] < dollars)

        return 1;
```



#### 列表 4.6 继续

注意，在临界区结束时恢复旧的取消状态，而不是无条件地设置为 `PTHREAD_CANCEL_ENABLE` 是非常重要的。这允许你从另一个临界区安全地调用 `process_transaction` 函数——在这种情况下，你的函数将保持它被调用时的取消状态。

### 4.2.3 何时使用线程取消

通常情况下，除非在特殊情况下，否则不使用线程取消来结束线程的执行是一个好主意。在正常运行期间，更好的策略是指示线程它应该退出，然后等待线程按照自己的顺序方式退出。我们将在本书的后续部分讨论与线程通信的技术，并在第 5 章“进程间通信”。

## 4.3 线程特定数据

与进程不同，同一个程序中的所有线程共享相同的地址空间。这意味着如果一个线程修改了内存中的一个值（例如全局变量），更改对所有其他线程都是可见的。这允许多个线程在不使用进程间通信机制（在第 5 章中描述）的情况下操作相同的数据。

然而，每个线程都有自己的调用堆栈。这允许每个线程执行不同的代码，并以通常的方式调用和返回子程序。与单线程程序一样，每个线程中每个子程序的调用都有自己的一组局部变量，这些变量存储在该线程的栈上。

然而，有时希望复制某个变量，以便每个线程都有单独的拷贝。GNU/Linux 通过为每个线程提供线程特定数据区域来支持这一点。存储在该区域中的变量会为每个线程复制一份，每个线程都可以修改其变量的拷贝而不影响其他线程。由于所有线程共享相同的内存空间，因此无法使用普通的变量引用访问线程特定数据。GNU/Linux 提供了特殊函数用于从线程特定数据区域设置和检索值。

你可以创建任意数量的线程特定数据项，每个项类型为 `void*`。项通过键进行引用。要创建一个新键，从而为每个线程创建一个新数据项，请使用 `pthread_key_create`。第一个参数是指向 `pthread_key_t` 变量的指针。该值可以被每个线程用于访问其对应数据项的拷贝。`pthread_key_t` 的第二个参数是一个清理函数。当每个线程退出时，GNU/Linux 会自动调用该函数，并传递与该键对应的线程特定值。这特别棘手，因为即使线程在执行的任意点被取消，清理函数也会被调用。如果线程特定值为 `NULL`，则不会调用清理函数。如果你不需要清理函数，可以传递 `NULL` 代替函数指针。

创建键后，每个线程可以通过调用 `pthread_setspecific` 设置其与该键对应的线程特定值。第一个参数是键，第二个是要存储的 `void*` 线程特定值。要检索线程特定数据项，请调用 `pthread_getspecific` 并传递键作为参数。

例如，假设你的应用程序将任务分配给多个线程。为了审计目的，每个线程都应该有一个单独日志文件，在其中记录线程任务的进度消息。线程特定数据区域是存储文件指针的方便地方。

### 列表 4.7 (tsd.c) 使用线程特定数据实现的每个线程日志文件

```c
#include <stdlib.h>
#include <pthread.h>
#include <stdio.h>

static pthread_key_t thread_log_key;

void close_thread_log(void* thread_log) {
  fclose((FILE*)thread_log);
}

void write_to_log(const char* message) {
  FILE* thread_log = (FILE*)pthread_getspecific(thread_log_key);
  fprintf(thread_log, "%s\n", message);
}

void thread_function(void* args) {
  char thread_log_filename[20];
  FILE* thread_log;

  /* 为此线程生成日志文件名。 */
  sprintf(thread_log_filename, "thread%d.log", (int) pthread_self());

  /* 打开日志文件。 */
  thread_log = fopen(thread_log_filename, "w");

  /* 将指针存储在 thread_log_key 下的线程特定数据中。 */
  pthread_setspecific(thread_log_key, thread_log);

  write_to_log("Thread starting.");

  /* 执行一些工作... */

  return NULL;
}

int main () {
  int i;
  pthread_t threads[5];

  /* 创建键以关联线程特定数据中的日志文件指针。
     使用 close_thread_log 清理文件指针。 */
  pthread_key_create(&thread_log_key, close_thread_log);

  /* 创建线程执行工作。 */
  for (i = 0; i < 5; ++i)
    pthread_create(&threads[i], NULL, thread_function, NULL);

  /* 等待所有线程完成。 */
  for (i = 0; i < 5; ++i)
    pthread_join(threads[i], NULL);

  return 0;
}
```

观察到 `thread_function` 没有关闭日志文件。这是因为日志文件已创建，且 `close_thread_log` 被指定为该键的清理函数。每当线程退出，GNU/Linux 都会调用该函数，传递线程日志键的线程特定值。该函数负责关闭日志文件。

## 4.3 线程特定数据 (Thread-specific Data)

### 4.3.1 清理处理器 (Cleanup Handlers)

线程特定数据键的清理函数对于确保线程在退出或被取消时不泄漏资源非常有用。然而，有时在不为每个线程创建重复的新的线程特定数据项的情况下，能够指定清理函数是有用的。GNU/Linux 为此目的提供了清理处理程序。

清理处理程序就是一个在线程退出时应该被调用的函数。该处理程序接收一个 `void*` 参数，其参数值在注册处理程序时提供——这使得使用同一个处理程序函数来处理多个实例变得非常简单。

清理处理程序是一种临时措施，仅当线程退出或被取消而不是完成特定代码区域的执行时，才用于释放资源。在正常情况下，当线程没有退出也没有被取消，应该显式地释放资源并移除清理处理程序。

要注册清理处理程序，请调用 `pthread_cleanup_push`，并传递处理程序的指针及其参数值。对 `pthread_cleanup_push` 的调用必须与相应的 `pthread_cleanup_pop` 调用匹配，后者会取消注册清理处理程序。为了方便，`pthread_cleanup_pop` 接受一个 `int` 标志；如果标志非零，则会在取消注册的同时实际执行清理操作。

列表 4.8 中的程序展示了如何使用清理处理程序来确保动态分配的缓冲区被清理。

列表 4.8 (cleanup.c) 展示线程清理的程序

```c
#include <malloc.h>
#include <pthread.h>

/* 分配一个临时缓冲区。 */
void* allocate_buffer(size_t size) {
    return malloc(size);
}

/* 释放临时缓冲区。 */
void deallocate_buffer(void* buffer) {
    free(buffer);
}

void do_some_work() {
    /* 分配一个临时缓冲区。 */
    void* temp_buffer = allocate_buffer(1024);

    /* 为此缓冲区注册清理处理器，以便在线程退出或被取消时释放它。 */
    pthread_cleanup_push(deallocate_buffer, temp_buffer);

    /* 执行一些可能会调用 pthread_exit 或被取消的工作... */

    /* 取消注册清理处理程序。因为在这种情况下 pthread_cleanup_pop 的参数是非零，所以清理函数 deallocate_buffer 在这里被自动调用，不需要显式调用。在简单简单的情况下，我们可以使用标准库函数 free 作为我们的清理处理程序。 */
}
```

### 4.3.2 C++ 中的线程清理

C++ 程序员习惯于通过在析构函数中封装操作来“免费”获得清理工作。当对象超出作用范围时（无论是因为块执行完毕还是因为抛出了异常），C++ 会确保对所有具有析构函数的自动变量调用析构函数。这提供了一种方便的机制，可以确保无论以何种方式退出块，清理代码都会被调用。

然而，如果线程调用了 `pthread_exit`，C++ 并不保证会对线程栈上的所有自动变量调用析构函数。恢复此功能的一种巧妙方法是通过抛出一个特殊异常，在线程的顶层调用 `pthread_exit`。列表 4.9 中的程序演示了这一点。使用这种技术，函数通过抛出 `ThreadExitException` 而不是调用 `pthread_exit` 来表示其退出线程的意图。异常在线程顶层中被捕获，随着异常向上传递，线程栈上的所有局部变量都将被正确销。

列表 4.9 (c-exit.cpp) 使用 C++ 实现安全的线程退出

```cpp
#include <pthread.h>

class ThreadExitException {
public:
    /* 创建一个带有返回值的用于信号线程退出的异常。 */
    ThreadExitException(void* return_value) : return_value_(return_value) {}

    /* 使用构造函数中提供的返回值实际退出线程。 */
    void* DoThreadExit() {
        pthread_exit(thread_return_value_);
    }

private:
    /* 退出线程时将使用的返回值。 */
    void* thread_return_value_;
};

void do_some_work() {
    while (1) {
        /* 在这里执行一些有用的事情... */
    }

    if (should_exit_thread_immediately())
        throw ThreadExitException(NULL /* 线程的返回值 = */ NULL);
}

void* thread_function(void*) {
    try {
        do_some_work();
    } catch (ThreadExitException ex) {
        /* 某些函数指示我们应该退出线程。 */
        ex.DoThreadExit();
    }
    return NULL;
}
```

## 4.4 同步与临界区 (Synchronization and Critical Sections)

使用线程进行编程非常复杂，因为大多数线程程序都是并发程序。特别是，没有办法知道系统何时调度一个线程运行，以及它何时运行。一个线程可能会运行很长时间，或者系统可能会在线程之间快速切换。在具有多个处理器的系统上，系统可能会让多个线程在字面上同一时刻运行。

调试线程程序是困难的，因为你总是无法重现导致问题的行为。你可能运行一次程序时一切正常；但下一次运行时，它可能会崩溃。没有方法能让系统调度线程的方式与之前完全相同。

大多数涉及线程的 bug 的根本原因是线程正在访问相同的数据。正如之前提到的，这会导致竞态条件。

### 4.4.1 竞态条件 (Race Conditions)

假设两个线程恰好同时检查队列，但只有一个任务剩余。第一个线程进入队列。此时，第二个线程也检查队列，发现它为空，但实际上任务正在被处理。在这种情况下，在队列为空时，线程函数可能看起来像列表 4.10 所示。

列表 4.10 (queue.c) 从队列处理任务的线程函数

```c
#include <malloc.h>
#include <pthread.h>

struct job {
    /* 分配一个临时缓冲区。 */
    struct job* next;

    /* 处理队列。 */
};

struct job* queue = NULL;

/* 处理队列。 */
void* thread_function(void* arg) {
    /* 分配一个临时缓冲区。 */
    struct job* next_job;

    while (queue != NULL) {
        /* 获取下一个任务。 */
        next_job = queue;
        queue = queue->next;

        /* 清理。 */
        free(next_job);
    }

    return NULL;
}
```

### 4.4.2 互斥锁 (Mutexes)

任务队列问题的解决方案是允许只有一个线程访问队列。线程开始查看队列时，其他线程不应该访问它，直到第一个线程决定是否处理任务并从列表中移除任务。实现这一点需要操作系统的支持。GNU/Linux 提供了互斥锁（mutexes）。互斥锁是一种特殊的锁，允许一次只有一个线程锁定。如果一个线程锁定互斥锁，然后另一个线程尝试锁定互斥锁，第二个线程会被阻塞或挂起。只有当第一个线程解锁互斥锁时，第二个线程才会被解除——允许恢复执行。GNU/Linux 保证在尝试锁定互斥锁的线程之间不会发生竞态条件；只有一个线程会获得锁，所有所有都被阻塞。

将互斥锁想象成厕所门上的锁。先进入厕所的人锁上门。如果有人在占用期间尝试进入，那个人会发现门锁着，被迫在外面等待，直到使用者离开。

要创建互斥锁，创建一个类型为 `pthread_mutex_t` 的变量，并将指针传递给 `pthread_mutex_init`。`pthread_mutex_init` 的第二个参数是互斥锁属性对象的指针，它指定了互斥锁的属性。正如

`pthread_create`，如果属性指针为空，则假设使用默认属性。互斥锁变量应初始化一次。这段代码片段演示了互斥锁变量的声明和初始化。

```
pthread_mutex_t mutex;
pthread_mutex_init(&mutex, NULL);
```

创建默认属性互斥锁的另一种简单方法是使用特殊值 `PTHREAD_MUTEX_INITIALIZER` 对其进行初始化。不需要额外调用 `pthread_mutex_init`。这对于全局变量（在 C++ 中则为静态数据成员）特别为方便。之前的代码片段可以写成这样：

```
pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
```

线程可以通过对互斥锁调用 `pthread_mutex_lock` 来尝试锁定该互斥锁。如果互斥锁处于未锁定状态，它将变为锁定状态并且函数立即返回。如果互斥锁已被另一个线程锁定，`pthread_mutex_lock` 会阻塞执行，并在当另一个线程解锁该互斥锁时才返回。可能有多个线程同时阻塞在一个锁定的互斥锁上。当互斥锁被解锁时，只有阻塞线程中的其中一个（随机选择）会被解除阻塞并允许锁定互斥锁；其他线程保持阻塞状态。

调用 `pthread_mutex_unlock` 会解锁互斥锁。此函数应始终由锁定该互斥锁的线程调用。

列表 4.11 显示了任务队列示例的另一个版本。现在队列由互斥锁保护。在访问队列（无论是读还是写）之前，每个线程都会首先锁定互斥锁。只有当完成检查队列和移除任务的整个序列后，互斥锁才会被解锁。这防止了之前描述的竞态条件。

## 列表 4.11 由互斥锁保护的任务队列函数

```c
#include <stdlib.h>
#include <pthread.h>

struct job {
    /* 链表的连接字段。 */
    struct job* next;

    /* 其他描述待执行任务的字段... */
};

/* 等待任务的链表。 */
struct job* job_queue;

/* 保护 job_queue 的互斥锁。 */
pthread_mutex_t job_queue_mutex = PTHREAD_MUTEX_INITIALIZER;

/* 处理队列中的任务直到队列为空。 */
void thread_function(void* arg) {
    while (1) {
        struct job* next_job;

        /* 锁定任务队列上的互斥锁。 */
        pthread_mutex_lock(&job_queue_mutex);

        /* 现在检查队列是否为空是安全的。 */
        if (job_queue == NULL)
            next_job = NULL;
        else {
            /* 获取下一个可用任务。 */
            next_job = job_queue;
            /* 从列表中移除此任务。 */
            job_queue = job_queue->next;
        }

        /* 解锁任务队列上的互斥锁，因为我们现在已经处理完队列。 */
        pthread_mutex_unlock(&job_queue_mutex);

        /* 队列为空吗？如果是，则结束线程。 */
        if (next_job == NULL)
            break;

        /* 执行任务。 */
    }
}
```



```c
        process_job(next_job);

        /* 清理。 */

        free(next_job);

    }

    return NULL;

}
```

所有对 `job_queue`（共享数据指针）的访问必须位于调用 `pthread_mutex_lock` 和调用 `pthread_mutex_unlock` 之间。存储在 `next_job` 中的任务对象只有在对象对象从队列中移除后，才在该区域之外被访问，因此它对其他线程是不可见的。

请注意，如果队列为空（即 `job_queue` 为 `null`），我们不会立即跳出循环，因为这会导致互斥锁被永久锁定，并防止任何其他线程访问任务队列。相反，我们通过将 `next_job` 设为 `null` 来记住这一点，并且在解锁互斥锁后才跳出循环。

使用互斥锁锁定 `job_queue` 代码不是自动的；这需要你自己在访问该变量之前添加锁定互斥锁的代码，并在之后进行解锁。例如，一个向任务队列添加任务的函数可能如下：

```c
void enqueue_job(struct job* new_job) {

    pthread_mutex_lock(&job_queue_mutex);

    new_job->next = job_queue;

    job_queue = new_job;

    pthread_mutex_unlock(&job_queue_mutex);

}
```

## 第 4 章 线程

### 4.4.3 互斥死锁

互斥锁提供了一种允许一个线程阻塞另一个线程执行的机制。这开启了一种新类型错误的可能性，称为死锁。当一个或多个线程等待某个将会发生的事情时，就会发生死锁。

当同一个线程尝试连续两次锁定互斥锁时可能会发生简单的死锁。这种行为取决于使用的互斥锁类型。存在三种互斥锁：

- 锁定快速互斥锁（默认类型）会导致死锁发生。尝试锁定互斥锁会阻塞，直到互斥锁被解锁。但由于持有互斥锁的线程阻塞在同一个互斥锁上，因此锁无法释放。
- 锁定递归互斥锁不会导致死锁。递归互斥锁可以被同一个线程安全地锁定多次。线程会记住该线程对 `pthread_mutex_lock` 的调用次数，该线程必须进行相同次数的 `pthread_mutex_unlock` 调用，互斥锁才能真正被解，并允许另一个线程锁定它。
- 锁定错误检查互斥锁不会导致死锁。如果线程尝试锁定已被另一个线程锁定的互斥锁，函数将立即返回错误代码 `EDEADLK`。

### 4.4.4 非阻塞互斥锁测试

有时，测试互斥锁是否被锁定而不进行阻塞是有用的。例如，一个线程可能需要锁定互斥锁，但如果互斥锁已被锁定，它可以执行其他工作。由于 `pthread_mutex_lock` 在互斥锁解锁之前不会返回，因此需要另一个函数。

GNU/Linux 提供了 `pthread_mutex_trylock` 用于此。如果你在未解锁的互斥锁上调用 `pthread_mutex_trylock`，你将像调用 `pthread_mutex_lock` 一样锁定互斥锁，并且 `pthread_mutex_trylock` 返回零。然而，如果互斥锁已被另一个线程锁定，`pthread_mutex_trylock` 不会阻塞。相反，它会立即返回错误 `EAGAIN`。你可以稍后重试。

### 4.4.5 线程信号量

在之前的示例中，如果多个线程从队列处理任务，线程的主函数执行下一个任务直到没有任务然后退出线程。这种方案在所有任务预先进入队列或新任务进入的速度至少等于线程处理的速度时是有效的。然而，如果线程运行得太快，任务队列将为空，线程将退出。如果之后有了新任务，可能没有剩余线程来处理它们。我们可能需要的机制是在队列为空时阻塞线程，直到新任务可用。

信号量提供了一种实现此点的方便方法。信号量是一种用于同步多个线程的计数器。通过互斥锁，GNU/Linux 保证检查或修改信号量的值可以安全进行，而不产生竞态条件。

每个信号量都有一个计数值，是非负整数。信号量支持两个基本操作：

- 将值减1。如果值已经是零，操作将阻塞，直到信号量的值变为正数（由于其他线程的操作）。当信号量的值变为正数时，它加1并且等待操作返回。
- 将信号量的值加1。如果信号量之前为零，则阻塞在该信号量上等待的线程中的其中一个，其等待操作将完成（这将信号量的值回到零）。

注意：GNU/Linux 提供了两种略有不同的信号量实现。我们在这里描述的是 POSIX 标准信号量实现。在线程间通信时请使用这些信号量。另一种用于进程间通信的实现请见第 5.2 节“进程信号量”。如果你使用信号量，请包含头文件 `<semaphore.h>`。

信号量由 `sem_t` 变量表示。在用 `sem_init` 函数对其初始化之前，需要传递指向 `sem_t` 变量的指针。第二个参数应为零，第三个参数是信号量的初始值。如果你不再需要某个信号量，最好用 `sem_destroy` 将其释放。

要等待信号量，请使用 `sem_wait`。要向信号量发送信号，请使用 `sem_post`。还提供了一个非阻塞函数 `sem_trywait`。它类似于 `pthread_mutex_trylock`——如果因为信号量的值为0而导致等待阻塞，则该函数将立即返回错误 `EAGAIN`，而不是进行阻塞。

GNU/Linux 还提供了一个用于获取信号量当前值的函数 `sem_getvalue`，它将值放在其第二个参数所指向的 `int` 变量中。你不应该使用该函数返回的值来决定是否对信号量进行发送或等待。这样做可能会导致竞态条件：另一个线程可能会调用 `sem_getvalue` 和调用另一个信号量函数之间改变信号量的值。请使用原子的发送和等待函数。

回到我们的任务队列示例，我们可以使用信号量来统计队列中等待的任务数量。`enqueue_job` 函数通过信号量来控制队列。

## 列表 4.12 (job-queue3.c) 由信号量控制的任务队列

```c
#include <malloc.h>

#include <pthread.h>

#include <semaphore.h>

struct job {

    /* 链表的链接字段。 */

    struct job* next;

    /* 描述待执行工作的其他字段... */

};

/* 待处理任务的链表。 */

struct job* job_queue;

/* 保护 job_queue 的互斥锁。 */

pthread_mutex_t job_queue_mutex = PTHREAD_MUTEX_INITIALIZER;
```

非零值将表示跨进程共享的信号量，但 GNU/Linux 不支持此类类型的信号量。

```c
/* 统计队列中任务数量的信号量。 */

sem_t job_queue_count;

/* 对任务队列进行一次初始化。 */

void initialize_job_queue () {

    /* 队列初始为空。 */

    job_queue = NULL;

    /* 初始化用于信号量计数任务的信号量。其

       初始值应为零。 */

    sem_init(&job_queue_count, 0, 0);

}

/* 处理队列中的任务直到队列为空。 */

void thread_function (void* arg) {

    while (1) {

        struct job* next_job;

        /* 等待任务队列信号量。如果其值为正，

           表示队列不空，则计数减 1。

           如果队列为空，则阻塞直到有新任务入队。 */

        sem_wait(&job_queue_count);

        /* 锁定任务队列上的互斥锁。 */

        pthread_mutex_lock(&job_queue_mutex);

        /* 因为有信号量，我们知道队列不空。获取

           下一个可用的任务。 */

        next_job = job_queue;

        /* 从列表中移除此任务。 */

        job_queue = job_queue->next;

        /* 释放任务队列上的互斥锁，因为我们暂时

           已经处理完队列了。 */

        pthread_mutex_unlock(&job_queue_mutex);

        /* 执行工作。 */

        process_job(next_job);

        /* 清理。 */

        free(next_job);

    }

    return NULL;

}

/* 将新任务插入任务队列的头部。 */

void enqueue_job (/* 在此处传递任务特定数据... */) {

    struct job* new_job;

    /* 分配一个新的任务对象。 */

    new_job = malloc(sizeof(struct job));

    /* 在此处设置任务结构的其他字段... */

    /* 在访问队列之前锁定队列上的互斥锁。 */

    pthread_mutex_lock(&job_queue_mutex);

    /* 将新任务放在队列队头。 */

    new_job->next = job_queue;

    job_queue = new_job;

    /* 向信号量发送信号，表示另一个任务可用。

       如果线程阻塞在信号量上，它们将被唤醒

       以处理该任务。 */

    sem_post(&job_queue_count);

    /* 释放队列互斥锁。 */

    pthread_mutex_unlock(&job_queue_mutex);

}
```

在从队列头部获取任务之前，每个线程将首先等待信号量。如果信号量的值为零（表示队列为空），线程将一直阻塞直到信号量的值变为正（表示已添加任务）。`enqueue_job` 函数将任务加入队列。与 `thread_function` 类似，它在修改队列之前需要锁定队列。在列表 4.12 所示的版本中，线程处理任务；如果没有可用任务，线程在 `sem_wait` 处阻塞。

## 4.4.6 条件变量

我们已经展示了如何使用互斥锁来防止多个线程并发访问变量，以及如何使用信号量来实现共享计数器。条件变量是 GNU/Linux 的一种同步设备；通过它，你可以实现更复杂的线程执行条件。

假设你写了一个执行循环的线程函数，在每次迭代中执行某些工作。然而，线程循环需要由一个标志控制；只有当标志设置时循环才运行；当标志未设置时，它暂停。列表 4.13 显示了如何通过循环中设置标志来实现。在循环的每次迭代中，线程函数检查标志是否设置。由于多个线程访问该标志，它受互斥锁保护。这种实现可能是正确的，但效率低下。当标志未设置时，线程函数每次都会锁定和解锁互斥锁，消耗大量 CPU。你真正想要的是在标志未设置时让线程睡眠，直到某些情况将标志设置为。

## 列表 4.13 (spin-cond.c) 简单的条件变量实现

```c
#include <pthread.h>

int thread_flag;

pthread_mutex_t thread_flag_mutex;

void initialize_init () {

    pthread_mutex_init(&thread_flag_mutex, NULL);

    thread_flag = 0;

}

/* 当标志设置时重复调用 do_work；否则旋转。 */

void* thread_function(void* thread_arg) {

    while (1) {

        int flag_is_set;

        /* 使用互斥锁保护标志。 */

        pthread_mutex_lock(&thread_flag_mutex);

        flag_is_set = thread_flag;

        pthread_mutex_unlock(&thread_flag_mutex);

        if (flag_is_set) {

            do_work();

        } /* 否则什么都不做。再次循环。 */

    }

    return NULL;

}

/* 将线程标志的值设置为 flag_value。 */

void set_thread_flag(int flag_value) {

    /* 使用互斥锁保护标志。 */

    pthread_mutex_lock(&thread_flag_mutex);

    thread_flag = flag_value;

    pthread_mutex_unlock(&thread_flag_mutex);

}
```

条件变量允许实现线程执行的条件，反之亦实现线程阻塞的条件。只要每个可能改变状态的线程都正确使用条件变量，Linux 就能保证在条件变化时阻塞的线程会被唤醒。

与信号量一样，线程可能会等待条件变量。如果线程 A 等待条件，它会被阻塞直到另一个线程 B 信号同一个条件变量。与信号量不同，条件变量没有计数器或内存；线程 A 必须在 B 信号它之前等待条件变量。如果线程 B 在 A 等待之前信号了条件变量，信号就会丢失，A 将阻塞直到另一个线程再次信号条件变量。

这就是你如何使用条件变量使上一个示例更高效的方法：

- `thread_function` 中的循环检查标志。如果标志未设置，线程等待条件变量。
- `set_thread_flag` 在更改标志值后信号条件变量。这意味着，如果 `thread_function` 阻塞在条件变量上，它将被唤醒并再次检查条件。

这种方法有一个问题：在检查标志值与信号或等待条件变量之间存在竞态条件。假设 `thread_function` 检查了标志并发现其未设置。在此时，Linux 调度器暂停并恢复了主线程。巧合的是，主线程处于 `set_thread_flag` 中。它设置了标志然后信号了条件变量。由于此时没有线程在等待条件变量（记住 `thread_function` 在调用条件变量之前被暂停了），信号丢失了。现在，当 Linux 重新调度另一个线程时，它开始等待条件变量并最终永久阻塞。

为了解决这个问题，我们需要用同一个互斥锁将标志和条件变量锁在一起。坦率地说，GNU/Linux 正好提供了这种机制。每个条件变量必须与互斥锁配合使用，以防止这种类的竞态条件。使用这种方案，线程遵循以下步骤：

1. `thread_function` 中的循环锁定互斥锁并读取标志值。
2. 如果标志已设置，解锁互斥锁并执行工作函数。
3. 如果标志未设置，它原子地解锁互斥锁并等待条件变量。

这里的关键特征在于步骤 3，在 GNU/Linux 中允许你原子地解锁互斥锁并等待条件变量，而没有其他线程干预的可能性。这消除了另一个线程在 `thread_function` 测试标志值和等待条件变量之间改变标志值并信号条件变量的可能性。

## 4.4 同步与临界区

条件变量由 `pthread_cond_t` 实例表示。记住，每个条件变量都应该有一个互斥锁（`mutex`）。这些是操作条件变量的函数：

- `pthread_cond_init` 初始化一个条件变量。第一个参数是指向 `pthread_cond_t` 实例的指针。第二个参数是指向条件变量属性对象的指针，在 GNU/Linux 下会被忽略。
  互斥锁必须按照第 4.4.2 节“互斥锁”中的描述单独初始化。
- `pthread_cond_signal` 信号一个条件变量。一个阻塞在条件变量上的单个线程将会被解锁。如果没有其他线程阻塞在该变量上，则信号将被忽略。参数是指向 `pthread_cond_t` 实例的指针。
- 类似的调用 `pthread_cond_broadcast` 会唤醒所有阻塞在条件变量上的线程，而不仅仅是一个线程。
- `pthread_cond_wait` 阻塞调用线程，直到条件变量被信号化。参数是指向 `pthread_cond_t` 实例的指针。第二个参数是指向 `pthread_mutex_t` 互斥锁实例的指针。
  当调用 `pthread_cond_wait` 时，调用线程必须已锁定互斥锁。该函数会原子地解锁互斥锁并阻塞在条件变量上。当条件变量被信号且调用线程解除阻塞时，`pthread_cond_wait` 会自动重新获取互斥锁的锁。

当你的程序执行可能改变你用条件变量所保护的条件含义的操作时，它应该执行这些步骤。（在我们的示例中，条件是线程标志的状态，因此每当标志发生变化时，必须采取这些步骤。）

1. 锁定与条件伴随的互斥锁。
2. 执行可能改变条件含义的操作（在我们的示例中，是标志）。
3. 根据所需的行为，信号化或广播条件变量。
4. 解锁与条件变量伴随的互斥锁。

列表 4.14 再次显示了之前的示例，现在使用条件变量来保护线程。注意，在 `thread_function` 中，在检查 `thread_flag` 的值之前持有了互斥锁的锁。该锁会在 `pthread_cond_wait` 阻塞之前自动释放，并在之后自动重新获取。同样注意 `set_thread_flag` 在设置 `thread_flag` 的值并信号化之前锁定了互斥锁。

### 列表 4.14 (condvar.c) 使用条件变量控制线程

```c
#include <pthread.h>

int thread_flag;

pthread_cond_t thread_flag_cv;

pthread_mutex_t thread_flag_mutex;

void initialize_flag() {

    /* 初始化互斥锁和条件变量。 */

    pthread_mutex_init(&thread_flag_mutex, NULL);

    pthread_cond_init(&thread_flag_cv, NULL);

    /* 初始化标志值。 */

    thread_flag = 0;

}

void *thread_function(void *arg) {

    /* 无限循环。 */

    while (1) {

        /* 在访问标志之前锁定互斥锁。 */
```



```c
pthread_mutex_lock(&thread_flag_mutex);

while (!thread_flag) {

    /* 标志为空。等待条件变量上的信号，

       指示标志已改变。当信号到达且

       线程解除阻塞时，循环并再次检查

       标志。 */

    pthread_cond_wait(&thread_flag_cv, &thread_flag_mutex);

}

/* 当我们到达这里时，知道标志一定已设置。解锁

   互斥锁。 */

pthread_mutex_unlock(&thread_flag_mutex);

/* 执行工作。 */

do_work();

return NULL;

}

void set_thread_flag(int flag_value) {

    /* 在访问标志之前锁定互斥锁。 */

    pthread_mutex_lock(&thread_flag_mutex);

    /* 设置标志值，然后发送信号，以防 thread_function

       阻塞在等待标志被设置的状态。 */

    thread_flag = flag_value;

    pthread_cond_signal(&thread_flag_cv);

    /* 解锁互斥锁。 */

    pthread_mutex_unlock(&thread_flag_mutex);

}
```

由条件变量保护的条件可以是任意复杂的。然而，在执行任何可能改变条件含义的操作之前，应该需要一个互斥锁，并在之后信号化条件变量。条件变量也可以在没有条件的情况下使用，仅作为阻塞线程直到另一个线程“唤醒”的机制。信号量也可以用于该目的。主要区别在于，如果没有线程阻塞在信号量上，信号量会“记住”唤醒调用，而条件变量除非确实有线程阻塞在上面，否则会丢弃唤醒调用。此外，信号量只交付一次唤醒；而 `pthread_cond_broadcast` 可能同时唤醒任意数量未知的阻塞线程。

### 4.4.7 两个或多个线程的死锁

当两个（或多个）线程被阻塞并等待一个只有另一个线程才能引起的条件时，就会发生死锁。例如，如果线程 A 阻塞在条件变量上等待线程 B 给它信号，而线程 B 阻塞在条件变量上等待线程 A 给它信号，那么就发生了死锁，因为两者都不会向对方发送信号。你应该小心避免这种情况发生的可能性，因为它们很难检测。

导致死锁的常见错误涉及一个多个线程尝试锁定同一组对象的问题。例如，考虑一个程序，其中不同的线程需要锁定互斥锁。假设不同的线程运行不同的函数需要锁定互斥锁。假设线程 A 锁了互斥锁 1 然后是互斥锁 2，而线程 B 恰好在锁定互斥锁 1 之前锁了互斥锁 2。在足够糟糕的调度下，Linux 可能调度线程 A 足够久来锁定 1，然后线程 B 锁定 2。现在没有线程可以进展，因为每个线程都在等待另一个线程持有的互斥锁。

这是一个更通用的死锁示例，不仅涉及互斥锁等同步对象，还涉及文件或设备等资源。问题发生在多个线程以不同的顺序锁定资源时。解决方案是确保所有线程以相同的顺序锁定资源。

## 4.5 GNU/Linux 线程实现

POSIX 线程在 GNU/Linux 实现与其他许多 Unix 类系统的不同在于：在 Linux 上，线程被实现为进程。每当你调用 `pthread_create` 创建新线程时，Linux 会创建一个运行该线程的新进程。然而，这个进程与使用 `fork()` 创建的进程不同；它与原始进程共享地址空间和资源，而不是接收副本。

列表 4.15 中的程序演示了这一点。该程序创建一个线程；原始线程和新线程都调用 `getpid` 函数并打印它们的进程 ID，然后无限循环。

### 列表 4.15 (thread-pid) 为线程打印进程 ID

```c
#include <pthread.h>

#include <stdio.h>

#include <unistd.h>

void thread_function(void *arg) {

    printf(stderr, "子线程 pid 为 %d\n", (int) getpid());

    /* 无限循环。 */

    while (1) {

        return NULL;

    }

}

int main () {

    pthread_t thread;

    printf(stderr, "主线程 pid 为 %d\n", (int) getpid());

    pthread_create(&thread, NULL, &thread_function, NULL);

    /* 无限循环。 */

    while (1) {

        return NULL;

    }

}
```

在后台运行该程序，然后调用 `ps` 显示正在运行的进程。忘记在之后杀死 `thread-pid` ——它在无所事的情况下消耗大量的 CPU。输出可能如下：

```
% cc thread-pid.c -o thread-pid -lpthread
./thread-pid & 14608
[1] 14608
main线程 pid 为 14608
子线程 pid 为 14610
ps x
PID TTY           STAT TIME COMMAND
14042 pts/9      S    0:00 bash
14608 pts/9      R    0:01 ./thread-pid

14609 pts/9 S 0:00 /thread-pid
14610 pts/9 R 0:01 /thread-pid
14611 pts/9 R 0:00 ps x
% kill 14608
[1]+ /thread-pid
```

### Shell 中的作业控制通知

以 [1] 开头的行是来自 shell 的输出。当你在后台运行一个程序时，shell 会为它分配一个作业号——在本例中为 1——并打印程序的 pid。如果后台作业终止，shell 会会在你下次调用命令时报告。

注意，有三个进程正在运行 `thread-pid`。其中第一个（PID 为 14608）是程序的主线程；第二个（PID 为 14610）是运行为了执行 `thread_function` 而创建的第三个线程。

那么 PID 为 14609 的第二个线程呢？它是“管理线程”，是 GNU/Linux 线程内部实现的一部分。当程序第一次调用 `pthread_create` 创建新线程时，就会创建该管理线程。

### 4.5.1 信号处理

假设一个多线程程序接收到一个信号。信号处理程序哪个线程中被调用？信号与线程之间交互的行为在不同的 UNIX 类系统之间有所不同。在 GNU/Linux 中，这种行为由线程实现为进程这一事实决定。

由于每个线程都是独立的进程，而且信号是传递给特定进程的，因此哪个线程接收信号并没有歧义。通常，从程序外部发送的信号会发送给与程序主线程对应的进程。例如，如果一个程序进行了 fork 且子进程执行了一个多线程程序，父进程将持有子进程主线程的 ID，并使用该 ID 向子进程发送信号。在向多线程程序发送信号时，这通常是一个遵循良好的约定。

注意，GNU/Linux 对 pthreads 的这种实现与 POSIX 线程标准不一致。在旨在具有移植性的程序中，不要依赖这种行为。

在多线程程序内部，一个线程可以专门向另一个线程发送信号。我们使用 `pthread_kill` 函数来实现这一点。它的第一个参数是线程 ID，第二个参数是信号号。

### 4.5.2 clone 系统调用

尽管在同一个程序中创建的 GNU/Linux 线程被实现为独立的进程，但它们共享虚拟内存空间和其他资源。然而，通过 fork 创建的子进程会获得这些项目的拷贝。前者是如何创建的？

Linux clone 系统调用是 fork 和 `pthread_create` 的通用形式，允许调用者指定调用进程与新创建进程之间共享哪些资源。此外，`clone` 要求你为新进程将使用的执行栈指定内存区域。虽然我们在这里为了满足读者的好奇心提到了 `clone`，但通常不在程序中使用系统调用。请使用 `fork` 创建新进程或使用 `pthread_create` 创建线程。

## 4.6 进程对比 线程

对于受益于并发的程序，决定使用进程还是线程可能是困难的。以下是一些指南，帮助你决定哪种并发模型最适合你的程序：

- 程序中的所有线程必须运行相同的可执行文件。相比之下，子进程可以通过调用 `exec` 函数运行不同的可执行文件。
- 出错的线程可能会损害同一进程中的其他线程，因为线程共享相同的虚拟内存空间和其他资源。例如，一个线程中通过未初始化的指针进行的内存写入可能会损坏另一个线程可见的内存。
- 另一方面，进程无法这样做，因为每个进程都有一个程序内存空间的副本本。
- 与创建新线程相比，为新进程拷贝内存会增加额外的性能开销。然而，拷贝仅在内存发生变化时才会执行，因此如果子进程只读取内存，这种代价是微乎其微的。
- 需要细粒度并行的程序应该使用线程。例如，如果问题可以分解为多个几乎相同的任务，线程可能是一个很好的选择。需要粗粒度并行的程序应该使用进程。
- 线程之间共享数据是非常轻易的，因为线程共享相同的内存。（但是，必须非常小心以避免竞态条件，如前所述。）进程之间的数据共享需要使用第 5 章中描述的 IPC 机制。这可能更繁琐，但它让多个进程遭受并发 bug 的概率较低。

## 5 进程间通信

第 3 章“进程”讨论了进程的创建，并展示了一个进程如何获取子进程的退出状态。这是两个进程之间通信最简单的形式，但绝不是最强大的。第 3 章的机制没有提供父进程与子进程通信的任何方法（通过命令行参数和环境变量与父环境通信外），也没有提供子进程与父进程通信的任何方法（通过子进程退出状态外）。这些机制中没有一种可以在子进程实际运行时与其通信的手段，而且这些机制也不允许与父子关系之外的进程进行通信。

本章描述了绕过这些局限性的进程间通信方法。我们将介绍父子之间、不相关进程之间、甚至不同机器之间通信的各种方法。

进程间通信 (IPC) 是进程之间的数据传输。例如，Web 浏览器可能向 Web 服务器请求 Web 页，然后服务器发送 HTML 数据。这种传输通常使用 sockets。另一个例子是，你可能想使用 `ls | lpr` 命令打印目录中的文件名。shell 会创建一个 `ls` 进程和一个独立的 `lpr` 进程，并用管道 $||$ 连接两者。管道允许相关进程之间的单向通信。`ls` 进程向管道写入数据，`lpr` 进程从管道读取数据。在本章中，我们讨论了五种 IPC：

- 共享内存进程通过简单读写指定位置进行通信。
- 映射内存与共享内存类似，但与文件中的文件关联。
- 管道允许从一个进程到相关进程的顺序通信。
- FIFO 与管道类似，但由于管道在文件系统中有一个名称，因此不相关的进程也可以进行通信。
- Sockets 支持不同计算机上不相关进程之间的通信。

这些 IPC 类型根据以下标准不同：

- 是否严格限制相关进程（具有共同祖先的进程）、共享相同文件系统的不相关进程，或连接到网络的任何计算机
- 通信进程是否仅限于写入数据或仅读取数据
- 允许通信的进程数量
- 通信进程是否由 IPC 进行同步——例如，读取进程在有可用数据读取之前停止

### 5.1 共享内存

进程间通信简单的方法之一是使用共享内存。共享内存允许或多个进程访问相同的内存，就像它们都调用了 `malloc()` 并返回指向实际内存的指针一样。当一个进程更改内存时，所有其他进程都能看到修改。

#### 5.1.1 快速本地通信

共享内存是最快的进程间通信形式，因为所有进程共享同一块内存。访问这种共享内存与访问进程非共享内存一样，并且不需要系统调用或进入内核。它还避免了不必要的数据拷贝。

由于内核不会对共享内存的访问进行同步，因此你必须提供自己的同步机制。例如，进程在数据写入内存之前不应从内存读取，且两个进程不能同时向同一内存位置写入数据。避免这些竞态条件的常用策略是使用信号量，这将在下一节中讨论。然而，我们的示例程序仅展示了单进程访问共享内存，以便关注共享内存机制，并避免在示例代码中充斥同步逻辑。

#### 5.1.2 内存模型

要使用共享内存，必须由一个进程分配该段。然后，每个想要访问该段的进程必须挂载该段。在完成对该段的使用后，每个进程都会卸载该段。在某个时刻，必须由一个进程释放该段。

理解 Linux 内存模型有助于解释分配和处理。在 Linux 下，每个进程的虚拟内存被分为页。每个进程维护一个从其地址到这些虚拟页的映射，这些页包含实际数据。尽管每个页都有自己的地址，但多个进程的映射可以指向同一个页，从而允许内存共享。内存页将在第 8 章“Linux 系统调用”中的第 8.8 节“页家族：锁定物理内存”中进一步讨论。

分配新的共享内存段会导致虚拟页的创建。由于所有进程都想要访问同一个共享段，因此应由一个进程分配新段。分配已有的段不会创建新页，但它会返回现有页的标识符。为了允许进程使用共享内存段，进程会将其挂载，这会添加从其虚拟内存到该段页的映射。当完成该段的使用后，这些映射条目将被移除。当不再有进程访问这些共享内存段时，必须恰好有一个进程释放虚拟页。

所有共享内存段都是按系统页大小的整数倍分配的，页大小是内存中一页的字节数。在 Linux 系统上，页大小为 4KB，但你应该通过调用 `getpagesize` 函数获取此值。

#### 5.1.3 分配

进程使用 `shmget("Shared Memory GET")` 分配共享内存段。它的第一个参数是一个整数键，用于指定要创建哪个段。互不相关的进程可以通过指定相同的键值来访问同一个共享段。遗憾的是，其他进程可能也选择了相同的固定键，这可能会导致冲突。使用特殊的 `IPC_PRIVATE` 作为键值可以保证创建一个全新的内存段。

它的第二个参数指定了段中的字节数。由于段是使用页分配的，实际分配的字节数会向上取整为页大小的整数倍。

第三个参数是位或（bitwise or）标志值，指定 `shmget` 的选项。标志值包括：

- `IPC_CREAT`—此标志表示应该创建一个新段。这会在指定键值的同时创建一个新段。
- `IPC_EXCL`—此标志始终与 `IPC_CREAT` 一起使用，如果段已经存在，则会导致 `shmget` 失败。因此，这可以确保调用进程拥有一个“独占”的段。如果没有给出此标志并使用了已存在段的键，`shmget` 将返回现有段而不是创建一个新段。
- 模式标志—此值由 9 位组成，表示授予所有者、组和其他的权限，用以控制对该段的访问。执行位被忽略。指定权限的一种简单方法是使用`<sys/stat.h>` 中定义的常量，这些常量在 `stat` 手页的第 2 节中有所记录。`S_IRUSR` 和 `S_IWUSR` 是共享内存段所有者的读写权限，`S_IROTH` 和 `S_IWOTH` 是其他人的读写权限。例如，此 `shmget` 调用创建了一个新的共享内存段（如果 `shm_key` 已使用，则访问现有段），该段对用户可读可写但对其他人不可。

```c
int shm_id = shmget(shm_key, getpagesize(), IPC_CREAT | S_IRUSR | S_IWUSR);
```

如果调用成功，`shmget` 返回一个段。如果共享内存段已存在，则会验证权限并检查该段未被标记为删除。

#### 5.1.4 挂载与卸载

为了让共享内存段可用，进程必须使用 `shmat("Shared Memory Attach")`。其传递由 `shmget` 返回的共享内存标识符。第二个参数是一个指针，指定了你想在进程地址空间的何处映射共享内存；如果你指定 `NULL`，Linux 将选择一个可用地址。第三个参数是标志，可以包括以下内容：

- `SHM_RND`—表示为第二个参数指定的地址应该向下取整为页大小的倍数。如果你没有指定此标志，必须手动对第二个参数进行页对齐。
- `SHM_RDONLY`—表示该段是只读的，不可写。这些位与文件使用的相同。它们在第 10.3 节“文件权限”中进行了描述。

如果调用成功，它返回挂载的共享段的地址。通过 `fork` 调用创建的子进程继承共享段；它们根据需要卸载共享内存。当你完成对共享内存的使用后，应使用 `shmd("Shared Memory Detach")` 卸载该段。传递由 `shmat` 返回的地址。如果段被释放且这是使用它的最后一个进程，它将被移除。调用 `exit` 和 `exec` 会自动卸载段。

#### 5.1.5 控制和释放共享内存

`shmctl("Shared Memory Control")` 调用返回关于共享内存段的信息并对其进行修改。第一个参数是共享内存标识符。要获取有关共享段的信息，将 `IPC_STAT` 作为第二个参数，并传递一个 `struct shmid_ds` 的指针。要移除段，将 `IPC_RMID` 作为第二个参数，并将 `NULL` 作为第三个参数。当最后一个挂载该段的进程卸载时，该段会被移除。

完成共享内存段的使用后，应显式使用 `shmctl` 释放它，以避免违反系统内存段总数的限制。调用 `exit` 和 `exec` 会卸载段但不会分配它们。请参考 `shmctl` 手页以获取可以在共享内存段上执行的其他操作的描述。

#### 5.1.6 示例程序

列表 5.1 中的程序说明了共享内存的使用。

列表 5.1 (shm.c) 共享内存

```c
#include <stdio.h>

#include <sys/shm.h>

#include <sys/stat.h>

int main () {

    int segment_id;

    char* shared_memory;

    struct shmid_ds shmbuffer;

    int segment_size;
```



`const int shared_segment_size = 0x6400;`

`/* 分配共享内存段。 */`

`segment_id = shmget(IPC_PRIVATE, shared_segment_size, IPC_CREAT | IPC_EXCL | S_IRUSR | S_IWUSR);`

列表 5.1 继续

```c
/* 挂载共享内存段。 */
shared_memory = (char*) shmat (segment_id, 0, 0);
printf("shared memory attached at address %p\n", shared_memory);
/* 确定段的大小。 */
shmctl(segment_id, IPC_STAT, &shmbuffer);
segment_size = shmbuffer.shm_seize;
printf("segment size: %d\n", segment_size);
/* 向共享内存写入字符串。 */
sprintf(shared_memory, "Hello, world.");
/* 卸载共享内存段。 */
shmd(shared_memory);
/* 在不同的地址重新挂载共享内存段。 */
shared_memory = (char*) shmat (segment_id, (void*) 0x5000000, 0);
printf("shared memory reattached at address %p\n", shared_memory);
/* 从共享内存中打印字符串。 */
printf("%s\n", shared_memory);
/* 卸载共享内存段。 */
shmd(shared_memory);
/* 释放共享内存段。 */
shmctl(segment_id, IPC_RMID, 0);
return 0;
}
```

### 5.1.7 调试

`ipc` 命令提供进程间通信设施的信息，包括共享段。使用 `-m` 标志获取有关共享内存的信息。例如，此代码说明编号为 1627649 的共享段正在使用中：

```
% ipcs -m
Shared Memory Segments
key shmid owner perms bytes nattch status
0x00000000 1627649 user 640 25600 0
```

如果此内存段被程序错误留下，可以使用 `ipcrm` 命令将其移除。

```
% ipcrm shm 1627649
```

## 5.2 进程信号量入门（101）

### 5.1.8 优点与缺点

共享内存分段允许任意数量的进程之间进行快速的双向通信。每个用户都可以进行读写操作；程序必须建立并遵循某些协议以防止竞态条件，例如在信息被读取之前对其进行覆盖。遗憾的是，即使你使用 `IPC_PRIVATE` 创建了新的共享段，Linux 也不保证提供独占访问。

此外，为了让多个进程使用同一个共享段，它们必须安排好使用相同的键值（key）。

## 5.2 进程信号量

如上一节所述，进程必须协调对共享内存的访问。正如我们在第 4 章第 4.4.5 节“线程的信号量”中所讨论的，信号量提供了信号信号的独特实现，可用于同步进程（称为进程信号量，有时称为 System V 信号量）。进程信号量的分配、使用和释放方式与共享内存段类似。虽然单个信号量就足够用于所有场景，但进程信号量是以集合形式存在的。在本节中，我们将介绍进程信号量的系统调用，并展示如何使用它们来实现单个二进制信号量。

### 5.2.1 分配与释放

`semget` 和 `semctl` 调用用于分配和释放信号量，这与共享内存的 `shmget` 和 `semctl` 类似。调用 `semget` 时，使用指定信号量集的键值、集合中的信号量数量以及权限标志，类似于 `shmget`；其值为信号量集标识符。你可以通过指定正确的键值来获取现有信号量集的标识符；在这种情况下，信号量的数量可以为零。

即使在所有使用信号量的进程终止后，信号量仍然存在。最后一个使用信号量的进程必须显式地删除它，以确保操作系统不会耗尽信号量。要这样做，调用 `semctl` 并传入信号量标识符、集合中的信号量数量、`IPC_RMID` 作为第三参数，并将任何 `union semun` 作为第四参数（该参数会被忽略）。调用进程的有效用户 ID 必须与信号量分配者匹配（或调用者必须是 root）。与共享内存段不同，删除信号量集会导致 Linux 立即释放。

列表 5.2 展示了分配和释放二进制信号量的函数。

#### 列表 5.2 (sem_all_dealloc.c) 分配与释放二进制信号量

```c
#include <sys/ipc.h>
#include <sys/sem.h>
#include <sys/types.h>

/* 我们必须自己定义联合体 semun。 */
union semun {
    int val;
    struct semid_ds *buf;
    unsigned short int *array;
    struct seminfo *buf;
};

/* 获取二进制信号量的 ID，必要时进行分配。 */
int binary_semaphore_allocation(key_t key, int sem_flags)
{
    return semget(key, 1, sem_flags);
}

/* 释放二进制信号量。所有用户必须已完成使用。失败返回 -1。 */
int binary_semaphore_deallocate(int semid)
{
    union semun ignored_argument;
    return semctl(semid, 1, IPC_RMID, ignored_argument);
}
```

### 5.2.2 初始化信号量

分配和初始化信号量是两个独立的操作。要初始化信号量，使用 `semctl` 并将第二个参数设置为零，第三个参数设置为 `SETALL`。对于第四参数，你必须创建一个 `union semun` 对象并让其数组字段指向无符号短值数组。每个值都用于初始化集合中的一个信号量。

列表 5.3 展示了一个初始化二进制信号量的函数。

#### 列表 5.3 (sem_init.c) 初始化二进制信号量

```c
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/sem.h>

/* 我们必须自己定义联合体 semun。 */
union semun {
    int val;
    struct semid_ds *buf;
    unsigned short int *array;
    struct seminfo *buf;
};

/* 初始化一个值为 1 的二进制信号量。 */
int binary_semaphore_initialize(int semid)
{
    union semun argument;
    unsigned short values[1];
    values[0] = 1;
    argument.array = values;
    return semctl(semid, 0, SETALL, argument);
}
```

### 5.2.3 等待（Wait）与发布（Post）操作

每个 `semop` 都有一个非负值并支持等待和发布操作。`semop` 系统调用实现了这两种操作。第一个参数指定信号量集标识符。第二个参数是 `struct sembuf` 元素数组，指定了你想执行的操作。第三个参数是该数组的长度。`struct sembuf` 的字段列举如下：

- `sem_num` 是执行操作的信号量集中的信号量编号。
- `sem_op` 是一个指定信号量操作的整数。如果 `sem_op` 是正数，则该数会立即加到信号量值。
- 如果 `sem_op` 是负数，则从信号量值中减去该数的绝对值。如果会导致信号量值变为负数，则调用将阻塞。
- `sem_fl` 是一个指定额外选项的标志（例如 `IPC_AIT`、`SEM_UNDO`、`SEM_NOWAIT`）。

（注：原文此处存在大量重复的段落，已按要求保留核心逻辑翻译并去除了冗余）

MAP_SHARED—写入将立即反映在底层文件中，而不是对写入进行缓冲。在 IPC（进程间通信）中使用映射内存时使用此模式。此模式可能与 `MAP_PRIVATE` 配合使用。

如果调用成功，它返回一个指向内存起始位置的指针。如果失败，返回 `MAP_FAILED`。

当你完成内存映射后，使用 `munmap` 释放它。向它传递映射内存区域的起始地址和长度。Linux 会在进程终止时自动取消区域的映射。

### 5.3.2 示例程序

让我们来看两个程序，说明如何使用内存映射区域来读写文件。第一个程序（列表 5.5）生成一个随机数并将其写入内存映射的文件。第二个程序（列表 5.6）读取该数，打印出来，并将内存映射文件中的值替换为其两倍。两个程序都接受一个作为要映射文件的命令行参数。

### 列表 5.5 (mmap-write.c) 向内存映射的文件写入随机数

```c
#include <stdlib.h>
#include <stdio.h>
#include <fcntl.h>
#include <sys/mman.h>
#include <sys/stat.h>
#include <time.h>
#include <unistd.h>

#define FILE_LENGTH 100

/* 返回 [low,high] 范围内的均匀随机数。 */
int random_range(unsigned const low, unsigned const high) {
    unsigned const range = high - low + 1;
    return low + (int)((double) range) * rand() / (RAND_MAX + 1.0);
}

int main(int argc, char * argv[]) {
    int fd;
    void* file_memory;

    /* 设置随机数生成器的种子。 */
    srand(time(NULL));

    /* 准备一个足够容纳无符号整数的大文件。 */
    fd = open(argv[1], O_RDWR | O_CREAT, S_IRUSR | S_IWUSR);
    lseek(fd, FILE_LENGTH+1, SEEK_SET);
    write(fd, " ", 1);
    lseek(fd, 0, SEEK_SET);

    /* 创建内存映射。 */
    file_memory = mmap(0, FILE_LENGTH, PROT_WRITE, MAP_SHARED, fd, 0);
    close(fd);

    /* 将随机整数写入内存映射区域。 */
    printf((char*)file_memory, "%d", random_range(-100, 100));

    /* 释放内存（不需要，因为程序会退出）。 */
    munmap(file_memory, FILE_LENGTH);
}
```

`mmap-write` 程序打开文件，如果文件之前不存在则创建它。`open` 的第三个参数指定以读写模式打开文件。由于我们不知道文件的长度，我们使用 `lseek` 来确保文件足够大以存储一个整数，然后将文件位置移动到开头。程序映射文件并关闭文件描述符，因为不再需要它了。程序将随机整数写入映射的内存，然后写入文件，并取消内存映射。`munmap` 调用是不必要的，因为 Linux 在程序终止时会自动取消文件的映射。

### 列表 5.6 (mmap-read.c) 从内存映射的文件读取整数并将其翻倍

```c
#include <stdlib.h>
#include <stdio.h>
#include <fcntl.h>
#include <sys/mman.h>
#include <sys/stat.h>
#include <unistd.h>

#define FILE_LENGTH 0x100

int main(int argc, char* const argv[])
{
    int fd;
    void *file_memory;
    int integer;

    /* 打开文件。 */
    fd = open(argv[1], O_RDWR, S_IRUSR | S_IWUSR);

    /* 创建内存映射。 */
    file_memory = mmap(0, FILE_LENGTH, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    close(fd);

    /* 读取整数，打印它，并进行处理。 */
    sscanf(file_memory, "%d\n", &integer);
    printf("value: %d\n", integer);
    sprintf((char*)file_memory, "%d\n", 2 * integer);

    /* 释放内存（不需要，因为程序会退出）。 */
    munmap(file_memory, FILE_LENGTH);
    return 0;
}
```

`mmap-read` 程序从文件中读取数字并将翻倍后的值写入文件。首先，它可以假设文件足够大可以存储一个无符号整数，我们不需要像上一个程序那样使用 `seek`。程序使用 `sscanf` 从内存中读取并解析值，然后使用 `sprintf` 格式化并写入翻倍的值。以下是运行这些示例的例子。它映射了文件 `/tmp/integer-file`。

- `$ mmap-write /tmp/integer-file`
- `cat /tmp/integer-file`
  42
- `$ mmap-read /tmp/integer-file`
  value: 42
- `cat /tmp/integer-file`
  84

观察测试可以发现 42 在没有调用 `write` 的情况下被写入磁盘，并且在没有调用 `read` 的情况下被读回。请注意，这些示例程序仅为了演示目的使用 `printf` 和 `sscanf` 将整数作为字符串进行读写——实际上你可以在内存映射文件中存储和检索任意二进制数据。

### 5.3.3 文件的共享访问

不同的进程可以使用与同一文件相关的内存映射区域进行通信。指定 `MAP_SHARED` 标志，以便对这些区域的任何写入都会立即传输到底层文件并对其他进程可见。如果你不指定此标志，Linux 可能会在将其传输到磁盘之前进行缓冲。或者，你可以通过调用 `msync` 强制 Linux 整合写入。它的第一个参数指定了这些值：

- `MS_ASYNC`：更新已调度，但不一定在调用返回之前执行。
- `MS_SYNC`：更新是即时的；调用将阻塞直到完成。
- `MS_INVALIDATE`：所有其他映射都将失效。

例如，要刷新映射在地址 `mem_addr` 长度为 `mem_length` 的共享文件，调用此代码：

```c
msync(mem_addr, mem_length, MS_SYNC | MS_INVALIDATE);
```

对于共享内存段，内存映射区域的用户必须建立一种协议以避免竞态条件。例如，可以使用信号量来防止多个进程同时访问映射的内存。或者，可以使用 `fcntl` 在第 8 章描述的锁机制。

### 5.3.4 私有映射

指定 `MAP_PRIVATE` 创建一个私有拷贝。对该区域的任何写入都不会反映在底层文件中，而是被缓冲在内存中。当进程终止时，缓冲区会被丢弃。

### 5.3.5 mmap 的其他用途

`mmap` 调用可以用于除文件映射以外的用途。一种常见的用法是用于进程间通信。例如，在第 6 章 2.2 节描述的，可以使用 `mmap` 映射匿名内存。`mmap` 还可以用于映射共享库。此外，`mmap` 还可以用于通过 `mmap` 映射（在第 6 章“设备”中描述，`mmap` 映射到内存。

## 5.4 管道

管道是一种允许单向通信的设备。写入管道“写入端”的数据可以从“读端”读回。管道是串行设备；数据总是按照写入顺序读取。串行情况下，管道用于单个进程内的线程之间，或用于父进程和子进程之间。

在 shell 中，符号 `|` 创建一个管道。例如，这个 shell 命令导致 shell 产生两个子进程：

- `ls | less`

shell 同时也创建一个管道，连接 `ls` 的标准输出与 `less` 的标准输入。`ls` 列出的文件名发送到 `less` 的顺序就像直接发送到终端一样。

管道的数据容量是有限的。如果写入进程写入的速度于读取进程消耗数据的速度，且管道无法存储更多数据，写入进程将阻塞直到有更多可用空间。如果读者尝试读取但没有可用数据，它将阻塞直到数据可用。因此，管道会自动同步这两个进程。

### 5.4.1 创建管道

要创建管道，调用 `pipe` 命令。提供一个大小为 2 的整数数组。`pipe` 调用将读取描述符存储在数组位置 0，将写入描述符存储在位置 1。例如，考虑以下代码：

```c
int pipe_fds[2];
int read_fd;
int write_fd;
pipe(pipe_fds);
read_fd = pipe_fds[0];
write_fd = pipe_fds[1];
```



写入描述符 `read_fd` 的数据可以从 `write_fd` 读回。

### 5.4.2 父进程与子进程间的通信

调用 `pipe` 创建文件描述符，这些描述符仅在该进程及其子进程中有效。然而，当进程调用 `fork` 时，文件描述符会被拷贝到新的子进程。因此，管道只能连接相关的进程。

在列表 5.7 程序中，`fork` 产生了一个子进程。子进程继承了管道文件描述符。父进程向管道写入字符串，子进程将其读取。示例程序使用 `fdopen` 将这些文件描述符转换为 `FILE` 流。由于我们使用的是流而不是文件描述符，可以使用高级别的 C 库 I/O 函数，如 `printf` 和 `fgets`。

## 5.4 管道 (Pipes)

列表 5.7 (pipe.c) 使用管道与子进程通信

```c
#include <stdlib.h>

#include <stdio.h>

#include <unistd.h>

/* 向 STREAM 写入 COUNT 份 MESSAGE，每个之间暂停一秒。 */

void writer(const char* message, int count, FILE* stream)
{
    for (; count > 0; --count) {
        /* 将消息写入流中，并立即发送。 */
        fprintf(stream, "%s", message);
        fflush(stream);

        /* 休息一会儿。 */
        sleep(1);
    }
}

/* 尽可能地从流中读取随机字符串。 */

void reader(FILE* stream)
{
    char buffer[1024];
    /* 读取到流结束为止，
    无论是换行符还是文件结束。 */
    while (!feof(stream)
        && !ferror(stream)
        && fgets(buffer, sizeof(buffer), stream) != NULL)
        fputs(buffer, stdout);
}

int main()
{
    int fds[2];
    pid_t pid;
    /* 创建管道。管道两端的文件描述符
    放在 fds 数组中。 */
    pipe(fds);

    /* 派生子进程。 */
    pid = fork();
    if (pid == (pid_t)0) {
        FILE* stream;
        /* 这是子进程。关闭我们对文件描述符写端的副本。 */
        close(fds[1]);

        /* 将读取端描述符转换为 FILE 对象，并从中进行读取。 */
        stream = fdopen(fds[0], "r");
        reader(stream);
    }
}
```

列表 5.7 续

在 `main()` 函数开始处，`fds` 被声明为大小为 2 的整数数组。`pipe` 调用创建了一个管道，并将读、写文件描述符放入该数组中。程序随后派生出一个进程。在关闭管道的读端后，父进程开始向管道写入。在关闭管道的写端后，子进程从管道中读取字符串。

注意，在 `writer` 函数中写入后，父进程通过调用 `fflush(...)` 刷新管道。否则，字符串可能不会立即通过管道发送。

当你调用命令 `ls | less` 时，会发生两次 `fork`：一次是为了创建 `ls` 子进程，另一次是为了创建 `less` 子进程。这两个进程都继承了管道描述符，因此它们可以使用管道进行通信。若要让不相关的进程之间进行通信，请使用 FIFO 代替，如第 5.4.5 节“FIFOs”中所讨论的那样。

### 5.4.3 重定向标准输入、输出和错误流

通常，你可能想要创建一个子进程，并将管道之一设置为其标准输入或标准输出。使用 `dup2` 调用，你可以将一个文件描述符等同于另一个。例如，要将进程的标准输入重定向到文件描述符 `fd`，请使用此行：

```c
dup2(fd, STDIN_FILENO);
```

符号常量 `STDIN_FILENO` 代表标准输入的文件描述符，其值为 0。该调用会关闭标准输入并将其重新打开，作为 `fd` 的副本，以便二者可以互换。等同的文件描述符共享相同的文件位置和同一组文件状态标志位。因此，从 `fd` 读取的字符不会再次从标准输入中读取。

列表 5.8 中的程序使用 `dup2` 将管道的输出发送到 `sort` 命令。在创建管道后，管道进行了派生（`fork`）。父进程向管道打印字符串。子进程使用 `dup2` 将管道的文件描述符附加到它的标准输入上。它执行 `sort` 程序。

## 列表 5.8 (dup2.c) 使用 dup2 从管道重定向输出

```c
#include <stdio.h>

#include <sys/types.h>

#include <sys/wait.h>

#include <unistd.h>

int main()
{
    int fds[2];
    pid_t pid;

    /* 创建管道。管道两端的文件描述符存放在 fds 中。 */
    pipe(fds);

    /* 派生子进程。 */
    pid = fork();

    if (pid == (pid_t)0) {
        /* 这是子进程。关闭我们对文件描述符写端的副本。 */
        close(fds[1]);

        /* 将管道的读端连接到标准输入。 */
        dup2(fds[0], STDIN_FILENO);

        /* 用 "sort" 程序替换子进程。 */
        execl("sort", "sort", NULL);
    } else {
        /* 这是父进程。 */
        FILE *stream;

        /* 关闭我们对文件描述符读端的副本。 */
        close(fds[0]);

        /* 将文件写入描述符转换为 FILE 对象并进行写入。 */
        stream = fdopen(fds[1], "w");

        fprintf(stream, "This is a test.\n");
        fprintf(stream, "Hello, world.\n");
        fprintf(stream, "My dog has fleas.\n");
        fprintf(stream, "One fish, two fish.\n");

        fflush(stream);

        close(fds[1]);

        /* 等待子进程完成。 */
        waitpid(pid, NULL, 0);
    }

    return 0;
}
```

### 5.4.5 FIFOs

先入先出（FIFO）文件是文件系统中的管道。管道的两个端不需要是相关的。FIFOs 也称为命名管道。你可以使用 `mkfifo` 命令创建 FIFO。例如，在命令行中创建 FIFO：

```bash
$ mkfifo /tmp/fifo
```

`ls` 输出的第一个字符 `p` 表示该文件是一个管道。在一个窗口中，通过以下命令读取 FIFO：

```bash
$ cat < /tmp/fifo
```

通过编程使用 `mkfifo` 函数创建 FIFO。第一个参数是创建 FIFO 的路径；第二个参数指定管道的所有者、组和世界权限。由于管道必须有一个读取者和一个写入者，权限必须包含读和写。如果无法创建管道（例如，文件名已存在），`mkfifo` 返回 -1。如果你调用了 `mkfifo`，需要包含 `<sys/types.h>` 和 `<sys/stat.h>`。

访问 FIFO 就像访问普通文件一样。为了通过 FIFO 进行通信，一个程序必须打开它写入，另一个程序必须打开它读取。可以使用低级 I/O 函数（`open`, `write`, `read`, `close` 等，见附录 B，“低级 I/O”）或 C I/O 函数（`fopen`, `fprintf`, `fscanf`, `fclose` 等）。

# 116 第 5 章 进程间通信

FIFO 可以有多个读取者或多个写入者。来自每个写入者的字节是原子写入的，最大长度为 `PIPE_BUF`（Linux 上为 4KB）。来自同时写入者的数据块可能会发生交错。同时读取也遵循类似的规则。

## 与 Windows 命名管道的区别

Win32 操作系统中的管道与 Linux 管道非常相似（有关这些的技术细节请参阅 Win32 库文档）。主要区别在于命名管道，在 Win32 中，它们的功能更像套字（sockets）。Win32 管道可以连接通过网络连接到不同计算机上的进程。在 Linux 上，此目的是套字。此外，Win32 允许在命名管道上建立多个读写连接而产生数据交错，且管道可以用于双向通信。

## 5.5 套字

套字是一种双向通信设备，可以用于与同一机器上的另一个进程通信，也可以与运行在其他机器上的进程通信。在本章中讨论的唯一允许不同计算机间进程通信的方法就是套字。Telnet、HTTP、FTP 和万维网等互联网程序都使用了套字。

例如，你可以使用 Telnet 程序从 Web 服务器获取 WWW 页面，因为它们都使用套字进行网络通信。要打开到位于 `www.codesource.com` 的 WWW 服务器的连接，请使用 `telnet www.codesource.com 80`。魔术常量 80 指定连接到运行在 `www.codesource.com` 的 Web 服务器，而不是其他进程。在建立连接后尝试 `GET /`。这通过套字向 Web 服务器发送消息，服务器将通过发送主页的 HTML 源代码进行回复，然后关闭连接——例如：

```
% telnet www.codesource.com 80
Trying 206.168.99.1...
Connected to merlin.codesource.com (206.168.99.1).
Escape character is '~'.
GET /
<<html>
<head>
<meta http-equiv="Content-Type" content="text/html;charset=iso-8859-1">
n...
```

- 注意，只有 Windows NT 可以创建命名管道；Windows 9x 程序只能建立客户端连接。
- 通常，你会使用 `telnet` 连接 Telnet 服务器进行远程登录。但你也可以使用 `telnet` 连接到不同类型的服务器，然后直接对其输入注释。

## 5.5.1 套字概念

创建套字时，必须指定三个参数：通信样式、命名空间和协议。

通信样式控制套字如何处理传输的数据，并规定了通信伙伴的数量。当数据通过套字发送时，它会被封装成数据包。通信样式决定了如何处理数据包以及如何从发送者到接收者进行寻址。

- 连接样式（Connection styles）保证按照发送顺序交付所有数据包。如果由于网络问题导致数据包丢失或重序，接收者会自动请求发送者重传。
- 连接样式的套字就像电话通话：在建立连接时，发送者和接收者的地址在通信开始时就固定了。
- 数据报样式（Datagram style）不保证交付或到达顺序。由于网络错误或其他状况，数据包在传输过程中可能会丢失或重序。每个数据包都必须标记其身份标识，并保证以“尽力而为”（best effort）的方式交付，因此数据包可能会消失，或者到达顺序与发送顺序不同。
- 数据报样式的套字更像邮信。发送者为每条单独的消息指定接收者的地址。

套字命名空间（socket namespace）规定了套字地址的写法。套字地址识别一个套字连接。例如，“本地命名空间”中的套字地址是普通文件名。在“互联网命名空间”中，套字地址是连接到网络的主机的套字地址（称为互联网协议地址或 IP 地址）和一个端口号。端口号用于区分同一主机上的多个套字。

常用的协议包括 TCP/IP、Unix 协议。

### 5.5.2 系统调用

以下是比之前更灵活的套字操作：

- 创建套字（`socket`）：创建套字
- 关闭（`close`）：销毁套字
- 连接（`connect`）：建立连接
- 绑定（`bind`）：将地址绑定到套字
- 监听（`listen`）：配置等待的连接
- 接收（`accept`）：接受连接

创建和销毁套字

创建套字时，必须指定三个参数。

创建套字（`socket`）时，需要指定通信样式、命名空间和协议。

通信样式控制套字如何处理传输的数据，并规定了通信伙伴的数量。当数据通过套字发送时，它会被封装成数据包。通信样式决定了如何处理数据包以及如何从发送者到接收者进行寻址。

- 连接样式保证按照发送顺序交付所有数据包。如果由于网络问题导致数据包丢失或重序，接收者会自动请求发送者重传。
- 连接样式的套字就像电话通话：在建立连接时，发送者和接收者的地址在通信开始时就固定了。
- 数据报样式不保证交付或到达顺序。由于网络错误或其他状况，数据包在传输过程中可能会丢失或重序。每个数据包都必须标记其身份标识，并保证以“尽力而为”的方式交付，因此数据包可能会消失，或者到达顺序与发送顺序不同。
- 数据报样式的套字更像邮信。发送者为每条单独的消息指定接收者的地址。

套字命名空间规定了套字地址的写入方式。套字地址识别一个套字连接。例如，“本地命名空间”中的套字地址是普通文件名。在“互联网命名空间”中，套字地址是连接到网络的主机的套字地址（称为互联网协议地址或 IP 地址）和一个端口号。端口号用于区分同一主机上的多个套字。

常用的协议包括 TCP/IP、Unix 协议。

### 5.5.3 服务器

套字的生命周期包括创建套字、绑定地址、监听、接受连接，然后关闭套字。

在绑定地址到套字时，其第一个参数是文件描述符。第二个参数是套字结构的指针；第三个参数是地址的长度（字节）。

在监听时，它规定了可以队列的连接数量。如果队列满了，额外的连接将被拒绝。这并不限制服务器可以处理的连接总数，而是限制了尚未接受的尝试连接的数量。

服务器通过 `accept` 接受客户端请求。第一个参数指向套字结构，其中填充了客户端地址。第三个参数是地址结构的长度（字节）。服务器可以使用客户端地址来判断是否要与客户端通信。`accept` 创建一个新的套字并返回相应的文件描述符。服务器继续接受新连接。要从套字中读取数据但不将其移除队列，可以使用 `recv`。它具有与 `read` 相同的参数，多了一个 `FLAGS` 参数。`MSG_PEEK` 标志允许读取数据但不从队列中移除。

## 5.5.4 本地套字

在同一计算机上连接的套字可以使用由 `PF_LOCAL` 和 `PF_UNIX` 表示的本地命名空间。这些被称为本地套字或 UNIX 套字。套字地址通过文件名指定，仅在创建连接时使用。

套字的名字指定在 `sockaddr_un` 中。你必须将 `sun_family` 字段设置为 `AF_LOCAL`，表示这是一个本地命名空间。`sun_path` 字段指定文件名，长度可能为 108 字节。`struct sockaddr_un` 的实际长度应使用 `SUN_LEN` 宏来计算。任何文件名都可以使用，但进程必须具有目录写权限，这允许向目录添加文件。要连接到套字，进程必须对该文件具有读取权限。由于存在于文件系统中，本地套字被列为一个文件。例如，注意初始的：

```
% ls -l /tmp/socket
srwwx-- -1 user group @ Nov 13 19:18 /tmp/socket
```



在使用本地套字后，调用 `unlink` 将其删除。

## 5.5.5 使用命名空间套接字（Namespace Sockets）示例

我们通过两个程序来演示套接字。列表 5.10 中的服务器程序创建了一个本地命名空间套接字并在上面监听连接。当它接收到连接时，会从连接中读取文本消息并打印它们，直到连接关闭。如果其中一条消息是“quit”，服务器程序将移除套接字并结束。该服务器程序将套接字的路径作为命令行参数。

### 列表 5.10 (`socket-server.c`) 本地命名空间套接字服务器

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/un.h>
#include <unistd.h>

/* 从套接字读取文本并打印。持续直到
socket关闭。如果客户端发送了 'quit'
消息，返回非零，否则返回零。 */

int server(int client_socket) {
    while (1) {
        int length;
        char *text;

        /* 首先，从套接字读取文本消息的长度。如果
        read返回零，客户端关闭了连接。 */
        if (read(client_socket, &length, sizeof(length)) == 0)
            return 0;

        /* 分配一个缓冲区存储文本。 */
        text = (char *)malloc(length);

        /* 读取文本本身并打印它。 */
        read(client_socket, text, length);
        printf("%s\n", text);

        /* 释放缓冲区。 */
        free(text);

        /* 如果客户端发送了消息 'quit'，我们就完工了。 */
        if (strcmp(text, "quit") == 0)
            return 1;
    }
}

int main (int argc, char *argv[]) {
    const char *const socket_name = argv[1];
    int socket_fd;
    struct sockaddr_un name;
    int client_sent_quit_message;

    /* 创建套接字。 */
    socket_fd = socket(PF_LOCAL, SOCK_STREAM, 0);

    /* 表明这是一个服务器。 */
    name.sun_family = AF_LOCAL;
    strcpy(name.sun_path, socket_name);
    bind(socket_fd, &name, SUN_LEN(&name));

    /* 监听连接。 */
    listen(socket_fd, 5);

    /* 重复接受连接，为每个客户端启动一个 server(1)
    进行处理。持续直到客户端发送 'quit' 消息。 */
    do {
        struct sockaddr_un client_name;
        socklen_t client_name_len;
        int client_socket_fd;

        /* 接受连接。 */
        client_socket_fd = accept(socket_fd, &client_name, &client_name_len);

        /* 处理连接。 */
        client_sent_quit_message = server(client_socket_fd);

        /* 关闭我们这一端的连接。 */
        close(client_socket_fd);
    } while (client_sent_quit_message);

    /* 移除套接字文件。 */
    close(socket_fd);
    unlink(socket_name);

    return 0;
}
```

列表 5.11 中的客户端程序连接到本地命名空间套接字并发送消息。套接字的名称路径和消息均在命令行上指定。

### 列表 5.11 (`socket-client.c`) 本地命名空间套接字客户端

```c
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/un.h>
#include <unistd.h>

/* 向文件描述符 SOCKET_FD 提供的套接字写入 TEXT。 */

void write_text(int socket_fd, const char* text)
{
    /* 写入字符串的字节数，包括
       NUL 终止符。 */
    int length = strlen(text) + 1;

    write(socket_fd, &length, sizeof(length));

    /* 写入字符串。 */
    write(socket_fd, text, length);
}

int main (int argc, char* argv[])
{
    const char* socket_name = argv[1];
    const char* message = argv[2];
    int socket_fd;
    struct sockaddr_un name;

    /* 创建套接字。 */
    socket_fd = socket(PF_LOCAL, SOCK_STREAM, 0);

    /* 将族名存储在套接字地址中。 */
    name.sun_family = AF_LOCAL;
    strncpy(name.sun_path, socket_name);

    /* 连接到套接字。 */
    connect(socket_fd, &name, SUN_LEN(name));

    /* 将命令行上的文本写入套接字。 */
    write_text(socket_fd, message);

    close(socket_fd);

    return 0;
}
```

在客户端发送消息文本之前，它会通过整数变量 `length` 的字节发送该文本的长度。同样，服务器通过从套接字读取到一个整数变量来读取文本的长度。这允许服务器在从套接字读取文本之前，分配一个适当大小的缓冲区来存储消息文本。

要尝试这个示例，请在一个窗口中启动服务器程序。指定一个套接字路径——例如 `/tmp/socket`。

- `./socket-server /tmp/socket`

在另一个窗口中，运行客户端几次，指定相同的套接字路径并发送：

- `./socket-client /tmp/socket "Hello, world."`

服务器接收并打印这些消息。要关闭服务器，发送消息：

```bash
./socket-client /tmp/socket "quit"
```

服务器程序终止。

## 5.5.6 互联网域套接字（Internet-Domain Sockets）

UNIX 命名空间套接字只能用于同一台计算机上进程间的通信。相反，互联网域套接字可以用于连接不同机器的进程。通过网络套接字使用 `AF_INET` 用于 IPv4 或 `AF_INET6` 用于 IPv6 地址。最常用的 IPv4 结构是 `sockaddr_in`，它包含了 IP 地址和端口号。

### 列表 5.12 (`inet.c`) 读取 WWW 服务器

```c
#include <stdlib.h>
#include <stdio.h>
#include <netinet/in.h>
#include <netdb.h>
#include <sys/socket.h>
#include <unistd.h>
#include <string.h>

/* 输出服务器的主页内容。 */

void get_home_page (int socket_fd) {
    char buffer[10000];
    size_t number_characters_read;

    /* 从套接字读取。read 调用可能一次性返回所有数据，因此持续读取直到耗尽。 */
    while (1) {
        number_characters_read = read(socket_fd, buffer, 10000);

        if (number_characters_read <= 0)
            return;

        /* 将数据写入标准输出。 */
        fwrite(buffer, sizeof(char), number_characters_read, stdout);
    }
}

int main (int argc, char* const argv[]) {
    int socket_fd;
    struct sockaddr_in name;
    struct hostent *hostinfo;

    if (argc != 2) {
        fprintf(stderr, "Usage: %s <hostname>\n", argv[0]);
        return 1;
    }

    /* 创建套接字。 */
    socket_fd = socket(AF_INET, SOCK_STREAM, 0);

    /* 将服务器的名称存储在套接字地址中。 */
    name.sin_family = AF_INET;

    /* 将字符串转换为数字。 */
    hostinfo = gethostbyname(argv[1]);

    if (hostinfo == NULL) {
        fprintf(stderr, "Error resolving hostname\n");
        return 1;
    } else
    name.sin_addr = *((struct in_addr *)hostinfo->h_addr);

    /* Web 服务器使用 80 端口。 */
    name.sin_port = htons(80);

    /* 连接到服务器。 */
    if (connect(socket_fd, (struct sockaddr *)&name, sizeof(name)) < 0) {
        perror("connect error");
        return 1;
    }

    get_home_page(socket_fd);
    close(socket_fd);

    return 0;
}
```

## 5.5 套接字

```c
/* 连接到 Web 服务器 */
if (connect(socket_fd, &name, sizeof(struct sockaddr_in)) == -1) {
    perror('connect');
    return 1;
}
/* 获取服务器的首页。 */
get_home_page(socket_fd);
return 0;
}
```

该程序从命令行获取 Web 服务器的主机名（不是 URL —— 也就是说，不包含 `http://`）。它调用 `gethostbyname` 将主机名转换为数值 IP 地址，然后将一个流式（TCP）套接字连接到该主机的 80 端口。Web 服务器使用超文本传输协议 (HTTP)，因此程序发出 HTTP GET 命令，服务器通过发送首页文本进行响应。

## 标准端口号

按照惯例，Web 服务器在 80 端口上监听连接。大多数互联网网络服务都与一个标准端口号相关联。例如，使用 SSL 在 443 端口连接的安全性 Web 服务器，以及使用 SMTP 协议的邮件服务器使用 25 端口。

在 GNU/Linux 系统上，协议/服务名称与标准端口号之间的关联列在 `/etc/services` 文件中。第一列是协议或服务名称。第二列列出端口号和连接类型：`tcp` 表示面向连接，`udp` 表示数据报。

如果你使用互联网域套接字（Internet-domain sockets）实现自定义网络服务，请使用大于 1024 的端口号。

例如，要从 `www.codesourcey.com` 网站检索首页，请调用：

```bash
% /socket-inet www.codesourcey.com

<html>
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1">
..
```



## 5.5.7 套接字对

正如我们之前看到的，`pipe` 函数为管道的开头和结尾创建两个文件描述符。管道之所以链接在一起，是因为文件描述符必须被相关进程使用，并且通信是单向的。`socketpair` 函数为同一台计算机上两个连接的套接字创建两个文件描述符。这些文件描述符允许相关进程之间进行双向通信。它的前三个参数与 `socket` 调用相同：它们指定域、连接样式和协议。最后一个参数是一个两个整数的数组，其中填充了两个套接字的文件描述符，类似于 `pipe`。当你调用 `socketpair` 时，必须指定 `PF_LOCAL` 为域。

## 精通 Linux

- 6 设备
- 7 `/proc` 文件系统
- 8 Linux 系统 `syscall` 调用
- 9 内联汇编代码
- 10 安全
- 11 示例 GNU/Linux 应用程序

## 6 设备

`Linux` 与大多数操作系统一样，通过称为设备驱动程序的模块化软件组件与硬件设备进行交互。设备驱动程序将硬件设备通信协议的特殊性从操作系统隐藏，并允许系统通过标准化接口与设备交互。

在 `Linux` 下，设备驱动程序是内核的一部分，可以静态链接到内核中，也可以作为内核模块按需加载。设备驱动程序作为内核的一部分运行，用户进程无法直接访问。然而，`Linux` 提供了一种进程与设备驱动程序通信的机制——通过类文件对象。这些对象出现在文件系统中，程序可以打开它们、对其进行读取和写入，几乎就像处理普通文件一样。使用 `Linux` 的低级 I/O 操作（见附录 B，“低级 I/O”）或标准 C 库的 I/O 操作，你的程序都可以通过这些类文件对象与硬件设备通信。

`Linux` 还提供了若干类文件对象，它们直接与内核通信而不是与设备驱动程序通信。这些没有链接到硬件设备；相反，它们提供了各种特殊行为，对应用程序和系统程序有用。

## 访问设备时务必小心！

本章中的技术提供了访问运行在 `Linux` 内核中的设备驱动程序的直接路径，并通过它们连接到系统的硬件设备。请谨慎使用这些技术，因为误用可能会导致 GNU/`Linux` 系统损坏或数据丢失。

请特别查看侧边栏“块设备的危险性”。

## 6.1 设备类型

设备文件不是普通文件——它们不代表磁盘文件系统上的数据区域。相反，从设备文件读取或写入设备文件的数据会传递给相应的设备驱动程序，然后从那里传递到底层设备。设备文件有两种：

- **字符设备**：代表读取或写入串行数据字节流的硬件设备。串口和并行端口、磁带驱动器、终端设备和声卡都是字符设备的示例。
- **块设备**：代表以固定大小块读取或写入数据的硬件设备。与字符设备不同，块设备提供对存储在设备上数据的随机访问。磁盘驱动器是块设备的示例。

典型的应用程序永远不会使用块设备。块设备通过类文件对象进行通信，就像它们是普通文件一样。使用 `Linux` 的低级 I/O 操作（见附录 B，“低级 I/O”）或标准 C 库的 I/O 操作，你的程序都可以通过这些类文件对象与硬件设备通信。

## 块设备的危险性

本章的技术提供了访问运行在 `Linux` 内核中的设备驱动程序的直接路径，并通过它们访问连接到系统的硬件设备。请谨慎使用这些技术，因为误用可能会导致 GNU/`Linux` 系统损坏或数据丢失。

块设备提供对磁盘的直接访问。非 root 进程配置为无法访问这些设备，root 进程通过写入块设备可能会造成严重破坏。

在访问块设备时务必小心。

应用程序有时会使用字符设备，尽管我们将在接下来的章节中讨论它们。

## 6.2 设备号

`Linux` 使用两个数字来识别设备：主设备号和次设备号。主设备号指定设备对应的驱动程序。次设备号区分由单个驱动程序控制的设备。

例如，主设备号 3 对应 IDE 控制器。IDE 控制器可以连接两个设备（磁盘、磁带或光驱驱动器）；其“主”设备的次设备号为 0，“从”设备的次设备号为 64。主设备上的分区（如果设备支持分区）由次设备号 1, 2, 3 等表示。从设备上的分区由次设备号 65, 66, 67 等表示。主设备号列在 `Linux` 文档中。在某些 `Linux` 发行版中，这些文档可以在 `/usr/src/linux/documentation/devices.txt` 找到。`/proc/devices` 列出了当前加载到内核的设备驱动程序的主设备号。（更多信息请参见 `/proc` 文件系统。）

## 6.3 设备目录

设备目录在许多方面与普通文件相同。你可以使用 `mv` 命令移动它，如果你尝试使用 `cp` 复制设备目录，你将从设备读取字节（如果设备支持读取）并写入目标文件。如果你覆盖设备目录，你将把字节写入相应的设备目录。

你可以使用 `mknod` 命令（查看 `man 1 mknod`）在文件系统中创建设备目录，或者使用 `mknod` 系统调用（查看 `man 2 mknod`）。只有超级用户进程可以使用 `mknod` 系统调用创建块设备和字符设备。

要使用 `mknod` 命令创建设备，请在第一个参数中指定设备目录在文件系统中出现的路径。在第二个参数中，指定 `b` 表示块设备或 `c` 表示字符设备。将主设备号和次设备号作为第三和第四参数提供。例如，此命令在当前目录下创建一个名为 `/dev/lp0` 的字符设备。该设备的主设备号为 6，次设备号为 0。这些数字对应于第一个并行端口。

```bash
# mknod /dev/lp0 c 6 0
```

# 132 第6章 设备

记住，只有超级用户进程可以创建块和字符设备，因此你必须以 root 登录才能成功调用此命令。

`ls` 命令专门显示设备条目。如果你调用 `-l` 或 `-o` 选项，输出每行的第一个字符将指定条目的类型。回想起 `-`（连字符）表示普通文件，而 `d` 表示目录。同样，`b` 表示块设备，`c` 表示字符设备。对于后两者，`ls` 会打印主设备号和次设备号，而这里通常会显示普通文件的大小。例如，我们可以显示创建的块设备：

```text
brw-r---- 1 root      6, 0 Mar 7 17:03 /dev/lp0
```

在程序中，你可以使用 `stat` 判断文件系统是否是块设备或字符设备，然后检索其设备号。请参见附录 B 中的 B.2 节“stat”。

要删除条目，请使用 `rm`。这不会删除设备或设备驱动；只是从文件系统中删除设备条目。

```bash
% rm /dev/lp0
```

### 6.3.1 `/dev` 目录

按照习惯，GNU/`Linux` 系统包含一个 `/dev` 目录，其中包含了 `Linux` 已知的所有字符设备和块设备条目。`/dev` 中的条目具有对应主设备号和次设备号的标准名称。

例如，连接到主 IDE 控制器的主设备其主、次设备号分别为 3 和 0，标准名称为 `/dev/hda`。如果该设备支持分区，则其上的第一个分区（设备号为 1）的标准名称为 `/dev/hda1`。你可以在你的系统上检查这一点：

```bash
% ls -l /dev/hda /dev/hda1

brw-r---- 1 root      disk      3, 0 May 5 1998 /dev/hda
brw-r---- 1 root      disk      3, 1 May 5 1998 /dev/hda1
```

同样，`/dev` 包含一个我们之前使用过的并行端口字符设备条目：

```bash
% ls -l /dev/lp0

crw-r---- 1 root      daemon    6, 0 May 5 1998 /dev/lp0
```

在大多数情况下，你不应该使用 `mknod` 创建自己的设备条目。`/dev` 中已经存在这些条目。非超级用户程序只能使用预有的条目，因为它们无法自己创建。通常，只有系统管理员和处理特殊硬件设备的开发人员才需要创建设备条目。大多数 GNU/`Linux` 发行版包含帮助系统管理员创建正确名称的标准设备条目的工具。

## 6.3.2 通过打开文件访问设备

如何使用这些设备？对于字符设备，操作非常简单：像打开普通文件一样打开设备，并对其读取或写入。你甚至可以使用 `cat` 等普通文件命令，或使用 shell 的重定向语法向设备发送或从设备接收数据。

例如，如果你将打印机连接到计算机第一个并行端口，可以通过将文件直接发送到 `/dev/lp0` 来打印文件。要打印 `document.txt` 的内容，调用以下命令：

```bash
% cat document.txt > /dev/lp0
```

你必须拥有写入设备条目的权限才能成功；在许多 GNU/`Linux` 系统上，权限被设置为只有 root 和系统的打印守护进程 (`lpd`) 可以写入该设备文件。此外，打印机的输出取决于你的打印机如何解释你发送的数据内容。打印机会打印你发送的纯文本文件，而另一些则不会。PostScript 打印机会渲染并打印你发送的 PostScript 文件。例如，在程序中，向设备发送数据就是如此简单。它使用低层 I/O 函数将缓冲区的内容发送到 `/dev/lp0`。

## 6.4 硬件设备

表 6.1 列出了一些块设备。类似设备的设备遵循显而易见的模式（例如，第一块 SCSI 驱动器上的第二个分区是 `/dev/sda2`）。在检查 `/proc/mounts` 中的已挂载文件系统时，知道这些设备名称代表哪些设备有时很有用（更多信息请参见第 7 章第 7.5 节“驱动器、挂载和文件系统”）。

| 表 6.1 常见块设备部分列表 |
| :--- | :--- | :--- | :--- |
| 设备 | 名称 | 主设备号 | 次设备号 |
| :--- | :--- | :--- | :--- |
| 第一个软驱驱动器 | `/dev/fd0` | 2 | 0 |
| 第二个软驱驱动器 | `/dev/fd1` | 2 | 1 |
| 主 IDE 控制器，主设备 | `/dev/hda` | 3 | 0 |
| 主 IDE 控制器，主设备，第一个分区 | `/dev/hda1` | 3 | 1 |

> 1. Windows 用户会识别出此设备类似于神奇的 Windows 文件 `LPR1`。
> 2. 你的打印机可能在每行末尾需要显式的回车符（ASCII 码 14），并在每页末尾需要分页符（ASCII 码 12）。

| 表 6.1 续 |
| :--- | :--- | :--- | :--- |
| 设备 | 名称 | 主设备号 | 次设备号 |
| :--- | :--- | :--- | :--- |
| 主 IDE 控制器，主设备 | `/dev/hda` | 3 | 0 |
| 主 IDE 控制器，主设备，第一个分区 | `/dev/hda1` | 3 | 1 |
| 次 IDE 控制器，主设备 | `/dev/hdc` | 3 | 0 |
| 次 IDE 控制器，主设备，第一个分区 | `/dev/hdc1` | 3 | 1 |
| 第三 IDE 控制器，主设备 | `/dev/hde` | 3 | 0 |
| 第三 IDE 控制器，主设备，第一个分区 | `/dev/hde1` | 3 | 1 |
| 第一个 SCSI 驱动器，主设备 | `/dev/sda` | 3 | 0 |
| 第一个 SCSI 驱动器，主设备，第一个分区 | `/dev/sda1` | 3 | 1 |
| 第二个 SCSI 驱动器，主设备 | `/dev/sdb` | 3 | 2 |
| 第二个 SCSI 驱动器，主设备，第一个分区 | `/dev/sdb1` | 3 | 3 |
| 第三个 SCSI 驱动器，主设备 | `/dev/sdc` | 3 | 4 |
| 第三个 SCSI 驱动器，主设备，第一个分区 | `/dev/sdc1` | 3 | 5 |
| 第四个 SCSI 驱动器，主设备 | `/dev/sdd` | 3 | 6 |
| 第四个 SCSI 驱动器，主设备，第一个分区 | `/dev/sdd1` | 3 | 7 |
| 第五个 SCSI 驱动器，主设备 | `/dev/sde` | 3 | 8 |
| 第五个 SCSI 驱动器，主设备，第一个分区 | `/dev/sde1` | 3 | 9 |
| 第六个 SCSI 驱动器，主设备 | `/dev/sdf` | 3 | 10 |
| 第六个 SCSI 驱动器，主设备，第一个分区 | `/dev/sdf1` | 3 | 11 |

## 表 6.2 字符设备

| 设备 | 名称 | 主设备号 | 次设备号 |
| :--- | :--- | :--- | :--- |
| 第一个并行端口 | `/dev/lp0` | 6 | 0 |
| 第二个并行端口 | `/dev/lp1` | 6 | 1 |
| 第一个软驱驱动器 | `/dev/fd0` | 2 | 0 |
| 第二个软驱驱动器 | `/dev/fd1` | 2 | 1 |
| 主 IDE 控制器，主设备 | `/dev/hda` | 3 | 0 |
| 主 IDE 控制器，主设备，第一个分区 | `/dev/hda1` | 3 | 1 |
| 次 IDE 控制器，主设备 | `/dev/hdc` | 3 | 0 |
| 次 IDE 控制器，主设备，第一个分区 | `/dev/hdc1` | 3 | 1 |
| 第三 IDE 控制器，主设备 | `/dev/hde` | 3 | 0 |
| 第三 IDE 控制器，主设备，第一个分区 | `/dev/hde1` | 3 | 1 |
| 第一个 SCSI 驱动器，主设备 | `/dev/sda` | 3 | 0 |
| 第一个 SCSI 驱动器，主设备，第一个分区 | `/dev/sda1` | 3 | 1 |
| 第二个 SCSI 驱动器，主设备 | `/dev/sdb` | 3 | 2 |
| 第二个 SCSI 驱动器，主设备，第一个分区 | `/dev/sdb1` | 3 | 3 |
| 第三个 SCSI 驱动器，主设备 | `/dev/sdc` | 3 | 4 |
| 第三个 SCSI 驱动器，主设备，第一个分区 | `/dev/sdc1` | 3 | 5 |
| 第四个 SCSI 驱动器，主设备 | `/dev/sdd` | 3 | 6 |
| 第四个 SCSI 驱动器，主设备，第一个分区 | `/dev/sdd1` | 3 | 7 |
| 第五个 SCSI 驱动器，主设备 | `/dev/sde` | 3 | 8 |
| 第五个 SCSI 驱动器，主设备，第一个分区 | `/dev/sde1` | 3 | 9 |
| 第六个 SCSI 驱动器，主设备 | `/dev/sdf` | 3 | 10 |
| 第六个 SCSI 驱动器，主设备，第一个分区 | `/dev/sdf1` | 3 | 11 |

## 6.5 特殊设备

`Linux` 还提供了若干不对应硬件设备的字符设备。这些条目均使用主设备号 1，该编号与 `Linux` 内核的内存设备相关，而不是设备驱动程序。

### 6.5.1 `/dev/null`

`/dev/null` 条目，即空设备（null device），非常方便。它有两个用途；你可能至少熟悉第一个：

- `Linux` 会丢弃任何写入 `/dev/null` 的数据。一个常用的技巧是在某些不需要输出的场景中将 `/dev/null` 指定为输出文件。例如，为了运行一个命令并丢弃其标准输出（而不打印或将其写入文件），可以将标准输出重定向到 `/dev/null`：
  ```bash
  % verbose_command > /dev/null
  ```
- 从 `/dev/null` 读取总是导致文件结束（end-of-file）。例如，使用 `open` 打开 `/dev/null` 的文件描述符并尝试从该文件描述符读取，`read` 将不会读取任何字节并返回 0。如果你从 `/dev/null` 复制到另一个文件，目标文件将是一个长度为 0 的文件：
  ```bash
  % cp /dev/null empty-file
  % ls -l empty-file
  -rw-r---- 1 samuel samuel 0 Mar 8 00:27 empty-file
  ```

### 6.5.2 `/dev/zero`

`/dev/zero` 设备条目的行为就像一个填充了 0 字节的无限文件。无论你尝试从 `/dev/zero` 读取多少数据，`Linux` 都会“生成”足够的 0 字节。

为了说明这一点，请运行附录 B B.1.4 节“读取数据”中列表 B.4 提供的 `hexdump` 程序。该程序以十六进制格式打印文件内容。

```bash
% hexdump /dev/zero

00000000 : 00 00 00 00 00 00 00 00 00 00 00 00
00000010 : 00 00 00 00 00 00 00 00 00 00 00 00
00000020 : 00 00 00 00 00 00 00 00 00 00 00 00
00000030 : 00 00 00 00 00 00 00 00 00 00 00 00
```

当你确信它会无限运行时，按下 Ctrl+C。内存映射 `/dev/zero` 是一种分配内存的高级技术。更多信息请参阅第 5 章“进程间通信”中的第 5.3.5 节“mmap 的其他用途”，并参阅第 8 章“Linux 系统调用”第 8.9 节“mprotect: 设置内存权限”中的侧边栏“获取页对齐内存”作为示例。

### 6.5.3 `/dev/full`

`/dev/full` 条目的行为就像位于一个没有空间的文件系统上的文件。对 `/dev/full` 的写入将失败，并将 `errno` 设置为 `ENOSPC`，这通常表示写入的设备已满。

例如，你可以尝试使用 `cp` 命令向 `/dev/full` 写入：

```bash
% cp /etc/fstab /dev/full

cp: /dev/full: No space left on device
```



### 6.5.3 `/dev/full`

`/dev/full` 条目主要用于测试你的程序在写入文件时如果磁盘空间耗尽时的表现。

### 6.5.4 随机数设备

特殊设备 `/dev/random` 和 `/dev/urandom` 提供了对 Linux 内核内置随机数生成设施的访问。

大多数生成随机数的函数（例如标准 C 库中的 `random` 函数）实际上生成的是伪随机数。尽管这些数字满足随机数的一些属性，但它们是可重复的：如果你从相同的种子值开始，每次都会获得相同的伪随机数序列。这种行为是不可避免的，因为计算机本质上是确定且可预测的。对于某些应用程序，这种行为是不希望的；例如，如果你能获取加密算法所采用的随机数序列，可能会破解该算法。

要在计算机程序中获取更好的随机数需要外部随机性源。Linux 内核利用了一个特别好的随机性源：你！通过测量你的操作（如击键和鼠标移动）之间的时间延迟，Linux 能够生成不可预测的高质量随机数流。你可以通过读取 `/dev/random` 和 `/dev/urandom` 来访问此流。你读取的数据是一个随机生成的字节流。

这两个设备之间的区别在 Linux 耗尽其随机性源时体现出来。如果你尝试在没有输入操作（不移动鼠标或执行类似操作）的情况下读取大量字节，Linux 会阻塞读取操作。只有当你提供随机性时，Linux 才会生成更多随机字节并返回给程序。

例如，尝试使用 `od` 命令显示 `/dev/urandom` 的内容。每行输出显示 16 个随机数。

*   我们使用 `od` 而不是列表 B.4 中的 `hexdump` 程序，尽管它们的功能几乎相同，因为 `hexdump` 在数据耗尽时会终止，而 `od` 会等待更多数据的可用。`-t x` 允许你以十六进制格式打印文件内容。

```bash
% od -t x1 /dev/random
00000000 2c 9c 7a 8b 2e 79 3d 65 36 c2 e2 1b 52 75 1e
00000020 2d 6d 1e 7a 91 05 2d 04 c3 a6 54 29 f4 46 04
00000040 b3 b0 8d 94 21 57 f3 96 01 26 dc a2 94 c3 9b 3a
00000060 05 a3 02 bc 22 0a bc c9 45 dd a6 59 40
```

你看到的输出可能会有很多，但当 Linux 耗尽随机性存储时，输出将停止。现在尝试移动鼠标或在键盘上输入，观察额外的随机数出现。为了获得更好的随机性，可以让你的猫在键盘上走动。

相比之下，来自 `/dev/urandom` 的随机永远不会。如果 Linux 耗尽了随机性，它将使用加密算法从过去的随机字节序列生成伪随机字节。尽管这些字节对于许多用途来说已经足够随机，但它们通过随机性测试的数量没有从 `/dev/random` 获取的字节多。

例如，如果你调用以下命令，随机字节将无限流动，直到你用 `Ctrl+C` 杀死程序：

```bash
% od -t x1 /dev/urandom
00000000 62 71 3d 3e a5 dd de 62 c0 42 78 bd 29 69 64
```

## 6.5 特殊设备

3. 使用回环设备（loopback device）挂载文件系统。要这样做，请使用 `mount` 命令并将磁盘镜像文件指定为挂载设备。通过 `-o` 选项指定 `loop=loopback-device` 作为挂载点，告知 `mount` 使用哪个回环设备。

例如，要挂载我们的磁盘镜像文件系统，请执行这些命令。记住，只有超级用户可以使用回环设备。第一条命令创建一个目录 `/tmp/virtual-fs` 作为虚拟文件系统的挂载点。

```bash
% mkdir /tmp/virtual-fs
% mount -o loop=/dev/loop0 /tmp/disk-image /tmp/virtual-fs
```

现在，你的磁盘镜像就像一个普通的 10MB 硬盘驱动器一样被挂载了。

```bash
% df -h /tmp/virtual-fs
% echo 'Hello, world!' > test.txt
% ls -l
```

| 文件系统 | 容量 | 已用 | 可用% | 挂载于 |
| :--- | :--- | :--- | :--- | :--- |
| `/tmp/disk-image` | 9.7M | 13k | 9.2M | 0% | `/tmp/virtual-fs` |

```bash
drwxr-xr-x 2 root root 12288 Mar 8 02:00 lost+found
-rw-rw-- 1 root root 14 Mar 8 02:12 test.txt
% cat test.txt
Hello, world!
```

你可以像使用其他磁盘一样使用它：

注意，`lost+found` 是由 `mkefs` 自动添加的目录。

5. 如果文件系统发生损坏，并且恢复了某些未与文件关联的数据，则它们会被放置在 `lost+found` 中。

完成后，请卸载虚拟文件系统。

```bash
% cd /tmp
% umount /tmp/virtual-fs
```

如果你愿意，可以删除 `disk-image`，也可以在以后重新挂载它以访问虚拟文件系统中的文件。你也可以将其拷贝到另一台计算机上并在那里挂载——你创建的整个文件系统将保持完好。

与其从零创建文件系统，不如直接从设备拷贝一个。例如，你只需通过从 CD-ROM 设备拷贝，即可创建 CD-ROM 内容的镜像。

如果你有一个 IDE CD-ROM 驱动器，请使用之前描述的相应设备名称，例如 `/dev/hda`。如果你还使用 SCSI CD-ROM 驱动器，设备名称将为 `/dev/scd` 或类似名称。你的系统可能还有一个指向相应设备的符号链接 `/dev/cdrom`。查阅你的 `/etc/fstab` 以确定哪个设备名称对应你计算机的 CD-ROM 驱动器。

只需拷贝到文件。生成的文件将是驱动器中 CD-ROM 文件系统的完整磁盘镜像——例如：

```bash
% dd if=/dev/cdrom of=/tmp/cdrom-image
```

这可能需要几分钟时间，取决于你拷贝的 CD-ROM 以及驱动器的速度。生成的镜像文件会很大——与 CD-ROM 的内容一样大。

现在你可以在不在驱动器中插入原始 CD-ROM 的情况下挂载这个 CD-ROM。例如，要将其挂载到 `/mnt/cdrom`，请使用此行：

```bash
% mount -o loop=/dev/loop0 /tmp/cdrom-image /mnt/cdrom
```

因为镜像在硬盘上，它的运行速度会比实际的 CD-ROM 磁盘快得多。注意大多数 CD-ROM 使用的文件系统类型为 `iso9660`。

## 6.6 PTY

如果你不带任何参数运行 `mount` 命令（这会显示挂载在你的系统上的文件系统），你会注意到类似下面的一行内容：

```bash
none on /dev/pts type devpts (rw,gid=5,mode=628)
```

这表示一种特殊的文件系统 `devpts` 挂载在 `/dev/pts`。该文件系统不与任何硬件设备关联，是由 Linux 内核创建的“魔法”文件系统。它类似于 `/proc` 文件系统；有关其工作原理的更多信息请参见第 7 章。

与 `/dev` 目录类似，`/dev/pts` 包含了对应设备的条目。但与普通目录 `/dev` 不同，`/dev/pts` 是一个由 Linux 内核动态创建的特殊目录。目录的内容随时间变化，并反映运行系统的状态。

`/dev/pts` 中的条目对应于伪终端（或伪 TTY，即 PTY）。Linux 为你打开的每一个新终端窗口创建一个 PTY，并在 `/dev/pts` 中显示对应的条目。PTY 设备就像终端设备一样工作——它接受来自键盘的输入，并显示运行在其中的程序的文本输出。PTY 是有编号的，且 PTY 编号就是 `/dev/pts` 中对应条目的名称。

你可以使用 `ps` 命令显示与进程关联的终端设备。使用 `-o` 选项将 `tty` 指定为自定义格式的字段之一。要显示共享同一终端的每个进程的进程 ID、TTY 和命令行，请执行 `ps -o pid,tty,cmd`。

### 6.6.1 PTY 演示

例如，你可以通过在以下命令中调用它，来确定与给定终端窗口关联的 PTY：

```bash
% ps -o pid,tty,cmd
PID TTY CMD
28832 pts/4
```

# 148 第 7 章 /proc 系统

这个文件里有什么？`/proc/version` 的内容包含一个描述 Linux 内核版本号的字符串。它包含了第 8 章“Linux 系统调用”中描述的 `uname` 系统调用可以获取的版本信息，以及其他信息，例如用于编译内核的编译器版本。你可以像读取其他文件一样轻松地读取 `/proc/version`。例如，使用 `cat` 命令显示内容的一种简单方法。

```text
/proc/version
Linux version 2.2.14-5.8 (root@x86.devel.redhat.com) (gcc version egcs-2.91.6 19980314/Linux (egcs-1.1.2 release)) #1 Tue Mar 7 21:07:39 EST 2000
```

`/proc` 文件系统中的各种条目在 `/proc` 页（第 5 节）中有详细描述。要查看它，请调用此命令：

```bash
man 5
```

在本章中，我们将描述 `/proc` 文件系统中对应用程序程序员可能最有用的某些特性，并提供使用它们的示例。`/proc` 的某些特性也难以调试。

如果你对 `/proc` 的具体工作原理感兴趣，可以查看 Linux 内核源码中 `/usr/src/linux/fs/proc/` 下的源代码。

## 7.1 从 /proc 提取信息

`/proc` 中的大多数条目提供的信息格式化为人类可读，但这些格式足够简单，易于解析。例如，`/proc/cpuinfo` 包含了有关系统 CPU（对于多处理器，则为多个 CPU）的信息。输出是一个值表，每行一个值，每个值前面都有一个描述该值的描述符和一个冒号。

例如，输出可能如下所示：

```text
/proc/cpuinfo
processor : 0
vendor_id : GenuineIntel
cpu family : 6
model : 5
model name : Pentium II (Descartes)
stepping : 2
cpu MHz : 400.913520
cache size : 512 KB
fdiv_bug : no
hlt_bug : no
sep_bug : no
fear_bug : no
coma_bug : no
fpu : 
fpu_exception : yes
cpuid level : 2
wp : yes
flags : fpu vme de pse tsc msr mace ce8 apic fsxr
mtr pge mca cmov pse 36 fxsr
bogomips : 399.77
```

从此输出中提取值的简单方法是将文件读取到缓冲区，并使用 `scanf` 在内存中进行解析。列表 7.1 显示了该示例。该程序包含了 `get_cpu_clock_speed` 函数，该函数从 `/proc/cpuinfo` 读取到内存并提取第一个 CPU 的时钟频率。

列表 7.1 (clock-speed.c) 从 `/proc/cpuinfo` 提取 CPU 时钟频率

```c
#include <stdio.h>
#include <string.h>

/* 返回系统 CPU 的时钟频率（单位为 MHz），由
/proc/cpuinfo 报告。在多处理器机器上，返回第一个 CPU 的速度。出错时返回 0。 */

float get_cpu_clock_speed () {
    FILE *fp;
    char buffer[1024];
    size_t bytes_read;
    char* match;
    float clock_speed;

    /* 将 /proc/cpuinfo 的整个内容读到缓冲区。 */
    fp = fopen("/proc/cpuinfo", "r");
    bytes_read = fread(buffer, 1, sizeof(buffer), fp);
    close(fp);

    /* 如果读取失败或缓冲区不够大则退出。 */
    if (bytes_read == 0 || bytes_read == sizeof(buffer))
        return 0;

    /* 文本添加空终止符。 */
    buffer[bytes_read] = '\0';

    /* 找到以 "cpu MHz" 开头的行。 */
    match = strstr(buffer, "cpu MHz");
    if (match == NULL)
        return 0;

    /* 解析该行以提取时钟频率。 */
    sscanf(match, "cpu MHz : %f", &clock_speed);

    return clock_speed;
}

int main ()
{
    printf("CPU clock speed: %4.0f MHz\n", get_cpu_clock_speed ());
    return 0;
}
```

注意，`/proc` 文件系统中条目的名称、语义和输出格式在新的 Linux 内核版本中可能会发生。如果你在程序中使用它们，应该确保当 `/proc` 条目缺失或格式异常时，程序的行为能够优雅降级。

## 7.2 进程条目

`proc` 文件系统包含每个在 GNU/Linux 系统上运行的进程的目录。每个目录的名称是对应进程的进程 ID（PID）。这些目录随着进程在系统中启动和终止而动态出现和消失。每个目录都包含若干条目，提供访问运行进程信息的接口。`/proc` 系统通过这些进程目录得出了其名称。

每个进程目录包含以下条目：

*   `cmdline` 包含进程的参数列表。`cmdline` 条目在第 7.2.2 节“进程参数列表”中有描述。
*   `cwd` 是指向进程当前工作目录的符号链接（例如，通过某些操作设置）。
*   `environ` 包含环境变量。`environ` 条目在第 7.2.3 节“环境变量”中有描述。
*   `exe` 是指向正在运行的程序的符号链接。`exe` 条目在第 7.2.4 节“可执行文件”中有描述。
*   `fd` 是子目录，包含进程打开的文件描述符。`fd` 条目在第 7.2.5 节“文件描述符”中有描述。
*   `maps` 显示映射到进程地址空间的文件。详细信息见第 5 章“内存”。
*   `root` 是指向进程根目录的符号链接。通常，它是指向 `/` 的链接。
*   `stat` 包含大量进程统计信息。这些数据与 `status` 条目相同，但采用原始数值格式。格式难以阅读，但更适合解析。
*   `statm` 包含进程使用的内存信息。`statm` 条目在第 7.2.6 节“内存统计信息”中有描述。
*   `status` 包含大量进程状态和统计信息，格式化为人类可理解。第 7.2.7 节“统计信息”包含 `status` 条目的描述。
*   `cpu` 条目仅出现在 SMP 内核上。它包含了按 CPU 分类的进程时间（用户态和内核态）。

注意，出于安全考虑，某些条目的权限被设置为允许进程所有者（或超级用户）访问。

### 7.2.1 /proc/self

`/proc` 文件系统中的一个条目使得程序能够使用 `/proc` 查找自身进程的信息。条目 `/proc/self` 是指向当前进程对应的 `/proc` 目录的符号链接。`/proc/self` 的目标取决于哪个进程查看它：每个进程看到自己的进程目录作为目标。

例如，列表 7.2 中的程序读取 `/proc/self` 链接的目标以确定其进程 ID（我们这样做是为了说明；调用第 3 章“进程”中 3.1.1 节“进程 ID”中的 `getpid` 函数是实现相同功能的简单得多的方法）。该程序使用 `readlink` 系统调用，见第 8.11 节“readlink：读取符号链接”，来提取符号链接的目标。

# 列表 7.2 (get-pid.c) 从 /proc/self 获取进程 ID

```c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>

/* 返回调用进程的进程 ID */
```

在第 2.1.1 节中，我们在列表 2.1 中展示了一个打印其参数列表的程序。使用 `/proc` 文件系统中的 `cmdline` 项，我们可以实现一个打印另一个进程参数的程序。列表 7.3 就是这样一个程序；它打印指定进程 ID（PID）进程的参数列表。由于 `cmdline` 内容中可能包含多个 NUL 而不是在末尾只有一个，我们无法使用 `strlen` 来确定字符串长度，因为 `strlen` 只计数到遇到 NUL 的字符数。相反，我们通过 `read` 获取 `cmdline` 的长度，`read` 返回读取的字节数。

## 7.2 进程项

列表 7.3 (print-arg-list.c) 打印运行进程的参数列表

```c
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

/* 打印 PID 指定进程的参数列表，每个参数占一行。 */

void print_process_arg_list(pid_t pid)
{
    int fd;
    char filename[24];
    char arg_list[1024];
    size_t length;
    char* next_arg;

    /* 生成进程的 cmdline 文件名。 */
    snprintf(filename, sizeof(filename), "/proc/%d/cmdline", (int) pid);
```



```c
    /* 读取文件内容。 */

    fd = open(filename, O_RDONLY);

    length = read(fd, arg_list, sizeof(arg_list));

    close(fd);

    /* read 不会对缓冲区进行 NUL 终止处理，因此在这里处理。 */

    arg_list[length] = '\0';

    /* 遍历参数。参数由 NUL 分隔。 */

    next_arg = arg_list;

    while (next_arg < arg_list + length) {

        /* 打印参数。每个参数都以 NUL 终止，因此将其
        视为普通字符串处理。 */

        printf("%s\n", next_arg);

        /* 移动到下一个参数。由于每个参数都
        以 NUL 终止，strlen 统计的是下一个参数的长度，
        而不是整个参数列表。 */

        next_arg += strlen(next_arg) + 1;

    }

}

int main(int argc, char *argv[]) {

    pid_t pid = (pid_t) atoi(argv[1]);

    print_process_arg_list(pid);

    return 0;

}
```

例如，假设进程 `372` 是系统日志守护进程 `syslogd`。

```bash
% ps 372
PID TTY      STAT TIME COMMAND
372 7       S 0:00 syslogd -m 0

./print-arg-list 372
```

```
syslogd
-m
0
```

在这种情况下，`syslogd` 被调用时带有参数 `-m`。

### 7.2.3 进程环境

`environ` 变量包含了进程的环境（参见第 2.1.6 节，“环境”）。与 `cmd` 类似，各个环境变量之间由 `NUL` 分隔。每个元素的格式与 `environ` 变量使用的格式相同，即 `VARIABLE=value`。

列表 7.4 展示了第 2.1.6 节列表 2.3 中程序的通用版本。该版本在命令行上接受一个进程 ID，并通过读取 `/proc` 来打印该进程的环境。

列表 7.4 (`print-environment.c`) 显示进程的环境

```c
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

/* 打印 PID 指定进程的环境，每个环境变量独占一行。 */

void process_environment (pid_t pid)

{

    int fd;

    char filename[24];

    char environment[8192];

    size_t length;

    char* next_var;

    /* 生成进程的环境文件名。 */

    snprintf(filename, sizeof(filename), "/proc/%d/environ", (int) pid);

    /* 读取文件内容。 */

    fd = open(filename, O_RDONLY);

    length = read(fd, environment, sizeof(environment));

    close(fd);

    /* read 不会对缓冲区进行 NUL 终止处理，因此在这里处理。 */

    environment[length] = '\0';

    /* 遍历变量。变量由 NUL 分隔。 */

    next_var = environment;

    while (next_var < environment + length) {

        /* 打印变量。每个变量都以 NUL 终止，因此只需
           视为普通字符串处理。 */

        printf("%s\n", next_var);

        /* 移动到下一个变量。由于下一个变量以
           NUL 终止，strlen 统计的是下一个参数的长度， */

        next_var += strlen(next_var) + 1;

    }

}
```

### 7.2.4 进程执行文件

`exe` 项指向可执行文件。在第 2.1.1 节中，我们解释过 `exe` 项是指向程序的符号链接。但注意，通过检查 `/proc/self/exe`，你可以找到调用进程的路径。这是确定可执行文件位置的一种有用技术。

列表 7.5 (`get-executable-path.c`) 获取可执行文件的路径

```c
#include <limits.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>

/* 查找可执行文件的路径。 */

void get_executable_path(char* buffer) {

    int fd;

    fd = open("/proc/self/exe", O_RDONLY);

    size_t length = read(fd, buffer, sizeof(buffer) - 1);

    close(fd);

    buffer[length] = '\0';

}

int main() {

    char path[PATH_MAX];

    get_executable_path(path);

    // ... (代码其余部分)

}
```

### 7.2.5 文件描述符

`fd` 子目录包含已打开的文件描述符项。回想我们在第 2.1.4 节“标准 I/O”中提到，文件描述符 `0`、`1` 和 `2` 分别初始化为标准输入、输出和错误。因此，通过向 `/proc/[pid]/fd/1` 写入，你可以向第一个窗口连接到 `stdout` 的设备（在本例中为终端）写入内容。在第二个窗口中，尝试向该文件写入消息：

```bash
% echo 'Hello, world.' >> /proc/1261/fd/1
```

文本出现在第一个窗口。标准输入、输出和错误的文件描述符也出现在 `fd` 子目录中。列表 7.6 显示了一个程序，它只是打开命令行指定的文件描述符，然后无限循环。

列表 7.6 (`open-and-spin.c`) 打开文件读取

```c
#include <fcntl.h>
#include <stdio.h>
#include <unistd.h>

int main (int argc, char* argv[]) {

    if (argc < 2) {

        fprintf(stderr, "Usage: %s <filename>\n", argv[0]);

        return 1;

    }

    const char* filename = argv[1];

    int fd = open(filename, O_RDONLY);

    printf("in process %d, file descriptor %d is open to %s\n",

           (int) getpid(), (int) fd, filename);

    while (1) {

        // loop forever

    }

    return 0;

}
```

```
lrwx------      1 samuel samuel    64 Jan 30 01:30 1 -> /dev/pts/2
lrwx------      1 samuel samuel    64 Jan 30 01:30 2 -> /dev/pts/2
lr-x------      1 samuel samuel    64 Jan 30 01:30 3 -> /etc/fstab
```

注意文件描述符 `3` 的项，它链接到在该描述符上打开的 `/etc/fstab` 文件。

文件描述符也可以在套接字或管道上打开（更多信息请参见第 5 章）。在这种情况下，对应文件描述符的符号链接目标将显示“socket”（套接字）或“pipe”（管道），而不是指向普通文件或设备。

## 7.2.6 进程内存统计

`statm` 项包含一个七个数字的列表，用空格分隔。每个数字都代表进程在特定类别中使用的内存页计数。这些类别按照数字出现的顺序列如下：

- 进程总大小
- 驻留在物理内存中的进程大小
- 与其它进程共享的内存——即同时被此进程和至少另一个进程映射的内存（例如共享库或未触碰的写页）
- 进程大小——即已加载的可执行代码大小
- 映射到此进程的共享库大小
- 此进程用于堆栈的内存
- 脏页数量——即被程序修改过的内存页

### 7.2.7 进程统计

`status` 项包含了关于进程的各种信息，采用了便于人类理解的格式。这些信息包括进程 ID (`PID`) 和父进程 ID (`PPID`)、真实和有效用户 ID 及组 ID、内存使用情况以及指定哪些信号被捕获、忽略和阻塞的位掩码。

## 7.3 硬件信息

`/proc` 文件系统中的其他几个项提供了对系统硬件信息的访问。虽然这些项通常对系统配置员和管理员感兴趣，但这些信息有时对应用程序开发人员也有帮助。我们在这里介绍一些更有实用的项。

### 7.3.1 CPU 信息

如前所示，`/proc/cpuinfo` 包含了关于运行 GNU/Linux 系统的 CPU 或 CPU 的信息。`Processor` 字段列出了处理器编号；对于单处理器系统，该值为 0。`Vendor`、`CPU Family`、`Model` 和 `Stepping` 字段允许你确定 CPU 的确切型号和修订。更有用的是 `Flags` 字段显示设置了哪些 CPU 标志，这指示了 CPU 可用的特性。例如，“mmx”表示扩展 MMX 指令可用。

来自 `/proc/cpuinfo` 的大部分信息源自 `cpuid` x86 汇编指令。该指令是程序获取 CPU 信息的底层机制。要更深入地理解 `/proc/cpuinfo` 的输出，请参阅英特尔《IA-32 架构软件开发手册第 2 卷：指令集参考》中 `cp` 指令的文档。该手册可以通过 `http://developer.intel.com/design` 获取。

最后一个元素 `bogsip` 是一个 Linux 特有的值。它是对处理器在紧凑循环中速度的测量，因此不是整体处理器速度的良好指标。

### 7.3.2 设备信息

`/proc/devices` 文件列出了系统可用的字符设备和块设备的设备号。关于设备类型和设备号的信息，请参见第 6 章“设备”。

### 7.3.3 PCI 总线信息

`/proc/pci` 文件列出了连接到 PCI 总线或总线的设备摘要。这些是真实的 PCI 扩展卡，也可能包括系统主板上的设备以及 AGP 卡。列表包含了设备类型；设备 ID 和厂商 ID；设备名称（如果可用）；设备提供的特性信息；以及设备使用的 PCI 资源信息。

### 7.3.4 串口端口信息

`/proc/tty/driver/serial` 文件列出了串口端口的配置信息和统计数据。串口端口从 0 开始编号。可以使用 `setserial` 命令获取并修改串口端口的配置信息。然而 `/proc/tty/driver/serial` 显示了关于每个串口端口中断数的额外统计。

3. 参阅《IA-32 英特尔架构软件开发手册》获取 MMX 指令的文档，并参考本书第 9 章“内联汇编代码”获取如何在 GNU/Linux 程序中使用这些及其他汇编指令的信息。
4. 注意，在 DOS 和 Windows 下，串口端口从 1 开始编号，因此 `COM1` 在 Linux 下对应串口端口号 0。

例如，来自 `/proc/tty/driver/serial` 的行：
（此处省略了重复的示例内容）

## 7.5.2 驱动器与分区

`/proc` 文件系统包含了连接到 IDE 控制器和 SCSI 控制器的设备信息（如果系统包含这些设备）。

在典型系统中，`/proc/ide` 子目录可能包含 `ide0` 和 `ide1` 两个子目录之一，分别对应主、从 IDE 控制器。这些目录包含对应于连接到控制器上的物理设备的进一步子目录。如果 Linux 未识别到任何连接的设备，则控制器或设备目录可能不存在。四个可能的 IDE 设备的完整路径列在表 7.1 所示。

| 控制器 | 设备 | 子目录 |
| --- | --- | --- |
| 主 (Primary) | 主 (Master) | `/proc/ide/ide0/hda/` |
| 主 (Primary) | 从 (Slave) | `/proc/ide/ide0/hdb/` |
| 从 (Secondary) | 主 (Master) | `/proc/ide/ide1/hdc/` |
| 从 (Secondary) | 从 (Slave) | `/proc/ide/ide1/hdd/` |

关于 IDE 设备名称的更多信息，请参见第 6.4 节，“硬件设备”。每个 IDE 设备目录包含多个条目，提供对设备标识和配置信息的访问。这里列出了一些最有用的条目：

- `model` 包含设备的型号标识字符串。
- `media` 包含设备的介质类型。可能值为 `disk`、`cdrom`、`tape`、`floppy` 和 `UNKNOWN`。
- `capacity` 设备的容量，以 512 字节块为单位。注意，对于 CD-ROM 设备，该值将为 $2^{-1}$，而不是驱动器磁盘的容量。注意 `capacity` 中的值代表整个物理磁盘的容量；磁盘分区内文件系统的容量会更小。

例如，这些命令显示了如何确定从 IDE 控制器主设备的介质类型和设备标识。在这种情况下，结果是一个 Toshiba CD-ROM 光驱。

```bash
% cat /proc/ide/ide1/hdc/media
cdrom

% cat /proc/ide/ide1/hdc/model
TOSHIBA CD-ROM QM-6702B
```

5. 如果配置适当，Linux 内核可以支持额外的 IDE 设备控制器。这些控制器从 `ide2` 开始按顺序编号。

## 7.5 驱动器、挂载与文件系统

如果系统中存在 SCSI 设备，`/proc/scsi/scsi` 包含了它们标识值的摘要。例如，内容可能如下所示：

```bash
% cat /proc/scsi/scsi
Attached devices:

Host: scsi Channel: 00 ID: 00 Lun: 00
Vendor: QUANTUM Model: ATLAS_V_9_WLS Rev: 0230
Type: Direct-Access ANSI: SCSI revision: 03

Host: scsi Channel: 00 ID: 04 Lun: 00
Vendor: QUANTUM Model: QM3910TD-SW Rev: N491
Type: Direct-Access ANSI SCSI revision: 02
```

这台计算机包含一个单通道 SCSI 控制器（指定为 `"scsi0"`），连接了两个 Quantum 驱动器，SCSI 设备 ID 分别为 `0` 和 `4`。

`/proc/partitions` 项显示了已识别磁盘设备的分区。对于每个分区，输出包含了主设备号和次设备号、1024 块的数量以及对应于分区的设备名。

`/proc/sys/dev/cdrom/info` 条目显示了关于 CD-ROM 驱动器能力的杂项信息。这些字段是自明的：

```bash
% cat /proc/sys/dev/cdrom/info
CD-ROM information, id: cdrom.c 2.56 1999/09/09

drive name: hdc
drive speed: 48
drive # of slots: 0
Can close tray: 1
Can open tray: 1
Can lock tray: 1
Can change speed: 1
Can select disk: 0
Can read multisession: 1
Can read MCN: 1
Reports media changed: 1
Can play audio: 1
```



## 7.5.3 挂载

`/proc/mounts` 提供了已挂载文件系统的摘要，对应单个挂载描述符，并列出了挂载的设备、挂载点和其他信息。注意 `/proc/mounts` 包含的信息与普通文件 `/etc/mtab` 相同，后者由 `mount` 命令自动更新。

这些是挂载描述符的元素：

- 行的第一个元素是挂载的设备（第 6 章）。对于如 `/` 等特殊文件系统，此项为空。
- 第二个元素是挂载点，即根系统中文件系统内容出现的位置。对于根文件系统本身，挂载点列为 `/`。对于交换分区（swap drives），挂载点列为 `swap`。
- 第三个元素是磁盘驱动器文件系统，DOS 或 Windows 驱动器可能以其他文件系统类型挂载，例如 `fat` 或 `vfat`。大多数 CD-ROM 包含 `iso9660` 文件系统。查看 `mount` 命令的手页以获取文件系统类型列表。
- 第四个元素列出了挂载标志。这些是在添加挂载时指定的选项。查看 `mount` 命令的手页以获取有关各种文件系统类型标志的说明。

在 `/proc/mounts` 中，最后两个元素始终为 `0` 且没有意义。

关于挂载描述符格式的详情，请参见 `fstab` 的帮助页。

GNU/Linux 包含了帮助你解析挂载描述符的函数；查看 `getdent` 函数的手页以获取使用这些函数的信息。

## 7.5.4 锁

第 8.3 节“fcntl：锁和其他文件操作”描述了如何使用 `fcntl` 系统调用来操作文件的读锁和写锁。`/proc/locks` 条目描述了系统中所有当前处理的锁。输出中的每一行对应一个锁。

对于使用 `fcntl` 创建的锁，行的前两个元素是 `POSIX ADVISORY`。第三个是 `WRITE` 或 `READ`，取决于锁的类型。下一个数字是持有锁的进程 `PID`。接下来的三个用冒号分隔的数字是文件所在设备的主设备号、次设备号以及 inode 节点号（后者用于在文件系统中定位该文件）。该行的剩余部分列出了内核内部的值，这些不具有通用性。

将 `/proc/locks` 的内容转换为有用信息需要一些侦查工作。例如，你可以通过运行列表 8.2 中的程序为文件 `/tmp/test-file` 创建锁，从而监控它的写锁。

```
% touch /test-file

% ./lock-file /tmp/test-file

file /tmp/test-file

opening /tmp/test-file

locking

locked; hit enter to unlock...
```

在另一个窗口中，查看 `/proc/locks` 的内容。

```
% cat /proc/locks

1: POSIX ADVISORY WRITE 5467 08:05:181288 2147483647 d1b5f740 00000000

dfea7d40 00000000 00000000
```

- `/etc/fstab` 文件列出了 GNU/Linux 系统的静态挂载配置。

## 7.6 系统统计

输出可能还有其他行，对应于其他程序持有的锁。在这种情况下，`5467` 是 `lock-file` 程序的 `PID`。使用 `ps` 来确定该进程正在运行。

```
% ps 5467

PID TID STAT COMMAND

5467 S 0:00 /lock-file /tmp/test-file
```

锁定的文件 `/tmp/test-file` 位于主设备号分别为 `8` 和 `5` 的设备上。这些数字恰好对应于 `/dev/sda`。

```
% df /tmp

Filesystem 1k-blocks Available Use% Mounted on

/dev/sda 845764 5094292 2935736 63% /
```

文件 `/tmp/test-file` 本身在该设备上的 inode 为 `181288`。

```
% ls --inode /tmp/test-file

18288 /tmp/test-file
```

关于设备号的更多信息，请参见第 6.2 节，“设备号”。

`/proc` 中的两个条目包含了有用的系统统计。`proc/loadavg` 文件包含了系统负载信息。前三个数字代表系统中活跃任务（实际运行的进程）在过去 `1`、`5` 和 `15` 分钟内的平均值。下一个条目显示当前可运行任务的数量（当前调度运行而非阻塞在系统调用中的进程）以及系统的总进程数。最后一个条目是最近运行的进程的 `PID`。

`/proc/uptime` 文件包含了系统启动以来的时间，以及系统空闲的时间。这两个值都以浮点数形式给出，单位为秒。

```
% /proc/uptime

3248936.18 3072330.49
```

列表 7.7 中的程序从系统提取提取运行时间和空闲时间，并以易读的单位显示它们。

# 第 166 页 第7 章 /proc 文件系统

## 列表 7.7 继续

```c
/* 转换常量。 */

const long minute = 60;

const long hour = minute * 60;

const long day = hour * 24;

/* 生成输出。 */

printf("%s:% ld days, %ld:%02ld:%02ld\n", label, time / day,
       (time % day) / hour, (time % hour) / minute, time % minute);

}

int main () {

  FILE *fp;

  double uptime, idle_time;

  /* 从 /proc/uptime 读取系统运行时间和累计的空闲时间。 */

  fp = fopen("/proc/uptime", "r");

  sscanf(fp, "%lf %lf\n", &uptime, &idle_time);

  fclose(fp);

  /* 进行进行总结。 */

  print_time("uptime", (long) uptime);

  print_time("idle time", (long) idle_time);

  return 0;

}
```

`uptime` 命令和 `sysinfo` 系统调用（见第 8.14 节，“sysinfo：获取系统统计数据”）也可以获取系统的运行时间。`uptime` 命令还会显示在 `/proc/loadavg` 中的负载平均值。

# 第8 章 Linux 系统调用

到目前为止，我们已经介绍了许多程序可以调用的用于执行系统相关功能的函数，例如解析命令行选项、处理进程和映射内存。如果你深入底层查看，你会发现根据实现方式，这些函数可以分为两类：

- `库函数` 是存在于程序外部库中的普通函数。我们到目前为止介绍的大多数库函数都在标准 C 库 `libc` 中。例如，`getopt_long` 和 `strtok` 就是 C 库提供的函数。

  调用库函数就像任何其他函数调用一样。参数被放在处理器寄存器或栈上，执行流转移到函数代码的起点，这些代码通常位于已加载的共享库中。

- `系统调用` 是在 Linux 内核中实现的。当程序发出系统调用时，参数会被封装并交给内核，内核将接管程序的执行，直到调用完成。系统调用不是普通的函数调用，需要一种特殊的程序来将控制权转移给内核。然而，GNU C 库（GNU/Linux 系统提供的标准 C 库的实现）通过函数封装了 Linux 系统调用，以便你能够轻松地调用它们。低级 I/O 函数（如 `read` 和 `write`）就是 Linux 上系统调用的示例。

Linux 系统调用集构成了程序与 Linux 内核之间最基础的接口。每个调用都提供了一个基本操作或能力。

某些系统调用非常强大，对系统产生巨大影响。例如，某些系统调用允许你关闭 Linux 系统，或分配系统资源并防止他人访问。这些调用具有限制：只有以超级用户权限运行的进程（由 `root` 账户运行的程序）才能调用它们。如果由非用户进程调用，这些调用将失败。

Linux 目前提供了约 `200` 种不同的系统调用。你所使用的 Linux 内核的系统调用列表位于 `/usr/include/asm/unistd.h` 中。其中一些供系统内部使用，另一些则仅用于实现库函数。在本章中，我们将介绍一组可能对应用程序程序员和系统程序员最有用的系统调用。大多数这些系统调用都定义在 `<unistd.h>` 中。

## 8.1 使用 strace

在开始讨论系统调用之前，介绍一个可以帮助你学习和调试系统调用的命令将非常有帮助。`strace` 命令跟踪另一个程序的执行过程，列出程序执行的任何系统调用以及它收到的任何信号。

要查看程序中的系统调用和信号，只需调用 `strace`，随后跟上程序及其命令行参数即可。例如，要查看由 `hostname` 命令调用的系统调用，可以使用以下命令：

```bash
$ strace hostname
```

```bash
execve("/bin/hostname", ["hostname", /* 49 vars */]) = 0
```

1. 不带任何标志的 `hostname` 仅仅是将计算机的主机名打印到标准输出。
2. 在 Linux 中，`exec` 族函数是通过 `execve` 系统调用实现的。

## 8.2 access：测试文件权限

第一个参数是要运行的程序名称；第二个是它的参数列表（仅包含一个元素）；第三个是它的环境列表，`strace` 为了简洁起省略了该部分。接下来的 30 多行是从共享库文件加载标准 C 库的机制的一部分。

最后是实际执行程序工作的系统调用。`uname` 系统调用用于从内核获取系统主机名，`uname(sys="Linux", node="hostname", ... ) = 0`。

观察发现 `strace` 很好地标记了结构体参数的字段（`sys` 和 `node`）。该结构体由系统调用填充——Linux 将 `sys` 字段设置为操作系统，将 `node` 字段设置为系统主机名。将进一步讨论 `uname` 调用。

列表 8.1 所示的程序使用 `access` 来检查文件是否存在并确定读/写权限。在命令行中指定要检查的文件名。

### 列表 8.1 (check-access.c) 检查访问权限

```c
#include <errno.h>

#include <stdio.h>

#include <unistd.h>

int main (int argc, char* argv[])

{

    if (argc != 2) {

        fprintf(stderr, "Usage: %s <filename>\n", argv[0]);

        return 1;

    }

    char* path = argv[1];

    int rval;

    /* 检查是否存在。 */

    rval = access(path, F_OK);

    if (rval == 0)

        printf("%s exists\n", path);

    else {

        if (errno == ENOENT)

            printf("%s does not exist\n", path);

        else if (errno == EACCES)

            printf("%s is not accessible\n", path);

    }

    /* 检查读权限。 */

    rval = access(path, R_OK);

    if (rval == 0)

        printf("%s is readable\n", path);

    else

        printf("%s is not readable (access denied)\n", path);

    /* 检查写权限。 */

    rval = access(path, W_OK);

    if (rval == 0)

        printf("%s is writable\n", path);

    else {

        if (errno == EACCES)

            printf("%s is not writable (access denied)\n", path);

        else if (errno == EROFS)

            printf("%s is not writable (read-only filesystem)\n", path);

    }

    return 0;

}
```

例如，要检查 CD-ROM 上名为 `README` 的文件的访问权限，可以这样调用：

```bash
% ./check-access /mnt/cdrom/README

/mnt/cdrom/README exists

/mnt/cdrom/README is readable

/mnt/cdrom/README is not writable (read-only filesystem)
```

## 8.3 fcntl: 锁和其他文件操作

`fcntl` 系统调用是对文件描述符进行若干高级操作的入口。`fcntl` 的第一个参数是一个已打开的文件描述符，第二个参数是指示要执行什么操作的值。对于某些操作，`fcntl` 接受一个额外的参数。在这里我们描述最实用的 `fcntl` 操作之一：锁。关于其他操作的信息，请参阅 `fcntl` 手册页。

`fcntl` 系统允许程序对文件加读锁或写锁，这与第 5 节“进程间通信”中的互斥锁（mutex locks）有些相似。读锁加在可读的文件描述符上，写锁加在可写的文件描述符上。同一时间不允许有多个进程持有对同一个文件的读锁，但只能有一个进程持有写锁，且同一个文件不能同时被读锁和写锁。请注意，锁实际上并不会阻止其他进程打开文件、读取或写入该文件，除非它们也通过 `fcntl` 获取了锁。

要对文件加锁，首先创建并清零一个 `struct flock` 变量。结构的 `l_type` 字段对于读锁为 `F_RDLOCK`，对于写锁为 `F_WRLCK`。然后调用 `fcntl`，传递文件描述符、`F_SETLKW` 操作码以及指向 `flock` 变量的指针。如果另一个进程持有阻止新锁获取的锁，`fcntl` 将阻塞直到该锁被释放。

列表 8.2 中的程序打开了一个由命令行提供的文件进行写入模式，并对其加了写锁。该程序等待用户按回车键，然后解锁并关闭文件。

### 列表 8.2 (lock-file.c) 使用 fcntl 创建写锁

```c
#include <fcntl.h>

#include <stdio.h>

#include <string.h>

#include <unistd.h>

int main (int argc
```

### 列表 8.2 续

```c
printf("locked; hit Enter to unlock...");

/* 等待用户按回车。 */

getchar();

printf("unlocking\n");

/* 释放锁。 */

lock_type = F_UNLCK;

fcntl(fd, F_SETLKW, &lock);

close(fd);

return 0;
```



在测试文件上（例如 `/tmp/test-file`）编译并运行程序，如下：

```
cc -o lock-file lock-file.c
touch /tmp/test-file
./lock-file /tmp/test-file
opening /tmp/test-file
locking
locked; hit Enter to unlock...
```

现在，在另一个窗口中尝试对同一个文件运行它。

```
./lock-file /tmp/test-file
opening /tmp/test-file
locking
```

注意，第二个实例在尝试加锁时被阻塞了。回到第一个窗口并按回车：

```
locking
```

在第二个窗口中运行的程序立即获取了锁。

如果你希望 `fcntl` 在无法获取请求的锁时不阻塞，请使用 `F_SETLK` 代替 `F_SETLKW`。如果无法获取锁，`fcntl` 会立即返回 -1。

Linux 还提供了通过 `flock` 调用实现的另一种文件锁机制。`fcntl` 版本有一个主要优势：它可以在 NFS 上的文件系统中工作（只要 NFS 服务器经过最近且正确的配置）。因此，如果你可以访问两台通过 NFS 挂载相同文件系统的机器，你可以使用两个不同的机器重复之前的示例。在一台机器上运行 `lock-file` 并指定 NFS 文件系统上的文件，然后在另一台机器上再次运行并指定同一个文件。当第一个程序释放锁时，NFS 会唤醒第二个程序。

网络文件系统（NFS）是一种常见的网络共享技术，类似于 Windows 共享和网络驱动器。

## 8.4 `fsync` 和 `fdatasync`: 刷新磁盘缓冲区

在大多数操作系统中，当你写入文件时，数据不会立即写入磁盘。相反，操作系统会将写入的数据缓存在内存缓冲区中，以减少所需的磁盘写入次数并提高程序的响应。当缓冲区满或发生其他条件时（例如，经过了足够的时间），系统会一次性将缓存数据写入磁盘。

Linux 也提供了这种缓存。通常情况下，这对性能非常有益。然而，这种行为可能会导致依赖磁盘记录完整性的程序变得不可靠。如果系统突然崩溃（例如由于内核崩溃或断电），程序在内存缓存中写入的任何数据尚未写入磁盘。

例如，如果你正在编写一个保存日志文件的事务处理程序。日志包含所有已处理事务的记录，以便在发生系统故障时，可以重建事务状态。保持日志文件的完整性显然很重要——每处理一个事务，其日志条目应立即发送到磁盘驱动器。

为了帮助实现这一点，Linux 提供了 `fsync` 系统调用。它接受一个参数，即可写的文件描述符，并将写入此文件的所有数据刷新到磁盘。在数据物理写入之前，`fsync` 调用不会返回。

列表 8.3 中的函数说明了 `fsync` 的用法。它向日志文件写入单行条目。

### 列表 8.3 (`write_journal.entry.c`) 写入并同步日志条目

```c
#include <fcntl.h>
#include <string.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

const char* journal_filename = "journal.log";

void write_journal_entry(char* entry) {
  int fd = open(journal_filename, O_WRONLY | O_CREAT | O_APPEND, 0660);
  write(fd, entry, strlen(entry));
  fsync(fd);
  close(fd);
}
```

另一个系统调用 `fdatasync` 与 `fsync` 作用相同。然而，虽然 `fsync` 保证更新修改时间，但 `fdatasync` 不；它只保证数据会被写入。在当前的 Linux 版本中，这两个系统调用实际上是相同的，都会更新修改时间。打开文件时使用 `O_SYNC` 标志。

## 8.5 `getrlimit` 和 `setrlimit`: 资源限制

`getrlimit` 和 `setrlimit` 系统调用允许你读取并设置程序消耗资源限制。你可能熟悉 `ulimit` shell 命令，它可以限制你运行的程序；这些系统调用允许程序自己做到这一点。

对于每个资源有两个限制：硬限制和软限制。软限制永远不能超过硬限制，只有具有特权的进程才能更改硬限制。通常，应用程序会降低软限制来限制其使用的资源。

`getrlimit` 和 `setrlimit` 都接受资源限制类型和指向 `rlimit` 变量的指针作为参数。`getrlimit` 调用填充该结构的字段，而 `setrlimit` 调用根据其内容更改限制。`rlimit` 结构体有两个字段：`rlim_cur` 是软限制，`rlim_max` 是硬限制。

这里列出了可以更改的一些有用的资源限制及其代码：

- `RLIMIT_CPU`: 程序使用的最大 CPU 时间（以秒为单位）。这不是程序实际在 CPU 上执行的时间，这与墙钟时间并不一定相等。如果程序超过此时间限制，将被 `SIGXCPU` 信号终止。
- `RLIMIT_DATA`: 程序可以为数据分配的最大内存。超过此限制的额外分配将失败。
- `RLIMIT_NPROC`: 该用户允许运行的进程的最大数量。如果进程调用 `fork` 且系统中属于该用户的进程运行过多，`fork` 将失败。
- `RLIMIT_FILE`: 进程同时可以打开的文件描述符的最大数量。

查看 `setlimit` 手册页以获取系统资源的完整列表。

列表 8.4 中的程序说明了如何设置程序消耗的 CPU 时间限制。它设置了 1 秒的 CPU 时间限制，然后进入无限循环。Linux 在程序超过 1 秒 CPU 时间后不久就会杀掉该进程。

1. 有关 `ulimit` 的更多信息，请参阅你 shell 的手册页。

## 8.6 `getrusage`: 进程统计

### 列表 8.4 (`limit-cpu.c`) CPU 时间限制演示

```c
#include <sys/resource.h>
#include <sys/time.h>
#include <unistd.h>

int main () {
    struct rlimit rl;

    /* 获取当前限制。 */
    getrlimit(RLIMIT_CPU, &rl);

    /* 设置 CPU 限制为 1 秒。 */
    rl.rlim_cur = 1;

    setrlimit(RLIMIT_CPU, &rl);

    /* 执行忙碌工作。 */
    while (1);

    return 0;
}
```

当程序被 `SIGXCPU` 终止时，shell 会贴心地打印出一条解释该信号的消息：

```
./limit_cpu
CPU time limit exceeded（CPU 时间限制超出）
```

`getrusage` 系统调用从内核检索进程统计信息。通过将 `RUSAGE_SELF` 作为第一个参数可以获取当前进程的统计数据；通过传递 `RUSAGE_CHILD` 则可以获取由该进程及其子进程产生的所有终止子进程的统计数据。`usage` 的第二个参数是一个指向 `struct rusage` 变量的指针，该变量将被填充统计数据。

`struct rusage` 中一些最有趣的字段列如下：

- `ru_utime`—一个时间字段，包含进程所消耗的用户时间（秒）。用户时间是执行用户程序时花费的 CPU 时间，而不是在内核调用中花费的时间。
- `ru_stime`—一个时间字段，包含进程消耗的系统时间（秒）。系统时间是代表进程执行系统调用时花费的 CPU 时间。
- `ru_maxrss`—在执行过程中，进程数据一次性占用的最大物理内存。

`getrusage` 的 man 页面列出了所有可用字段。关于 `struct timeval` 的信息，请参见第 8.7 节“`gettimeofday`: 挂钟时间”。

### 列表 8.5 (`print-ctime-times.c`) 显示进程的用户时间和系统时间

```c
#include <stdio.h>
#include <sys/resource.h>
#include <sys/time.h>
#include <unistd.h>

void print_cpu() {
    struct rusage usage;
    getrusage(RUSAGE_SELF, &usage);
    printf("CPU time: %ld.%06ld sec user, %ld.%06ld sec system\n",
           usage.ru_utime.tv_sec, usage.ru_utime.tv_usec,
           usage.ru_stime.tv_sec, usage.ru_stime.tv_usec);
}
```

## 8.7 `gettimeofday`: 挂钟时间

`gettimeofday` 系统调用获取系统的挂钟时间。它接收一个指向 `struct timeval` 变量的指针。该结构表示一个时间，以秒为单位，分为两个字段。`tv_sec` 字段包含整数秒，`tv_usec` 字段包含额外的微秒数。此 `struct timeval` 代表自 UNIX 纪元（即 UTC 时间 1970 年 1 月 1 日午夜）开始以来经过的秒数。`gettimeofday` 调用还接收第二个参数，该参数应为 `NULL`。使用此系统调用时包含 `<sys/time.h>`。

列表 8.5 中的函数也打印了当前进程的用户时间和系统时间。

对于秒秒数通常非常有用。`localtime` 函数接收一个指向 `struct timeval` 变量的指针。该结构表示一个时间，以秒为单位，分为两个字段。`tv_sec` 字段包含整数秒，`tv_usec` 字段包含额外的微秒数。此 `struct timeval` 代表自 UNIX 纪元（即 UTC 时间 1970 年 1 月 1 日午夜）开始经过的秒数。

填充的 `struct tm` 包含有用字段：
- `tm_year`—年份。
- `tm_mon`—月份。
- `tm_hour`—小时。
- `tm_min`—分钟。
- `tm_mday`—日期。
- `tm_wday`—星期几。
- `tm_dst`—指示是否处于夏令时的标志。

`strftime` 函数此外可以根据格式从 `struct tm` 生成字符串，显示日期和时间。例如，使用 8.6 格式：

```c
"%Y-%m-%d %H:%M:%S"
```

## 8.8 `mlock`: 锁定物理内存

`mlock` 系列允许程序将其地址空间的一部分或全部锁定在内存中。这防止了 Linux 将内存交换到分区。锁定内存区域的方法是简单调用 `mlock` 并传入区域的起始指针和长度。Linux 按页划分内存，并且一次只能锁定整页；`getpagesize` 函数返回页大小，在 x86 上为 4KB。

例如，要分配 32MB 地址空间并将其锁定到内存，你会使用：

```c
int alloc_size = 32 * 1024 * 1024;
char* memory = malloc(alloc_size);
mlock(memory, alloc_size);
```

注意，仅仅分配内存并使用 `mlock` 锁定并没有为进程预留物理内存，因为页面可能是写时复制。因此，你应该向每个页写入一个无效值：

```c
size_t i;
size_t page_size = getpagesize();

for (i = 0; i < alloc_size; i += page_size)
    memory[i] = 0;
```

解锁区域的方法是调用 `munlock`，其参数与 `mlock` 相同。

如果你想将程序的整个地址空间锁定在物理内存中，调用 `mlockall`。此系统调用接收一个标志参数：`MCL_CURRENT` 锁定所有已分配的内存，但未来的分配不锁定；`MCL_FUTURE` 锁定调用后分配的所有页面，包括当前后续。

锁定大量内存（尤其是使用 `mlockall`）对整个 Linux 系统都是危险的。无限制的内存锁定是导致系统停止的好方法，因为其他运行进程被迫竞争更小的物理内存资源，并在内存和交换分区之间频繁切换（这被称为抖动）。由于此原因，只有具有超级权限的进程可以使用 `mlock` 或 `mlockall` 锁定内存。如果非用户进程调用这些函数，它将失败、返回 -1 并将 `errno` 设置为 `EPERM`。

## 8.9 `mprotect`: 设置内存权限

监控程序内存使用情况的一种方便方法是使用 `top` 命令。在 `top` 的输出中，`SIZE` 列显示了每个程序的虚拟地址空间大小（你的程序代码、数据和栈的总大小，其中部分可能被分页到交换空间）。`RSS` 列（代表驻留集合）显示了每个程序当前驻留的物理内存量。所有运行程序的 `RSS` 值之和不能超过你计算机的物理内存大小，且所有地址空间的总和被限制为 2GB（对于 32 位的 Linux 版本）。

如果你使用了 `mlock` 系统调用，请包含 `<sys/mman.h>`。

在第 5.3 节“映射内存”中，我们展示了如何使用 `mmap` 系统调用将文件映射到内存中。回想 `mmap` 的第三个参数是内存保护标志 `PRO_READ`、`PRO_WRITE` 和 `PRO_EXEC` 的按位或，分别代表读、写、执行权限，或者使用 `PRO_NONE` 表示无内存访问。如果程序尝试对这些权限不允许的内存位置执行操作，它将会被 `SIGSEGV`（段错误）信号终止。

内存被映射后，可以使用 `mprotect` 系统调用修改这些权限。`mprotect` 的参数是内存区域的地址、该区域的大小以及一组保护标志。内存区域必须由整个页面组成；区域的地址必须相对于系统的页大小的，且区域的长度必须是页大小的倍数。这些页面的保护标志将被指定的值替换。

### 获取页对齐内存

请注意，`malloc` 返回的内存区域通常不是页对齐的，即使内存的大小是页大小的倍数。如果你想保护从 `malloc` 获取的内存，你必须分配一个更大的内存区域并在其中找到一个页对齐的区域。

或者，你可以使用 `mmap` 系统调用跳过 `malloc`，直接从 Linux 内核分配页对齐的内存。详情请见第 5.3 节“映射内存”。

例如，假设你的程序通过映射 `/dev/zero` 分配了一页内存，如第 5.3.5 节“`mmap` 的其他用途”所述。该内存最初是可读且可写的。

```c
int fd = open("/dev/zero", O_RDONLY);
char* memory = mmap(NULL, pagesize(), PRO_READ | PRO_WRITE, MAP_PRIVATE, fd, 0);
close(fd);
```

随后，你的程序可以通过调用 `mprotect` 将内存设为只读：

```c
mprotect(memory, pagesize(), PRO_READ);
```

监控内存访问的一种高级技术是使用 `mmap` 保护内存区域，或者保护并处理 Linux 在程序尝试访问内存时发送给程序的 `SIGSEGV` 信号。列表 8.7 中的示例说明了这种技术。

### 列表 8.7 (`mprotect.c`) 使用 `mprotect` 检测内存访问

```c
#include <fcntl.h>
#include <signal.h>
#include <stdio.h>
#include <string.h>
#include <sys/mman.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

static int alloc_size;
static char* memory;

void segv_handler(int signal_number)
{
    printf("memory accessed!\n");
    mprotect(memory, alloc_size, PRO_READ);
}

int main()
{
    int fd;
    struct sigaction sa;

    /* 安装 segv_handler 作为 SIGSEGV 的处理函数。 */
    memset(&sa, 0, sizeof(sa));
    sa.sa_handler = &segv_handler;
    sigaction(SIGSEGV, &sa, NULL);

    /* 通过映射 /dev/zero 分配一页内存。初始将内存映射为只写。 */
    alloc_size = pagesize();
    fd = open("/dev/zero", O_RDONLY);
    memory = mmap(NULL, alloc_size, PRO_WRITE, MAP_PRIVATE, fd, 0);
    close(fd);

    /* 写入该页以获取私有副本。 */
    memory[0] = 0;

    /* 使内存不可写。 */
    mprotect(memory, alloc_size, PRO_NONE);

    /* 写入分配的区域。 */
    memory[0] = 1;

    /* 全部完成；取消内存映射。 */
    printf("all done\n");
    munmap(memory, alloc_size);

    return 0;
}
```



该程序遵循以下步骤：
1. 程序为 `SIGSEGV` 安装信号处理程序。
2. 程序通过映射 `/dev/zero` 分配一页内存并向该页写入值以获取私有副本。
3. 程序通过调用带有 `PRO_NONE` 的 `mprotect` 保护内存。
4. 当程序随后写入内存时，Linux 向其发送 `SIGSEGV`，由 `segv_handler` 处理。信号处理程序取消内存保护，允许内存访问继续。
5. 当信号处理程序完成后，控制返回到 `main`，程序在其中使用 `munmap` 释放内存。

## 8.10 nanosleep: 高精度睡眠

`nanosleep` 系统调用是标准 UNIX `sleep` 的高精度版本。`nanosleep` 不是睡眠整数秒，而是接收一个指向 `struct timespec` 对象的指针，该对象可以表示精确到纳秒级的时间。然而，由于 Linux 内核的工作细节，`nanosleep` 提供的实际精度是 1 毫秒——仍然比 `sleep` 提供的精度好。这种额外的精度非常有用，例如用于调度间隔短的频繁操作。

`struct timespec` 结构有两个字段：`tv_sec`（整数秒）和 `tv_nsec`（额外的纳秒数）。`tv_nsec` 的值必须小于 `1e9`。

`nanosleep` 相比 `sleep` 具有另一个优势。在 `sleep` 中，信号的传递会中断 `sleep` 的执行，这会将 `errno` 设置为 `EINTR` 并返回 -1。然而，`nanosleep` 接收第二个参数，另一个指向 `struct timespec` 对象的指针，如果该指针不为空，则会被填充剩余时间（即请求的睡眠时间与实际睡眠时间之间的差值）。这使得恢复睡眠操作变得简单。

列表 8.8 中的函数提供了 `sleep` 的另一种实现。与普通系统调用不同，该函数接收一个表示秒数的浮点值，并在被中断时重新启动。

### 列表 8.8 (better_sleep.c) 高精度睡眠

```c
#include <errno.h>
#include <time.h>

int better_sleep(double sleep_time) {
    struct timespec tv;

    /* 从秒数构造 timespec。 */
    tv.tv_sec = (time_t)sleep_time;

    /* 剩余纳秒。 */
    tv.tv_nsec = (long)((sleep_time - tv.tv_sec) * 1e9);

    while (1) {
        /* 指定的时间进行睡眠。 */
        int rval = nanosleep(&tv, &tv);

        if (rval == 0) {
            /* 完成整个睡眠。 */
            return 0;
        } else if (errno == EINTR) {
            /* 被信号中断。重试。 */
            continue;
        } else {
            /* 其他错误；退出。 */
            return -1;
        }
    }
}
```

## 8.11 readlink: 读取符号链接

`readlink` 获取符号链接的目标。它接受三个参数：符号链接的路径、接收目标的缓冲区以及缓冲区的长度。通常，`readlink` 不会对填充的缓冲区进行 NUL 终止。然而，它会返回目标的字符数，因此对字符串进行终止非常简单。

如果 `readlink` 的第一个参数指向的文件不是符号链接，`readlink` 将 `errno` 设置为 `EINVAL` 并返回 -1。

列表 8.9 中的小型程序打印命令行指定的符号链接的目标。

### 列表 8.9 (print-symlink.c) 打印符号的目标

```c
#include <errno.h>
#include <stdio.h>
#include <unistd.h>

int main(int argc, char* argv[])
{
    if (argc < 2) return 1;

    char target_path[256];
    char* link_path = argv[1];

    /* 尝试读取符号链接的目标。 */
    int len = readlink(link_path, target_path, sizeof(target_path));

    if (len == -1) {
        /* 调用失败。 */
        if (errno == EINVAL)
            /* 不是符号链接；报告此信息。 */
            fprintf(stderr, "%s is not a symbolic link\n", link_path);
        else
            /* 发生其他问题；打印通用消息。 */
            perror("readlink");

        return 1;
    } else {
        /* 对路径进行 NUL 终止。 */
        target_path[len] = '\0';

        /* 打印它。 */
        printf("%s\n", target_path);
        return 0;
    }
}
```

例如，你可以创建一个符号链接并使用 `print-symlink` 读取它：

```sh
% ln -s /usr/bin/wc my_link
% ./print-symlink my_link
/usr/bin/wc
```

## 8.12 sendfile: 快速数据传输

`sendfile` 系统调用提供了从一个文件描述符拷贝到另一个的高效机制。文件描述符可以是磁盘文件、套接字或其他设备。

通常，为了从一个文件描述符拷贝到另一个，程序会分配一个固定大小的缓冲区，从一个拷贝一些数据到缓冲区，将输出写入另一个描述符，并重复此过程直到完成所有数据。这在时间和空间上都是低效的，因为需要额外的内存来分配缓冲区，并且对该缓冲区执行了一次额外的拷贝。

### 第 8 章 Linux 系统调用

使用 `sendfile`，可以消除中间缓冲区。调用 `sendfile` 并传递要写入的文件描述符；要读取的描述符；偏移量变量的指针；要传输的字节数。偏移量变量携带了从输入文件中开始读取的偏移量（0 表示文件开头），并在传输后更新为文件中的相应位置。返回值是传输的字节数。如果你的程序使用了 `sendfile`，请在程序中包含 `<sys/sendfile.h>`。

### 列表 8.10 (copy.c) 使用 sendfile 复制文件

```c
#include <fcntl.h>
#include <stdlib.h>
#include <stdio.h>
#include <sys/sendfile.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    int read_fd;
    int write_fd;
    struct stat stat_buf;
    off_t offset = 0;

    /* 打开输入文件。 */
    read_fd = open(argv[1], O_RDONLY);

    /* 统计输入文件以获取大小。 */
    fstat(read_fd, &stat_buf);

    /* 打开输出文件进行写入，权限与源文件相同。 */
    write_fd = open(argv[2], O_WRONLY | O_CREAT, stat_buf.st_mode);

    /* 将字节从一个文件发送到另一个文件。 */
    sendfile(write_fd, read_fd, &offset, stat_buf.st_size);

    /* 关闭。 */
    close(read_fd);
    close(write_fd);

    return 0;
}
```

`sendfile` 调用可以用于许多地方以使复制更加高效。一个很好的例子是在 Web 服务器或其他网络守护进程中，它们通过网络向客户端程序提供文件内容。通常，会从连接到客户端计算机的套接字接收请求。服务器程序打开本地磁盘文件以检索要提供的数据，并将文件内容写入网络套接字。使用 `sendfile` 可以显著加快此操作。为了使网络传输尽可能高效，还需要采取其他步骤，例如正确设置套接字参数。然而，这些超出了本书的范围。

## 8.13 setimer: 设置间隔定时器

`setimer` 系统调用是 `alarm` 调用的泛化。它调度在固定时间过去后，在未来的某个时间点递送信号。程序可以使用 `setimer` 设置三种不同类型的定时器：

- 如果定时器代码为 `ITIM_REAL`，在指定的墙上钟时间过去后，向进程发送 `SIGALRM` 信号。
- 如果定时器代码为 `ITIM_VIRTUAL`，在进程执行了指定时间后，向进程发送 `SIGVTALRM` 信号。进程未执行的时间（即内核或其他进程运行的时间）是不计入的。
- 如果定时器代码为 `ITIM_PROF`，当在进程执行期间或代表进程执行系统调用期间指定的时间过去后，向进程发送 `SIGPROF` 信号。

`setimer` 的第一个参数是定时器代码，指定要设置哪个定时器。第二个参数是指向 `struct itimerval` 对象的指针，指定定时器的新设置。第三个参数如果不为空，则是一个指向另一个 `struct itimerval` 对象的指针，用于接收旧的定时器设置。

`struct itimerval` 变量有两个字段：

- `it_value` 是一个 `struct timeval` 字段，包含定时器下一次过期并发送信号之前的时间。如果其为 0，则定时器被禁用。
- `it_interval` 是另一个 `struct timeval` 字段，包含定时器过期后重置的值。如果其为 0，则定时器在过期后将被禁用。如果不为零，则定时器将每隔该间隔重复过期。

`struct timeval` 类型在第 8.7 节“gettimeimeofday：墙上钟时间”中有描述。

列表 8.11 中的程序说明了如何使用 `setimer` 来跟踪程序的执行时间。定时器被配置为每 250 毫秒过期一次，并发送 `SIGVTALRM` 信号。

### 列表 8.11 (itimer.c) 定时器示例

```c
#include <signal.h>
#include <stdio.h>
#include <string.h>
#include <sys/time.h>

void timer_handler(int signum)
{
    static int count = 0;
    printf("定时器过期 %d 次\n",count);
}

int main () {
    struct sigaction sa;
    struct itimerval timer;

    /* 将 timer_handler 安装为 SIGALRM 的信号处理程序。 */
    memset(&sa, 0, sizeof(sa));

    sa.sa_handler = &timer_handler;
    sigaction(SIGVTALRM, NULL);

    /* 配置定时器每 250ms 过期一次。 */
    timer.it_value.tv_sec = 0;
    timer.it_value.tv_usec = 250000;
    timer.it_interval.tv_sec = 0;
    timer.it_interval.tv_usec = 250000;

    /* 启动定时器。 */
    setimer(ITIM_VIRTUAL, &timer, NULL);

    /* 等待。 */
    while (1);

    return 0;
}
```

## 8.14 sysinfo: 获取统计信息

`sysinfo` 系统调用填充一个结构体以获取系统统计。它的唯一参数是指向 `sysinfo` 的指针。`sysinfo` 的一些有趣的字段包括：

- `uptime` — 自启动以来的时间（秒）
- `totalram` — 总可用 RAM
- `freeram` — 空闲 RAM
- `procs` — 进程数

列表 8.12 中的程序打印了系统的统计信息。

### 列表 8.12 (sysinfo.c) 使用 sysinfo 打印统计

```c
#include <linux/kernel.h>
#include <sys.h>
#include <stdio.h>
#include <sys/sysinfo.h>

int main () {
    struct sysinfo si;

    sysinfo(&si);

    printf("启动时间: %ld 秒\n", si.uptime);
    printf("总 RAM: %u 字节\n", si.totalram);
    printf("空闲 RAM: %u 字节\n", si.freeram);
    printf("进程数: %d\n", si.procs);

    return 0;
}
```

## 8.15 uname

`uname` 调用填充一个结构体以各种系统信息，包括计算机的网络名、域名和操作系统版本。为 `uname` 传递一个参数 `utsname` 对象。如果你使用 `uname`，请包含 `<utsname.h>`。

`uname` 这些字段：

- `sysname` — 操作系统名称（如 Linux）
- `release`, `version` — 内核发布版本和版本
- `machine` — 关于运行的硬件平台。对于 x86，这将是 i386 或 i686。
- `node` — 计算机的主机名
- `domain` — 计算机的域名

这些每一个都是字符字符串。

列表 8.13 中的小型程序打印了 Linux 发布版本、版本以及硬件信息。

### 列表 8.13 (print-uname) 打印版本和硬件

```c
#include <stdio.h>
#include <utsname.h>

int main () {
    struct utsname u;

    uname(&u);

    printf("%s 发布 %s (版本 %s) 在 %s\n", u.sysname, u.release, u.version, u.machine);

    return 0;
}
```

## 内联汇编代码

今天，很少程序员使用汇语言。高级语言如 C 和 C++ 运行在几乎所有架构上，并且编写和维护代码的效率更高。当程序员需要在程序中使用汇编指令时，GNU 编译器允许程序员向程序添加依赖架构的汇编语言指令。

GCC 的内联汇语句不应盲目使用。汇编指令是依赖架构的，因此例如使用 x86 指令的程序无法在 PowerPC 上编译。要使用它们，你需要对应架构的汇编语言支持。然而，内联汇语句允许你直接访问硬件并产生更快的代码。

`asm` 指令允许你在 C 和 C++ 程序中插入汇编指令。例如，这条指令：

```c
asm ("fsin" : (answer) : "%0" (angle));
```

是这段 C 语句的一种 x86 特有写法：

```c
answer = sin(angle);
```



-1. `sin(angle)` 表达式通常实现为对数学库的调用，但如果你指定了 `-O1` 或更高的优化标志，`GCC` 足够智能，可以将函数调用替换为单个的 `fsin` 汇编指令。

## 第 9 章 内联汇编代码

注意，与普通的汇编指令不同，`asm` 语句允许使用 C 语法指定输入和输出操作数。
要了解更多关于 x86 指令集（本章中将使用的 x86），请参阅 `http://developer.intel.com/design/pentium/manuals/` 和 `http://www.x86-64.org/documentation`。

## 9.1 何时使用汇编代码

尽管 `asm` 语句可能会被滥用，但它们允许程序直接访问计算机硬件，并能产生执行快速的程序。在编写需要直接与硬件交互的操作系统代码时可以使用它们。例如，`/usr/include/asm/io.h` 包含了直接访问输入输出端口的汇编指令。Linux 源码文件 `/usr/src/linux/x86/kernel/process.s` 提供了另一个示例，在空闲循环代码中使用 `itlt`。参见 `/usr/src/linux/arch/` 和 `/usr/src/linux/drivers` 中的其他 Linux 源文件。

汇编指令还可以加速计算机程序的内层循环。例如，如果程序运行的大部分时间都在计算相同角度的正弦和余弦，这个内层循环可以使用 `fsincos` x86 指令进行重写。例如 `/usr/include/bits/mathsim.h`，它将其封装在内联汇编序列的宏中，从而加速了超越函数的计算。

你应该只在万不得已的情况下才使用内联汇编来加速代码。目前的编译器非常复杂，对于它们所生成代码的处理器细节了如指掌。因此，编译器通常可以选择某些看似不直观或迂回、但实际执行速度比指令序列更快的代码序列。除非你非常熟悉你的处理器的指令集和调度，否则让编译器的优化器为你的大多数操作生成汇编代码可能更好。

偶尔，一或两条汇编指令可以替换几行高层语言代码。例如，使用 C 语言确定一个非零整数最高位非零位的位置需要循环或浮点计算。包括 x86 在内的许多架构都使用一条汇编指令（`bsr`）来计算此位元位置。我们将在第 9.4 节“示例”中演示其中之一的使用：

- 2. 算法或数据结构的改变可能比使用汇编指令更有效地减少程序的运行时间。

## 9.2 简单内联汇编

这里我们通过一个 x86 示例介绍 `asm` 汇编指令的语法，将值右移 8 位：

```c
asm ("shrl $8, %%0" : "r" (answer) : "cc");
```

关键字 `asm` 后面跟着一个括号表达式，由由冒号分隔的节组成。第一部分包含一条汇编指令及其操作数。第一部分 `shrl` 右移位其第一个操作数中的位。它的第一个操作数由 `%%0` 表示。第二个操作数是常量 `$8`。

第二部分指定输出。指令的一个输出将放在 C 变量 `answer` 中，字符串 `"r` 包含一个等号表示输出操作数，`r` 表示 `answer` 存储在寄存器中。

第三部分指定输入。C 变量 `operand` 指定要位移的值。字符串 `%r` 表示它存储在寄存器中，但省略了等号，因为它是输入操作数，而不是输出操作数。

第四部分指示指令更改了状态码 `cc` 的值。

### 9.2.1 将 asm 转换为汇编指令

`GCC` 对 `asm` 语句的处理非常简单。它产生汇编指令来处理 `asm` 的操作数，并用你指定的指令替换 `asm` 语句。它不会对指令进行任何形式的分析。

例如，`GCC` 将此代码片段

```c
double foo, bar;

asm ("mycool_asm %%1, %%0" : "r" (bar) : "r" (foo));
```

转换为这些 x86 汇编指令：

```assembly
mov -8(%ebp),%edx
mov -4(%ebp),%ecx
mycool_asm %ecx,%edx
mov %edx,-16(%ebp)
mov %ecx,-12(%ebp)
```

请记住，在 32 位 x86 架构上，`foo` 和 `bar` 每个都需要两个字的栈存储空间。寄存器 `ebp` 指向栈。
当 `mycool_asm` 执行时，第一条指令将 `foo` 拷贝到寄存器 `EDX` 和 `ECX` 中。编译器决定使用相同的寄存器来存储答案，最后两条指令将其拷贝到 `bar` 中。它选择合适的寄存器，甚至复用相同的寄存器，并自动地在适当的位置之间拷贝操作数。

## 9.3 扩展汇编语法

在接下来的子节中，我们将描述 `asm` 语句的语法规则。它们的节由冒号分隔。

我们将引用这个内联汇编语句，它计算布尔表达式 `x < y`：

```c
asm ("%fucomp %%st(1), %%st; seta %%al" :

  =="a" (result) : "c" (y), "t" (x) : "cc", "st");
```

首先，`fucomp` 比较两个操作数 `x` 和 `y`，并将指示结果的值存储到状态码寄存器中。然后 `seta` 将这些值设置为结果 0 或 1。

### 9.3.1 汇编指令

第一部分包含括在引号内的汇编指令。示例 `asm` 包含两条汇编指令 `fucomp` 和 `seta`，用分号分隔。如果汇编器不允许使用分号，请使用换行符。`%%(1)` 的含义取决于架构。

### 9.3.2 输出

第二部分使用 C 语法指定输出操作数。每个操作数通过一个约束字符串后跟跟一个 C 表达式来指定。对于必须是值的输出操作数，约束字符串应该以等号开头。指定特定架构寄存器的字母可以在 `GCC` 源代码中找到。表 9.1 总结了这些。

表 9.1 x86 架构的寄存器字母

| 寄存器 | 可能使用的寄存器 |
| --- | --- |
| R | 通用寄存器 (EAX, ECX, EBX, EC, ESI, EDI, EBP, ESP) |
| q | 数据通用寄存器 (EAX, EBX, ECX, EDX) |
| f | 浮点寄存器 |
| t | 栈顶浮点寄存器 |
| u | 次栈顶浮点寄存器 |
| a | EAX 寄存器 |
| b | EBX 寄存器 |
| c | ECX 寄存器 |
| d | EDX 寄存器 |
| x | SSE 寄存器（流式 SIMD 扩展） |
| y | MMX 多媒体寄存器 |
| A | 由 EAX 和 EDX 形成的 8 字节值 |
| D | 字符串操作的目标指针 (EDI) |
| S | 字符串的源指针 (ESI) |

### 9.3.3 输入

第三部分指定汇编指令的输入操作数。输入操作数的约束字符串不应有等号，等号表示左值。否则，输入操作数的语法与输出操作数相同。

要指示从同一个寄存器读取并写入同一个 `asm`，请使用输入约束字符串。例如，要指示输入寄存器与第一个输出寄存器相同，使用 `%.0`。输出操作数从左到右从 0 开始编号。仅仅为输出操作数和输入操作数指定相同的 C 表达式并不能保证这两个值被放在同一个寄存器中。

如果没有输入操作数且随后的破坏节（clobber）为空，则可以省略此输入部分。

### 9.3.4 覆盖（Clobbers）

如果一条指令作为副作用修改了一个或多个寄存器的值，请在 `asm` 的第四部分指定被覆盖的寄存器。例如，该指令修改了状态码寄存器，用 `cc` 表示。用逗号分隔表示被覆盖寄存器的字符串。如果指令可以修改任意内存位置，请指定 `memory`。编译器会利用这些覆盖信息来确定在 `asm` 执行后哪些值必须重新加载。如果你没有正确指定此内容，`GCC` 可能会错误地假设寄存器仍然包含（实际上已经被覆盖掉的）值，这将影响你程序的正确性。

## 9.4 示例

x86 架构包含了用于确定字（word）中设置的最低位（LSB）和最高位（MSB）位置的指令。处理器可以非常高效地执行这些指令。相比之下，在 C 中实现相同的操作则需要循环和位移。

例如，`bsr` `asm` 指令会计算其第一个操作数中最高位的位置，并将该位位置（从 0 开始计数，最低位）放入其第二个操作数中。为了放置数字的位位置，我们可以使用此 `asm` 语句：

```
asm ("bsrl %%1
```

你可以在 C 中实现相同操作的一种方法是使用以下循环：

```c
long i;

for (i = (number >> 1), position = 0; i >= 1; ++position);
```

为了测试这两个版本的结果，我们将它们放在一个循环中，计算大量数值的位位置。列表 9.1 使用 C 循环实现实现了这一点。该程序遍历整数，范围从 1 直到命令行指定的数值。对于每个数字，它都会计算出被设置的最高位。列表 9.2 使用内联汇编指令执行相同的操作。注意，在两个版本中，我们都将计算出的位位置赋值给 `volatile` 类型的变量 `result`。这样做是为了强制编译器优化器，使其不要消除整个位位置计算；如果结果未被使用或存储在内存中，优化器会将该计算视为“死代码”并将其简化。

> 列表 9.1 (`bit-pos-loop.c`) 使用循环查找位位置

```c
#include <stdio.h>
#include <stdlib.h>

int main (int argc, char* argv[])
{
    long max = atoi(argv[1]);
    long number;
    long i;
    unsigned position;
    volatile unsigned result;

    /* 对大量数值重复该操作。 */
    for (number = 1; number <= max; ++number) {
        /* 不断地向右位移数字，直到结果为
        零。记录所需的位移所需的次数。 */
        for (i = (number >> 1); position = 0; i != 0; ++position)
            i >>= 1;
        /* 设置的最高位的位置就是我们在第一次位移后
        所需要的位移次数。 */
        result = position;
    }
    return 0;
}
```

列表 9.2 (`bit-pos-asm.c`) 使用 `bsrl` 查找位位置

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    long max = atoi(argv[1]);
    long number;
    unsigned position;
    volatile unsigned result;
    /* 对大量数值重复该操作。 */
    for (number = 1; number <= max; ++number) {
        /* 使用 bsrl 汇编指令计算最高设置位的位置。 */
        asm ("bsrl %%1, %%0" : "r" (number));
        result = position;
    }
    return 0;
}
```

我们将使用全位位优化优化编译这两个版本：
`% cc -02 -o bit-pos-loop bit-pos-loop.c`
`% cc -02 -o bit-pos-asm bit-pos-asm.c`

现在让我们使用 `time` 命令运行每个版本来测量执行时间。我们将指定一个大值作为命令行参数，以确保每个版本至少运行几秒。

```
% time .bit-pos-loop 250000000
19.5user 0system 0:20.32elapsed 95%CPU (@avgtext+@avgdata)
@maxresident)0inputs+outputs (73major+11minor)pagefaults0swaps

% time .bit-pos-asm 250000000
31.9user 0system 0:03.22elapsed 95%CPU (@avgtext+@avgdata)
@maxresident)0inputs+outputs (73major+11minor)pagefaults0swaps
```

注意，使用内联汇编的版本执行速度快得多（此示例的结果可能会有所不同）。

## 9.5 优化问题

`GCC` 优化器尝试重排和重写程序代码，以在存在 `asm` 表达式的情况下化执行时间。如果优化器确定 `asm` 的输出值未被使用，除非在 `asm` 和其参数之间出现 `volatile` 关键字，否则该指令将被省略。（作为一个特殊情况，`GCC` 不会在循环之外移动没有输出 `asm`。）任何 `asm` 都可以以难以预测的方式移动，即使是跨越跳转。确保其执行的唯一方法是使用 `volatile` 变量。

## 9.6 维护与可移植性

如果你决定使用不可移植的 `asm` 语句，将它们封装在函数中将有助于维护。例如，如果你使用了依赖架构的指令，可以将它们封装在函数中，为其他架构提供 C 实现。

## 10 安全性

Linux 的安全性来自于它处理用户和组的方式。每个文件和目录都有所有者和一个组，权限定义了谁可以读、写或执行。例如，你可能想创建一个经理可以读取但普通员工不能读取的文件。这是通过将组设置为经理并相应设置权限来实现的。确保执行的唯一方法是使用 `volatile` 变量。

## 10.1 用户与组

每个 Linux 用户分配有一个唯一的数字，称为用户 ID (UID)。每个用户 ID 都可以多个组的成员，但组只包含用户。像用户一样，组也有名称。然而，就像用户名，组名并不重要；系统内部使用组 ID。继续我们的示例，你可以创建一个组并将 ID 放入其中。

如果你好奇想查看自己的 ID 以及所在的组，可以使用 `id` 命令。例如，输出可能如下：

```
$ id
uid=501(mitchell) gid=501(mitchell) groups=501(mitchell),503(cs1)
```

第一部分显示运行命令的用户 ID 为 501。该命令还推断出相应的用户名并显示在括号中。该部分显示用户 ID 501 实际上在两个组中：组 501 (名为 mitchell) 和组 503 (名为 cs1)。你可能疑惑为什么组 501 出现了两次：一次在 gid 字段中，一次在 groups 字段中。我们稍后会解释这一点。

## 10.2 处理用户 ID 和进程组 ID

### 10.1.1 超用户

有一个用户账户非常特殊。该用户的用户 ID 为 0，用户名通常为 `root`。它有时被称为超级用户账户（superuser）。`root` 用户可以做任何事情：读取任何文件、删除任何文件、添加新用户、关闭网络访问等。以 `root` 身份运行的进程——即以 `root` 身份运行——可以执行许多特殊操作。

这种设计的麻烦在于，许多程序需要由 `root` 运行，因为许多程序需要执行特殊操作。如果这些程序中的任何一个出现异常，可能会导致混乱。当程序以 `root` 运行时，没有有效的方法可以限制它；它可以做任何事情。由 `root` 运行的程序必须仔细编写。

## 10.2 用户 ID 和组 ID

到目前为止，我们讨论的是由特定用户执行的命令。这并不完全准确，因为计算机永远不知道是谁在使用它。如果 Alice 留下了她的用户名和密码，那么 Eve 就可以以 Alice 的身份登录，计算机允许 Eve 做任何事情。系统只知道在使用哪个用户，而不知道是谁在打字。

系统安全的责任由开发者、系统用户和系统管理员共同承担。每个进程都有一个关联的用户 ID 和组 ID。当你调用一个命令时，它通常运行在一个进程中，该进程的用户 ID 和组 ID 与你的用户和用户组相同。当我们说一个用户执行了某项操作时，我们实际上是指具有相应用户 ID 的进程执行了该操作。当进程发出系统调用时，内核决定是否继续该操作。它通过检查进程试图访问的资源以及检查与进程关联的用户 ID 和组 ID 来做出这一判断。

现在你知道 `id` 命令是做什么的了。它显示的是当前进程的组 ID。尽管 Alice 属于多个组，但当前进程只能有一个组。如果你在程序中必须操作用户 ID 和组 ID（而且你正在编写处理安全的程序），你应该使用在 `<sys/types.h>` 中定义的 `uid_t` 和 `gid_t` 类型。尽管用户 ID 和组 ID 本质上是整数，但要避免对这些类型使用了多少位做任何假设，只需将它们视为用户和组身份的不透明句柄（opaque handles）。

要获取当前进程的用户 ID 和组 ID，可以使用 `<unistd.h>` 中声明的 `getuid()` 和 `getegid()` 函数。这些函数不接受任何参数，并且始终有效；你不需要检查错误。列表 10.1 显示了一个简单的程序，它提供了 `id` 命令的部分功能：

# 列表 10.1 (`simple.c`) 打印用户 ID 和组 ID

```c
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    uid_t uid = getuid();
    gid_t gid = getegid();
    printf("uid=%d gid=%d\n", (int)uid, (int)gid);
    return 0;
}
```

当运行此程序时（由运行该程序的同一用户运行），输出如下：
```
./simple
uid=501 gid=501
```



## 10.3 文件系统权限

查看用户和组如何运作的好方法是查看文件系统权限。通过检查系统如何将权限与每个文件关联，然后查看内核如何检查谁允许访问哪些文件，用户 ID 和组 ID 的概念将变得更加清晰。

每个文件恰好有一个所有用户和一个组。当你创建一个新文件时，该文件由创建进程的用户和组所有。在 Linux 看来，你对文件可以执行的基本操作是读取、写入和执行。（注意，创建文件和删除文件不是你对文件本身可以做的事；它们被认为是对包含该文件的目录可以做的事。我们稍后会讲这一点。）如果你无法读取一个文件，Linux 不允许你查看文件的内容。如果你无法写入一个文件，你就无法更改其内容。如果你对某个程序没有执行权限，你就无法运行该程序。

- 1. AT&T UNIX 操作系统只有一个特殊用户这一事实。相比之下，早期的一个具有多个特殊用户的操作系统被称为 MULTICS。
- 2. 实际上，有一些稀罕的例外，涉及粘滞位（sticky bits），稍将在第 10.3.2 节“粘滞位”中讨论。

Linux 允许你指定这三项操作——读取、写入和执行——中的哪些可以由所有者、所有组以及其他人执行。例如，你可以说所有者可以对文件做任何他想做的事，所有组中的任何人都可以读取和执行该文件（但不能写入），而其他人完全无法访问该文件。

你可以通过 `ls` 命令的 `-l` 或 `-o` 选项交互地查看权限位，或通过 `stat` 系统调用编程地查看。你可以通过 `chmod` 程序交互地设置权限位，或通过同名的系统调用编程地设置。要查看名为 `hello` 的文件的权限，请使用 `ls -l hello`。输出如下：

```
% ls -l hello
-rw-r--r-- 1 samuel csl 11734 Jan 22 16:29
```

## 10.4 安全

如果我们以 `mitchell` 的身份访问文件，情况会好一些，他是 `cs1` 组的成员。让我们尝试以 `mitchell` 的身份访问文件：

```
% id
uid=501 gid=501
```

我们可以列出文件内容并运行它（这是一个简单的脚本），但仍然无法写入它。如果我们以所有者（`samuel`）的身份运行，甚至可以覆盖文件：

```
% id
uid=502 gid=502
```

只有当你是文件的所有者（或超级用户）时才能更改与文件关联的权限。例如，如果你现在想允许所有人执行该文件，可以这样做：

```
% chmod o+x hello
% ls -l hello
-rw-r--x 1 samuel csl 3138 Jan 22 16:38 hello
```

注意第一个字符串末尾有一个 `x`。`o+x` 位意味着你想为其他人（不是文件所有者或其所属组的成员）添加执行权限。你可以使用 `g-w` 来移除组的写入权限。参见第 1 节主页有关此语法的详细信息：

通过编程，可以使用系统调用来查找与文件关联的权限。该函数接受两个参数：你想查询的文件名，以及一个填充了文件信息的数据结构的地址。参见附录 B，“低级 I/O”，第 B.2 节，“stat”，有关可以使用 `stat` 获取的其他信息的讨论。列表 10.2 显示了使用 `stat` 获取权限的示例。

### 列表 10.2 (stat-perm.c) 确定文件所有者的写入权限

```c
#include <stdio.h>
#include <sys/stat.h>

int main (int argc, char *argv[])
{
    const char* filename = argv[1];
    struct stat buf;

    /* 获取文件信息。 */
    stat(filename, &buf);
    /* 如果权限设置为文件所有者可以对该文件
     * 进行写入操作，则打印一条消息。 */
    if (buf.stat_mode & S_IWUSR) {
        printf("Owning user can write '%s.\n", filename);
    }
    return 0;
}
```

如果你在我们的 `hello` 程序上运行这个程序，它会输出：

```
% ./stat-perm hello
Owning user can write 'hello'.
```

`S_IWUSR` 常量对应所有者的写入权限。其他文件也有相应的常量。例如，`S_IRGRP` 是所有组的读取权限，而 `S_IXOTH` 是对不是所有者也不是所有组成员的用户执行权限。如果你将权限存储在变量中，请使用 `typedef mode_t` 来定义变量。与大多数系统调用一样，`stat` 将返回 -1，且 `errno` 无法获取有关文件的信息。

你可以使用 `chmod` 来更改现有文件的权限位。你调用 `chmod` 时，传入想要更改的文件名以及设置的权限位，这些权限位是通过前面提到的各种常量进行按位或运算得到的。例如，下面这行代码将使 `hello` 对所有者可读可执行，但禁用与 `hello` 关联的所有其他权限：

```
chmod ("hello", S_IRUSR, S_IXUSR);
```

相同的权限适用于目录，但它们的含义不同。如果允许用户读取目录，则允许用户查看该目录中存在的文件列表。如果允许用户写入目录，则允许用户在该目录中添加或删除文件。请注意，如果用户正在删除一个目录，她可以从该目录删除文件。如果允许用户写入目录，即使她没有修改该目录的权限也是允许的。如果允许用户执行目录，则允许用户进入该目录并访问其中的文件。如果无法访问某个目录，无论文件本身的权限如何设置，用户都不允许访问该目录中的文件。

- 总结一下，让我们回顾内核如何决定是否允许进程访问特定文件。它会检查访问的用户是否是所有者、所有组的成员还是其他人。访问用户所属的类别被用于确定检查哪一组读/写/执行位。内核会将正在执行的操作与适用于该用户的权限位进行比对。

如果其文件路径中的某个组件目录无法访问，内核也可能拒绝访问。例如，如果进程无法访问目录 `/tmp/private/`，那么它可能无法读取 `/tmp/private/data`，即使后者的权限被设置为允许访问。

有一个重要的例外：以 root 运行的进程（用户 ID 为 0 的进程）始终被允许访问任何文件，无论与其相关的权限如何。

### 10.3.1 安全漏洞：没有执行权限的程序

这是一个安全问题变得非常棘手的例子。你可能认为，如果禁止执行某个程序，就没有人能运行它。毕竟，这就是“禁止执行”的意思。但恶意用户可以创建该程序的副本，更改权限使其可执行，然后运行副本！如果你依赖于用户无法运行不可执行的程序，但随后没有阻止他们复制程序，你就拥有了一个安全漏洞——用户可以通过这种方式执行某些你无意让他们执行的操作。

### 10.3.2 粘滞位 (Sticky Bits)

除了读、写、执行程序外，还有一个称为粘滞位（sticky bit）的魔位。该位仅适用于目录。

设置了粘滞位的目录允许你在不是文件所有者的情况下删除该文件。正如之前提到的，通常如果你对目录有写入权限，就可以删除文件，即使你不是文件的所有者。当设置了粘滞位时，你仍然必须对目录有写入权限，但你必须是你想要删除的文件的所有者。

典型的 GNU/Linux 系统上的几个目录设置了粘滞位。例如，`/tmp`（任何用户都其中放置临时文件）设置了粘滞位。该目录专门设计供所有用户使用，因此该目录必须对所有人可写。如果一个用户可以删除另一个用户的文件将是糟糕，因此在该目录上设置了粘滞位。这样，只有所有者（当然还有 root）可以移除文件。

当你运行 `ls /tmp` 时，可以通过权限位末尾的 `t` 看到设置了粘滞位：

```
$ ls -ld /tmp root 2048 Jan 24 17:51 /tmp
```

如果你想使用 `stat` 创建行为类似于 `/tmp` 的目录（即许多人可以在那里放置东西，但不应该能删除他人的文件），你应该通过调用以下命令使用 `chmod` 命令对目录设置粘滞位：

```
$ chmod o+t directory
```

5 这个名字是过时的；它追溯到了一个设置粘滞位会导致程序在执行时保留在主内存中的时代。分配给程序的页面被“卡”在内存中。

## 10.4 真实 ID 和有效 ID

要通过程序设置粘滞位，请调用带有 `S_ISVTX` 标志的 `chmod`。例如，要将 `dir_path` 指定目录的粘滞位设置为与 `tmp` 相同，并赋予所有用户完全的读、写、执行权限，请使用：

```
chmod (dir_path, S_IRWX | S_IRWX0 | S_ISVTX);
```

到目前为止，我们讨论与进程相关的用户 ID 和组 ID 时，好像只有一个这样的用户 ID 和组 ID 一样。但实际上，并非如此。

每个进程有两个用户 ID：有效用户 ID（effective user ID）和真实用户 ID（real user ID）。用于更改进程用户 ID 的函数是 `setuid`。（当然，还有一个 `setgid` 函数。）该函数接受两个参数：第一个是所需的真实用户 ID；第二个是所需的有效 ID。例如，这里是您更改有效 ID 和真实 ID 的方法：

```
setuid(getuid());
```

显然，内核不会让任何进程随意更改其用户 ID。如果允许进程随意更改其有效 ID，那么任何用户都可以通过简单更改有效 ID 来轻松伪装任何其他用户。内核允许以有效 ID 为 0 运行的进程按其需要更改其用户 ID。（再次，注意以 root 运行的进程拥有多大的权力！有效 ID 为 0 的进程可以随心所欲。）然而，任何其他进程只能执行以下操作之一：

- 将其有效 ID 设置为与真实 ID 相同
- 将其真实 ID 设置为与有效 ID 相同
- 交换两个用户 ID

第一种方案用于我们的计数进程在以 `mitchell` 身份访问文件后想要返回 root 身份。第二种方案可以用于登录程序在将有效 ID 设置为登录用户 ID 之后。设置真实 ID 确保用户永远无法回到 root。

如果你想让该用户 ID 保持不变，可以向 `setuid` 的任何参数传递 `-1`。还有一个名为 `setuid` 的便利函数。该函数设置有效用户 ID，但不修改真实 ID。以下两个语句的作用完全相同：

```
setuid(id);
setuid(-1, id);
```

## 10.4.1 Setuid 程序

使用之前的技术，你知道如何让一个 root 进程临时伪装另一个进程并返回 root。你还知道如何通过设置其真实用户 ID 和有效用户 ID 来让 root 进程放弃所有特权。

这里有一个谜题：你能以非 root 用户的身份变成 root 吗？使用之前的技术这似乎是不可能的，但这里有证明它是可以行的：

```
% whoami
mitchell
% su
Password: ...
% whoami
root
```

`whoami` 命令就像 `id` 命令，区别在于它只显示有效用户 ID，而不显示所有其他信息。如果你知道 root 密码，`su` 命令可以让你变成超级用户（superuser）。

`su` 是如何工作的？因为我们最初运行时，其真实用户 ID 和有效用户 ID（EID）都被设置为 `mitchell`，内核不会允许我们更改其他用户 ID。

技巧在于 `su` 程序是一个 setuid 程序。这意味着当它运行时，进程的有效用户 ID 将是文件所有者的 ID，而不是执行 `exec` 调用的进程的有效 ID。（真实用户 ID 仍然是执行用户的 ID。）要创建一个 setuid 程序，你可以在命令行使用 `chmod +s`，或者在通过程序调用 `chmod` 时使用 `S_ISUID` 标志。

例如，考虑列表 10.3 中的 `setuid-test.c`。

### 列表 10.3 Setuid 演示

```c
#include <stdio.h>
#include <unistd.h>

int main () {
    printf("uid=%d eid=%d\n", (int) getuid(), (int) geteguid());
    return 0;
}
```

现在假设该程序被设置为 setuid 并且由 root 所有。在这种情况下，`ls` 的输出将是这样的：

```
-rwsr----x 1 root  root  11931 Jan 24 18:25 setuid-test
```

`s` 位表示该文件不仅是可执行的（正如 `x` 位所示的那样），而且还设置了 setuid 和 setgid。当我们使用这个程序时，会得到像这样的输出：

```
% whoami
mitchell
./setuid-test
uid=501 eid=0
```

- 6. 当然，还有一个类似的概念是 setgid 程序。运行时，它的有效组 ID 与文件组所有者的组 ID 相同。大多数 setuid 程序也是 setgid 程序。

## 10.4.2 第 10 章 安全

注意，当程序运行时，有效用户 ID 被设置为 0。

你可以使用 `chmod` 命令配合 `u+s` 或 `g+s` 参数来分别为可执行文件设置 setuid 和 setgid 位，例如：

```
% ls -l program
-rwxr-xr-x 1 samuel  csl      @ Jan 30 23:38 program
% chmod g+s program
% ls -l program
-rwxr-sr-x 1 samuel  csl      @ Jan 30 23:38 program
% chmod u+s program
% ls -l program
-rwsrxr-x 1 samuel  csl      @ Jan 30 23:38 program
```

你也可以使用带有 `S_ISUID` 或 `S_ISGID` 模式标志的 `chmod` 调用。`su` 能够通过这种机制更改有效用户 ID 吗？它初始运行有效用户 ID 为 0。然后它提示你输入密码。如果密码与 root 密码匹配，它会将真实用户 ID 也设置为 root 并启动一个新的 shell。否则，它会毫不留情地让你留在非特权用户。

看看 `su` 程序的权限：

```
% ls -l /bin/su
-rwxr-xr-x 1 root      14188 Mar 7 2000 /bin/su
```

注意，它由 root 所有，并且设置了 setuid 位。

> 注意，它实际上并没有改变运行它的 shell 的用户 ID。相反，它会以新的用户 ID 启动一个新的 shell 进程。原始的 shell 会被阻塞，直到新的 shell 完成且 `su` 退出。

## 10.5 用户验证

通常，如果你有一个 setuid 程序，你可能不想向所有人提供它的服务。例如，`su` 程序只有在你知道 root 密码时才让你变成 root。你制作的程序在执行操作之前，会证明你有权变成 root。这个过程被称为身份验证（authentication）——`su` 程序正在检查你的身份是否真实。

如果你正在管理一个非常安全的系统，你可能不想让人们通过输入普通密码来登录。用户倾向于写下密码，而黑客可能会涉及他们的生日、宠物的名字等。密码并不总是安全的。

- 7. 发现系统管理员选择 `god` 作为密码的频率比任何其他密码都高。（随你怎么想。）所以，如果你确实需要某台机器的 root 权限，而系统管理员不在，一点神圣的启迪可能正是你需要的。

例如，许多组织现在要求使用特殊的“一次性”密码，这些密码由用户随身携带的特殊身份卡生成。同一个密码不能使用两次，如果不输入 PIN 码就无法从身份卡中获得有效密码。因此，攻击者必须同时获得实体卡和 PIN 码。

### 列表 10.4 (pam.c)

```c
#include <stdio.h>
#include <security/app.h>
#include <security/pam_misc.h>

int main () {
    pam_handle_t *pamic;
    struct pam_conv pamc;
    
    /* 设置 PAM 对话。 */
    pamc.conv = &init_get_conv;
    pamc.appdata_ptr = NULL;
    
    /* 启动新会话。 */
    pamic = pam_start("su", "USER", &pamc, NULL);
    
    /* 验证用户。 */
    if (pam_authenticate(pamic, 0) != PAM_SUCCESS) {
        fprintf(stderr, "验证失败!\n");
    } else {
        fprintf(stderr, "验证通过。\n");
    }
    
    /* 全部完成。 */
    pam_end(pamic, 0);
    
    return 0;
}
```

要编译此程序，你必须链接两个库：`libpam` 库和一个名为 `libpam_misc` 的辅助库。

```
% gcc -o pam pam.c -lpam -lpam_misc
```



## 10.6 更多安全漏洞

这里涵盖的基础知识对于大多数简单程序已经足够了。关于 PAM 如何工作的完整文档可以在大多数 GNU/Linux 系统的 `/usr/doc/pam` 目录下找到。

虽然本章将指出几个常见的安全漏洞，但你绝不能依赖本书涵盖所有可能的安全漏洞。已经有大量的漏洞被发现，还有更多在等待被发现。如果你正试图编写安全代码，那么没有什么比让安全专家审计你的代码更可靠了。

### 10.6.1 缓冲区溢出

几乎每一个 Internet 守护进程，包括 `sendmail` 守护进程、`finger` 守护进程，都曾在某一个时刻通过缓冲区溢出被攻破。

如果你正在编写任何可能以 `root` 身份运行的代码，你绝对必须意识到这种特定的安全漏洞。如果你正在编写执行任何类型进程间通信的程序，如果你正在编写一个读取（或可能读取）不属于执行程序的用户的文件的程序，你应该意识到这种安全漏洞。最后一条标准适用于几乎所有程序。从根本上说，如果你打算编写 GNU/Linux 软件，你就应该了解缓冲区溢出。

缓冲区溢出攻击背后的思想是欺骗程序执行它本意不想执行的代码。实现这一壮举的通常机制是覆盖程序栈的某些部分。程序的栈包含许多内容，例如内存、当当前函数返回时程序将转移控制权的位置。因此，如果你可以将你想要执行的代码放在某处，然后将返回地址更改指向该内存，你就可以导致程序执行任何内容。当程序从它正在执行的函数返回时，它将跳转到新代码并执行它正在运行的任何内容，且具有当前进程的权限。显然，如果进程是以 `root` 或另一个用户运行的，那么对于该用户来说就是一场“灾难”，对于任何其他依赖于该用户拥的文件内容的人等等也是如此。

如果程序作为守护进程运行并监听传入的网络连接，情况会更加糟糕。守护进程通常以 `root` 身份运行。如果它包含缓冲区溢出漏洞，任何可以通过网络连接到运行该守护进程计算机的人都可以通过向守护进程发送恶性数据序列来获取计算机的控制。不参与网络通信的程序要安全得多，因为只有已经准备好登录运行程序的计算机的用户才能对其进行攻击。

`finger`、`talk` 和 `sendmail` 的这些漏洞版本都有一个共同缺陷。它们都使用一个固定长度的字符串缓冲区，这意味着字符串的大小有一个恒定的上限，但随后允许恶意的网络客户端提供溢出缓冲区的字符串。例如，它们包含类似下面的代码：

```c
#include <stdio.h>

int main () {

    /* 任何头脑正常的人都不会让其用户名超过 32 个字符。此外，我认为 UNIX 只允许 8 个字符的用户名。所以，这个空间足够了。 */

    char username[32];

    /* 提示用户输入用户名。 */

    printf("Enter your username: ");

    /* 读取一行输入。 */

    gets(username);

    /* 在此处执行其他操作... */

    return 0;

}
```

32 字符的缓冲区与 `gets` 函数的结合允许缓冲区溢出。`gets` 函数读取输入直到下一个换行符为止，并将整个结果存储在 `username` 缓冲区中。代码中的注释是正确的，因为人们的用户名通常很短，所以没有好意的用户可能会输入超过 32 个字符。但当你编写安全软件时，你必须考虑恶意攻击者可能会做什么。在这种情况下，攻击者可能会故意输入一个非常长的用户名。本地变量（如 `username`）存储在栈上，因此通过超过数组边界，可能会放入任意字节。当程序从它执行的函数返回时，它将跳转到新代码并以当前进程的权限执行它正在运行的任何内容。显然，如果进程是以 `root` 或另一个用户运行的，对于该用户来说就是一场“灾难”，对于任何其他依赖于该用户拥的文件内容的人等等也是如此。

如果程序作为守护进程运行并监听传入的网络连接，情况更加糟糕。守护进程通常以 `root` 身份运行。如果它包含缓冲区溢出，任何可以通过网络连接到运行该守护进程计算机的人都可以通过向守护进程发送恶性数据序列来获取计算机的控制。不参与网络通信的程序要安全得多，因为只有已经准备好登录运行程序的用户才能对其进行攻击。

`finger`、`talk` 和 `sendmail` 的版本共同缺陷。它们都使用一个固定长度的字符串缓冲区，这意味着字符串的大小有一个恒定的上限，但随后允许恶意的网络客户端提供溢出缓冲区的字符串。例如，它们包含类似下面的代码：

```c
#include <stdio.h>

int main () {

    /* 任何头脑正常的人都不会让其用户名超过 32 个字符。此外，我认为 UNIX 只允许 8 个字符的用户名。所以，这个空间足够了。 */

    char username[32];

    /* 提示用户输入用户名。 */

    printf("Enter your username: ");

    /* 读取一行输入。 */

    gets(username);

    /* 在此处执行其他操作... */

    return 0;

}
```

32 字符的缓冲区与 `gets` 函数的结合允许缓冲区溢出。`gets` 函数读取输入直到下一个换行符为止，并将整个结果存储在 `username` 缓冲区中。代码中的注释是正确的，因为人们的用户名通常很短，所以没有好意的用户可能会输入超过 32 个字符。但当你编写安全软件时，你必须考虑恶意攻击者可能会做什么。在这种情况下，攻击者可能会故意输入一个非常长的用户名。本地变量（如 `username`）存储在栈上，因此通过超过数组边界，可能会放入任意字节。当程序从它执行的函数返回时，它将跳转到新代码并执行它正在运行的任何内容，且具有当前进程的权限。显然，如果进程是以 `root` 或另一个用户运行的，那么对于该用户来说就是一场“灾难”，对于任何其他依赖于该用户拥的文件内容的人等等也是如此。

如果程序作为守护进程运行并监听传入的网络连接，情况更加糟糕。守护进程通常以 `root` 身份运行。如果它包含缓冲区溢出，任何可以通过网络连接到运行该守护进程计算机的人都可以通过向守护进程发送恶性数据序列来获取计算机的控制。不参与网络通信的程序要安全得多，因为只有已经准备好登录运行程序的用户才能对其进行攻击。

`finger`、`talk` 和 `sendmail` 的这些版本共同缺陷。它们都使用一个固定长度的字符串缓冲区，这意味着字符串的大小有一个恒定的上限，但随后允许恶意的网络客户端提供溢出缓冲区的字符串。例如，它们包含类似下面的代码：

```c
#include <stdio.h>

int main () {

    /* 任何头脑正常的人都不会让其用户名超过 32 个字符。此外，我认为 UNIX 只允许 8 个字符的用户名。所以，这个空间足够了。 */

    char username[32];

    /* 提示用户输入用户名。 */

    printf("Enter your username: ");

    /* 读取一行输入。 */

    gets(username);

    /* 在此处执行其他操作... */

    return 0;

}
```

32 字符的缓冲区与 `gets` 函数的结合允许缓冲区溢出。`gets` 函数读取输入直到下一个换行符为止，并将整个结果存储在 `username` 缓冲区中。代码中的注释是正确的，因为人们的用户名通常很短，所以没有好意的用户可能会输入超过 32 个字符。但当你编写安全软件时，你必须考虑恶意攻击者可能会做什么。在这种情况下，攻击者可能会故意输入一个非常长的用户名。本地变量（如 `username`）存储在栈上，因此通过超过数组边界，可能会放入任意字节。当程序从它执行的函数返回时，它将跳转到新代码并执行它正在运行的任何内容，且具有当前进程的权限。显然，如果进程是以 `root` 或另一个用户运行的，那么对于该用户来说就是一场“灾难”，对于任何其他依赖于该用户拥的文件内容的人等等也是如此。

### 10.6.2 /tmp 中的竞态条件

另一个非常常见的问题涉及在 `/tmp` 目录下创建文件。假设你的程序以 `root` 身份运行，总是创建一个文件，恶意用户可以将 `/tmp/prog` 指向系统上的任何其他文件。当你的程序去创建文件时，`open` 系统调用将成功。相反，它将被写入攻击者选择的任意文件。

这种攻击被认为利用了竞态条件。你和攻击者之间隐含着一个竞态关系。先创建文件的人获胜。

这种攻击通过创建适当的链接来破坏系统的重要部分，例如通过创建一个指向 `/etc/passwd` 的符号链接，攻击者可以删除你的系统密码数据库。恶意用户还可以可以通过这种系统获取 `root` 权限。

对这种设备的一种尝试是使用随机化的文件名。例如，你可以从 `/dev/random` 读取一些位到文件的名字中。这使得恶意用户猜到文件名变得困难，但不能使其不可能。即使她必须尝试 10,000 次才能在竞态条件中获胜，也可能是灾难性的。

另一种方法是在调用 `open` 时使用 `O_EXCL` 标志。该标志会在文件已存在时打开失败。不幸的是，如果你正在使用网络文件系统 (NFS)，或者任何使用你程序的人可能使用 NFS，这不是一个足够稳健的方法，因为 `O_EXCL` 在使用 NFS 时不可靠。你无法确定你的代码是否运行在使用 NFS 的系统上，所以如果你非常担心，不要使用 `O_EXCL`。

在第 2 章“编写 GNU/Linux 软件”第 2.1.7 节“使用临时文件”中，我们展示了如何使用 `mktemp` 创建临时文件。

不幸的是，Linux上的 `mktemp` 在尝试一个难以获取的名字后使用 `O_EXCL` 打开。换句话说，如果 `/tmp` 挂载了 NFS，`mktemp` 就是不。因此，使用 `mktemp` 比没有好，但它并不完全安全。

- 有些程序员认为 C++ 是一种糟糕且过度复杂的语言。关于多继承和其他复杂性的争论有一定的道理，但在 C++ 中编写避免缓冲区溢出和其他问题的代码比在 C 中更容易。
- 显然，如果你也是系统管理员，你不应该将 `/tmp` 挂载到 NFS 上。

## 第 10 章 安全

列表 10.5 展示了一个尝试在 `/tmp/` 中安全地打开文件的函数。本书的作者没有对其进行过专业的审计，我们也不是专业的安全专家，因此它很可能也存在漏洞。我们不建议您在没有经过审计的情况下使用这段代码，但它会让你相信编写安全代码是一件棘手的事情。为了起到威慑作用，我们让该接口在实际程序中变得难以使用。错误检查是编写安全软件的重要部分，因此我们在示例中包含了错误检查逻辑。

### 列表 10.5 (temp-file.c) 创建临时文件

```c
#include <fcntl.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <unistd.h>
```

```c
/* 返回新创建的临时文件的描述符。
* 临时文件将允许当前进程的有效
* 用户读取和写入，但其他人将无法
* 读取或写入。
* 如果无法创建临时文件，则返回 -1。 */

int secure_temp_file()
{
    /* 此文件描述符指向 /dev/random，允许我们获取
    * 良好的随机位源。 */

    static int random_fd = -1;

    /* 一个随机整数。 */

    unsigned int random;

    /* 一个缓冲区，用于将数字转换为随机数的
    * 字符串表示。此缓冲区大小固定，意味着
    * 如果此机器上的整数具有“很多”位，
    * 我们可能存在缓冲区溢出漏洞。 */

    char *filename[128];

    /* 新临时文件的文件描述符。 */

    int fd;

    /* 关于新创建文件的信息。 */

    struct stat stat_buf;

    /* 如果我们还没有打开 /dev/random，现在打开。（这
    * 不是线程安全的。） */

    if (random_fd == -1) {
        /* 打开 /dev/random。注意，我们假设 /dev/random
        *确实是一个随机位源，而不是攻击者放置
        * 在那里的全零文件。 */

        random_fd = open("/dev/random", O_RDONLY);

        /* 如果无法打开 /dev/random，则放弃。 */

        if (random_fd == -1)
            return -1;

        /* 从 /dev/random 读取一个整数。 */

        if (read(random_fd, &random, sizeof(random)) != 
            sizeof(random))
            return -1;

        /* 根据随机数生成文件名。 */

        sprintf(filename, "/tmp/%u", random);

        /* 尝试打开文件。 */

        fd = open(filename,
            /* 使用 O_EXCL，即使它在 NFS 上不起作用。 */
            O_RDWR | O_CREAT | O_EXCL,
            /* 确保没有其他人可以读取或写入该文件。 */
            S_IRUSR | S_IWUSR);

        if (fd == -1)
            return -1;

        /* 对文件调用 lstat，确保它不是一个符号
        * 链接。 */

        if (lstat(filename, &stat_buf) == -1)
            return -1;

        /* 如果文件不是普通文件，说明有人试图欺骗
        * 我们。 */

        if (!S_ISREG(stat_buf.st_mode))
            return -1;

        /* 如果我们不是该文件的所有者，其他人可能
        * 在我们查看时删除它、读取或更改它。 */

        if (stat_buf.st_uid != getuid() || stat_buf.st_gid != getegid())
            return -1;

        /* 如果文件上设置了任何权限位，
        * 事情就很可疑。 */

        if ((stat_buf.st_mode & (S_IRUSR | S_IWUSR)) != 0)
            return -1;

        return fd;
    }
}
```

此函数调用 `open` 来创建文件，并在几行后调用 `lstat` 以确保该文件不是符号链接。如果你仔细思考，你会发现在这一点似乎存在竞态条件。特别地，攻击者可以在我们打开文件和调用 `lstat` 之间删除该文件并将其替换为符号链接。这不会伤害我们，因为我们已经拥有了指向新创建文件的打开文件描述符，但它会导致我们向调用者报告错误。这种攻击不会产生任何直接伤害，但它让操作无法完成。

### 10.3 在 popen 中使用 system

你担心的第三种常见方法涉及 shell。作为一个玩具示例，让我们考虑

列表 10.6 (grep-dictionary.c) 在字典中查找单词

```c
#include <stdio.h>
#include <stdlib.h>

/* 仅当单词出现时，返回非零值。
. . */

int grep_for_word(const char* word)
{
    size_t length;

    char* buffer;

    int exit_code;

    /* 构建字符串 grep -x。为了防止缓冲区溢出： */

     length = strlen("grep -x ") + strlen(word) + 11;

     buffer = (char*)malloc(length);

        sprintf(buffer, "grep -x %s /dev/null", word);

/* 运行命令。 */

    exit_code = system(buffer);

    /* 释放缓冲区。 */

    free(buffer);

    /* 如果 get 返回 0，则单词存在于字典中。 */

    return exit_code == 0;
}
```

注意，通过计算所需的字符数量然后动态分配字符串来避免缓冲区溢出。10.6 显示了你可能会执行：

```
grep -x
```



在这种情况下，服务器将执行此命令：

```
grep -x foo /dev/null; rm -rf /
```

现在问题显而易见了。用户将一个命令（表面上调用 `grep`）变成了两个命令，因为 `shell` 将分号视为命令分隔符。第一个命令仍然是无害的 `grep` 调用，但第二个命令删除了整个系统上的文件！即使服务器不是以 `root` 身份运行，运行服务器的用户可以删除的所有文件都会被删除。

有两种方法避免这些问题。使用 `exec` 系列函数代替 `system` 或 `popen`。这种解决方案解决了问题，因为 `shell` 特殊处理的字符（例如之前命令中的分号）在 `exec` 调用的参数列表中出现时不会被特殊处理。当然，你放弃了 `system` 和 `popen` 的便利性。

另一种方案是验证字符串以确保它是无害的。在字典服务器示例中，你会确保提供的单词仅包含字母，使用 `isalpha` 函数。如果它不包含任何其他字符，就没有办法欺骗 `shell` 执行第二个命令。不要通过寻找危险和意外的字符来实现检查；显式检查你已知是安全的字符总是比预测所有可能引起问题的字符更安全。

# 11 示例 GNU/Linux 应用程序

本章是所有内容的汇聚点。我们将描述并实现一个完整的 `GNU/Linux` 程序，该程序整合了书中描述的许多技术。该程序通过 Web 接口提供其运行所在的系统信息。

该程序是我们之前描述的 `GNU/Linux` 编程方法以及在短程序中演示的某些方法的完整演示。此程序的编写方式更接近“真实世界”中的代码，与我们在前面章节中展示的大多数代码列表不同。它可以作为你编写自己的 `GNU/Linux` 程序的起点。

## 11.1 概述

示例程序是一个监控运行中的 `GNU/Linux` 系统的一部分。它包含以下特性：

- 程序集成了一个极简的 Web 服务器。本地或远程客户端通过通过 `HTTP` 向服务器请求 Web 页面来访问系统信息。
- 程序不提供静态 `HTML` 页面。相反，页面由模块动态生成，每个模块提供一个总结系统状态某个方面的页面。
- 模块没有静态链接到服务器的可执行文件。相反，它们从共享库中动态加载。在服务器运行时，可以添加、删除或替换模块。
- 服务器在子进程中处理每个连接。这使得服务器即使在单个请求需要较长时间完成时也能保持响应，并保护服务器不受模块故障的影响。
- 服务器运行不需要超级用户权限（只要它不在特权端口上）。然而，这限制了它可以收集的系统信息。

我们提供了四个示例模块，演示了如何编写这些模块。它们进一步说明了书中之前介绍的一些收集系统信息的技术。`time` 模块演示了使用 `gettimeofday` 系统调用。`issue` 模块演示了低级 `I/O` 和 `sendfile` 系统调用。`diskfree` 模块通过在子进程中运行命令演示了 `fork`、`exec` 和 `dup2` 的使用。`processes` 模块演示了 `/proc` 文件系统和各种系统调用的使用。

### 11.1.1 注意事项

该程序包含了应用程序中许多特性，例如命令行解析和错误检查。同时，我们进行了一些简化以提高可读性，并专注于书中讨论的 `GNU/Linux` 特有主题。在检查代码时请记住这些注意事项。

- 我们没有尝试提供完整的 `HTTP` 实现。相反，我们只实现了让服务器与 Web 客户端交互所需的。真实的程序会提供更完整的 `HTTP` 实现，或者与各种优秀的 Web 服务器实现之一建立接口，而不是直接提供 `HTTP` 服务。
- 同样，我们的目标并不是完全符合 `HTML` 规范（参见 `http://www.w3.org/Markup/`）。我们生成可以被 Web 浏览器处理的简单 `HTML` 输出。
- 服务器没有针对高性能或最小资源消耗进行优化。特别是，我们刻意忽略了一些你在 Web 服务器中会预期的网络配置代码。此主题超出了本书的范围。更多信息，请参阅网络应用开发的许多优秀参考文献之一，例如 `W. Richard Stevens` 编写的《`UNIX Network Programming, Volume 1: Networking APIs—Sockets and XTI`》（`Prentice Hall`, 1997）。
1. `GNU/Linux` 最受欢迎的开源 Web 服务器是 `Apache`，可以从 `http://www.apache.org` 获取。
- 我们没有尝试限制服务器或其模块消耗的资源（进程数、内存使用等）。许多多进程 Web 实现使用固定的进程池来处理连接，而不是为每个连接创建一个新的子进程。
- 服务器在每次被请求时加载服务器模块的共享库，并在请求完成后立即卸载它。更高效的实现可能会缓存已加载的模块。

## HTTP

超文本传输协议（`HTTP`）用于 Web 客户端和服务器之间的通信。客户端通过连接到已知端口与服务器建立连接（通常互联网 Web 服务器使用 `80` 端口，但可以使用任何端口）。`HTTP` 请求和标头由纯文本组成。一旦连接，客户端就会向服务器发送请求。一个典型的请求是 `GET /page HTTP/1.0`。`GET` 方法表示客户端请求服务器向其发送 Web 页面。第二个元素是服务器的路径。第三个元素是协议和版本。后续行包含标头字段，格式与邮件头部类似，包含了关于客户端的额外信息。标头有一个空行。

服务器发送响应以指示处理请求的结果。一个典型的响应是 `HTTP/1.0 200 OK`。第一个元素是协议版本。接两个元素指示结果；在这种情况下，`200` 表示请求已成功处理。后续行包含标头字段，格式与邮件头部类似。标头以空行结束。服务器随后可以发送任意数据以满足请求。

通常，服务器通过返回 Web 页面的 `HTML` 源码来响应页面请求。在这种情况下，响应头将包含 `Content-type: text/html`，表示结果是 `HTML` 源码。`HTML` 源码紧随标头之后。

更多信息请参见 `http://www.w3.org/Protocols/` 上的 `HTTP` 规范。

## 11.2 实现

除了极小的程序外，所有用 `C` 编写的程序都需要仔细组织以保留源代码的模块化可维护性。该程序分为四个主要的源文件。

每个源文件导出程序其他部分可以调用的函数或变量。为了简单起见，所有导出的函数和变量都声明在一个头文件 `server.h` 中（参见列表 11.1），该文件被其他文件包含。供单个编译单元内使用的函数声明为 `static` 且不在 `server.h` 中声明。

列表 11.1 (`server.h`) 函数和变量声明

```c
#ifndef SERVER_H

#define SERVER_H

#include <netinet/in.h>

#include <sys/types.h>

/****************************************************************/

/* 程序名称。 */

extern const char* program_name;

/* 如果非零则打印详细信息。 */

extern int verbose;

/* 类似于 malloc，如果分配失败则终止程序。 */

extern void* xmalloc(size_t size);

/* 类似于 realloc，但分配失败则终止程序。 */

extern void* xalloc(void* ptr, size_t size);

/* 类似于 strdup，但分配失败则终止程序。 */

extern char* xstrdup(const char* s);

/* 为失败的调用打印错误信息，使用 errno 的值和程序。 */

extern void system_error(const char* operation);

/* 为涉及原因的失败打印错误信息，包括描述性消息并结束程序。 */

extern void error(const char* cause, const char* message);

/* 返回运行程序的可执行文件所在的目录。

这是一个内存缓冲区，调用者必须使用 free 释放。

此函数在失败时会调用 abort。 */

extern char* get_self_executable_directory();

/****************************************************************/

/* 加载的服务器模块的实例。 */

struct server_module {

    /* 对应加载模块的共享库句柄。 */

    void* handle;

    /* 描述模块的名称。 */

    const char* name;

    /* 生成该模块 HTML 结果的函数。 */

    void (*generate_function)(int);

};

/* 加载模块的目录。 */

extern char* module_dir;

/* 尝试加载名为 MODULE_PATH 的服务器模块。如果存在
该路径的服务器模块，则加载该模块并返回一个表示该模块的 server_module 结构体。否则，返回 NULL。 */

extern struct server_module* module_open (const char* module_path);

/* 关闭服务器模块并释放 MODULE 对象。 */

extern void module_close (struct server_module* module);

/*** 在 server.c 中定义的符号。 *************************************** */

/* 在 LOCAL_ADDRESS 和 PORT 上运行服务器。 */

extern void server_run (struct in_addr local_address, uint16_t port);

#endif /* SERVER_H */
```

### 11.2.1 通用函数

`common.c`（参见列表 11.2）包含了贯穿整个程序使用的通用工具函数。

列表 11.2 (`common.c`) 通用工具函数

```c
#include <errno.h>

#include <stdio.h>

#include <stdlib.h>

#include <string.h>

#include <unistd.h>

#include "server.h"

const char* program_name;

int verbose;

void* xmalloc(size_t size)

{

  void* ptr = malloc(size);

  /* 如果分配失败，则终止。 */

  if (ptr == NULL)

    abort();

  else

    return ptr;

}

void* xrealloc(void* ptr, size_t size)

{

    ptr = realloc(ptr, size);

    /* 如果分配失败，则终止。 */

    if (ptr == NULL)

        abort();

    else

        return ptr;

}

char* xstrdup(const char* s)

{

    char* copy = strdup(s);

    /* 如果分配失败，则终止。 */

    if (copy == NULL)

        abort();

    else

        return copy;

}

void system_error(const char* cause, const char* operation)

{

    /* 为 errno 生成错误消息。 */

    error(operation, strerror(errno));

}

void error(const char* cause, const char* message)

{

    /* 将错误消息打印到 stderr。 */

    fprintf(stderr, "%s: error: %s\n", program_name, cause, message);

    /* 退出程序。 */

    exit(1);

}

char* get_self_executable_directory ()

{

    int rval;

    char link_target[1024];

    char* last_slash;

    size_t result_length;

    char* result;

    /* 读取符号链接 /proc/self/exe 的目标。 */

    rval = readlink("/proc/self/exe", link_target, sizeof (link_target));

    if (rval == -1)

        /* readlink 调用失败，所以退出。 */

        abort();

    else {

        /* 目标进行 NUL 终止。 */

        link_target[rval] = '\0';

        /* 我们想修掉可执行文件的文件名，以获取
        包含它的目录。找到最右边的斜杠。 */

        last_slash = strchr(link_target, '/');

        if (last_slash == NULL || last_slash == link_target)

            /* 发生了一些异常。 */

            return NULL;

        /* 分配一个缓冲区来存放结果路径。 */

        result_length = last_slash - link_target;

        result = (char*) xmalloc(result_length + 1);

        /* 拷贝结果。 */

        strncpy(result, link_target, result_length);

        result[result_length] = '\0';

        return result;

    }

}
```

你也可以在程序中使用这些函数；此文件的内容可能会被包含在多个项目共享的公共库中：

- `get_executable_directory` 返回当前进程中运行的可执行文件所在的目录。该目录路径可以用于定位程序的其他组件，这些组件在运行时被安装在相同的位置。该函数通过检查 `/proc` 文件系统中的符号链接 `/proc/self/exe` 来工作（参见第 7 章“`/proc` 文件系统”中的第 7.2.1 节，“`/proc/self`”）。

此外，`common.c` 定义了两个实用的全局变量：

- `program_name` 的值是正在运行的程序名称，如其参数列表中指定的（参见第 2 章中的第 2.1.1 节，“参数列表”）。当程序通过 `shell` 调用时，这是用户输入的程序路径和名称。
- 如果变量 `verbose` 不为零，则表示程序以详细模式（`verbose mode`）运行。在这种情况下，程序的各个部分会向 `stdout` 打印进度消息。

### 11.2.2 加载服务器模块

`module.c`（参见列表 11.3）提供了动态加载服务器模块的实现。加载的服务器模块由 `server_module` 实例表示，该结构体定义在 `server.h` 中。

列表 11.3 (`module.c`) 服务器的加载与卸载

```c
#include <dlfcn.h>

#include <stdlib.h>

#include <stdio.h>

#include <string.h>

#include "server.h"

char* module_dir;

struct server_module* module_open (const char* module_name)

{

    char* module_path;

    void* handle;

    struct server_module* module;

    /* 构建要加载的模块完整路径。 */

    module_path = (char*)malloc(strlen(module_dir) + strlen(module_name) + 2);

    sprintf(module_path, "%s/%s", module_dir, module_name);

    /* 尝试打开共享库。 */

    handle = dlopen(module_path, RTLD_NOW);

    if (handle == NULL) { /* 打开共享库失败。 */

        free(module_path);

        return NULL;

    }

    /* 从共享库中解析符号。 */

    module_generate = (void (*) (int))dlsym(handle, "module_generate");

    if (module_generate == NULL) /* 符号缺失。 */

        dlclose(handle);

        free(module_path);

        return NULL;

    }

    /* 分配并初始化模块对象。 */

    module = (struct server_module*)malloc(sizeof(struct server_module));

    module->handle = handle;

    module->name = strdup(module_name);

    module->generate = module_generate;
```



### 11.2.3 服务器

`server.c`（参见列表 11.4）是最小 HTTP 服务器的实现。

**列表 11.4** (`server.c`) 实现

```c
#include <arpa/inet.h>
#include <assert.h>
#include <errno.h>
#include <netinet/in.h>
#include <signal.h>
#include <stdio.h>
#include <string.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <sys/wait.h>
#include <unistd.h>
#include "server.h"

/* 成功请求的 HTTP 响应和头部。 */
static char* ok_response =
  "HTTP/1.0 200 OK\n"
  "Content-type: text/html\n"
  "\n";

/* HTTP 响应、头部和正文，表示我们未理解请求。 */
static char* bad_response =
  "HTTP/1.0 400 Bad Request\n"
  "Content-type: text/html\n"
  "\n"
  "<html>\n"
  "<body>\n"
  "<h1>Bad Request</h1>\n"
  "<p>This server did not understand your request.</p>\n"
  "</body>\n"
  "</html>\n";

/* HTTP 响应、头部和正文模板，表示未找到请求的文档。 */
static char* not_found_response_template =
  "HTTP/1.0 404 Not Found\n"
  "Content-type: text/html\n"
  "\n"
  "<html>\n"
  "<body>\n"
  "<h1>Not Found</h1>\n"
  "<p>The requested URL %s was not found on this server.</p>\n"
  "</body>\n"
  "</html>\n";

/* HTTP 响应、头部和正文模板，表示方法未被理解。 */
static char* bad_method_response_template =
  "HTTP/1.0 Method Not Implemented\n"
  "Content-type: text/html\n"
  "<html>\n"
  "<body>\n"
  "<h1>Method Not Implemented</h1>\n"
  "<p>The method %s is not implemented by this server.</p>\n"
  "</body>\n"
  "</html>\n";

/* SIGCHLD 处理器，用于清理已终止的子进程。 */
static void clean_up_child_process(int signal_number)
{
  int status;
  wait(&status);
}

/* 处理针对 PAGE 的 HTTP "GET" 请求，并将结果发送到文件描述符 CONNECTION_FD。 */
static void handle_get(int connection_fd, const char* page)
{
  struct server_module* module = NULL;

  /* 确保请求的页面以斜杠开头且不包含任何额外的斜杠——我们不支持任何子目录。 */
  if (page[0] == '/' && strchr(page + 1, '/') == NULL) {
    char module_file_name[64];

    /* 页面名称看起来没问题。通过在页面名后附加 .so 来构造模块名。 */
    sprintf(module_file_name, sizeof(module_file_name), "%s.so", page + 1);

    /* 尝试打开模块。 */
    module = module_open(module_file_name);

    if (module == NULL) {
      /* 或者请求的页面格式不正确，或者我们无法打开带有指定名称的模块。无论何种，返回 HTTP 响应 404, Not Found。 */
      char response[1024];

      /* 生成响应消息。 */
      sprintf(response, sizeof(response), not_found_response_template, page);

      /* 发送给客户端。 */
      write(connection_fd, response, strlen(response));
    } else {
      /* 模块加载成功。 */
      /* 发送表示成功的 HTTP 响应以及 HTML 页面的 HTTP 头部。 */
      write(connection_fd, ok_response, strlen(ok_response));

      /* 调用模块，它将生成 HTML 输出并发送到客户端文件描述符。 */
      (module->generate_function)(connection_fd);

      /* 我们处理完毕模块。 */
      module_close(module);
    }
  }
}

/* 处理文件描述符 CONNECTION_FD 上的客户端连接。 */
static void handle_connection(int connection_fd)
{
  char buffer[256];
  size_t bytes_read;

  /* 从客户端读取一些数据。 */
  bytes_read = read(connection_fd, buffer, sizeof(buffer) - 1);

  if (bytes_read > 0) {
    char method[sizeof(buffer)];
    char url[sizeof(buffer)];
    char protocol[sizeof(buffer)];

    /* 成功读取了某些数据。对缓冲区进行 NUL 终止，以便我们可以对其进行字符串操作。 */
    buffer[bytes_read] = '\0';

    /* 客户端发送的第一行是 HTTP 请求，它由方法、请求的页面以及协议版本组成。 */
    sscanf(buffer, "%s %s %s", method, url, protocol);

    /* 客户端可能会在请求之后发送各种头部信息。在此实现中，我们不关心这些信息。但是，我们需要读取客户端尝试发送的任何数据。继续读取数据，直到到达头部的结尾，头部由一个空行分隔。HTTP 规定 CR/LF 为行分隔符。 */
    while (strchr(buffer, "\r\n\r\n") == NULL) {
      bytes_read = read(connection_fd, buffer, sizeof(buffer));

      /* 确保最后一次读取没有失败。如果失败了，说明连接存在问题——所以放弃。 */
      if (bytes_read == -1) {
        close(connection_fd);
        return;
      }
    }
  }
}

void server_run(struct in_addr local_address, uint16_t port)
{
  struct sockaddr_in socket_address;
  int rval;
  struct sigaction sigchild_action;
  int server_socket;

  /* 安装 SIGCHLD 处理器，以清理已终止的子进程。 */
  memset(&sigchild_action, 0, sizeof(sigchild_action));
  sigchild_action.sa_handler = &clean_up_child_process;
  sigaction(SIGCHLD, &sigchild_action, NULL);

  /* 创建一个 TCP 套接字。 */
  server_socket = socket(PF_INET, SOCK_STREAM, 0);
  if (server_socket == -1) {
    system_error("socket");
  }

  /* 为想要监听连接的本地地址构造一个套接字地址。 */
  memset(&socket_address, 0, sizeof(socket_address));
  socket_address.sin_family = AF_INET;
  socket_address.sin_port = port;
  socket_address.sin_addr = local_address;

  /* 将套接字绑定到该地址。 */
  rval = bind(server_socket, &socket_address, sizeof(socket_address));
  if (rval != 0) {
    system_error("bind");
  }

  /* 指令套接字接受连接。 */
  rval = listen(server_socket, 10);
  if (rval != 0) {
    system_error("listen");
  }

  if (verbose) {
    /* 在详细模式下，显示我们监听的本地地址和端口号。 */
    socklen_t address_length;

    /* 查找套接字的本地地址。 */
    address_length = sizeof(socket_address);
    rval = getpeername(server_socket, &socket_address, &address_length);

    if (rval == 0) {
      /* 打印消息。端口号需要从网络字节序（大端）转换为主机字节序。 */
      printf("server listening on %s:%d\n", inet_ntoa(socket_address.sin_addr), ntohs(socket_address.sin_port));
    }
  }

  /* 循环处理连接。 */
  while (1) {
    struct sockaddr_in remote_address;
    socklen_t address_length;
    int connection;
    pid_t child_pid;

    /* 接受连接。此调用阻塞直到连接准备就绪。 */
    address_length = sizeof(remote_address);
    connection = accept(server_socket, &remote_address, &address_length);

    if (connection == -1) {
      /* accept 调用失败。 */
      if (errno == EINTR) {
        /* 调用被信号中断。重试。 */
        continue;
      } else {
        /* 发生了错误。 */
        system_error("accept");
      }
    }

    /* 我们有一个连接。如果运行详细模式，则打印消息。 */
    if (verbose) {
      socklen_t address_length;

      /* 获取连接的远程地址。 */
      address_length = sizeof(remote_address);
      rval = getpeername(connection, &remote_address, &address_length);

      if (rval == 0) {
        /* 打印消息。 */
        printf("connection accepted from %s\n", inet_ntoa(remote_address.sin_addr));
      }
    }

    /* Fork 一个子进程来处理连接。 */
    child_pid = fork();

    if (child_pid == 0) {
      /* 这是子进程。它不应该使用 stdin 或 stdout。 */
      close(STDIN_FILENO);
      close(STDOUT_FILENO);

      /* 此进程也不应该对监听套接字做任何操作。 */
      close(server_socket);

      /* 来自连接的请求。我们有连接套接字的副本。 */
      handle_connection(connection);

      /* 全部完成；关闭连接套接字并结束子进程。 */
      close(connection);
      exit(0);
    } else if (child_pid > 0) {
      /* 这是父进程。子进程处理连接，所以我们不需要连接套接字描述符副本。然后继续循环接受另一个连接。 */
      close(connection);
    } else {
      /* fork 调用失败。 */
      system_error("fork");
    }
  }
}
```



这些是 `server.c` 中的函数：

- `server_run`: 运行服务器的主入口。该函数启动服务器并开始接受连接，除非发生严重错误，否则不会返回。服务器使用 TCP 流套接字（见第 5 章“进程间通信”中的 5.5.3 节“服务器”）。
  - `server_run` 的第一个参数指定接受连接的本地地址。GNU/Linux 计算机可能有多个网络地址，每个地址可能绑定到不同的网络接口。要限制服务器从特定接口接受连接，请指定相应的网络地址。使用 `INADDR_ANY` 接受任何本地地址的连接。
  - `server_run` 的第二个参数是接受连接的端口号。如果端口号已被占用，或者它对应于特权端口且服务器未以超级权限运行，则服务器将失败。特殊值 `0` 指令 Linux 自动选择一个未使用的端口。
  - 有关互联网域名地址和端口号的更多信息，请参阅 `inet` 手页。
  - 服务器通过通过 `fork` 创建的子进程处理每个客户端连接（见第 3 章“进程”中的 3.2.2 节“使用 fork 和 exec”）。在处理连接时，（父）进程继续接受新连接。子进程调用 `handle_connection` 然后关闭套接字并退出。

- `handle_connection`: 使用传递的套接字文件描述符处理单个客户端连接。此函数从套接字读取数据并尝试将其解释为 HTTP 页面请求。
  - 服务器只处理 HTTP 版本 1.0 和 1.1 请求。当遇到不同的协议或版本时，它通过发送 HTTP 结果码 `400` 和消息 `bad_request_response` 来响应。服务器只理解 HTTP `GET` 方法。如果客户端请求任何其他方法，服务器通过发送 HTTP 结果码 `501` 和消息 `bad_response_template` 来响应。

## 11.2 实现

如果客户端发送了对应服务器模块的页面请求，`handle_get` 会向客户端发送 `200` 头部，这表示请求已成功处理，并调用模块的 `module_generate` 函数。该函数生成 Web 页面的 HTML 源码并发送到 Web 客户端。

- `server_run` 将 `clean_up_child` 作为 `SIGCHLD` 的信号处理程序。该函数仅负责清理终止的进程（参见第 3 章 3.4.4 节“异步清理子进程”）。

### 11.2.4 主程序

`main.c`（见列表 11.5）为服务器程序提供了主函数。它的职责是解析命令行选项、检测并报告命令行错误，以及配置并运行服务器。

### 11.5 (main.c) 主服务器程序和命令行解析

```c
#include <assert.h>
#include <getopt.h>
#include <netdb.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/stat.h>
#include <unistd.h>
#include "server.h"

/* getopt_long 的长选项描述。 */
static struct option long_options[] = {
    { "address", 1, NULL, 'a' },
    { "help", 0, NULL, 'h' },
    { "module-dir", 1, NULL, 'm' },
    { "port", 1, NULL, 'p' },
    { "verbose", 0, NULL, 'v' },
};

/* getopt_long 的短选项描述。 */
static const char *short_options = "a:hm:p:v";

/* 摘要文本。 */
static const char *usage_template = 
    "Usage: %s [options] \n"
    "  -a, --address ADDR 绑定到本地地址（默认情况下，绑定\n"
    "到所有本地地址）。\n";
```

`-h, --help` 打印此信息。
`-m, --module-dir DIR` 从指定目录加载模块（默认使用可执行文件所在目录）。
`-p, --port S` 绑定到指定端口。
`-v, --verbose` 打印详细信息。

```c
/* 打印用法信息并退出。如果 IS_ERROR 非零，则写入 stderr 并使用错误代码退出。否则，写入 stdout 并使用非错误终止代码。函数不返回。 */
static void print_usage(int is_error)
{
    fprintf(is_error ? stderr : stdout, usage_template, program_name);
    exit(is_error ? 1 : 0);
}

int main(int argc, char* argv[])
{
    struct in_addr local_address;
    uint16_t port;
    int next_option;

    /* 存储程序名，将在错误消息中使用它。 */
    program_name = argv[0];

    /* 设置选项的默认值。将服务器绑定到所有本地地址，并自动分配未使用的端口。 */
    local_address.s_addr = INADDR_ANY;
    port = 0;

    /* 不打印详细信息。 */
    verbose = 0;

    /* 从包含此可执行文件的目录加载模块。 */
    module_dir = get_self_executable_directory();
    assert(module_dir != NULL);

    /* 解析选项。 */
    do {
        next_option = 
        getopt_long(argc, argv, short_options, long_options, NULL);
        switch ('a':
            /* 用户指定 -a 或 --address。 */
            struct hostent* local_host_name;
            /* 查找用户指定的机名。 */
            local_host_name = gethostbyname(optarg);
            if (local_host_name == NULL || local_host_name->h_length == 0)
```

```c
/* 无法解析名称。 */
            error (optarg,'invalid host name');
        else
            /* 主机名正常，因此使用它。 */
            local_address.s_addr =
                ((int*) (local_host_name->h_addr_list[0]));
        break;
        case 'h':
            /* 用户指定 -h 或 --help。 */
            print_usage(0);
        case 'm':
            /* 用户指定 -m 或 --module-dir。 */
            {
                struct stat dir_info;
                /* 检查它是否存在。 */
                if (access(optarg, F_OK) != 0)
                    error (optarg,'module directory does not exist');
                /* 检查是否可访问。 */
                if (access(optarg, R_OK) != 0)
                    error (optarg,'module directory is not accessible');
                /* 确保它是一个目录。 */
                if (stat (optarg, &dir_info) != 0 || !IS_DIR(dir_info.st_mode))
                    error (optarg,'not a directory');
                /* 看起来正常，因此使用它。 */
                module_dir = strdup(optarg);
            }
            break;
        case 'p':
            /* 用户指定 -p 或 --port。 */
            {
                long value;
                char *end;
                value = strtol(optarg, &end, 10);
                if (*end != '\0') {
                    /* 用户指定的端口数字。 */
                    print_usage(1);
                    /* 端口号需要转换为网络字节序。 */
                    port = (uint16_t) htons(value);
                }
            }
            break;
        case 'v':
            /* 用户指定 -v 或 --verbose。 */
            verbose = 1;
            break;
        case '?':
            /* 指定了未识别的选项。 */
            print_usage(1);
        case -1:
            /* 完成选项处理。 */
            break;
        default:
            abort ();
    } while (next_option != -1);

    /* 此程序不接受参数。如果用户指定了参数，则报错。 */
    if (optind != argc)
        print_usage(1);

    /* 如果运行详细模式，打印目录。 */
    if (verbose)
        printf("modules will be loaded from %s\n", module_dir);

    /* 运行服务器。 */
    server_run(local_address, port);

    return 0;
}
```

`main.c` 包含这些函数：

- `main` 调用 `getopt_long`（参见第 2.3 节“使用 getopt_long”）来解析命令行选项。它提供了长短选项形式，分别位于 `long_options` 数组和 `short_options` 字符串中。服务器端口的默认值为 `0`，本地地址为 `INADDR_ANY`。这些可以通过 `--port (p)` 和 `--address (a)` 覆盖。
- 加载模块的目录默认是可执行文件所在的目录，由 `get_executable_directory` 确定。用户可以使用 `--module-dir (m)` 覆盖它；`main` 会确保该目录可访问。
- 默认不打印详细信息。用户可以通过指定 `--verbose (v)` 来启用它们。
- `gethostname` 执行名称解析。
- 如果用户指定 `--help (h)` 或无效选项，`main` 调用 `print_usage` 打印摘要并退出。

## 11.3 模块

我们提供了四个模块来演示可以实现的功能。实现服务器模块只需要定义 `module_generate` 函数返回相应的 HTML 文本即可。

### 11.3.1 显示时间

`time.so` 模块（见列表 11.6）生成包含服务器本地时间的简单页面。该 `module_generate` 调用 `gettimeofday` 获取当前时间（参见第 8 章“系统调用”中的“gettimeofday: 钟时间”），并使用 `localtime` 和 `str` 创建其文本表示。该表示嵌入在 HTML 模板 `page_template` 中。

# 列表 11.6 (time.c) 显示时间的服务器模块

```c
#include <stdio.h>
#include <sys/time.h>
#include <time.h>
#include "server.h"

/* 此模块生成的 HTML 页面模板。 */
struct char *page_template = 
"<html>\n"
  "<head>\n"
  "<meta http-equiv=\"refresh\" content=\"5\">\n"
  "</head>\n"
  "<body>\n"
  "<p>The current time is %s.</p>\n"
  "</body>\n"
"</html>";

void module_generate (int fd) {
  struct timeval tv;
  struct tm *ptm;
  char time_string[40];
  FILE *fp;
  /* 获取时间并将其转换为 tm 结构体。 */
  getimeofday(&tv, NULL);
  ptm = localtime(&tv.tv_sec);
```

# 列表 11.6 继续

```c
/* 格式化日期时间精确到秒。 */
strftime(time_string, sizeof(time_string), "%H:%M:%S", ptm);

/* 创建对应客户端 socket 文件描述符的流。 */
fp = fdopen(fd, "w");
assert(fp != NULL);

/* 生成 HTML 输出。 */
printf(fp, page_template, time_string);

/* 完成；刷新流。 */
fflush(fp);
}
```

该模块使用标准 C 库 I/O 例程为了方便。`fdopen` 调用生成了一个与客户端 socket 文件描述符对应的指针 (`FILE*`)（参见附录 B B.4 节“与标准 C 库函数的关系”，“底层 I/O”）。模块使用 `printf` 向其写入并使用 `fflush` 刷新，以防止在 socket 关闭时丢失缓冲区数据。
`time.so` 模块返回的 HTML 页面头部包含一个 `<meta>` 元素，指示客户端每 5 秒重新加载一次页面。通过这种方式，客户端显示当前时间。

### 11.3.2 显示 GNU/Linux 版本

`issue.so` 模块（见列表 11.7）显示运行在服务器上的 GNU/Linux 版本信息。这些信息通常存储在 `/etc/issue` 文件中。该模块发送该文件的内容并封装在 HTML 页面的 `<pre>` 元素中。

# 列表 11.7 (issue.c) 显示 GNU/Linux 版本的信息的服务器模块

```c
#include <fcntl.h>
#include <string.h>
#include <sys/sendfile.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>
#include "server.h"

/* 我们生成的页面开始部分的 HTML 源码。 */
static char *page_start = 
  "<html>\n"
  "<head>\n"
  "<body>\n";
```

## 11.3 模块 241

```c
/* HTML source for the end of the page we generate. */
static char* page_end =
  "<pre>\n"
  "<body>\n"
  "</html>\n";
```

/* HTML source for the page indicating there was a problem opening /proc/issue. */

```c
static char* error_page =
  "<html>\n"
  "<body>\n"
  "<p>Error: Could not open /proc/issue.</p>\n"
  "</body>\n"
  "</html>\n";
```

/* HTML source indicating an error. */

```c
static char* error_message = "Error reading /proc/issue."

void module_generate (int fd)
{
  int input_fd;
  struct stat file_info;
  int rval;

  /* Open /etc/issue. */
  input_fd = open("/etc/issue", O_RDONLY);
  if (input_fd == -1)
    system_error("open");
```



```c
/* Obtain file information about it. */

rval = fstat (input_fd, &file_info);

/* Either we couldn't open the file or we couldn't read from it. */

if (rval == -1)

    write(fd, error_page, strlen(error_page));

else {

    int rval;

    off_t offset = 0;

    /* Write the start of the page. */

    write(fd, page_start, strlen(page_start));

    /* Copy from /proc/issue to the client socket. */

    rval = sendfile(fd, input_fd, &offset, file_info.st_size);

    if (rval == -1) {

      /* Something went wrong sending the contents of /proc/issue. */

      /* Write an error message. */

      write(fd, error_message, strlen(error_message));

    }

}

```

```c
#include <stdlib.h>

#include <string.h>

#include <sys/types.h>

#include <sys/wait.h>

#include <unistd.h>

#include "server.h"

/* HTML source for the start of the page we generate. */

static char* page_start = 

  "<html>\n"

  "<body>\n"

  "<pre>\n";

/* HTML source for the end of the page we generate. */

static char* page_end = 

"<pre>\n"

"<body>\n"

"</html>\n";

void module_generate(int fd) {

    pid_t child_pid;

    int rval;

    /* Write the start of the page. */

    write(fd, page_start, strlen(page_start));

    /* Fork a child process. */

    child_pid = fork();

    if (child_pid == 0) {

        /* This is the child process. */

        /* Set up an argument list for the invocation of df. */

        char* argv[] = { "/bin/df", "-h", NULL };

        /* Duplicate stdout and stderr to send data to the client socket. */

        rval = dup2(fd, STDOUT_FILENO);

        if (system_error("dup2") == -1)

            rval = dup2(fd, STDERR_FILENO);

        if (rval == -1)

            system_error("dup2");

        /* Run df to show the free space on mounted file systems. */

        execv(argv, argv);

        /* A call to execv does not return unless an error occurred. */

        system_error("execv");

    } else if (child_pid > 0) {

        /* This is the parent process. Wait for the child process to finish. */

        rval = waitpid(child_pid, NULL, 0);

        if (rval == -1)

            system_error("waitpid");

    } else {

        /* The call to fork failed. */

        system_error("fork");

    }

    /* Write the end of the page. */

    write(fd, page_end, strlen(page_end));

}
```

虽然 `issue` 模块使用 `sendfile` 发文件内容，但此模块必须调用命令并将输出重定向到客户端。为了实现这一点，模块遵循以下步骤：

1. 首先，模块使用 `fork` 创建子进程（参见第 3 章 3.2.2 节“使用 `fork` 和 `exec`”）。
2. 子进程将客户端 `socket` 文件描述符复制到描述符 `STDOUT_FILENO` 和 `STDERR_FILENO`，它们对应标准输出和标准错误（参见第 2 章 2.1.4 节“标准 I/O”）。文件描述符使用 `dup2` 调用复制（参见第 5 章 5.4.3 节“重定向标准输入、输出和错误流”）。该进程到这些流的所有后续输出都将发送到客户端 `socket`。
3. 子进程通过调用 `execv` 调用带有 `-h` 选项 `df` 命令（参见第 3 章 3.2.2 节“使用 `fork` 和 `exec`”）。
4. 父进程通过调用 `waitpid` 等待子进程退出（参见第 3 章 3.4.2 节“系统调用”）。你可以轻松地调整此模块以调用不同的命令并重定向其输出。

### 11.3.4 总结进程

`processes` 模块（参见列表 11.9）是一个更复杂的服务器模块。它生成一个总结服务器上运行进程的页面。表格列出了 `PID`、执行文件名称、所属用户和组以及驻内存大小。

列表 11.9 (`processes.c`) 总结模块
```c
#include <assert.h>

#include <dirent.h>

#include <fcntl.h>

#include <grp.h>

#include <pwd.h>

#include <stdio.h>

#include <stdlib.h>

#include <string.h>

#include <sys/stat.h>

#include <sys/types.h>

#include <io.h>

#include <unistd.h>

#include "server.h"

/* 将 UID 和 GID 分别设置为 PID 的所属用户 ID 和组 ID。成功返回 0，失败返回非零。 */

static int get_uid_gid(pid_t pid, uid_t* uid, gid_t* gid) {

    char dir_name[64];

    struct stat dir_info;

    int rval;

    /* 生成 /proc 中的进程目录名。 */

    sprintf(dir_name, sizeof(dir_name), "/proc/%d", (int) pid);

    /* 获取目录信息。 */

    rval = stat(dir_name, &dir_info);

    if (rval != 0) {

        /* 未找到它；进程可能不存在。 */

        return 1;

    }

    /* 确保它是目录；其他情况均不符合。 */

    assert(S_ISDIR(dir_info.st_mode));

    /* 提取 ID。 */

    *uid = dir_info.st_uid;

    *gid = dir_info.st_gid;

    return 0;

}

static char* get_user(uid_t uid) {

    struct passwd* entry;

    entry = getpwuid(uid);

    if (entry == NULL) {

        system_error("getpwuid");

    }

    return strdup(entry->pw_name);

}

/* 返回组名。调用者必须分配并释放返回的缓冲区。UID 必须是有效的 ID。 */

static char* get_group_name(gid_t gid) {

    struct group* entry;

    entry = getgrgid(gid);

    if (entry == NULL) {

        system_error("getgrgid");

    }

    return strdup(entry->gr_name);

}
```

列表 11.9 (`processes.c`) 继续

```c
/* 返回进程的驻内存大小 (RSS)，以 KB 为单位。失败返回 -1。 */
static int get_rss(pid_t pid) {
    char file_name[64];
    int fd;
    char mem_info[128];
    int rval;
    int rss;

    /* 生成 /proc/ 目录中进程的 "statm" 条目。 */
    sprintf(file_name, sizeof(file_name), "/proc/%d/statm", (int) pid);
    /* 打开它。 */
    fd = open(file_name, O_RDONLY);
    if (fd == -1) {
        /* 无法打开；进程可能不存在。 */
        return -1;
    }

    /* 读取文件内容。 */
    rval = read(fd, mem_info, sizeof(mem_info)) - 1;
    close(fd);
    if (rval < 0) {
        /* 无法读取；退出。 */
        return -1;
    }

    /* 提取 RSS。它是第二项。 */
    rval = scanf(mem_info, "%*d %d", &rss);
    if (rval != 1) {
        /* statm 内容格式我们无法理解。 */
        return -1;
    }

    /* stat 中的值以系统页大小为单位。将 RSS 转换为 KB。 */
    return rss * getpagesize() / 1024;
}

/* 为 PID 生成 HTML 表格行。返回指向缓冲区的指针，调用者必须释放内存，如果发生错误则返回 NULL。 */
static char* format_process_info(pid_t pid) {
    int rval;
    uid_t uid;
    gid_t gid;
    char* user_name;
    char* group_name;
    int rss;
    char* program_name;
    size_t result_length;
    char* result;

    /* 获取进程的 ID ID 和组 ID。 */
    rval = get_uid_gid(pid, &uid, &gid);
    if (rval != 0)
        return NULL;
    /* 获取进程的 RSS。 */
    rss = get_rss(pid);
    if (rss == -1)
        return NULL;
    /* 获取进程的程序名。 */
    program_name = get_program_name(pid);
    if (program_name == NULL)
        return NULL;
    /* 将用户 ID 和组 ID 转换为相应的名称。 */
    user_name = get_user(uid);
    group_name = get_group_name(gid);

    /* 计算存储结果所需的字符串长度，并分配内存。 */
    result_length = strlen(program_name)
    + strlen(user_name) + strlen(group_name) + 128;
    result = (char*)malloc(result_length);
    /* 格式化结果。 */
    sprintf(result, result_length,
"<tr align="left">%s</td><td align="right">%s</td><td>%s</td></tr>\n"
"<tr align="left">%s</td><td align="right">%s</td><td>%s</td></td></td></td></td></tr>\n",
    (int) pid, program_name, user_name, group_name, rss);
    /* 清理工作。 */
    free(program_name);
    free(user_name);
    free(group_name);
    /* 全部完成。 */
    return result;
}
```

## 11.3 模块 249

```html
* <th>RSS (KB)</th>
* </tr>
* </head>
* <tbody>
```

```c
/* HTML source for the end of the process listing page. */
static char* page_end = \
  " </body>\n"
  " </table>\n"
  " </body>\n"
* </html>\n;
```

```c
void module_generate (int fd) {
  size_t i;
  DIR* proc_listing;
```

```c
/* Set up an iovec array. We'll fill this with buffers that'll be
part of our output, growing it dynamically as necessary. */
/* 数组中已使用的元素个数。  */
size_t vec_length = 0;
/* 数组的分配大小。  */
size_t vec_size = 16;
/* iovec 元素数组。  */
struct iovec* vec = (struct iovec*) kmalloc(vec_size * sizeof(struct iovec));
```

```c
/* The first buffer is the HTML source for the start of the page. */
vec[vec_length].iov_base = page_start;
vec[vec_length].iov_len = strlen (page_start);
++vec_length;
```

```c
/* Start a directory listing for /proc. */
proc_listing = opendir("/proc");
if (proc_listing == NULL)
  system_error("/opendir");
/* Loop over directory entries in /proc. */
while (1) {
  struct dirent* proc_entry;
  const char* name;
  pid_t pid;
  char* process_info;
```

```c
/* Get the next entry in /proc. */
proc_entry = readdir(proc_listing);
if (proc_entry == NULL)
  /* We've hit the end of the listing. */
  break;
```

# 250 第 11 章 示例 GNU/Linux 应用程序

### 11.9 继续



```c
/* If this entry is not composed purely of digits, it's not a
process directory, skip it. */
name = proc_entry->d_name;
if (strcsp(name, "0123456789") != strlen(name))
    continue;
/* The name of the entry is the process ID. */
pid = (pid_t) atoi(name);
/* Generate HTML for a table row describing this process. */
process_info = format_process_info(pid);
if (process_info == NULL) {
    /* Something went wrong. The process may have vanished while we
    were looking at it. Use a placeholder instead. */
    process_info = "<td colspan='5'>ERROR</td>";
}
/* Make sure the iovec array is long enough to hold this buffer
(plus one more we'll add an extra element when we're done
listing processes). If not, grow it to twice its current size. */
if (vec_length == vec_size) {
    vec_size *= 2;
    vec = realloc(vec, vec_size * sizeof(struct iovec));
}
/* Store this buffer as the next element of the array. */
vec[vec_length].iov_base = process_info;
vec[vec_length].iov_len = strlen(process_info);
++vec_length;
/* End the directory listing operation. */
closedir(proc_listing);
/* Add one last buffer with HTML that ends the page. */
vec[vec_length].iov_base = page_end;
vec[vec_length].iov_len = strlen(page_end);
++vec_length;
/* Output the process to the client file descriptor all at once. */
writev(fd, vec, vec_length);
/* Deallocate the buffers we created. The first and last are static
and should not be deallocated. */
for (i = 1; i < vec_length - 1; ++i) {
    free(vec[i].iov_base);
}
/* Deallocate the iovec array. */
free(vec);
```

## 11.3 模块

收集进程数据并将其格式化为 `HTML` 表格被分为几个更简单的操作：

-   `get_uid_gid` 提取进程所有用户和组的 ID。为了实现这一点，该函数对 `/proc` 中的进程子目录调用 `stat`（参见附录 B 中的 B.2 节“stat”）（参见第 7 章中的 7.2 节“进程条目”）。拥有该目录的用户和组与进程的所有者组相同。
-   `get_user_name` 返回与 UID 对应的用户名。此函数简单地调用了 C 库函数 `getpwuid`，它会查询系统的 `/etc/passwd` 文件并返回结果的副本。`get_group_name` 返回与 GID 对应的组名。它使用了 `getgid` 调用。
-   `get_program_name` 返回在指定进程中运行的进程名称。此信息从 `/proc` 目录下的 `stat` 条目中提取（参见第 7 章中的 7.2 节“进程条目”）。我们使用此条目而不是使用符号链接（参见第 7 章中的 7.2.4 节“进程可执行文件”）或 `cmdline` 条目（参见第 7 章中的 7.2.4 节“进程可执行文件”）。
-   `get_rss` 返回进程的驻存内存大小。这在 `/proc` 中的 `stat` 条目可用。由于我们无法预知进程数量，必须从一个数组开始并随着新进程的添加进行扩展。`vec_length` 包含了使用的元素个数，而 `vec_size` 包含分配的大小。当 `vec_length` 即将超过 `vec_size` 时，通过调用 `realloc` 将 `vec` 扩展两倍。
-   `format_process_info` 生成单行的 `HTML` 字符串。`module_generate` 生成整个页面，包括表格。它使用 `sprintf` 生成页面的开始和结束。

为了优化数据成包，我们使用单次 `writev` 调用（参见附录 B 中的 B.3 节“矢量读写”）。如果我们单独调用将每个字符串写入 `socket`，这将产生不必要的流量，因为每个字符串可能会作为单独的数据包发送。释放 `vec` 指向的所有动态字符串以及 `vec` 本身。

## 11.4 使用服务器

如果我们计划以源码形式发布此程序、对其进行持续维护或用于其他平台，我们可能希望使用 `GNU Automake` 和 `GNU Autoconf` 或类似的配置自动化系统进行打包。这些工具超出了本书的范围；有关它们的更多信息，请参考 `Autoconf`、`Automake` 和 `Libtool`（由 Vaughan, Tromey 和 Taylor 著，New Riders 出版，2000年）。

### 11.4.1 Makefile

与其使用 `Autoconf` 或类似的工具，我们提供了一个与 `GNU Make` 兼容的简单 `Makefile`，以便编译和链接服务器及模块。`Makefile` 位于列表 11.10。有关文件语法的细节，请查看 `GNU Make` 的信息页。

**Listing 11.10 (Makefile) GNU Make 配置文件**

```make
### Configuration. options.
################################################

# C 编译器选项。
CFLAGS = -Wall -g
# 服务器的 C 源文件。
SOURCES = server.c module.c common.c main.c
# 对应的对象文件。
OBJECTS = $(SOURCES).o
# 服务器模块共享库文件。
MODULES = diskfree.so issue.so processes.so time.so

################################################################

# 规则。

# 伪目标（Phony targets）不对应构建的文件；它们是概念性构建目标的重命名。
.PHONY: all clean
```

```make
# 默认目标：构建所有内容
all: server $(MODULES)
```

```make
# 清理构建产物。
clean: rm -f $(OBJECTS) $(MODULES) server
```

```make
# 主服务器程序。使用 -W1,-export-dynamic 进行链接，以便
# 动态加载的模块可以绑定程序中的符号。链接 libld，它包含了动态加载的调用。
server: $(OBJECTS)
	$(CC) $(CFLAGS) -Wl,-export-dynamic -o $@ -ldl
```

```make
# server 中的所有对象文件都依赖于 server.h。但使用
# 从源文件构建对象的默认规则。
$(OBJECTS): server.h
```

```make
# 从相应的源文件构建共享库的规则。编译 -fPIC 
# 并生成共享对象文件。
$(MODULES): %.so server.h
	$(CC) $(CFLAGS) -fPIC -shared -o $@ $<
```

`Makefile` 提供了这些目标：

-   `all`（如果你在不带参数的情况下调用 `make`，它是 `Makefile` 中的第一个目标，即默认目标）包含了服务器可执行文件和所有模块。模块列在变量 `MODULES` 中。
-   `clean` 删除 `Makefile` 生成的任何构建产物。
-   `server` 链接服务器可执行文件。变量 `SOURCES` 中列出的源文件被编译并链接其中。
-   最后一条规则是用于从相应的源文件为服务器模块编译共享对象的通用模式。

请注意，服务器的源文件是用 `-fPIC` 选项编译的，因为它们链接到了共享库（参见第 2 章 2.3.2 节“共享库”）。

此外还可以观察到服务器可执行文件是用编译器选项 `-W1,-export-dynamic` 链接的。通过此选项，`GCC` 将 `-export-dynamic` 选项传递给链接器，创建一个将其外部符号作为共享库导出的可执行文件。这允许作为共享库动态加载的模块引用 `common.c` 中的函数，而这些函数是静态链接到服务器可执行文件的。

### 11.4.2 构建服务器

构建程序非常简单。在包含源文件的目录中，只需调用 `make`：

```bash
% make
cc -Wall -g -o server.c
cc -Wall -g -o module.c
cc -Wall -g -o common.c
cc -Wall -g -Wl,-export-dynamic -o server.o module.o main.o -lm
cc -Wall -g -fPIC -shared diskfree.so
cc -Wall -g -fPIC -shared issue.so
cc -Wall -g -fPIC -shared processes.so
cc -Wall -g -fPIC -shared -o time.so time.c
```

这构建了服务器程序和服务器共享库。

```bash
% ls -l server *.so
-rw-r--r--x 1 samuel samuel 25769 Mar 11 01:15 diskfree.so
-rw-r--r--x 1 samuel samuel 31184 Mar 11 01:15 issue.so
-rw-r--r--x 1 samuel samuel 41579 Mar 11 01:15 processes.so
-rw-r--r--x 1 samuel samuel 71758 Mar 11 01:15 server
-rw-r--r--x 1 samuel samuel 13980 Mar 11 01:15 time.so
```

### 11.4.3 运行服务器

要运行服务器，只需调用服务器可执行文件。使用 `--port` (`-p`) 选项，`Linux` 将为你选择一个端口；在这种情况下，指定 `--verbose` (`-v`) 让服务器打印出正在使用的端口号。

如果你没有通过 `--address` (`-a`) 指定地址，服务器将在你计算机的所有地址上运行。如果你的计算机连接到了网络，那么这意味着只要其他人知道正确的端口号并进行请求，他们就能访问服务器。出于安全考虑，除非你确定服务器运行正常且不想发布任何不想公开的信息，否则指定 `localhost` 地址是一个好主意。绑定到 `localhost` 会导致服务器绑定到本地网络设备（指定为 `"lo"`）——只有运行同一台计算机上的程序才能连接到它。如果你指定了不同的地址，它必须是与计算机对应的地址：

```bash
$ ./server --address localhost --port 4000
```

服务器现在正在运行。打开浏览器窗口，尝试通过此端口号联系服务器。请求一个名称与其中一个模块匹配的页面。例如，使用此 `URL` 调用 `diskfree.so` 模块：

```bash
http://localhost:4000/diskfree
```

代替 `4000`，输入你指定的端口号（或 `Linux` 为你选择的端口号）。完成后按 `Ctrl+C` 杀死服务器。

如果你没有指定 `localhost` 作为服务器地址，你也可以在 `URL` 中使用计算机主机名，通过另一台计算机上运行的网络浏览器连接到服务器：

```bash
http://host.domain.com:4000/diskfree
```

如果你指定了 `-verbose` (`-v`) 选项，服务器会在启动时打印一些信息并显示连接到它的每个客户端的数字 `Internet` 地址。如果你通过 `localhost` 连接，服务器会在启动时打印信息并显示连接到它的每个客户端的数字 `Internet` 地址。

## A.2 查找动态内存错误

在编写程序时，你通常无法知道程序在运行时需要多少内存。例如，运行时从文件中读取的一行可能具有有限的长度。`C` 和 `C++` 程序使用 `malloc`、`free` 及其变体在程序运行时动态分配内存。动态内存的规则包括这些：

-   分配调用次数（对 `malloc` 的调用）必须与释放调用次数（对 `free` 的调用）完全匹配。
-   对分配内存的读写操作必须在内存内部进行，不能在内存范围之外。
-   分配的内存不能在分配之前或释放后使用。

由于动态内存的分配和释放发生在运行时，静态分析很少发现违规行为。相反，内存检查工具会运行程序，收集数据以判断是否违反了这些规则。工具可能会发现以下违规行为：

-   在分配内存之前读取内存
-   在分配内存之前写入内存
-   在分配内存开始位置之前读取
-   在分配内存开始位置之前写入
-   在分配内存结束后读取内存
-   在分配内存结束后写入内存
-   在释放内存后读取内存
-   在释放内存后写入内存
-   未能释放已分配的内存
-   重复释放同一块内存
-   释放未分配的内存

在请求分配 `0` 字节之前进行也是很有用的，这可能表明程序员的错误。

表 A.1 显示了四种不同工具的诊断能力。遗憾的是，没有一个工具可以诊断所有的内存错误。没有工具声称能检测在分配内存之前的读取或写入，但这样做可能会导致段错误（segmentation fault）。两次释放内存也可能导致段错误。这些工具仅诊断程序运行时实际发生的错误。如果你提供的程序输入不包含需要分配的内存，工具将指示没有内存错误。要测试程序，你必须使用不同的输入运行程序，以确保程序中每种可能的路径都会发生。此外，你一次只能使用一个工具，因此必须使用多个工具重复测试以获得最佳错误检查。

## 262 附录 A 其他开发工具

表 A.1 内存检查工具的能力（`X` 表示检测，`O` 表示某些情况下可检测）

| 错误行为 | malloc 检查 | mtrace | cmalloc | Electric Fence |
| :--- | :--- | :--- | :--- | :--- |
| 分配内存前读取 | | | | |
| 分配开始前写入 | | | | X |
| 分配开始前读取 | O | | O | X |
| 分配结束后读取 | | | | X |
| 分配结束后写入 | | | X | X |
| 释放后读取 | | | | X |
| 释放后写入 | | | | X |
| 未释放已分配的内存 | | X | X | |
| 重复释放内存 | X | | X | |
| 释放未分配的内存 | | X | X | |
| 零大小内存分配 | | | | X |

在随后的章节中，我们首先描述如何使用更易用的 `malloc` 检查和 `mtrace`，然后是 `cmalloc` 和 `Electric Fence`。

### A.2.1 用于测试内存分配和释放的程序

我们将使用列表 A.2 中的 `malloc-use` 程序来说明内存的分配、释放和使用。要开始运行它，将分配内存区域的最大数量作为唯一的命令行参数。例如，`malloc-use 12` 会创建一个包含 `12` 个字符指针的数组 `A`，这些指针不指向任何地方。程序接受五种不同的命令：

-   通过数组 `A[i]` 分配 `b` 字节，输入 `i b`。数组索引可以是任何小于命令行参数的非负数。字节数必须为非负。
-   在索引 `i` 处分配内存，输入 `d i`。
-   从索引 `i` 处的分配内存中读取第 `p` 个字符（如 `A[i][p]`），输入 `i p`。这里，`p` 可以是一个整数。
-   向索引 `i` 处分配内存的第 `p` 个位置写入字符，输入 `w i`。
-   完成后，输入 `q`。

我们稍将在 A.2.7 节介绍程序的代码，并说明如何使用它。

## A.2 查找动态内存错误 263

### A.2.2 malloc 检查

`GNU C` 库提供的内存分配函数可以检测分配开始之前的写入以及两次释放同一分配。将环境变量 `MALLOC_CHECK_` 设置为值 `2` 会导致程序在检测到错误时停止。（注意环境变量结尾的下划线）。不需要重新编译程序。

我们来说明诊断对分配开始位置之前位置的写入。

```bash
% export MALLOC_CHECK_=2
% ./malloc-use 12
Please enter a command: a 0 10
Please enter a command: w 0 -1
Please enter a command: d 0
Aborted (core dumped)
```

`export` 开启 `malloc` 检查。指定值 `2` 会导致程序一旦检测到错误立即停止。

使用 `malloc` 检查的优点是程序不需要重新编译，但其诊断错误的能力有限。基本上，它检查分配器数据结构没有被损坏。因此，它可以检测到同一分配的双重释放。此外，在内存分配开始位置之前的写入通常可以被检测到，因为分配器在分配区域之前存储了每次内存分配的大小。因此，在分配内存之前的写入会破坏该区域。遗憾的是，一致性检查只有在分配被释放时才会发生。

### A.2.3 使用 mtrace 查找内存泄漏



`mtrace` 工具帮助诊断使用 `mtrace` 时常见的错误：分配和释放不匹配。有四个步骤来使用 `mtrace`，它是 GNU C 库自带的：

1. 修改源代码包含 `<malloc.h>` 并在程序启动时调用 `mtrace()`。`mtrace` 开启对内存的跟踪。

2. 指定存储文件的名称：

```
% export MALLOC_TRACE=memory
```

3. 运行程序。所有的分配和释放都存储在日志文件中。

4. 使用 `mtrace` 命令分析该文件以确保它们匹配。

```
% mtrace memory
```

`mtrace` 产生的消息相对容易理解。例如，对于我们的 `malloc-use` 示例，输出如下：

```
- 0000000000 3 Free was never'd malloc-use.c
```

Memory not freed:

| 地址 | 调用者 |
| :--- | :--- |
| `0x08049d48` | `0c` `malloc-use.c:30` |

这些消息表示 `malloc-use.c` 的 39 行尝试释放未分配的内存，以及 30 行的分配未被释放。`mtrace` 通过在 `MALLOC_TRACE` 指定的范围内记录所有分配和释放来诊断错误。`mtrace` 命令必须正常执行。

### A.2.4 使用 cmalloc

`cmalloc` 库通过替换 `malloc` 和 `free` 并跟踪它们的使用来诊断内存错误。如果程序顺利跟踪，它会生成内存泄漏和其他错误的报告。`cmalloc` 库由 Armin 编写。

你可能需要自己下载并安装 `cmalloc` 库。从 `http://www.inf.ethz.ch/personal/biere/projects/cmalloc/` 下载代码，解压并运行 `configure`。运行 `make` 并安装，将 `cmalloc.cfg` 文件复制到你要检查程序的目录，并将其重命名为 `.cmalloc`。现在可以使用该工具了。

程序的对象文件必须与 `cmalloc` 库和动态链接库链接。在你的命令中附加 `-cmalloc -ld` 进行链接，例如：

```
% gcc -g -Wpedantic malloc-use.c -o cmmalloc -cmalloc -ldl
```

执行程序以产生报告。例如，运行 `malloc-use` 程序分配但不释放内存会产生如下报告：

```
./cmalloc-out does not contain valid symbols
trying to find executable in current directory ...
using symbols from 'cmalloc-use'
(to speed up this startup specify 'file cmalloc-use'
in the startup file '.cmalloc')
Please enter a command: a 12
nPlease enter a command: q
```

## 264 附录 A 其他开发工具

## A.2 查找动态内存错误 265

```
ccmalloc report |
===========================================
| total # of | allocated | deallocated | garbage |
+-----------+-----------+-------------+----------+
| bytes | 60 | 48 | 12 | |
+-----------+-----------+-------------+----------+
| allocations| | 2 | 1 | 1 |
+-------------+-----------+-------------+----------+
```

number of checks: 1

number of counts: 3

retrieving function names for addresses ... done.

reading file info from gdb ... done.

sorting by number of no reclaimed bytes ... done.

number of call chains: 1

number of ignored call chains: 0

number of reported call chains: 1

number of internal call chains: 1

number of library call chains: 0

===========================================

*100.0% = 12 Bytes of garbage allocated in 1 allocation

```
0x400389cb in <??>

0x08049198 in <main>
    at malloc-use.c:89

0x08048fdc in <allocate>
    at malloc-use.c:30

---> 0x08049647 in <malloc>
    at src/wrapper.c:284
```

最后几行显示了分配了未释放内存的调用链函数。

若要使用 `ccmalloc` 诊断分配区域开始之前或结束之后的写入操作，你需要修改当前目录下的 `.ccmalloc` 文件。该文件在程序开始执行时会被读取。

### A.2.5 Electric Fence

`Electric Fence` 由 Bruce Peters 编写，它会在发生分配区域之外的写入或读取时的精确行停止执行程序。这是唯一发现非法读取的工具。它包含在大多数 GNU/Linux 发行版中，但源代码可以在 `http://www.perens.com/FreeSoftware` 找到。

与 `emalloc` 类似，你的程序对象文件必须通过在链接命令后添加 `-lfence` 来链接 `Electric Fence` 库，例如：

```
% gcc -g -Wall -pedantic malloc-use -o malloc -lfence
```

当程序运行时，分配的内存使用将进行正确性检查。违规会导致段错误（segmentation fault）：

- `Electric Fence 2.0.5 Copyright (C) 1987-1998 Bruce Perens.`

`nPlease enter a command: a 12`

`nPlease enter a command: r 12`

`Segmentation fault`

使用调试器，你可以确定非法操作的上下文。

默认情况下，`Electric Fence` 只诊断超出分配结束部分的访问。若要查找分配开始之前的访问而非分配结束之后的访问，请使用以下代码：

```
% EF_PROTECT_BELOW=1
```

要查找对已释放内存的访问，请将 `EF_PROTECT_FREE` 设置为 1。更多功能请参见 `libfence` 手页。

`Electric Fence` 通过将每个分配存储在两个内存页上来诊断非法内存。它将分配放在第一个页的末尾；在第二个页上发生的任何超出分配结束位置的访问都会导致段错误。如果你将 `EF_PROTECT_BELOW` 设置为 1，它则会将分配放在第二个页的开头。由于它每次调用 `malloc` 都会分配两个内存页，`Electric Fence` 会消耗大量的内存。请仅将此库用于调试。

### A.2.6 在不同的内存调试工具之间进行选择

我们讨论了四种独立的、不兼容的工具来诊断动态内存的错误使用。GNU/Linux 程序员如何确保动态内存是正确的？没有工具能保证发现所有错误，但使用其中任何工具都能增加发现错误的概率。为了轻松地找到动态分配的内存错误，请单独开发和测试处理动态内存的代码。这可以减少你必须搜索的代码量。如果你使用 C++，请编写一个处理所有动态内存的类。如果你使用 C，请尽量减少使用分配和释放的函数数量。测试这些代码时，不要一次只使用一种工具，因为它们是不兼容的。在测试程序时，确保改变程序的执行方式，以测试代码中最执行频繁的部分。

你应该使用这四种工具中的哪一个？因为分配和释放不匹配是最常见的动态内存错误，因此在初始开发期间使用 `mtrace`。该程序在所有 GNU/Linux 系统上可用并已通过良好测试。在确保分配和释放的次数匹配后，使用 `Electric Fence` 寻找非法内存访问。这将消除几乎所有的内存错误。在使用 `Electric Fence` 时，你需要小心不要进行过多的分配和释放，因为每次分配至少需要两个页内存。使用这两个工具将揭示大部分内存错误。

### A.2.7 动态内存程序的源代码

列表 A.2 显示了用于说明动态内存分配、释放和使用的程序源代码。关于如何使用它的描述，请参见第 A.2.1 节“测试内存分配和释放的程序”。

**列表 A.2 (`malloc-use.c`) 动态内存分配检查示例**

```
/* 使用 C 的动态内存分配函数。 */
/* 使用一个命令行参数指定数组的（大小）来调用程序。该数组包含指向（可能）分配的数组的指针的指针。
程序正在运行，请在以下命令中选择：
分配内存: a <size>
释放内存: d <index>
从内存读取: r <index>
向内存写入: w <index>
退出: q

用户负责遵守（或不遵守）动态内存使用的规则。 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <assert.h>

/* 分配指定大小的内存 */
void allocate(char** array, size_t size) {
    *array = (char **) calloc(size, sizeof(char *));
    if (*array == NULL) exit(1);
}

/* 释放内存。 */
void deallocate(char** array, int index) {
    free(array[index]);
}

/* 从内存读取。 */
void read_from_memory(char** array, int index) {
    printf("%s\n", array[index]);
}

/* 向内存写入。 */
void write_to_memory(char** array, int index, const char* value) {
    strcpy(array[index], value);
}

int main(int argc, char* argv[]) {
    if (argc != 2) {
      fprintf(stderr, "%s <size>\n", argv[0]);
      return 1;
    }

    size_t array_size = strtol(argv[1], 0, 0);
    char** array = NULL;
    int error = 0;
    char command[32];
    int array_index;
    int size_position;
    char command_letter;

    while (error) {
      printf("Please enter a command: ");
      command_letter = getchar();
      assert(command_letter != EOF);
      switch (command_letter) {
        case 'a':
          fgets(command, sizeof(command));
          if (sscanf(command, "%u %i", &array_index, &size_position) == 2
              && array_index < array_size) {
            allocate(&array, size_position);
          } else {
            error = 1;
          }
          break;
        case 'd':
          fgets(command, sizeof(command));
          if (sscanf(command, "%u", &array_index) == 1
              && array_index < array_size) {
            deallocate(&array, array_index);
          } else {
            error = 1;
          }
          break;
        case 'r':
          fgets(command, sizeof(command));
          if (sscanf(command, "%u %i", &array_index, &size_position) == 2
              && array_index < array_size) {
            read_from_memory(array, array_index);
          } else {
            error = 1;
          }
          break;
        case 'w':
          fgets(command, sizeof(command));
          if (sscanf(command, "%u %i %s", &array_index, &size_position, command) == 3
              && array_index < array_size) {
            write_to_memory(array, array_index, command);
          } else {
            error = 1;
          }
          break;
        case 'q':
          free ((void*) array);
          return 0;
        default:
          error = 1;
      }
    }
    free ((void*) array);
    return 1;
  }
}
```

## 270 附录 A 其他开发工具

在本节中，我们将描述如何使用 `gprof`。重写代码以使其运行得更快需要创造力和对算法的仔细选择。获取分析信息需要三个步骤：

1. 编译并链接你的程序以启用分析功能。
2. 执行你的程序以生成分析数据。
3. 使用 `gprof` 分析并显示分析数据。

在阐述这些步骤之前，我们先介绍一个足够大的程序，使分析过程变得有趣。

### A.3.1 简单的计算器

为了说明这一点，我们将使用一个简单的计算器程序。为了确保计算器花费非琐碎的时间，我们将在计算中使用一进制数（unary numbers），这是我们在现实世界的程序中绝对不会想要这么的。该程序的代码出现在本章的末尾。

一进制数用与其数值相等的符号数量表示。例如，数字 1 用 `"x"` 表示，2 用 `"xx"` 表示，3 用 `"xxx"` 表示。程序并没有使用 `x`，而是使用一个包含许多元素的链表来表示非负整数的值。数字文件包含创建数字 0、给数字加 1、从数字减去 1、加、减和乘数字的例程。另一个函数将持有非负十进制数的字符串转换为一进制数，另一个函数将一进制数转换为 `int`。加法是通过重复加 1 实现的，而减法使用重复删除 1 实现。乘法是使用重复加法定义的。一进制谓词 `even`（偶数）和 `odd`（奇数）每当且仅当一个操作数分别为偶数或奇数时，它们分别返回值为 1 的一进制数；否则，它们返回值为 0 的一进制数。这两个谓词是相互递归的。例如，如果一个数字是零，或者它减 1 是奇数，则该数字是偶数。

计算器接受单行后缀表达式并打印每个表达式的值——例如：

```
 /calculator
Please enter a postfix expression:
2 3 +
5
Please enter a postfix expression:
2 3 +
4
1
```

1. 在后置表示法中，二元运算符放在操作数之后，而不是它们之间。因此，例如，将 6 和 8 相乘，你会使用 `6 × 8`。要将 6 和 8 相乘并在结果上加 5，你会使用 `6 × 8 + 5`。

计算器定义在 `calculator.c` 中，读取每个表达式，并将中间值存储在位于 `stack.c` 中的一进制数栈上。栈以链表形式存储其一进制数。

### A.3.2 收集信息

分析程序的第一步是对其可执行文件进行注释以收集分析信息。要做到这一点，请在编译目标文件和链接时都使用 `-pg` 编译器标志。例如，考虑以下：

```
% gcc -pg -c -o calculator.o calculator.c
% gcc -pg -c -o stack.o stack.c
% gcc -pg -c -o number.o number.c
% gcc -pg -o number.o number.o -o calculator
```

这使得能够收集函数调用信息和计时信息。要收集按行的使用信息，还需指定调试标志 `-g`。要计算基本块的执行次数（例如循环迭代），使用 `-a`。

第二步是运行程序。在程序运行时，分析数据会被收集到一个名为 `gmon.out` 的文件中，但仅针对已执行的代码部分。你必须改变程序的输入或命令，以运行你想要分析的部分。程序必须正常终止才能写入分析文件。

### A.3.3 显示分析数据



给定可执行文件的名称，`gprof`会分析`gmon.out`文件以显示每个函数执行了多少时间。例如，考虑使用我们的计算器程序计算`1787 x 13 - 1918`的“平坦”（flat）分析数据，它是通过执行`gprof ./calculator`产生的：

Flat profile:

| time seconds | self seconds | self ms/call | total ms/call | decrement_number | name |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 26.07 | 1.76 | 1.34 | 20795463 | 0.00 | 1.72 add |
| 24.44 | 3.41 | 1.65 | 1792 | 0.02 | zero |
| 19.85 | 4.75 | 1.12 | 63241058 | 0.00 | zero |
| 15.11 | 5.77 | 1.02 | 1792 | 0.25 | destroy_number |
| 14.37 | 6.74 | 0.97 | 20795463 | 0.00 | add_one |
| 0.15 | 6.75 | 0.88 | 1788 | 0.01 | copy_number |
| 0.00 | 6.75 | 0.00 | 1792 | 0.00 | make_zero |
| 0.00 | 6.75 | 0.00 | 1792 | 0.00 | empty_stack |



计算函数 `decrement_number` 及其调用的所有函数需要 26.07% 的时间。此处存在重复的翻译内容。



### A.3.3 显示分析数据

给定可执行文件的名称，`gprof` 会分析 `gmon.out` 文件以显示每个函数执行了多少时间。例如，考虑使用我们的计算器程序计算 1787 x 13 - 1918 的“平坦”分析数据，它是通过执行 `gprof ./calculator` 产生的：

Flat profile:

| time seconds | self seconds | self ms/call | total ms/call | decrement_number | name |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 26.07 | 1.76 | 1.34 | 20795463 | 0.00 | 1.72 add |
| 24.44 | 3.41 | 1.65 | 1792 | 0.02 | zero |
| 19.85 | 4.75 | 1.12 | 63241058 | 0.00 | zero |
| 15.11 | 5.77 | 1.02 | 1792 | 0.25 | destroy_number |
| 14.37 | 6.74 | 0.97 | 20795463 | 0.00 | add_one |
| 0.15 | 6.75 | 0.88 | 1788 | 0.01 | copy_number |
| 0.00 | 6.75 | 0.00 | 1792 | 0.00 | make_zero |
| 0.00 | 6.75 | 0.00 | 1792 | 0.00 | empty_stack |

计算函数 `decrement_number` 及其调用的所有函数需要 26.07% 的时间。计算 `decrement_number` 函数及其其他调用的所有函数需要 26.07% 的时间。

## A.3.5 计算器程序的源代码

列表 A.3 展示了一个用于计算后置表达式求值的程序。

列表 A.3 (`calculator.c`) 主计算器程序

```c
/* 使用一元数进行计算。 */

/* 使用逆波后置表示法输入单行表达式，例如：
602 7 5 3 *
非负数使用十进制法输入。
支持
运算符 '+'、'-' 和 '*'。一元运算符
"even" 和 "odd" 分别在其操作数为偶数或奇数时
返回数字 1。所有单词之间必须用空格分隔。
不支持负数。 */

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#include "definitions.h"

/* 从栈中获取操作数并应用二元函数，
将结果推入栈中。成功时返回非零。 */

int apply_binary_function(number (*function)(number, number), Stack *stack)
{
    number operand1, operand2;
    if (empty_stack (*stack))
        return 0;
    operand2 = pop_stack(stack);
    if (empty_stack (*stack))
        return 0;
    operand1 = pop_stack(stack);
    push_stack(stack, (*function)(operand1, operand2));
    destroy_number(operand1);
    destroy_number(operand2);
    return 1;
}

/* 从栈中获取操作数并应用一元函数，
将结果推入栈中。成功时返回非零。 */

int apply_unary_function(number (*function)(number), Stack *stack)
{
    number operand;
    if (empty_stack (*stack))
        return 0;
    operand = pop_stack(stack);
    push_stack(stack, (*function)(operand));
    destroy_number(operand);
    return 1;
}

int main () {
    char command_line[1000];
    char* command_to_parse;
    char* token;
    Stack number_stack = create_stack ();

    while (1) {
        printf("Please enter a postfix expression:\n");
        if (fgets(command_line, sizeof(command_line), stdin) == NULL)
            break;
        
        command_to_parse = strtok(command_line, " \t\n");
        if (command_to_parse == NULL)
            return 0;

        while (token != NULL) {
            if (isdigit(token[0])) {
                push_stack (&number_stack, string_to_number (token));
            } else if ((strcmp(token, "+") == 0) &&
                        !apply_binary_function(&add, &number_stack)) ||
               (strcmp(token, "-") == 0) &&
                        !apply_binary_function(&subtraction, &number_stack)) ||
               (strcmp(token, "*") == 0) &&
                        !apply_binary_function(&product, &number_stack)) ||
               (strcmp(token, "/") == 0) &&
                        !apply_binary_function(&division, &number_stack)) ||
               (strcmp(token, "even") == 0) &&
                        !apply_unary_function(&even, &number_stack)) ||
               (strcmp(token, "odd") == 0) &&
                        !apply_unary_function(&odd, &number_stack)) {
                return 1;
            }
            token = strtok(NULL, " \t\n");
        }
        if (empty_stack(number_stack))
            return 1;
        else {
            number answer = pop_stack (&number_stack);
            printf("%u\n", number_to_unsigned_int (answer));
            destroy_number(answer);
            clear_stack (&number_stack);
        }
    }
    return 0;
}
```

## 附录 A 其他开发工具

列表 A.4 中的函数使用空链表实现了一元数。



# 列表 A.4 (number.c) 一元数实现

```c
/* 对一元数进行操作。 */

#include <assert.h>
#include <stdlib.h>
#include <limits.h>
#include "definitions.h"

/* 创建一个表示零的数字。 */
number make_zero ()
{
    return 0;
}

/* 如果数字表示零，则返回非零。 */
int zerop (number n)
{
    return n == 0;
}

/* 将一个正数减 1。 */
number decrement_number (number n)
{
    number answer;
    assert (zerop (n));
    answer = n->one_less_;
    free (n);
    return answer;
}

/* 给数字加 1。 */
number add_one (number n)
{
    number answer = malloc(sizeof (struct LinkedListNumber));
    answer->one_less_ = n;
    return answer;
}

/* 销毁一个数字。 */
void destroy_number (number n)
{
    while (!zerop (n)) {
        n = decrement_number (n);
    }
    free(n);
}

/* 拷贝一个数字。需要此函数仅是因为内存分配的原因。 */
number copy_number (number n)
{
    number answer = make_zero ();
    while (!zerop (n)) {
        answer = add_one (answer);
        n = decrement_number (n);
    }
    return answer;
}

/* 相加两个数字。 */
number add (number n1, number n2)
{
    number answer = copy_number (n2);
    while (!zerop (n1)) {
        answer = add_one (answer);
        n1 = decrement_number (n1);
    }
    return answer;
}

/* 从另一个数字中减去一个。 */
number subtraction (number n1, number n2)
{
    number answer = copy_number (n1);
    while (!zerop (n2)) {
        answer = decrement_number (answer);
    }
    return answer;
}

/* 返回两个数字的积。 */
number product (number n1, number n2)
{
    // 实现省略以保持简练
    return 0;
}
```

## B 低级 I/O (输入输出)

`GNU/Linux` 上的程序员可以使用两套输入/输出函数。标准 C 库 I/O 函数提供了 `printf`、`fopen` 等函数¹。`Linux` 内核本身提供了另一组 I/O 操作，其运行级别比 C 库函数更低。

由于本书是为已经熟悉 C 语言的人编写的，我们假设你已经遇到过并知道如何使用 C 库 I/O 函数。

通常有充分的理由使用 `Linux` 的底层 I/O 函数。其中许多是内核系统调用，为应用程序提供了对底层能力最直接的访问。事实上，标准 C 库 I/O 程序是实现在 `Linux` 低级 I/O 系统调用之上的。使用后者通常是执行输入输出操作最高效的方法——有时也更加方便。

- + 1. C++ 标准库提供了具有类似功能的 `istream`。C++ 语言同样可以使用标准 C 库。
- 2. 请参阅第 8 章“`Linux` 系统调用”，了解系统调用与普通函数调用之间的区别。

在本书中，我们假设你熟悉本附录中所描述的调用。你可能已经熟悉了它们，因为它们与其他 `UNIX` 和类 `UNIX` 操作系统（以及 `Win32` 平台）提供的调用几乎相同。然而，如果你不熟悉，请继续读下去；如果你先熟悉这些材料，你会发现本书的其他部分更容易理解。

### B.1 读取和写入数据

你在学习 C 语言时可能遇到的第一个 I/O 函数是 `printf`。它将格式化一个文本字符串并将其打印到标准输出。通用版本 `fprintf` 可以将文本打印到标准输出以外的流中。流由 `FILE*` 指针表示。你通过 `fopen` 打开文件来获取 `FILE*` 指针。除了 `fprintf`，你还可以用 `fclose` 关闭它。你可以使用 `fput`、`fputs` 和 `fwrite` 等函数向流写入数据，或使用 `scanf`、`fscanf`、`gets` 和 `fread` 读取数据。

使用 `Linux` 低级 I/O 操作时，你使用称为文件描述符（file descriptor）的句柄而不是 `FILE*` 指针。文件描述符是一个整数，指向单个进程中的特定打开文件。它可以以读、写或读写模式打开。文件描述符并不一定指向一个打开的文件；它也可以代表与能够发送或接收数据的另一个系统组件的连接。例如，请参阅第 6 章“设备”，如打开的套（见第 5 章“进程间通信”，第 5.5 节“`Sockets`”）或管道的一端（见第 5.4 节“`Pipes`”）。

如果你使用此处描述的任何低级 I/O 函数，请包含头文件 `<stdio.h>`、`<sys/types.h>`、`<sys/stat.h>` 和 `<unistd.h>`。

#### B.1.1 打开文件

要打开文件并生成访问该文件的描述符，使用 `open` 调用。它以文件路径（字符字符串）和指定打开方式的标志作为参数。你可以使用 `open` 创建新文件；如果是这样，传递第三个参数来指定新文件的访问权限。

如果第二个参数是 `O_RDONLY`，则文件以只读模式打开；如果你随后尝试写入生成的文件描述符，将会报错。同样，`O_WRONLY` 导致文件描述符为只写。指定 `O_RDWR` 会产生一个可以同时读取和写入的文件描述符。注意，并非所有文件都可以在所有三种模式下打开。例如，文件的权限可能会禁止特定进程以读或写方式打开；只读设备（如 `CD-ROM` 驱动器）上的文件可能无法以写打开。

你可以通过将此值与一个或多个标志进行位或运算来指定额外的选项。这些是最常用的值：

- `O_TRUNC`：如果打开的文件之前存在，则将其截断。写入文件描述符的数据将替换文件之前的内容。
- `O_APPEND`：向现有文件追加内容。写入文件描述符的数据将将添加到文件末尾。
- `O_CREATE`：创建一个新文件。如果你提供给 `open` 的文件名不存在，且该文件目录存在且进程有权限在该目录下创建文件，则将创建一个新文件。如果文件已存在，则打开它。
- `O_EXCL` 配合 `O_CREATE` 使用，强制创建一个新文件。如果文件已存在，调用将失败。

如果你带有 `O_CREATE` 调用 `open`，请提供一个额外的参数来指定新文件的权限。请参阅第 10 章“安全”，第 10.3 节“文件系统权限”，获取权限位及其使用方法的描述。

例如，列表 B1 中的程序根据命令行上指定的文件名创建一个新文件。如果你在调用 `open` 时使用 `O_EXCL` 标志，那么如果文件已存在，就会发生错误。新文件将赋予所有者和所属组读写权限，并仅赋予其他人读取权限（如果你的 `umask` 设置为非零值）。

#### Umasks

当你创建一个文件时，`umask` 决定了权限。`umask` 被设置为非零值。要更改 `umask`，请使用 `umask` 命令并指定数值。例如，`umask 0022` 设置权限，使所有者具有读写访问权限，而组和其他人只有读取权限。

要更改 `umask`，请使用 `umask` 命令并指定数值。例如，`umask 0022` 设置权限，使所有者具有读写访问权限，而组和其他人只有读取权限。

`umask` 是一个掩码，用于从新创建的文件中屏蔽某些权限。例如，如果 `umask` 为 0022，用权限 0666 创建的文件将具有 0644 (`rw-r--r--`) 权限。

`umask` 是一个掩码，用于从新创建的文件中屏蔽某些权限。例如，如果 `umask` 为 0022，用权限 0666 创建的文件将具有 0644 (`rw-r--r--`) 权限。

#### B.1.2 关闭描述符

当你完成文件描述符的操作后，应该关闭它。在某些情况下（如 B1 中的程序），没有必要显式关闭，因为进程会终止。

`Linux` 限制了进程同时允许打开的文件描述符数量。典型的限制是每个进程 1024 个描述符。你可以使用 `setlimit` 系统调用调整此限制；请查看第 8.5 节“`getlimit` 和 `setlimit`”获取更多信息。

#### B.1.3 写入数据

使用文件描述符、缓冲区指针和写入字节数向文件描述符写入数据。文件描述符必须已打开。写入的数据不需要字符串；`write` 将任意字节复制到文件描述符。

列表 B2 中的程序将当前时间追加到命令行指定的。。如果文件不存在，则会创建它。此程序还使用了 `time`、`localtime` 和 `ctime` 函数来获取并格式化当前时间；请查看各自的手页（man pages）获取更多信息。

##### 附录 B 代码示例

```c
char* get_timestamp() {
    time_t now = time(NULL);
    return asctime(localtime(&now));
}

int main (int argc, char *argv[]) {
    /* 要追加时间戳的文件。 */
    char *filename = argv[1];
    /* 获取当前时间戳。 */
    char *timestamp = get_timestamp();
    /* 以写模式打开文件。如果存在则追加；否则创建一个新文件。 */
    int fd = open(filename, O_WRONLY | O_CREATE | O_APPEND, 0666);
    /* 计算时间戳字符串的长度。 */
    size_t length = strlen(timestamp);
    /* 将时间戳写入文件。 */
    write(fd, timestamp, length);
    /* 完成。 */
    close(fd);
    return 0;
}
```

`## 286 附录 B 低级 I/O`

以下 `timestamp` 程序的工作原理如下：

```bash
% ./timestamp tsfile
% cat tsfile
Thu Feb 1 23:25:20 2001
% ./timestamp tsfile
% cat tsfile
Thu Feb 1 23:25:20 2001
Thu Feb 1 23:25:47 2001
```

注意，当我们第一次调用 `timestamp` 时，它创建文件 `tsfile`，而第二次调用时则是追加到该文件中。

`write` 调用返回实际写入的字节数，如果发生错误则返回 -1。对于某些类型的文件描述符，写入的字节数可能少于请求的字节数。在这种情况下，由你再次调用 `write` 来写入剩余数据。函数 B.3 演示了如何这样做。请注意，对于某些应用程序，你可能需要在写入操作中间检查特殊情况。例如，如果你正在向网络套接字写入，你必须增强此函数以检测网络连接是否在写入操作过程中已关闭，如果是，则必须做出适当反应。

##### 列表 B.3 `(write-all.c)` 写入缓冲区中的所有数据

```c
/* 将 BUFFER 中的所有 COUNT 字节写入文件描述符 FD。
   出错时返回 -1，或返回写入的字节数。 */

size_t write_all(int fd, const void* buffer, size_t count)
{
    size_t left_to_write = count;
    while (left_to_write > 0) {
        size_t written = write(fd, buffer, count);
        if (written == -1)
            /* 发生错误；退出。 */
            return -1;
        else
            /* 记录我们还需要写入多少字节。 */
            left_to_write -= written;
    }
    /* 我们写入的内容应该超过 COUNT 字节！ */
    assert(left_to_write == 0);
    /* 写入的字节数正好等于 COUNT。 */
    return count;
}
```

#### B.1.4 读取数据

读取数据的对应调用是 `read`。像 `write` 一样，它接受一个文件描述符、一个缓冲区指针和一个计数。计数器指定了从文件描述符读取到缓冲区中的字节数。`read` 调用在出错时返回 -1，或返回实际读取的字节数。这可能小于请求的字节数，例如，如果文件中剩余的字节数不足。

##### 读取 DOS/Windows 文本文件

在读完这本书后，我们非常确定你会选择为 `GNU/Linux` 编写所有的程序。你的程序偶尔可能需要读取由 `DOS` 或 `Windows` 程序生成的文本文件。预判这两个平台之间文本文件结构上的重要差异是非常重要的。

在 `GNU/Linux` 编辑器中，每行都通过换行符与下一行分隔。换行符由字符常量 `'\n'` 表示，其 ASCII 码为 10。然而，行之间是由两个字符组合分隔的：一个回车（字符 `'\r'`，其 ASCII 码为 13），后跟一个换行符。

某些 `GNU/Linux` 文本编辑器在显示 `Windows` 文本文件时，会在每行尾显示 '`M`'——这就是回车字符。`Em` 能正确显示 `Windows` 文本文件，但通过在缓冲区底部的状态行中显示 `(DOS)` 来指示它们。某些编辑器（如记事本）会将 `GNU/Linux` 文本文件中的所有文本显示在单行，因为它们期望每行尾有一个回车。处理 `GNU/Linux` 和 `Windows` 文本文件的其他程序在输入格式错误的文本文件时，可能会报告某些神秘的错误。

如果你的程序读取由 `Windows` 程序生成的文本文件，你可能希望将序列 `'\r\n'` 替换为单个换行符。同样，如果你的程序编写所需的 `Windows` 程序读取的文本文件，请将单独的换行符替换为 `'\r\n'` 组合。无论你是使用本文介绍的底层 I/O 调用还是标准库 I/O 函数，都必须这样做。

列表 B.4 提供了 `read` 的简单演示。该程序输出命令行指定的文件的内容的十六进制转储。每行显示文件中的偏移量和后续 6 个字节。

##### 列表 B.4 `(hexdump.c)` 打印文件的十六进制转储

```c
#include <fcntl.h>
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
  unsigned char buffer[16];
  size_t offset = 0;
  size_t bytes_read;
```

`Hexdump` 运行示例。它显示正在打印其自身可执行文件的转储：

```text
% ./hexdump
0x000000: 7f 45 4c 4f 46 01 01 00 00 00 00 00 00 00 00 00
0x000010: 02 00 03 00 01 01 00 00 c8 03 04 08 34 00 00 00
0x000020: e6 23 01 00 00 00 00 00 00 00 00 00 00 00 00 00
0x000030: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
```

`Hexdump` 运行示例。它显示正在打印其自身可执行文件的转储：

你的输出可能不同，取决于你如何编译 `hexdump`。

## B.2 stat（系统调用）

通过 `open` 和 `read`，你可以提取文件的内容。但其他信息呢？例如，调用 `ls -1` 会显示当前目录下的文件信息，如文件大小、最后修改时间、权限和所有者。

`stat` 调用用于获取文件信息。调用时传入你感兴趣的文件路径和一个指向 `struct stat` 类型变量的指针。如果 `stat` 调用成功，它将返回 0 并用该文件的信息填充结构体的字段；否则，它返回 -1。

以下是 `struct stat` 中最实用的字段：

- `st_mode` 包含文件的访问权限。文件权限在第 10.3 节“文件权限”中解释。
- 除了访问权限外，`st_mode` 字段在高位中编码了文件类型。请参阅此列表随后的文本获取有关解码这些信息的说明。
- `st_uid` 和 `st_gid` 分别包含文件所属的用户 ID 和组 ID。用户 ID 和组 ID 在第 10.1 节“用户和组”中描述。
- `st_size` 包含文件的大小，单位为字节。
- `st_atime` 包含文件最后被访问（读取或写入）的时间。
- `st_mtime` 包含文件被修改的时间。

这些宏检查 `st_mode` 字段的值以确定你调用的是什么种类型的文件。如果文件属于该类型，则宏为真。

```
S_ISBLK (mode) 块设备
S_ISCHR (mode) 字符设备
S_ISDIR (mode) 目录
S_ISFIFO (mode) fifo (命名管道)
S_ISLN (mode) 符号链接
S_ISREG (mode) 普通文件
S_ISSOCK (mode) socket
```



`st_dev` 字段包含文件所在硬件设备的主设备和次设备号。设备号在第 6 章中进行了讨论。主设备号左移 8 位；次设备号占用低位。`st_ino` 字段包含该文件的 `inode` 号（节点号）。这在文件系统中定位该文件。

## 附录 B 低层 I/O

如果你对符号链接进行调用，`stat` 会跟随该链接，你可以获取链接所指向的文件信息，而不是链接本身的信息。这意味着对于 `stat` 的结果，`S_ISNK` 永远为假。如果你不想跟随符号链接，请使用 `lstat` 函数；该函数获取链接本身的信息，而不是链接的目标。如果你对非符号链接的文件调用 `lstat`，其效果等同于 `stat`。对断开的链接（指向不存在或不可访问目标的链接）进行调用会导致错误，而对这种链接调用 `lstat` 则不会。

如果你已经有一个文件描述符作为第一个参数进行读或写操作，请调用 `fstat` 而不是 `stat`。列表 B.6 展示了一个函数，它分配一个足够容纳文件内容的缓冲区，然后将其读入。该函数使用 `fstat` 来确定需要分配的缓冲区大小，并检查该文件确实是一个普通文件。

### 列表 B.6 (read_file.c) 将文件读入缓冲区

```c
#include <fcntl.h>
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>
```

```c
/* 将内容读入新分配的缓冲区。

缓冲存的大小存储在 LENGTH 中。返回缓冲区，

调用者必须释放它。如果 FILENAME 不对应于

普通文件，则返回 NULL。 */

char* read_file(const char* filename, size_t* length)

{

    int fd;

    struct stat file_info;

    char* buffer;

    /* 打开文件。 */

    fd = open(filename, O_RDONLY);

    /* 获取文件信息。 */

    fstat(fd, &file_info);

    *length = file_info.st_size;

    /* 确保文件是一个普通文件。 */

    if (!S_ISREG(file_info.st_mode)) {

        /* 如果不是，则放弃。 */

        close(fd);

        return NULL;

    }

    /* 分配一个足够容纳文件内容的缓冲区。 */

    buffer = (char*) malloc(length);

    /* 将文件读入缓冲区。 */

    read(fd, buffer, length);

    /* 完成工作。 */

    close(fd);

    return buffer;

}
```

## B.3 向量读写

`write` 调用接受的参数是指向数据缓冲区起始位置指针以及该缓冲区的长度。它将连续的内存区域写入文件描述符。`writev` 调用允许你在单次操作中写入多个不连续的内存区域，这比多次调用 `write` 效率更高。

### 列表 B.7 (write-args.c) 使用 writev 将参数列表写入文件

```c
#include <fcntl.h>
#include <stdlib.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <sys/uio.h>
#include <unistd.h>

int main (int argc, char * argv[])
{
    int fd;

    struct iovec *vec;

    struct iovec *vec_next;

    int i;

    /* 我们需要一个包含换行符的'buffer'。使用
       普通的字符变量来实现。 */

    char newline = '\n';

    /* 第一个命令行参数是输出文件名。 */

    char * filename = argv[1];

    /* 跳过参数列表的前两个元素。元素
       0 是程序的名称，元素 1 是输出
       文件名。 */

    argc = 2;

    argv = 2;

    /* 分配一个 iovec 元素数组。参数列表中的
       每个元素我们需要两个，一个用于文本本身，
       一个用于换行符。 */

    vec = (struct iovec *) malloc(2 * argc * sizeof(struct iovec));

    /* 遍历参数列表，构建 iovec 条目。 */

    vec_next = vec;

    for (i = 0; i < argc; i++) {
        /* 第一个元素是参数本身的文本。 */

        vec_next->iov_base = argv[i];

        vec_next->iov_len = strlen(argv[i]);

        ++vec_next;

        /* 第二个元素是单个换行符。struct iovec
           数组中的多个元素指向同一内存区域           是允许的。 */

        vec_next->iov_base = &newline;

        vec_next->iov_len = 1;

        ++vec_next;
    }

    /* 将参数写入文件。 */

    fd = open(filename, O_WRONLY | O_CREAT);

    writev(fd, vec, 2 * argc);

    free(vec);

    close(fd);

    return 0;
}
```

## B.4 与标准C库 I/O 函数的关系

这里是运行 `write-args` 的示例。

```
% ./write-args outputfile "first arg" "second arg" "third arg"
% cat outputfile
first arg
second arg
third arg
```

Linux 提供了一个相应的函数 `readv`，它可以在单次操作中将数据读取到多个不连续的内存区域。与 `writev` 类似，一个 `iovec` 元素数组指定了将从文件描述符读取数据的内存区域。

我们之前提到过，标准 C 库 I/O 函数是在这些低级 I/O 函数之上实现的。有时，结合文件描述符使用标准库函数是困难的，或者在标准库的 `FILE*` 流上使用低级 I/O 函数也很困难。GNU/Linux 允许你同时完成这两者。

如果你使用 `fopen` 打开了一个文件，可以使用 `fileno` 函数获取底层的文件描述符。该函数接受一个 `FILE*` 参数并返回文件描述符。例如，为了使用标准库的 `open` 调用打开文件但使用 `writev` 写入，你可以使用以下代码：

```c
FILE* stream = fopen (filename, "w");

int file_descriptor = fileno (stream);

write (file_descriptor, vector, vector_length);
```

注意 `stream` 和 `file_descriptor` 对应于同一个打开的文件。如果你调用了这一行，你可能无法再向 `file_descriptor` 写入：

```c
close (stream);
```

同样，如果你调用了这一行，你可能无法再向 `stream` 写入：

```c
close (file_descriptor);
```

要进行反向操作，即从文件描述符到流，请使用 `fdopen` 函数。它会构造一个与文件描述符对应的 `FILE*` 流指针。`fdopen` 函数接受一个文件描述符参数和一个指定创建流的模式的字符串参数。模式参数的语法与 `fopen` 的第二个参数相同，并且必须与文件描述符兼容。例如，为读文件描述符指定模式 `r`，或为写文件描述符指定模式 `w`。

与 `fclose` 一样，流和文件描述符指向同一个打开的文件，因此如果你关闭了其中一个，可能就无法再使用另一个。

## B.5 其他文件操作

一些其他对文件和目录的操作也很有用：

- `getcwd` 获取当前工作目录。它接受两个参数：一个 `char` 缓冲区和缓冲区长度。它将当前工作目录的路径拷贝到缓冲区中。
- `chdir` 将当前工作目录更改为参数提供的路径。
- `mkdir` 创建新目录。它的第一个参数是新目录的路径。第二个参数是用于新文件的访问权限。权限的解释与 `open` 调用的第三个参数相同，并会被进程的 `umask` 修改。
- `rmdir` 删除目录。它的参数是目录的路径。
- `unlink` 删除文件。它的参数是文件的路径。此调用也可用于删除其他文件系统对象，例如命名管道（"FIFOs"）或设备（见第 6 章）。实际上，`unlink` 并不一定删除文件的内容。正如其名所示，它将文件从包含它的目录中取消链接。该文件不再列在目录中，但如果有任何进程持有该文件的打开文件描述符，文件的内容就不会从磁盘中移除。因此，如果一个进程打开一个文件进行读写，然后第二个进程 `unlink` 了该文件并创建一个同名的新文件，第一个进程将看到文件的旧内容而不是新内容（除非它关闭文件并重新打开）。
- `rename` 重命名或移动文件。它的两个参数是文件的旧路径和新路径。如果路径在不同的目录中，`rename` 会移动文件，只要它们都在同一个文件系统上。你也可以使用 `rename` 移动目录或其他文件系统对象。

## B.6 读取目录内容

GNU/Linux 提供了读取目录内容的函数。虽然这些与本附录描述的低级 I/O 函数没有直接关系，但我们仍然在这里展示了它们，因为它们在应用程序中经常有用。

要读取目录内容，请遵循以下步骤：

1. 调用 `opendir`，传递要检查的目录路径。`opendir` 返回一个 `DIR*` 句柄，你用它访问目录内容。如果发生错误，调用返回 `NULL`。
2. 重复调用 `readdir`，传递从 `opendir` 获取的 `DIR*` 句柄。每次调用 `readdir` 时，它都会返回一个指向下一个目录条目的 `struct dirent` 实例的指针。当到达目录末尾时，`readdir` 返回 `NULL`。从 `readdir` 获取的 `struct dirent` 有一个字段 `d_name`，它包含目录条目的名称。
3. 调用 `closedir` 并传递 `DIR*` 句柄，结束目录列表操作。

如果你在程序中使用这些函数，请包含 `<sys/types.h>` 和 `<dirent.h>`。注意，如果你需要按特定顺序排列目录内容，必须自己进行排序。

列表 B.8 中的程序打印目录内容。可以在命令行指定目录，但如果没有指定，程序将使用当前目录。对于目录中的每个条目，它会显示类型和路径。

### 列表 B.8 打印列表

```c
#include <assert.h>
#include <dirent.h>
#include <stdio.h>
#include <string.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>
#include <stdlib.h>

/* 返回描述文件类型的字符串 */

const char* get_type(const char* path) {
    struct stat st;
    stat(path, &st);
    if (S_ISLNK(st.st_mode))
        return "symbolic link";
    else if (S_ISDIR(st.st_mode))
        return "directory";
    else if (S_ISCHR(st.st_mode))
        return "character device";
    else if (S_ISBLK(st.st_mode))
        return "block device";
    else if (S_ISFIFO(st.st_mode))
        return "fifo";
    else if (S_ISSOCK(st.st_mode))
        return "socket";
    else if (S_ISREG(st.st_mode))
        return "regular file";
    else
        return "unknown";
}

int main(int argc, char *argv[]) {
    char *dir_path;
    DIR *dir;
    struct dirent *entry;
    char entry_path[PATH_MAX];
    size_t path_len = 2;

    /* 在命令行上指定了目录，使用它 */
    if (argc >= 2) {
        dir_path = argv[1];
    } else {
        /* 否则，使用当前目录 */
        dir_path = ".";
    }

    /* 将目录路径拷贝到 entry_path */
    strncpy(entry_path, dir_path, sizeof(entry_path));
    path_len = strlen(entry_path);

    /* 如果路径不以斜杠结尾，添加一个 */
    if (entry_path[path_len-1] != '/') {
        entry_path[path_len] = '/';
        entry_path[path_len+1] = '\0';
    }
    path_len++;

    /* 开始对指定的目录列表 */
    dir = opendir(dir_path);

    /* 遍历所有目录条目 */
    while ((entry = readdir(dir)) != NULL) {
        /* 通过拼接名称构建条目的路径 */
        strncpy(entry_path + path_len, entry->d_name, sizeof(entry_path) - path_len);

        /* 确定条目的类型 */
        const char *type = get_type(entry_path);

        /* 打印条目的类型和路径 */
        printf("%-18s: %s\n", type, entry_path);
    }

    /* 全部完成 */
    closedir(dir);

    return 0;
}
```

这里列出 `/dev` 目录的前几行输出。（你的输出可能略有不同。）

```
% ./listdir /dev

total 124

drwxr-xr-x 7 root root 36864 Feb 1 15:14 .

drwxr-xr-x 22 root root 4096 Oct 11 16:39 ..

crw-rw-rw- 1 root root - Dec 10 01:31:3 log

crw-rw-rw- 1 root root 1, 3 May 1998 null

-rw-rw--x 1 root root 26689 Mar 2 2000 MAKEDEV

prw------- 1 root root 0 Dec 11 18:37 initctl

crw-rw-rw- 1 root root 10, 175 Feb 3 2000 agpgart

...
```

`ls` 输出中每行的第一个字符表示条目的类型。

## 信号列表

表 C.1 列出了你最可能遇到或使用的 Linux 信号。请注意，某些信号具有多种解释，具体取决于它们发生的位置。

此处列出的信号名称被定义为预处理器宏。要在你的程序中使用它们，请包含 `<usr/include/sys/signal.h>`，该文件是 `<signal.h>` 的一部分。

要获取 Linux 信号的完整列表（包括每个信号的简要描述以及信号传递时的默认行为），请通过以下命令查看第 7 节的帮助页：

```
% man 7 signal
```



| 名称 | 描述 |
| --- | --- |
| `SIGHUP` | 当进程与终端断开连接时，Linux 向其发送进程信号。许多 Linux 程序将 `SIGHUP` 用于另一个无关目的：指示正在运行的程序它应该重新读取配置文件。 |
| `SIGINT` | 当用户尝试通过按下 `Ctrl+C` 结束程序时，Linux 向其发送此信号。 |
| `SIGILL` | 当进程尝试执行非法指令时会收到此信号。这可能表明程序的栈已损坏。 |
| `SIGABRT` | `abort` 函数会导致进程接收此信号。 |
| `SIGFPE` | 进程执行了无效的浮点数学指令。根据 CPU 的配置，无效的浮点操作可能会返回特殊的非数字值，如 `inf`（无限大）或 `NaN`（非数字），而不是触发 `SIGFPE`。 |
| `SIGKILL` | 此信号立即终止进程且无法被处理。 |
| `SIGUSR1` | 此信号保留供应用程序使用。 |
| `SIGUSR2` | 此信号保留供应用程序使用。 |
| `SIGSEGV` | 程序尝试进行无效的内存访问。该访问可能是指向进程虚拟内存中无效的地址，或者访问被目标内存的权限禁止。解引用“野指针”可能会导致 `SIGSEGV`。 |
| `SIGPIPE` | 程序尝试访问已损坏的数据流，例如已被对方关闭的 socket。 |
| `SIGALRM` | 闹钟调用调度在稍后传递此信号。有关 `setimer`（`alarm` 的通用版本），请参阅第 8 章“Linux 系统调用”中的第 8.13 节“`setimer`: 设置间隔定时器”。 |
| `SIGTERM` | 此信号请求进程终止。这是 `kill` 命令发送的默认信号。 |
| `SIGCHLD` | 当子进程退出时，Linux 向其发送此进程信号。请参阅第 3 章“进程”中的第 3.4.4 节“异步清理清理”。 |
| `SIGXCPU` | 当进程超过其允许消耗的 CPU 时间限制时，Linux 向其发送此信号。有关 CPU 时间限制，请参阅第 8 章第 8.5 节“`getrlimit` 和 `setrlimit`: 资源限制”。 |
| `SIGVTALRM` | `setimer` 在未来时间调度此信号。请参阅第 8.13 节“`setimer`: 设置间隔定时器”。 |

## 在线资源

本附录列了一些可以在网上访问的地方，以学习更多关于 GNU/Linux 系统的编程。

### D.1 普通信息

- `http://www.advancedlinuxprogramming.com` 是本书在互联网上的主页。在这里，你可以下载本书的全文和程序源代码，找到指向其他在线资源的链接，并获取更多关于 GNU/Linux 编程的信息。同样的信息也可以 `http://www.newriders.com` 找到。
- `http://www.linuxdoc.org` 是 Linux 文档项目（Linux Documentation Project）的主页。该网站是存储丰富的文档、FAQ 列表、HOWTO 以及其他关于 GNU/Linux 系统和软件文档的仓库。

### D.2 关于 GNU/Linux 软件的信息

- `http://www.gnu.org` 是 GNU 项目的主页。从该网站，你可以下载海量复杂的自由软件应用程序。其中包含 GNU C 库（GNU C library），它是每个 GNU/Linux 系统的一部分，并包含了本书中描述的许多函数。GNU 项目还提供了有关你如何通过编写代码或文档、使用自由软件以及传播自由软件理念为 GNU/Linux 系统的开发做出贡献的信息。
- `http://www.kernel.net` 是 Linux内核源码分发的主要网站。对于关于 Linux 如何的最棘手和技术细节最详尽的问题，源代码是最好的查找处。此外请查看 `Documentation` 目录以了解内核原理。
- `http://www.linuxux.com` 也分发内核源码、补丁和相关信息。
- `http://gcc.gnu.org` 是 GNU 编译器集（GCC）的主页。GCC 是 GNU/Linux 系统上使用的主要编译器，包含了用于 C、C++、Objective C、Java、Chill 和 Fortran 的编译器。
- `http://www.gnome.org` 和 `http://www.kde.org` 是最流行的窗口环境主页。

### D.3 其他网站

- `http://www.intel.com` 提供关于 x86 架构的信息。
- `http://amd.com/dev` 提供关于 AMD处理器的信息。
- `http://freshmeat.net` 提供关于 Linux 安全的信息。
- `http://www.linuxsecurity.com` 包含安全技术。
- `http://www.opentent.org/openpub/`

## 附录 E 开放出版许可证版本 1.0

### I. 版权

每个开放出版物的版权归其作者或指定人所有。

### II. 许可范围

除非文档另有明确说明，以下许可条款适用于所有开放出版作品。仅仅在同一媒体上聚合开放出版物或其部分不会导致本许可适用于其他作品。聚合作品应包含一个说明包含开放出版物的通知和版权声明。

- **可分割性**。如果许可的任何部分在任何司法管辖区被认为不可执行，许可的其余部分仍然有效。
- **无保证**。开放出版物按“现状”提供，不提供任何形式的明示或隐含保证，包括但不限于对可销性和特定用途适用性的保证，以及对不侵权的保证。

### III. 修改作品的要求

所有受本许可保护的文档修改版本（包括翻译、文集、编译和部分文档）必须满足以下要求：

- 必须标识修改者，并注明修改日期。
- 必须按照学术引用习惯保留原作者和出版者的认可（如果适用）。
- 必须标识原始未修改文档的位置。
- 未经原作者（或作者）许可，不得使用原作者姓名来声称或暗示对结果文档的支持。

### IV. 对未修改和修改作品的要求

在遵守许可条款的前提下，可以在任何媒介（物理或电子）上全部或部分复制分发开放出版物。版权所有 `<年份>` `<作者姓名>`。在标准纸质格式中，出版者的名称应出现在书的所有表面。

### V. 良好实践建议

除了本许可的要求，要求并强烈建议分发者：

- 如果你在纸质或 CD-ROM 上分发开放出版物，你必须在稿件或媒体冻结前 30 天向作者发送电子邮件通知你的分发意图，以便给作者留出更新文档的时间。此通知应描述对文档的任何修改。

- 所有的实质性修改（包括删除）要么在文档中被明确标记，要么在文档的附件中进行描述。

- 最后，尽管本许可并非强制要求，但向作品作者（们）提供任何受“开放出版”（Open Publication）许可作品的纸质版和 CD-ROM 形式的免费副本被认为是一种良好的做法。

## VI. 许可选项

受开放出版许可文档的作者（或）或出版者可以在许可的引用或副本后附加语言来选择某些选项。这些选项被视为许可实例的一部分，并且必须在衍生作品中与许可（或通过引用包含许可）一并。

- A. 禁止在没有作者（们）明确许可的情况下分发经过实质性修改的版本。“实质性修改”被定义为对文档语义内容的更改，但不包括格式的更改或拼写纠正。

  要实现这一点，请在许可引用或副本中添加短语“未经版权所有者明确许可，禁止分发本文档的实质性修改版本”。

- B. 除非事先获得版权所有者的许可，否则禁止以标准（纸质）书籍的形式为了商业目的出版本作品或其衍生作品整体或部分。

  要实现这一点，请在许可引用或副本中添加短语“未经版权所有者事先许可，禁止以任何标准（纸质）书籍形式分发作品或其衍生作品”。

## 开放出版政策附录

（此部分不视为许可的一部分）

开放出版作品可以通过开放出版主页 `http://works.opencontent.org/` 以源码格式获取。

希望在自己的开放出版作品中包含其自定义许可的开放出版作者可以这样做，只要其条款不比开放出版许可严格。

如果您对“开放出版列表”有疑问，请通过电子邮件联系 David Wiley，或通过 `opal@opencontent.org` 联系开放出版作者列表。

要订阅开放出版作者列表，请向 `opal-request@opencontent.org` 发送邮件，并在正文中包含“`subscribe`”字样。

要在开放出版作者列表中发布帖子，请向 `opal@opencontent.org` 发送邮件，或直接回复之前的帖子。

要从开放出版作者列表中取消订阅，请向 `opal-request@opencontent.org` 发送邮件，并在正文中包含“`unsubscribe`”字样。

# GNU 通用公共许可证

第 2 版，1991 年 6 月

版权所有 © 1989, 1991 Free Software Foundation, Inc.
59 Temple Place-Suite 330, Boston, MA 02111-1307, USA

每个人允许复制和分发本文档的原样副本，但不允许对其进行更改。

## 前言

大多数软件的许可旨在剥夺您分享和更改它的自由。相比之下，GNU 通用公共许可证旨在保证您分享和更改自由软件的自由——让软件对所有用户都是自由的。通用公共许可证适用于自由软件会的大部分软件，以及任何承诺使用它的其他程序。（某些其他自由软件则由 GNU 库通用公共许可证覆盖。）您也可以将其应用于您的程序。

当我们谈论自由软件时，我们指的是自由，而不是价格。我们的通用公共许可证旨在确保您有自由分发自由软件副本（如果您愿意，可以为此服务收取费用），您有自由接收源代码或在需要时获取源代码的自由；您可以在新的自由程序中更改软件或其部分；并且您知道自己可以做这些事情。

1. 本许可证可以在网上找到：`http://www.gnu.org/copyleft/gpl.html`。

为了保护您的权利，我们需要制定一些限制，禁止任何人剥夺您的这些权利或要求您放弃这些权利。这些限制意味着，如果您分发软件副本或对其进行修改，则将承担相应的责任。

例如，如果您分发此类程序的副本（无论是免费还是付费），您都必须向接收者提供您所拥有的权利。您必须确保他们也接收或获取源代码。并且必须向他们展示这些条款，以便他们知道自己的权利。

我们通过两个步骤保护您的权利：(1) 对软件进行版权保护，(2) 为提供本许可证，允许您复制、分发和修改软件。

此外，对于自由软件，我们希望在软件被他人修改并传递时，让接收者知道其没有保证。最后，任何程序都受到专利的威胁。我们希望防止任何分发程序的人获得获得专利。为了这一点，我们希望明确，任何修改程序都是根据本许可证许可的。（例外：如果程序本身是交互式的但不打印公告，您的基于程序的作品不需要打印公告。）

复制、分发和修改的条款如下：

## 复制、分发和修改的条款

0. 本许可适用于任何出版的、包含程序或其部分的程序，无论是原样还是经过修改的。“程序”指的是任何程序或作品，而“基于程序的作品”指的是根据程序制作的任何作品（下文“翻译”包含在内）。”除复制、分发和修改以外的活动均不受本许可的限制。

1. 您可以在任何介质上复制并分发程序的原样副本，只要在每个副本上显著地发布相应的版权声明和免责声明；并向程序的其他接收者提供本许可证的副本。

   您可以对分发的物理行为收取费用，并可以根据需要交换费用提供保证。

2. 您可以修改您的程序或程序的任何部分以形成基于程序的作品，并根据第 1 条分发此类修改或作品，前提是还满足以下所有条件：

   a) 您必须在修改后的文件中包含通知，说明您更改了这些文件以及更改日期。
   b) 您必须确保您分发或出版的包含程序或源自程序的任何作品，整体上根据本许可证进行许可。
   c) 如果修改后的程序在运行时通常是交互式的，您必须确保它以通常方式进行交互式使用时打印或显示包含适当通知的公告，该公告说明没有保证（或者说明您提供保证），并且用户可以根据这些条件重新分发程序，并告知用户如何查看本许可证副本。（例外：如果程序本身是交互式的但不打印公告，您的基于程序的作品不需要打印公告。）

   这些要求适用于修改后的整体。如果可以识别的作品部分并非源自程序，并且可以被认为是独立的独立作品，那么在将其作为独立作品分发时，本许可及其条款不适用于这些部分。但当您将这些部分作为基于程序的整体的一部分进行分发时，整体必须根据本许可的条款分发，本许可的许可适用于整个作品，无论由谁编写。

   因此，本节的意图并不是主张或反对您完全编写的作品权；而是行使分发衍生或集合作品的权利。

   此外，仅仅在存储或分发介质上将其他非程序作品（或基于程序的作品）聚合在一起，并不会将其他作品纳入本许可的范围。

## 附录 F GNU/通用公共许可证

3. 您可以根据上述第 1 条和第 2 条的条款，以目标代码或可执行形式复制并分发程序（或根据第 2 条基于此的作品），前提您还须以下操作之一：

- a) 附带完整的相应的机器可读源代码，该源代码必须根据上述第 1 条和第 2 条的条款，在通常用于软件交换的介质上分发；或者，
- b) 附一份有效期至少三年的书面报价，承诺向任何第三方收取不超过物理分发源代码成本的费用，提供完整的机器可读源代码副本，并将根据上述第 1 条和第 2 条的条款，在通常用于软件交换的介质上分发；或者，
- c) 附带您收到的分发相应源代码要约的信息。（这种替代方案仅适用于非商业性分发，且仅当您根据第 b 小节以目标代码或可执行形式收到此类要约的程序时有效。）

作品源代码意味着对该作品进行修改的首选形式。对于可执行作品，完整源代码意味着其包含的所有模块的所有源代码，加上任何相关的接口定义文件，以及用于编译和安装可执行程序的脚本。但是，作为一个特殊例外，所需的源代码不包括通常与运行该可执行程序的操作系统主要组件（编译器、内核等）一起（以源代码或二进制形式）分发的内容，除非该组件本身随可执行程序一起。

如果通过提供访问指定位置复制的机会来分发可执行代码或目标代码，则从相同位置提供等量的源代码访问被视为源代码的分发，尽管各方并不强制在复制目标代码的同时复制源代码。

4. 除非本许可证明确规定，否则您不得复制、修改、分许可或分发程序。任何其他尝试复制、修改、分许可或分发程序的尝试均无效，并将自动终止您根据本许可证享有的权利。然而，根据本许可证获得副本或权利的各方，只要保持完全遵守规定，其许可就不会终止。

5. 您不要求接受本许可证，因为您还没有签署它。但是，没有其他任何条款授予您修改或分发程序或其衍生作品。如果您不接受本许可证，这些行为是法律禁止的。因此，通过修改或分发程序（或任何基于程序的作品），您表示接受本许可证此类行为，以及所有复制、分发或修改程序或基于程序的作品的条款和条件。

## 复制、分发和修改的条款

6. 每当重新分发程序（或任何基于程序的作品）时，接收方自动获得原始许可方的许可，根据这些条款和条件复制、分发或修改程序。您不得对接收方行使本许可证授予的权利施加任何进一步限制。您不对第三方强制遵守本许可证的行为负责。

7. 如果由于法院判决、专利侵权指控或其他任何原因（不限于专利问题），对您施加了（无论是通过法院命令、协议或其他方式）与本许可证条款矛盾的条件，只要无法满足您在本许可证及任何其他相关义务（如有），您将不进行分发。例如，如果许可不允许所有通过您直接或间接接收副本的人对程序进行特许权的再分发，那么您同时满足此项规定和许可证的唯一方法就是完全停止分发该程序。

如果本节的任何部分在任何情况下被认为无效或不可执行，该节的其余部分应适用，整个节在其他情况下也适用。

本节的目的不是诱导您侵犯任何专利或其他财产主张，或质疑此类主张的有效性；本节的唯一目的是保护自由软件分发系统的完整性，该系统是通过公共许可实践实施的。许多人依靠该系统的一致应用，对该系统分发的广泛软件做出了慷慨贡献；作者/捐赠者决定其是否愿意通过任何其他系统分发软件，被许可者不能选择该选择。

本节旨在彻底澄清被认为是本许可证其他部分的结果。

8. 如果程序的分发和或或在某些国家受到专利或版权保护接口的限制，将程序置于本许可证下的原始版权持有者可以增加明确的地理分发限制以排除这些国家，从而仅允许在未此类排除的国家内或国家之间分发。在这种情况下，本许可证包含了该限制，如同写在本许可证正文中一样。

9. 自由软件基金可能会随时发布通用公共许可证的修订和/或新版本。这些新版本精神上与当前版本相似，但在细节上可能不同，以解决新的问题或关注。

## 附录 F GNU/通用公共许可证

每个版本都有一个不同的版本号。如果程序指定了适用于它的本许可证版本号以及“任何后续版本”，则您可以选择遵循该版本或自由软件基金会发布的任何后续版本的条款和条件。如果程序没有指定本许可证的版本号，您可以选择自由软件会发布过的任何版本。

10. 如果您希望将程序的某些部分整合到分发条件不同的其他自由程序中，请写信给作者寻求许可。对于由自由软件会拥有版权的软件，请写信给自由软件会。

11. 本程序按“原样”分发，不提供任何形式的明示或暗示保证，包括对商品性或特定用途的保证。在任何情况下，版权持有者或索赔者不对因合同、侵权或与程序或其他引起的任何索赔、损害承担责任。

## 如何将这些条款应用于新程序

如果您开发了一个新程序，并希望它是自由的，实现此点的最佳方法是在每个文件中添加以下通知：

- 版权所有 © `<年份>` `<作者>`
- 一行关于程序名称及其功能的说明

本程序是自由软件，您可以根据自由软件会发布的通用公共许可证（版本 2 或根据您的选择任何后续版本）进行分发和/或修改。

分发程序时，我们希望它是有用的，但不提供任何保证，甚至没有对商品性或特定用途的暗示保证。您应该已经收到一份通用公共许可证的副本；如果没有，请写信自由软件会，地址为 59 Temple Place, Boston, MA 22107, USA。

另添加如何通过电子邮件和纸质邮件联系您的信息。

如果程序是交互式的，让它在交互模式启动时输出如下简短通知：

`程序版本年份`，版权所有 © `<年份>` `<作者>`

程序完全没有任何保证；详情请输入 `show w`。这是自由软件，您可以在某些条件下重新分发它；详情请输入 `show c`。

假设的命令 `show w` 和 `show c` 应显示通用公共许可证的相关部分。当然，您使用的命令可以不是 `show w` 和 `show c`；它们可以是鼠标点击或菜单项。

如有，您还应该让您的雇主（如果您作为程序员工作）或您的学校（如果有）对该程序签署一份“版权免责声明”。这是一个示例；请修改名称：

Yoyodyne, Inc. 特此放弃对 James Hacker 编写的（冒充编译器的）`'Gnomvision'` 程序的全部版权。
签名：Ty Coon, 1989 年 4 月 1 日

Ty Coon, Yoyodyne 总裁

本通用公共许可证不允许将您的程序整合到专有程序中。如果您的程序是一个子程序库，您可能认为允许专有应用程序与该库进行链接会更有用。如果您确实想这样做，请使用 GNU 库通用公共许可证代替本许可证。

FSF & GNU 咨询与问题请发送至 `gnu@gnu.org`。对这些网页的评论请发送至 `webmasters@www.gnu.org`，其他问题发送至 `gnu@gnu.org`。

上方版权声明。Free Software Foundation, Inc., 59 Temple Place–Suite 330, Boston, MA 02111, USA 更新：2000 年 7 月 31 日 jonas

# 索引

# 符号

- `$(CFLAGS)`, `make` 变量, 108
- `/dev` 目录, 132
- `/dev/full`, 137
- `/dev/loop#` (回环设备), 139-142
- `/dev/null` (空设备), 136
- `/dev/pts` (PT 终端), 142
- `/dev/random` (随机数设备), 136
- `/dev/urandom` (随机数设备), 139-142
- `/dev/zero`, 136
- `/etc/services` 文件, 125
- `/proc` 文件系统, 147-148
- CD-ROM 驱动器信息, 163
- CPU 信息, 159
- 设备信息, 159
- 文件锁信息, 164-165
- 文件大小, 147
- 文件系统信息, 161
- 主机名和域名, 162
- IDE 设备信息, 162
- 内核内存使用情况, 161
- med 文件系统, 163-164
- 输出自, 148-150
- 分区信息, 163
- PCI 总线信息, 159
- 进程参数列表, 152-154
- 进程目录, 150-151
- 进程环境, 154-155
- 进程执行文件, 155-156
- 进程文件描述符, 156-158
- 进程内存统计, 158
- 进程统计, 158
- SCSI 设备信息, 163
- 串口串口信息, 159–160
- 系统负载信息, 165
- 系统运行时间信息, 165–166
- 内核版本号, 148, 160
- `/proc/cpuinfo` (系统 CPU 信息), 148-150, 159
- `/proc/devices` (设备信息), 159
- `/proc/file systems` (文件系统信息), 161
- `/proc/ide` (IDE 设备信息), 162
- `/proc/loadavg` (系统负载信息), 165
- `/proc/locks` (文件锁信息), 164-165
- `/proc/meminfo` (内核内存使用情况), 161
- `/proc/mounts` (挂载文件信息), 163-164
- `/proc/pci` (PCI 总线信息), 159
- `/proc/scsi` (SCSI 设备信息), 163
- `/proc/self/`, 151-152
- `/proc/sys/devcdrom/info` (CD-ROM 驱动器信息), 163
- (域名), 160
- `/proc/sys/kernel/domainname` (主机名), 160
- `/proc/sys/tty/driver` (串口信息), 159-160
- `/proc/uptime` (系统运行时间), 165-166
- `/proc/version` (内核版本号), 148, 160
- `/tmp` 目录, 竞态条件 (安全漏洞), 213-216
- `|` (管道符号), 110

# `abort` 函数

# A

- `abort` 函数, 终止进程, 55
- `accept` 函数, 119
- 访问速度, 共享内存, 96-97
- `access` 系统调用, 169-170
- 访问
    - 字符设备, 134-135
    - 通过打开文件设备, 133
    - `FIFOs`, 115-116
    - 终端, 135
- 活跃进程, 查看, 46-47
- 地址
    - Internet 域套接字, 123
    - 套接字, 117
- `alarm` 系统调用, 185
- 分配
    - 资源信号量, 101
    - 共享内存, 97-98
- `app.c` (带有库函数的程序), 列表, 2.8, 37
- 存档 (静态库), 37-38
- 与共享库对比, 41-42
- `arg` 参数 (`main` 函数), 18-19
- `arglist.c` (`arg` 和 `argv` 参数), 列表, 2.1, 18-19
- 参数列表, 18-19
- 命令行选项, `getopt_long_function`, 20-23
- 进程, 152-154
- 参数, 线程定义, 62
- 传递数据, 64-65
- `argv` 参数 (`main` 函数), 18-19
- `asm` 语句 (汇编代码), 189-190
- 维护与移植性, 196
- 语法, 191-192
- 输入操作数, 193
- 输出操作数, 192-193
- 与 C 代码对比, 194-196
- 使用场景, 190
- `asm` 宏 (错误检查), 30-31
- 异步可取消线程, 70
- 原子操作, 79
- 附加, 共享内存, 98-99
- 属性, 自定义, 68
- 音频, 播放, 135
- 验证, 208-211

# B

- `better_sleep.c` (高精度睡眠), 列表, 8.8, 182
- `bind` 函数, 119
- 信号量, 见信号量 (进程)
- 确定 (汇编代码) 与 C 代码对比, 194-196
- `bit-pos-asm.c` (带 `bsr`), 列表, 8.2, 195
- `bit-pos-loop.c` (带 `list`), 列表, 9.1, 194-195
- 块设备, 定义, 130
- 回环设备, 139-142
- 警告, 130
- 阻塞函数, 定义, 34
- `break` 命令, 12
- 缓冲区溢出 (安全漏洞), 211-213
- 缓冲输出与错误流, 24
- 磁盘缓冲区 示例程序, 254
- 空设备, 136
- 随机数设备, 137-139
- `char_print` 函数, 64
- `chdir` 系统调用, 296
- `check-access.c` (文件访问权限), 列表, 8.1, 170
- 子进程, 49
- 清理, 59-60
- 与父进程通信, 管道, 110-112
- 僵尸进程, 57-59

# C

- C 代码与汇编代码对比, 性能, 194-196
- C 库函数, 与底层 I/O 函数的关系
- `-c` 选项 (GCC 编译器), 7
- C++, 线程清理处理器, 76-77
- 磁盘缓冲区 程序示例, 270-280
- `chmod` 系统调用, 修改权限位, 203
- `setuid` 程序, 208
- 粘滞位, 204
- 目标 (`make`), 9
- 清理子进程, 59-60
- 清理处理器, 线程, 75-76
- 在 C++ 中, 76-77
- `calculator.c` (计算器程序), 列表, A.3, 274-275
- 取消线程, 69-70
- 异步可取消与同步可取消线程, 70
- 不可取消线程, 71-72
- 使用场景
- `cleanup.c` (清理处理器), 列表, 4.8, 75-76
- 清除环境变量, 26
- `client.c` (网络客户端程序), 列表, 2.4, 26
- 客户端, 定义, 118
- 覆盖寄存器, 语法, 194
- 取消点 (线程), 70
- 回车符, 读取 DOS/Windows 文件, 287
- `cmalloc` (动态内存分配), 264-265
- 与其他动态内存分配工具对比, 262
- `clock-speed.c` (来自 `/proc/cpuinfo` 的时钟频率), 列表, 7.1, 149
- `clone` 系统调用, 93-94
- `close` 系统调用, 118, 284
- `close userid`, 297
- CD-ROM 驱动器信息, 163
- `/proc/sys/devcdrom/info`, 163
- `dect.c` (`ioctl`), 列表, 6.2, 144
- 字符设备, 访问, 134-135
- 设备, 定义, 136
- `/dev/full`, 137
- `/dev/zero`, 136
- 关闭文件描述符, 156-158
- 关闭, 118-284
- 输出, 148-150
- 代码, 189-190
- 命令行选项, 18-19
- 命令, 39
- `common.c` (实用函数), 列表, 12.2, 223
- 配置信息, 267
- `connect` 函数, 118
- 连接型套接字, 117
- 对话对象 (PAM), 210
- 转换, 主机名, 160
- 将 `asm` 语句转换为汇编代码, 191
- 写时复制页, 定义, 178
- `copy.c` (`sendfile` 系统调用), 列表, 8.10, 184
- 从文件描述符拷贝, 183-185
- 虚拟文件系统, 142
- `cp` 命令, 设备条目, 131
- CPU 信息, `/proc/cpuinfo`, 148-150, 159
- `cpu` 进程项, 151
- `create-file.c` (创建新文件), 列表, 8.1, 170
- 创建分离线程, 69
- `FIFOs`, 115-116
- 键 (线程特定数据), 73
- 互斥锁, 79
- 管道, 110
- 套接字, 118
- 线程, 62-63
- 临界区, 不可取消线程, 71-72
- `critical-section.c` (临界区), 列表, 4.6, 71
- 自定义线程属性, 68-69
- `cxx-exit.cpp` (C++ 线程清理处理器), 列表, 4.9, 77
- 守护进程, 缓冲区溢出 (安全漏洞), 211-213
- 数据结构, 映射内存, 109
- 数据传输, `sendfile` 系统调用, 183-185
- 数据报套接字, 117
- 日期信息, `gettimeofday` 系统调用, 176-177
- `dd` 命令 (块拷贝), 140
- 锁锁, 82-83
- 非多线程, 91

# D

## DNS (域名解析服务) 321

- 释放
- 信号量 (进程), 101
- 共享内存, 99
- 调试代码。见见错误检查
- 调试器，
- 设备项, 131-132
- `/dev` 目录, 132
- 访问设备, 133
- `cp` 命令, 131
- 创建, 131-132
- 显示, 132
- 移除, 132
- `GDB`, 11
- 使用...编译, 11
- 运行, 11-13

- 调试
- 信号量 (进程), 105
- 共享内存, 100
- 系统调用，`trace` 命令, 168-169
- 线程, 77-78

- 设备文件，类型, 130
- 设备信息, `/proc/devices`, 159
- 设备号，定义, 130-131

- `definitions.h` (计算器程序的头文件), 列表 A.6, 280

- 设备
- 通过打开文件访问, 133
- 块设备，列表, 133-134
- 字符设备
- 访问, 134-135
- 列表, 134
- `ioctl` 系统调用, 144
- `PTYs` (伪终端), 142-144
- 特殊设备, 136

- 删除
- 文件，粘滞位 (`sticky bits`), 204
- 临时文件, 28

- 拒绝服务 (DoS) 攻击, 216
- 依赖
- 库, 40-41
- `make`, 9

- `/dev/full`, 137
- `/dev/zero`, 136
- 回环设备, 139-142
- 空设备, 136
- 随机数生成设备, 137-139

- 销毁套接字, 216
- 分离状态 (线程), 68
- 分离线程
- 创建, 69
- 定义, 68

- 目录
- `/dev`, 132
- `/proc` 文件系统目录, 150-151
- `/tmp`，竞态条件 (安全漏洞), 213-216
- 权限, 203

- `detached.c` (创建分离线程), 列表 4.5, 69
- 分离，共享内存, 98-99
- 开发工具
- 动态内存分配, 261-262
- `amalloc`, 264-265
- `Electric Fence`, 265-266
- `malloc`, 262-263
- `nstrac`, 263-264
- 示例程序, 267-269
- 选择, 266-267

- 粘滞位, 204-205
- 读取内容, 297-299
- 磁盘缓冲区, 173-174
- `diskfree.c` (释放磁盘空间信息), 列表 11.8, 242-243
- `diskfree.so` 模块 (示例应用程序), 224-244

- `gprof` (269-270)
- 计算器程序示例, 270-280
- 收集信息, 271-273
- 显示数据, 271-273
- 静态程序分析, 259-260

- `DISPLAY` 环境变量, 25
- 处置 (信号), 53
- `disclose` 函数, 43
- `dlerror` 函数, 43
- `dloopen` 函数, 42-43
- `dlsym` 函数, 43

- 设备驱动
- 定义, 129
- 关于...警告, 130

- DNS (域名解析服务), 123

## 322 文档

- 文档, 13
- 头文件, 15
- `Info` 文档系统, 14–15
- `man` 页面, 14
- 示例应用程序, 255–256
- 源代码, 15

- 域名解析服务 (DNS), 123
- 域名,
- `/proc/sys/kernelname`, 160
- DoS (拒绝服务) 攻击, 216
- DOS/Windows 文件，读取, 287
- 驱动程序。见设备 (此处原文为 devices)

- `Emacs`, 4
- 自动格式化, 5
- 打开源文件, 4
- 在...中运行 `GDB`, 13
- 语法高亮, 5
- `environ` 全局变量, 26
- `environ` 进程项, 150, 154–155

- 环境
- 定义-25,27
- 打印, 25
- 进程, 154–155
- 环境变量, 25-27
- 访问, 26
- 清除, 26
- 作为配置信息, 26–27
- 列举所有, 26

- `dup2` 系统调用, 112–113
- `dup2.c` (输出重定向), 列表, 5,183

- 动态链接 (库), 36
- 动态内存分配, 261–262
- `cmalloc`, 264–265
- `Electric Fence`, 265–266
- `malloc`, 262–263
- `ntrace`, 263–264
- 示例程序, 267–269
- 选择开发工具, 266–267

- `MALLOC_CHECK`, 263
- `MALLOC_TRACE`, 264
- 设置, 26
- `errno` 变量, 33
- 错误检查, 30
- 错误标记, 30–31
- 资源分配, 35–36
- 系统调用失败, 42
- 动态运行时加载，共享库, 42–43
- 动态链接库。见共享库
- 错误函数, 225
- 错误流，通过管道重定向, 112–113
- 错误检查函数，内存分配, 225
- 错误检查互斥锁, 82
- 错误 (`stderr` 流), 23–24
- 错误代码，系统失败, 33–35
- 示例程序。见应用程序
- `exe` 进程项, 150, 155–156
- 创建进程, 48, 50–51
- 避免安全漏洞, 217

- 编辑器
- 定义, 4
- 自动格式化, 5
- 打开源文件, 4
- 在...中运行 `GDB`, 13
- 语法高亮, 5
- 有效用户 ID 与用户 ID, 205–206
- `setuid` 程序, 206–208

- `EINTR` 错误代码, 34
- `Electric Fence` (动态内存分配), 265–266
- 可执行文件，进程, 155–156
- 执行权限，关于, 204
- 在 shell 中执行程序，安全漏洞, 216–218
- `execve` 系统调用, 168
- `exit` 代码, 24-25, 55-56
- `exit` 系统调用, 164, 171-172
- 退出线程, 63, 69
- 清理处理程序, 75-77
- `export` 命令, 25
- `ext2` 文件系统中的隙, 290

## F

- `-f` 选项 (`ps` 命令), 47
- 快速互斥锁，锁定, 82
- `fctl` 系统调用, 164, 171-172
- `fd` 进程项, 150, 156-158
- `fasync` 系统调用, 173-174
- `fdopen` 函数, 295
- `FIFOs` (先进先出文件), 114-115
- 访问, 115-116
- 创建, 115
- Windows32 命名管道, 116
- 文件描述符 (底层 I/O), 282
- 关闭底层 I/O 函数, 284-285
- 复制到/自, 183-185
- I/O 和错误流, 23
- 移动 I/O 函数, 288-290
- 进程, 156-158
- 从底层 I/O 函数读取数据, 287-288
- 使用 C 库函数, 295-296
- 向底层 I/O 函数写入数据, 285-286
- 文件系统信息, `/proc/filesystems`, 161
- `FILE*` 指针, 282
- `FILE` 流，使用底层 I/O 函数, 295-296
- `fileno` 函数, 295

- 文件
- 删除粘滞位, 204
- 通过设备处理, 133
- 底层 I/O 函数, 282-284
- 所有者, 200
- 权限位，掩码, 283
- 权限, 200-204
- 关于执行权限的警告, 204
- 临时文件, 27
- 删除, 28
- `mkstep` 函数, 28-29
- `tempfile` 函数, 29
- 先进先出文件。见 `FIFOs` 标志
- `lock` 系统调用, 172
- 刷新磁盘缓冲区, 173-174
- `open` 函数, 295
- `fork` 系统调用，创建进程, 48-51
- `fork-exec.c` (`fork` 和 `exec` 函数), 列表 3.4, 51
- `fork.c` (`fork` 函数), 3.3, 49
- 使用 `Emacs` 形成源文件, 5
- `-fPIC` 选项 (GCC 编译器), 38
- `printf` 函数, 282
- `free` 命令, 161
- 释放磁盘空间信息，示例应用程序, 242-244
- `fsstat` 系统调用, 292
- `fsync` 系统调用, 173-174
- 函数, 53。另见命令：系统调用
- `abort`，终止进程, 55
- `accept`, 119
- `bind`, 119
- 阻塞函数，定义, 34
- `char_print`, 64
- 文件锁, 171
- 错误检查函数，内存分配, 225
- 错误检查
- 错误检查互斥锁，锁定, 82
- 错误 (`stderr` 流), 23–24
- 错误代码，系统失败, 33–35
- 示例程序。见应用程序
- `exe` 进程项, 150, 155–156
- 创建进程, 48, 50–51
- 避免安全漏洞, 217

# HTTP (超文本传输协议) 325

# G

`gettimeofday` 系统调用, 176-177
- `-g` 选项 (GCC 编译器), 11
- 示例应用程序, 239
- `g++` (C++ 编译器), 7
- `GID` (组标识符), 18
- `GCC` (C 编译器), 6-7
- GNU 编码标准, 19
- 汇编代码, 189-190
- GNU 调试器 `GDB`
- `asm` 语法, 191-194
- GNU 通用许可证, 309-316
- 汇编转换, 191
- 维护与可移植性, 196
- GNU `Make`. 参见 `make`
- 优化, 196
- 版本 C 代码性能, 194-196
- GNU/Linux 发行版信息,
- 何时使用, 190
- 示例应用程序, 240,
- 链接目标文件, 7-8
- GNU/Linux 在线资源
- 源码编译选项, 123
- 303-304
- `-pedantic` 选项, 260
- `gprof` (性能分析) 开发工具,
- `-Wall` 选项, 260
- 269-270

# GDB (GNU 调试器), 11

- 计算器程序, 270-280
  + 命令
  - `break` (断点), 12
  - `next` (单步), 13
  - `print` (打印), 12
  - `run` (运行), 12
  - `step` (单入), 13
  - `up` (上层), 12
  - `where` (位置), 12
- 收集信息, 271, 273
- 显示数据, 271-273
- `grep-dictionary.c` (单词搜索),
- 列出 10.6, 216-217
- 组标识符 (`GID`), 198
- 组
- 进程组标识符, 199-200
- `UID` (用户 ID) 和 `GID` 组, 198
- 使用 11 编译
- 运行, 13

# H

- `get-exe-path.c` (程序可执行路径), 列出 7.5, 155-156
- 硬限制, 定义, 174
- `get-pid.c` (从 `/proc/self/` 获取进程 ID), 列出 7.2, 151-152
- 硬件设备
- 块设备，列表, 133-134
- `getcwd` 系统调用, 2296
- 字符设备
- `getgid` 系统调用, 200
- 访问, 134-135
- `getenv` 函数, 26
- 列表, 134
- 头文件, 15
- `getgetuid` 函数, 200
- `gethostname` 函数, 123
- `hello.c` (Hello World), 列出 A.1, 260
- `getline` 函数, 缓冲区溢出,
- `hexdump.c` (打印十六进制文件储), 列出 B.4, 287-288
- `gettop` 函数, 203
- `getopt_long.c` (`getopt_long` 函数), 列出 2.2, 21-23
- 来自 `Emacs` 高亮源文件, 5
- `HOME` 环境变量, 25
- `getpagesize` 函数, 97, 178
- `hostname` 命令, 168
- `getrlimit` 系统调用, 174-175
- 主主机
- `/proc/sys/kernel/hostname`, 160
- `getrusage` 系统调用, 175-176
- 转换, 123
- `gets` 函数, 缓冲区溢出, 212
- `htons` 函数, 123
- HTTP (超文本传输协议), 125, 221

# -l 选项 (GCC 编译器)

# I
- `-I` 选项 (GCC 编译器), 7

## I/O (输入/输出)
- HFO 访问, 115-116
- 输入/输出和错误流, 23-24
- `- mmap` 函数, 109
- 管道重定向, 112-113
- I/O 函数，低级. 参见低级 I/O 函数
- 198
- `id` 命令, 198
- IDE (集成开发环境), 9
- IDE 设备信息, `proc/code`, 162
- 空闲时间信息, `/proc/uptime`, 165-166
- `Info` 文档系统, 14-15, 256
- `init` 进程, 59
- 初始化，信号量 (进程), 102
- 内联汇编代码. 参见汇编代码
- 输入操作数，作为语法, 193
- 输入. 参见 I/O (输入/输出)
- 集成开发环境 (IDE), 9
- 英特尔 x86 架构，寄存器字母, 193
- 互联网协议 (IP), 123
- 互联网域套接, 123-125
- 进程间通信 (IPC) 定义, 95
- 映射内存, 106-108
- `mmmap` 函数, 105-109
- 私有映射, 109
- 共享文件访问, 108-109
- + 信号量, 101
  - 分配与释放, 101
  - 调试, 105
  - 初始化, 102
  - 等 和 `post` 操作, 103-104
- 共享内存, 96
  - 访问速度, 96-97
  - 优缺点, 101
  - 分配, 97-98
  - 挂载与卸载, 88-99
  - 释放, 99
  - 调试, 100
  - 示例程序, 99-100
  - 内存模型, 97
  - 套接字, 116
    - `connect` 函数, 118
    - 创建, 118
    - 销毁, 118
    - 函数列表, 117
  - 互联网域套接字, 123-125
  - 本地套接字, 119-123
  - `send` 函数, 118
  - 服务器, 118-119
  - 套接字对, 125-126
  - 术语, 117
  - 间隔计时器，设置, 185-186
  - `ioctl` 系统调用, 144
  - IP (互联网协议), 123
  - IPC. 参见进程间通信
  - `ipcrm` 命令, 100
  - `ipcrm`, 105
  - `ipcs -s` 命令, 105
  - `ipcs` 命令, 100
  - (GNU/Linux 发行版信息), 列出 7.7, 240-242
  - `.so` 模块 (示例程序), 240-242
  - 创建, 110
  - `FIFOs`, 114-116
  - 父子进程通信, 110-112
  - `popen` 和 `pclose` 函数, 114
  - 减少, 113
  - `-j` 选项 (`ps` 命令), 47
  - 任务控制，在 shell 中, 93
  - `job-queue1.c` (竞态条件), 列出 0.0, 78
  - `job-queue2.c` (互斥锁), 列出 1.1, 80
  - `job-queue3.c` (信号量), 列出 2, 84-86
  - 可合并线程, 68
  - 合并线程, 65-66
  - `better-sleep.c` (高精度睡眠), 182
  - `-pos-loop.c` (带循环的), 194-195
  - `-pos-asm.c` (带循环的汇编), 195
  - 键 (线程特定数据), 创建, 73

## L
- `calculator.c` (主程序), 274-275
- `cd-eject.c` (`ioctl` 示例), 144
- `check-access.c` (文件访问), 170
- `cleanup.c` (处理器), 75-76
- `client.c` (网络程序), 223
- `clock.c` (从 `/proc/cpuinfo` 获取速度), 149
- `condvar.c` (条件变量), 90-91
- `copy.c` (创建新文件), 184
- `create-file.c` (创建新文件), 184
- `critical-section.c` (临界区), 71
- `exit.cpp` (C++ 线程), 76-77
- `definitions.h` (计算器头文件), 36-37
- `detached.c` (创建分离线程), 69
- `diskfree.c` (磁盘空间), 242,243
- `dup2.c` (输出重定向), 118
- `fork.c` (为了 `fork`), 49
- `fork-exec.c` (`fork` 和 `exec` 函数), 51
- `limit-cpu.c` (资源限制), 175
- `get-exe-path.c` (程序可执行路径), 155-156
- `get-long` (`getopt_long` 函数), 列出 2.2, 21-23
- `get-pid.c` (从 `/proc/self/` 获取进程 ID), 151-152
- `g-dictionary.c` (单词搜索), 216-217
- `hello.c` (Hello World), 260
- `hexdump.c` (打印十六进制文件储), 列出 B.4, 287-288
- `gettop` 函数, 203
- `getopt_long.c` (`getopt_long` 函数), 列出 2.2, 21-23
- `getpagesize` 函数, 97, 178
- `gethostname` 命令, 168
- `getrlimit` 系统调用, 174-175
- `getrusage` 系统调用, 175-176
- `hostnames`
- `/proc/sys/kernel/hostname`, 160
- `conversion`, 123
- `gets` 函数, 缓冲区溢出, 212
- `htons` 函数, 123
- HTTP (超文本传输协议), 125, 221

- `ldd` 命令
- `LD_LIBRARY_PATH` 变量, 04
- `libraries`, 2, 36
- `linking to` (静态库), 37–38
- `dynamic runtime`, 42–43
- `library dependencies`, 40–41
- `shared libraries`, 38–40
- `versus archives`, 41–42
- `standard libraries`, 40
- `get-pid.c` (从 `/proc/self/` 获取进程 ID), 151-152
- `g-dictionary.c` (单词搜索), 216-217
- `hello.c` (Hello World), 260
- `hexdump.c` (打印十六进制文件), 287–288
- `links, symbolic`, 182–183
- `listen` 函数, 119
- `lock-file.c` (写锁), 171-172
- `malloc-use.c` (动态内存分配), 267-269
- `main.c` (C 源文件), 153
- `main.c` (主程序), 235-238
- `map-read.c` (映射内存), 107
- `module.c` (加载服务器模块), 226-227
- `mprotect.c` (内存访问), 180-181
- `number.c` (数字实现), 276-278
- `open-and-spn.c` (打开文件), 175
- `pam.c` (PAM 示例), 209
- `pipe.c` (父子进程通信), 111
- `popen.c` (`popen` 命令), 114
- `primes.c` (线程中的质数计算), 67
- `print-arg-list.c` (打印参数列表), 153
- `print-times.c` (进程统计), 176
- `print-env.c` (打印执行环境), 26
- `print-environment.c` (进程环境), 154-155
- `print-pid-c` (打印进程 ID), 46
- `print-symlink.c` (符号链接), 183
- `print-time.c` (日期/时间打印), 177
- `print-uname.c` (版本号和硬件信息), 188
- `print-uptime.c` (系统更新和空闲时间), 165-166
- `processes.c` (总结进程), 244-250
- `random-number.c` (随机数生成), 138-139
- `readfile.c` (错误检查期间资源分配), 35-36
- `read-file.c` (将文件读入缓冲区), 292-293
- `reciprocal.cpp` (C++ 源文件), 6
- `reciprocal.hpp` (头文件), 7
- `sem_all_deall.c` (信号量分配与释放), 102
- `sem_init.c` (信号量初始化), 102
- `sem_pv.c` (信号量等 和 `post` 操作), 104
- `server.c` (服务器实现), 228-233
- `server.h` (函数和变量声明), 222-233
- `setuid-test.c` (`setuid` 程序), 207
- `shm.c` (共享内存), 99-100
- `schild.c` (清理子进程), 60
- `signal.c` (信号处理器), 54
- `simplistic.c` (打印用户和组 ID), 200
- `socket-client.c` (本地套接字), 121
- `socket-inet.c` (互联网域套接字), 124
- `socket-server.c` (本地套接字), 120
- `spnd-condvar.c` (条件变量), 87
- `stack.c` (数字用法), 279-280
- `stat-perm.c` (通过系统调用查看文件权限), 202
- `sysinfo.c` (系统统计), 187
- `sysystem.c` (系统函数), 48
- `temp-file.c` (`mkst` 函数), 28-29
- `temp-file.c` (临时文件创建), 214-215
- `test.c` (库内容), 37
- `thread-create.c` (创建线程), 63
- `thread-create2` (创建两个线程), 64-65
- `thread-create2.c` (修改后的主函数), 65
- `thread-pid` (打印线程进程 ID), 92
- `tifflest.c` (库 `fifo`), 40
- `time.c` (显示墙钟锁), 239-240
- `timestamp.c` (追加时间戳), 285
- `tread.c` (线程特定数据), 73-74
- `write-all.c` (写入所有缓冲区数据), 286
- `write-args.c` (`writev` 函数), 294-295
- `write_journal_entry.c` (数据缓冲区刷新), 173

# M
- 加载服务器模块（示例应用程序）, 226-227
- 宏
    - 本地套接, 119
    - 示例程序, 120-123
- `assert` (错误检查), 30-31
- 等待 GCC 命令行, 8
- `NDEBUG`, 30
- `localtime` 时间函数, 176
- `lock-file.c` (写锁), 列表 8.2, 171-172
- `main` 函数
    - `argc` 和 `argv` 参数, 18-19
    - 与操作环境的交互, 17
    - 等待写入, 65
        - 锁
    - 物理内存, 177-179
    - 线程
        - 非阻塞互斥测试, 83
        - 使用互斥锁, 79-83
- 主服务器程序（示例应用程序）, 235-239
- 锁, `fcnt` 系统调用, 171-172
- 锁信息, `/proc/locks`, 164-165
- `main.c` (C 源文件), 列表 1.1, 6
- `main.c` (主服务器程序), 列表 11.5, 235-238
- 长格式 (命令行选项), 19
- 环回设备, 139-142
- 维护, 汇编代码, 196
- 主设备号定义, 130-131
    - 低级 I/O 函数, 281-282
- `chdir`, 296
- 关闭文件描述符, 284-285
- 文件描述符, 282
- `getcwd`, 296
- `mkdir`,
- `make`, 编译源文件, 9-11
- `Makefile`, 10-11
- 示例应用程序, 列表 11.10, 252-253
    - 移动文件描述符, 288-290
- 打开文件, 282-284
- 从文件描述符读取数据, 287-288
- 与 C 库函数的关系, 295-296
- `malloc` (动态内存分配), 262-263
- 与其他动态内存分配工具的比较, 262
    - `rename`, 296
- `rmdir`, 296
- `stat` (文件状态信息), 291-293
- `unlink`, 296
- 向量读取, 295
- 向量写入, 293-295
- 向文件描述符写入数据, 285-286
- `malloc-use.c` (动态内存分配), 列表 A.2, 267-269
- `MALLOC_CHECK` 环境变量, 263
    - `is` 命令, 299
- 显示设备项, 132
- 查看权限位, 288-290
- `MALLOC_TRACE` 环境变量, 264
    - `lseek-huge.c` (创建大文件), 列表 B.5, 289-290
- `man` 命令, 14, 255
- 手页, 14
- 写入, 255
- 映射内存, 105
- 示例程序, 106-108
- `mmap` 函数, 105-106, 109
- 私有映射, 109
- 共享文件访问, 108-109
    - `lstat` 系统调用, 292
- 竞态条件, 214
- 映射进程项, 150

## memory
- `mmap` 系统调用, 105-106, 109, 179

## memory
- 动态分配, 261-262
- `calloc`, 264-265
- `Electric Fence`, 255-266
- `malloc`, 262-263
- `trimac`, 263-264
- 示例程序, 267-269
- 开发选择工具, 266-267
- 映射内存, 105
- `mmap-read.c` (映射内存), 列表 5.6, 107
- `mmap-write.c` (映射内存), 列表 5.5, 106
- `mode`. 见权限位
- 示例程序, 106-108
- `mmap` 函数, 105-106, 109
- 私有映射, 109
- 共享文件访问, 108-109
- `module.c` (加载服务器模块), 列表 11.3, 226-227
- 模块，示例应用程序, 239
- 页面对齐内存, 分配, 179
- 页面, 178
- 物理内存, 锁, 177-179
- 共享内存, 96
- `diskfree.so`, 242-244
- `sio.so`, 240-242
- 加载服务器模块, 226-227
- `processes.so`, 244-252
- 时间, 239-240
- 访问速度, 96-97
- 优点与缺点, 101
- 分配, 97-98
- 挂载与卸载, 98-99
- 释放, 99
- 调试,
    - 示例程序, 99-100
    - 内存模型, 97
    - `mount` 系统调用, 141
    - 挂载的文件系统信息, `/proc/mounts`, 163-164
    - 移动文件描述符, 低级 I/O 函数, 288-290
- 抖动, 定义, 178
- 内存分配函数, 225
- `mprotect` 系统调用, 179-181
- `mprotect.c` (内存访问), 列表 8.7, 180-181
- `msync` 系统调用, 108
- 内存 (动态内存), 263-264
- 页面对齐内存, 179
- 内存模型, 共享内存, 97
- 内存权限, 设置, 179-181
- 内存统计, 进程, 158
- 与其他动态内存工具的比较, 262
- `munlock` 系统调用, 178
- `munmap` 系统调用, 106
- 内核使用, `/proc/meminfo`, 161
- 次设备号, 定义, 130-131
- 互斥锁条件变量, 88
- 死锁, 在, 82-83
- `mkdir` 系统调用, 296
- `mkfifo` 命令, 115
- `mknod` 系统调用, 创建设备项, 131-132
- 互斥锁函数, 28-29
- 互斥锁. 见互斥锁
- 竞态条件, 213
- `lock` 系统调用, 177-179
- `lock` 系统调用, 178
- 命名管道. 见 `FIFOs`
- `nanosleep` 系统调用, 181-182

## PIC (位置无关代码)
- `NDEBUG` 宏, 30
- 网络字节序 (套接), 123
- 网络文件系统 (NFS), 172
- 换行符, 读取 DOS/Windows 文件, 287
- `next` 命令, `GDB`, 13
- NFS (网络文件系统), 172
- `nice` 系统调用, 进程, 52
- `niceness` 值, 进程, 52
- 非阻塞模式 (等待), 59
- 非阻塞互斥测试 (线程), 83
- NUL 于 NULL, 152
- 空设备, 136
- `number.c` (一元实现), 列表 A.4, 276
- 来自 `/proc` 文件系统的输出, 148-150. 见 I/O (输入/输出)
- 输出操作数, `asm` 语法, 192-193
- 文件所有者, 200
- 数据包, 117
- 页面对齐内存, 分配, 179
- 页面, 写时复制, 178
- 内存页面, 178
- 共享内存, 97
- PAM (可插身份模块), 209-211
- `pam.c` (PAM 示例), 列表 10.4, 209
- 父进程 ID (`ppid`), 46
- 父进程, 49

## O
- `-o` 选项 GCC 编译器, 8
- `-O2` 选项 GCC 编译器, 8
- 对象文件, 链接, 8-9
- 在线资源,列表, 303-304
- Open Public License Version 1.0, 305-308
- `open` 系统调用, 282-284
- `open-and-spin.c` (打开文件), 列表 7.6, 157
- 与子进程的通信, 110-112
- 分区 (设备) 信息, 163
- 向线程传递数据, 64-65
- 密码, 用户认证, 208-209
- `PATH` 环境变量, 25
- PCI 总线信息, `/proc/pci`, 159
- `pclose` 函数, 114
- `-pedantic` 选项 GCC 编译器, 260
- 性能, 汇编代码, 194-196. 见优化
- 权限位
    - 通过打开文件访问设备, 133
    - 低级 I/O 函数, 282-284
- 权限
    - 目录, 203-205
    - 粘位, 223
    - 文件权限, 200-204
    - 验证, 169-170
    - 关于执行权限的警告, 204
    - 内存权限, 设置, 179-181
- 优化. 见性能汇编代码, 196
- GCC 编译器选项, 8
- `gprof` (性能分析) 开发工具, 269-270
- 收集程序示例, 270-271, 274-280
- 收集信息, 271, 273
- 显示数据, 271-273
- `perror` 函数, 33
- 物理内存, 锁, 177-179
- PIC (位置无关代码), 38

## pid (进程 ID)
- `pid` (进程 ID), 46
- `pipe` 系统调用, 110
- `pipe.c` (父子进程), 列表 5.7, 114
- `print-symlink.c` (符号链接), 列表 8.9, 183
- `print-uptime.c` (进程时间), 列表 8.5, 176
- 管道
    - `FIFOs`, 115
    - 创建, 110
    - 父子通信, 112
    - 重定向, 110
- `printenv` 命令, 25
- `printf` 函数, 282
- 输出环境, 25
- 私有映射, 映射内存, 109
- PAM (可插身份模块), 209-211
- `popen` 命令, 114
- 安全漏洞, 216-218
- `popen.c` (`popen` 命令), 列表 5.9, 114
- 端口号 (套接), 123
- 标准, 125
- 可移植性, 汇编代码, 196
- 位置无关代码 (PIC), 38
- 后置操作 (互斥锁), 83, 103-104
- 进程组 ID, 199-200
- 进程 ID, 46
- 进程互斥锁. 见互斥锁 (进程)
- 进程统计, 175-176
- 进程用户 ID, 199-200
- 进程. 见进程通信 (IPC)
- `/proc` 文件系统目录, 150-151
- `/proc/self`, 151-152
- 参数列表, 152-154
- 子进程, 49
    - 与 `fork` 和 `exec` 函数, 48-51
    - 与系统调用, 48
- 环境, 154-155
- 可执行文件, 155-156
- 文件描述符, 156-168
- 实现线程为, 92-93
- `close` 系统调用, 93-94
- 信号处理, 93
- 初始进程, 59
- 内存统计, 158
- 父进程, 49
- 进程 ID, 46
- 与线程的关系, 61-62
- 调度, 52
- 信号, 52-54
- 统计, 158
- 后置表示法, 定义, 270
- `ppid` (父进程 ID), 46
- `primes.c` (线程质数数计算), 列表 4.4, 67
- `print` 命令, `GDB`, 12
- `print-arg-list.c` (打印进程参数列表), 列表 7.3, 153
- `print-times.c` (进程统计), 列表 8.5, 176
- `print-environment.c` (打印环境), 列表 7.4, 154-155
- `print_env.c` (打印执行环境), 列表 2.3, 26
- `print-pid.c` (打印进程 ID), 列表 3.1, 46

# PTYs (伪终端) 333

- 终止. 47, 55-56
- 清理子进程, 59-60
- 等待函数, 56-57
- 僵尸进程, 57-59
- 与线程对比，何时使用, 94
- 查看激活状态, 46-47

- IP (网协议), 123
- 套接字 (`sockets`), 117
- TCP (传输控制协议), 123

- `processes.c` (总结运行中的进程), 列出 11.9, 244-250

- `ps` 命令
- 显示终端设备, 143
- 查看激活进程, 46-47

- `processes.so` 模块 (应用程序), 244-252

- 伪终端 (PTYs), 142-144
- 伪随机数, 137

- 程序的性能分析, `gprof` 开发工具, 269-270

- 线程函数, 62
- `thread_attr_setdetachstate` 函数, 69

- 计算器程序示例, 270-271, 274-280
- 收集信息, 271, 273
- 显示数据, 271-273

- `thread_cancel` 函数, 69
- `thread_cleanup_pop` 函数, 75
- `thread_cleanup_push` 函数, 89

- 程序列出。参见列出

- `thread_cond_init` 函数, 89
- `thread_cond_signal` 函数, 89
- `thread_cond_wait` 函数, 89

# program

- `thread_create` 函数, 62
- `thread_detach` 函数, 69
- `thread_equal` 函数, 68

- + 参数参数列表, 18-19
- 命令行选项, 19
- `getopt_long` 函数, 20-23
- 开发工具
- 环境, 25-27
- 错误检查, 30-31

- `thread_exit` 函数, 63, 69
- C++ 中的线程清理, 76

- + 资源分配, 35-36
- 系统调用失败, 32-35
- 退出码, 24-25
- 与操作环境的交互, 17
- 链接到库, 36-37
- 存档 (静态库), 37-38
- 动态运行时加载, 42-43
- 库依赖, 40-41
- 共享库, 38-40
- 共享库存档, 41-42
- 标准库, 40

- `thread_join` 函数, 65
- `thread_key_create` 函数, 73
- `thread_mutexattr_destroy` 函数, 82
- `thread_mutexattr_init` 函数, 82

- + 示例应用程序。参见示例应用程序
- 标准 I/O, 23-24
- 临时文件, 27
- `mstemp` 函数, 28-29
- `tmpfile` 函数, 29

- `thread_mutex_init` 函数, 79
- `thread_mutex_lock` 函数, 80
- `thread_mutex_trylock` 函数, 83
- `thread_mutex_unlock` 函数, 80

# protocols

- + 与标准端口号关联, 125

- `thread_self` 函数, 68
- `thread_setcancelstate` 函数, 71
- `thread_setcanceltype` 函数, 70
- `thread_setspecific` 函数, 73
- `thread_testcancel` 函数, 70

- HTTP (超文本传输协议), 125

- PTYs (伪终端), 142-144

# Q-R

- 竞态条件 (安全漏洞), 213-216
- 竞态条件 (安全漏洞), 78-79
- + 使用互斥锁避免, 79-82
- 死锁, 82-83

- 随机数设备, 137-139
- `random_number.c` (随机数生成), 列出 6.1, 138-139
- `read` 系统调用, 277-288

- `read-file.c` (读取文件到缓冲区) 列出 B.6, 292-293
- `readir` 系统调用, 297
- `readfile.c` (错误检查期间的资源分配), 列出 2.6, 35-36

- 从文件描述符读取数据，低级 I/O 函数, 278-288
- 目录内容, 296-297, 299
- DOS/Windows 文件, 287
- 符号链接, 182-183

- `readlink` 系统调用, 182-183
- `readv` 系统调用, 295
- 真实用户 ID 与有效用户 ID, 205-206
- `setuid` 程序, 206-208

- `reciprocal.c` (C++ 源文件), 列出 1.2, 6
- `reciprocal.hpp` (头文件), 列出 1.3, 7
- 递归互斥锁, 锁定, 82
- `rcv` 函数, 119

- 重定向 I/O 和输出流, 23
- 使用管道重定向, 112-113
- Intel x86 架构中的寄存器, 193
- 寄存器清理处理器, 75
- 删除设备条目, 132
- `name` 系统调用, 296
- `renice` 命令，进程调度, 52

- 资源分配，错误检查, 35-36
- 资源限制，设置, 174-175

- 返回值 (线程), 66-67
- `rm` 命令，删除设备条目, 132
- `rmdir` 系统调用, 296
- 根进程条目, 150
- 根用户账户, 199
- 权限, 204
- `setuid` 程序, 206-208

- 规则 (`make`), 9
- `run` 命令, `GDB`, 12
- 可运行任务，定义, 165
- 运行中的进程 (总结示例程序), 244-252
- 运行服务器 (示例应用程序), 255-255

- 运行时检查, `assert`, 30-31
- 运行时加载，共享库, 42-43
- 运行时工具。参见开发工具

# S

- 示例应用程序, 219
- 构建, 254
- 通用函数, 223-224, 226
- 文档, 255-256
- 实现, 221, 223
- 加载服务器模块, 226-227
- 主服务器程序, 235-239
- `Makefile`, 252-253
- `diskfree.so`, 242-244
- `time.so`, 240
- `processes.so`, 244-252

- 概述, 219
- 运行服务器, 254-255
- 服务器实现, 228-235
- 调度, 52
- 序列信息, `/proc/si/scsi`, 163
- 安全身份验证, 208-209
- 目录权限, 203
- 粘性位, 214
- 权限, 200-204
- , 335

- `GID` (组), 198
- 漏洞, 211
- 缓冲区溢出, 211
- 使用 shell 执行程序, 216-218
- 竞态条件 (安全漏洞), 213-216
- 权限掩码, 283
- 根进程, 150
- 根用户账户, 199
- 权限, 204
- 用户 ID (`UID`), 198
- 真实用户 ID 与有效用户 ID, 205-206
- 共享内存 (段), 97
- 优点与缺点, 101
- 挂载与卸载, 97-98
- 调试, 100
- 示例程序, 99-100
- 线程工具, 269-270
- 共享内存 (线程), 103
- 分配与取消分配, 101
- 调试, 105
- 初始化, 102
- 与条件, 91
- 等待与操作, 103-104
- 线程 (信号量), 83
- `setctl` 函数, 101
- `setget` 函数, 101
- `setop` 函数, 103
- `setdestroy` 函数, 82
- `setgetvalue` 函数, 101
- `setinit` 函数, 102
- `setpost` 函数, 84
- `setrywait` 函数, 83
- `setwait` 函数, 84
- `send` 函数, 118

- 文件系统调用, 277-288
- 序列信息, `/proc/si/scsi`, 163
- 服务器实现, 228-235
- 服务器模块, 226-227
- 服务器程序, 244-252
- 运行服务器, 254-255
- 套接字, 117
- 连接, 118
- 创建, 118
- 销毁, 118
- 函数列表, 117
- 域套接字, 123-125
- 本地套接字, 119
- 示例程序, 120-123
- `send`, 118
- 服务器, 118-119

- `shmctl` 函数, 99
- `mget` 函数, 97
- 短格式, 18-19
- `sigABRT` 信号, 302
- `sigaction` 系统调用, 278-288
- `sigCHLD` 信号, 302
- `sigHUP` 信号, 302
- `sigILL` 信号, 302
- `sigKILL` 信号, 302
- `sigPIPE` 信号, 302
- `sigSEGV` 信号, 302
- `sigTERM` 信号, 302
- `sigUSR1` 信号, 302
- `sigUSR2` 信号, 302
- `sigVTALRM` 信号, 302
- `sleep` 函数, 181-182
- 套接字地址, 117
- `socket` 函数, 118
- `socket-client.c` (本地套接字) 列出 5.11, 121
- `socket-inet.c` (域套接字), 列出 5.12, 124
- `socket-server.c` (本地套接字) 列出 5.10, 120
- `socketpair` 函数, 125-126
- 术语, 117

## 系统调用 337

- 标准端口号, 125
- 
- `stat` 进程条目, 151
- `stat` 系统调用, 291-293
- 查看权限位, 201-202
- `stat-perm.c` (使用 `stat` 系统调用查看文件权限), 获取, 10.2, 202
- 静态库: 参见存档 (`archives`)
- 静态链接 (库), 36
- 静态程序分析工具, 259-260
- 统计
    - 内存统计, 进程, 158
    - 进程, 158-176
    - 系统统计, 获取, 186-187
- `statrm` 进程条目, 151, 158
- `stat` 进程条目, 151, 158
- `stderr` (错误流), 23-24
- `stdin` (输入流), 23-24
- `stdout` (输出流), 23-24
- `step` 命令, `GDB`, 13
- 粘位 (安全), 204-205
- `strace` 命令, 168-169
- 流, 管道重定向, 112-113
- `strerror` 函数, 33
- `strime` 函数, 176-177
- 结构. 参见数据结构 (`data structures`)
- `su` 程序, 207-208
- 超级用户 (`superuser`). 参见 `root` 用户 (`root user account`)
- 符号链接
    - 竞态条件 (安全漏洞), 213-216
    - 读取, 182-183
    - `stat` 函数, 292
- 线程同步
    - 条件变量, 86-91
    - 锁锁, 83-82
    - 在多线程上, 79-82
- 互斥锁 (`mutexes`)
    - 非阻塞互斥锁测试, 83
    - 竞态条件, 78-79
    - 与信号量配合, 83-86
- 同步可取消线程, 70
- 使用 `Emacs` 的语法高亮, 5
- `sysinfo` 系统调用, 166, 186-187
- `sysinfo.c` (系统统计), 列出, 8.12, 187
- 系统调用失败, 32
    - 错误代码, 33-35
- 系统调用. 参见命令 (`commands`); 函数 (`functions`)
- 访问, 169-170
- `alarm`, 185
- `chdir`, 296
- `chmod`, 更改权限位, 203
- `clone`, 118, 284
- 调试, 阶段, 168-169
- 定义, 167-168
- `dup2`, 112-113
- `execve`, 166
- `exit`, 终止进程, 55-56
- `fcntl`, 164, 171-172
- `flatasync`, 173-174
- `flock`, 172
- `fork`, 创建进程, 48-51
- `stat`, 292
- `sync`, 173-177
- `cgetwnd`, 296
- `tegetgid`, 200
- `getuid`, 200
- `getlimit`, 174-175
- `getrusage`, 175-176
- `gettimeofday`, 176-177, 239
- `ioctl`, 144
- `kill`, 55
- 列表, 168
- `seek`, 288-290
- 竞态条件, 214
- `mkdir`, 296
- `mknod`, 创建设备条目, 131-132
- `lock`, 177-179
- `lockall`, 178
- `map`, 105-106, 109, 179
- `mount`, 141, 147
- `mprot`, 179-181
- `msync`, 108
- `munlock`, 178
- `munlockall`, 178
- `map`, 106
- `nanosleep`, 181-182
- `nice`, 进程调度, 52
- `open`, 282-284
- `pipe`, 110
- `read`, 287-288

## 系统调用
- `readdr`, 297
- `readlink`, 182-183
- `adv`, 295
- `rename`, 296
- `rmdir`, 296
- `sendfile`, 183-185
- `setimer`, 185-186
- `setreuid`, 206
- `setlimit`, 174-175
- `sigaction` (信号处理), 53
- `stat`, 291-293
- `sysinfo`, 166, 186-187
- `time`, 95
- `hitr`, 174
- `uname`, 169, 187
- `unlink`, 28, 119, 296
- `write`, 169, 285-286
- `writev`, 293-295
- 临时文件, 27
- 删除, 28
- `mkstemp` 函数, 28-29
- `tmpfile` 函数, 29
- `temp_file.c` (`mkstemp` 函数), 列表 2.5, 28-29
- 终端
    - 访问, 135
    - `PTYs` (伪终端), 142-144
- 终止进程, 55-56
- 清理子进程, 59-60
- `wait` 函数, 56-57
- 僵尸进程, 57-59
- `test.c` (库内容), 2.7, 37
- 抖抖 (`thrashing`), 定义, 178
- 线程参数
    - 定义, 62
    - 传递数据, 64-65
- 线程属性
    - 自定义, 68-69
    - 定义, 62
- 线程函数
    - 定义, 62
    - 用途, 68
- 安全钩子, 216
- 系统信息
    - 创建进程, 48
    - 定义, 62
    - 传递数据, 64-65
    - `uname` 系统调用, 187
    - 线程 ID, 62
    - 系统负载, `/proc/loadavg`, 65
    - 系统统计, 获取, 186-187
    - 系统运行时间, `/proc/uptime`, 165
    - `thread-create.c` (创建线程), 4.1, 63
    - `thread-create2.c` (创建线程), 4.2, 67
    - `thread-pid.c` (打印线程 ID), 75
- 线程数据, 74

## TCP (传输控制协议)
- 原子操作, 79
- 取消, 69-70
- 异步和同步取消线程, 70
- 不可取消线程, 71-72
- 清理, 75-76
- 头文件, 13
- 手册, 14
- 源码, 15
- `temp-file.c` (创建临时文件), 列表 10.5, 214-215
- 创建, 62
- 定义, 78
- 定义, 70
- 退出, 63
- `clone` 系统调用, 93-94
- 信号处理, 93
- 可连接线程, 68
- 合并, 65-66
- 传递数据, 64-65
- `pthread` 函数, 62
- 返回值, 66-67
- 同步条件变量, 88-91
- 锁锁, 82-83
- 在多线程上的死锁, 91
- 非阻塞互斥锁测试, 83
- 竞态条件, 78-79
- 与信号量配合, 83-86
- 线程 ID 用途, 68
- 线程数据, 72-74
- 使用进程, 94
- 时间系统调用, 95
- 时间信息, `gettimeofday` 系统调用, 176-177
- `time.c` (显示墙钟时间), 列表 11.6, 239-240
- `time.so` (示例程序), 239-240
- 定时器, 设置间隔, 185-186
- `timestamp.c` (添加时间戳), 列表 B.2, 285
- `tmpfile` 函数, 29
- `top` 命令, 179
- 数据传输, `sendfile` 系统调用, 183-185
- `troff` 格式映射, 255
- 故障排除. 参见错误检查
- `tsd.c` (线程数据), 列表 4.7, 73-74

## U
- `UID` (用户 ID), 198
- `ulimit` 系统调用, 174
- 权限位, 283
- `uname` 系统调用, 169, 187
- 单目数字, 定义, 270
- 不可取消线程, 71-72
- 定义, 70
- Unix epoch, 定义, 176
- Unix 域套接字. 参见本地套接字 (local sockets)
- `unlink` 系统调用, 28, 119, 296
- `unset` 函数, 26
- `up` 命令, `GDB`, 12
- `uptime` 命令, 166
- 运行时间, `/proc/uptime`, 155-166
- 用户身份认证, 208-209, 211
- 用户环境变量, 25
- 用户 ID (`UID`), 198
- 真实有效 `UID`, 205-206
- `setuid` 程序, 206-208
- 用户名, `UID` (用户 ID), 198
- 进程用户 ID, 199-200
- `root`, 99
- `UID` (用户 ID) 和 `GID` (组), 198

## V
- 变量
    - 条件变量, 同步, 86-91
    - 环境变量, 27
    - 访问, 135
    - 清除, 26
    - 枚举所有, 26
    - 线程数据, 72-74
    - 向量读取, 低层, 295
    - 向量写入, 低层, 295
    - 版本号, 148
    - 版本, 140
