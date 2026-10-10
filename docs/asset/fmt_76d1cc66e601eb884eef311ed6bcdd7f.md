
尝试实践项目 8–8 在后台运行程序。

## 监控进程

监控正在运行的进程非常有价值，因为你可以识别哪些进程是活跃的，并判断是否有任何想要停止的进程，例如在后台运行的进程或与你不再使用的程序相关的进程。在另一种情况下，你可能会启动一个运行长时间的程序，例如处理海量数据的统计程序。启动程序后，你可能会改变主意，并停止程序以便重新重置计算参数。
`ps` 命令显示当前正在运行的进程列表。当你不带选项使用该命令时，它显示与当前登录会话相关的进程列表。当你使用 `-A` 或 `-e` 选项时，它会显示系统上所有运行进程的详细列表，如图 8–4 所示。

### `ps [-options]` 语法

### 详解

- 提供当前运行进程的列表
- 有用的选项包括：
  - `-A` 或 `-e` 显示系统当前运行的所有进程
  - `-C commandname` 根据指定的命令名选择的进程
  - `-p PID` 根据指定的 PID 选择的进程
  - `-l PID` 显示进程信息的详细列表
  - `1 PID`（无连字符）显示进程信息的详细列出，且其显示类别与 `-l` 选项略有不同
  - `1 PID`（无连字符）显示进程信息的详细列出，且其显示类别与 `-l` 选项略有不同

## 管理进程 413

实践项目 9 显示如何使用 `ps`。
图 8-4 查看所有进程

## 杀死进程

如果你是具有 root 权限的管理员，你可能发现需要杀死运行故障或消耗过多资源的进程。如果你经常使用某个文件，你可能会为它创建一个备份副本以保存。稍后你想查看自创建备份副本以来原始文件是否发生了变化。你可以使用 `cmp` 工具比较两个文件的内容，如果存在差异，命令将报告文件开始不同的位置。例如，如果你比较 `filea`，它包含行内容：
This is one file.
to `fileb`，它包含以下内容：
This is a different file.
PID 或进程名。
语法 `kill [PID]` 或 `kill [processname]`

### 详解

- 杀死进程
- 使用 `[signal]`

实践项目 10 允许你使用 `kill` 命令。

## 检查文档的拼写

如果你在 UNIX/Linux 中创建许多文档，知道如何检查拼写是有价值的。例如，你可能会经常创建电子邮件、附件（如 readme 文件）或论文。你可以使用 `ispell` 检查拼写。
语法 `ispell [-options] filenames*`

### 详解

- 检查一个或多个文件的单词拼写并建议更改
- 有用的选项包括：
  - `-b` 创建原始文件的备份 `(.bak)`
  - `-S` 按建议概率从高到低排序
`ispell` 工具扫描文档，在屏幕上显示错误，并建议其他单词。屏幕底部出现的菜单显示修正选项和退出代码。（见图 8–5。）
在实践项目 8–11 中，你对文档使用 `ispell`。

```
mpramer@localhost:~

File Edit View Terminal Help

Characters form words.

Word documents.

File consist of words.

Words form lines.

Characters form words.

1) Files 6) Files

2) Fl-es 7) Floes

3) Files 8) BFiles

4) Fleas 9) Flees

5) Flees 10) Flees

6) Ignore 11) Impore all

7) Replace 12) Replace all

8) Add 13) Add Lower

9) Abort 14) Exit
```

图 8-5 使用 `ispell` 检查文档拼写

## 比较文件

假设你有一个经常使用的文件。你可能会为它创建一个备份副本以保存。稍后你想查看自创建备份副本以来原始文件是否发生了变化。你可以使用 `cmp` 工具比较两个文件的内容，如果存在差异，命令将报告文件开始不同的位置。
语法 `cmp [-options] file1 file2`

### 详解

- 比较两个文件并指示它们是否不同
当你比较两个文件时，如果内容相同，则没有输出。如果内容不相同，你会看到一条消息，指明文件之间第一个不同的字节（字符）。例如，如果你比较 `filea`，它包含行：
This is one file.
to `fileb`，它包含以下内容：
This is a different file.
命令 `cmp filea fileb` 的结果是

```
filea fileb differ: byte 9, line 1
```
