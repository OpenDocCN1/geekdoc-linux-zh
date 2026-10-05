

## 1.13 我完成了安装。我如何第一次登录？

作为 root 用户，"root" 是在初始安装后唯一存在的账户（较较新的安装程序会在安装期间提示你创建一个普通用户账户）。登录示例如下：

```
my_machine_name login: root
Password: my_password
```

在上面的示例中，我在登录提示符处输入了 "root" 单词。之后，我输入了在初始 Linux 安装期间选择的密码。输入密码时屏幕上不会显示（出于安全考虑）。

"root" 是一个对系统拥有绝对权限的特殊账户，用于系统管理。你肯定想以后至少创建一个“user”（用户）账户来执行常规（而非系统管理）工作。请继续阅读了解如何操作。

前往第 2 部分：Linux 资源、帮助和一些链接

# Linux 新手管理员指南

vver. 0.56 1999-10-29

# 第 2 部分：Linux 资源、帮助和一些链接

由 Peter, Stan 和 Maria Klimas 编写

一些常见 Linux 问题的解答
根据通用公共许可协议发布：http://www.gmu.org/copyleft/gpl.html。欢迎您的反馈、意见、修正和改进。请发送至 bklimas@magma.ca

# 网站快速导航：

- - 开始：Linux 新手管理员指南
- 第 0 部分：针对犹豫者（Linux 的优势）
- 第 1 部分：Linux 安装之前
- 第 2 部分：<Linux 资源、帮助和一些链接>
- 第 3 部分：基本操作 FAQ
- 第 4 部分：Linux 新手管理员 FAQ
- 第 5 部分：如何升级内核
- 第 6 部分：Linux 快捷键和命令
- 第 7 部分：核心 Linux 应用（无论是否专利）

# 本页目录：

# 2. Linux 资源、帮助和一些链接

- 2.1 有任何 Linux 阅读材料？[页 21]
- 2.2 有 help 命令吗？[页 22]
- 2.3 [页 23]
- 2.4 有任何 Linux 互联网链接吗？[页 24]

# 2. Linux 资源、帮助和一些链接

## 2.1 有任何 Linux 阅读材料？

检查你的 RedHat CD 中是否有 RedHat 手册的软拷贝（专为新手编写）。
在 Linux 下，你可以阅读它：

```
lynx /mnt/cdrom/doc/rhmanual/manual/index.htm
```

这将启动 lynx，一个简单的文本模式 HTML 浏览器，用于查看手册。你也可以使用 Netscape 或任何其他 html 浏览器。如果你的 RedHat 还没有安装，你可以使用基于 Windows 的浏览器查看手册，例如适用于 Windows 的 Netscape。只需访问 CD 上上方命令所示目录下的 `index.htm` 文件即可。

如果你已经安装了 Linux，请检查 `/usr/doc/LDP` 获取优秀的 Linux 文档项目（Linux Documentation Project）手册。（如果你没有安装文档，考虑现在安装所有内容。）例如，这些命令将让你浏览《Linux 管理员指南》：

```
cd /usr/doc/LDP/sag
lynx.sag
```

此外，检查 `/usr/doc/HOWTO` 获取 HOWTO 文档，检查 `/usr/doc/HOWTO/mini` 获取 MINIHOWTO。检查 `/usr/doc/FAQ` 获取一组 FAQ。例如，这些命令将让你在光驱上查看 Linux-FAQ（必须先挂载光驱）：

```
cd /mnt/cdrom/doc/FAQ/txt/
less Linux-FAQ
```

由于 RedHat CD 上也有这些文档，因此你可以在 Linux 安装之前阅读它们。例如，假设你在 DOS 下的光驱是 D: 盘，这将让你在 DOS 下阅读 Linux-FAQ：

```
d:
cd \FAQ\txt
edit Linux-FAQ
```

更多或更新的文档，请参 http://metalab.edu/mdw/index.html。

## 2.2 有 help 命令吗？

大多数 Linux 命令可以使用 `--help` 选项运行。例如：

