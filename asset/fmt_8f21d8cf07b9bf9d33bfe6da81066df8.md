
同样，让他惊讶的是 shell 只是将他的输入回到了屏幕上，没有列出任何文件。他继续尝试示例7.12。

现在他看到了四个可能文件中的三个。仍然，这种方法并不是获取隐藏 `.bash` 文件完整列表的有效方法。

## 示例 7.12 方括号 [] 通配符展开例外的例外

Perez 回想起之前使用星号和通配符时发生的情况，在他的主目录下输入了以下内容：

```bash
$ echo .bash[-*}<Enter>
.bash_history .bash_logout .bash_profile
```

## 感叹号作为通配符

你在方括号内使用感叹号 `!` 作为通配符来排除可能性。再次，如示例 7.13 所示，括号所在的位置由 shell 展开为单个字符。但与列表括号不同，位置上的字符不是括号内指定字符集的文件会被命令的输入。将 `!` 视为“不”可能会有帮助。

> 警告 使用某些字符的通配符，特别是 `rm` 删除命令是有风险的。你可能会得到意外且不受欢迎的结果。我们建议在想要包含通配符时使用交互式形式，即 `rm -i`。当你想要引入可能会更改树所有目录内容的递归选项 `-R` 时，这一建议特别有用。

## 示例 7.13 感叹号 (!) 和方括号 [] | 通配符

延续示例 7.12，Perez 复制了他的 `.bash_history` 但将副本重命名为 `.bash-history` 然后，他输入了在示例 7.12 中使用的相同命令，以找到带有连字符或下划线的所有可能的 `.bash` 文件：

```bash
$ cp .bash_history .bash-history<Enter>
$ echo .bash[-]*<Enter>
.bash_history .bash_history .bash_logout .bash_profile
```

现在，他决定使用感叹号通配符来排除新的 `.bash_history` 文件，如下：

```bash
$ echo .bash[-]*<Enter>
.bash_history .bash_logout .bash_profile
```

他的感叹号告诉 shell 忽略中间带有连字符的 `.bash` 文件。结果是：他看到了与示例 7.12 中看到的相同的三个文件。

## 用于范围的方括号

你不仅可以将方括号用于列表，还可以将其用于范围。在这里，由方括号位置定义的位置同样由 shell 扩展，但仅限于单个字符。这一次，只有在该位置上的字符属于括号中指定的字符范围的文件会被作为命令的输入。此功能允许使用更大量的字符列表，减少了定义列表所需的字量。参见示例 7.14。

示例 7.14 Juana仍在尝试她的电话列表文件，她发现也可以这样使用范围括号：

```
$ ls *[1-3]<Enter
RFI_Tel1 RFI_Tel2 RFI_Tel3
```

## 引用元字符以禁用 Shell 解析

引用是指禁用、覆盖、否定或转义其他元字符、变量或命令名称的特殊含义。之所以被称为“引用”，是因为这三种方法中的两种使用了双引号。

基本上，这些引用技术配备了它们自己的一组元字符，用于覆盖或禁用 shell 对其他元字符的正常解释。表 7.3 总结了引用元字符的功能，并给出了简单示例。

### 引用元字符使得包含的元字符被字面量解释

例如，单引号导致 `HOME` 被解释为 `--HOME--`，因为美元符号变成了一个普通的美元符号，而不是一个命令，或者不按照 shell 通常会解释和执行的方式进行扩展。例如，`echo .*` 返回 `*`，而不是所有文件名中除第一个位置外包含单个点的文件列表。

> 记住，你必须成对使用单引号和双引号。否则，会出现你的次级命令行提示符。在大多数情况下，下一行会出现一个角括号 `>`，shell 将等待指令。要返回到主提示符，请按 `Ctrl-C`。

表 7.3 引用元字符及其功能

