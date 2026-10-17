
如你所示，这比使用打印机向导要简单直接得多。你还可以使用 `NET` 命令管理远程机器上的打印机队列。`NET PRINT` 命令允许你挂起打印作业、恢复打印作业或终止打印作业。有关如何使用 `NET USE` 或 `NET PRINT` 的详细信息，请参见本章末尾出现的 NET 命令摘要。

到此，我们结束对配置 Windows 98 以访问 Linux 资源的讨论。

## 使 Windows 98 资源对 Linux 可用

在上一节中，我们描述了如何配置 Windows 98，使其能够与 Linux 通过 Samba 服务器提供的 Linux 打印机资源配合。在本节中，我们将研究硬币的另一面：你如何配置 Windows 98 通过 `smbfs` 和 `smbclient` 将其资源提供给 Linux ——并让其他 Windows 98 也能使用这些资源。

# 第 16 章：将 Windows 连接到 SuSE Linux 网络

## 开启服务

在从 Linux 开始操作 Windows 98 文件共享之前，你必须让它们对工作可见。第一步是：

1. 从“Start”（开始）菜单选择“Programs”（程序）；当菜单弹出时，选择“MS-DOS Prompt”（MS-DOS 提示符）。这将打开一个可以输入 MS-DOS 命令的文本窗口。
2. （此处对应原文未在正文中详细列出的步骤 2）这将打开一个显示已连接打印机的窗口。

## 使目录联机

在从 Linux 开始操作 Windows 98 文件共享之前，你必须让它们对工作可见。第一步是：

1. 从“Start”（开始）菜单选择“Programs”（程序）。
2. （此处对应原文未在正文中详细列出的步骤 2...）这将打开一个显示已连接打印机的窗口。

## 第五部分：添加其他操作系统

在从 Linux 开始操作 Windows 98 文件共享之前，你必须让它们对工作可见。第一步是：

1. 从“Start”（开始）菜单选择“Programs”（程序）。
2. （此处对应原文未在正文中详细列出的步骤 2...）这将打开一个显示已连接打印机的窗口。

---

### 共享打印机配置步骤

4. 在打印机窗口顶部的菜单栏中，将鼠标移动到“文件”（File）。当文件下拉菜单出现时，选择“属性”（Properties）。
5. 当“属性”窗口打开时，填写内容；然后点击“共享”（Sharing）选项卡。
6. 当“共享”窗口打开时，填写内容；然后点击“确定”（OK）按钮。

对你希望工作组内其他机器使用的每个打印机重复这些步骤。这样，你的 Windows 98 机器就准备好与内网上的其他机器（包括你的 Linux 机器）共享打印机资源了。

# Windows 网络应用程序

在本章结束之前，我们将描述如何配置和使用一些最常用的 Windows 网络应用程序。你很可能熟悉 Microsoft Internet Explorer 和 Netscape Navigator，因此我们不会介绍它们。然而，Windows 还附带了其他这些实用的网络工具：

- Microsoft Outlook Express，一个功能完备的邮件管理器
- 一组 TCP/IP 工具，包括 `ping`、`ftp` 和 `telnet`
- Windows 命令 `NET` 和 `NETSTAT`，它们允许你配置网络并查看网络状态

我们将逐一讨论它们。

# Microsoft Outlook Express

Microsoft Outlook Express 是一个功能完备的邮件客户端，其工作原理类似于第 8 章中介绍过的 Netscape Messenger。简而言之，它通过 SMTP 向远程系统上传邮件，并通过 POP3 或 IMAP 从邮件服务器下载邮件。

在本节中，我们将描述如何配置 Outlook Express 并测试你的配置。

## 配置 MICROSOFT OUTLOOK EXPRESS

要开始配置 Microsoft Outlook Express，点击桌面上的 Outlook Express 图标。Windows 会做出响应并打开 Outlook Express 窗口。你现在必须为你配置一个邮件账户。邮件账户描述了你是谁、你希望如何配置邮件，以及 Outlook Express 应如何为你发送和接收邮件。请按照以下方式进行配置：

