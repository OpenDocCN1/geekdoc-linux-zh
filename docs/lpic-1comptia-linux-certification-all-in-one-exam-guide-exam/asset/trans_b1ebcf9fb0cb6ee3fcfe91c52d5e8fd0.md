

## 答案

- 1. D. 硬件和操作系统是模块化的。只要硬件受到支持，你就可以安装任何针对你的特定 CPU 架构设计的操作系统。
- 2. B. Linux 内核是处理操作系统功能的组件。
- 3. C. 库包含预编写的代码，程序员可以在其应用程序中复用这些代码。
- 4. D. 当大学不再被允许访问 UNIX 源代码时，Andrew Tanenbaum 编写了 Minix 操作系统。
- 5. E. Linus Torvalds 将其 Linux 内核的源代码发布到互联网上，并邀请其他程序员对其进行修改和增强。
- 6. A. Richard Stallman 倡导了 GNU 背后的自由分发源代码概念。
- 7. D. 在 GPL（通用公共许可证）下，你可以自由下载 Linux 源代码并进行修改。
- 8. A. Linux 提供了一系列功能强大的电子邮件软件包，使其非常适合大型组织使用。
- 9. C, D. CUPS 服务为其他 Linux 系统提供网络打印功能。当与 Samba 结合使用时，网络打印功能可以扩展到 Windows 系统（以及任何支持 Samba 的操作系统，包括 Linux 和 Mac OS X）。
- 10. B, D. NFS 服务可用于为运行 NFS 客户端的系统提供文件共享。Samba 服务也可用于支持兼容 Samba 的客户端，例如 Windows、Mac OS X 和 Linux 系统。
- 11. A, C. MySQL 和 PostgreSQL 都是功能强大的 Linux 数据库服务。
- 12. E. Squid 服务可以将 Linux 系统转变为应用层网关。

## 使用 Linux Shell

在本章中，你将学习以下内容：

- Linux shell 的工作原理
- 使用 shell 提示符
- 获取 Linux shell 命令的帮助
- 处理环境变量
- 处理别名
- 使用重定向和管道

为了使操作系统有用，它必须提供某种方式让用户与其通信。用户需要一种方法来告诉操作系统需要完成哪些任务，例如运行程序、复制文件或关闭系统。这些命令通过用户界面下达。Linux 提供两种类型的用户界面：

- **命令行界面 (CLI)** 通过命令行界面，用户通过在命令提示符下输入命令来与 Linux 操作系统通信，如图 2-1 所示。
- **图形用户界面 (GUI)** 除了命令行界面，Linux 还为用户提供了一个易用的图形用户界面。虽然大多数系统管理员熟悉 Linux CLI，但许多最终用户并不熟悉。他们更习惯使用 GUI。由于 Microsoft Windows 在家庭计算机市场的主导地位，大多数最终用户从未使用过命令行类型的界面。为了简化生活，X 窗口系统被开发出来，以便在 Linux 操作系统上提供基于窗口的 GUI。使用 X 窗口系统以及窗口管理器和桌面环境（如 GNOME 或 KDE），用户可以使用鼠标与 Linux 内核进行交互。GNOME 图形界面如图 2-2 所示。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_60_0.png)

**图 2-1** Linux 命令行界面

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_61_0.png)

在本章中，我们将重点介绍如何使用 Linux CLI。Linux GUI 的使用和配置将在后续章节中讨论。

### Linux Shell 的工作方式

虽然图形用户界面通常更容易使用，但管理和支持 Linux 系统所需的许多任务必须通过命令行完成。基本上，最终用户使用的是 GUI，而管理员使用的是命令行。

> **考试提示** 在 LPIC-1 和 Linux+ 考试中，你对使用 Linux CLI 管理系统的能力将接受非常严格的测试。

因此，我们将在本书中花费大量时间研究 Linux 命令行界面。我们将讨论以下主题：

- Linux shells
- 管理 shell 配置文件

让我们从讨论常用的 Linux shells 开始。

### Linux Shells

要完全理解 Linux 下命令行界面是如何工作的，你需要理解 shell 的概念。Shell 是一个命令解释器，允许你在键盘上输入命令，这些命令会被发送到操作系统内核。

在 Windows 出现之前，大多数计算机用户别无选择，只能熟悉命令行 shell。在当时的各种 DOS 版本中，你与操作系统通信的唯一方式是通过一个名为 COMMAND.COM 的命令行解释器输入命令。

Linux 也使用命令行 shell。然而，与 DOS 不同，Linux 允许你从多种 shell 中进行选择。与 Linux 的许多其他方面一样，你可以尝试几种不同的命令行 shell，并选择你最喜欢的那一个。一些更流行的 shell 包括：

- **sh (Bourne Shell)** sh shell 是最早的 shell，于 20 世纪 70 年代末为 UNIX 开发。虽然它在 Linux 系统上并不广泛使用，但它仍在 UNIX 系统上频繁使用。
- **bash (Bourne-Again Shell)** bash shell 是 sh shell 的改进版本，是当今最流行的 shell 之一。事实上，它是大多数 Linux 发行版默认使用的 shell。如果你在 Linux 系统上使用命令行界面，很可能你正在使用 bash shell。
- **csh (C Shell)** csh shell 最初是为 BSD UNIX 开发的。它使用与 C 编程非常相似的语法。
- **tsh** tsh shell 是 C shell 的改进版本。它是 FreeBSD 系统中使用的默认 shell。
- **zsh (Z Shell)** Z shell 是 bash shell 的改进版本。

当你首次启动 Linux 系统并登录时，你的默认 shell 会被加载。你可以通过在命令提示符下输入 `echo $SHELL` 来识别你正在使用哪个 shell。`echo` 命令用于在屏幕上显示文本。在 `echo` 命令中添加 `$SHELL` 告诉 `echo` 显示当前登录用户的 SHELL 环境变量的内容。图 2-3 展示了一个示例，其中 bash shell 被设置为 rtracy 用户账户的默认 shell。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_63_0.png)

然而，你并不局限于默认 shell。如果你想切换到不同的 shell，只需在提示符下输入该 shell 的命令名称即可。例如，如果你当前使用 bash shell 并想改用 zsh，只需在提示符下输入 `zsh`。若要停止使用新 shell 并返回到原始 shell，请输入 `exit`。

> **考试提示** 你还可以通过修改用户账户详细信息来指定要使用的默认 shell。我们将在本书的后续章节中讨论如何执行此操作。LPIC-1 和 Linux+ 考试仅要求你熟悉 bash shell。因此，本章将仅涉及 bash。

Linux 能够同时运行多个 shell 会话。每个会话都可以运行自己的程序，且全部同时运行。如果你有一个程序在运行，然后需要访问命令提示符，这将非常有用。只需按 ALT-Fx（其中 x 是 2 到 6 之间的数字）即可打开新会话。例如，要切换到第三个备用控制台屏幕，请按 ALT-F3。然后，你可以通过按 ALT-F1 返回到原始会话。

与 Windows 一样，你还可以在 Linux GUI 中运行终端会话。这是通过运行 Konsole 或 GNOME Terminal 等终端程序来实现的。要运行多个命令行会话，只需打开两个或更多终端窗口。每个 shell 会话独立于其他会话运行其程序。如图 2-4 所示。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_63_1.png)

这也可以通过另一种方式实现。当你在 Linux GUI 中时，按 CTRL-ALT-Fx（其中 x 是 1 到 6 之间的数字）。这将把你切换到基于文本的 shell 提示符。要切换回你的 GUI 环境，请按 ALT-F7（在大多数发行版上）。