| 元字符 | 给 shell 的指令 | 示例 |
|---|---|---|
| 单引号 `''` | 忽略引号内所有的元字符 | `$ echo '$HOME'<Enter` <br> `$HOME` |
| 双引号 `""` | 忽略除美元符号 `$`、反引号 `` `` `` 和反斜杠 `\` 之外的所有元字符 | `$ echo "$HOME"<Enter` <br> `/home/quixoted` <br> `$ echo "*.*"<Enter` <br> `**` |
| 反斜杠 `\` | 忽略下一个元字符的特殊含义 | `$ echo \$HOME<Enter` <br> `$HOME` |

反斜杠字符值得特别关注。如果你使用反斜杠在另一行继续执行命令，该反斜杠将禁用紧随其后的 `Enter` 键的特殊含义。通常 `Enter` 键会将行上的所有内容提交给 shell 进行解释。通过在这里使用反斜杠，是在告诉 shell：“命令尚未结束；忽略下一个 Enter 并让我继续输入指令。”然后，下一个 Enter 键会将命令提交给 shell。

## 示例 7.15 引用元字符

```
$ echo "This is a double quotation mark \""<Enter
This is a double quotation mark "
```

## 标准文件：重定向与管道

对于 Linux 系统中调用的每个进程，会自动打开三个文件：

- **标准输入 `stdin`。** 命令期望接收输入的位置。通常，该位置是键盘。
- **标准输出 `stdout`。** 命令期望发送结果的位置。通常，该位置是屏幕，但也可以是文件。
- **标准错误 `stderr`。** 命令期望发送错误信息的位置。通常，该位置是用户的终端屏幕，也可以是系统控制台。

默认位置的描述存储在命令的文件描述符表中。不过，你可以通过重定向更改位置，例如屏幕、文件或控制台，我们稍后会描述这一点。

## 文件描述符

每个命令或工具都会打开自己的文件描述符，以跟踪数据文件、输入、输出和错误消息。文件描述符取决于运行的命令或工具。文件描述符条目指向特殊的设备指针文件，这些文件指向系统设备，如终端或磁盘驱动器。参见表 7.4 中的描述符。注意，从 0 到 2 的描述符和运算符具有默认值，但用户可以定义 3 到 9 的其他值。同时，请记住在 Linux/UNIX 中，并不是所有文件名都指向数据文件。此外，现在请不要担心设备指针编号。我们稍后讨论重定向时会专门使用它们。

考虑 `cat` 命令，它用于列出我们在命令行中提供的文件的内容。如果不指定文件名，`cat` 仅仅会将你在按下 `Enter` 之前在命令行上输入的任何内容回显到终端屏幕。对于 `cat` 来说，默认的 `stdin` 是键盘，`stdout` 是终端屏幕。

## 表 7.4 文件描述符参数

| 描述符名称 | 运算符 | 指针 | 默认设备 |
| --- | --- | --- | --- |
| 标准输入 `stdin` | `<` | 0 | 键盘 |
| 标准输出 `stdout` | `>` | 1 | 屏幕 |
| 标准错误 `stderr` | `&` | 2 | 系统控制台 |
| 用户定义 | | 3 | |
| 用户定义 | | 4 | |
| 用户定义 | | 5 | |
| 用户定义 | | 6 | |
| 用户定义 | | 7 | |
| 用户定义 | | 8 | |
| 用户定义 | | 9 | |

## 输入重定向

重定向允许你指定命令在哪里接收输入。也就是说，如果你不想让它来自默认位置，通常是键盘，可以使用小于符号 `<`。

## 示例 7.16 定义文件描述符

如果你想定义一个描述符，例如输出到特定文件，你可能使用以下操作：

```bash
$ date > filename<Enter
```

## 输出重定向

重定向还允许你指定想让标准输出去哪里；也就是说，如果你不想让它去默认位置，通常是屏幕，则使用大于符号 `>`。

## 破坏性重定向

如果你的意图是向现有文件添加数据或“临时”创建一个文件，那么你可以使用破坏性重定向。它被称为“破坏性”，是因为如果目标文件已存在且其中已有数据，这些数据将被覆盖。语法是：

```
$ command > filename<Enter>
```

## 示例 7.17 使用 `<` 重定向输入

使用小于符号 `<` 告诉程序从文件查找输入：

```bash
$ cat < filename<Enter>
```

## 示例 7.18 使用 `>` 进行破坏性输出重定向

Juana 通过她的操作说明了 `ls` 命令的默认标准输出。首先，她进入 `/gutiejua/admin/phone#` 子目录。然后，她用 `ls` 列出内容：

