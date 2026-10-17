
```
../configure --with-prefix=/usr --with-lisp-dir=/usr/share/emacs/site-lisp --info-dir=/usr/info
```

如果你希望将 Info 文档文件放在 `/usr/local/info` 以外的其他位置，请使用 `--info-dir` 开关。

现在，将新创建的 `makefile` 加载到 Emacs 会话中，并在文件顶部附近查找以下部分：

```
##################################################
#
# user configurable parameters
#

prefix=/usr

# LIB_DIR should be a private place for notes-mode stuff.
LIB_DIR=$(prefix)/share/notes-mode

# EL_DIR should be where your site-specific emacs .el[.c]s go.
EL_DIR=/usr/share/emacs/site-lisp
# INFO_DIR is for emacs info files.
INFO_DIR=$(prefix)/info
INSTALL_INFO=/usr/sbin/install-info
# must be perl 5.000 or better.
PERL=/usr/bin/perl
# must be 19 or greater
EMACS=emacs
MKDIR_P=mkdir -p
#
       !
# end of user configurable parameters
#
##################################################
```

检查参数是否准确反映了你希望安装软件包的方式。进行必要的更改并将文件保存到磁盘。

### XEmacs 用户

XEmacs 用户需要进行一项额外编辑；将此行：

```
EMACS=emacs
```

改为：

```
EMACS=xemacs
```

这假设 XEmacs 可执行文件在你的路径中。否则，也输入路径——例如像这样：

```
EMACS=/opt/bin/xemacs
```

现在 `makefile` 已准备就绪，你可以输入

```
make install
```

Lisp 文件将由非交互式 Emacs 或 XEmacs 进程在后台进行字节编译，然后复制到你的 `site-lisp` 目录。Perl 脚本被复制到 `/usr/local/share/notes-mode`（或者——如果你指定了不同的前缀，则为你指定的位置），Info 文档文件加入你的其他 Info 文件。你需要在 Info 目录的 `dir` 文件中添加一行如下所示：

```
* Notes Mode: (notes-mode). On-line note organizer
```

### 初始化

在你可以开始使用 Notes 模式之前，还有一个最后步骤。切换到 Perl 脚本安装的目录（默认位置是 `/usr/local/share/notes-mode`）。通过输入以下命令执行其中一个脚本

```
notesinit
```

这是一个交互式脚本。你会被询问各种问题，例如你希望笔记目录位于何处，脚本根据你的回答完成设置，如有必要则创建目录。如果你希望使用该模式，系统上的每个用户都必须运行此脚本。

`notesinit` 脚本执行的一项任务是设置你的 `crontab` 文件，以便其他 Perl 工具在适当间隔被调用。这是否有效取决于你的 Linux 发行版中 `cron` 的配置方式。

阅读你的 `cron` 文档以了解 `crontab` 配置文件位于何处，并检查是否已为 Notes 模式的 `mkall` 命令添加了条目。如果出错且未添加，你需要添加一个每日 `cron` 任务。以下命令需要在每日 `cron` 会话期间执行：

```
/usr/local/share/notes-mode/mkall
```

例如，在我的 Debian 系统上，各种 `cron` 任务是位于 `/etc/cron.daily`、`/etc/cron.weekly` 和 `/etc/cron.monthly` 目录中的 shell 脚本形式。以下是名为 `notes-mkall` 的 shell 脚本的内容，它每天运行一次 `mkall` Perl 脚本：

```
#!/bin/sh
# notes-mode cron daily
/usr/local/share/notes-mode/mkall
```

这样的脚本需要由类似以下命令设为可执行：

```
chmod +x /etc/cron.daily/notes-mkall
```

你真的需要确保 `cron` 已设置为每天运行 `mkall`，尽管我想你可以每两三天自己运行一次该命令。不过，让笔记索引保持最新而无需自己记住去做，是件好事。

运行 `notesinit` 的一个结果是，会创建一个示例笔记文件并将其插入到你新的笔记目录中。这个文件能让你了解笔记文件的格式。以下是示例的样子：

```
• Today ------
to do list goes here?
```

