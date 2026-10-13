
| linuxbase.org | www.linuxbase.org |

| urpmi | www.linuxbase.org/urpmi |

| urpmi | www.linuxbase.org/urpmi |

| linuxbase.org | www.linuxbase.org |

| setup.sh | www.linuxbase.org/setup.sh |

| linuxbase.org | www.linuxbase.org |

| urpmi | www.linuxbase.org/urpmi |

| urpmi | www.linuxbase.org/urpmi |

| linuxbase.org | www.linuxbase.org |

| setup.sh | www.linuxbase.org/setup.sh |

| linuxbase.org | www.linuxbase.org |

| urpmi | www.linuxbase.org/urpmi |

| urpmi | www.linuxbase.org/urpmi |

| linuxbase.org | www.linuxbase.org |

## 编程站点

存在大量的工具可以帮助你操作 RPM。以下站点列出了一些主要工具：

- 对于 `vim` 文本编辑器，你可以从 http://pegasus.rutgers.edu/~elfjord/vim/syntax/spec.vim 下载 `spec.vim` 语法文件。

- 对于 `emacs`，你可以从 http://tihilde.org/~stig/rpm-spec-mode.el 下载用于 spec 文件的 Emacs 模式。

![](img/9d29d6681c5f42792ea5da4b12142ca2_502_0.png)

附录 F 列出了许多文本编辑器的链接。

- 第 13 章中提到的 `rpmlint` 工具可以在 http://people.mandrakesoft.com/~flepied/projects/rpmlint 获取。

表 E-3 列出了许多与 RPM 相关的工具以及你可以查找这些工具更多信息的站点。

## 与 RPM 的站点

文件系统标准（FHS）涵盖了目录和格式。详情请见 `linuxbase.org`。

## 访问邮件列表和新闻组

RPM 邮件列表提供了技术信息的最佳来源。你可以在那里提问并获得用的回复。为了避免垃圾邮件（换句话说），你需要注册用户名和密码来订阅列表。名为 `redhat.rpm` 的新闻组提供了一个提问论坛。你可以使用任何新闻阅读程序阅读新闻组。

## 附录 F

## 文本编辑器和开发工具

本附录包含

- 通用文本编辑器

- C 特定工具和集成环境

- Python 特定开发工具

Linux 包含了许多编辑器和集成开发环境（IDE），从老旧文本编辑器到复杂的工具。这些工具适用于脚本编写、C 语言和 Python 编程，并且 Linux 发行版包含了各种设置的编辑器。

你可能没有安装这些编辑器中的任何一个，但它们都是 Linux 的一部分。你可以从你的 Linux 发行版包中安装 `vi`、`emacs`、`gedit` 或 `kato`。

注意互联网站点可能会变化或消失，因此你可能需要搜索这些工具。

## 第五部分：附录

要启动一个编辑器，请输入如下命令：

```
$ gedit listrmpkgs &
```

符号 `&` 会在后台启动程序。将 `gedit` 替换为你选择的编辑器。

## 编程文本编辑器

![](img/9d29d6681c5f42792ea5da4b12142ca2_507_0.png)

