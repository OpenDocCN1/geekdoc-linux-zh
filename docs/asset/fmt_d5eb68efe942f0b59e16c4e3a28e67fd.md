
最后，探索 VMware 的快照功能，它允许我们在出现问题时恢复或重置虚拟机到干净状态。定期拍摄快照可以在出现问题时节省大量时间和烦恼。

## 2.2 Kali 菜单

Kali 菜单包含了该发行版中许多工具的分类链接。这种结构有助于明确每个工具的作用以及其用法的背景。

花些时间浏览 Kali Linux 菜单，以帮助熟悉可用的工具及其分类。

## 2.3 Kali 文档

作为一个功能完整的操作系统，Kali Linux 提供了许多我们在本课程中无法充分探索的功能和能力。不过，有几个官方 Kali Linux 资源可供进一步的研究和学习：

- Kali Linux 官方文档²³

- Kali Linux 支持论坛²⁴

# 攻击安全 (OFFENSIVE SECURITY)

www.offensive-security.com

Kali Linux 渗透测试 2.0

- Kali Linux 工具网站²⁵

- Kali Linux 错误跟踪器²⁶

- Kali Linux 培训²⁷

### 2.3.1 Kali Linux 官方文档

Kali Docs 网站²⁸ 正如其名，是 Kali Linux 文档库。该网站提供了最新的 Kali 细节，包含许多步骤，应被视为 Kali Linux 故障排除和支持的首站。

### 2.3.2 Kali Linux 支持论坛

故障排除和支持的下一步是 Kali Linux 支持论坛。²⁹ 在发布之前，请阅读论坛规则和指南³⁰，因为不符合规则的帖子通常会被审核或忽略。在创建新主题之前，请务必在论坛中彻底搜索之前发布的解决方案。

### 2.3.3 Kali Linux 工具网站

### 2.3.4 Kali Linux 错误跟踪器

偶尔某些工具可能会崩溃或产生意外结果。当这种情况发生时，在 Kali Linux 错误跟踪器³² 上搜索错误消息可能会确定问题是否为 bug，如果是，以及如何解决。用户也可以通过该网站报告 bug 来帮助社区。

### 2.3.5 Kali Linux 培训网站

Kali Linux 培训³³ 托管官方 Kali Linux 手册和培训课程。这个免费网站基于《Kali Linux Revealed》³⁴ 书籍，包含 HTML 和 PDF 格式的书籍内容、测试你对手册掌握程度的练习、一个支持论坛等等。该网站包含了大量有用信息，帮助用户更好地熟悉 Kali Linux。

²⁵ (Offensive Security, 2019), https://tools.kali.org

²⁶ (Offensive Security, 2019), https://bugs.kali.org

²⁷ (Offensive Security, 2019), https://kali.training

²⁸ (Offensive Security, 2019), https://docs.kali.org

²⁹ (Offensive Security, 2019), https://forums.kali.org

³⁰ (Offensive Security, 2019), https://forums.kali.org/forumdisplay.php?f=72-Forums-Rules-and-Guidelines

³¹ (Offensive Security, 2019), https://tools.kali.org

³² (Offensive Security, 2019), https://bugs.kali.org

³³ (Offensive Security, 2019), https://kali.training

³⁴ (Offensive Security, 2019), https://kali.training

PWK 2.0 版权 © Offensive Security Ltd. 版权所有。 36

### 2.3.6 练习

（这些练习不需要报告）

- 1. 启动你的 Kali 操作系统并将 `kali` 用户密码更改为安全的密码。

2. 花些时间熟悉 Kali Linux 菜单。

3. 使用 Kali 工具网站，找到你喜欢的工具并查看其文档。如果你没有喜欢的工具，任选一个即可。

## 2.4 在 Kali 中穿行

### 2.4.1 Linux 文件系统

Kali Linux 遵循文件系统层次结构标准 (FHS)，为所有 Linux 用户提供了一个熟悉且通用的布局。你将最常用的目录有：

- `/bin` - 基本程序 (`ls`, `cd`, `cat`, 等)

- `/sbin` - 系统程序 (`fdisk`, `mkfs`, `swctl`, 等)

- `/etc` - 配置文件

- `/tmp` - 临时文件（通常在启动时删除）

- `/usr/bin` - 应用程序 (`ncat`, `ncat`, `nmap`, 等)

- `/usr/share` - 应用支持和数据文件

还有许多其他目录你很少需要进入，但对 Linux 文件系统布局良好的熟悉将极大提高你的效率。

### 2.4.2 基础 Linux 命令

#### 2.4.2.1 手册页 (Man Pages)

接下来，让我们深入 Kali 的用法并探索一些基础命令行，提供正式的文档，通常被称为手册（manual）或手册页³⁵。一个名为 `man` 的特殊程序用于查看这些页面。手册页通常包含名称、摘要、命令目的的描述以及相应的选项、参数或开关。让我们看看 `ls` 命令的手册页：

```
man ls
```

> Listing 3 - 查看 ls 命令的手册

³⁵ (Linux Foundation, 2016), https://wiki.linuxfoundation.org/lsb/fhs