```
• Environment/notes ---------------
Set up notes with notesinit.
```

`mkall` Perl 脚本（每天作为 `cron` 任务运行）会对所有现有的笔记文件进行索引和交叉引用。你创建的每个笔记文件都会自动获得一个反映其创建日期的数字名称。举个例子，我是在 2001 年 2 月 17 日撰写这段文字的。今天早上为我创建的笔记文件的文件名和路径如下：`/home/layers/Notes/200102/010217`。

目录名称 `200102` 应解释为 2001 年的第二个月，而文件名 `010217` 则使用年份的后两位数字，接着是月份和日期。这些名称并非真正供你直接使用的；它们是为了供在后台运行的索引 Perl 程序使用，以保持你的笔记有序且易于访问。

Perl 脚本每天生成一个新的索引，将你的笔记按主题标题排序，而单个笔记文件则按时间顺序排列。索引缓冲区中的每一项（可以从任何 Notes 模式缓冲区调用）都是指向你的某个笔记文件的可点击链接。

具有特定主题行的条目可以通过按键命令从所有现有笔记复制到单个摘要缓冲区中。这是一种便捷的方式，可以查看具有相同主题的每个笔记，作为按时间顺序和主题从一个笔记移动到另一个笔记的替代方法。

图 15.1 显示了一个摘要缓冲区。这是一个临时缓冲区，但可以保存到文件中。

脚本完成的另一项任务是更新笔记文件内的所有链接。如果你在一周前写了一篇主题行为“** 政治”的笔记，今天又写了一篇具有相同主题的笔记，那么一周前的文件中会插入一个新的“下一个”链接，指向今天的文件。你的旧笔记会不断被更新，以包含指向较新笔记的链接。

![](img/c8827ea52a0796def3f6891892ed9d3a_301_0.png)

Notes 模式将任何以星号后跟空格开头的行识别为主题标题。`**Today**` 标题是一个特殊的标题。该标题及其后续内容会从上一个笔记文件复制到下一个新文件中。这是插入“待办”事项的地方；它们会出现在后续的所有笔记中，直到你删除它们。如果你不习惯制作待办事项列表，只需删除示例条目，并将 `**Today**` 类别用作导航到前一天笔记的方法。

只要行以星号开头且名称前有一个空格，你随时可以创建新的类别。一旦你使用过某个主题行并且它已被索引，下次输入它时你就可以使用 Tab 补全功能。

在输入带有星号空格标识符的主题前按 Enter 键即可开始一个新笔记。主题行会自动被下划线标记，并为该笔记创建伪 URL。如果存在具有该主题标题的前一个笔记，也会插入其伪 URL，这样你就可以立即返回到该笔记（如果你希望的话）。

外部链接是指向你机器或网络上其他文件的指针。它们的工作方式类似于 HTML 链接，作为一种伪 URL。它们看起来像这样：

```
file:////usr//local/articles/mencken.txt
```

在积累了一定数量的笔记之前，Notes 模式的强大和便利功能真的无法被充分认识。按日期、索引或主题在一个笔记之间导航，类似于浏览万维网，只不过那是你个人的笔记网络。

## 键盘和鼠标命令

笔记导航可以基于鼠标或键盘。按键绑定基于 `Ctrl-c` 前缀：

| 命令 | 操作 |
|---|---|

| `Ctrl-c Ctrl-n` | 移动到具有相同主题的下一个笔记。 |

| `Ctrl-c Ctrl-p` | 移动到具有相同主题的上一个笔记。 |

| `Ctrl-c Ctrl-i` | 移动到索引缓冲区，其中包含指向每个笔记的链接。 |

| `Ctrl-c Enter` | 跟随伪 URL 链接。 |

| `Ctrl-c Ctrl-k` | 将当前笔记的伪 URL 复制到 kill ring。 |

| `Ctrl-c Ctrl-s` | 将所有具有当前笔记主题标题的笔记收集到一个摘要缓冲区中。 |

| `M-Ctrl-a` | 跳转到当前条目的开头。 |

| `M-Ctrl-e` | 跳转到当前条目的末尾。 |
