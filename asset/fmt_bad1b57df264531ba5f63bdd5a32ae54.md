
接下来，你需要为 AWS 为你创建的虚拟机指定一些细节。

## 选择 Amazon 机器映像

首先，为你的 Linux 版本选择合适的 Amazon 机器映像 (`AMI`)。请确保选择一个标记为“符合免费层级（Free Tier Eligible）”的选项。

## 选择实例类型

确保选择了默认的实例类型 `t2.micro`。它符合免费层级，且性能足够满足你的需求。

由于你不需要配置任何高级选项，请点击**审核并启动（Review and Launch）**。

## 审核实例

你将在“审核启动”页面上看到“安全组对世界开放”的警告，这通知你任何知道实例地址的人都可以尝试连接。由于你没有在实例上放置任何内容，你可以安全地忽略此警告。

点击右下角的启动按钮，另一个屏幕将弹出。不要关闭此屏幕——这就是你选择密钥对的地方！确保选中了你导入的密钥对，如图 22-7 所示。

![](img/1b4376e88e3e983d901a0c536b9dd3c9_364_0.png)

你需要勾选“我确认我有访问私钥的权限”复框。AWS 正在警告你，如果你没有与上传的公钥关联的私钥，将无法连接到实例。启动实例将需要几秒钟。勾选此实例旁边的复框，如图 22-8 所示。

![](img/1b4376e88e3e983d901a0c536b9dd3c9_364_0.png)

图 22-8：选择虚拟机

启动成功后，你将返回 EC2 仪表板。选择实例。

![](img/1b4376e88e3e983d901a0c536b9dd3c9_365_0.png)

图 22-8：选择虚拟机

在实例实例，，，222222222222-2 所示。

![](img/1b4376e88e3e983d901a0c536b9dd3c9_365_0.png)

图 22-9：选择虚拟机

2------

-

33

3

333

333331311333333333333333333333333333333333333  222-  9。

![](img/1b4376e88e3e983d901a0c536b9dd3c9_365_1.png)

图 22-9：连接虚拟机

## 使用 SSH 连接虚拟机

在图 22-9 所示的 SSH 标签页中，你应该看到你将运行的具体命令：

```
ssh -i ~/.ssh/effective-shell ec2-user@213.71.135.ap-southeast-1.compute.com
```

此命令包含了三个部分：

- 用于连接的用户凭据，由 `-i` 标志指示；
- 连接的用户名，位于 `@` 之前；
- 主机名，或实例地址，位于 `@` 之后。

现在从你的本地运行 SSH 程序以连接虚拟机。当我运行此命令时，我会得到：

主机 'ec2-213.71.135.ap-southeast-1.compute.com (213.71.135)' 的身份无法建立。

ED25519 指纹为 SHA256:Bw6XuXaEk/BO3odiae+BWUFTunzv4XidfY6F

该密钥不被任何名称识别。你的 SSH 客户端告诉我我从未连接过这台机器，并询问我是否要继续。一旦，我的 SSH 客户端将记录机器的 IP 地址和主机名，以便以后当我连接时，它将识别这台机器。

输入 `yes` 并按回车继续连接，你应该会在 AWS Linux 虚拟机中看到 bash：

警告：已将 'ec2-213.71.135.ap-southeast-1.compute.com' (ED25519) 添加到已知主机列表中。

![](img/1b4376e88e3e983d901a0c536b9dd3c9_367_0.png)

https://aws.amazon.com/amazon-linux-2/

[ec2-user@ip-172-31-23-196 ~]$

如果你看到了来自 AWS 的此欢迎消息，你已成功通过本地机器的 SSH 程序在虚拟机上运行 shell！

你可以通过检查 `SHELL` 变量来查看正在使用的 shell：

```bash
[ec2-user@ip-172-31-23-196 ~]$ echo SHELL
bin/bash
```

现在你准备好在这台机器上运行任何你喜欢的命令了。此时，你可能会安装程序、操作文件等。当你准备好断开连接时，运行 `exit` 命令关闭与虚拟机的连接。

权限为 -rw-r--，其含义如下：

- -rw- 所有者（owner）具有读和写权限，即 dwmkererr
- -r- 所属组（group）具有读取权限，即 dwmkererr
- --- 所有用户均无权限

