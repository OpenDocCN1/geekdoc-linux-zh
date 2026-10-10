
## 自动补全

大多数 shell 都支持命令行补全。命令行补全用于让 shell 自动完成命令或文件路径。在大多数系统上，使用 Tab 键即可激活命令行补全，如下例所示。

```bash
$ whe<TAB>
$ whereis
```

使用命令行补全

在上述示例中，输入 whe 并按下 Tab 键后，命令 whereis 会自动补全，而无需输入完整命令。

自动补全也适用于文件路径。输入 ls -1 /etc/en 并按下 Tab 键会自动补全为文件 /etc/environment，如下例所示。

```bash
$ ls -1 /etc/en<TAB>
$ ls -1 /etc/environment
```

文件名命令行补全

当找到多个匹配项时，shell 将显示所有匹配结果。在下例中，输入 ls -1 /etc/host 并按下 Tab 键将显示 /etc 目录中所有匹配的文件。

```bash
$ ls -1 /etc/host<TAB>
host.conf  hostname  hosts  hosts.allow  hosts.deny
```

使用文件名补全显示多个匹配项

> **提示：** 除了命令行补全外，某些 shell 还支持使用键盘上的上箭头键调取之前执行的命令。

## 通配符

通配符用于将一个模式与一个或多个文本元素进行匹配。它们在命令行上非常有用，可执行批量任务，如列出或删除一组文件。下表列出了命令行中可用的不同类型的通配符。

| 通配符 | 功能 |
| :--- | :--- |
| **\*** | 匹配 0 个或多个字符 |
| **?** | 匹配 1 个字符 |
| **[abc]** | 匹配列出的字符之一 |
| **[a-c]** | 匹配范围内的一个字符 |
| **[!abc]** | 匹配任何未列出的字符 |
| **[!a-c]** | 匹配任何不在范围内的字符 |
| **{tacos,nachos}** | 匹配列表中单词的一个 |

通配符类型

星号（**\***）是最简单且最有用的通配符。下面的示例演示了使用星号通配符显示所有匹配文件名的文件。

```bash
$ ls -l /etc/host*

-rw-r--r-- 1 root root   92 2008-12-23 12:53 /etc/host.conf
-rw-r--r-- 1 root root    6 2009-04-23 15:50 /etc/hostname
-rw-r--r-- 1 root root  251 2009-05-22 14:55 /etc/hosts
-rw-r--r-- 1 root root  579 2009-04-20 09:14 /etc/hosts.allow
-rw-r--r-- 1 root root  878 2009-04-20 09:14 /etc/hosts.deny
```

使用星号通配符列出文件

输入 `ls -l /etc/host*` 会列出 /etc 目录中以单词 *host* 开头的所有文件。其他通配符的示例如下所示。

```bash
$ ls -l /etc/hosts.{allow,deny}

-rw-r--r-- 1 root root 579 2009-04-20 09:14 /etc/hosts.allow
-rw-r--r-- 1 root root 878 2009-04-20 09:14 /etc/hosts.deny

$ ls -l /etc/hosts.[a]*

-rw-r--r-- 1 root root 878 2009-04-20 09:14 /etc/hosts.deny

$ ls -l /etc/host?

-rw-r--r-- 1 root root 251 2009-05-22 14:55 /etc/hosts
```

其他通配符示例

在此示例中，第一个命令使用 `{allow,deny}` 来显示所有以单词 *allow* 或 *deny* 结尾的匹配项。第二个命令使用 `[a]*` 来显示在点号后以字母 *a* 开头的匹配项。第三个示例使用 `?` 通配符来匹配单个字符。

## 管道

管道（也称为流水线）可用于将一个命令的输出定向到另一个命令的输入。管道通过使用键盘上的 **|** 键（通常位于反斜杠键上方）执行。

```bash
$ ls -l /etc | more
total 968
-rw-r--r--  1 root root     2975 2008-08-18 13:30 adduser.conf
-rw-r--r--  1 root root       44 2010-04-06 16:59 adjtime
-rw-r--r--  1 root root       53 2008-08-18 13:49 aliases
-rw-r--r--  1 root root    12288 2009-08-28 13:39 aliases.db
drw-r--r-x  2 root root     4096 2010-04-05 10:59 alternatives
drwxr-xr-x  7 root root     4096 2010-04-05 10:59 apache2
drwxr-xr-x  3 root root     4096 2008-08-18 13:48 apm
drwxr-xr-x  2 root root     4096 2009-08-28 13:39 apparmor
drwxr-xr-x  6 root root     4096 2008-08-18 13:47 apparmor.d
drwxr-xr-x  4 root root     4096 2010-01-25 13:43 apt
-rw-r--r--  1 root daemon    144 2008-02-20 07:41 at.deny
-rw-r--r--  1 root root     1733 2008-05-12 13:33 bash.bashrc
-rw-r--r--  1 root root   216529 2008-04-14 20:45 bash_complet
drwxr-xr-x  2 root root     4096 2010-04-05 10:59 bash_completion.d
:
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_41_0.png)

对 **/etc** 目录使用 **ls -l** 通常会快速滚动显示该目录的内容。将 **ls -l** 的输出通过管道传给 **more** 命令（见第 71 页）会逐页显示 **/etc** 目录的内容。

另一个与管道常用配合的命令是 **grep**（见第 76 页）。**grep** 工具可用于过滤命令或文件的输出并显示匹配结果。下一个示例演示了将 **ls** 命令的输出通过管道传给 **grep** 以过滤结果并显示包含单词 *hosts* 的匹配项。

```bash
$ ls -l /etc | grep host
-rw-r--r-- 1 root root  92 2007-10-20 06:51 host.conf
-rw-r--r-- 1 root root   9 2008-08-19 15:29 hostname
-rw-r--r-- 1 root root 300 2009-12-07 09:19 hosts
-rw-r--r-- 1 root root 579 2008-08-18 13:30 hosts.allow
-rw-r--r-- 1 root root 878 2008-08-18 13:30 hosts.deny
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_41_1.png)

