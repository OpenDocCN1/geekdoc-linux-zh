
### 命令参考

以下命令用于处理文本。

## sed

`sed` 的标准选项所示：

| | |
|---|---|
| `-n` | 防止显示模式空间（pattern space） |
| `-e filename` | 执行文件 `filename` 中包含的脚本 |
| `-V` | 显示版本号 |

## awk

`awk` 的标准 POSIX 选项所示：

| | |
|---|---|
| `-f filename` | `filename` 是要处理的 `awk` 文件名 |
| `-F field` | `field` 是字段分隔符 |
| `-v x=y` | `x` 是变量，`y` 是值 |
| `-W lint` | `lint` 检查 |
| `-W lint-old` | 使用旧式 `lint` 检查 |
| `-W traditional` | 强制传统用法 |
| `-W version` | 显示版本号 |

### 总结

在本章中，我们检查了基础文本编辑和命令行处理，以及更高级的文本处理工具如 `sed` 和 `awk`。作为 `PERL` 的前身，`sed` 和 `awk` 被广泛用于 shell 脚本（见下一章）以执行模式分析和匹配。

## 第 7 章：Shell、脚本与调度

图形用户界面（GUI）变得越来越流行，但命令行界面（CLI）仍然是与操作系统交互的核心特性。`shell` 是一个作为用户和内核之间接口的程序。它解释用户输入的命令并执行它们。

### 核心概念

`shell` 提供了一个可以运行程序和编写脚本的环境。脚本是一个包含 `shell` 执行的命令的文件。脚本用于自动化重复任务并执行复杂操作。

## Shell

有很多 `shell` 可，如 `bash`、`csh`、`zsh` 和 `sh`。每个 `shell` 自己的语法和特性，但它们共享许多功能。`bash` `shell` 是大多数 Linux 发行版的默认 `shell`。你可以通过 `chsh` 命令更改你的默认 `shell`。

## 环境变量

环境变量是影响许多进程的变量。例如，`PATH` 变量决定了 `shell` 搜索执行文件的目录。你可以使用 `export` 和 `unset` 命令设置和修改环境变量。

## 调度

调度允许你在特定时间自动运行任务。为此最常用的工具是 `cron`。你可以使用 `crontab` 命令创建 `cron` 作业。

表 7-1 不同提示符下的环境变量设置

| 设置 | 说明 | 输出 |
|---|---|---|
| `\a` | ASCII 响铃字符 | "beep" |
| `\d` | 日期字符串 | Sep 6 |
| `\h` | 短主机名 | www |
| `\H` | 完整主机名 | www.example.com |
| `\s` | Shell 名称 | bash |
| `\t` | 当前时间（12小时制） | 10:53:44 |
| `\T` | 当前时间（24小时制） | 10:53:55 |
| `\@` | 当前时间（A.M./P.M. 格式） | 10:54 A.M. |
| `\u` | 用户名 | Root |
| `\v` | Shell 版本 | 2.05 |
| `\W` | 带修订版本的 Shell 版本 | 20.5.0 |
| `\!` | 命令历史数 | 223 |
| `\$` | 权限标识 | # |
| `\u:\$` | 用户名、命令历史数和权限标识 | root:173:# |

假设你正在使用终端窗口执行命令，那么 `admintool` 窗口将出现在桌面上。一旦 `shell` 在“前台”执行命令（如 `admintool`），就无法执行其他命令。然而，通过将命令进程发送到“后台”，你可以在 `shell` 中执行多个命令。你可以通过在命令行末尾添加 `ampersand`（`&`）立即将进程发送到后台：

```bash
oracle@db:/usr/sbin ./admintool &
```

一旦命令执行，你可以通过按下 `CTRL-Z` 将其挂起，然后使用 `bg` 命令将其发送到后台：

```bash
oracle@db:/usr/sbin /admintool
^Z[1] + Stopped (SIGTSTP) admintool
oracle@db:/usr/sbin bg
[1] admintool&
oracle@db:/usr/sbin
```

应用程序名称将与作业号一起显示

你可以使用以下命令将应用程序带回前台：

```
oracle@db:/usr/sbin> fg
admintool
```

这默认会将第 1 号任务带回前台。然而，如果你有多个挂起的任务，则需要使用 `fg` 命令指定一个任务号：

```
oracle@db:/usr/local/bin/ . /netscape
^Z[2] + Stopped (SIGTSTP) netscape
oracle@db:/usr/sbin> bg
[2] netscape&
oracle@db:/usr/sbin> fg
netscape
```

你可以通过输入以下命令来获取当前 `shell` 中所有运行任务的列表：

```
$ jobs
[2] + Running ./netscape&
[1] - Running admintool&
```

### 步骤

以下步骤是理解 `shell` 以及如何对操作进行脚本化和调度的必要知识。

## 编写 Shell 脚本

Shell 脚本是 `shell` 和用户命令的组合，以非交互模式执行，用于广泛的目的。无论你是需要一个转换一组文件名扩展名的脚本、一个通过电子邮件向系统管理员磁盘空间不足的脚本，还是一个执行其他功能的脚本，你都可以使用 `shell` 脚本。你放置在 `shell` 脚本内部的命令通常也可以在交互式 `shell` 模式下执行，这使得在普通登录 `shell` 中拆分大型脚本并按行调试变得容易。在本节中，我们只检查在 `bash` 下运行的脚本——尽管许多脚本可以在不修改的情况下使用其他 `shell` 运行，但在尝试在另一个 `shell` 中运行脚本之前，最好检查你所选 `shell` 的语法。

## 处理 Shell 参数

编写 `shell` 脚本的一个常见目标是让它们尽可能通用，以便你可以将其用于各种输入。通常，`shell` 脚本可以利用命令行参数，这些参数是按数字排序的参数，可以在 `shell` 脚本内部访问。例如，一个将文件从一台计算机移动到另一台计算机的 `shell` 脚本可能需要源主机、目标主机以及要移动的文件名。显然，你想将这些参数传递给脚本，而不是将它们硬编码在代码中。这是 `shell` 脚本（如 `PERL` 程序）优于 C 等编译语言的优势之一：脚本很容易修改，且其执行对用户是完全透明的。

`shell` 脚本的参数可以通过单一方案识别——即带有参数 `$0` 执行的命令，第一个参数识别为 `$1`，第二个参数识别为 `$2`，以此此类推，最多有九个参数。因此，使用这些参数执行的脚本

```
$ display_hardware.sh cdrom scsi ide
```

会将 `cdrom` 指向 `$1`，将 `scsi` 指向 `$2`，将 `ide` 指向 `$3`。
让我们看看如何在脚本内部有效使用参数来处理输入参数。第一个脚本简单地计算文件的行数（使用 `wc` 命令），该文件由单个命令行参数 (`$1`) 指定。首先，创建一个空脚本文件：

```
$ touch count_lines.sh
```

接下来，设置文件权限为可执行：

```
$ chmod +x count_lines.sh
```

接下来，编辑该文件

```bash
$ vi count_lines.sh
```

并添加适当的代码：

```bash
#!/bin/bash
echo "Number of lines in file \$1"
wc -l $1
```

脚本获取第一个命令行参数，打印行数，然后退出。使用命令运行脚本：

```
$ ./count_lines.sh /etc/group
```
