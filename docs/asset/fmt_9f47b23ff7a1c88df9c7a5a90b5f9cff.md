
castle% `ls -l core*`
```
-rw-rw-rw- 1 winsor staff 0 Jan 14 15:50 core.o
```
castle%

## 退出状态

```
0
```
非零    发生失败时，例如不存在的进程 ID。

## 文件

```
core.process-id
```
Core 映像。

## 属性

查看 `attributes(5)` 可获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNwtoo (32-bit)<br>SUNwtoox (64-bit) |

## 参见

```
kill(1), core(4), proc(4), attributes(5)
```

# `gencat` — 生成格式化消息目录

## 语法

`/usr/bin/gencat catfile msgfile...`

## 描述

使用 `gencat` 命令将消息文本源文件 `msgfile` 合并到格式化的消息数据库 `catfile` 中。如果数据库 `catfile` 不存在，则会创建它。如果 `catfile` 已经存在，其消息将包含在新的 `catfile` 中。如果设置了且消息编号冲突，则使用当前包含在 `catfile` 中的新消息文本定义新文本。你输入到 `gencat` 的消息文本源文件（或文件集）可以是设置了消息编号的，也可以仅是消息编号，在这种情况下假设使用默认消息集 `NL_SETD`（参见 `nl_types(5)`）。

# 消息文本源格式

消息文本源行的格式描述如下。

> 注意 — 消息文本源行的字段由单个 ASCII 空格或 Tab 制符分隔。任何其他 ASCII 空格或 Tab 制符都被视为后续字段的一部分。

`$set n comment`
指定一个集标识符，其中 `n` 指定直到下一个 `$set,$delset,$end-of-file` 之前的消息集标识符。`n` 必须是 (1–NL_SETMAX) 范围内的数字。单个源文件内的集标识符不需要连续。将集标识符后的任何字符串视为注释。如果你在消息文本源文件中没有指定 `$set` 指令，则在默认消息集 `NL_SETD` 中查找所有消息。

`$delset n comment`
从现有目录中删除消息集 `n`。将集编号后的任何字符串视为注释。（注意：如果 `n` 不是有效集，则被忽略。）

`$ comment`
将以美元符号开头后跟 ASCII 空格或 Tab 制符的行视为注释。

`$m message-text`
表示消息标识符，范围 (1–NL_MSGMAX) 范围内的数字。将 `message-text` 存储在由最后一个 `$set` 指令定义的集标识符和标识符 `m` 的消息目录中。如果 `message-text` 为空且存在 ASCII 空格或 Tab 分隔符，则在消息目录中存储空字符串。如果消息源行有消息编号但既没有字段分隔符也没有消息文本，则从目录中删除该编号的现有消息（如果有）。消息标识符不需要连续。

`$quote c` 指定一个可选的引号字符 `c`，可用于包围 `message-text`，以便消息源行中的尾随空格或空（空值）消息是可见的。默认情况下或如果你指定了 `$quote` 指令，则不识别 `message-text` 的引号。消息源文件中的空行会被忽略。文本字符串可以包含下方的特殊字符和转义序列。

| 描述 | 符号 | 序列 |
| --- | --- | --- |
| 新行 | NL (LF) | `\n` |
| 水平制表符 | HT | `\t` |
| 垂直制表符 | VT | `\v` |
| 退格 | BS | `\b` |
| 回车 | CR | `\r` |
| 分页符 | FF | `\f` |
| 反斜线 | `\` | `\\` |
| 位进制 | ddd | `\ddd` |

消息文本源行的格式如下描述。

`$` 文本源行的

使用 `gencat` 命令将消息文本源文件 `msgfile` 合并到格式化的消息数据库 `catfile` 中。如果数据库 `catfile` 不存在，则会创建它。如果 `catfile` 已经存在，其消息将包含在新的 `catfile` 中。如果设置了且消息编号冲突，则使用当前包含在 `catfile` 中的新消息文本定义新文本。你输入到 `gencat` 的消息文本源文件（或文件集）可以是设置了消息编号的，也可以仅是消息编号，在这种情况下假设使用默认消息集 `NL_SETD`（参见 `nl_types(5)`）。

# `genmsg` — 从源文件提取消息生成消息源文件

## 语法

```
/usr/bin/genmsg [-abdrnx] [-c message-tag] [-g project-file]
[-l project-file] [-m prefix] [-M suffix]
[-o message-file] [-p preprocessor] [-s set-tags] file ...
```

## 描述

`genmsg` 从源文件中提取调用 `catgets(3)` 的字符串，并以适用于 `gencat(1)` 的格式写入。

## 调用

`genmsg` 读取一个多个输入文件，默认生成名称为第一个输入文件名加上 `.msg` 后缀的消息源文件。如果你指定了 `-o` 选项，`genmsg` 使用选项参数作为输出文件。

| 命令 | 输出文件 |
| --- | --- |
| `genmsg prog.c` | main.c util.c tool.c |
| `genmsg -o prog.msg` | mail.c util.c |

`genmsg` 还允许你调用预处理器来解决宏和定义语句对 `catgets(3)` 的依赖。

# 消息自动编号

`genmsg` 根据项目文件将消息编号替换为 `-1`。它生成带有新消息编号的输入文件副本以及项目文件的副本。

项目文件是一个存储集编号及其最大消息编号的数据库。项目文件中的每行由集编号和它的最大消息编号组成：

```
```

在项目文件中，以数字符号 (`#`) 或 ASCII 空格开头的行被视为注释并忽略。`genmsg` 还具有反向操作可以将所有消息编号替换为 `-1`。

# 注释提取

`genmsg` 允许你对消息和集编号进行注释，以告知 `transl` 如何翻译消息。它从输入文件中提取由注释指示包围且内部包含指定标签的注释，并以美元符号 (`$`) 前缀写入输出文件。

# 测试

`genmsg` 生成两种类型的消息用于测试：

-   前缀消息允许你检查你的程序是否正在从消息目录中检索消息。
-   长消息允许你检查你的窗口程序的初始大小和位置。

## `genmsg`

### 423

#### Notes

`genmsg` 不处理 `catgets(3)` 调用中的指针或变量。
示例：
```c
const int set_num = 1;
extern int msg_num(const char *);
const char *msg = "Hello";
catgets(catd, set_num, msg_num(msg), msg);
```

当使用预处理器开启消息时，如果 `catgets(3)` 行中有多个 `-1`，`genmsg` 将该行中所有的 `-1` 替换为计算出的数字。例如，给定输入：
```c
#define MSG(id
```

# 命令产生的输出为

```c
#define MSG(id
```

解决方法是将输出分为以下两行：
```c
if (ret == -1)
printf("%s0)
```