1. 点击 Outlook Express 窗口顶部菜单栏中的“工具”（Tools）。当“工具”菜单出现时，选择“账户”（Accounts）。
2. Windows 打开 Outlook Express 账户窗口。点击窗口顶部的“邮件”（Mail）选项卡；Windows 响应并打开其邮件表单。
3. 要添加新账户，点击窗口右侧显示所有当前账户的“添加”（Add）按钮。会弹出一个菜单，询问你是要创建邮件账户、新闻账户还是目录管理账户。点击“邮件”（Mail）。
4. Outlook Express 将调用一个向导来为你构建邮件账户。第一个标题为“你的名称”（Your Name）的窗口要求你输入姓名，该姓名将在邮件头部“发件人”（From:）字段显示。完成后，点击“下一步”（Next）。
5. 下一个标记为“Internet 地址”（Internet E-mail Address）的窗口要求你输入电子邮件地址，该地址将在你的消息头部“回复至”（Reply To:）字段中显示。这应该是接收邮件的地址——而不是你 Windows 机器上的地址。输入完邮件地址后，点击“下一步”。
6. 下一个标记为“邮件服务器名称”（E-mail Server Names）的窗口要求你输入下载邮件的服务器名称或 IP 地址，以及上传邮件的服务器的名称或 IP 地址。如果你输入的是名称而不是 IP 地址，请确保 Windows 知道如何通过 hosts 文件或 DNS 将这些名称解析为 IP 地址，否则它将无法管理邮件。对于入站邮件，还必须选择使用的协议——POP3 或 IMAP。完成所有操作后，点击“下一步”。
7. 下一个标记为“Internet 登录”（Internet Mail Logon）的窗口要求你输入在从下载邮件的机器上访问邮箱时所需的用户名和密码。执行此操作后点击“下一步”。
8. 最后一个窗口要求你确认已输入的内容；如果都满意，点击“完成”（Finish）。

就是这样。你已经创建了一个账户，Microsoft Outlook Express 可以从中从互联网检索邮件。

如果你希望更改定义用户账户时输入的任何信息，请点击 Internet 账户（Internet Accounts）窗口左侧窗格中的账户条目。然后点击标记为“属性”（Properties）的按钮。Windows 会显示一个表单，你可以在其中修改账户的任何信息。特别是，你应该使用此功能为账户提供一个描述性名称。

## 测试配置

要测试配置，请尝试给自己发送一封邮件。点击 Outlook Express 工具栏上的“撰写邮件”（Compose Message）按钮；Outlook Express 会打开一个窗口，你可以在其中输入消息。你应该确保使用在 Linux 机器上设置的完整电子邮件地址。消息应被上传到 Linux 机器；用户可以将消息下载回 Windows 机器。片刻后，Microsoft Outlook Express 框中应该会出现该条目。如果消息出现了，恭喜你！你的 Windows 现在可以与你的 Linux 服务器、扩展以及互联网交换邮件。

如果消息没有出现，请执行以下操作：

- 登录你的 Linux 工作站并给自己发送一封邮件。如果邮件送达，说明你的邮件服务器工作正常。如果没有到达，请检查邮件系统是否配置正确（如第 8 章所述）。
- 登录到内网之外的系统，并给自己发送邮件。如果邮件送达，说明你的互联网邮件服务工作正常。如果没有送达，请检查你到远程邮件服务器的连接是否正常。例如，如果你正在使用 `fetchmail` 下载邮件，请确保服务器的 IP 地址设置正确，并且你使用的是正确的登录标识符和密码。
- 如果你的 Linux 邮件配置区域看起来正确，请检查你的 Windows 邮件账户配置。特别是，请确保邮件服务器（入站和出站）的 IP 地址是正确的，并且访问 Linux 邮件账户的登录标识符和密码设置正确。

到此对 Microsoft Outlook Express 的讨论结束。我们的下一节涉及一些更熟悉的网络工具。