³⁶ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Man_page

# 攻击安全 (OFFENSIVE SECURITY)

Kali Linux 渗透测试 2.0

手册页不仅包含用户命令的信息，还有关于系统管理命令的文档。手册分为以下章节：

| 章节 | 内容 |
| :--- | :--- |
| 1 | 用户命令 |
| 2 | 系统调用 |
| 3 | C 库 |
| 4 | 设备驱动程序 |
| 5 | 文件格式 |
| 6 | 游戏 |
| 7 | 杂项 |
| 8 | 系统管理 |

要确定相应的章节，可以使用以下命令：

```bash
man 5 passwd
```

> Table 2 - 章节组织

然而，在命令中，正则表达式由脱字符 (`^`) 和美元符号 (`$`) 表示，用于匹配行首行尾。我们现在查看感兴趣的精确手册：

```bash
man 5 passwd
```

> List 4 - 执行密码搜索

手册页是查找特定命令文档的最快方法，花时间以更详细的方式探索它们。

### 2.4.2.2 apropos

通过 `apropos`⁸ 我们可以根据关键词在手册页描述列表中搜索特定的匹配。虽然这种方法有点粗浅，但对于根据描述查找特定内容非常有帮助。让我们来看一个例子：假设我们要对硬盘进行分区，但不记得命令的名字。我们可以通过对 "partition" 进行 `apropos` 搜索来解决：

```bash
kali@:- apropos partition
addpart (8) - 通知内核分存在
cfdisk (8) - 显示分区表
cgisk (8) - 字符界面 GUID 分区表 (GPT) 操作器
cogpt (7) - 使用 Chromium 管理 GPT 分区的工具
delpart (8) - 通知内核忘记某个分区
undeletelete (1) - 从 ext3 或 ext4 分区中删除文件的工具
fdisk (8) - 管理分区表
fixparts (8) - MBR 分区表修复工具
gdisk (8) - 交互式 GUID 分区表 (GPT) 操作器
gparted (8) - 用于管理磁盘分区的 GN 分区编辑器。
```

³⁷ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Regular_expression

³⁸ (The Linux Information Project, 2004), http://www.linfo.org/apropos.html

PWK 2.0 版权 © Offensive Security Ltd. 版权所有。 39

## 列表 7 - 使用 apropos 查找描述中包含 'partition' 的命令

请注意，`apropos` 的功能似乎与 `man -k` 相同，事实上，它们是完全等价的。

### 2.4.2.3 列出文件

`ls` 命令在屏幕上打印出基础的文件列表。我们可以使用各种选项来修改输出结果。`-a` 选项用于显示所有文件（包括隐藏文件），`-1` 选项将每个文件显示在单行，这非常有用。

```
kali@kali:~$ ls
Desktop Downloads Music Pictures Public Templates Videos

kali@kali:~$ ls /etc/apache2/sites-available/*.conf
/etc/apache2/sites-available/default-ssl.conf

kali@kali:~$ ls -ai
...
.bash_history
.bashrc
.cache
.config
Desktop
Documents
...
```

> 列表 8 - 列出文件

### 2.4.2.4 移动

Linux 不使用 Windows 风格的驱动器号。相反，所有文件、文件夹、设备和设备都是根目录的子节点，由字符 `/` 表示。我们可以使用 `cd` 命令后跟指定目录的路径。`pwd` 命令将打印当前目录（如果你迷了路，这很有帮助），使用 `cd ~` 可以返回主目录。

```
kali@kali:~$ cd /usr/share/metasploit-framework/
kali@kali:~$ /usr/share/metasploit-framework pwd
/usr/share/metasploit-framework
kali@kali:~$ /usr/share/metasploit-framework cd ~
kali@kali:~$ pwd
/home/kali
```

> 列表 9 - 在文件系统中移动

### 2.4.2.5 创建目录

使用 `mkdir` 命令后跟目录名称可以创建指定的目录。目录名称可以包含空格，但由于我们将在命令行花费大量时间，我们通常使用连字符或下划线来代替，这样可以省去很多麻烦。这些字符会让自动补全（通过 [Tab] 键执行）变得更更容易完成。

```
kali@kali:-$ mkdir notes
kali@kali:-$ cd notes/
kali@kali:/~/notes$ mkdir module one
kali@kali:/~/notes$ ls
module one
kali@kali:/~/notes$ rm -rf module/one/
kali@kali:/~/notes$ mkdir "module one"
kali@kali:/~/notes$ cd module one/
kali@kali:/~/notes/module one$
```

列表 10 - 在 Kali 中创建目录

我们可以使用非常有用的 `mkdir -p` 一次创建多个目录，它还会创建任何所需的父目录。这可以与大括号扩展结合，创建一个目录结构，例如你的渗透测试笔记。在下面的示例中，我们正在创建一个名为 `test` 的目录，并在该目录下创建三个名为 `recon`、`exploit` 和 `report` 的子目录。

```
kali@kali:-$ mkdir -p test/{recon,exploit,report}
kali@kali:-$ ls -l test/
exploit
recon
report
```