从 www.jedit.org 下载 edit。从 Sun (http://java.sun.com/j2se/downloads.html) 或 IBM (www.ibm.com/java/jdk/) 下载 jedit 的 Java 运行时环境，并选择适用于 Linux 的 IBM 开发工具包。

## C 语言编程的集成开发环境

如果你想要更多的图形化环境，Red Hat Linux 自带了 `KDevelop`，这是一个用于 C 和 C++ 编程的 IDE。`Ajuta` 提供了一个基于 GK/GNOME 的 IDE，作为基于 KDE 的 KDevelop 的替代方案。然而，KDevelop 支持 KDE、GNOME、Qt 以及文本模式的 C 和 C++ 应用程序。

![](img/9d29d6681c5f42792ea5da4b12142ca2_507_1.png)

从 www.anjuta.org 下载 Ajuta。

## 附录 F：Linux 文本编辑器和开发工具

`Eclipse` IDE 主要用于 Java 开发，但它有一个名为 `CDT`（C/C++ 开发工具）的模式。Eclipse 之所以非常重要，是因为 Red Hat 为 Eclipse 提供了一个构建 RPM 的插件。

![](img/9d29d6681c5f42792ea5da4b12142ca2_508_0.png)

从 www.ajanta.org 下载 Ajanta。从 www.eclipse.org 下载 Eclipse，从 www.eclipse.org/tools/downloads.html 下载 Eclipse CDT。

## Python 编程的集成开发环境

与 C 程序一样，Python 脚本由包含 Python 命令的文本文件组成，因此你需要一个文本编辑器或某种开发环境来创建 Python 程序。之前列出的任何工具都能很好地用于 Python 应用程序。关键要求是控制制表符（tabs）和缩进的能力，因为这对 Python 语法至关重要。

`IDLE` 是一个图形化控制台和编辑器，支持创建 Python 应用。它被认为是 Python 的一部分。`IDLE` 需要 `python-tools` 包。

此外，你还可以从专注于 Python 的工具中选择，例如重构工具 Bicycle Repair Man，或者两个 Python IDE Boa Constructor 和 Black Adder。

![](img/9d29d6681c5f42792ea5da4b12142ca2_508_1.png)

> Boa Constructor 可以从 http://boa-constructor.sourceforge.net 获取。Black Adder 是可以在 www.thekomany.com 获取的商业工具。

之前提到的 Eclipse IDE 支持许多 Python 插件。结合 C 和 C++ 工具以及构建 RPM 的插件，Eclipse 汇集了 Linux 上进行 Python 开发所需的所有工具。

![](img/9d29d6681c5f42792ea5da4b12142ca2_508_2.png)

Eclipse 可以在 www.eclipse.org 获取，Python 插件可从 http://sourceforge.net/projects/pyeclipse、http://sourceforge.net/projects/pe4eclipse 或 http://www.kalab.com/freeware/pythoneclipse/pythoneclipse.htm 获取。

## 第五部分：附录

对于 Python 工具来说，这只是冰山一角。你可以在互联网上找到更多工具。

![](img/9d29d6681c5f42792ea5da4b12142ca2_509_0.png)

大量的 Python 编辑器列表列于 http://www.python.org/cgi-bin/mo1nmo/PythonEditors。

## 附录 G

## RPM 许可

当将他人的现有代码整合到你的软件项目时，你应该始终仔细检查代码的许可，确保你理解其含义，并确保你愿意遵守这些规定。你还需要确保你有法律权利将其他代码整合到你的项目中。这对于商业代码和商业项目是如此，对于免费许可代码和自由软件项目同样如此。

RPM 本身以及大多数讨论过的辅助程序（`rpmlint`、`rpm-spec-mode` 等）都是自由软件，这意味着程序本身是免费提供的。此外，这些工具的大多数被视为开源软件，这意味着应用程序的源代码也是可用的。

这些事实并不意味着它们没有许可，或者它们的源代码可以以任何想要的方式使用。RPM 和这些辅助程序根据 GNU 通用公共许可证 (`GPL`) 的条款，以源码和二进制格式免费提供。`GPL` 的条款在此处复制，在将任何受 `GPL` 许可的源代码或二进制文件整合到你的项目之前，应当咨询这些条款。基本上，`GPL` 规定，你可以出于任何目的使用 `GPL` 许可的源代码或二进制文件，只要你始终向任何接收基于 `GPL` 许可源码的派生软件的用户提供相同的权利（包括访问你程序源代码的权利，尽管应该咨询律师以获得 `GPL` 对你项目影响的分析，但你应该自行决定使用 `GPL` 许可）。

# GNU 通用公共许可证

第 2 版，1991 年 6 月

版权 (C) 1989-1991 Free Software Foundation, Inc.

675 Mass Ave, Cambridge, MA 02139
