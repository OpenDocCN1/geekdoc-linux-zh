

用于检验您对所学内容掌握程度的练习、支持论坛，以及其他更多资源。该网站包含大量有用的信息，以帮助用户更深入地了解 Kali Linux。

## 2.3.6 练习

*（这些练习不需要报告结果）*

- 1. 启动您的 Kali 操作系统，并将 kali 用户的密码更改为更安全的密码。
- 2. 花些时间熟悉一下 Kali Linux 菜单。
- 3. 使用 Kali Tools 网站，找到您最喜欢的工具并查阅其文档。如果没有特别喜欢的工具，可以任意选择一个。

## 2.4 在 Kali 中导航

### 2.4.1 Linux 文件系统

Kali Linux 遵循文件系统层次结构标准（FSH），[^35] 它为所有 Linux 用户提供了一个熟悉且通用的布局。您会发现以下目录最为常用：

- **/bin** - 基本程序（ls, cd, cat 等）
- **/sbin** - 系统程序（fdisk, mkfs, sysctl 等）
- **/etc** - 配置文件
- **/tmp** - 临时文件（通常在启动时删除）
- **/usr/bin** - 应用程序（apt, ncat, nmap 等）
- **/usr/share** - 应用程序支持文件和数据文件

还有许多其他目录，其中大多数您很少需要进入，但熟悉 Linux 文件系统布局将极大提高您的效率。

### 2.4.2 基本 Linux 命令

#### 2.4.2.1 手册页

接下来，让我们深入探讨 Kali Linux 的使用，并探索一些基本的 Linux 命令。

大多数用于 Linux 命令行的可执行程序都提供一份正式文档，通常称为*手册*或*手册页*（man pages）。[^36] 使用名为 **man** 的专用程序来查看这些页面。手册页通常包含名称、概要、命令用途的描述，以及相应的选项、参数或开关。让我们看一下 *ls* 命令的手册页：

```
kali@kali:~$  man  ls
```

*列表 3 - 探索 ls 命令的手册页*

[^35]: (Linux Foundation, 2016), https://wiki.linuxfoundation.org/fsb/fhs
[^36]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/Man_page

手册页不仅包含关于用户命令的信息，还包含系统管理命令、编程接口等方面的文档。手册的内容被分为若干部分，编号如下：

| 章节 | 内容 |
| :--- | :--- |
| 1 | 用户命令 |
| 2 | 内核系统调用的编程接口 |
| 3 | C 库的编程接口 |
| 4 | 特殊文件，如设备节点和驱动程序 |
| 5 | 文件格式 |
| 6 | 游戏和娱乐，如屏幕保护程序 |
| 7 | 杂项 |
| 8 | 系统管理命令 |

*表 2 - 手册页的组织结构*

要确定合适的手册章节，只需执行关键字搜索即可。例如，假设我们想了解 /etc/passwd 文件格式的更多信息。在命令行输入 `man passwd` 将显示手册第 1 部分中关于 passwd 命令的信息（图 4），这并不是我们感兴趣的内容。

![](img/ec25e59d75726b7041242a56d3376832_38_0.png)

*图 4：请求 passwd 文件的手册条目*

然而，如果我们使用 man 的 -k 选项，就可以执行关键字搜索，如下所示：

```
kali@kali:~$ man -k passwd
chpasswd (8) - update group passwords in batch mode
chpasswd (8) - update passwords in batch mode
exim4_password (5) - Files in use by the Debian exim4 packages
exim4_password_client (5) - Files in use by the Debian exim4 packages
expect_mkpasswd (1) - generate new password, optionally apply it to a user
fgetpwent_r (3) - get passwd file entry reentrantly
getpwent_r (3) - get passwd file entry reentrantly
gpasswd (1) - administer /etc/group and /etc/gshadow
grub-mkpasswd-pbkdf2 (1) - generate hashed password for GRUB
htpasswd (1) - Manage user files for basic authentication
...
```

![](img/ec25e59d75726b7041242a56d3376832_39_0.png)

我们可以借助正则表达式进一步缩小搜索范围。[^37]

```
kali@kali:~$ man -k '^passwd$'
passwd (1) - change user password
passwd (1ssl) - compute password hashes
passwd (5) - the passwd file
```

![](img/ec25e59d75726b7041242a56d3376832_39_1.png)

在上面的命令中，正则表达式由脱字符（^）和美元符号（$）包围，以匹配整行并避免子字符串匹配。现在我们可以通过引用相应的章节来查看我们感兴趣的具体 passwd 手册页：

```
kali@kali:~$ man 5 passwd
```

![](img/ec25e59d75726b7041242a56d3376832_39_2.png)

手册页通常是查找特定命令文档的最快捷方式，因此请花些时间更详细地探索它们。

