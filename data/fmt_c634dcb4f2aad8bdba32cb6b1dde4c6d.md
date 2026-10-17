
下一个命令将两个名为 `memo.new` 和 `letter` 的文件复制到远程计算机 `bravo` 上 jenny 的主目录。`bravo` 上复制文件的绝对路径为 `/home/jenny/memo.new` 和 `/home/jenny/letter`。

```
$ rcp memo.new letter bravo:/home/jenny
```

最后一个命令将 `bravo` 上 Jenny 的 `reports` 目录中的所有文件复制到本地计算机的 `oldreports` 目录，保留副本上的原始修改日期和文件访问权限：

```
$ rcp -p 'bravo:reports/*@' oldreports
```

## 832 rcs

| rcs | 创建或更改 RCS 文件的属性 |
| :--- | :--- |
| 语法 | `rcs [options] file-list` |

### 总结

`rcs` 实用程序创建或更改 RCS 文件的属性。选项控制执行的操作。`rcs` 实用程序是版本控制系统（第 560 页）的一部分，用于管理源文件的存储、检索和更新。

### 参数

`file-list` 是 `rcs` 将处理的一个或多个普通文件的路径。

### 选项

- `-i` 创建一个空的 RCS 文件。
- `-l` 为文件设置锁。如果不指定版本，`rcs` 将锁定最新版本。
- `-u` 将版本添加到列表。如果不指定版本，`rcs` 将更新最新版本。
- `-e` 从列表中删除版本。如果不指定版本，`rcs` 将移除最新版本。

### 注意事项

RCS 编码文件的名称以 `,v` 结尾。简单文件名必须与 RCS 文件一致。RCS 文件通常存储在子目录（命名为 `RCS`）中。版本可以通过数字识别。主版本由两个整数组成，而分支版本至少由四个组成。

## 示例

以下命令创建一个名为 `RCS/menul,v` 的新 RCS 编码文件：

```
$ rcs -i menul

RCS file: RCS/menul,v

description, terminated with single '.' or end of file:

NOTE: This is NOT the log message!

>> basic menu

>> .

done
```

下一个示例将 Alex 和 Barbara 添加到允许更改 `menus_march` 文件的用户列表中：

```
$ rcs -aalex,barbara menus_march
```

将 Barbara 添加到列表后，你可以通过以下命令撤销她的权限：

```
$ rcs -barbara menus_march
```

下一行从 `menus_march` 文件中删除版本 1.5：

```
$ rcs -01.5:1 menul

RCS file: RCS/menul,v

deleting version 1.5

done
```

最后一个示例从 `menus_march` 文件中删除版本 1.5 到 1.8：

```
$ rcs -01.5:1.8 menus_march

RCS file: RCS/menus_march,v

deleting version 1.8

deleting version 1.7

deleting version 1.6

deleting version 1.5

done
```

## 834 rlog

## rlog 输出 RCS 文件历史的摘要

语法: `rlog [options] file-list`

### 总结

`rlog` 工具用于显示 RCS 文件历史的摘要。选项用于控制 `rlog` 显示的信息量。`rlog` 工具是 RCS（修订控制系统——第 560 页）的一部分，RCS 是一组用于管理源文件存储、检索和更新的相关工具集。第二部分中的 RCS 工具包括 `ci`、`co`、`rc` 和 `rlog`。

### 参数

`file-list` 是文件名列表，通常为工作文件。对于列表中的每个文件，`rlog` 会在工作文件所在目录查找对应的 RCS 文件，然后在工作文件所在的目录进行查找。关于 RCS 和工作文件名的更多信息，请参见下文的“注释”。

### 选项

- `-ddates[dates]` 使用文件检查日期来限制 `rlog` 显示的信息。你可以通过分号隔开每个日期范围来选择多个日期范围。每个日期范围使用大于 (`>`) 或小于 (`<`) 符号来指定，并且必须用引号括起来，以防止 shell 将符号解释为重定向。要查看某个文件在 1997 年 10 月份的历史，你将使用 `> "Oct 1 1997 08:00 AM LT < Oct 31 1997 12:00 pm LT"`

- `-r[revision-list]` 将 `rlog` 报告的信息限制在指定的修订版本或修订范围内。如果你使用 `-r` 选项但不带数字，`rlog` 将报告最新修订。可以通过包含冒号来指定修订范围。例如，要将显示限制在修订版本 1.2 到 1.4，请使用 `-r1.2:1.4`。要查看修订 1.2 到当前修订的信息，请使用 `-r1:2`。要查看修订 1.4 及所有更早修订的信息，请使用 `-r1:4`。

## 注释

RCS 编码文件名以两个字符 `.v` 结尾。工作文件的简单部分必须与 RCS 文件一致，但对应 RCS 文件的 RCS 文件名字符除外。对应 RCS 文件的 `RCS/mergecases.v` 可能是 `mergescases.c`，但不是 `gets.c`。如果你想了解更多关于文件命名（包括 `file-list` 中的 RCS 文件）的信息，请参阅 `rcs` 手页和其他文档。虽然你可以将 RCS 和工作文件存储在任何地方，但 RCS 文件通常存储在工作文件目录的子目录（命名为 `RCS`）中。有时两者都存储在同一个目录下。