> **注意：** *管道在命令行工作中极其有用。从现在开始，它们将在示例中频繁出现。*

## 重定向

命令的输出可以重定向到其他位置，例如文本文件。重定向通过使用键盘上的 > 字符启动。

```bash
$ date > date.txt
$ ls -l date.txt
-rw-r--r-- 1 nick nick 29 2009-06-10 11:37 date.txt
```

将 date 命令的输出重定向到文件

在上述示例中，`date` 命令的输出被重定向到名为 `date.txt` 的文件，而不是显示在屏幕上。如果指定的文件不存在，它将被自动创建。如果文件已存在，它将被覆盖。为了防止覆盖文件，可以使用 `>>` 将内容追加到文件中，如下例所示。

```bash
$ date >> date.txt
```

将命令的输出追加到文件

有两种不同类型的输出：

- 1. 标准输出 (STDOUT)
- 2. 错误输出 (STDERR)

`STDOUT` 和 `STDERR` 可以选择性地定向到特定文件。这在捕获错误消息时非常有用，如下所示。

```bash
$ ls -l /NonExistantFile 1>ls.txt 2>lserror.txt
$ ls -l ls*
-rw-r--r-- 1 nick nick 61 2009-06-10 11:46 lserror.txt
-rw-r--r-- 1 nick nick  0 2009-06-10 11:46 ls.txt
```

选择性重定向 STDOUT 和 STDERR

在此示例中，`1>` 代表 `STDOUT`，`2>` 用于 `STDERR`。由于请求的文件不存在，错误消息被记录在 `lserror.txt` 文件中。所有非错误输出都保存在 `ls.txt` 文件中。

除了 `STDOUT` 和 `STDERR`，您还可以将输入从其他位置（如文件）重定向到命令。这被称为标准输入或 `STDIN`。下一个示例演示了使用 `STDIN` 将文件内容传给 `mail` 命令（见第 163 页）。

```bash
$ mail gregnick@gmail.com < ShoppingList.txt
```

将输入从文件重定向到命令

## **mv**

**用途：** 移动或重命名文件和目录。

**使用语法：** `mv [OPTIONS] [SOURCE] [DESTINATION]`

```bash
$ ls -l
-rw-r--r-- 1 nick nick 55 2009-05-20 15:32 MyFile
$ mv MyFile MyFile.old
$ ls -l
-rw-r--r-- 1 nick nick 55 2009-05-20 15:32 MyFile.old
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_43_0.png)

`mv` 命令用于移动或重命名文件。在上述示例中，使用 `mv` 命令将 `MyFile` 文件重命名为 `MyFile.old`。在下一个示例中，`MyFile.old` 被移动到 `/tmp` 目录。

```bash
$ mv MyFile.old /tmp/
$ ls -l /tmp/
-rw-r--r-- 1 nick nick 55 2009-05-20 15:32 MyFile.old
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_43_1.png)

`mv` 命令也可用于移动或重命名目录。在下面的示例中，`NewFiles` 目录被重命名为 `OldFiles`。

```bash
$ ls -ld NewFiles/
drwxr-xr-x 2 nick nick 4096 2009-06-28 13:23 NewFiles/
$ mv NewFiles/ OldFiles/
$ ls -ld OldFiles/
drwxr-xr-x 2 nick nick 4096 2009-06-28 13:23 OldFiles/
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_43_2.png)

> **警告：** `mv` 命令的默认行为将覆盖任何现有文件。`-i` 选项会覆盖此行为，并在覆盖目标文件之前提示用户。

常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `mv [SOURCE] [DEST]` | 将文件或目录移动到指定位置 |
| `mv -i [SOURCE] [DEST]` | 在覆盖目标文件前提示 |
| `mv -f [SOURCE] [DEST]` | 如果目标文件存在则强制覆盖 |

