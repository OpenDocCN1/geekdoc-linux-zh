
```
man(1)  Manual pager utils  man(1)
```

# NAME
`man` an interface to the on-line reference manuals

# SYNOPSIS
`man [-c|-w|-tZTdevice] [-adhu7V] [-Msystem[,...]] [-Llocale] [-pstring] [-Mpath] [-Ppager] [-rprompt] [-Slist] [-eextension] [[section]page...]`

`man -l [-7] [-tZTdevice] [-pstring] [-Ppager] [-rprompt] file...`
`man -k [apropos options] regexp`
`man -f [whatis options] page ...`

# DESCRIPTION
`man` is the system's manual pager. Each page argument given to `man` is normally the name of a program, utility or function. The manual page associated with each of these arguments is then found and displayed. A section, if provided, will direct `man` to look only in that section of the manual. The default action is to search in all of the available sections, following a pre-defined order and to show only the first page found, even if page exists in several sections.

每个手册页的标题在左右两侧包含命令名称以及手册页所属的章节号。标题中央描述了该程序所属的程序类别。最后一行通常包含最后更改的日期。

手册页通常具有表 3-1 所示的若干部分或全部部分。

| 部分 | 内容 |
|---|---|
| 名称 | 命令的名称和简短描述 |
| 概要 | 语法描述 |
| 描述 | 命令的详细描述 |
| 选项 | 所有可用选项的描述 |
| 命令 | 程序运行期间可以给出的指令 |
| 文件 | 与命令以某种方式关联的文件 |
| 另请参阅 | 相关命令的提示 |
| 诊断 | 程序可能的错误信息 |
| 示例 | 调用命令的示例 |
| 已知问题 | 命令的已知错误和问题 |

表 3-1

`man` 程序使用 `less` 程序来显示手册页。在 `less` 中，文本的显示由表 3-2 所示的键控制。

| 键命令 | 描述 |
|---|---|
| Space | 向前翻一屏。 |
| b | 向后翻一屏。 |
| PageDown | 向前翻半屏。 |
| PageUp | 向后翻半屏。 |
| Down-arrow, Enter | 向前跳一行。 |
| Up-arrow | 向后跳一行。 |
| End | 转到手册页末尾。 |
| Home | 转到手册页开头。 |
| /expression | 从当前光标位置向前搜索 expression；匹配的行显示为屏幕上的第一行。 |
| ?expression | 从当前光标位置向后搜索 expression；匹配的行显示为屏幕上的第一行。 |
| n | 移至搜索中 expression 的下一个实例。 |
| N | 移至搜索中 expression 的上一个实例。 |
| q | 结束手册页的显示。 |

表 3-2

手册页按表 3-3 所示的部分组织。

| 部分 | 内容 |
|---|---|
| 1 | 可执行程序和 shell 命令（用户命令） |
| 2 | 系统调用 |
| 3 | 函数和库例程 |
| 4 | 设备文件 |
| 5 | 配置文件和文件格式 |
| 6 | 游戏 |
| 7 | 宏包和文件格式 |
| 8 | 系统管理命令 |

表 3-3

例如，输入以下内容可显示 `crontab` 命令的一般信息：

```
man 1 crontab
```

输入以下内容可显示 `crontab` 命令的配置文件信息：

```
man 5 crontab
```

当命令有多个手册页时，特别重要的是知道命令属于哪个部分。

例如，`uname` 命令既是用户命令也是系统调用。输入以下内容可显示有关用户命令的信息：

```
man 1 uname
```

输入以下内容可显示有关系统调用的信息（如名称和有关当前内核的信息）：

```
man 2 uname
```

你可以使用 `whatis` 命令显示命令或实用程序的所有可用手册页的简要描述（如以下所示）：

```
geek@dal10:~ > whatis uname
uname (1)  - print system information
uname (2)  - get name and information about
             current kernel
uname (1p) - return system name
uname (3p) - get the name of the current system
```

![](img/9129877170834ca9d5fdac5319bf5f12_94_0.png)

用 “p” 标记输出的手册页是 `uname` 命令（`uname (1p)`）和函数（`uname (3p)`）的 POSIX 手册页。POSIX（Portable Operating System Interface for Unix，Unix 可移植操作系统接口）由 IEEE 和 Open Group 为 UNIX 开发，作为应用程序与操作系统之间的标准化接口。

在 SUSE Linux Enterprise Server 中，手册页位于目录 `/usr/share/man/` 中。

如果输入 `man -k keyword` 或 `apropos keyword`，将显示在 NAME 部分出现该关键字的手册页列表。例如：

![](img/9129877170834ca9d5fdac5319bf5f12_94_1.png)

```text
gecko@a30:~> man -k printf
vsprintf (3) - print to allocated string
vwprintf (3p) - wide-character formatted output of a
standard argument list
vfprintf (3) - formatted output conversion
sprintf (3) - formatted output conversion
format (n) - format a string in the style of sprintf
swprintf (3) - formatted wide character output conversion
asprintf (3) - print to allocated string
vsprintf (3p) - format output of a stdarg argument list
printf (3p) - print formatted output
sprintf (3p) - formatted output
wprintf (3p) - print formatted wide-character output
vdprintf (3) - print to a file descriptor
fwprintf (3) - formatted wide character output conversion
sprintf (3) - formatted output conversion
dprintf (3) - print to a file descriptor
wdprintf (3) - formatted wide character output conversion
printf (3) - formatted output conversion
...
```

![](img/9129877170834ca9d5fdac5319bf5f12_94_2.png)

## 练习 3-1：访问和使用 man 手册页

在本练习中，使用 `whatis` 和 `man` 命令获取有关 `info` 命令的信息。在手册页中查找 `filename`。

### 完成此练习的详细步骤

- 1. 从 GNOME 桌面打开主菜单。
- 2. 选择 更多应用程序。
- 3. 在过滤器文本框中输入 `term`。
- 4. 选择 GNOME Terminal 图标以启动终端仿真。
- 5. 通过输入查找 `info` 命令手册页的各节
  - `whatis info`