```
$ cd /gutiejua/admin/phone#<Enter>
$ ls<Enter>
RFI_Tell RFI_2 RFI_3
```

表 7.5 列出了 Juana 刚刚执行的 `ls` 命令的默认描述符和行为。这是因为在此时，所有描述符的默认属性状态均为“未更改”。
Juana 现在将指示 `ls` 命令将其输出重定向到 `phone_no.out` 文件。如果 `phone_no.out` 文件存在，它将被覆盖。如果它还不存在，它将被创建：

```
$ ls > phone_no.out<Enter>
```

## 表 7.5 *ls* 命令的典型描述符表

| DEVICE POINTER | OPERATOR | DESCRIPTOR NAME | DEFAULT DEVICE | STATUS |
|---|---|---|---|---||
| 0 | `<` | stdin | keyboard | unchanged |
| 1 | `>` | stdout | terminal screen | unchanged |
| 2 | `2>` | stderr | terminal screen | unchanged |

## 表 7.6 *ls* 命令修改后的描述符表

| DEVICE POINTER | OPERATOR | DESCRIPTOR NAME | DEFAULT DEVICE | STATUS |
|---|---|---|---|---||
| 0 | `<` | stdin | keyboard | unchanged |
| 1 | `>` | stdout | phone_no.out file | changed |
| 2 | `2>` | stderr | terminal screen | unchanged |

由于 Juana 的指令，shell 识别出 `ls` 命令的描述符表实际上发生了更改，如表 7.6 所示。

## 非破坏性重定向

如果你的目的是为了向文件中添加数据或简单地避免覆盖现有数据，你可以将输出追加到现有文件中，称为*非破坏性重定向*。语法如下：

```
$ command >> filename
```

这种非破坏性重定向在示例 7.19 中所示。

## 示例 7.19 使用 `>>` 进行非破坏性输出重定向

Gregory 定期且规律地使用 `who` 命令检查系统中有哪些用户。当他这样做时，他将 `who` 的输出重定向到一个名为 `who_survey.out` 的现有文件，以备将来参考和统计。为了重定向输出并将其追加到该现有文件，他告诉 `who` 命令将其输出发送到 `who_survey.out` 文件，并将输出追加到文件中已有的任何数据之后：

```
$ who >> who_survey.out<Enter>
```

# 安装与管理 Linux 2E

**表 7.7** 命令修改后的描述符表

| DEVICE POINTER | OPERATOR | DESCRIPTOR NAME | DEFAULT DEVICE | STATUS |
|---|---|---|---|---||
| 0 | `<` | stdin | keyboard | unchanged |
| 1 | | stdout | who-survey.out file | changed |
| 2 | `2>` | stderr | terminal screen | unchanged |

由于 Reston 的指令，shell 识别出命令的描述符表实际上发生了更改，如表 7.7 所示。

# cat 和重定向输出

这里是输出重定向的一种方便的替代用法。我们已经知道 `cat` 命令通常用于列出文件内容。如果我们将 `cat` 和重定向输出结合起来，就可以快速创建文本文件，而无需调用文本编辑器。事实上，对于小文件，此过程可能被认为与使用文本编辑器一样，甚至优于它。以下是语法，我们包含了几行文本：

```
$ cat > filename<Enter>
Line 1 of filename ...<Enter>
Line 2 of filename ...<Enter>
After this line 3, we want to end the file ...<Enter>
<Ctrl>-d
```

注意，我们在文件末尾使用了 `Ctrl-D`。相比之下，使用 `Ctrl-C` 则会取消命令。这里有两个示例创建了这种类型的重定向：

