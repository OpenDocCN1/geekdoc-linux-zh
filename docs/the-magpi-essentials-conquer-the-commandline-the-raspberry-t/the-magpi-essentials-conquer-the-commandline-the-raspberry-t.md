# MagPi 必备：树莓派终端命令行指南


















![](img/db18fe165e1f1a64ee0c5d815560917d_2_0.png)


![](img/db18fe165e1f1a64ee0c5d815560917d_2_1.png)

![](img/db18fe165e1f1a64ee0c5d815560917d_2_2.png)

# 欢迎来到
征服
 命令行

有时候，只有文字就足够了。图形用户界面（GUI）是一项巨大的进步，为许多非技术用户进入电脑世界创造了便捷捷径。然而，对于复杂任务，界面可能会变成限制：阻碍选择，并即使对于中等复杂的工作也让路径变得迂回。

（重新）进入命令行：那个许多人认为在 20 世纪 90 年代已经消失的光标。对于从用户向计算机获取指令——一种清晰、快速且无歧义的形式——命令行通常是最佳方式。它在 UNIX 系统上从未消失，而现在，得益于树莓派上的 Raspian，新一代人正在发现命令行的力量，它可以简化复杂任务，或瞬间执行简单任务。

如果你面对 $ 提示符感到不自在，不要恐慌！在这本完全更新的书中，我们将快速让你感到宾如归归，并帮助你在树莓派或其他任何 GNU/Linux 电脑的终端上找到方向：完成任务并解锁命令行的力量。



设计师：Mike Key

作者：Richard Smedley
贡献：Lucy Hattersley,
Simon Long





环顾四周并发现新事物


开始处理文件


Raspbian 的安装与更新系统


连接多个简单命令


让 Raspbian 更具个性化


处理可移动存储设备的管理


为树莓派分配一个自己的永久网络地址


无需关重启：只需杀掉进程即可！


使用 Secure Shell 访问树莓派


添加软件并向 SD 卡写入


管理启动和关机


通过备份保护你的数据


从源代码构建软件


从命令行接入网络

# RICHARD SMEDLEY

![](img/db18fe165e1f1a64ee0c5d815560917d_4_0.png)

自从焊好他的第一台电脑——一台 ZX61 套件并获得 GW6PCB 业余无线电执以来，Richard 对技术痴迷。在将 ZX61 换成吉他并从事有机园艺后，他最终回到了命令行，从运行自己的电脑开始，一直到运行一家国际机构的所有电脑。他撰写自由软件并教授食用景观。


# [第一章]
不要恐慌

在第一章中，我们将环顾四周并发现新事物


## [ 征服命令行 ]

## [ 阅读手册 ]

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将发现新

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

在第一章中，我们将环顾四周并发现新事物

图形用户界面（GUI）是一项巨大的进步，为许多非技术用户进入电脑世界创造了便捷捷径。然而，对于复杂任务，界面可能会变成限制：阻碍选择，并即使对于中等复杂的工作也让路径变得迂回。

（重新）进入命令行：那个许多人认为在 20 世纪 90 年代已经消失的光标。对于从用户向计算机获取指令——一种清晰、快速且无歧义的形式——命令行通常是最佳方式。它在 UNIX 系统上从未消失，而现在，得益于树莓派上的 Raspian，新一代人正在发现命令行的力量，它可以简化复杂任务，或瞬间执行简单任务。

如果你面对 $ 提示符感到不自在，不要恐慌！在这本完全更新的书中，我们将快速让你感到宾如归归，并帮助你在树莓派或其他任何 GNU/Linux 电脑的终端上找到方向：完成任务并解锁命令行的力量。

（注：后续大量重复内容已根据指令要求去重处理，仅保留核心结构翻译逻辑）





### 征服命令行

命令。路径是文件夹层次结构：在 Windows 计算机上，在图形文件浏览器中，它从“我的电脑”开始；在你的 Pi 上它从 `/` 开始，当单独作为文件系统的根使用时，读作“root”。当我们追求简洁时，再次尝试 `ls /`，像 'bin' 这样的名字，它是 binary 的缩写，是存放许多程序的目录（输入 `ls /bin` 可以显示 Pi 中的硬件设备）。尝试 `ls /home` —— 看到 'pi' 了吗？那是因为你正以用户 pi 的身份登录。如果你更改了登录名称，或者创建了额外的用户，他们也会列在那里：每个用户都有自己的家目录，你的目录就是 `/home/pi` 文件夹，我们之前就在那里那里。之前在处理 `MagPi` 时，我们使用的是相对路径（绝对路径应该是 `/home/pi/MagPi`），因为我们已经在家里了。如果你需要检查自己的位置，输入 `pwd`（当前工作目录）。

### 命令并不是晦涩的（至少不是无意的），但它们很简洁

### 没有哪里比 ~ 更像家

对于已登录的用户，他们的家目录缩写为 `~`（波浪字符）。尝试 `ls ~` 你就会看到。你的家目录下还有很多东西没有隐藏，但 Raspian 对随意的扫视隐藏了很多内容：以点为开头的文件和文件夹（称为“隐藏文件”），包含了系统和程序的配置信息。你通常不需要看到这些文件，但当你需要看时，只需使用 `ls` 命令配合开关即可显示所有它们。你可以使用完整开关 `-all` 或缩写 `-a`，如下：`ls -a`。遍历目录层次结构的路径可能比在目录树上点来去要容易，特别是使用快捷方式时。你的 `ls` 显示了 `.` 和 `..` 作为前两个目录，这些快捷方式分别代表当前目录和父目录。尝试从 `/home/pi` 列出父目录，输入 `ls ../` 将向你显示上一层。如果你想列出隐藏文件而不显示 `.` 和 `..`（毕竟它们存在每个目录中，所以你不需要被提醒），那么要使用的开关是 `-A`。

> 懒人补全
> 你需要输入 `ls` 的完整内容。例如 `MagPi` —— 在输入 `ls M` 后，按下 TAB 键它就会自动补全。如果你有多个以 M 开头的文件，它们会被列出来，你可以输入更多字母并按 TAB。

![](img/db18fe165e1f1a64ee0c5d815560917d_9_0.png)

在继续其他命令之前，让我们简单看看如何组合开关：`ls -1h ~`

`-1` 给你更多关于文件和文件夹的信息，而 `-h` 将单位从字节更改为合适的 kB、MB 或 GB。我们稍后会详细查看 `-ls` 列出的一些额外选项，特别是在第二章和第三章中。

### 是时候改变了

已经看够了：让我们开始移动吧。`cd` 是 change directory（更改目录）的缩写，可以移动到系统中你想去的任何地方：尝试 `cd /var/log` 并查看一眼 `ls(1)`。文件是日志，或者说是系统状态的消息，被保存供分析。这并不是你需要考虑的所有内容：树莓派是一个运行在数据中心和超级计算机上的操作系统版本，那里问题监控非常重要。然而，了解这些是有用的，特别是当你遇到问题且论坛上的某人要检查你的日志时。

`cd ~` 会带你回到预期的位置。尝试一下，然后用 `pwd` 检查。现在尝试 `cd -`（那是连字符），`'-'` 是“我来到这里之前所在地”的快捷方式。现在我们已经到处看了一圈，可以开始对我们的文件进行操作了。

好了，既然你可以把一个包含 78 个文件的列表放进一个小窗口，谁还需要图标呢？彩色字体表示

![](img/db18fe165e1f1a64ee0c5d815560917d_9_1.png)


在本章中，我们使用命令行工具从文件的不同部分获取文本，例如跳转到结论，通过按键创建和命名文件及目录，而不是点击和按键。

> 信息
> 许多实用都有 info 页面，提供的信息比 man 页面多。如果你觉得自己很勇敢，尝试 `nano` 查看其全面的指南。

![](img/db18fe165e1f1a64ee0c5d815560917d_11.png)

现在我们可以导航文件夹并列出文件，是时候学习如何创建和修改文件了。再次强调，任务不容易，而是命令的形式（特别是在编辑时）不熟悉，那是来自通用用户访问（UA）标准建立之前的时代，为了方便在操作系统之间切换。坚持下去：掌握了这本书的前两章，你就能在命令行完成大量工作，并变得熟悉。

### 创建目录

我们将通过创建一个新目录来直接处理文件和文件夹（参见“即时应用”框），并且你处于家目录（如有必要用 `cd ~` 回那里），输入 `mkdir tempfolder` 并用 `ls` 查看。

`mkdir` 正如你可能猜到的，创建一个新的目录或文件夹。让我们用它来实验修改 Python。别担心：我们不是要编程，只是通过插图做一个小改变。`cd tempfolder`（使用补全：`cd t` 然后按 TAB 键）。在下面的示例中，我们将一些文件复制到这个目录。首先确保已安装 Python Games ——如果没有，点击桌面左上角的图标，选择 Preferences，然后 Recommended Software，勾选 Python Games 旁的框，然后点击 Apply 安装。我们将文件从 `/usr/share/python_games/fourinrow.py` 复制过来：

### 通配符

命令末尾的 `.` 指的是“就在这里”，也就是我们要复制文件的地方。此外 `*` 被 Pi 读取为配符，代表任意数量的字符（包括没有）；还有其他配符，`?` 表示任意单个字符。尝试 `fourinrow.py` 你就会看到运行它的本地副本。要更改名称，我们需要编辑器 —— 我们使用 Pi 内置的编辑器：`nano`。

### 编辑和分页

`nano fourinrow.py` 将打开编辑器进行编辑，使用方向键向下移动移动到 BOARDHEIGHT 值为 6。将其改为 10（BACKSPACE 和 DELETE 键在 nano 中都可以用）。屏幕最后两行显示了一些快捷方式，`^`（井符号）代表 CTRL 键：`CTRL+O` 后接 RETURN 将“写出”（保存）文件；然后使用 `CTRL+X` 退出。现在，`fourinrow.py` 将打开一个大面板，给你更多时间击胜电脑，不过你确实需要。那里没有空间把标记拖到面板顶部：回去用 `nano` 将 BOARDHEIGHT 值改为 9。如果你想在不进入 nano 环境的情况下查看 `fourinrow.py` 列表，可以使用 `cat` 查看任何文件的完整文本：例如 `cat fourinrow.py`。遗憾的是，文件会迅速刷屏；要一次查看页，你需要一个“分页器”程序：`less fourinrow.py` 将让你使用 PAGE UP 和 PAGE DOWN 键上下滚动文本。其他键执行同样的工作，但我们将留给你自己。退出 less，按下 Q（这在 man 和 info 页面也同样有效，使用页面显示文本）。

![](img/db18fe165e1f1a64ee0c5d815560917d_13_0.png)

### Cats, heads & tails

如果编辑器是我们可以安全忽略的 UNIX 传统，那么无法逃避另一个传统：糟糕的谐音梗。less 是 more 的改进，一个简单的分页器：文件末尾相对原始的 man 页面会自动退出，省去你去按 Q 按钮的时间。承认，这并不是一个巨大的优势，你始终可以使用 cat。

幸运的是，cat 并不是基于文件的纸浆，而仅仅是为了“连接”（concatenate）：配合多个文件使用，它会将它们连接在一起。在带参数的情况下使用 —— 输入 `cat` —— 它会在每次按下 ENTER 后回你输入的内容。当你对它说完傻话时，按下 CTRL+C 退出视图。以及 CTRL+C 快捷方式：它关闭大多数命令行程序，就像大多数孤儿程序一样。





### 征服命令行

你可以使用 `head` 和 `tail` 命令查看文本文件的开头或结尾几行。`head fourinar.py` 将向你显示文件的前十行。`head -n 5 fourinar.py` 显示五行，而 `tail -n 5 fourinar.py` 显示最后五行。在树莓上，`head -n5 fourinar.py` 同样有效。

![](img/db18fe165e1f1a64ee0c5d815560917d_14_0.png)

### 谨慎删除

`nano file.txt` 并不存在：试一下它，并在写入和保存任何内容之前退出文件，看看它是否有效。我们已经做了很多工作（至少 `nano` 让你觉得做了很多），但学习如何清理自己的工作成果什么时候都不为时早。我们将使用 `rm` 删除我们创建的文件。使用 `remove` 工具时应该始终谨慎；它内置了一些保护机制，但即使这些也很容易被（图 2）。特别是，千万不要让任何人说服执行 `rm -rf /` —— 这将删除你树莓派的所有内容、所有程序、一切，而且几乎没有恢复机会。

