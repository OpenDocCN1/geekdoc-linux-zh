
除了空格以外的字符经常充当字段分隔符。例如，`/etc/passwd`文件包含存储在冒号分隔字段中的用户信息。你可以使用 `-t` 选项指定备用字段分隔符。在下面的示例中，我根据由冒号分隔的字段对文件进行了排序。

# 118 第 4 章 • 针对高级用户的 GNU 工具

更改有三种类型：添加行（a）、修改行（c）和删除行（d）。图 4–10 显示了 `diff` 用于描述每种编辑的格式，其中第一个 `firstStart` 和 `firstStop` 表示第一个文件中的行号，而第二个 `secondStart` 和 `secondStop` 表示第二个文件中的行号。

### 添加行

`firstStart a secondStart, secondStop`

> 从第二个文件要添加到第一个文件中的行

### 删除行

`firstStart, firstStop d lineCount`

< 从第一个文件中删除的行

### 修改行

`firstStart, firstStop e secondStart, secondStop`

< 第一个文件中将被替换的行

--

> 第二个文件中用于替换的行

**图 4–10** `diff` 输出结果的含义。

在接下来的示例中，我比较了几个文本文件以观察它们的差异：

```
$ cat lady1 ...look at the first test file.
Lady of the night,
I hold you close to me,
And all those loving words you say are right.
$ cat lady2 ...look at the second test file.
Lady of the night,
I hold you close to me,
And everything you say to me is right.
$ cat lady3 ...look at the third test file.
Lady of the night,
I hold you close to me,
And everything you say to me is right.
It makes me feel,
I'm so in love with you.
Even in the dark I see your light.
$ cat lady4 ...look at the fourth test file.
Lady of the night,
I'm so in love with you.
Even in the dark I see your light.
$ diff lady1 lady2 ...compare lady1 and lady2.
3c3
```

< And all those loving words you say are right.

--

> And everything you say to me is right.

```
$ diff lady2 lady3 ...compare lady2 and lady3.
3a,6
```

> It makes feel,

> I'm so in love with you.

> Even in the dark I see your light.

```
$ diff lady3 lady4 ...compare lady3 and lady4.
2,4d1
```

< I hold you close to me,

< And everything you say to me is right.

< It makes me feel,

```
$
```

## 4.5 查找文件：find

`find` 工具的功能不仅仅是简单的定位命名文件；它还能对满足特定条件的文件集执行操作。例如，你可以使用 `find` 删除所有属于用户 `tim` 且在 3 天内未被修改过的文件。图 4–11 给出了正式描述。

工具：`find` `pathList` `expression`

`find` 工具会递归地遍历 `pathList` 并对每个文件应用 `expression`。`expression` 的语法见下文，并附带了一些 `find` 的示例。

**图 4–11** `find` 命令的描述。

| 表达式 (Expression) | 值/动作 |
|---|---|
| `-name pattern` | 如果文件名匹配 `pattern` 则为真，`pattern` 可能包含 shell 元字符 `*`、`[ ]` 和 `?`。 |
| `-perm oct` | 如果文件权限标志的八进制描述完全等于 `oct`，则为真。 |
| `-type ch` | 如果文件类型为 `ch`（b = 块，c = 字符，等），则为真。 |
| `-user userId` | 如果文件的所有者为 `userId`，则为真。 |
| `-group groupId` | 如果文件的组为 `groupId`，则为真。 |
| `-atime count` | 如果文件在 `count` 天内被访问过，则为真。 |

**图 4–12** `find` 表达式。（部分 1/2）

| 表达式 (Expression) | 值/动作 |
|---|---|
| `-mtime count` | 如果文件内容在 `count` 天内被修改过，则为真。 |
| `-ctime count` | 如果文件内容在 `count` 天内被修改，或者其任何属性被更改，则为真。 |
| `-exec command` | 如果执行命令的退出码为 0 则为真，命令必须由转义的分号 (`\`) 结束。如果你指定 `{}` 为命令行参数，它将被替换为当前文件名。 |
| `-print` | 打印当前文件名并返回真。 |
| `-ls` | 显示当前文件的属性（等于 `ls -dils`）并返回真。 |
| `-cpio device` | 将当前文件的属性以 c 格式写入设备并返回真。 |
| `!expression` | 返回表达式的逻辑取反。 |

**图 4–12** `find` 表达式。（部分 2/2）

以下是一些 `find` 实际运行的示例：
