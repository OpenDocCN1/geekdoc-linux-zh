

系统启动后，终端上会出现 login: 提示。如果你的系统配置为在启动时启动 X Window System，你会看到 X 登录屏幕而不是标准的登录提示。如果发生了这种情况，按 CTRL-ALT-F2 切换到文本登录屏幕；这在 Recipe 2.3 [Using Consoles and Terminals]，第 32 页中有进一步说明。

要登录系统，在 login: 提示符下输入你的用户名（后跟 RET），然后在提示时输入你的密码（也后跟 RET）。出于安全原因，输入密码时屏幕上不会显示任何内容；如果你在输入时出错，输入 CTRL-U 来擦除输入行并重新开始。

⇒ 要使用用户名为 “kurt” 且密码为 “empathy” 登录系统，输入：

```
Debian GNU/Linux 3.0 bardo tty1

bardo login: kurt RET
Password: empathy RET
Linux bardo 2.4.18 #1 Sat Dec 6 16:05:52 EST 2003 i686 unknown

Copyright (C) 1993-1998 Software in the Public Interest, and others

Most of the programs included with the Debian Linux system are freely redistributable; the exact distribution terms for each program are described in the individual files in /usr/doc/*/copyright

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.
Last login: Tue Apr 5 12:03:47 on tty1.
No mail.
$
```

一旦你登录，系统会显示 /etc/motd 的内容，即“每日消息”文件。然后系统会显示你上次登录的时间和日期，并报告你是否有邮件在等待（参见第 32 章 [Email]，第 611 页）。最后，系统将你置于一个 shell 中——你在其中与系统交互并向其发出命令。大多数 Linux 系统的默认 shell 是 Bash，其使用方法在第 3 章 [The Shell]，第 53 页中有讨论。

光标左侧显示的美元符号（$）称为 shell 提示符；它表示系统已准备好并等待输入。（你可以将此提示符更改为你喜欢的任何文本；要了解如何操作，请参阅 Recipe 3.5.6 [Changing the Shell Prompt]，第 80 页。）许多发行版默认将 shell 提示符设置为包含当前目录的名称，并将其放在美元符号左侧。登录时，你位于主目录中，shell 用波浪号字符（~）表示它。目录在第 5 章 [Files and Directories]，第 125 页中有说明。

NOTES：每个 Linux 系统都有自己的名称，称为系统的主机名；Linux 系统有时被称为主机，它在 login: 提示符处用主机名标识自己。为系统命名很重要；就像用户账户的用户名一样，主机名为你使用的系统提供了一个名称（当将系统放到网络上时它变得尤为重要）。系统管理员通常在系统初始配置时为系统命名（主机名可以随时更改；其名称保存在文件 /etc/hostname 中）。

与用户名一样，主机名是全部小写字母的单个单词。人们通常会给系统起一个他们喜欢的名字，例如 darkstar 或 shiva。在前面的示例中，“bardo”是这个特定 Linux 系统的主机名，该系统恰好运行的是 Debian 发行版。

你连接的终端名称显示在主机名之后。在此示例中，终端是 tty1，这意味着这是该特定系统的第一个终端。顺便说一下，“tty”是“teletype”的缩写，历史上这是大多数基于 UNIX 的系统默认使用的终端硬件类型。

### 2.2.2 Logging Out of the System

注销系统会释放你使用的终端——并确保没有人可以从该终端访问你的账户。

要结束你在系统上的会话，在 shell 提示符下输入 logout。该命令会注销你，终端上会出现新的 login: 提示符。

输入 logout 命令同样有效的方法是直接输入 CTRL-D（按住 CTRL 并按 D）。你甚至不需要在之后输入 RET。许多用户更喜欢这个快速快捷方式。

