
# Red Hat Linux 7.3 初学者指南

dummies.com 提供每日免费电子小贴士

Jon "maddadog" Hall，Linux International 执行董事

Paul G. Sery，《Red Hat Linux 网络工具包》作者

![](img/5275bfa3908ad63320aaea42eefe467c_0_0.png)

Steven & Shelley Huff

`startX` = 从命令提示符启动 X 窗口

## vi 命令

以下命令列表包含了控制 vi 编辑器最实用且最常用的命令。事实上，我从 1981 年开始就一直在使用 vi，而且没有学过比这些更多的命令。这证明了人可以很懒但也能完成工作。

你可以在 Shell 提示符下输入这些命令。详情请参见第 4 章。

| vi | 在 vi 中打开文件名 |
|---|---|
| i | 进入插入模式，在当前位置之前插入 |
| Shift+I | 进入插入模式，在当前行开头插入 |
| a | 进入插入模式，在当前位置之后插入 |
| Shift+A | 进入插入模式，在当前行末尾插入 |
| esc | 从插入模式返回命令模式 |
| d | 在命令模式下删除字符 |
| cw | 删除光标左侧的单词并使编辑器进入插入模式 |
| :w | 保存文件 |
| :q | 退出且不额外写入磁盘 |
| :wq | 保存文件并退出 |
| Shift+ZZ | 保存文件并退出 |
| :q! | 强制退出（放弃未保存的更改） |
| /string | 在文件中向前搜索字符串 |
| ?string | 在文件中向后搜索字符串 |
| n | 查找下一个字符串（向前或向后） |
| u | 撤销上一个命令 |

## 系统管理命令

我们在下方列出了若干常用的 Linux 命令，帮助你管理磁盘、关闭计算机并获取其相关信息。

你可以在 Shell 提示符下输入这些命令。有关如何输入命令的更多信息，请咨询第 4 章。

| `mount [options]` | 挂载文件系统 |
| `device_file_system` | |
| `umount [options]` | 卸载文件系统 |
| `file_system` | |
| `fsck [options]` | 检查指定文件系统的结构和完整性 |
| `file_system` | |
| `mkfs` | 在底层格式化的磁盘上建立目录结构 |
| `shutdown` | 直接关闭系统，而不是等待消息发送（Ctrl+Del 作用相同） |
| `vmstat [options]` | 查看虚拟内存性能 |
| `procinfo` | 收集进程信息 |

## 文件权限

以下示例展示了不同的文件权限组合。有关文件权限的更多信息请参阅第 15 章。

| `-wxrwxrwx` | 用户、组和其他人（所有人）的读、写、执行权限（模式 777） |
| `drwxrxr-x` | 一个所有者完全开放的目录，组可以读取和搜索，其他人仅可读取（不可搜索）（模式 754） |
| `cr-rw-r--` | 字符文件，所有者可以读或写，组和其他人只能读（模式 644） |
| `br-rw-r--` | 块文件；只有所有者可以读或写（模式 600） |

### 一些常用命令

下方列出了常用且有效的命令。你可以在 Shell 提示符下输入这些命令。请参阅第 4 章。

| `cd directory` | 将当前目录切换到目录 |
| `ls [options] [directory]` | 列出当前目录的内容 |
| `ls -l` | 列出当前目录的内容，以及文件的 own、权限、所有者和日期 |
| `ls -a` | 列出所有文件，包括隐藏文件（以点开头的文件名） |
| `pwd [option]` | 打印工作目录（你所在的目录） |
| `rm [options] filename` | 删除文件 |
| `mkdir directory_name` | 创建一个新的（空）目录 |
| `rmdir directory_name` | 删除空目录 |
| `cp [options] src filename_dst` | 复制文件 |
| `mv [options] filename filename_dst(s)` | 移动（或重命名）文件 |
| `cat [options] filename` | 将文件连接到标准输出（显示文件） |
| `more [options] filename` | 分页显示文件 |
| `less [options] filename` | 分页显示文件 |
| `touch [options] filename` | 创建新的（空）文件，更改现有文件的访问日期 |
| `chown [options] filename` | 更改文件或目录的所有者 |
| `chgrp [options] filename` | 更改文件或目录的组 |
| `chmod [options] filename` | 修改文件或目录的权限 |
| `sort [options] filename` | 按特定排序文件（取决于选项） |
| `echo [options] text string` | 在命令后显示输入的内容 |
| `date [options] text string` | 读取日期和时间（不带参数）；设置日期和时间（带参数） |
| `cut [options] filename` | 将宽文件拆分为多行 |
| `sed [options] source` | 用于大文件或实时编辑的流编辑器 |
| `ln [options] source filename/directory_target` | 将文件链接到另一个文件 |
| `grep [options] filename` | 使用通用表达式查找数据的搜索程序，并打印输出 |

![](img/5275bfa3908ad63320aaea42eefe467c_3_0.png)

你是否对电脑感到畏惧和困惑？你是否发现传统手册充满了你永远用不上的技术细节？你的朋友和家人是否总是打电话让你帮你修理 PC 上的简单问题？那么由 Wiley Publishing, Inc. 出版的“傻瓜”计算机书籍丛书正适合你。

“傻瓜”系列是为那些感到沮丧的计算机用户编写的，他们知道自己并不笨，但 PC 硬件、软件以及计算机领域独特的词汇确实让他们感到无助。“傻瓜”系列采用幽默的方法、接地气的风格，甚至使用卡通和幽默的图标来消除计算机新手的恐惧并建立他们的信心。这些书风格轻松但不轻量，是任何被迫使用电脑的人的完美生存指南。

> 我非常喜欢我的这本书，我告诉了朋友；现在他们也买了。
> —Irene C., 俄亥州奥尔亥

> “快速、简洁、非技术性且幽默。”
> —Jay A., 伊利诺伊州埃尔伯

> “感谢，我需要这本书。现在我晚上可以睡好觉了。”
> —Jay A., 伊利诺伊州埃尔伯

![](img/5275bfa3908ad63320aaea42eefe467c_4_0.png)

## 作者简介

Jon "maddog" Hall 是 Linux International 的执行董事，这是一个致力于推广 Linux 操作系统使用的供应商组织。他在计算机行业已经工作了超过四分之一世纪（这听起来似乎比直接说“25年”更有说服力），其中过去的 18 年里一直致力于编程和仰赖 UNIX 操作系统。目前，Jon 就职于康柏电脑公司（Compaq Computer Corporation），帮助制定康柏有关 Linux 的战略。在此之前，Jon 曾担任哈特福州立技术学院（Hartford State Technical College）计算机科学系主任，在他试图教学生操作系统设计、编译理论以及如何过尊严的生活时，学生们亲爱地（他希望是这样）给了他“maddog”这个绰号。

1994年5月在数字设备公司（Digital Equipment Corporation）工作期间，maddog 遇到了林斯·托瓦尔斯（Linus Torvalds），他足够聪明（他的批评者认为 maddog 只是幸运），意识到 Linux 操作系统的潜力改变了他的生活，主要是因为这让他提供了每天工作 22 小时的机会。然而，自从 maddog 开始接触 Linux 以来，他也开始遇到更多的女孩（特别是他的两个孙女）。你通常可以在各种 Linux 会议和活动上看到 Jon 演讲（maddog 在吠叫），他还闻名于长途跋涉为当地的 Linux 群组进行演讲。

Paul G. Sery 是就职于美国新墨西哥州阿尔伯克尔基桑迪亚国家实验室（Sandia National Laboratories）的计算机工程师。他是特殊项目计算机支持单元的成员，该单元专门负责管理和排除 UNIX 和 Linux 故障。