# TCP/IP 工具

回想一下，Windows 也带有一套标准的 TCP/IP 工具。这些包括 `ping`、`ftp` 和 `telnet`。即使在 Windows 这样面向图形的环境中，你可能在某些时候发现这些工具有用。

关于 `ping` 的讨论见第 6 章；第 7 章涵盖 `ftp` 和 `telnet`。

在本节中，我们重新介绍 `ping`、`ftp` 和 `telnet`，然后描述这些程序的 Windows 版本与其 Linux 类似物有何不同。

## PING：检查网络连接

在本章早前的“连接到你的内网”中，你使用 `ping` 命令来检查 Windows 机器是否可以访问内网上的其他机器。这个小程序是检查网络是否活动或另一台机器是否“在线”最快、简单的方法。

Windows 的 ping 实现与 Linux 实现非常相似。基本命令行与 Linux 版本相同：`ping hostname`。然而，Windows 版本的 ping 识别的命令行选项与 Linux 的 `datagram` 略有不同：

- `-f`——分片：在传输的数据包中设置“不分片”标记。
- `-l bytes`——发送一个大小为 bytes 的数据包。
- `-i ttl`——将数据包中的“生存时间”字段设置为 ttl。
- `-n count`——传输数据包的数量。默认为四个。
- `-r count`——计算跳数，记录数据包遵循的路径。当数据包返回源主机时，路径打印在屏幕上。
- `-t`——持续 ping 直到。这在 Linux 下是默认的，但在 Windows 下是一个选项。在 MS-DOS Shell 中，按 `Ctrl-C` 可中断命令。
- `-w milliseconds`——等待 milliseconds 后超时。例如，`ping thisisanexample -w 5000` 告诉 ping ping thisisanexample 并在五秒后超时。

## FTP：上传或下载文件

我们在第 7 章中介绍过 `ftp` 命令。快速回顾一下，`ftp` 使用 TCP/IP 文件传输协议 (FTP) 将文件上传到远程站点，或从那里下载文件。Windows 的 `ftp` 实现与在 Linux 下使用的实现几乎完全一样。在 Windows 下调用 `ftp`，打开 MS-DOS 窗口并输入命令 `ftp host`，其中 host 是要交换文件的主机的名称或 IP 地址。连接后，你可以使用它的命令来控制文件交换，正如我们在第 7 章描述的那样。

## TELNET：终端会话

`telnet` 命令与 `ftp` 命令一样，在第 7 章中介绍。简而言之，`telnet` 为你提供一个虚拟终端，通过它你可以登录到网络上基于 UNIX 的计算机并运行标准的终端会话。`telnet` 接受两个参数：

- `host` – 要连接的主机名称或 IP 地址
- `port` – 一个可选的参数，用于指定要连接的 TCP/IP 端口

Windows 版本的 `telnet` 实现与 Linux 实现的不同之处在于，Windows 版会在 Windows 桌面上打开一个窗口，而不是通过控制台或 xterm 工作。窗口顶部的命令（文件、编辑等）让你能够访问标准的 Windows 菜单。你还可以使用菜单来设置此类功能，例如要仿真的终端类型、显示器上使用的样式和字体，以及显示器的背景颜色。

> **提示**：如果你打算通过 `telnet` 运行任何带有界面的程序（例如邮件发送器 elm），你应该坚持使用默认字体。这是因为所有其他字体都是比例宽的，而 curses 库在屏幕上绘制框和表单时假设使用的是等宽字体。

到此，我们结束使用 TCP/IP 网络程序将 Windows 与你的内网连接的讨论。

# Windows 网络命令

为了结束关于如何配置 Microsoft Windows 的讨论，我们描述两个非常有用但文档较少的 Windows 命令：`NET` 和 `NETSTAT`。一本关于 Linux 的书应该详细介绍 Windows 的网络命令，这似乎是不协调的。然而，这本书的目标之一是帮助你建立一个包含许多不同类型机器的内网，而不仅仅是运行 Linux 的机器；如果你将让 Linux 与 Windows 交互，如果你熟悉一些 Windows 网络命令，你将能够更好地完成工作。