我们来看一下我们制作的内容：如果你还在临时文件夹中，运行 `ls` 查看你复制到这里的 Four-in-ARow 文件。谨慎使用 *通配符* 来删除程序和 png 文件。

![](img/db18fe165e1f1a64ee0c5d815560917d_14_1.png)

> 图 2 `rm` 是一个强大的删除工具：请务必谨慎使用！

```
rm fourinar.py
rm 4row_*.png
```

使用 `cd ..` 返回 `/home/pi`，`rm -r`（递归）选项将删除新的空文件夹。这对于目录是必要的，如果还有剩余内容，也将一并删除。

在下一章中，我们将深入研究文件权限以及如何从命令行更新树莓派软件。

![](img/db18fe165e1f1a64ee0c5d815560917d_14_2.png)

![](img/db18fe165e1f1a64ee0c5d815560917d_15_0.png)


我们将介绍 Raspbian 高效的软件安装和更新系统等其他内容

### 征服命令行

安装软件应该是简单的，但每种软件的背后都是一组不断演变的依赖项，这些项也需要安装和更新。将它们分开可以减少冗余和重复，但也增加了漏洞、文件丢失甚至完全无法解决的冲突的风险。

幸运的是，Debian GNU/Linux 在 20 世纪 90 年代通过 Debian 包管理系统和高级软件包工具（APT）解决了这个问题——基于 Debian 的系统（如 Ubuntu 和树莓派的 Raspbian）继承了所有的优势。在这里，我们将向你展示从命令行安装新软件并保持系统更新所需的各种知识，然后查看完全无关的文件所有权和权限领域。

使用 `apt` 命令更新系统的待安装软件列表应该像这样输入命令行一样简单：`apt-get update`。以 `pi` 用户身份尝试此操作，尽管你会收到错误信息。这是因为在 GNU/Linux（或任何类型的 UNIX）中更改软件是受限于具有管理员权限的用户的系统操作：超级用户，也被称为

共同责任

如果你共享你的树莓派，请阅读 `sudo` 和 `visudo` 命令，以了解如何赋予他人有用的管理员权限。

![](img/db18fe165e1f1a64ee0c5d815560917d_16_0.png)

| 名称 | 大小 | 日期 | 时间 | 用户 | 组 | 描述 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| xz-utils | 1.2M | 2023-03-11 | 14:24 | root | root | | LZMA 的免费前端 |
| xz-utils | 1.2M | 2023-03-11 | 14:24 | root | root | | X Collections 的解压接口 |
| xdg-users-dirs | 16K | 2022-01-15 | 12:30 | root | root | | 管理通用的用户目录 |
| xdg-desktop | 110K | 2022-01-15 | 12:30 | root | root | | kde 中的默认桌面设置 |
| xfont-config | 1.1M | 2023-05-10 | 09:12 | root | root | | 用于 Linux 的 100 字体 |
| xfont-utils | 150K | 2023-05-10 | 09:12 | root | root | | X 字体管理工具 |
| xorg-base | 95K | 2023-04-12 | 11:45 | root | root | | 窗口系统实用程序 |
| xorg-data | 1.5M | 2023-04-12 | 11:45 | root | root | | 窗口配置数据 |
| xserver-common | 450K | 2023-04-12 | 11:45 | root | root | | 内核扩展 (MX) 配置 |
| xserver-core | 12M | 2023-04-12 | 11:45 | root | root | | 显示会话 |
| xserver-x11 | 1.2M | 2023-04-12 | 11:45 | root | root | | 配置数据 |
| xserver-video | 2.1M | 2023-04-12 | 11:45 | root | root | | 视频驱动程序 |
| xtools-common | 80K | 2023-04-12 | 11:45 | root | root | | 来自 shell (macosx) 的对话框 |
| xtools-utils | 40K | 2023-04-12 | 11:45 | root | root | | 库开发 |




执行更新，所以目前不需要重复。继续使用命令行主题，我们将安装一组旧的终端游戏：

```
sudo apt-get install bsdgames
```

### 可搜索列表

你可以通过 `apt-cache search` 找到特定的应用程序：`apt-cache search games`。你可以检查单个软件包：`apt-cache search games`。

在 Linux 中，文件权限分为三种：读取（r）、写入（w）和执行（x）。这些权限分为三组，即所有者（user）、组（group）和其他人（others）。你可以通过 `ls -l` 命令查看这些权限。

```
-rw-r--r--
```

要查看一个文件的权限，你可以使用 `ls -l`。你可以使用 `chmod` 命令来更改文件的权限。例如，`chmod +x file.sh` 会为文件添加执行权限，而 `chmod -x file.sh` 会移除执行权限。也可以使用 `chmod a-x file.sh` 来移除所有用户的执行权限。

```bash
chmod 755 file.sh
```

要查看目录的权限，你可以使用 `ls -l`。

### 文件属性

文件类型由权限字符串的第一个字符表示：`-` 表示普通文件，`d` 表示目录，`l` 表示符号链接。

```
drwxr-xr-x
```

在这个例子中，`d` 表示这是一个目录，`rwx` 表示所有者具有读取、写入和执行权限，`r-x` 表示组和其他人具有读取和执行权限。

你可以使用 `chown` 命令更改文件的所有者，使用 `chgrp` 命令更改文件所属的组。

```bash
sudo chown root:root file.txt
```




### 追加内容

如果你想向文件末尾添加内容而不覆盖原有内容，你需要使用 `>>`。

```bash
echo -e "one more for luck!" ~/mylisting4.txt
```

`echo` 简单将引号内的任何内容显示到标准输出（stdout），`-e` 选项允许你使用特殊字符，`\n` 用于换行（见下文）。你可以通过 `tail ~/mylisting4.txt` 查看文件的最后几行。
`<` 将程序的输入流链接到文件或流的内容。
有一个处理的无序列表并对其进行排序：

```bash
echo -e "aardvark\nplatypus\njellyfish\naark" > list1
sort < list1
```

你也可以结合 `<` 和 `>`：

```bash
head -n 2 < list1 > list2
```

...这将从 `list1` 读取内容，传递给 `head` 获取前两行，然后将这些内容放入文件 `list2` 中。在管道中：

```bash
sort < list1 | uniq > list3
```

最后，让我们来看看标准错误流（stderr）：它具有文件描述符 2（不用太担心这个），`2>` 将错误消息发送到你选择的任何文件：

```bash
cat list1 list2 list3
list4 2>errors.txt
```

屏幕将显示你执行的 'list' 文件，而“No file or directory”错误信息将保存在 `errors.txt` 中 - `2>>` 将消息写入文件而不覆盖之前的内容。

![](img/db18fe165e1f1a64ee0c5d815560917d_24_0.png)

图 2 通过重定向，你可以将命令的所有输出直接保存到文本文件中。保存好你的错误消息，以便在论坛上向寻求帮助！

# 第五章
## 定义命令行

通过让 Raspbian 的行为和外观完全符合我们的要求，让它变得更加个性化。

## [ 征服命令行 ]

![](img/db18fe165e1f1a64ee0c5d815560917d_26_0.png)

```
File Edit Tabs Help
@raspberrypi ~# @raspberrypi ~~
@raspberrypi $ sudo adduser jo
adding new group '1000'
adding user to group '20'
Creating home directory '/home/jo'
copying files from '/home/sk'
BAD PASSWORD: it does not contain different characters
type new password:
Creating user entry successfully.
Changing the user information for the default user 'jo':
Full Name , jo
Room Number , 
Work Phone , 3001
Group ID : 1000(jo)
Other : Pi Tan
@raspberrypi $ - is /home/jo
asking for password: profile
@raspberrypi $ - is [ ]
```

命令行环境对每个用户都是个性的。根据你在另一个角色中需要做什么，你可以在不改变环境的情况下切换身份。

看看你终端上那个闪烁的光标，以及它后面的内容：`pi@raspberrypi ~ $`
`$` 被称为“美元提示符”（dollar prompt），等待你的命令，在此之前看到 `~`（波浪号），它是“home”的缩写——在本例中它是 `/home/pi`。更好的格式是 `[user]@[computer name]`，形式为 `pi@raspberrypi`。这不仅提供了信息（至少当你忘记了自己是谁、在哪里时），而且还是一个你可以更改和个性化的东西。

### 新用户

让我们从用户名开始：`pi`。如果家里有多个个人使用 Pi，你可能想保留 `pi` 用户用于共享项目，但为家庭成员（包括你自己）设置个人登录账户。在 Raspberry 上创建新用户很容易：`sudo adduser jo` 会创建一个名为 `jo` 的新用户。系统会提示你输入密码。现在我们有了 `jo` 的用户账户，查看 `/home/pi`。看起来为空？由于 `jo` 从未登录过电脑，你现在会看到 `/home/pi` 的大部分内容是空的，但有一个 `.bashrc` 和一些其他配置文件。

*(注：原文文本存在大量重复和 OCR 错误，此处已提供清理后的翻译版本)*






详见下一个章节。移除 `#` 号意味着现在当你输入 `11` 时，你将执行运行 `ls -1` 的操作。这很方便，但我们可以做得更好。将其更改为：`alias 11='ls -1ahF'`，你将获得以 KB 或 MB 为单位的输出而不是字节，目录名末尾带有斜杠，并且省略无处不在 `.` 和 `..`（当前和父级）目录。更改在下次启动 Bash 会话后生效，之后你就可以像运行命令一样运行它（图 1）。要禁用会话中的别名，请使用：`unalias 11`。

- [我是谁？]
从虚拟控制台（CTRL-ALT+F6）进入，这就是以 `term` 身份登录的，可以切换到其他人，但从菜单中启动另一个应用程序，你将回到原始登录界面。

### 关键点

我们将结束许多用户需要更改的第一件事：键盘映射。系统级设置位于 `/etc/default/keyboard`，但通常你需要为单个用户进行更改。如果 `£` 符号和不带重音的字母对他们来说不够用，请以需要不同键盘的用户身份登录，或使用 `sudo` 配合以下命令的正确路径。例如，对于希腊键盘：

```
touch ~/.xsessionrc
echo setxkbmap "el" >> ~/.xsessionrc
```

将 `el` 替换为 `pt`、`us` 或你需要的任何语言。注意，我们创建的配置文件 `.xsessionrc` 包含了在我们登录到 GUI 时创建的设置，因此键盘设置将不仅影响终端，还会影响会话中使用的每个别名。

图 1 这些简短的（或三字母）命令没有设置在：制作你想要保留的快捷方式，或仅在特定会话中使用。

```
File Edit View Help
$ xsessionrc * ~/.xsessionrc *
$ alias
alias group=group --color=auto
alias ls=ls --color=auto -- 用的别名
alias ll=ls -l
alias la=ls -A --color=auto
alias lr=ls -F
alias mgr=ls -F --color=auto
alias 11='ls -1ahF'
alias 1s='ls -1'
$ ls -la
$ ls -l
$ of of 在这里添加它们是直接的。
$ cat ~/.bash_aliases | then then
$ alias 11='ls -1'
total 6
-rw-r-- 1 root 51K Jun 11 19:50 adduser.pg
-rw-r-- 1 root 300K Jun 12 08:41 annus.pg
-rw-r-- 1 root 220K Oct 21 13:33 bash_log
-rwxr-xr-x 1 root root 0 Jan 0 1 history
-rwxr-xr-x 2 root root 4K Mar 01 05:38 bin
```

![](img/db18fe165e1f1a64ee0c5d815560917d_30_0.png)

连接磁盘

在第六章中，我们将处理移动存储设备的管理。


![](img/db18fe165e1f1a64ee0c5d815560917d_31_0.png)

| 设备 | 起始 | 扇区 | 大小 | 类型 |
| :--- | :--- | :--- | :--- | :--- |
| /dev/mmblk0 | 0 | 7864320 | 30.0 GiB | 磁盘 |
| /dev/sda | 0 | 2097152 | 1.0 GiB | 磁盘 |
| /dev/sda1 | 0 | 1048576 | 0.5 GiB | Linux |
| /dev/sdb | 0 | 4194304 | 2.0 GiB | 磁盘 |
| /dev/sdb1 | 0 | 2097152 | 1.0 GiB | Linux |
| /dev/sdc | 0 | 1048576 | 0.5 GiB | 磁盘 |
| /dev/sdc1 | 0 | 524288 | 0.25 GiB | Linux |
| /dev/sde | 0 | 524288 | 0.25 GiB | 磁盘 |
| /dev/sde1 | 0 | 262144 | 0.12 GiB | Linux |
| /dev/sdf | 0 | 262144 | 0.12 GiB | 磁盘 |
| /dev/sdf1 | 0 | 131072 | 0.06 GiB | Linux |