```
cp --help | less
```

通过命令行使用所谓的 `man` 页面访问更广泛的信息。例如：

```
man cp
```

将显示 "cp" 命令的手册页。手册页是 Linux 下标准的 "help" 系统，包含了丰富的详细信息，但通常需要花费精力理解。`man` 命令使用一个名为 `less` 的简单工具让你滚动文本。使用方向键滚动，按 "q" 退出。实际上，`info` 比这个更强大。按 "h" 查看运行 `less` 时的信息，或者学习使用 `man`。

还有 `info` 命令。例如：

```
info cp
```

如果你不确记得需要使用的命令名称，请尝试 `apropos`。例如，获取与 "copy" 相关的命令列表：

```
apropos copy
```

在菜单驱动的程序中，特别包括一个基于 GUI 的 "help" 浏览器，可以通过点击面板上的“书本”图标启动。该浏览器可以访问特定服务的帮助以及系统手册页。如果你想了解安装在 CD 上的许多 rpm 格式的软件包，你可能需要使用基于 kde 的 `info`（在 RH6.0 下，`info` 程序被 `man` 取代，后者快得多，但也不太方便）。

## 2.3 新闻组 (Newsgroups)

这是一个令人敬畏的地方——对于恶意的帖子，我在这里开个例，并通知他们的邮件提供商。

在进入新闻组之前，我强烈推荐 DejaNews (http://www.dejane.com/home_ps.html)。这是一个巨大的新闻组帖子存档，你可以使用搜索工具进行查询。无需翻阅大量垃圾信息，就能找到你问题的答案，也不会在发布一个“本周已被问过十次”的问题后让自己尴尬。你可能会对 DejaNews 的可用信息感到惊讶。

有几个致力于 Linux 的新闻组，似乎比其他新闻组更好（可能是 Linux 专家？）。这里有一个短列表：

- news:comp.os.linux.announce（受制的——帖子由版主在发布前进行审查。任何消息的页脚都包含关于如何发布的信息。）
- news:comp.os.linux.help
- news:comp.os.linux.setup
- news:comp.os.misc（杂项）
- news:comp.os.linux.advocacy（用于讨论 Linux 的优缺点，也许以及与其他系统的对比。）
- news:alt.linux.suz（在这里你可以阅读/编写关于 Linux 的真实观点。）
- news:comp.os.linux.networking
- news:comp.os.linux.x（X-windows）
- news:comp.os.unix（通用 UNIX 组）

请注意新闻组礼仪（网络礼仪），主要要点包括：
- 不要在一个与新闻组主题无关的话题上发帖；
- 不要同时向多个新闻组发帖（交叉发帖）；
- 使用纯 ASCII，不要发帖附件、图片、html 等；
- 不要打广告（特别是商业产品）。

有用的缩写：

| | |
|---|---|
| BTW | "顺便说一下"(By the way,) |
| AFAIK | "据我所知"(As far as I know,)（其实他们清楚，但很谨慎） |
| RTFD | "仔细读文档!"（不利且可能没礼貌） |
| ASAP | "尽快"(as soon as possible) |
| FYI | "供你参考"(For your information,)（意味着大家都知道。如果他把它放在新闻组里，他不能意味着它是机密的，对吧？） |
| IMHO | "我个人的浅见"(有很多变体，也通过其他表情来表达情绪。） |
| :-) | |
| c.o.l.a. | 新闻组 comp.os.linux.announcement (也许是 comp.os.linux.advocacy?) |
| Tia | "提前感谢!"(Thanks in advance!) |
| iirc | "如果我没记错的话"(If I remember correctly,) |
| fwiw | "尽管其价值有限"(回答者觉得答案可能不是决定性的。) |

如果你知道其他新手 Linux 管理员应该应该了解的缩写，请告诉我。

## 2.4 有任何 Linux 互联网链接吗？

一定有成千上万个致力于 Linux 的 网站。这里是我喜欢的 Linux 链接，按特定顺序排列。如果你需要其他内容，你应该能在这些页面找到有用的线索。