这并不是理想的：系统上的其他用户将被允许打开该文件，同一组的成员也将允许读取该文件。幸运的是，有一个快速的解决方法。将权限设置为仅对所有者可读写：

```bash
$ chmod 400 my-key.pem
$ ls -al
------- 1 dwmkererr dwmkererr 1103 Apr 19 12:02 my-key.pem
```

此 `chmod`（更改文件权限）命令将权限设置为 400，这意味着当前用户具有读和写权限。一旦你做了此更改，你就可以使用 ssh 连接到服务器，而不会收到关于密钥权限的报错。

## 配置 SSH 主机

记住虚拟机的细节（如主机名、密钥位置和用户名）可能会困难。为了让连接更简单更快速，你可以在 SSH 配置文件中创建一个条目来存储这些信息。这是一个点文件（dot file），类似于第 17 章讨论的用户特定特定配置文件，通常位于 `~/.ssh/config`。

要为虚拟机创建一个条目，我会在 `~/.ssh/config` 文件中添加以下内容：

```bash
Host effective-shell-aws-linux
HostName ec2-13-213-71.ap-southeast-1.compute.amazonaws.com
User ec2-user
IdentityFile "~/.ssh/effective-shell.pem"
```

此配置的第一部分是主机别名（host alias）——即当你想要连接到主机时所引用的名称。使用简短但具有描述性的名称以获得最大的便利（例如使用 `effective-shell-aws-linux`）。别名之后是一组设置，每个设置都通过制表符或两个空格缩进（缩进不是必须的，但可以帮助提高文件的可读性）：

```
Host 主机的完整地址
User 要登录的用户名
IdentityFile 连接时所需的私钥文件路径
```

现在，如果我想连接到虚拟机，只需运行以下命令：

```bash
ssh effective-shell-aws-linux
```

事实上，ssh 程序支持 shell 补全，因此我只需输入 `ssh` 和主机名的几个字母，然后按 `TAB` 键，shell 就会从我的配置中建议主机：

```bash
ssh <etab> 当我按下 Tab 时，shell 会扩展为如下：
ssh effective-shell-aws-linux
```

SSH 配置还有许多其他可用选项；你可以运行 `ssh_config` 查看所有选项。你将在第 24 章中看到一些其他选项。

## 运行 SSH 命令

你不需要实际上通过 SSH 在远程机器上运行一个 shell 来执行命令。你只需要向 ssh 程序提供你想运行的命令，它就会在服务器上执行这些命令。这是一个示例：

```bash
$ ssh effective-shell-aws-linux 'curl effective.sh | ES_EXISTING_FOLDER_ACTION=o sh'
```

```text
effective-shell: installed samples version 0.25.1 to '/home/ec2-user/effective-shell'
effective-shell: read 'effective shell' online at: effective-shell.com
```

你正在服务器上下载并运行 `effective-shell` 的示例安装程序。通常，当你安装示例时，安装程序会询问你是要覆盖、删除还是保留现有示例。这意味着它将向终端请求输入。但由于 ssh 程序并没有实际上附加到远程机器，你而是使用 `ES_EXISTING_FOLDER_ACTION=o` 选项来告诉安装程序覆盖示例。

如果你希望能够通过你的终端提供输入与服务器进行交互，请如下使用 `-t`（请求 TTY）参数：

```bash
$ ssh -t effective-shell-aws-linux 'curl effective.sh | sh'
effective-shell: downloaded samples, version 0.25.1
effective-shell: preparing to install the 'effective-shell.com' samples...
effective-shell: the '/home/ec2-user/effective-shell' folder already exists, would you like to:
effective-shell: [d]lete remove the effective folder
effective-shell: [o]verwrite extract over the existing folder
effective-shell: [q]uit
Your choice (d/o/q):
```

在这个示例中，我的终端通过 SSH 附加到远程服务器，因此我可以使用键盘为安装脚本提供输入。

## 处理断开连接

