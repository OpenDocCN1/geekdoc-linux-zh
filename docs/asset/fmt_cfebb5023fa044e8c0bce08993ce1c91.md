
图 3.9 diff 命令的描述。

| 添加 (Additions) |  |
| :--- | :--- |
| `firstStart a secondStart, secondStop` | > 从第二个文件到第一个文件的待添加行 |

| 删除 (Deletions) |  |
| :--- | :--- |
| `firstStart, firstStop d lineCount` | < 从第一个文件中待删除的行 |

| 修改 (Changes) |  |
| :--- | :--- |
| `firstStart, firstStop c secondStart, secondStop` | < 第一个文件中将被替换的行<br>-- > 第二个文件中将被用于替换的行 |

图 3.10 diff 输出结果的含义。

# 第 3 章 高级用户的 UNIX 工具

`firstStart` 和 `firstStop` 表示第一个文件的行号，`secondStart` 和 `secondStop` 表示第二个文件的行号。

在示例中，我比较了几个文本文件以观察它们的差异：

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

< And all loving words you say are right.

---

> And everything you say to me is right.

$ diff lady2 lady3 ...compare lady2 and lady3.

3a,6

> It makes me feel,

> I'm so in love with you.

> Even in the dark I see your light.

$ diff lady3 lady4 ...compare lady3 and lady4.

2,4di

< I hold you close to me,

< And everything you say to me is right.

< It makes me feel,

$ -
```

`diff` 的 `D` 选项常用于将两个文件合并为一个包含 C 处理器指令的单个。文件的每个版本都可以使用 `cc` 编译器配合合适的选项和宏定义重新创建。以下命令是说明性示例：

```
$ diff -Dflag lady3 lady4 ...look at the output.

Lady of the night,

#ifndef ...preprocessor directive.

I hold you close to me,

And everything you say to me is right.

It makes me feel,
#endif flag ...preprocessor directive.
I'm so in love with you.
Even in the dark I see your light.
$ diff -Dflag lady24 > lady.diff ...store output.
$ cc -P lady.diff ...invoke the preprocessor.
$ cat lady.i ...look at the output.
Lady of the night,
H hold you close to me,
And everything you say to me is right.
$ cc -Dflag P lady.diff ...obtain the other version.
$ cat lady.i ...look at the output.
Lady of the night,
I'm so in love with you.
Even in the dark I see your light.
$
```

## 查找文件：find

该工具的功能不仅仅是定位命名的文件；它还可以对满足特定条件的文件执行操作。例如，你可以使用 `find` 删除所有属于用户 tim 且三天内未修改过的文件。图 3.1 提供了 `find` 的正式描述，图 3.12 提供了表达式的语法。

Utility: `find pathList expression`

`find` 工具递归地遍历 `pathList` 并对每个文件应用 `expression`。表达式的语法如图 3.12 所示。

图 3.11 find 命令的描述。

| 表达式 (Expression) | 值/动作 |
| :--- | :--- |
| `-name pattern` | 如果匹配模式则为真，模式可能包含 shell 元字符 `*`、`[]` 和 `?` |
| `-perm oct` | 如果文件权限标志的八进制描述完全等于 `oct`，则为真 |
| `-type ch` | 如果文件类型为 `ch`（`b` = 块设备，`c` = 字符设备，等）则为真 |

| 表达式 (Expression) | 值/动作 |
| :--- | :--- |
| `-user userId` | 如果所有者为 `userId` 则为真 |
| `-group groupId` | 如果文件属于 `groupId` 则为真 |
| `-atime count` | 如果在 `count` 天内被访问过，则为真 |
| `-mtime count` | 如果在 `count` 天内被修改过，则为真 |
| `-ctime count` | 如果在 `count` 天内状态改变过，则为真 |
| `-exec command` | 如果退出代码为 0 则为真。命令必须以分号 (;) 结束 |
| `-print` | 打印文件名 |
| `-ls` | 显示文件属性 |
| `-cpio device` | 将文件写入 cpio 格式 |
| `!expression` | 表达式的否定 |
| `expr1 -o expr2` | `expr1` 和 `expr2` 的逻辑或 |

3.12 (继续)

这里有一些 `find` 的示例：

```
$ find . -name '*.c' -print
  ...打印当前目录或子目录下所有 .c 结尾的文件名。
in ".c".
$ find . -mtime 14 -ls
  ...显示过去 14 天内修改过的文件。
-rw-rr-- 1 glass 14155 May 1 16:58 .tty.txt
-rw-rr-- 1 glass 48 May 14:02 .myfile.doc
-rw-rr-- 1 glass 10 May 14:02 .rain.doc
-rw-rr-- 1 glass 47794 May 2 10:56 .tset.txt
$ find -name '*.bak' -ls -exec rm {} \;
  ...显示并删除以 .bak 结尾的文件。
-rw-rr-- 1 glass 9 16:01 .a.bak
-rw-rr-- 1 glass 9 12:01 .b.bak
-rw-rr-- 1 glass 15630 Jan 26 00:14 /.s6/gosh.bak
-rw-rr-- 1 glass 14841 Jan 26 12:59 /.s6/gosh2.bak
$ find \ -name '*' -o name '*.txt' \ -print
  ...打印所有 .c 或 .txt 文件的文件名。
```

## 存档

- 用于每日、每周、每月备份
