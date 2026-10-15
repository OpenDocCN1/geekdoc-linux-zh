
| 以 j 开头 | 跨平台 Java 应用 |
| 以 k 开头 | KDE 桌面应用、Linux 内核包或 Kerberos 安全包 |
| 以 py 开头 | Python 应用 |
| 以 rh 开头 | Red Hat 应用，通常用于配置你的系统 |
| 以 tk 开头 | 图形 Tcl 应用 |
| 以 x 开头 | X Window 系统图形应用 |
| 以 wm 结尾 | 用于控制屏幕窗口布局的窗口管理器 |

### 使用通配符查询

除了使用其他 Linux 命令外，`rpm` 命令还支持一些搜索选项。你可以向 `rpm -qa` 传递通配符（但不能只是 `rpm -q`，你需要 `-a` 来包含所有软件包）。例如：

```
$ rpm -qa "send*"
sendmail-cf-8.11.6-3
sendmail-8.11.6-3
```

> "`send*`" 周围的引号是为了防止 shell 扩展通配符字符 `*` 以尝试匹配本地目录中的文件名列表。通过将命令行参数作为 "`send*`" 传递，`rpm` 程序就能看到 `*` 字符。否则，shell 会扩展该参数，而在此情况下程序 `rpm` 永远看不到 `*`。

此命令搜索所有以 `send` 开头的包名。你可以使用感叹号来反转这一操作。例如：

```
$ rpm -qa '!send*'
```

![](img/9d29d6681c5f42792ea5da4b12142ca2_89_0.png)

此命令的作用类似于 `grep -v`，搜索所有不以 `*send` 开头的软件包。

还有许多其他 Linux 命令可以在管道中与 `rpm -qa` 命令配合使用，以过滤和显示数据，例如使用 `wc -l` 统计查询的软件包数量。你还可以使用其他查询选项从 RPM 数据库查找更专门的信息。

> 如果你不熟悉 `grep` 或其他 Linux 命令，可以阅读一些 Linux 教程，例如 Steve Oualine 和 Eric Foster-Johnson 编写的《Teach Yourself Linux》，由 Wiley Publishing, Inc. 出版。

### 查找哪些软件包拥有文件

软件包管理中的常见问题之一是当你想要跟踪系统上的某个特定文件，并追溯到“拥有”该文件的软件包（即安装时产生该文件的包）。

`-qf` 选项告诉 `rpm` 命令查询所有拥有特定文件的软件包。你也可以使用较长的选项 `--file` 来代替 `-f`。基本语法如下：

```
rpm -qf filename
```

例如，之前示例中使用的 `grep` 命令就是一个文件。（`-qf` 选项告诉 `rpm` 命令查询所有拥有特定文件的软件包。你也可以使用较长的选项 `--file` 来代替 `-f`。）基本语法如下：

```
rpm -qf filename
```

shell。Tcsh 是一种命令语言解释器，既可以作为交互式登录 shell，也可以作为 shell 脚本命令处理器。Tcsh 包含命令行编辑器、可编程的单词补全、拼写检查、历史机制、作业控制以及类似 C 语言的语法。

从这些描述中，你可以了解到许多关于软件包的信息，例如它来自哪里。注意描述中还列出了构建软件包程序时使用的源 RPM。

![](img/9d29d6681c5f42792ea5da4b12142ca2_93_0.png)

本章后续关于自定义查询的章节将展示你如何查询存储在包头中的任何信息，包括 `rpm -qi` 命令显示的所有信息以及任何其他包头标签。

## 软件包组 (Package groups)

RPM 软件包被分为组，这仅仅是一组软件包的任意名称。之前显示的 `rpm -qi` 命令会列出软件包所在的组（如果有的话）。对于上一个示例中的 tcsh 软件包，该包属于 SystemEnvironment/Shells。

`rpm -q` 命令的 `-q` 告诉 `rpm` 命令列出给定组中的所有软件包。你也可以使用较长的选项 `--group` 来代替 `-g`。基本语法如下：

```
rpm -qq group_name
```

例如：

```bash
# rpm -q "System Environment/Shells*"
bash-2.05b-5
sh-utils-2.0.12-3
ash-0.3.8-5
tcsh-6.12-2
```

![](img/9d29d6681c5f42792ea5da4b12142ca2_93_1.png)

该组的名称中包含空格，因此你需要用引号将组名作为一个参数传递给 `rpm` 命令。

# 第 5 章：使用 RPM 数据库

### 软件包中的列出文件 (l) 选项

`-l` (ell) 选项查询软件包中的所有文件。你也可以使用较长的选项 `--list` 来代替 `-l`。基本语法是：

```bash
rpm -ql package
```

例如，查询 tcsh 软件包中的文件，你将看到以下内容：

```bash
# rpm -ql tcsh
/bin/tcsh
/bin/tcsh
/usr/share/doc/tcsh-6.10
/usr/share/doc/tcsh-6.10/FAQ
/usr/share/doc/tcsh-6.10/Fixes
/usr/share/doc/tcsh-6.10/NewThings
/usr/share/doc/tcsh-6.10/complete.tcsh
/usr/share/doc/tcsh-6.10/eight-bit.txt
/usr/share/doc/tcsh-6.10/tcsh/header.html
/usr/share/doc/tcsh-6.10/tcsh/index.html
/usr/share/doc/tcsh-6.10/tcsh/lists.html
/usr/share/doc/tcsh-6.10/tcsh.man
/usr/share/doc/tcsh-6.10/tcsh.man2html
/usr/share/doc/tcsh-6.10/tcsh/top.html
/usr/share/local/de/LC_MESSAGES/tcsh
/usr/share/local/el/LC_MESSAGES/tcsh
/usr/share/local/fr/LC_MESSAGES/tcsh
/usr/share/local/it/LC_MESSAGES/tcsh
/usr/share/local/ja/LC_MESSAGES/tcsh
/usr/share/man/man1/tcsh.gz
```

![](img/9d29d6681c5f42792ea5da4b12142ca2_94_0.png)

你可以此选项传递多个软件包名称，但它不会告诉你哪个文件属于哪个包。使用 `--files` 选项按包列出文件（参见相关侧边栏）。`-v` (verbose) 选项在与其他查询选项配合使用时可以提供文件的更多信息。例如：
