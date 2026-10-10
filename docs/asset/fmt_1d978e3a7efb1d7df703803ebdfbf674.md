
`ssh` 是用于安全登录远程服务器的协议。通过 `ssh 用户@IP地址`，你可以建立加密连接。它使用加密密钥来传输数据，确保了安全性。

## 20. chmod

### 核心命令

用户权限是 Linux 安全中最重要的需要理解的部分。每个文件都有权限，定义了谁可以查看；谁可以读取和写入文件；以及谁可以将其作为程序执行。权限可以由访问者更改，但只能由特定用户更改；或者如果涉及到需要更改的目录并将其视为一个可更改的安装，这也是最基础的操作。

Wordpress 应该能够写入文件以便进行更新，但也有许多文件你不希望它们被更改——除非你这样做，否则你真的不想给它执行权限。问题是，许多插件需要某些权限，而且同样需要修改默认被锁的文件。

三个数字用于表示组内成员和其他人可以做什么。每个数字范围在 0-7 之间，其中 7 允许读取、写入和执行，而 1 仅允许执行。如果你的用户文件就绪，语法为：`chmod mode filename`。为了让所有用户都能读取和写入某个文件，出于各种原因，在 Web 服务器上留留此类文件并不是良好做法。如果你不需要该文件，需要将其添加到前面。

当你使用 `kill` 时，处理与应用程序名称匹配的进程。`kill` 会关闭 Linux 桌面上的带有浏览器的关闭窗口。

```
chmod 644 /etc/passwd
chmod 600 /etc/shadow
chmod 644 /etc/group
chmod 600 /etc/gshadow
chmod 440 /etc/sudoers
chmod 440 /etc/sudoers.d/
chmod 644 /etc/sudoers.d/*
```

- 从某个间隙到单行出现的命令。（注：OCR 文本错误 "From the whereas of gap" 可能指的是特定的命令上下文）。

- 如果你没有登录系统，那么还有另一个命令可用。你可以使用 `w` 来列出所有活动用户，尽管不要过度依赖它，因为对于黑客来说隐藏自己并不困难。

## 15 密码

请极其小心地使用密码。因为你书写的下一个单词将出现在你的登录密码之后，所以如果你输入错误，它就会消失，让你不得不自己去寻找。

默认情况下，你可以更改任何用户的密码，但如果你使用 `sudo`，可以使用用户名作为密码更改你的用户凭据。输入 `sudo passwd`，同时更改 root 用户的密码。

查看手册页（`man passwd`）以获取一些在一段时间后更改密码的有用选项等。

## 10 nano

- 命令的使用方式如下：

- 这将文件移动到该文件夹，前提是它位于正确的位置（如果不确定，请使用 `la`）。

`cd /path/file` 这将更改你在主目录内（`~` 字符）的文件位置。使用 `cd` 从你的主目录开始。以 `/` 开头将 `cd` 到驱动器根目录的路径。

如果你用过文本编辑器，它会在文本终端中为你提供复杂的程序。有几种文本编辑器不会修改文件：nano 和 vi。你也可以通过输入 `nano path/to/test.txt` 来编辑任何文件（vi 也是如此）。某些术语对你来说可能很奇怪。例如，按 Ctrl+O 保存更改。

## 17 历史

如果你整天都在忙于从网上复制粘贴命令，你可能想检查一下你到底做了什么。你可以使用 `history` 来获取你追溯很久以前执行的所有命令的列表。命令用数字编号，你可以使用向上和向下箭头返回最近的命令（并通过按回车键重新发送），或使用 Ctrl+R 搜索命令。

> 快速提示
>
> 一个很有价值的命令是 nano 的缩写。这个组将帮助其他朋友。要了解所有命令，只需查看此处。

`rm` 用于移除删除文件，`cp` 用于复制文件和文件夹。就像 `cd` 一样，你也可以在正在工作的目录中输入文件名或从驱动器根目录开始的路径。使用 `rm -`...

## 19 mv & cp

`mv` 用于重命名文件，将其作为文件管理器使用会变得简单且体验非常快速。当我们 `cd` 时，你需要记住的三个基本命令是 `rm`、`mv` 和 `cp`。`mv` 命令用于将文件从一个位置移动到另一个位置。

黑客手册 | 159

![](img/1e7c2db42dac866a51a0ace7df48feef_159_0.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_1.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_2.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_3.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_4.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_5.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_6.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_7.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_8.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_9.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_10.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_11.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_12.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_13.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_14.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_159_15.png)

理解我们生活的的世界，从科学和技术开始。从我们这里直接购买可以节省大量费用。100 种优秀标题，随处可用。全球配送，超安全订单。

![](img/1e7c2db42dac866a51a0ace7df48feef_160_0.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_1.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_2.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_3.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_4.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_5.png)

## 用书籍滋养你的大脑

探索宇宙的秘密，从恐龙时代到现代科学的奇迹！

![](img/1e7c2db42dac866a51a0ace7df48feef_160_6.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_7.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_8.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_9.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_10.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_11.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_12.png)

![](img/1e7c2db42dac866a51a0ace7df48feef_160_13.png)

> 发现最迷人问题的答案

![](img/1e7c2db42dac866a51a0ace7df48feef_160_14.png)

在 Instagram 上关注我们 @futurebookazines

www.magazinesdirect.com

杂志、过刊和书籍杂志。

## 订阅并节省高达 61%

直接送达家门或直接发送到设备

![](img/1e7c2db42dac866a51a0ace7df48feef_160_0.png)

从 80 多种杂志中进行选择，比商店价格节省大量费用！

也提供装订本、书籍和过刊。

只需访问：www.magazinesdirect.com

* 无隐藏费用 | 所有价格均含运费 | 我们配送至 100 多个国家 | 安全在线支付

![](img/1e7c2db42dac866a51a0ace7df48feef_161_1.png)

## 2022 黑客手册

## 164 页内容充实的页面！包含其他 Linux 手册不会告诉你的黑技巧

**安全** 利用漏洞并拦截攻击

**LINUX** 发现并定制内核

**隐私** 锁定你数据的每一个字节