我们将依次介绍每个命令。

## NET：管理网络

Windows 命令 `NET` 执行许多网络任务。它以行引导的方式工作。`NET` 是 Windows 随带的最重要且文档记录最少的命令之一。用 Tom Yager 的话说，这是一个“如此强大的命令，仅仅是理解它就能让你获得加薪（如果你还没有工作，就能获得一份工作）”。

该命令执行多个子命令。每个子命令又可以接受若干参数。以下列表包含了子命令及其参数。如果参数位于方括号中，则它是可选的；如果两个参数之间用竖线 (`|`) 分隔，你可以选择其中一个，但不能两个都选。

### NET CONFIG

命令 `NET CONFIG` 显示当前的工作组设置。它接受一个可选参数 `/YES`，它告诉 `NET` 不要提示你输入信息或确认其操作。

### NET DIAG

命令 `NET DIAG` 显示关于网络的诊断信息。它识别两个参数之一：

- `/NAMES machinename` – 指定一个正在运行 Microsoft 网络诊断程序的机器名称。如果你没有输入正在运行诊断的 machinename，则在当前机器上运行。
- `/STATUS machinename` – 指定你想要查看诊断信息的机器名称。如果你没有输入 machinename，`NET DIAG` 会提示你输入感兴趣的机器状态的名称。

### NET HELP

命令 `NET HELP` 提供有关如何使用 `NET` 命令的信息。如果你输入 `NET HELP` 而不带参数，你将看到所有 `NET` 子命令的摘要。如果你输入 `NET HELP subcommand`，你将看到关于该子命令的详细信息。例如，要打印如何使用子命令 DIAG 的摘要，输入 `NET HELP DIAG`。

获取命令信息的另一种方法是带有参数 `/?` 输入命令。例如，要查看命令 `NET HELP` 的信息，输入 `NET HELP /?`。

参数 `/errornumber` 打印关于错误 errornumber 的信息。

### NET INITIALIZE

此命令加载协议和网络适配器驱动程序，但不将其绑定到协议管理器。可选参数 `/DYNAMIC` 动态加载协议管理器。这对于某些第三方网络解决内存问题很有用。

### NET LOGOFF

此命令断开你的计算机与在另一台机器上使用的共享之间的连接。可选参数 `/YES` 告诉命令运行时不要提示你批准其执行的操作。

### NET LOGON

此命令将用户添加到工作组。如果你不带任何参数调用此命令，它会提示你输入用户名和密码，然后用户添加到工作组。你也可以使用以下参数调用此命令：

- `user:password` – 其中 user 是用户名；最多不超过 20 个字符。可选的密码最多不超过 14 个字符。密码为 `?` 告诉命令提示你输入密码。如果你不提供密码，该用户的访问将不受密码保护。
- `/DOMAIN:name` – 将用户添加到工作组名称 name。如果你不使用此参数，该子命令将用户添加到当前工作组。
- `SAVEPW:NO` – 不为用户创建密码列表文件。
- `/YES` – 在不提示你批准其执行的操作的情况下运行。

### NET PASSWORD

此命令更改访问计算机 machinename 的密码。可选参数 `\machename` 允许你为要更改密码的机器命名。可选参数 `password` 和 `newpassword` 允许你分别提供当前密码和新密码；如果你不使用这些参数，`NET PASSWORD` 将提示你输入当前密码和新密码。

### NET PRINT

此命令显示有关打印队列的信息，或操作打印作业。在不带参数 job 的使用时，此命令显示该打印作业的状态。此命令具有以下语法：

```
NET PRINT \\machename\printer | port [job /PAUSE | /RESUME | /DELETE] [/YES]
```

