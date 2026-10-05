

| emacs | (在终端中) emacs 编辑器。仅供高手使用。是的，也可以使用 "vi" 编辑器（不建议新手使用）。退出 "vi" 请按：:<Esc>:<Enter> |
| gcc filename.c | GNU C 编译器。非常直观。网上可以找到很棒的免费手册。 |
| g++ filename.C | GNU C++ 编译器。"C" 通常用于 C++ 源代码。 |
| perl | 现代且优雅的对象对象解释器。比 perl 更加强大且易于使用。网上可以找到由 G. van Rossum 编写的非常棒（且免费）的书（http://www.python.org/doc/ 或 http://python.org/download）。 |
| tcl | (通常读作 "tickle")。流行的脚本语言。 |
| wish | (xterm) Tk 的前前端，Tk 是 tcl 的一个 Windows 扩展。通常用于构建程序的前端。 |
| guile | "Scheme" 编程语言的一种实现。 |
| g77 | GNU FORTRAN。如果你使用 FORTRAN，你可能想检查：http://stdlib.physat.org/templon/html/ 寻找适合你特定需求的 FORTRAN 编译器。 |
| f2c | FORTRAN 转换工具。 |
| fort77 | FORTRAN 编译器。调用 f2c 然后是 gcc 或 g++。 |
| basic | "Chiptmunk Basic"。 |
| make | 运行 "make" 工具来编译当前目录下的 Makefile 中的项目。 |
| cvs | 并发版本控制。尝试：info cvs |
| diff file1 file2 pathfile | 比较两个文件的内容并列出任何差异。将输出保存到文件路径 pathfile。 |
| diff file1 file2 | 两个文本文件的并排比较。 |
| patch file_to_patch file_to_patch | 将补丁（由某个文件生成，列出两个文件之间的差异的文件）pathfile 应用到 file_to_patch。 |
| grep | 搜索文件中匹配模式的内容。至少学习此 grep 命令的基础知识绝对值得。模式使用一种名为“正则表达式”的强大且标准的表示法指定。 |
| tr | 翻译工具（处理 t 文件中的每个字符）。 |
| gawk | GNU awk（主要用于处理已删除的文件）。 |
| sed | 处理文本文件的工具。 |
| strings filename | 显示二进制文件 filename 中包含的字符串。 |

前往第 7 部分：Linux 应用（专有或非开源）

# Linux 新手管理员指南

版本 0.59 1999-11-07

# 第 7 部分：一些必要的 Linux 应用（专有或非开源）

作者 Peter, Stan, 和 Marie Klimas

## 一些常见 Linux 问题的解答
根据通用公共许可协议分发 http://www.gmu.org/copyleft/gql.html。感谢您的反馈、意见、纠正和改进。请发送至 bklimas@magma.ca

## 网站快速导航：

* 首页：Linux 新手管理员指南
* 第 0 部分：给犹豫不决者（Linux 的优势）
* 第 1 部分：安装 Linux 之前
* 第 2 部分：Linux 资源、帮助及链接
* 第 3 部分：基本操作常见问题 (FAQ)
* 第 4 部分：Linux 新手管理员常见问题 (FAQ)
* 第 5 部分：如何升级内核
* 第 6 部分：Linux 快捷键和命令
* 第 7 部分：>必要的 Linux 应用（专有或非开源）<

## 本页目录：

# 7. 一些必要的 Linux 应用（专有或非开源）：

* 7.1 Linux 版 Word Perfect 8 [第 120 页]
* 7.2 Star Office 套件 [第 120 页]
* 7.3 Applicware [第 121 页]
* 7.4 AbiWord [第 121 页]
* 7.5 表格软件 [第 121 页]
* 7.6 数据库 [第 122 页]
* 7.7 CAD [第 122 页]
* 7.8 Netscape 和 Lynx (x 浏览器) [第 123 页]
* 7.9 Klyx 和 Latex [第 124 页]
* 7.10 刻录 CD-R (cdrecord 和 cdparanoia) [第 126 页]

# 7. 一些必要的 Linux 应用（专有或非开源）：

这并不是 Linux 应用的完整列表。筛选标准为：

* * 该应用程序在默认 RedHat 安装期间未安装——用户必须采取主动步骤来查找/安装它。
* * 我们特别喜欢这个应用程序，或者某个可靠的来源让我们相信它非常值得推荐。

有成千上万个 Linux 程序。如果你对我们的精选结果不满意，请尝试：
http://www.linuxapps.com/ 或 http://stommel.tamu.edu/~baum/linuxlist/linuxlist/linuxlist.html 或
http://www.bootell.com/lsm/ 或 http://www.linuxlinks.com/Software/

# 7.1 Linux 版 Word Perfect 8

这是一个非常优秀且强大的文字处理器。提供免费版本供个人使用。尝试：
http://linux.core.com/download.htm。免费版缺少编辑器、内置图形编辑器、图表编辑器和“艺术字体”，但在其他方面，它是世界上最优秀文字处理器的全功能版本。完整版售价 50 美元。

在遇到的情况下，它与 MS Word 的文件级兼容性非常好，表明 WP8 实际上可能比 MS Word 本更能兼容 MS Word 格式的不同“子版本”。

# 7.2 Star Office 套件

Star Office 是一个完整的办公套件：包含文字处理器、电子表格和演示文稿。个人使用免费，尝试：http://www.stardivision.com/free/ (较大，60-80 MB)。

Star Office 看起来和操作非常像 MS Office（尽管很大且运行缓慢），在没有至少 32 MB 内存的情况下可能并不实用。它与 MS Office 有良好的兼容性（可以读写 MS Word、Excel 和 PowerPoint 格式）。旧版本的 Star Office 在你获得“密钥”后需要注册。注册密钥基于你给 Star Office 的邮箱，调调器。

# 7.3 Applicware

Applicware 是另一个完整的办公套件。它包含文字处理器、电子表格、图形、演示文稿、邮件、HTML 制作以及其他应用程序。有很多，所以请确保记住你给他们的邮箱，并在程序弹出注册框时输入密钥。如果你真的需要 Applicware，可以从 http://www.download.com 下载（你真的想要吗？我不知道，因为没有提供免费版。[抱歉，我必须说句：为什么版权律师要留着这些完美的软件？]

# 7.4 AbiWord

AbiWord (http://www.abisource.com/) 是一个很好的轻量级文字处理器。对于简单的文字处理非常值得尝试。虽然还不完整，但对我很有用，例如支持不需要 WordPerfect 的拼写检查。

# 7.5 表格软件

除了上述的表格应用程序（StarOffice 和 Applicware），你可能还想看看 "xess"：http://www.ais.com/linux_corner.html。他们还有一个稍微缩小的 "xessile"，可以从他们的网站下载。我们喜欢 xess 的整体设计（简单且几乎自自明）。它在工程应用方面似乎很强大，在我们看来，它可能是目前 Linux 上最好的表格软件。

你可能想关注“Gnumeric”（包含在你的 RH6.0 发行版中，属于 Gnome 项目）。它仍然相对不完整，但已经可用。它正在密集开发中，在不久未来非常有变得非常棒的潜力——它已经有很多内置功能，但打印功能不可靠。如果你安装了它，可以通过 X-windows 终端输入命令来启动：

```
gnumeric
```

或者

```
find / -name "gnumeric"
```

