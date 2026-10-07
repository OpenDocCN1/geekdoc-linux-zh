
你可以通过在命令行中指定来合并 RCS 文件的任意版本。例如，以下 `rcmerge` 命令合并了 `input.c` 的版本 1.2 和 3.2，并将合并后的版本存储在 `merged_input.c`。

```
$ rcmerge -r1.2 -r3.2 -p input.c > merged_input.c
RCS file: RCS/input.c,v
retrieving revision 1.2
retrieving revision 3.2
Merging differences between 1.2 and 3.2 into input.c;
result to stdout
$
```

你可以使用该命令撤销你当前检出的 `input.c` 版本中版本 1.2 和 2.1 之间的更改。注意版本的顺序（较后的版本在前）。

```
$ rcmerge -r2.1 -r1.2 input.c
RCS file: RCS/input.c,v
retrieving revision 2.1
retrieving revision 1.2
Merging differences between 2.1 and 1.2 into input.c
$
```

在接下来的章内练习中，你将练习合并 RCS 文件的多个版本。

## 章内练习

20.13. 创建几个 `input.c` 文件的版本，并执行 `rcmerge` 命令将它们全部合并到 `merged_input.c` 文件中。

## 限制 RCS 文件的访问权限

只要用户对文件具有适当权限并可以访问文件的路径，任何用户都可以检出 RCS 文件。你可以通过使用 `rcs` 命令的 `-a` 和 `-e` 选项通过限制对一个或多个用户的访问来保护你的 RCS 文件。如 `rcs` 命令的简要描述所示，你可以使用 `-a` 选项将文件的检出权限赋予一个或多个用户。所有其他用户都允许检出该文件的只读副本。你可以使用 `-e` 选项从列表中删除一个或多个用户。命令行可以使用多个 `-a` 和 `-e` 选项。

## 程序生成工具

在接下来的节中，我们将演示这两个选项的用法。第一个 `rcs` 命令将用户 `matt`、`chang` 和 `mona` 添加到列表中，以便他们检出 `input.c` 文件的可编辑版本并提交；不允许其他用户执行这些任务。第二个 `rcs` 命令添加了用户 `davis`。最后一个 `rcs` 命令拒绝 `chang` 访问文件的用户列表（即 `input.c` 的编辑访问权限）。`rlog` 命令的输出显示当前的访问列表。

```
$ rcs -amatt,chang,mona input.c
RCS file: RCS/input.c,v
done
$ rcs -adavis input.c
RCS file: RCS/input.c,v
done
$ rlog -h RCS/input.c,v
RCS file: RCS/input.c,v
Working file: input.c
head: 2.1
branch:
locks: strict
access list:
matt
chang
mona
davis
symbolic names:
keyword substitution: k v
total revisions: 6
```

```
$ rcs -echang input.c
RCS file: RCS/input.c,v
done
$ rlog -h RCS/input.c,v
...
access list:
matt
```

## 程序生成工具 683

任何之前的软件发布版本，无论软件当前状态如何。你也可以查看特定日期的软件发布。

在本节中，我们将描述 CVS 的一些基本功能。你需要使用 CVS 工具来与 CVS 交互。该工具通过调用不同的命令来执行软件修订控制涉及的各种任务。虽然 CVS 拥有丰富的命令可以供你执行许多与版本控制相关的日常工作，但我们将重点关注实践中常用的基本命令。以下是这些命令的简要描述。

```
cvs [cvs-options] command [command-options-and-arguments]
```

用途：此命令允许你调用 CVS 功能来执行与软件版本控制相关的任务。

常用的选项/功能：

- `-H` [cvs-command] 显示 'cvs-command' 的用法信息；如果未指定 'cvs-command'，则显示 cvs 命令的简要描述
- `-d` CVS-root-dir 使用 'CVS-root-dir' 作为源仓库的绝对路径；覆盖环境变量 `CVSROOT` 的设置
- `-e` editor 使用 'editor' 输入修订日志信息；覆盖环境变量 `CVSEDITOR` 和 `EDITOR` 的设置；默认编辑器为 `vi`
- `-n` 尝试执行给定的 cvs-command 但不进行任何更改；仅发布报告
- `-t` 跟踪程序执行并显示执行 cvs-command 时发生的 cvs 活动序列；有助于理解 cvs 命令的语义

我们将在下文中讨论 cvs 命令中一些更常用的选项和命令。

## 684 第 20 章 用于软件开发的 Linux 工具

