
使用 `-l` 标志会产生“长”格式列表，显示更多关于 `file1` 的信息。你以类似的方式列出目录（第二个示例显示了 `dir1` 是空的）：

```bash
ls -l
total 10
drwxr-xr-x 1 joe users 0 Oct 28 22:05 dir1
0
```

## 2.4.4 复制文件和目录

你可以使用 `cp` 命令复制文件。以下语句

```bash
cp file1 file2
```

将 `file1` 复制到 `file2`。复制文件夹或目录需要使用递归或 `-r` 标志，表示 `cp` 应该进入目录并复制所有子文件和子文件夹：

```bash
cp -r dir1 dir2
```

练习 2.4.4：现在现在创建一个这样的目录。清楚地解释以下示例与上述的不同：

```bash
cp file1 dir1
```

```bash
cp -r dir1 dir2/
```

```bash
cp -r dir1 dir2/dir3
```

## 2.4.5 移动文件和目录

移动文件就像重命名一样简单。这允许你将文件移动到另一个目录：

```bash
mv file2 file3
```

```bash
mv file1 dir1/file2
```

你移动目录的方式与移动文件完全相同：

```bash
mv dir1 dir3
```

## 2.4.6 更改目录

更改当前目录通过 `cd` 命令完成：

```bash
cd dir1
```

```bash
cd ..
```

## 2.4.7 删除文件和目录

普通文件使用 `rm` 命令删除：

```bash
rm file1
```

删除目录也通过 `rm` 命令完成，但同样你需要使用“递归”或 `-r` 标志：

```bash
rm -r dir1
```

## 2.5 输入输出、重定向和管道

I/O 指的是输入（I）和输出（O）。重定向允许你改变命令的输入和输出。

### 2.5.1 输入输出

I/O 指的是标准输入（`stdin`）和标准输出（`stdout`）。重定向允许你改变命令的输入和输出。在 UNIX 中重定向到标准输入（`stdin`）、标准输出（`stdout`）和标准错误（`stderr`）。

| 名称 | 缩写 | 描述符 |
| --- | --- | --- |
| 标准输入 | `stdin` | 0 |
| 标准输出 | `stdout` | 1 |
| 标准错误 | `stderr` | 2 |

### 2.5.2 重定向

重定向允许你将命令的输出重定向到文件。使用 `>` 符号可以将输出重定向到文件：

```bash
ls > file.txt
```

使用 `>>` 符号可以将输出追加到文件：

```bash
ls >> file.txt
```

使用 `2>` 符号可以将标准错误重定向到文件：

```bash
ls 2> error.txt
```

使用 `&>` 符号可以同时将标准输出和标准错误重定向到文件：

```bash
ls &> output.txt
```

你可以使用 `<` 符号将输入重定向，即从文件读取命令的输入：

```bash
cat < file.txt
```

你还可以将输出或错误重定向到特殊设备，例如 `/dev/null`，这通常用于丢弃输出：

```bash
ls > /dev/null 2>&
```

### 2.5.3 管道

管道允许将一个命令的输出作为另一个命令的输入。使用 `|` 符号来连接命令：

```bash
ls | sort
```

## 2.6. 命令行编辑

这向我们展示了可能性，并再次返回以便我们可以继续输入命令。请记住，`tcsh` 具有与 `bash` 相同的自动补全机制。只需使用 `<Ctrl-D>` 即可。

### 2.6.3 命令行替换与历史

在 `tcsh` 和 `bash` 中，我们都拥有命令行替换（Command Line Substitution）和命令历史（Command History）功能。命令行替换允许你在命令内部替换动态表达式——

```bash
<bash>: echo My name is $USER
My name is Joe
<bash>:
```

`$` 符号允许 `bash` 在行内处理表达式，稍后将结果提供给 `echo` 命令。命令历史允许你在当前命令中使用旧命令中的内容。记住：循环利用对环境是有益的。以下列表显示了 `bash` 和 `tcsh` 的历史引用语法：

