

# 712 DEBIAN GNU/LINUX 2.1

apt 是“package tool”的缩写，是 Debian 2.1 中引入的新功能。从长远来看，apt 旨在完全取代 dselect 程序，并与 gnome-apt 结合实现直观的软件包管理。遗憾的是，目前还没有这一步；apt 仅处于开发阶段。

然而，通过 dselect 已经可以实现的功能允许你相当方便地从合适的设置 http 或 ftp 归档安装或更新单个软件包。在选择 apt 选项后，你必须指定一个 http 或 ftp 地址。预定义的地址是 Debian 中央服务器的地址（www.debian.org 或 ftp.debian.org）。不过，使用本地镜像要明智得多。或者，你也可以指定一个包含准备就绪归档的文件系统目录。

# UPDATE

这一步不会更新已安装的软件包，但一个内部列表存储了哪些软件包可用以及它们的版本信息。dselect 不仅为了软件包选择需要这些信息，还需要用于自动更新所有安装的软件包（例如，如果安装介质包含比原始安装更新的版本）。这些信息存储在 /var/lib/dpkg/available。

# SELECT

此选项首先进入帮助文本，随后（按下空格键后）进入一个几乎无尽的列表，显示所有可用和已安装的软件包。在这个列表中，你可以选择软件包进行安装，并标记已安装的软件包进行卸载。输入简单的 - 即可终止选择。（详情见下一个子节。）

# INSTALL

之前选择的软件包现在被安装。同时，所有在 CD-ROM 上的版本比已安装版本更新的软件包都将进行更新。（其本身，这种自动更新是一项实用的功能，有助于在任何可能的情况下将发行版保持最新状态。然而，当你突然遇到程序的新版本，导致配置文件不再工作等情况下，这种做法可能是完全正确的。如果你想防止自动更新，必须在 SELECT 阶段使用 - 将相应的软件包设置为“锁定（hold）”。

# CONFIG

通常情况下，在软件包安装期间期间，系统会立即提示你进行配置（如果需要的话）。如果发生错误，或者你现在暂时不想进行配置，可以在稍后阶段通过 CONFIG 来完成配置。已经配置过的软件包不受此影响：如果你想重新配置这些软件包，必须手动启动 /usr/sbin 中的配置脚本。

# REMOVE

在 SELECT 期间被标记为卸载的软件包现在被移除。除非该软件包被标记为完全删除（purge'），否则配置文件将被保留。

# QUIT

退出 dselect。

# Package selection（软件包选择）

dselect 中最难理解的部分可能是软件包列表，其顶部内容大致如下：

```
dselect - main package listing (avail., priority) mark+=/- verbose:v help?
EIOM Pri Section Package Inst.ver Avail.ver Description
--- Up to date installed packages ---
*** req base adduser 3.2 3.2 Add users and groups
*** req base ae 962-14 962-14 Anthony's Editor -- a
*** req base base-files 1.3.5 1.3.5 Debian Base System
--- Available packages (not currently installed) ---
Opt x11 <none> 1-4 libXG UTF fonts for X
Opt x11 9menu <none> 1.4-6 Creates X menus from
```

关于列含义的一些信息：字母 EIOM 分代表错误（error）、已安装（installed）、旧标记（old mark）和标记为（marked for）。如果 dselect 检测到依赖项冲突并更改 M 列中的设置，则 O 和 M 列之间会出现差异（见下文）。

列 E（错误）
空格：正常状态。
R（重新安装）：在之前的安装尝试期间发生错误。该软件包需要重新安装。

列 I（已安装）
空格：未安装该软件包，也没有安装任何配置文件。

+ * 软件包将被安装
- 软件包将不被安装，但之前的安装留下了配置文件。

U, C 或 I：软件包已安装，但在安装过程中发生了错误。

列 O（旧标记），M（标记）

+ * 软件包将被安装
- 软件包将被移除，但将保留配置文件。
- 软件包将同其配置文件一起移除。
= 软件包将保持不变（'hold'，阻止自动更新）。
n 软件包是新的；没有可用的安装信息。

列 Pri（优先级）
此列指定了软件包对系统的重要性。可能的值有 Req（需要）、Imp（重要）、Std（标准）、Opt（可选）或 Xtr（额外）。

列 Section（区域）
此列将软件包分配给一个类别。可能的类别有：admin, base, comm, contrib, doc, dev, editors, electronics, games, graphics, hamradio, interpreters, libs, mail, math, misc, misc, net, news, non-free, others（用于其他操作系统的工具或文件系统）， shells, sound, text, util, web 和 x11。

其余列较易描述：软件包名称、当前安装的版本号、CD-ROM 上的软件包版本、简要描述。更详细的描述可以在屏幕下半部分找到。使用 T 可以在信息文本的不同模式之间切换，你可以（在可能）使用 U 和 D 进行翻阅。

# dselect 快捷键

| | |
|---|---|
| Home, End | 跳到开头或末尾 |
| N, P | 滚动上一个/下一个 |
| Shift+B, Shift+F | 搜索 |
| +, Ins | 安装（删除） |
| = | 不更改安装状态 |
| V | 显示（详细） |
| O | 更改排序 |
| I | 更改信息（依赖关系） |
| U, D | 翻阅信息（向上/向下） |
| ← | 退出；返回主菜单 |
| ? | 显示帮助 |

通常，软件包选择的工作方式如下：你搜索软件包（主要使用 T）并使用 [+] 安装或使用 [-] 卸载。当你认为已完成所有设置时，退出 dselect。

# Package dependencies（软件包依赖关系）

一旦你选择了一个依赖于其他软件包的软件包，就会出现一个显示缺失软件包的新屏幕。此列表显示了应该安装的所有软件包。需要的软件包已被标记为安装，而仅推荐的软件包未标记。以下行显示了 tkman 的未解决依赖关系。

```
* Xtr non-free tkman A graphical, hypertext, manual page browser.
* Opt libs tk42 The Tk toolkit for TCL and X11 v4.2 - Run-Time
* Xtr non-free rman Reverse compile pages
* Opt libs tcl76 Tool Command Language (TCL) v7.6 - Run-Time
```

```
tkman depends on tk42
tkman depends on rman
tk42 depends on tcl76 (>= 7.6-0)
```

在简单的情况下，你退出依赖页面。在这种情况下，直接接受所有设置。

然而，在按下之前，你也可以使用选择可选软件包进行安装，从而更改默认设置。但是，在存在未解决依赖关系的情况下，无法离开。（如果你知道自己在做什么，可以使用 Q 强制接受你的设置。）

如果所需软件包的范围太大，你想撤销对引起冲突软件包的选择，只需按 X。

# dpkg

dselect 为软件包安装和管理提供了一个较为友好的界面，但相同的任务可以通过命令行驱动的 dpkg 命令来实现。作为 Debian 用户，你通常使用 dpkg。如果你想快速安装单个软件包（例如从额外的 contrib CD 中），dpkg 是 dselect 的高效替代方案。不同的 dpkg-xyz 命令对于你想要构建自己的软件包来说通常非常有用。