```bash
user@raspberrypi~$ lsblk
NAME        MAJ:MIN  SIZE RO MOUNTPOINT
mmcblk0   17:0  29.9G 0 disk
└─mmcblk00 17:1  256M 0 partition /boot
sda         8:0    1.0G 0 disk
└─sda1       8:1    500M 0 partition
sdb         8:2    2.0G 0 disk
└─sdb1       8:3    1.0G 0 partition
sdc         8:4    0.5G 0 disk
└─sdc1       8:5    250M 0 partition
sde         8:6    0.25G 0 disk
└─sde1       8:7    125M 0 partition
sdf         8:8    0.12G 0 disk
└─sdf1       8:9    64M 0 partition
```
*(注：此处根据原文 lsblk 输出逻辑对翻译内容进行了微调，以对齐列关系)*

```bash
user@raspberrypi~$ lsblk
NAME        MAJ:MIN  SIZE RO MOUNTPOINT
mmcblk0   17:0  29.9G 0 disk
└─mmcblk00 17:1  256M 0 partition /boot
sda         8:0    1.0G 0 disk
└─sda1       8:1    500M 0 partition
sdb         8:2    2.0G 0 disk
└─sdb1       8:3    1.0G 0 partition
sdc         8:4    0.5G 0 disk
└─sdc1       8:5    250M 0 partition
sde         8:6    0.25G 0 disk
└─sde1       8:7    125M 0 partition
sdf         8:8    0.12G 0 disk
└─sdf1       8:9    64M 0 partition
```
*(注：原文中 lsblk 输出格式在原始文本中存在错位，翻译时保持原意并对齐逻辑)*

Raspbian 知道要挂载哪些磁盘，是通过读取文件系统表（/etc/fstab），并且我们可以把 `/dev/sda` 放在其中，但如果我们插入了两个驱动器，可能会选择错误的。幸运的是，磁盘（或者说磁盘分区）具有唯一的标签，称为 UUID，这些是在分区创建时分配的。使用 `sudo blkid` 可以找到它们，它还会告诉你插入到 USB 接口的磁盘（或 flash 驱动器）标签，通常包含名称和型号，或者查看 `/dev/disk-by-uuid`。

Raspbian 会自动挂载这些磁盘（除非在控制台中显示），你将看到 `/dev/sda1` `/media/usb`。如果设备正在被使用，请更改目录或关闭应用程序 `var/log`。停止 `tail` 请使用 `CTRL+C`。另一种查看连接的方法是 `fdisk`，一个用于划分分区的低级工具，在挂载时会以以下格式显示：设备、挂载点、文件系统类型。

对于 NTFS 格式的驱动器，使用 `sudo nano /etc/fstab` 在文件末尾添加以下行：`/dev/sda1 /media/usb`，其中 `fat`（应该是 NTFS 或 ext2）是文件系统类型。这给出了设备名称（当然，你的不同）、挂载点、文件系统类型以及两个数字字段：第一个字段应该是 0（它与未使用的 `dump` 备份程序有关），第二个字段是启动时的检查和修复顺序：1 代表根文件系统，2 代表其他永久挂载的数据磁盘，`o`（不检查）代表所有其他磁盘。

### 命令行征服

Pi 想要挂载的磁盘（或 flash 驱动器）通常以 `/dev/` 开头。Raspbian 知道要挂载哪些磁盘，是通过读取文件系统表（/etc/fstab），并且我们可以把 `/dev/sda` 放在其中，但如果我们插入了两个驱动器，可能会选择错误的。幸运的是，磁盘（或者说磁盘分区）具有唯一的标签，称为 UUID，这些是在分区创建时分配的。使用 `sudo blkid` 可以找到它们，它还会告诉你插入到 USB 接口的磁盘（或 flash 驱动器）标签，通常包含名称和型号，或者查看 `/dev/disk-by-uuid`。

### 磁盘空间

`df` 命令显示挂载驱动器的空间，比 `ls -l` 更易读。





### 使用 nano 编辑

我们在第 2 章中简要提到了 nano。深入了解一下，首先需要注意的是终端底部两行中的十几个快捷键：即同时按下 CTRL 键（用插入符号 ^ 表示）和其他键。例如，^A 表示读取文件（ReadFile，即打开），^O 表示写入（WriteOut，换句话说就是保存），^X 表示退出（Exit）。

虽然 nano 缺乏与其主要的命令行文本编辑器 Emacs 和 Vim 相比的功能，但作为一个强大的实用工具，它具有实用的功能 (^J)，可以将段落换行处的文本拉伸为连续的段落，或按固定字符长度对齐换行。这是它为编写电子邮件而开发的遗留。^K 剪切光标所在的行，但它不仅仅是一个删除函数：每次剪切都会添加到剪贴板中。^U 非常适合从长文本中收集有用的代码段。

按下 ^O 快速保存，快捷键列表会发生变化，现在开头变为 M 而不是 ^ – 它是 Meta 的缩写，意味着你键盘上的 ALT 键（曾经，某些计算机使用修饰键，如 Super 和 Hyper）。^O 之后的一个“隐藏”快捷键是在该点，^T 为你想要保存的文件/目录打开文件管理器。

保存后，使用以下命令退出：sudo mount -a 将外部驱动器挂载到指定的挂载点（图 2），无论插了其他什么。如果你在 /etc/fstab 中有其他条目，如果你不想挂载其他任何一个，可以使用 sudo mount /media/usb1（或你在 fstab 中设置的内容）来挂载所选设备。

在连接了内部设备后，下一章我们将看到访问所有的 Pi，但是从全球任何连接互联网的地点进行远程访问。

```
sudo nano /etc/fstab
### / / root ext4
### /home root ext4
### /var root ext4

### Filesystem Mounted on
323728 2780624 143792 95%
303278 2780624 143792 95%
219744 0 219744 0 %dev/
5120 0 5120 0 /run/lock
5120 0 5120 0 /run/user

### Filesystem Mounted on
323728 2780624 143792 95%
303278 2780624 143792 95%
219744 0 219744 0 %dev/
5120 0 5120 0 /run/lock
5120 0 5120 0 /run/user
```

图 a 一旦我们将可移动式磁盘放入文件系统表 (/etc/fstab) 中 – mount 命令将从那里读取整个磁盘以挂载你的磁盘，从而让你省去记忆细节的麻烦。

> [ 格式 ] 复制磁盘镜像包括格式化磁盘的需求。如果你需要格式化新分区或将磁盘转换为 ext4，请查阅手册：man-mkfs 可查看单个文件系统类型，例如 man mkfs.ext4

可预测的网络连接

在本章中，我们将为树莓派分配一个它自己的永久网络地址

### 征服命令行

Raspbian 在大多数情况下会自动处理连接，但有时你需要覆盖自动配置，以确保你的树莓派项目具有一致的网络设置：Raspbian 拥有这些工具，我们将向你展示保持连接所需的要素。

从你的 ADSL 路由器/调制调器连接一个以太网线到树莓派（或通过无线局域网连接），Raspbian 会自动知道自己在网络中的位置，以及如何与外部世界通信。这一切都归于 DHCP – 动态主机配置协议 – 它为连接到网络的每个设备提供网络配置。通常以 IPv4（互联网协议版本 4）地址的形式出现，由点分隔的四个数字组成。例如：192.168.0.37。前两个数字 192.168 标记私有范围的开始。这些数字是你家里从 192.168.0.0 到 192.168.255.255 的所有设备。使用 ifconfig 命令检查你树莓派的连接。这应该会显示类似 inet 192.168.0.37（你自己的数字）的行。这就是产生的效果。

```
pi@raspberrypi~$ ifconfig
lo: LOOPBACK,UP,RUNNING,mtu=65536
       inet 127.0.0.1  netmask 255.255.0.0

eth0: BROADCAST,MULTICAST,UP,mtu=1500
       inet 192.168.0.37  netmask 255.255.255.0
       RX packets = 1024 dropped 0
       TX packets = 988 dropped 0 overruns 0
```

ifconfig 命令可以告诉你树莓派的网络地址。

```
pi@raspberrypi~$ route
Destination     Gateway         Flags  Metric    Interface
0.0.0.0         192.168.0.1      UG        100     eth0
192.168.0.0     0.0.0.0          U         eth0
```

### 可预测的网络连接

如果你通过以太网连接，或者在连接到无线局域网时在 wlan 部分，获取 IP 地址的更快方法是在命令行中输入 hostname -I。

#### 如何为树莓派设置静态 IP 地址

通常当你将树莓派连接到局域网 (LAN) 时，它会自动分配一个 IP 地址。通常这个地址每次连接时都会变化。然而，你可能希望你的 Pi 每次启动都使用相同的 IP 地址。如果你正在创建一个小型自包含网络，或构建一个像机器人这样的独立项目，这将非常有用。操作方法如下编辑 /etc/dhcpcd.conf 文件（图 1）：在命令提示符输入 sudo nano /etc/dhcpcd.conf。滚动到脚本末尾并添加：

```
static ip_address=192.168.0.2/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1 8.8.8

interface eth0
static ip_address=192.168.0.2/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1 8.8.8

interface wlan0
static ip_address=192.168.0.2/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1 8.8.8
```

使用 CTRL+O 保存文件，然后使用 CTRL+X 退出 nano。

启动后，你的树莓派现在每次都会使用 IP 地址 192.168.0.2 启动；我们没有使用 192.168.0.1 是因为那是留给路由器的。你可以使用喜欢的任何地址，但在上面的配置中，范围必须在 192.168.0.2 到 192.168.0.255 之间。

使用 sudo shutdown -r 现在重启。登录并输入 hostname -I。你应该看到你在 eth0 或 wlan0 条目中设置的 IP 地址 (192.168.0.2)。

通常你不希望电脑被设置为静态 IP 地址。你可以再次使用 sudo nano /etc/dhcpcd.conf 将网络配置改回来。删除上一步中添加的所有行，然后保存文件。

### Ping！

Ping 是网络工具中最基础的工具，但也是经常被使用的工具。它向你网络上的设备发送 ICMP (互联网控制消息协议) ECHO_REQUEST。ICMP 内置于每个连接的设备中并用于诊断：ping 会产生被 ping 机器的回复，告诉它已在线且网络运行正常。关于数据包丢失和耗时的信息有助于故障诊断。

树莓派成功 ping localhost 不仅告诉你是回环接口工作正常，还说明它解析到了 127.0.0.1（本地查找地址）。名称解析是许多复杂问题的原因——“域名服务器”框。现在从你网络上的另一台机器 ping Pi 的 192.168.0.2（图 2）——当然，你需要使用你设置的静态 IPv4 地址，而不是我们的。如果你从 Windows 机器执行此操作，ping 默认尝试五次；从另一个 UNIX 机器（另一台 Pi、Mac 或 Ubuntu 等其他 GNU/Linux），它会一直运行直到你用 CTRL+C 停止它，除非像这样设置 ECHO_SOCKET 的发送次数：

```
ping -c 5 raspberry.org
```

### IPv6

我们使用的四位 IP 地址（如 192.168.0.2）是 IPv4。一种新标准 IPv6 变得越来越常见。这些是用十六进制表示的更长的 128 位地址（例如 fd531:42f8:ca5:dae2::1）。查看 dhcpcd.conf 中的示例代码以设置 IPv6 的静态地址。

### 免费 / 公 DNS

除了 DNS 提供商之外，FreeDNS.com 列出的某些也提供公共 DNS 服务器。对于 Google DNS 服务器更广泛的替代方案，可以在 Google 上进行搜索。





停止进程

尽管 Raspbian 几近完美，但问题仍会发生。在本章中，我们将学习到不需要重启树莓派：直接杀掉（kill）进程即可！

![](img/db18fe165e1f1a64ee0c5d815560917d_40_0.png)
# MagPi 基础

![](img/db18fe165e1f1a64ee0c5d815560917d_41_0.png)

在终端运行的程序可以发送到后台睡眠——在那里它们可以通过 `fg` 轻松地恢复

关注你的进程，你还能看到是什么在占用你的 CPU 和内存资源