- `!!`
- `!` 重复执行上一个命令。等同于 `-1`
- `!N` 重复最近的第 N 次命令（见下文）
- `!3` 重复最近的第 3 次命令
- `!N` 重复历史列表中的第 N 条
- `!string` 重复以字符串 "string" 开头的上一个命令
- `!string?` 包含文本 "string" 的最新命令

图 2.3: 历史引用规范

在历史引用的基础上，你可以通过在历史引用冒号（:）之后追加以下内容添加到 shell 命令行中：

- `0` 第一个（命令）单词
- `n` 命令旁边的第 n 个单词
- `-` 第一个单词，等同于 '1'
- `$` 最后一个单词
- `%` 由 ?s? 搜索匹配的单词
- `x-y` 单词范围。'-y' 是 '0-y' 的缩写
- `*` 等同于 '$-',但如果事件只包含 1 个单词，则返回空
- `x*` 等同于 '*'
- `x-` 等同于 '*'，但省略最后一个单词 ('$')

图 2.4: 历史修饰符

### 2.6.4 练习

你可以通过输入 `history` 获取你的历史列表。创建两个名为 `boogie.man` 和 `boogie.man.old` 的文件。文件内容对于本次练习并不重要。尝试上述历史机制的示例。具体的历史将根据你的操作而有所不同，请根据你的当前情况进行调整：

```bash
<bash>: history | tail -4
  9 8:30 touch boogie.man
  10 8:31 cp boogie.man boogie.man.old
  11 8:36 echo hello >> boogie.man
  12 8:37 diff boogie.man.old boogie.man
```

```bash
<bash>!-2
vi boogie.man
```

```bash
<bash>:diff !2-2:old !2-2
diff boogie.man.old boogie.man
```

```bash
<bash>:diff !!1.old !!2
diff boogie.man.old boogie.man
diff: boogie.man.old.old: No such file or directory
```

```bash
<bash>:!?cat?:0 !!2
cat boogie.man
```

# 第 3 章

## Linux 环境

在 Linux 和 UNIX 中，你携带许多本地属性，这些属性控制着你的直接 shell 界面如何与系统交互。这些属性被称为 Shell 变量和环境变量，对 Linux 的运行至关重要。UNIX 和 Linux 使用许多变量进行内部处理。这些变量帮助系统管理用户资源。本章将讨论所有 Linux 生存者需要知道的基础知识。

## 3.1 UNIX Shell 游戏

UNIX 的一个显著特征是，你可以控制与其通信的界面。这些接口被称为 shells，而原始的 shell 是 `sh`，它有许多兄弟版本，包括 `ash`。

许多用户倾向于使用伯克利 C 类型的 shell，如 `csh` 和 `tcsh`。然而，你的选择很大程度上取决于喜好，但我们将使用 `bash`。

## 3.2 Bash

`Bash` 是默认 shell。注意 `set` 提供了 `PS1` 以及其他变量。输入以下命令获取输出：

```
PRINTER=astro
PS1=$s
PWD=/home/joe
SHELL=/bin/bash
SHLVL=2
```

### 3.2.1 设置提示符

在交互式执行时，`bash` 在准备读取命令时显示主提示符 `PS1`，在需要输入时显示次提示符 `PS2`。

`\t` 当前时间，HH:MM:SS

`d` “星期 日期”格式日期

`w` shell 的名称，`$0` 的基名

`w` 当前工作目录

`W` 当前目录的基名

`u` 当前用户的用户名

`h` 主机名

# 命令的编号

`!` 该命令的历史编号

`$` 如果有效 UID 为 0，a, #

让我们通过添加命令编号更改 `bash` 提示符。这是一个示例：

```bash
bash PS1=' \s \u \t# \#: '
```

应该产生类似的结果

```
bash joe 00:02:07#: 13:
```

现在设置你的提示符，使其始终显示你的路径。尽管本手册将指定 `<bash>`，你仍应使用如下提示符：

```bash
bash PS1='<w> '
```

### 创建别名

现在，由于每次查看详细目录列表都要输入 `ls -Agl` 非常累，所以我想将命令 `d`（代表“directory”）别命名如下：

```bash
bash alias d='ls -Agl'
```