- `\\machename\printer` – machename 指定你想操作的打印队列机器。printer 指定你想操作的特定打印队列。要获取插入打印器的 Linux box 的打印队列信息，使用命令 `\\box\lp`。例如，如果 Windows box 通过 Samba 打印机，使用命令 `\\thisexample\lp`。
- `port` - 你想要信息的并行端口名称（例如 LPT1 或 LPT2）。此命令仅用于直接插入 Windows box 的打印机。
- `job /PAUSE | /RESUME | /DELETE` – 操作指定队列上的打印作业。job 提供打印作业编号。选项 `/PAUSE`、`/RESUME` 和 `/DELETE` 分别暂停作业打印、恢复暂停作业的打印以及从打印队列中删除作业（或终止作业打印）。
- `/YES` – 在不提示你批准其执行的操作的情况下运行。

### NET TIME

此命令从指定的机器读取时间。你可以显示时间，也可以将你的计算机时钟与从该机器检索的时间同步。

此命令具有以下语法：

```
NET TIME [\\computer | /WORKGROUP:groupname] [/SET /YES]
```

- `\\computer` – 你想要读取时间的计算机名称。
- `/WORKGROUP:groupname` – 从 Windows 工作组 groupname 的时间服务器读取时间。

> **注意**：如果正在操作的 Linux box 队列已将作业导出到另一台 Linux 机器，这些命令都将无法按预期工作。或者准确地说，它们会工作，但由于作业被导出了，命令将不会检查实际上执行打印作业的机器上的打印队列（即作业被导出的机器）。因此，如果你打算让 Windows 用户拥有管理其打印工作的 Linux 机器上打印作业的权限，你应该在实际上打印作业的机器上安装 Samba，并让用户直接将作业缓存到该机器。这种配置设置起来稍微复杂一些，但它让 Windows 用户能够正确地管理他们的打印作业。

- `/SET` – 将你的计算机时钟设置为从计算机组名中读取的时间。
- `/YES` – 运行而不提示你确认其执行的操作。

> **注意**：如果你的 Linux 机器被设置为格林尼治时间，并使用 TIMEZONE 环境变量将系统时间设置为本地时间（这是默认设置），那么将 Windows 机器的系统时间设置为 Linux 机器的时间将导致一些奇怪且可能不受欢迎的结果。

### NET USE

使用此命令连接或断开共享，或者显示 Windows 机器已连接的共享信息。当在不带参数的情况下调用此子命令时，它会显示 Windows 机器连接的共享。它接受多个参数：

- `NET USE [drive: | *] [\\computer\directory [password | ?]] [/SAVEPW:NO] [/YES] [/NO]` – 此子命令允许你将另一机器上的目录挂载为当前 Windows 机器上的网络驱动器。可以通过驱动器号访问，就像 Windows C 盘（硬盘）或 D 盘（CD 驱动器）一样。这种形式的命令识别以下参数：
  - `drive` – 分配给该驱动器的盘符。星号 (`*`) 告诉 Windows 使用下一个可用的字母。
  - `computer` – 你将其目录挂载为网络驱动器的计算机。这可以是一台 Linux 机器，也可以是一台 Windows 机器。
  - `directory` – 挂载为网络驱动器的目录名称。注意在命名目录时使用反斜杠。
  - `password` – 为此连接分配密码。`?` 告诉 Windows 提示密码。
  - `/SAVEPW` – 告诉 Windows 保存此密码。`/SAVEPW:NO` 告诉它不要保存密码。
  - `/YES` – 自动对所有提示回答“是”。`/NO` 自动对所有提示回答“否”。
- `NET USE [port:] [\\computer\printer [password | ?]] [/SAVEPW:NO] [/YES] [/NO]` – 此子命令将另一机器上的打印机挂载为共享打印机。port 指定你分配给共享打印机的并行 (LPT) 端口名称。例如，要将 Linux 机器 thisisanexample 上的 lp 打印队列挂载为并行端口 LPT3，你需要使用以下命令：

```
NET USE LPT3 \\thisisanexample\lp
```