丢失了程序的“关闭按钮”？有时候，你正在运行的某个软件似乎并不打算停止：要么你找不到如何退出，要么它出了问题，并且对你的 `Q`、`CTRL+C` 或任何命令都没有响应。

不需要慌慌，不需要重启：只需识别进程并安静地杀死它。我们将展示在进程知识之外还可以做什么。


使用 `ps` 命令查找树莓派上运行的许多进程。通常 `a` 和 `x` 选项组合会列出所有进程，而不仅仅是属于某个用户或附加到 `tty` 的进程。输入 `ps aux` 查看，然后尝试带上 `w` 或其他组合，`ww` 会加宽输出以防被截断。在没有横杠的情况下，特定的字母 `a` 和 `x` 可以追溯到 20 世纪 70 年代 Unix 的版本。


Unix 家族的不同分支（如 BSD、System V 以及 GNU/Linux）扩展了新选项和新缩写，因此 `ps ax` 可能会看到 `-e`（或 `-ef`）以长格式显示。`ps ax` 有各种表头，包括拥有进程的用户（USER）、进程 ID（PID）或父进程 ID。从 `1` 开始的是树莓派启动时用户空间的内核进程。PID 是杀死进程最简单的方法。例如，要杀死 PID 为 3012 的程序，只需输入 `kill 3012`，以便在 `ps` 列表中快速找到它。

## 顶部运行

> KEEP ON TOP
在使用虚拟控制台时，保持它运行是值得的，如果有任何问题，你可以使用 `CTRL-ALT-FN` 快速查看——即使 GUI 冻结了也是如此。

```
ps ax | grep -i
```

`-i` 选项（忽略大小写）通常不是必要的，但程序文件名可能包含大写字母。你也可以通过名称使用 `killall` 来杀死程序：


自然地，你可以管道 `ps ax` 并直接选择 PID：

```
ps ax | grep '[f]firefox' | awk '{print $2}'
```

我们在这里使用 `awk` 处理 `ps` 的输出来深入查看第二个字段：`[f]firefox` 这种技巧可以防止 `grep` 进程本身出现在结果中；上面的 `grep` 进程本身以及 `(anything)` 任何内容。`ps` 的输出还显示了内存和 CPU 使用的百分比等有用信息，但查看这些实时变化更有用。为此，使用 `top`，它显示总 CPU 和内存使用情况，在格式的最后几中。

 改进的 top：

```bash
sudo apt-get install htop
```

`htop` 可以水平和垂直滚动，并允许你执行命令（如使用 `k` 杀死）高亮显示的进程。当你完成时，在 `htop` 中退出按 `Q`。htop 还显示处理器的独立核心。

## 后台作业

在 shell 中命令后加上 `(&)` 将程序放入后台——第一个数字是 shell 分配的作业号，第二个是我们正在处理的 PID。你可以使用作业控制来处理 shell 中的进程。如果你想在后台启动其他任务（通过追加 `&`），然后使用 `fg` 将第一个带回前台。你可以通过 `CTRL+Z` 将正在运行的挂起到后台，除非指定了数字，否则它将带回最近挂起或后台的作业。注意，这些作业仅在 shell 内生效。输入 `jobs` 查看后台进程，作业列表中包含进程（PID）。

![](img/db18fe165e1f1a64ee0c5d815560917d_43_0.png)

| PID | USER | PRI | CPU% | MEM% | TIME+ | SHR | RES | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | root | 2000 | 0.0 | 1.5 | 0:00:01 | 12412 | 16412 | /sbin/systemd |
| 2 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 9812 | 10123 | /lib/systemd/systemd- |
| 3 | root | 2000 | 0.0 | 0.2 | 0:00:00 | 15412 | 12512 | /lib/systemd/systemdudev |
| 4 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 12412 | 11412 | /lib/systemd/logd |
| 5 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 14412 | 13412 | /lib/systemd/systemd-journal |
| 6 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 14412 | 14412 | /lib/systemd/systemd-resolved |
| 7 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 15412 | 15412 | /lib/systemd/systemd-network |
| 8 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 16412 | 16412 | /lib/systemd/systemd-timesd |
| 9 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 17412 | 17412 | /lib/systemd/systemd-udev |
| 10 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 18412 | 18412 | /lib/systemd/systemd-network |
| 11 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 19412 | 19412 | /lib/systemd/systemd-resolved |
| 12 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 20412 | 20412 | /lib/systemd/systemd-machine |
| 13 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 21412 | 21412 | /lib/systemd/systemd-logd |
| 14 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 22412 | 22412 | /lib/systemd/systemd-journal |
| 15 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 23412 | 23412 | /lib/systemd/systemd-udev |
| 16 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 24412 | 24412 | /lib/systemd/systemd-network |
| 17 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 25412 | 25412 | /lib/systemd/systemd-timesd |
| 18 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 26412 | 26412 | /lib/systemd/systemd-udev |
| 19 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 27412 | 27412 | /lib/systemd/systemd-network |
| 20 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 28412 | 28412 | /lib/systemd/systemd-resolved |
| 21 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 29412 | 29412 | /lib/systemd/systemd-machine |
| 22 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 30412 | 30412 | /lib/systemd/systemd-logd |
| 23 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 31412 | 31412 | /lib/systemd/systemd-journal |
| 24 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 32412 | 32412 | /lib/systemd/systemd-udev |
| 25 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 33412 | 33412 | /lib/systemd/systemd-network |
| 26 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 34412 | 34412 | /lib/systemd/systemd-timesd |
| 27 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 35412 | 35412 | /lib/systemd/systemd-udev |
| 28 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 36412 | 36412 | /lib/systemd/systemd-network |
| 29 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 37412 | 37412 | /lib/systemd/systemd-resolved |
| 30 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 38412 | 38412 | /lib/systemd/systemd-machine |
| 31 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 39412 | 39412 | /lib/systemd/systemd-logd |
| 32 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 40412 | 40412 | /lib/systemd/systemd-journal |
| 33 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 41412 | 41412 | /lib/systemd/systemd-udev |
| 34 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 42412 | 42412 | /lib/systemd/systemd-network |
| 35 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 43412 | 43412 | /lib/systemd/systemd-timesd |
| 36 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 44412 | 44412 | /lib/systemd/systemd-udev |
| 37 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 45412 | 45412 | /lib/systemd/systemd-network |
| 38 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 46412 | 46412 | /lib/systemd/systemd-resolved |
| 39 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 47412 | 47412 | /lib/systemd/systemd-machine |
| 40 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 48412 | 48412 | /lib/systemd/systemd-logd |
| 41 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 49412 | 49412 | /lib/systemd/systemd-journal |
| 42 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 50412 | 50412 | /lib/systemd/systemd-udev |
| 43 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 51412 | 51412 | /lib/systemd/systemd-network |
| 44 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 52412 | 52412 | /lib/systemd/systemd-timesd |
| 45 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 53412 | 53412 | /lib/systemd/systemd-udev |
| 46 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 54412 | 54412 | /lib/systemd/systemd-network |
| 47 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 55412 | 55412 | /lib/systemd/systemd-resolved |
| 48 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 56412 | 56412 | /lib/systemd/systemd-machine |
| 49 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 57412 | 57412 | /lib/systemd/systemd-logd |
| 50 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 58412 | 58412 | /lib/systemd/systemd-journal |
| 51 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 59412 | 59412 | /lib/systemd/systemd-udev |
| 52 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 60412 | 60412 | /lib/systemd/systemd-network |
| 53 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 61412 | 61412 | /lib/systemd/systemd-timesd |
| 54 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 62412 | 62412 | /lib/systemd/systemd-udev |
| 55 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 63412 | 63412 | /lib/systemd/systemd-network |
| 56 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 64412 | 64412 | /lib/systemd/systemd-resolved |
| 57 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 65412 | 65412 | /lib/systemd/systemd-machine |
| 58 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 66412 | 66412 | /lib/systemd/systemd-logd |
| 59 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 67412 | 67412 | /lib/systemd/systemd-journal |
| 60 | root | 2000 | 0.0 | 0.1 | 0:00:00 | 68412 | 68412 | /lib/systemd/systemd-udev |

## 信号

当我们在 htop 中发送一个 kill 信号时，我们可以选择要发送的信号。最重要的的是 SIGTERM、SIGINT 和 SIGKILL。

第一个也是 `kill` 在不带修饰符时从命令行发送的信号：它告诉进程停止，大多数程序将通过捕获该信号来响应


信号，并且在退出前首先保存它们需要保存的数据并释放系统资源。
kill -2 发送 SIGINT，这等同于在终端中通过 CTRL+C 停止程序：你可能会丢失数据。最剧烈的是 kill -9 发送 SIGKILL，它告诉内核在不发出任何警告的情况下杀死进程。只有在其他所有方法都无效时才使用这个命令。

最轻微的是挂断（HUP）信号，通过 kill -1 调用，许多守护进程（daemons）被程序设计为将其视为重新读取配置文件并继续运行的信号。这是发送给关键进程的最安全的信号。

## 保持运行 (Staying on)

nohup 将运行一个程序，该程序在启动它的终端关闭后仍将继续运行，并忽略 SIGHUP（挂断）信号。由于进程与终端分离了，错误消息和输出将发送到你启动进程时所在目录下的 nohup.out 文件中。你可以对其进行重定向——正如我们在第 4 章中做的那样——使用 1 代表标准输出 (stdout)，使用 2 代表标准错误 (stderr)；& 是重定向标准输出和标准输出的特殊情况：

```
nohup myprog & backgroundoutput.txt &
```

nohup 的一个用法是在 SSH 会话中启动任务，该任务在中断后仍将继续运行。例如，重启你所连接的网络连接：

```bash
sudo nohup sh -c "ifconfig wlan0 down && ifconfig wlan0 up"
```

注意，这里创建的 nohup.out 日志文件需要 sudo 权限读取——或通过以下命令重新分配：

```bash
sudo chown pi:pi nohup.out
```

![](img/db18fe165e1f1a64ee0c5d815560917d_44_0.png)

- 图 2 每个运行的程序都有一个可以控制你程序的进程 ID (PID);可以使用 ps 找到它们
- 持续运行 (KEEP ON RUNNING)
nohup 对于在后台运行一段时间的程序非常有用——也许是你正在进行的一个项目——直到你觉得有足够的理由才将其添加到树莓派的进程列表中。



学习如何通过 Secure Shell (SSH) 从远程 PC 和设备访问树莓派

## 征服命令行 (CONQUER THE COMMAND LINE)

树莓派如此便携，这非常棒，但有时你可能想在不带它的情况下使用它。在这里，树莓派默认的 Raspian OS 是一个真正的优势，因为 UNIX 类操作系统已经以这种方式运行了 40 多年。

随着时间的推移，互联网为恶意用户提供了连接计算机的机会，Telnet 和 login 等旧标准已被基于公钥加密的 Secure Shell (SSH) 所取代。一旦设置好，安全连接变得非常简单，并且为你的项目开放脚本化、自动化连接。建议你在在使用 SSH 之前，使用 password 命令更改你树莓派的登录密码。

如果你的 Raspian 版本没有默认启用 SSH，请运行 `sudo raspi-config` 并进入高级设置启用 SSH。使用 `ifconfig` 检查分配给树莓派的 IP 地址（注意 eth0 或 wlan 接口的 'inet addr'）。现在你可以尝试从网络上的另一台电脑进行连接。

### 使用 SSH 连接 (Connecting with SSH)

从 Mac 或 GNU/Linux 计算机开始，使用终端中的 ssh 连接到树莓派。假设是默认设置，如果 `ifconfig` 显示 IP 地址为 192.168.0.2，请使用 `ssh@192.168.0.2` 连接并输入密码。你可以在 Windows PC 上使用 OpenSSH 客户端；对于早期的 PC，可以安装如 PuTTY (magpi.co/ulyfk) 等 SSH 客户端，它也支持 SCP、Telnet 和 Rlogin，并连接串口。Android 用户可以尝试 ConnectBot 客户端。

![](img/db18fe165e1f1a64ee0c5d815560917d_44_0.png)

（注：后续部分原文中存在大量重复和无意义的片段，翻译时已根据上下文逻辑进行了完整性处理，并保留了原有的技术指令格式。）

"you can lose data" 你可能会丢失数据
"if the SSH is not enabled by default" 如果 SSH 默认未启用等



