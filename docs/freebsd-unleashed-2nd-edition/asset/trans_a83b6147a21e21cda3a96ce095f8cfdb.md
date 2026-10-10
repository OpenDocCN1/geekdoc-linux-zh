
 predecessors (Windows 3.1、DESQview 以及短命的 MS-DOS Shell)。许多程序会提供“退出到 shell”（shell out）到 DOS 或命令行界面的选项。这种选项在早于多任务操作系统或基于终端的程序中很常见，在这些程序中，你通常只能打开一个窗口来访问系统。在这些情况下，“退出到 shell”意味着从你当前所在的程序内部执行一个 shell 程序（例如 DOS 或 Unix 命令行），并在你执行位于其“上方”的操作时挂起该程序。

在第 7 章中，我们查看了 FreeBSD 中各种专为充当 shell 设计的程序选择，这里的 shell 是指能够运行专门 shell 脚本语言脚本的命令解释器。这些程序中的一些包括 sh、csh、bash、ksh 和 tcsh；这些 shell 在行为和支持的编程语言上存在细微差异。第 12 章“Shell 编程”涵盖了 Bourne shell（sh）环境中的脚本编写，这是迄今为止最流行的环境。然而，现在我们将把注意力转向一个更平凡且日常的话题：配置你所选择的 shell 以适应你的口味和需求。

在我们这样做之前，我们必须查看如何将未包含在基础系统中的 shell 添加到 FreeBSD，以及如何从一个 shell 切换到另一个。

## 向系统添加 Shell 并使其可用

大多数用户可能会满足于默认的 FreeBSD shell /bin/tcsh（与 /bin/csh 相同）。它提供了命令行编辑、Tab 补全、历史记录以及其他在更基础的 shell 中缺失的高级 shell 功能。然而，FreeBSD 默认使用 tcsh 而不是 bash（在 Linux 中常用）这一事实，反映了 BSD 传统和 System V 架构（后者构成了 Linux 架构的大部分）之间微妙的哲学差异，这一争论与 Unix 本身的历史一样悠久。过去，这些哲学差异比今天意义重大得多。商业版本的 Unix 通常归属于这两个阵营中的一个，并且多年来几乎没有实质性的变化；然而，在 Linux 和 FreeBSD 之间，更重要的哲学差异在于 GNU 和 BSD 许可证结构之间。这就是我们看到 Linux 偏好 bash 而 FreeBSD 偏好 tcsh 的根源所在。

因为 bash 是一个面向 GNU 的程序，并且因为 Linux 倾向于偏好在 GNU 通用公共许可证（GPL）下开发的软件，所以 bash 是 Linux 的默认 shell。bash 和 tcsh 的功能集非常相似，但这些功能以不同的方式访问，且这两个 shell 的配置过程和运行时行为存在细微差异。如果你习惯了 Linux，为了保持在熟悉的环境中，你可能想要安装 bash。另一方面，你可能来自一个你的 shell 是 ksh 或 zsh 的系统。安装和使用这些 shell 不成问题，正如你将在本章的下一节中了解到的那样。

本章剩余的部分将检查 *tcsh* 和 *bash*，展示每个 shell 在配置和使用上的差异。对于其他 shell，你需要自行处理——你需要安装这些 shell 并阅读它们的 *man* 页面以获取详细信息。

### 从 Ports 或 Packages 安装 Shell

在 FreeBSD 上安装软件的推荐方式是通过 *ports* 或 *packages*，这在第 14 章“安装附加软件”中有详细描述。该章解释了如何使用 ports 集合和 packages 来满足你所有的软件管理需求。然而，本节涵盖了安装新 shell 的最基本命令和步骤。

### 从 Packages 安装

通过 *sysinstall* 及其面向包管理器的接口安装新 shell 是最简单的方式。运行 */stand/sysinstall*，选择 *Configure*，然后选择 *Packages*。选择你的安装介质——如果你手头有 FreeBSD 安装 CD，则选择 CD-ROM；否则选择 FTP。

在你收到包列表后，进入“shells”子部分，并浏览可用 shell 的列表。按下空格键，在你想要安装的每个 shell 上标记一个 ×。完成选择要安装的 shell 后，按一次 *Enter*，你将返回到主要的包选择屏幕。使用右箭头键选择 *Install*，然后按 *Enter*。然后在显示所选包的确认屏幕上选择 *OK*。

现在软件将自动下载并安装。完成后，通过返回到 Configuration 菜单顶部的 *Exit* 选项来退出 *sysinstall*；然后从屏幕底部选择 *Exit Install*。你选择的 shell（多个或一个）现在已安装。你可以通过查看 */usr/local/bin* 并阅读已安装 shell 的 *man* 页面（例如 *man bash*）来验证此安装。

### 从 Ports 安装