如果你经常使用 ssh 连接到远程机器，很快就会遇到连接断开或丢失网络连接的痛苦。你可能没有注意到自己已经断开连接；更常见的情况是 ssh 会话直接冻结并停止对任何输入做出响应。令人恼的是，shell 完全没有反应，以至于你无法通过 `CTRL-D` 或 `CTRL-C` 解冻它。在这种情况下，你可以使用转义序列 `ENTER` 来结束损坏的会话。

在第 24 章中，我们将查看改进这种技术的方法，但现在，如果你忘记了“波浪波浪”（tilde tilde）转义序列，最好的办法就是直接关闭你的终端程序。

当你断开 SSH 会话时，你正在运行的命令也会终止，因为 shell 发送了挂断（hang up）信号。同样，如果你想让程序在服务器上运行，这可能会令人沮丧。你将在第 24 章学习如何处理这种行为。

## 使用 scp 传输文件

你可以如下使用 `scp`（OpenSSH 安全文件复制）程序从任何你有访问权的远程机器复制文件：

```bash
scp 参数 源 目标
```

你提供给 `scp` 的许多参数与 `ssh` 命令的参数相同，例如用于标识文件的 `-i`。源和目标通常是一对：一个本地，一个远程。然而，你也可以在两个远程机器之间进行复制。

这是一个 `scp` 命令的示例：

```bash
scp -i ~/.ssh/my-project.pem ~/project/output.zip dwmkerr@myserver.com:
```

- `-i` 指定密钥路径。
- 源是本地机器上名为 `output.zip` 的文件。
- 目标是主机名为 `myserver.com` 的服务器，使用用户 `dwmker` 连接，并放在用户的家目录下。

下面的 `scp` 示例将 `downloads.zip` 文件夹复制到本地的 `~/backups` 文件夹：

```bash
scp -P 8022 effective-shell.com:~/backups
```

```bash
[ec2-user@ip-172-31-23-196~$] chmod ./lookup.py
[ec2-user@ip-172-31-23-196~$] ./lookup.py cryptography > definition.txt
[ec2-user@ip-172-31-23-196~$] exit
```

logout

Connection to ec2-13-213-135.ap-southeast-1.compute.amazonaws.com. closed.

$ cp effective-shell-aws-linux:~/definition.txt

definition.txt 100% 277 1.0KB/s 00:00

$ cat definition.txt

cryptography: 关注通信安全的学科（例如消息的机密性、消息的完整性、发送者身份验证、消息不可否认性以及许多其他相关问题），无论使用的媒介是铅笔纸还是计算机。

在服务器上运行脚本之前，你需要使用 `chmod` 命令来确保脚本可以执行。就是这么简单！一旦你了解了 ssh 的工作原理，使用 `scp` 在远程机器之间传输文件和文件夹将非常容易。

你可以使用 `scp` 执行许多其他操作；要了解更多关于该工具的信息，请运行 `scp`。

## 总结

在本章中，我们讨论了 SSH 协议以及如何使用密钥连接到远程服务器。你学习了如何设置 AWS 账户、创建一个带有公钥的虚拟机、使用 `ssh` 程序连接到它，以及如何配置 SSH 别名来加快连接速度。你还看到了网络连接方面的一些挑战（第 24 章将向你展示处理这些问题的一些技术），并学习了如何与远程机器之间复制文件。

现在你已经可以连接到远程服务器了，你需要知道如何在其中进行工作。下一章将介绍终端编辑器，它们允许你在不离开 shell 的情况下快速处理文本，这对于没有桌面环境的远程机器或系统来说是完美的解决方案。

# 23

# 终端编辑器的威力

终端编辑器是一种运行在 shell 中的文本编辑器，针对键盘而非鼠标进行了优化。在对远程机器或没有桌面环境的系统进行工作时，它有时是唯一的选择。但即使你有可用的基于桌面的编辑器，从 shell 运行终端编辑器对于许多文本处理任务来说可能更高效。

一些最流行的终端编辑器有 Vim、Emacs 和 GNU nano。本章将重点介绍 Vim，向你展示几个功能，希望这些功能能激发你深入探索其能力的兴趣。

许多用户起初觉得终端编辑器很难使用，而且某些编辑器（包括 Vim）有极其复杂的声誉。所以，让我们先讨论一下你为什么想要使用它。

## 为什么要使用终端？