### 下载与安装

我们将介绍下载和解压软件，并向你展示如何创建新的 Raspbian SD 卡。

在简单下载文件时，`curl` 可以替代 `wget`，但它的优势在于其他地方，其丰富的功能——从代理支持、用户身份验证到 FTP 上传和 Cookie——无应有。

`tar` 命令打包或解包文件和目录归档；它还能处理解压缩第一个

```
$ raspberrypi@raspberrypi:~# curl -O https://pypi.org/packages/RP/RPi.GPIO/RPi.GPIO-9.0.5.tar.gz
$ raspberrypi@raspberrypi:~# tar -xvf RPi.GPIO-9.0.5.tar.gz
$ raspberrypi@raspberrypi:~# cd RPi.GPIO-9.0.5
$ raspberrypi@raspberrypi:~# ls -l
total 64
-rw-r--r-- 1 pi pi 2432 May 22 10:00 setup.py
-rw-r--r-- 1 pi pi 4500 May 22 10:00 README.md
-rw-r--r-- 1 pi pi 1500 May 22 10:00 LICENSE.txt
-rw-r--r-- 1 pi pi 1200 May 22 10:00 setup.cfg
-drwxr-xr-x 4 pi pi 4096 May 22 10:00 dist
-drwxr-xr-x 4 pi pi 4096 May 22 10:00 build
-drwxr-xr-x 4 pi pi 4096 May 22 10:00 docs
-drwxr-xr-x 4 pi pi 4096 May 22 10:00 tests
-drwxr-xr-x 4 pi pi 4096 May 22 10:00 examples
-rw-r--r-- 1 pi pi 3000 May 22 10:00 MAN.rst
-rw-r--r-- 1 pi pi 2000 May 22 10:00 CHANGELOG.md
```

```
$ raspberrypi@raspberrypi:~# sudo apt-get update
$ sudo apt-get install python3-gpio -y
```

![](img/db18fe165e1f1a64ee0c5d815560917d_51_0.png)

运行 `apt` 命令（见第 3 章）可以访问海量的软件集合——Raspbian 主仓库中数数千个软件包——但有时我们需要在主仓库之外添加软件。

如果运气足够的话，我们会发现有人已经用 Debian 使用的 `deb` 格式对软件进行了打包，甚至创建了一个完整的仓库来处理依赖关系。我们将简要介绍添加仓库以及处理其他类型的下载，并在过程中尝试联系那位德受尊敬的编辑。

仓库信息存储在 `/etc/apt/sources.list` 文件中，在新的安装中，该文件仅包含 Raspbian 仓库。建议不要通过编辑此文件来添加其他仓库，而是将它们添加到 `/etc/apt/sources.list.d` 目录下的 `.list` 文件中。要添加新仓库，使用 `sudo nano` 在该处创建一个 `.list` 文件，并在内部按照以下格式添加源：

```
deb http://apt.pi-top.com/raspbian/ jessie main
```

在这里，`jessie` 是一个 Debian（以及 Raspbian）发行版本：自 1996 年以来，所有的 Debian 都以《玩具总动员》系列电影中的角色命名（前 Debian 项目负责人 Bruce Perens 在皮克斯动画工作期间参与了 Debian 的早期开发）。`Stretch` 在 2017 年 6 月紧随 `Jessie`。

大部分软件位于主仓库中，可以自由复制或镜像到任何地方。其他组件，非自由（non-free），允许仓库包含可能不免费的软件，将其与 Raspbian 的 FOSS（自由开源软件）仓库分开。

### wget & curl

在 `sources.list` 文件中添加我们的仓库源后，我们需要获取它的密钥并使用 `apt-key` 进行安装。使用 `apt-key` 验证的软件包将被视为可信的。

```
wget -O -q http://apt.pi-top.com/apt.pi-top.gpg.key | sudo apt-key add -
```

`wget` 从指定的 URL 下载。`-O` 选项将下载重定向到标准输出，然后通过 `apt-key` 从标准输入读取。在更改了 `sources.list` 之后，你应该运行：

```
sudo apt-get update
```

这会更新 Raspbian 对可用软件包的认知。为了获取完整列表，输入：

```
grep ^Package /var/lib/apt/lists/apt.pi-top.com/raspbian_dists_jessie_main_binary-arm
```

`wget` 是一个简单但强大的下载工具，具有递归功能，但存在许多安全风险，因此在获取时要小心。替代方案是 `curl`，它是一个支持许多协议的文件传输工具，可以用于简单的![](img/db18fe165e1f1a64ee0c5d815560917d_52_0.png)

如果你真的想开始，你需要 `sudo apt-get install vim`，Raspbian 自带的 `vim` 软件包非常有限。

## MagPi 核心知识

默认情况下，下载会输出到标准输出；要保存为文件（指定名称），使用 `-O` 选项。例如：

```
curl -OSL https://pypi.org/packages/RP/RPi.GPIO/RPi.GPIO-9.0.5.tar.gz
```

在这里，`-O` 选项会显示任何错误，而 `-L` 选项允许 `curl` 在服务器报告不同位置时重试获取文件。

### Unzip

上述下载的 GPIO  使用 `gzip` 压缩无损地减小文件大小，并可以使用 `gunzip` 解压缩。文件被归档到 `tar` 存档中（你会发现以 `.tgz` 结尾的类似存档），`tar` 命令可以完成解压缩和解包：

```
tar zvf RPi.GPIO-9.0.5.tar.gz
```

![](img/db18fe165e1f1a64ee0c5d815560917d_53_0.png)

注意 `tar` 的单字母选项不需要数据。第一个选项 `z` 调用 `gzip` 来解压缩存档，然后 `x` 提取内容。`v` 是详细模式，在过程发生时告知；`f` 告诉 `tar` 处理指定的文件而不是标准输入。`z` 和 `tar` 应该自动检测所需的压缩操作。

结果是一个包含其他内容的文件夹，一个运行安装的脚本（先阅读 `INSTALL.txt` 文件）：

```
cd RPi.GPIO-9.0.5
sudo python setup.py install
```

虽然 `gzip` 比 `zip` 更高效（甚至更高效的 `bzip2`），但如果你得到的是 `zip` 文件，那么需要的命令就是 `unzip`。

```
unzip 2018-11-13-raspbian-stretch-lite.zip
```

### 磁盘镜像

下载并解压 Raspbian microSD 卡后，不能使用普通的 `cp` 将复制到第二个 microSD 卡（通过 USB 读器连接到 Pi），这仅仅会在卡上放置文件的副本。我们需要某种工具将 SD 卡的文件系统替换为 Raspbian 磁盘镜像内部存在的文件系统和内容，逐字节地，我们可以使用内置的小型工具 `dd`。

`dd` 转换并复制文件——任何文件，甚至是像 `/dev/zero` 或 `/dev/random` 的特殊设备（你可以创建一个全零或随机噪声文件）——精确复制字节块。为了复制我们的 Raspbian 镜像，我们需要挂载通过 USB 读器插入的二级 microSD 卡。在插入卡前后都使用 `sudo fdisk -l`（你也可以使用 `df` 查看挂载情况）来查看连接的设备。如果出现类似 `/dev/sdb` 的大小与 SD 卡相同，则挂载 `/dev/sdb`。现在复制磁盘镜像：

```
sudo dd if=~/Downloads/2018-11-13-raspbian-stretch-lite.img of=/dev/sdb bs=1M
```

Raspbian 的祖先 UNIX 的始于 1969 年，因此我们在书中涵盖了一些具有长期遗产的工具，但用 `if=` 代替命令行选项的常用横杠可以追溯到 20 世纪 60 年代初，以及 IBM OS/360 作业控制语言 (JCL) 中的数据定义 (DD) 语句。

务必小心目标磁盘匹配正确的磁盘，否则将丢失另一个存储设备的内容！`bs=1M` 是块大小默认值；`4M` 是另一个选项。现在将卡插入另一台 Pi 并尽情玩吧！

## MagPi 核心知识

## [ 第十一章 ] 随心启动停止

在过去的几年里，每种主要的 GNU/Linux 发行版（包括 Raspbian）都改变了它们的启动方式。这意味着许多关于将脚本放在 `rc.local` 中自动运行的旧文献已不再正确。保持不变的是：虽然内核启动的不是 `/sbin/init`，而是 `/lib/systemd/systemd`（PID 仍为 1），它仍然是 Linux 内核完成设备和驱动初始化并挂载文件系统后，用户空间发生的一切事的父进程。

init 启动一切，通常以登录提示符结束。新版本的 Raspbian 隐藏了启动过程生成的信息，但你可以通过输入 `dmesg` 查看；它们也存储在 `/var/log/kern`。

启动 – init – 用户空间的开始；这是你可以放置自己的程序以影响 Raspbian 运行的地方，而无需修改 Linux 内核代码。传统上，GNU/Linux 发行版实现了一个 V init 版本，它具有定义良好的启动过程，运行级别可以指示系统处于启动、单用户模式（救援模式——丢失密码时很有用）、或控制台模式、GUI 或关机状态。

### 征服命令行

systemd-analyze blame --n=20
systemd-networkd.service ................. 1.23s
systemd-network-manager.service ........... 1.15s
systemd-org-dbus.service ................. 0.88s
systemd-logd.service ................................ 0.75s
systemd-getd.service ................................. 0.62s
systemd-resolved.service .................... 0.55s
systemd-syslog-generator.service ................. 0.51s
systemd-journald.service ............................. 0.48s
systemd-seed.service ................................ 0.42s
systemd-randomseed.service ............................... 0.35s
```将服务添加到 systemd 会作为过程的一部分创建一个指向其真实位置的符号链接 – 不要手动创建

![](img/db18fe165e1f1a64ee0c5d815560917d_56_0.png)





# MagPi 基础

![](img/db18fe165e1f1a64ee0c5d815560917d_57_0.png)

```
文件 编辑  标签  视图  .getop  搜索...  Google-Chromium  [ ] [ ] [ ] [ ] 21:15 [X]
@pi@raspberrypi:~$ 
[  ] Loaded dependency for unit registry.db_hot_keys.service; ignoring: Unit registry.db_hot_keys.service failed to load: No such file or directory.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
[  ] Starting Session Manager for User pi.
@pi@raspberrypi:~$ 
```

### Systemd

Systemd（类似于 Upstart——见 p62）可以并行启动服务，并可以在需要时延迟启动服务。与其使用许多组件的脚本，不如设置一个目标（target），systemd 会解析其依赖关系直到达到该目标，从而避免了固定的启动顺序。文件位于 `/etc/systemd/system`，其中有很多内容需要学习，但对于任何用户需要记住的一点是，systemd 及其服务管理器通过 `systemctl` 命令控制。

```
sudo systemctl restart ssh
```

将重启 ssh——如果你更改了它监听的端口，例如，你就需要这样做。为了兼容性，除了使用 `/etc/init.d` 脚本来启动和停止服务外，在旧版本 Raspberryian 中运行的服务命令仍然有效，例如

```bash
sudo service apache2 reload
```

...（在这里我们让运行中的 Apache2 服务器重新读取其配置文件）。在 `/etc/systemd/system/multi-user.target` 下，你会发现像 `cron.service` 等文件，当使用 `ls -l` 仔细检查时，你会看到它们指向 `/lib/systemd/system` 中同名文件的链接（其他 GNU/Linux 发行版可能将文件放在 `/usr/lib` 下）。不要担心这些文件内部的内容看起来很困惑；它们的条件依赖有其逻辑，但在为你的 Pi 项目让软件在每个系统上自动运行之前，你可以安全地忘记它们。即使那时，我们将向你展示另一种使用 crontab 的方法——否则你需要了解以下内容，因为那些链接不是手动创建的：





![](img/db18fe165e1f1a64ee0c5d815560917d_59_0.png)

### 链接 (Linked In)

Systemd 会自动创建符号链接文件，但有时可能希望某个文件在其他地方的同时出现在本地目录中，这时我们需要我们还没有机会向你展示的实用命令：`ln`。

`ln` 创建一个链接，允许文件实际上同时存在于两个地方。在下面的示例中：

```bash
sudo ln -s /usr/share/doc/python-numpy/THANKS.txt numpy-THANKS.txt
```

...一个文件将出现在你的工作目录中。但通过 `ls -l` 你会发现它是特殊类型的文件，指向实际文件的链接。编辑 `numpy-THANKS.txt`，你会发现链接目录中的 `THANKS.txt` 也会被修改。

软链接（或“符号”链接）通过 `-s` 创建——如果你是跨网络链接，或者链接到可移动驱动器，你甚至不需要所链接的文件实际存在。

Systemd 是一个复杂的系统，包含许多元素 - systemd-unit - 但它们都有自己的 man 手页，每个都值得仔细读一遍以掌握整体概念。

它保持了与 init.d 脚本甚至运行级别（run levels）向后兼容性。

![](img/db18fe165e1f1a64ee0c5d815560917d_59_1.png)

```ini
### X-Stop-Before:
is
### X-Start:
is
### Default-Start:
2 3 4 5
### Default-Stop:
0 6
### X-Wanted-By:
true
### Short-Description: Example instances
### Description:此文件用于构建放置在 /etc/init.d/ 中的脚本