## rlog 835

修订版本可以通过数字识别，该数字由偶数个点分隔的整数组成。主干上的修订版本有两个整数，分支修订版本至少包含四个整数。你也可以使用符号名称来识别修订版本。

在指定日期时，默认时区是协调世界时 (`UTC`)，也称为格林治标准时间 (`GMT`)。RCS 命令识别多种格式的日期，例如：

```
5:00 PM LT

1:00am, Jul. 18, 1997

Fri Jul 18 17:00:00 PDT 1997
```

在此示例中，`LT` 代表本地时间（在这种情况下是 `PDT`，太平洋夏令时间）。

如果源文件同时被多个一个开发者修改，或者你在目录层次结构中组织了大量的源文件，你可能希望考虑 `cvs`（第 567 页）而不是 RCS 工具。`cvs` 工具扩展了 RCS 的功能以适应大型项目开发。`cvs` 接口与 RCS 相似，易于 RCS 用户学习和使用。

## 示例

下面，`rlog` 显示了对 `RCS/thesis,v` 文件所做更改的标准信息：

```
$ rlog file: thesis

RCS file: thesis,v

Working file: thesis

head: 2.7

branch:

locks: strict

alex: 2.7

access list:

symbolic names:

comment leader: ""

keyword substitution: kv

total revisions: 14      selected revisions: 14

description:

Alex Watson's thesis

----------------------

revision 2.7      locked by: alex;

date: 1996/08/08 21:15:47      author: alex;      state: Exp      lines: +663 -0

add examples
```

下一个示例仅打印关于修订版本 1.3 的信息：

```
$ rlog -1.3 thesis
```

最后一个示例显示了 7 月最后两周内所做更改的信息：

```
$ rlog -d"Jul 15 1997 8:00 am LT < Jul 31 1997 5:00 pm LT" thesis
```

## login

| 语法 | `login [option] remote-computer` |

### 总结

`login` 工具通过网络在远程计算机上建立登录会话。

### 参数

`remote-computer` 是你的系统可以通过网络访问的计算机名称。

### 选项

- `-login-name` `login` 以 `login-name` 指定的用户身份登录到远程计算机，而不是以你自己的身份登录。

## 注释

如果位于远程计算机上的 `/etc/hosts.equiv` 文件指定了你本地计算机的名称，远程计算机将不会提示你输入密码。列在 `/etc/hosts.equiv` 文件中的计算机系统被视为与你的本地机器一样安全。

如果位于远程计算机上的 `/etc/hosts.equiv` 文件指定了你本地计算机的名称，远程计算机将不会提示你输入密码。列在 `/etc/hosts.equiv` 文件中的计算机系统被视为安全的本地机器。

## 示例

以下命令行在工作目录和另一个目录删除文件：

```
$ login memo
$ login letter memo2
$ login /home/jenny/temp
```

## rm 886

## 删除文件（删除）

语法: `rm [options] file-list`

### 总结

`rm` 工具删除一个或多个文件。它可以用于删除硬链接和符号链接。当你删除文件时，会释放所占空间。关于链接的更多信息请参见第 4 章。

### 参数

`file-list` 包含要删除的文件列表。该列表可能包含模糊引用。由于可以使用一个命令删除大量文件，因此请谨慎使用 `rm`，特别是当使用模糊引用时。如果你对带有引用的 `rm` 命令的效果不确定，请先使用 `echo` 工具配合相同的引用来评估生成的列表。

### 选项

- `-f` 删除你没有权限的文件而不征求许可。如果文件不存在，还会抑制信息输出。
- `--interactive` 在删除每个文件之前询问。如果你在使用递归选项时，`rm` 会在检查每个目录之前询问。
- `-r` recursive 删除指定目录的内容，包括所有子目录以及目录本身。谨慎使用此选项。

## 注释

第 84 页和 766 页关于 `In` 工具的包含了关于删除链接的讨论。如果你需要删除空目录，请参考 `rmdir` 工具（第 839 页）。

当你想要删除以连字符开头的的文件时，必须防止 `rm` 将文件名解释为选项。一种方法是在文件名之前给出特殊选项 `--`。这个特殊选项告诉 `rm` 后面不再有更多选项——其后的参数都是文件名，即使它们看起来像选项。

## 838 rm

## 示例

以下命令行在工作目录和另一个目录删除文件：

```
$ rm memo
$ rm letter memo1 memo2
$ rm /home/jenny/temp
```

下一个示例在删除特殊字符及其子目录中的每个文件之前询问用户。此命令对于删除包含特殊字符的文件非常有用，特别是空格、制表符和换行符。（你不应该故意创建包含这些字符的文件名，但可能会意外发生。）

```
$ rm -ir .
```

# rmdir 删除目录

语法: `rmdir directory-list`

# 摘要

`rmdir` 实用通过删除指向这些目录的链接，从文件系统中删除空目录。

### 参数

`directory-list` 包含 `rmdir` 要删除的空目录的路径名。

### 注意事项