显示 CVS 帮助。你可以使用 `cvs -H` 命令显示 cvs 命令的简要描述。`cvs -H` 命令可用于显示每个 cvs 命令的用途。下面的会话显示了示例运行：

```
$ CVS -H
用法: cvs [cvs-options] command [command-options-and-arguments]
其中 cvs-options 为 -q, -n 等。
（指定 -help-options 获取选项列表）
其中 command 为 add, admin 等。
（指定 -help-commands 获取命令列表，
或指定 -help-synonyms 获取命令同义词列表）
其中 command-options-and-arguments 取决于特定命令
（指定 -H 后跟一个命令名以获取特定命令的帮助）
指定 --help 以接收此消息
```

```
$ CVS -H
CVS 命令有：
- add | 向仓库添加新文件/目录
- admin | rcs 的管理前端
- annotate | 显示每行都修改过的最后修订状态
- checkout | 检出源代码进行编辑
- commit | 将文件提交到仓库
- diff | 显示版本之间的差异
- edit | 准备编辑被监控的文件
- editors | 查看谁正在编辑被监控的文件
- export | 从 CVS 导出源代码，类似于 checkout
- history | 显示仓库访问历史记录
- import | 使用供应商分支将源代码导入 CVS
- init | 如果 CVS 仓库不存在，则创建一个 CVS 仓库
- log | 打印文件的历史信息
- login | 提示输入密码以验证服务器身份
- logout | 移除 .cvpass 中远程仓库的条目
- rdiff | 在发布之间创建 'patch' 格式的差异
- release | 表明某个模块不再使用
- remove | 从仓库中删除条目
- rtag | 为模块添加符号标记
- status | 显示检出文件的状态信息
- tag | 为已检出的文件版本添加符号标记
- unedit | 撤销编辑命令
- update | 使工作树与仓库保持同步
- watch | 设置监控
- watchers | 查看谁正在监控文件
```

你可以使用 `cvs -H` 命令并将命令名作为参数来获取任何 CVS 命令的帮助。在下面的会话中，我们显示了 `add` 和 `commit` 命令的帮助信息。

```
$ cvs -H add
用法: cvs add [-k rcs-kflag] [-m message] files...
-k 使用 "rcs-kflag" 添加带有指定 kflag 的文件。
-m 使用 "message" 作为创建日志。
（指定 --help 全局选项获取其他帮助选项列表）

$ cvs -H commit
用法: cvs commit [-nRlf] [-m message] -F logfile] [-r rev] files...
-n 不运行模块程序（如果有）。
-R 递归处理目录。
-l 仅限本地目录（不递归）。
-f 强制提交文件；禁用递归。
-F 从文件读取日志消息。
-m msg 日志消息。
-r rev 提交到此分支或主干版本。
（指定 --help 全局选项获取其他帮助选项列表）
$
```

## 686 第 20 章 用于软件开发的 Linux 工具

创建源仓库。由 CVS 维护在名为源仓库的目录源码包含目录的 RCS 历史 `.v` 文件，该目录称为 `CVSROOT`，其中包含管理文件。在执行简单的例行开发任务时，你不需要访问 `CVSROOT` 目录中的文件。在启动 CVS 之前，你需要设置源仓库的位置。你可以通过设置环境变量 `CVSROOT` 或使用 `cvs` 命令的 `-d` 选项来实现。

## 688 第 20 章 用于软件软件的 LINUX 工具

```
语法：
cvs import [options] repository vendor-tag release-tag
```

常用的选项 / 特性：

- `-b` branch 将供应商分支 ID 设置为 'branch'
- `-d` 使用文件的修改时间作为导入时间
- `-m` message 记录我们希望在历史文件中显示的消息 'message'

`cvs import` 命令用于将这些源码导入源码库。`-m` 选项用于向 CVS 提供一条消息，该消息将与历史文件一起显示。如果没有此选项，`cvs import` 命令将启动一个编辑器让你输入消息。所调用的编辑器名称从环境变量 `CVSEDITOR` 获取。如果未设置此变量，则从变量 `EDITOR` 获取编辑器名称。如果两个变量未设置，则调用 `vi` 编辑器。命令行参数 'project1' 是包含源文件的目录名称，参数 'DemoCVS' 是供应商标签。最后一个参数必须是 'start'。

```
$ cd CVSAREA/project1
$ ls
compute compute.h input.c input.h main.c main.h Makefile
$ cvs import -m "Imported Demo Sources" project1 DemoCVS start
N project1/compute.c
N project1/compute.h
N project1/input.c
N project1/input.h
N project1/main.c
N project1/main.h
```