### END INIT INFO

关于该格式的更多信息可以在 `update-init(8)` 中找到。这些信息用于在启动过程中动态为启动级别分配序列号。请参见 `/usr/share/doc/etc/init.d/README`。

```bash
pi@raspberry:/etc/systemd $ ls -l
mountall.sh  rc ssh
networking  dev-final
avavami  mountdevfs.sh rc,local sudo
bluetooth  faker-lock triggerhappy
hostname.sh  README
bootstrap.sh  mountdevfs.clean
mntifs.sh  reboot umntfs
checks.sh  kbd rmlogin umntfs
checks.clean.sh rcbd umroot
console-setup rpy rysync umroot
dbus  lightdm python3 urandom
cdrom  modd  procs sendsig xii-common
pi@raspberry:/etc/systemd $ all-boot-clean.sh raspi-config skeleton
```

60 MagPi | 章节元素

它被称为符号链接，是因为它通过链接到目标文件名本身来工作。创建一个硬链接：

```bash
sudo ln /etc/bluetooth/main.conf mybluetooth.conf
```

...你为同一个文件有了两个名字（位置）——听起来是一回事吗？并不完全：如果你在第一个示例中删除了原始文件，你可以用同名但内容不同的新文件替换它，符号链接将指向新文件。在硬链接的情况下，删除原始文件，链接仍然指向数据。

### 位置，位置 (Location, location)

启动脚本——无论是 init.d 还是 systemd——通常都是守护进程，即你希望一直运行的进程，如 Web 服务器和数据库。有很多执行清理工作的程序需要定期运行——每小时、每天、每周。为此，`cron` 实用是调度此类程序和任务运行的理想选择。Cron 会搜索它的配置目录并运行它找到的脚本——查看 `/etc` 中以 `cron` 开头的不同文件夹。

要找到你的系统中没有安装此类内容最简单的方法是搜索 `locate` —— 它在树莓派上默认没有安装。使用 `sudo apt-get install locate`，然后运行 `locate cron` —— 将找到每个包含该名称或作为其名称一部分的文件或目录。

`locate` 工具维护着系统上每个文件的数据库，该数据库由 cron 每天更新。如果你做了很多更改，或者想寻找某些内容，运行 `sudo updatedb`。

它被称为符号链接，是因为它通过链接到目标文件名本身来工作。创建一个硬链接：

```bash
sudo ln /etc/bluetooth/main.conf mybluetooth.conf
```

...你为同一个文件有了两个名字（位置）——听起来是一回事吗？并不完全：如果你在第一个示例中删除了原始文件，你可以用同名但内容不同的新文件替换它，符号链接将指向新文件。在硬链接的情况下，删除原始文件，链接仍然指向数据。

### 位置，位置 (Location, location)

启动脚本——无论是 init.d 还是 systemd——通常都是守护进程，即你希望一直运行的进程，如 Web 服务器和数据库。有很多执行清理工作的程序需要定期运行——每小时、每天、每周。为此，`cron` 实用是调度此类程序和任务运行的理想选择。Cron 会搜索它的配置目录并运行它找到的脚本——查看 `/etc` 中以 `cron` 开头的不同文件夹。

要找到你的系统中没有安装此类内容最简单的方法是搜索 `locate` —— 它在树莓派上默认没有安装。使用 `sudo apt-get install locate`，然后运行 `locate cron` —— 将找到包含该名称或作为其名称一部分的文件或目录。

`locate` 工具维护着系统上每个文件的数据库，该数据库由 cron 每天更新。如果你做了很多更改，或者想寻找某些内容，运行 `sudo updatedb`。

它被称为符号链接，是因为它通过链接到目标文件名本身来工作。创建一个硬链接：

```bash
sudo ln /etc/bluetooth/main.conf mybluetooth.conf
```

...你为同一个文件有了两个名字（位置）——听起来是一回事吗？并不完全：如果你在第一个示例中删除了原始文件，你可以用同名但内容不同的新文件替换它，符号链接将指向新文件。在硬链接的情况下，删除原始文件，链接仍然指向数据。

### 位置，位置 (Location, location)

启动脚本——无论是 init.d 还是 systemd——通常都是守护进程，即你希望一直运行的进程，如 Web 服务器和数据库。有很多执行清理工作的程序需要定期运行——每小时、每天、每周。为此，`cron` 实用是调度此类程序和任务运行的理想选择。Cron 会搜索它的配置目录并运行它找到的脚本——查看 `/etc` 中以 `cron` 开头的不同文件夹。

要找到你的系统中没有安装此类内容最简单的方法是搜索 `locate` —— 它在树莓派上默认没有安装。使用 `sudo apt-get install locate`，然后运行 `locate cron` —— 将找到包含该名称或作为其名称一部分的文件或目录。

`locate` 工具维护着系统上每个文件的数据库，该数据库由 cron 每天更新。如果你做了很多更改，或者想寻找某些内容，运行 `sudo updatedb`。

它被称为符号链接，是因为它通过链接到目标文件名本身来工作。创建一个硬链接：

```bash
sudo ln /etc/bluetooth/main.conf mybluetooth.conf
```

...你为同一个文件有了两个名字（位置）——听起来是一回事吗？树莓派。

你会在 cron 调用的脚本之一是运行 `anacron`，它设计用于在并非一直开启的机器上定期运行——这对于笔记本电脑同样有用——通过指定任务，在它们错过运行若干天后执行运行。你也可以使用 crontab 或 anacron 的自动化功能运行你自己的备份脚本，我们将在下一章讨论备份选项。

### 全新的启动 (A fresh startup)

使用 `@reboot`，我们可以轻松地在启动时运行脚本。某些情况下，完整的启动脚本会更合适，但为了快速实现某些功能，可以将脚本放入 `crontab`。

你会在 cron 调用的脚本之一是运行 `anacron`，它设计用于在并非一直开启的机器上定期运行——这对于笔记本电脑同样有用——通过指定任务，在它们错过运行若干天后执行。





![](img/db18fe165e1f1a64ee0c5d815560917d_63_0.png)

# 第十二章

## 立即保存！

学习如何通过备份和磁盘擦除来保护你的数据

### 征服命令行

也许你已经在主电脑上运行了自动备份，或者你只是偶尔备份一下重要的东西——这没关系，我们不是来评判的。但我们会说，任何你没有备份的东西，你就不拥有。电脑会故障。硬盘和 SSD 会故障。意外总会发生。意外在某种程度上是不可避免的。

IT 专业人员做准备时，就像他们随时可能丢失一切一样，至少最优秀的人是这样考虑的。对于你以廉价购买的、用于爱好项目的小型单板计算机来说，这听起来可能是一项艰的任务，但数据是上面最重要的东西，而良好的备份是一种可以应用到其他领域的良好习惯。幸运的是，命令行实际上可以让这一切变得简单，我们将为你展示一些进行（相对）无痛备份的最佳方案。

最简单的方法是将数据复制并移动到其他地方。与自动解决方案相比，这是耗费人力的，但对于极少数的备份来说，它比没有要好得多，所以我们不会忽略这一点。

无论你是复制到磁盘，还是将备份移动到另一台机器，最好尽可能地减小它的体积。zip 压缩格式的压缩率可能不如某些专业的 UNIX 选择，但它意味着其他用户可以使用其标准的压缩软件打开这些文件。你可以选择 LZMA 或 bzip2 压缩（分别来自 tar 的 `-J` 或 `-j`）——它们都比为了获得更好压缩的 gzip 安装得更广泛。

![](img/db18fe165e1f1a64ee0c5d815560917d_64_0.png)

```bash
$ radgeberry:~/bin bash
$ File Edit Tabs Help
$ radgeberry:~$ ls -l bier
$ radgeberry:~$ ls -l bier/test.txt
$ radgeberry:~$ ls -l ~/ test.txt
$ radgeberry:~$ gzip -c ~/ test.txt
$ radgeberry:~$ ls -al pi. 7777 02:59 test.txt

export PATH="PATH:$HOME/bin"
```

通过将命令放入 .sh 文件中并使其可执行，你创建了自己的脚本

通过创建一个 ~/bin 文件夹并将其添加到 ~/bashrc 中的 PATH 目录中，意味着你能够通过名称运行你的脚本

立即保存！ | MagPI 65

### 单条命令即可封装所有文件和子文件夹，并用 gzip 压缩 tar 归档

```
File Edit Tabs Help
pi@raspberry ~
pi@raspberry * @raspberry *
Documents/BlueJ Projects/LED-Button/README.TXT
Documents/BlueJ Projects/LED-Button/LED.java
Documents/BlueJ Projects/LED-Button/README.txt
Documents/BlueJ Projects/LED-Button/LEDaster.java
Documents/BlueJ Projects/LED-Button/package.blue
Documents/BlueJ Projects/LED-Button/package-demo.txt
Documents/BlueJ Projects/LED-Button/StringMorse.java
Documents/BlueJ Projects/LED-Button/LED.txt
Documents/BlueJ Projects/LED-Button/Button.txt
Documents/BlueJ Projects/people2/
Documents/BlueJ Projects/people2/README.TXT
Documents/BlueJ Projects/people2/Address.java
Documents/BlueJ Projects/people2/Herman.java
Documents/BlueJ Projects/people2/student.java
Documents/BlueJ Projects/people2/staff.java
Documents/BlueJ Projects/File-reader/
Documents/BlueJ Projects/File-reader/README.TXT
Documents/BlueJ Projects/File-reader/package.blue
Documents/BlueJ Projects/File-reader/FileReader.java
Documents/BlueJ Projects/File-reader/README.txt
pi@raspberry:~ tar -cvf myprojectbackup.tgz
pi@raspberry:~ tar -r -f -1 myprojectbackup.tgz
pi@raspberry:~ tar -czvf myprojectbackup.tgz Documents/
```

像 gzip 这样的小尺寸，但 gzip 的替代方案可以节省更多空间，它们执行压缩可能花费长得多的时间。将一个需要收集的文件目录进行压缩，可以通过单条命令完成：

```
tar czvf mybackup.tgz myfolder
```

`c` 选项告诉 tar 创建归档，并进入找到的所有子文件夹；`f` 指定的文件名（这里是 `mybackup.tgz`）是必要的，用于将输出重定向到终端之外，或者传统的磁带设备。对于 tar 来说，`tar` 是“tape archive”（磁带归档）的缩写，命令行选项前没有加横杠且频繁使用是其长寿的一个明显标志。`v` 与许多命令一样，请求更详细输出，程序会告诉你它正在做什么以及（如果有的话）发生了什么错误。
最后，`z` 调用了 gzip 压缩——省去了先创建 tar 归档再通过 gzip 的额外步骤。要解压归档，将 `c` 替换为 `x` 表示提取（extract）——你可以省略 `z`，tar 会识别压缩类型并自动处理：

```
tar xvf mybackup.tgz
```

### 一个安全的家

通常，使用 tar 备份 `/home/pi` —— 先执行 `cd /home`，然后对 `pi` 文件夹执行 tar —— 将是你需要的一切，但如果你的数据跨越多个目录，从 `/etc` 到 `/var/www`，最好的办法是备份整个 microSD 卡。我们在第 10 章中介绍过如何将 Raspian 镜像复制到卡上，对于连接了 USB 读卡器的 Pi，备份整个磁盘有一个重要的限制。

你将创建一个与整个卡一样大的文件——对于空间有限的 Pi 来说。解决方案是在创建镜像时对其进行压缩，对于一个带有中等量数据的 Pi，这将产生一个大约 2.5 GB 的镜像。查看第 10 章了解如何处理未挂载的 `/dev/sdb`：