如果你需要删除非空目录及其内容，请参考带有 `-r` 选项的 `rm` 实用。

# 示例

以下命令行从当前工作目录删除空的 `literature` 目录：

```
$ rmdir literature
```

下条命令行使用绝对路径名删除 `letters` 目录：

```
$ rmdir /home/jenny/letters
```

# rsh

在远程计算机上执行命令

语法: `rsh [option] host [command-line]`

# 摘要

`rsh` 实用通过在远程系统上启动 shell，在 *host* 上运行 `command-line`。如果你省略了 `command-line`，`rsh` 将调用 `login`，这将你登录到远程计算机。

### 参数

必须将远程计算机的名称作为 *host* 给出。*host* 之后的任何参数都是 `command-line` 的一部分，该部分将在远程系统上运行。如果你不想让本地 shell 在将其传递给 *rsh* 之前展开 `command-line` 中的 shell 特殊字符，则必须对其加引号或转义。

### 选项

- `- login` 如果你在远程计算机上的登录名与本地登录名不同，可以使用此选项提供远程登录名。

### 注意事项

你的本地登录名和本地计算机名称应该出现在远程计算机上用账户的家目录下的 `.rhosts` 文件中。参见“login”（第 836 页）中的示例 `.rhosts` 文件。

# 示例

在第一个示例中，Alex 使用 **rsh** 获取他在 **bravo** 上家目录下的文件列表：

```
$ rsh bravo ls

Cost-of-living

Info

Work

preferences
```

在第二个示例中，上一个命令的输出被重定向到文件 **bravo.ls**。由于重定向字符 `>` 没有被转义，它被本地 shell 解析，并在本地机器上创建了 **bravo.ls** 文件。

```
$ rsh bravo ls > bravo.ls
$ cat bravo.ls

Cost-of-living

Info

Work

preferences
```

# 841

下一个示例对重定向字符 `>` 加了引号。文件 `bravo.ls` 在远程计算机（`bravo`）上创建，如在 `bravo` 上运行 `ls` 所示所示。

```
$ rsh ls "> bravo.ls
$ rsh bravo ls

Cost-of-living

Info

Work

bravo.ls

preferences
```

在最后一个示例中，不带 `command-line` 的 `rsh` 登录到远程计算机。这里 Alex 使用了 `-l watson` 选项以 `watson` 的身份登录 `bravo`。必须配置 `/home/watson/.rhosts` 文件以允许 Alex 以这种方式登录该账户。

```
$ rsh -l bravo

Last login: Sat Jul 27 16:13:53 from :0.0

Linux 2.0.18. (POSIX).

$ hostname

bravo

$ exit

rlogin: connection closed.
```

# 842 rwho

| rwho | 显示连接到网络的计算机上的用户名 |
| :--- | :--- |
| 语法: `rwho [option]` | |

# 摘要

`rwho` 实用显示当前登录到网络计算机的用户名，连同他们的终端设备号、登录时间以及自他们在键盘上输入以来已过去的时间。默认情况下，`rwho` 只显示过去一小时内使用过其终端的用户。

### 参数

无参数。

### 选项

- `-a` 显示所有当前登录的用户名，即使他们已经空闲超过了一小时。

### 注意事项

`rwho` 显示的信息由 `rwhod` 守护进程在网络上广播，该守护进程通常在系统重启时由运行命令脚本启动。`rwhod` 守护进程可能会在网络上产生大量流量，并且在你的站点可能没有运行。如果 `rwho` 没有显示任何信息，很可能是 `rwhod` 没有运行。

# 示例

以下示例说明了 `rwho` 的用法。用户名出现在第 1 列，随后是计算机名称和终端行，以及用户登录的时间。如果第四列为空，则用户正在终端上活动打字；否则，第四列指示自上次使用键盘以来已过了多少小时和分钟。

```
$ rwho -a

watson bravo:tty01 Sep 14 10:19

barbara hurrah:tty01 Sep 13 10:54 2:33

jenny hurrah:tty02 Sep 14 14:24 :01
```

# sed 843

| sed | 编辑文件（非交互式） |
| :--- | :--- |
| 语法: `sed [-n]-f script-file [file-list]` | |
| 语法: `sed [-n] script [file-list]` | |

# 摘要

`sed`（流编辑器）实用是一个批处理（非交互式）编辑器。`sed` 命令通常存储在脚本文件中（如上面所示的第一种格式），尽管你也可以向命令行提供简单的 `sed` 命令（如第二种格式）。默认情况下，`sed` 将行从文件复制到标准输出。

`sed` 逐行处理输入的行。对于每一行，它会执行脚本中的命令。脚本由地址和指令组成。地址选择要操作的行，指令指定要的操作。

### 参数

`script-file` 是包含命令的文件路径名。`file-list` 包含要编辑的文件名。

### 选项

- `-n` 抑制自动打印模式空间。
- `-f` 从脚本文件读取命令。

# 讨论

`sed` 逐行处理输入。对于每一行，它执行脚本中的命令。脚本由地址和指令组成。地址选择要操作的行，指令指定操作。

脚本由以下格式：

```
[address] instruction
```