许多技术人员熟悉桌面环境环境的文本编辑器，例如 Visual Studio Code、Notepad++ 和 Sublime。软件工程师可能会熟悉集成开发环境（IDE），例如 Visual Studio 和 JetBrains 家族的 IDE，这些环境包含了针对许多语言（如 C# 或 Java）的专用环境。

在有许多强大且易于使用的文本编辑选项的情况下，你为什么选择终端编辑器呢？

原因有很多，但也许最令人信服的理由是你没有可用的桌面环境。如果你像第 22 章描述的那样通过 ssh 在远程服务器上工作，可能没有正在运行可以打开图形化工具的桌面环境。在这种环境下，编辑文本、代码或脚本的最简单选项可能是终端编辑器，因为终端是你与服务器交互的主要界面。如果你在 Docker 容器等轻量级 Linux 环境中编辑文件，可能也无法轻松访问桌面环境。

以下是熟悉终端编辑器的其他一些理由：

- **最小化工作流中断**：如果你已经在 shell 中工作并需要编辑文本，能够在不离开 shell 的情况下快速完成操作（理想情况下甚至不需要触碰鼠标），可以让你在工作时保持心流。
- **编辑效率**：一旦你度过了最初的学习曲线，使用 Vim 和 Emacs 等编辑器编辑文本将变得极其高效。特别是，它的设计初衷是尽可能让你的手指留在键盘的起始行上，这样你就可以非常快速地处理文本。
- **自定义选项**：你可以根据自己的工作风格自定义终端编辑器，并通过第 17 章描述的、跨环境共享的点文件（dot files）来管理这些自定义。
- **向图形界面编辑器和其他工具的可扩展性**：如果你学会了使用 Vim 或 Emacs 并熟练掌握它们的用法，你可以在图形界面编辑器或 IDE 中安装插件，让你能够使用相同的命令编辑文本。甚至有浏览器插件可以让你使用 Vim 风格的移动命令浏览网页。这让你能够将键盘界面的效率带到现代桌面编辑器中。

总而言之，掌握终端编辑器的基础知识是非常有用的。在与远程机器工作和从 shell 编辑文本时，你会变得更高效，你可能发现像 Vim 这样的编辑器可以替代你许多任务中的其他工具。

## 开始使用 Vim

Vim 是一个非常流行的编辑器，大多数 Linux 发行版都预装了它。但它的编辑样式——模式编辑（modal editing）起初可能会让人困惑。你投入练习的时间越多，你的效率就会越高。

一些最流行的终端编辑器有 Vim、Emacs 和 GNU nano。本章将重点介绍 Vim，向你展示几个功能，希望这些功能能激发你深入探索其能力的兴趣。

许多用户起初觉得终端编辑器很难使用，而且某些编辑器（包括 Vim）有极其复杂的声誉。所以，让我们先讨论一下你为什么想要使用它。

键盘快捷键与敏感性

在命令模式下，状态栏会显示 Vim 处于何种模式。某些命令像组合键（chords），有些像序列（sequences）。

- **组合键**：同时按下的键（例如 `CTRL+C`）。
- **序列**：一个接一个按下的键。

在插入模式下，状态栏显示 -- INSERT -- 要返回命令模式，按下 `ESC`。

在执行模式下，状态栏显示一个冒号 (`:`)。执行模式像插入模式，但是用于编写命令。要执行管理任务（如保存文件或调用另一个程序），你需要切换到执行模式（ex 是 execute 的缩写）。

让我们使用 `q!`（不保存退出）命令关闭 Vim。现在输入该命令：

```
:q!
```

你现在已经看到了 Vim 模式编辑的基础。现在你将开始构建自己的快捷查表，以探索它的更多功能。

## 构建快捷查表

构建 Vim 快捷查表是展示 Vim 能力的一种极方法，同时在这个过程中记录你的学习情况。随着时间的推移，你将用最有用的命令扩展你的查表。

首先创建一个存储清单的文件夹，并初始化一个空的 Git 仓库以跟踪其更改：

```bash
$ mkdir ~/vim-cheatsheet
$ cd ~/vim-cheatsheet
$ git init -b main
```

# 创建文件