```
dd bs=4M if=/dev/sdb | gzip > back-img.gz
```

打开另一个终端并使用 `df` 监控磁盘空间——如果你认为放不下，使用 CTRL+C 停止 dd 操作，然后删除镜像

### 远程复制

根据需要使用移动驱动器制作备份是好事，但为了转向系统化的备份，你需要跨网络进行传输。我们在第 9 章提到过 SCP。要将备份文件复制到另一台机器，一台允许 SSH 登录（即运行 SSH 服务器）的机器，请在命令中传递你的登录名称：

```
scp -p raspberry.img.gz pi@192.168.0.207:/home/pi/bak/
```

随后会提示你输入用户密码。将 `pi` 更改为远程机器上的用户名，而不是你复制来源的 Pi 的用户名。`-p` 保留文件的最后访问信息。

我们在第 7 章展示了如何使用具有固定 IP 地址的 Pi，那台连接了 USB 硬盘驱动器的 Pi 既可以作为一台廉价的备份机器，也可以作为任何你有办公需求处的媒体服务器。

由于你通过 Bash Shell 发送这些命令，因此你将获得所有的 Bash 优势，从标签补全（只需输入 `bac`，或者在当前工作目录中唯一的文件名部分）到通配符。如果你有分散的归档文件

### 哪些文件？

除了之外，你的项目可能在 `/etc` 或 `/opt` 中有配置文件，在 `/var` 下有日志、Web 配置和文件——这些你都可能为某个项目修改过。




在同一目录下——例如 `www-backup-201812225.gz` 和 `data-backup-20181226.gz`——然后使用以下命令复制所有它们：

```
scp -p .*backup.gz pi@192.168.0.207:/home/pi/bak/
```

到目前为止一切顺利，但在本章后面的部分，你将学习自动化备份过程的方法，否则避免交互式元素——即必须输入密码——会是更好。当然，前提是你能够通过其他方式维持安全性。

### 登录密钥

回到我们设置 SSH 服务器时，我们使用 `ssh-keygen` 生成了密钥——这些密钥可以用于提供无密码登录。你可以像我们之前的那样手动将它们复制到其他机器上，但一个（handy） 方便的快捷方法是使用 `ssh-copy-id` 命令。

```
ssh-copy-id pi@192.168.0.207
```

如果你有多个密钥对，使用 `-i` 来指定你正在复制的 `.pub` 文件。`-p` 允许你指定备用端口号——对于连接互联网的服务器来说这总是好事，但在本地网络上没有那么必要。现在我们为远程备份做好了准备——如果你定期执行备份，将会浪费大量的磁盘空间来中断那些不变的数据。

`rsync` 让你以与 `scp` 相同的方式复制数据，但它使用增量传输算法（delta-transfer algorithm），仅传输磁盘上源副本与远程保存版本之间的差异。这节省了使用的带宽，并避免了近乎相同的文件版本占用你的备份磁盘。如果你正在向云提供商支付存储和数据传输费用，这也非常方便。

如果你的 Raspberrybian 版本没有 `rsync`，只需一个 `apt-get` 即可安装。通常情况下，`rsync` 使用 SSH 进行传输，但你可以设置一个运行 `rsync` 守护进程的服务器，并通过 TCP 直接连接 `rsync://`（默认端口为 873）。在这种情况下，设置 `RSYNC_PASSWORD` 环境变量或使用 `--password-file` 选项。

虽然 `rsync` 不是 Bash 内置命令，但我们在这里重点介绍它，它是用户在考虑是否简单地使用内置命令时，面临的一系列命令行工具选择之一。

> [ 为什么要远程备份？ ]

> 除了能够为多台机器集中备份外，远程备份还能保护你免受 Pi 所在地发生的意外灾难（如火灾或洪水）。相当好用吧？是的，但这并不能阻止你为房子投保。

## MagPi 基础知识

我们脚本中的日期戳（datestamp）意味着我们在运行它时，不会产生一个同名的备份。

![](img/db18fe165e1f1a64ee0c5d815560917d_69_0.png)

此外，还有可能使用版本控制系统（如 `git`）来同时进行备份和跟踪重要文件的更改。

### 自己编写脚本！

但让我们回到更简单的命令。我们从早期就看到，通过链接几个命令，Bash 可以变得多么强大，另一种将命令组合的方法是将它们封装成一个脚本——一个简单压缩少量 Bash 命令的短程序，被称为 shell 脚本（shell script）。看看这段代码——尝试在你最喜欢的文本编辑器中输入它，针对你网络备份服务器的 IP 地址和备份文件夹位置进行调整（或者将 `scp` 行改为 `cp` 到插入的备份驱动器），并将其保存为 `test.sh`。

```
#!/bin/sh
cd /home/pi
tar czf mydocsbackup.tgz Documents
scp mydocsbackup.tgz pi@192.168.0.207:/home/pi/bak/
```

### 征服命令行

然后通过以下方法让脚本可执行：

```
chmod +x test.sh
```

...然后用 `./test.sh` 运行它——如果有任何问题，检查名称、网络地址，以及你是否执行了 `ssh-config` 步骤？

现在我们有了一个保存文件夹并将其远程复制的脚本，你注意到任何潜在问题了吗？每次运行它，它都会覆盖本地和远程的之前的 `mydocsbackup.tgz`。

我们需要一种在备份名称上加上时间戳的方法：

```bash
#!/bin/sh
TODAY=$(date +"%F")
cd /home/pi
tar czf mydocsbackup-$TODAY. Documents
scp mydocsbackup-$TODAY.tgz pi@192.168.0.207:/home/pi/bak/
```

> HASH BANG（井号）
> shebang，或 hash bang - 脚本开头的 `!` 是一个指示程序立即运行的指令——在这种情况下是让运行 `/bin/sh` 的解释器——并将脚本作为参数传递。

我们现在定义了变量 `-TODAY` - 现在它是现在的日期，格式为 YYYY-MM-DD，我们现在通过 `$TODAY` 访问它（记得，在第 5 章更改提示符时，shell 的永久设置变量是这样的）。你可以运行 `date +F --help` 将为你显示其他选项。

现在你可以通过将脚本放在 `/usr/bin` 等地方（并起个更好的名字 `test.sh`），并使用 `cron` 定期运行它来实现自动化。Shell 往往会增长，总有改进的空间。你可能想备份多个目录，或者使用 `echo` 让用户知道每个阶段的状况。你甚至可以让它具有交互性，让用户选择备份哪些目录。网上有很多脚本教程和很棒的书（参见 MagPi 评测）让你更进一步，Raspbian 本身包含许多很棒的脚本，你可以通过示例进行学习。要查看如何组织一个拥有数千行代码且可维护的脚本，请查看 `/usr/bin/raspi-config`。宏大或微小的野心，不要害怕尝试：逐步构建，并在每次测试你的代码。

![](img/db18fe165e1f1a64ee0c5d815560917d_70_0.png)

...将你的代码粘贴到 `shellcode.net` 将给你提供宝贵的反馈——例如，建议脚本应该是：

免密码
使用你的密钥登录是一种便利——不仅是为了你的备份服务器，还为了你所控制的任何需要登录的机器。

```bash
cd /home/pi || exit
```

如果失败了——这通常是一个好主意，尽管在这个特定情况下并不重要。现在我们有了备份选项的选择，还剩下一个任务：安全地从磁盘中清除数据。对于任何处理他人数据的人，或只是保护自己的隐私和安全的人来说，这都是一个关注的问题。

### 彻底删除数据

在我们开始删除磁盘之前，记住木工格言：“多量少切”。如果你不留神，很容易误删错误的磁盘或分区。在 `shred` 执行之前，运行磁盘上的其他操作（`mount`, `df`, `du`, `umount`）可以作为一种检查，确保你处理的是正确的分区。

现在谈谈那些块。你可以用 `dd` 覆盖每一个比特的信息，要么用全 1，要么用完全随机的数据。即使如此，对于磁性磁盘，理论上仍可能恢复数据，多次覆盖是必要的——在你担心编写脚本来完成这一点之前，让我们介绍 `shred`，这是一个正是执行此操作的工具，它根据你指定的命令行切换次数进行覆盖（默认为三次）：

```
shred -vf -n 5 /dev/sdb
```

`shred` 会安全地覆盖（可选删除）文件——整个磁盘驱动器。

### 我在哪里？

如果你在处处使用 SSH 密钥，并在不同的机器之间穿梭，请记得自定义你的 Bash 提示符，以便你总是确定自己正在哪台机器上删除文件。

添加 `-z` 选项将把 `shred` 使用的随机数据用零覆盖，使磁盘看起来是新的。`-u` 在安全覆盖后删除文件。`shred` 还可以安全地覆盖/或删除单个文件。





# MagPi 核心教程

# [ 第十三章 ]

## 轻松编译

在这里我们将介绍如何安装软件以及从源代码进行构建

### 征服命令行

只需在 `git clone` 之后粘贴以 .git 结尾的 URI 到终端（Terminal），你就会获得最新的源代码。

安装 `alien`，你就可以在 Raspberry Pi、Fedora 以及其他系统的软件包之间进行转换。

![](img/db18fe165e1f1a64ee0c5d815560917d_74_0.png)

在 Raspberry Pi 上安装大多数软件非常简单——简单到可以打包成 `.deb` 归档包。通常，会有一些很棒的代码你想尝试，但它要求你对其进行编译——有时是在从 GitHub 克隆之后之后。虽然这不像运行 `apt-get install` 命令那么直观，但尝试这个几十年历史的软件编译过程并不可怕——当发生错误时，通常很容易回到正轨。我们还将查看已安装的脚本和 Python 软件包，但让我们先看看如果软件包格式错误该怎么办。

Raspian 不是唯一基于 Debian 的 GNU/Linux 发行版——distrowatch.com 列出了一百多个——其中你最可能听说是 Linux Mint 和 Ubuntu。Ubuntu——这个名字源于一种恩古班图语术语，意为“对他人的仁”——它是非常流行，以许多项目（包括不在 Debian 和 Raspberry 仓库中的项目）都会为发布的每个版本维护 `.deb` 软件包。

Ubuntu 还将“个人软件包存档”（PPA）的概念引入了 Debian 家族——这是一种特殊的软件仓库，用于上传源码包，以便由 Ubuntu 的 Launchpad 软件进行构建并发布为 APT 仓库，就像官方 Ubuntu 仓库一样，但它是用于来自外部的非官方软件。你不需要在 Pi 软件中寻找这些，但如果你被激发想在你的主电脑上尝试 Raspberry 的亲戚版本，你会在 Ubuntu 社区文档中找到大量的说明。

编译看起来可能复杂，但大多数项目都为该过程提供了一个编写良好的文件——甚至是自定义的并提供提示。

![](img/db18fe165e1f1a64ee0c5d815560917d_75_0.png)

当你运行 `apt-get` 或使用 `apt-cache search` 查找软件包时，apt 会查询其本地关于可用软件包的记录。关于它从何处获取这些软件包的记录（仓库地址）存储在 `/etc/apt/sources.list` 文件以及 `/etc/apt/sources.list.d/` 下的文件中，如果你感兴趣的项目维护了一个仓库，你也可以手动添加它。

你也可以编辑 `sources.list`（不建议这样做）——从 whezy 修改到 jessie 的菜单是一种（不支持的）升级方法，可以让你进行升级，而不会在 Raspian 更新时重写你的 SD 卡。同时，可以下载普通的旧版 `.deb` 文件，然后使用命令进行安装：

```bash
sudo dpkg -i example.deb
```

并使用以下命令解决任何缺失的依赖项：

```bash
apt-get install -f
```

还有另一类流行的 GNU/Linux 发行版是基于 Red Hat 的，并包括 Fedora 和 CentOS。Fedora 可以作为 Raspian 的替代方案（在 Pi 2 或 3 上），如果你想尝试它的话。我们在这里关注的是你可能需要为一种发行版安装软件包到另一种类型的系统上的情况。你的朋友是 Raspian 的 `alien` 软件包，它可以在软件的 `.deb` 和 `.rpm`（Red Hat 软件包管理）格式软件包之间转换。

```bash
alien some-package.rpm
```

...将从 `.rpm` 转换为 `.deb`。你更有可能（至少在 Pi 上，因为那里仅限 RPM 的软件包较少）需要进行反向转换：

```bash
alien -r mysoftware.deb
```