- 第一个示例创建一个名为 `newfile` 的零长度文件。如果 `newfile` 已经存在，此过程将删除该文件的原始内容。

```
$ cat > newfile<Enter>
<Ctrl>-d
```

- 第二个示例创建了一个名为 `file3` 的文件，它包含 `file1` 和 `file2` 的合并内容。

```
$ cat file1 > file3<Enter>
<Ctrl>-d
```

# Shell 基础 201

# 示例 7.20 和用于创建文件的重定向

示例 7.20 的第一部分显示了 `cat` 的典型用法：列出文件内容。第二部分使用 `cat` 配合重定向创建一个新文件。Freston 以其正常功能使用 `cat` 命令列出 Juana 的 `RFI_Tel3` 的内容：

```
$ cat /home/gutieuz/admin/phone#s/RFI_Tel3<Enter>
Emergencies - +34 91 800 09 87
Human Resources - +34 91 900 55 87
Fax/Mail Room - +34 91 555 32 10
Web Site Design/Management - +34 958 55 19 21
```

现在，他想创建他自己的专用电话列表 `RFI_et_al_Tel#s` 的开头。我们使用 `cat` 配合重定向来创建新文件：

```
$ cat > /root/RFI_et_al_Tel#<Enter>
RFI Web Site Design/Management - +34 958 55 19 21
Fernando's Web Creation, Inc. - +34 91 555 66 22
Rodriguez's Internet Services, Inc. (Sevilla) - +34 95 555 22 66
<Ctrl>-d
```

表 7.8 列出了 `cat > /root/RFI_et_al_Tel#` 示例的描述符。

## 错误重定向

错误消息通常立即发送到屏幕或系统控制台。然而，有时你出于各种原因想重定向错误消息。有两种类型的错误重定向：

- 将错误消息重定向到文件
- 将错误消息重定向到 `/dev/null`

我们将详细讨论每一种。

表 7.8 `cat` 命令修改后的描述符表

| DEVICE POINTER | OPERATOR | NAME | DEVICE | STATUS |
|---|---|---|---|---|
| 0 | `<` | stdin | keyboard | unchanged |
| 1 | `>` | stdout | RFI_et_al_Tel# file | changed |
| 2 | `2>` | stderr | terminal screen | unchanged |

## 将错误消息重定向到文件

有时你需要从脚本或 shell 程序中收集错误消息以供将来参考或故障排除。这种重定向的一种应用是系统错误日志或网络分析。

以下是将输出破坏性重定向到文件的语法：

```
command 2> filename<Enter>
```

错误重定向与普通重定向的区别在于大于符号之前包含了 `2`。

以下是将输出追加即非破坏性重定向到文件的语法，其格式与普通重定向输出类似：

```
command 2>> filename<Enter>
```

注意 记住标准重定向的操作符是 `2>` 和 `>>` 示例 7.21 将输出重定向到文件

Juana 为 Nicholas 提供了一个标准错误的副本，查看标准输出 `RFI_et_al_Tel#` 如何直接进入系统控制台：

```
$ ls /root/RFI_et_al_Tel#<Enter>
Emergencies - +34 91 800 09 87
Human Resources - +34 91 900 55 87
Fax/Mail Room - +34 91 555 32 10
Web Site Design/Management - +34 958 55 19 21
```

Nicholas 现在尝试另一种他在示例 7.20 和 7.21 中尝试过的过程变体。他非常想 `cat RFI_Tel3`，但不那么想成功 `cat /root/RFI_et_al_Tel#s`。因此，他决定将任何错误消息发送到 `/dev/null`：

```
$ cat /root/RFI_et_al_Tel# 2> /dev/null<Enter>
```

## 204 安装与管理 Linux 2E

```
$ cat RFI_Tel /root/RFI_at_Tel_s 2> /dev/null<Enter
Emergencies - +34 91 800 09 87
Human Resources - +34 91 900 55 87
Fax/Mail Room - +34 91 555 32 10
Web Site Design/Management - +34 958 55 19 22
```