安装软件的另一种方式，也在第 14 章中有描述，是使用 *ports collection*。这是一种结构严谨的方法，用于在你的机器上编译和安装软件，同时保证安装的文件将被放置在正确的位置（例如，根据 FreeBSD 层级规则，位于 */usr/local* 内部）。如果安装了 ports collection，它位于 */usr/ports*，并包含与通过 *sysinstall* 浏览 packages 时发现的相同的层级结构。

进入 */usr/ports/shells* 并查看一下。这是 ports 集合中相当小的一部分；*usr/ports* 的大部分其他类别（子目录）都有更多可用的程序供你安装。以下目录列表显示的每个目录都包含一个 makefile、各种校验和和补丁文件，以及一个打包列表。

- 44bsd-csh/
- Makefile
- bash1/
- bash2/
- es/
- esh/
- fd/
- flash/
- ksh93/
- mudsh/
- nologinmsg/
- osh/
- pash/
- perlsh/
- pkg/
- podsh/
- rc/
- sash/
- tcsh/
- vshnu/
- wapesh/
- zsh/
- zsh+euc_hack/
- zsh-devel

你所要做的就是进入该目录并输入 **make**；系统将获取发行版文件，解包、打补丁、配置并编译它。然后你需要输入 **make install** 来安装包，并输入 **make clean** 来删除构建过程中创建的所有临时文件：

```bash
# cd /usr/ports/shells/bash2
# make
...
# make install
...
# make clean
...
```

一旦此过程完成，新的 shell 将被安装并可供使用。

> **注意**
> 安装任何新程序后，你可能需要输入 **rehash**（如果你使用的是 **tcsh**），以强制 shell 程序重新读取你的 shell 配置文件以及路径中可用的程序；否则，除非你注销然后再登录，否则你将无法访问这些程序。

### /etc/shells 文件

在处理 shell 时，你需要了解的一个重要系统文件是 /etc/shells。此文件包含系统中已安装的 shell 的名称，并列出了它们的完整路径。以下是一个示例，展示了一个工作系统上 /etc/shells 的内容，该系统安装了三个额外的 shell：

```text
# cat /etc/shells
# $FreeBSD: src/etc/shells,v 1.3 1999/08/27 23:23:45 peter Exp $

# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/sh
/bin/csh
/bin/tcsh
/usr/local/bin/bash
/usr/local/bin/zsh
/usr/local/bin/ksh
```

`/etc/shells` 的目的是指定你，作为管理员，认为“有效”的 shell 程序。`chsh` 程序（我们稍后将讨论）不允许普通用户将其默认 shell 更改为你未在 `/etc/shells` 中列出的任何程序。这种安全措施允许你确保用户不能将其默认 shell 更改为未设计用作 shell 的程序。特别有问题的是 `setuid` 程序，即具有所有者用户有效 UID 的程序（如第 9 章“用户、组和权限”中所述）。如果 `setuid` 程序由 root 拥有，它可以执行具有 root 特权的任何操作；显然，用户仅仅通过登录就获得这些特权是不可取的。

用户的 shell 指定在 `/etc/master.passwd` 用户数据库中，位于用户记录的第 10 个字段（或 `/etc/passwd` 中的第 7 个字段），如你在第 7 章中所见。这是一个示例：

```text
/etc/master.passwd:
foo::*:$1$SLXZkCuzDS70a8LyRgbjY0b.XrXiBad.:1001:1001::999066364:0:
Foo Bar:/home/foo:/usr/local/bin/ksh

/etc/passwd:
foo:*:1001:1001::Foo Bar:/home/foo:/usr/local/bin/ksh
```

如果该字段的值（在本例中为 `/usr/local/bin/ksh`）设置为 `/etc/shells` 中出现的 shell，则用户被允许使用 FTP 等服务登录。如果不是，则被拒绝。

此外，`/etc/shells` 用于生成在 `adduser` 过程中可以分配给用户的可用 shell 列表，我们在第 9 章中涵盖了这一点。

每次通过 ports 或 packages 安装 shell 时（如前所述），都会自动向 `/etc/shells` 添加条目。请注意，虽然只有管理员（root）可以将用户的 shell 更改为 `/etc/shells` 中未列出的程序，但无论分配的 shell 是否出现在 `/etc/shells` 中，用户都可以登录为 shell 用户。`shells` 数据库还控制通过 FTP 对系统的访问。一个常见的陷阱是管理员在没有使用 ports 或 packages（因此不会向 `/etc/shells` 添加条目）的情况下安装 shell，然后切换到该新 shell（因为管理员被允许这样做）。普通用户可以使用 `telnet` 或 `ssh` 毫无问题地访问机器，但一旦他尝试通过 ftp 访问，就会被无缘无故地拒绝访问。解决此问题的方法很简单，确保用户的 shell 列在 `/etc/shells` 中。始终使用 ports 或 packages 正确安装 shell。