列表 11 - 创建目录结构

### 2.4.3 在 Kali Linux 中查找文件

在 Kali Linux 中查找文件的三个常用的 Linux 命令包括 `find`、`locate` 和 `which`。这些工具有相似之处，但工作方式和返回数据的方式不同，并可能用于不同的情况。

#### 2.4.3.1 which

`which` 命令³⁹ 在 `$PATH` 环境变量中定义的目录中按名称搜索文件。该变量包含了当在发布命令时不带其路径时，Kali 搜索的目录列表。如果找到匹配项，`which` 将返回文件的完整路径，如下所示：

```
kali@kali:-$ echo $PATH
/usr/local/bin:/usr/local/bin:/usr/sbin:/usr/bin:/usr/bin:/bin
```

```
kali@kali:-$ which sbd
/usr/bin/sbd
```

> ³⁹ (die.net, 2019), https://linux.die.net/man/1/which

PWK 2.0 版权 © Offensive Security Ltd. 保留所有权利21

列表 12 - 探索命令

### 2.4.3.2 locate

`locate` 命令⁴⁰ 是在 Kali 中查找文件和目录最快的方法。为了提供更短的搜索时间，`locate` 搜索内置数据库 `locate.db` 而不是整个硬盘索引。该数据库由 cron 调度器定期自动更新。要手动更新 `locate.db` 数据库，可以使用 `updatedb`

```
kali@kali:~$ sudo updatedb
kali@kali:~$ locate sbd.exe
/usr/share/windows-resources/sbd/sbd.exe
```

列表 13 - 探索 locate 命令

### 2.4.3.3 find

`find` 命令⁴¹ 是这三个工具中最复杂且最灵活的搜索工具。掌握它的语法可能很困难，但它的功能超越了普通的文件搜索。`find` 命令的基本用法如列表 14 所示，其中我们从根系统目录开始递归搜索，查找任何包含字母 "sbd" 的文件。

```
kali@kali:~$ find / -name "sbd*"
/usr/bin/sbd
/usr/share/windows-resources/sbd/sbd.exe
```

列表 14 - 探索 find

`find` 相比于 `locate` 的主要优势是它可以按大小、所有者、类型、时间戳、权限等进行搜索。

### 2.4.3 练习

- 使用 `systemctl` 启用服务。

- 使用 `man` 查找命令。

- 使用 `which` 查找服务。

- 使用 `locate` 识别服务。

- 使用 `find` 搜索文件。

> ⁰ (die.net, 2019), https://linux.die.net/man/1/locate

> ¹ (die.net, 2019), https://linux.die.net/man/1/find

> ² (Stack Exchange, 2015), https://stackoverflow.com/questions/60205

## 2.5 管理 Linux 服务

Kali Linux 是一个针对安全人员的专用 Linux 发行版。作为此类，它包含了标准功能。Kali 安装自带了一些服务，如 SSH、HTTP 等。因此，这些服务会在启动时加载，导致 Kali 暴露多个端口。Kali 通过设置来解决这个问题。

### 2.5.1 SSH 服务

SSH（Secure Shell）⁴ 通常用于远程访问计算机，使用安全的加密协议。该服务基于 TCP 并监听 22 端口。要在 Kali 中启动 ssh 服务，我们使用 `systemctl` 命令后跟服务名称（本例中为 ssh）：

```
kali@kali:~# sudo systemctl start ssh
kali@kali:~$
```

当命令成功执行时，它不会返回任何输出，但我们可以通过 `ss` 命令并将输出传递到 `grep` 来验证 ssh 服务正在运行并监听 22 端口：

```
kali@kali:~# sudo ss -antlp | grep sshd
LISTEN 0 128 :::22 *:*: users:("sshd",pid=1343,fd=3))
```

（注：此处原文代码块似乎显示不完整，已按逻辑尽可能对齐）

如果我们希望 ssh 服务在启动时自动运行（许多用户都是如此），只需使用 `systemctl` 启用它。不过，请确保先更改默认密码！

```
kali@kali:~# sudo systemctl enable ssh
Synchronizing state of ssh.service with SysV service script with /lib/systemd/systemd-install
Executing: /lib/systemd/systemd-install enable ssh
Created symlink /etc/systemd/system/ssh.service -> /lib/systemd/system/ssh.service.
```

我们可以使用 `systemctl` 启用和禁用 Kali Linux 中的大部分服务。

### 2.5.2 HTTP 服务

Apache HTTP 服务在渗透测试期间使用，用于托管网站，或为向受害者机器提供下载文件的平台。HTTP 服务是 TCP 的

默认在 80 端口监听。为了在 Kali 中启动 HTTP 服务，我们可以像启动 SSH 服务一样使用 `systemctl`，只需将服务名称替换为 "apache2"：

```
kali@kali:~$ sudo systemctl start apache2
kali@kali:~$ 
```

列表 18 - 使用 systemctl 在 Kali 中启动 apache 服务

与 SSH 服务一样，我们可以使用 `ss` `grep` 命令来验证 HTTP 服务是否正在运行并监听 tcp 端口 80。