#### 2.4.2.2 apropos

使用 apropos[^38] 命令，我们可以根据关键字搜索手册页描述列表中的可能匹配项。虽然这种方法略显粗糙，但对于根据描述查找特定命令非常有帮助。让我们看一个例子。假设我们想要对硬盘进行分区，但记不起命令名称。我们可以通过对"partition"进行 **apropos** 搜索来找出答案。

```
kali@kali:~$ apropos partition
addpart (8) - tell the kernel about the existence of a partition
cfdisk (8) - display or manipulate a disk partition table
cgdisk (8) - Curses-based GUID partition table (GPT) manipulator
cgpt (1) - Utility to manipulate GPT partitions with Chromium OS ...
delPart (8) - tell the kernel to forget about a partition
extundelete (1) - utility to undelete files from an ext3 or ext4 partition.
fdisk (8) - manipulate disk partition table
fixparts (8) - MBR partition table repair utility
gdisk (8) - Interactive GUID partition table (GPT) manipulator
gparted (8) - GNOME Partition Editor for manipulating disk partitions.
...
```

> *列表 7 - 使用 apropos 查找描述中包含 'partition' 的命令*

请注意，**apropos** 似乎执行了与 **man -k** 相同的功能；事实上，它们是等效的。

#### 2.4.2.3 列出的文件

**ls** 命令会在屏幕上输出基本的文件列表。我们可以使用各种通配符来修改输出结果。** -a** 选项用于显示所有文件（包括隐藏文件），而 **-1** 选项将每个文件显示在一行中，这在自动化过程中非常有用。

```
kali@kali:~$ ls
Desktop Documents Downloads Music Pictures Public Templates Videos

kali@kali:~$ ls /etc/apache2/sites-available/*.conf
/etc/apache2/sites-available/000-default.conf
/etc/apache2/sites-available/default-ssl.conf

kali@kali:~$ ls -a1
.
..
.bash_history
.bashrc
.cache
.config
Desktop
Documents
...
```

> *列表 8 - 列出文件*

#### 2.4.2.4 移动位置

Linux 不使用 Windows 样式的驱动器字母。相反，所有文件、文件夹和设备都是根目录的子项，根目录用 "/" 字符表示。我们可以使用 **cd** 命令后跟路径来切换到指定目录。**pwd** 命令会打印当前目录（如果您迷路了这很有帮助），运行 **cd ~** 将返回主目录。

```
kali@kali:~$ cd /usr/share/metasploit-framework/

kali@kali:/usr/share/metasploit-framework$ pwd
/usr/share/metasploit-framework

kali@kali:/usr/share/metasploit-framework$ cd ~

kali@kali:~$ pwd
/home/kali
```

> *列表 9 - 在文件系统中移动*

#### 2.4.2.5 创建目录

**mkdir** 命令后跟目录名称可创建指定目录。目录名称可以包含空格，但由于我们将在命令行上花费大量时间，使用连字符或下划线代替空格可以为我们省去很多麻烦。这些字符将使自动补全（通过按 [Tab] 键执行）变得更加容易。

```
kali@kali:~$ mkdir notes

kali@kali:~$ cd notes/

kali@kali:~/notes$ mkdir module one

kali@kali:~/notes$ ls
module  one

kali@kali:~/notes$ rm -rf module/ one/

kali@kali:~/notes$ mkdir "module one"

kali@kali:~/notes$ cd module\ one/

kali@kali:~/notes/module one$
```

我们可以使用极其实用的 `mkdir -p` 一次创建多个目录，它还会创建任何所需的父目录。这可以与花括号扩展结合使用，以高效地创建目录结构，例如用于存储您的渗透测试笔记。在下面的示例中，我们正在创建一个名为 **test** 的目录，并在该目录内创建名为 **recon**、**exploit** 和 **report** 的三个子目录。

```
kali@kali:~$ mkdir -p test/{recon,exploit,report}

kali@kali:~$ ls -l test/
exploit
recon
report
```

### 2.4.3 在 Kali Linux 中查找文件

Kali Linux 中用于定位文件的三个最常见 Linux 命令包括 `find`、`locate` 和 `which`。这些实用程序有相似之处，但工作方式和返回数据的方式不同，因此可能适用于不同的情况。

#### 2.4.3.1 which

**`which`** 命令 [^39] 在 `$PATH` 环境变量中定义的目录中搜索给定的文件名。该变量包含 Kali 在发出未包含路径的命令时搜索的目录列表。如果找到匹配项，**`which`** 将返回文件的完整路径，如下所示：

```
kali@kali:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

kali@kali:~$ which sdb
/usr/bin/sdb
```

[^37]: 正则表达式参考
[^38]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/Apropos
[^39]: (die.net, 2019), https://linux.die.net/man/1/which