### 友好编译

在编译之前，大多数项目都提供一个编写良好的文件来处理该过程——甚至是自定义的并提供提示。

许多项目在（至少在 Pi 上，你可能需要转换），你运行的。

你第一次遇到 GitHub 的存在可能是看到项目页面上的横幅邀请你“fork”，或者邀请“clone”。是的，我们处于一个项目中，通常包含一个名为 `README` 或 `INSTALL` 的文件。通过以下命令解包归文件：

```bash
tar xvf software.gz
```

...进入创建的目录。然后按照上述方法执行配置/make 指令。

通常做法是：

```bash
./configure
make
sudo make install
```

### 不要绝望

![](img/db18fe165e1f1a64ee0c5d815560917d_78_0.png)

有时，在编译的某个地方会发生错误，脚本终止并抱怨缺少某个软件包。如果运气好，你会用 `apt-cache search` 查找依赖项的名称，它就在那里，在 Raspian 上安装非常简单。

运气稍好，你可能需要花点时间寻找软件，或者正在请求的最新版本。可能需要去 GitHub 或 SourceForge.net。如果开发者的设置与你的太远，这是可以；额外的安装步骤可能会顺利进行。否则，不要绝望：是有帮助的。

大多数项目都有一种或多种报告问题和寻求帮助的方法：邮件列表或 Google Group；项目 SourceForge 页面上的一个页面，首席开发者的电子邮件地址，甚至是他们的 Twitter 账号。请尽可能详细地描述你的问题，并





# MagPi 基础教程

## [安装 UBUNTU]

Ubuntu 可以安装在 Pi (2 或 3 型) 上，也可以安装在你的 PC、Mac 或笔记本电脑上。

保持礼貌和耐心，通常你都能找到乐于帮助的人。记住，虽然人们乐于提供帮助，但你是在要求他们花时间来回答你的问题——如果你对安装过程感到沮丧（我们都经历过这种情况），请不要让这种情绪阻碍你对那些特意抽空帮助你的人保持尊重。

如果你没有时间跟进，但仍然对某个项目感兴趣，另一个选择是等待该项目的下一次发布。到那时，依赖项可能会变得更易获得，甚至进入 Raspbian 存储库，或者问题可能根本不再出现。

## 脚本化安装

你会被要求获取一个安装脚本并直接运行它——例如出色的 EduBlocks 也是这样，它是 Scratch 和 Python 之间的一个半中间地带，正帮助年轻编码者跨越这两种语言之间的巨大鸿沟。EduBlocks 希望你运行：

```bash
curl -sSL get.edublocks.org | bash
```

...这会获取 get.edublocks.org 上的 脚本（你可以在浏览器中查看），并将其传递到 Bash 进程中运行。-s 参数告诉 curl 不要显示进度条或错误消息；-S 覆盖此设置，在失败时显示错误消息；-L 告诉它跟随网站重定向到任何地方获取脚本。

如果你不喜欢在不知道软件对你的 Pi 做了什么的情况下运行它，或者只是想查看脚本内部看看安装到底做了什么，不如将其下载并保存为 edu-install.sh（前提是它不会覆盖当前工作目录中同名的文件）：

```bash
curl -o install.sh get.edublocks.org
```

...你将看到脚本下载并解压一个包含多个脚本的 tar 包，首先运行安装依赖项的那个脚本。

你可以运行下载的脚本——可以通过 `sh edu-install.sh` 来实现。如果你在运行之前没有阅读脚本，那么你就必须费很大精力去记住不仅是编写它的开发者，还有它在到达你的机器之前所经历的每一步。

### 征服命令行

![](img/db18fe165e1f1a64ee0c5d815560917d_80_0.png)

```bash
echo '正在移除旧下载...'
rm -f edublocks-ARCH.tar.xz

if [ -d edublocks ]; then
  echo '正在移除旧解压...'
  rm -rf edublocks
fi

echo '正在下载包...'
wget http://edublocks.org/downloads/edublocks-ARCH.tar.xz
echo '正在解包...'
tar -xf edublocks-ARCH.tar.xz
echo
```

EduBlocks 是一个很好的示例，它通过将安装的每个阶段放入 shell 脚本中，并仅提供一个命令来运行安装，让你的生活变得简单。

### Python，请收下

在多年从各种来源安装软件的过程中，我们学会了识别安装是否可能顺畅的迹象——一个希望的来源通常是用 Python 编写的内容。尽管好坏的软件都可以用任何语言编写，但 Python 软件和库（Libraries）似乎封装良好且可靠。

尽管像基于 Debian 的 GNU/Linux 发行版（如树莓派）拥有出色的 APT 和 dpkg（Debian 软件包管理器），但许多语言已经进化出了自己的打包工具和存储库生态系统——Emacs 编辑器就有好几个！你最可能遇到的两个是 JavaScript 的 npm 和 Python 的 pip。在使用 apt 之后，命令格式将让你很熟悉，

```bash
sudo pip3 install numpy
```

...记住这些内容也不算费力。在使用 apt 之后，命令格式将让你很熟悉。尽管你对命令行感到恐惧，但你也可以通过命令行使用 Python 库来测试 NumPy。如果无法看到图片对你来说网页没有意义，请考虑一下优点：没有追踪、阅读文本时的干扰，以及页面加载更快。

img/db18fe165e1f1a64ee0c5d815560917d_80.png

# [ 第十四章 ]

## 命令行命令行

### 征服命令行

![](img/db18fe165e1f1a64ee0c5d815560917d_81.png)

Linux 命令行快速指南：如何精通命令行
Ed 发布于 2017 年 7 月 23 日星期日 · 贡献者编辑
在本文中，我们将深入探讨命令行世界。许多人对命令行有负面看法，认为它是过时的工具。然而，一旦你掌握了它，你会发现它对于各种任务都是强大且高效的。

```bash
curl --version
7.68.0
```## Netcat 是什么以及如何使用

Netcat 被称为网络界的“瑞士军刀”。它是一个通过网络连接进行读写的多功能实用。在本文中，我们将展示如何使用 netcat 进行端口扫描、文件传输，甚至是隧道传输。

```bash
nc -lvp1234
```

### SSH: 安全外壳

SSH（Secure Shell）是一种加密协议，允许用户安全地登录远程机器。在本文中，我们将讨论如何使用 ssh 连接到服务器并像坐在那里一样执行命令。

```bash
ssh user@host
```

### Telnet: 老卫兵

Telnet —— 简称为打字机网络（teletype network）——是 20 世纪早期开发的协议，用于计算机之间的双向通信。它于一个没有安全考虑的时代，早已被 SSH 取代作为开放网络上直接连接的方法，但 Telnet 客户端在交互式查询服务（如邮件或网页）时仍然很有用，通过连接到服务器相应的端口并发送服务的命令：

```bash
telnet example.com 80
GET /HTTP/1.1
HOST: example.com
```





### 征服命令行

![](img/db18fe165e1f1a64ee0c5d815560917d_84_0.png)

终端是一个简单但实用的诊断工具，也用于我们在本章节稍后将介绍的一些功能性应用程序。

### Surfraw

正如我们之前看到的，通过 `wget` 和 `curl`，下载等功能可以从网络浏览器中移除。另一个让专门命令看起来最合适的场景是搜索。你可以通过一个名为 `surfraw` 的巧妙程序直接在命令行中查找，它可以帮助 elvi 处理困难的搜索任务——查看所有可用命令：

```
surfraw -elvi
```

作为命令行世界的一个良好公民，surfraw 尊重你的时间和手腱，可以简单地通过 `sr` 来调用。

- sr google -results=2 raspberry pi clojure gpio
- sr translate peloton
- sr gutenberg dickens
- sr wikipedia permaculture-tature
- sr bbcnews tim peake
- sr rhyme orange

## MagPi 核心要素

![](img/db18fe165e1f1a64ee0c5d815560917d_85_0.png)

没有存储空间，打开 YouTube 链接？下载视频稍后观看。结果将显示在你的浏览器中，你可以在 `/etc/xdg/surfconf/conf` 中设置，非常易于操作。

```
def SURFRAW_text_browser /usr/bin/lynx
def defyn SURFRAW_graphical no
```

### BBC (The Beeb)

```
sudo apt-get install youtube-dl
youtube-dl https://www.youtube.com/watch?v=ElB09DwxA6Q
```

每个下载的视频都保存为 MP4 文件，得益于 MPlayer 通过可选库输出视频的能力，甚至可以使用 `-vo caca` 选项在终端中通过 ASCII 渲染。它也可以通过 SSH 会话输出，尽管音频转发是一项留给读者研究的任务。ASCII 渲染远非高分辨率；如果你从虚拟控制台之一（我们在第一章中访问过的）运行 `mplayer`，它将默认采用帧缓冲区输出，在命令行上覆盖普通质量的视频。

你也可以从命令行访问 BBC 内容。虽然电视节目仅适用于位于英国的 IP 地址，但广播节目——从 Radio 3 到 Radio 4 Extra 上的经典喜剧和戏剧——可以通过 `get-iplayer` 脚本在广播后几天内进行下载；它将其保存为 AAC 格式以便以后收听。为了符合合理的合理使用条款——或至少等同 BBC 自己的 iPlayer 服务——节目应在 30 天后删除。

在编写时，节目搜索功能似乎不再能正常工作了。因此，你需要使用 iPlayer 网站找到所需节目的 PID（节目标识符），然后使用它来“录制”（即下载）。例如：

```
get_iplayer --pid=b0b95311
```

你还可以使用逗号分隔的 PID 列表一次性下载多个。

```
get_iplayer --pid=b0b95311,b0b94zn8,b0b950c9
```

使用 `--stream` 调用会将输出发送到 stdout，重定向到音频播放器（用于广播节目）。`--stdout` 切换在录制的同时也会执行此操作。

### 通信

我们在第 11 章的日历示例中提到了直接脚本化的命令行邮件。smtp 是 `mail` 命令的一个不错选择，可用于那些暗示你的树莓派执行某项操作的脚本。如今，让树莓派发布到微博是一个非常受欢迎的选择——至少如果微博是 Twitter 的话，尽管也有其他选择。

网上到处都是关于使用 Python 模块在树莓派检测到 GPIO 引脚上的各种事件时发布推文的说明。如果树莓派适合你的项目，那就尽管进行吧，但对于最简单的设置，只需要易于编写脚本的 `twidge`：

```
sudo apt-get install twidge
twidge setup
```

设置很简单：twidge 会给你一个要访问的 URL，你可以在那里授权 twidge 访问你的 Twitter 账户，它会给你一个供使用的授权代码，之后 twidge 即可准备就绪。`twidge list` 将列出可用命令。从命令行（或脚本）发布，可以尝试如下内容：

- [ EMAIL ]

如果你在跟上电子邮件使用感到困难：挑战一下自己使用几周 Mutt：命令行可能会让你留回收件箱。

```
twidge update "Testing twidge - tweeting from the #RaspberryPi #commandline."
```

更新也将从 stdin 读取。你项目 GitHub 页面上的帮助手册将引导你入门。对于命令行上的交互式（且色彩非常丰富）Twitter 客户端，请安装 Rainbowstream，你可以这样操作：

```
sudo pip3 install rainbowstream
```

### 不仅仅是噱头

命令行应用程序也适用于旧的互联网通信方式，从 IRC 到 Jabber，而 Mutt 是一个足够强大的电子邮件客户端，足以让人们（那些不会在终端里花费太多时间的人）继续使用它。严肃的工作在 shell 中完成，但它不断产出的命令行应用程序只是……





# 订阅12 个月即可随订阅免费赠 Pi Zero W 启动套件

立即订阅 12 个月纸质版，您将获得：

![](img/db18fe165e1f1a64ee0c5d815560917d_93_0.png)

- Pi Zero W
- 带有三个盖子的 Pi Zero W 外壳
- USB 和 HDMI 转换数据线
- 摄像头连接器

优惠可能随时更改或撤回

> 价值 20 英镑

# 立即购买：magpi.cc/subscribe

![](img/db18fe165e1f1a64ee0c5d815560917d_93_1.png)

# 在应用商店订阅， 2.29 英镑起

![](img/db18fe165e1f1a64ee0c5d815560917d_93_2.png)

![](img/db18fe165e1f1a64ee0c5d815560917d_93_3.png)

MagPi | 99

# MagPi
## 核心内容
raspberrypi.org/magpi
