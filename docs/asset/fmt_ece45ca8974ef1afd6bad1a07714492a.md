
`/install /bin /local /last+found /mnt /proc /root /sbin /test /usr`

`/var /vmlinuz ...`

```bash
$ echo /[a-c]*
/bin /boot /cdrom /dosa /dosc /etc /install /bin /local /proc /sbin /var
/zimage
```

```bash
$ echo /*
/bin/Mail /bin/arch /bin/bash ....
/boot/any.b /boot/any_d.b ...
/dev/MAKEDEV /dev/arp /dev/bmouseatxl ...
```

由于文件名生成并不是由相关的程序（即 `bash`）执行的，因此结果与你预期的不同。在这种情况下，`ls` 可能会导致一个看似无止尽的文件列表，尽管当前目录下只有几个文件。在展开 `*` 之后，`ls` 接收到了一个所有文件和目录的列表。然而，`ls` 显示的不仅是目录的名称，还有它们的内容。如果你只想获得所有文件和目录的简单列表，必须使用 `-d` 选项，该选项防止显示参数列表中指定目录的内容。

| 符号 | 说明 |
| :--- | :--- |
| `?` | 恰好一个任意字符 |
| `*` | 任意数量的任意字符（甚至是零个）（但不包括文件！） |
| `[abc]` | 指定字符之一 |
| `[a-f]` | 指定范围内的一个字符 |
| `![abc]` | 不属于指定字符的任意字符 |
| `^[abc]` | 同上 |
| `~` | 主目录的缩写 |
| `.` | 当前目录 |
| `..` | 父目录 |

如果你想获得关于 `bash` 内部工作的反馈，可以执行 `set -x`。在这种情况下，`bash` 会显示内部命令行（带有所有

```bash
$[3*4]
arithmetic calculations
```

## 命令替换

命令替换允许你将命令行中的某个命令替换为其执行结果。为了实现这一目的，命令必须包含在两个字符之间，或者使用 `$(command)`。后者的表示法更好：首先；它减少了由三种不同类型的引号（`'` `'` `` ` `` 和 `` `` ``）引起的混淆；其次，它是可以嵌入的。

无论如何编写，命令都会被其结果替换。这种替换允许对多个命令进行嵌入式调用，其中一个命令将其结果传递给下一个命令。下面的示例说明了这种非常强大的机制：

```bash
$ ls -l 'find /usr/doc -name '*README*'\n$ ls -l $(find /usr/doc -name '*README*') # 替代表示法
```

使用上述命令，首先执行 `find /usr/doc -name '*README*'`。该命令的结果是 `/usr/doc` 目录下包含 "README" 字符的文件列表。此列表现在被插入到 `find` 命令的命令行中。现在，命令行可能如下：

```bash
$ ls -l /usr/doc/xpm33/README /usr/doc/term/README.gz\n> /usr/doc/mt-st/README/README.gz
```

该命令提供以下结果：

| 权限 | 所有者 | 大小 | 日期 | 名称 |
| :--- | :--- | :--- | :--- | :--- |
| `-rw-r--r--` | `1` | `root` | `1854` | `Apr 24 22:49` | `/usr/doc/README.gz` |
| `-rw-r--r--` | `1` | `root` | `847` | `Sep 21 1993` | `/usr/doc/mt-st/README.gz` |
| `-rw-r--r--` | `1` | `root` | `5796` | `Apr 20 1994` | `/usr/doc/term/README.gz` |
| `-rw-r--r--` | `1` | `root` | `5550` | `Jan 30 1994` | `/usr/doc/xpm33/README.gz` |

请注意，无法通过使用 `|` 字符的简单管道获得该结果。`ls` 期望从标准输入读取数据，并忽略通过管道由 `find` 提供的信息。因此，以下命令仅显示当前目录的内容。结果文件未找到！

```bash
$ find /usr/doc -name '*README*' | ls -l # 这不起作用
```

然而，还有另一种不需要命令替换的解决方案：通过命令 `xargs` 将数据从标准输入重定向到 `xargs` 指定的命令：

```bash
$ find /usr/doc -name 'README' | xargs -l
```

| 表示法 | 说明 |
| :--- | :--- |
| `'command'` | 将命令替换为其结果 |
| `$(command)` | 同上，替代表示法 |

## 字符字符串中的特殊字符

由于在 `bash` 中几乎每个字符（字母和数字）似乎都具有某些特殊含义，在字符字符串或文件名中使用这些字符似乎完全是不可能的。这个问题可以通过引号来解决。如果你使用单引号，内部的字符被视为字面量。如果你使用双引号，某些特殊字符仍然会被解释，而另一些则不会。

## 局部变量与全局变量

(环境变量)

描述变量时使用的“局部”和“全局”术语源自编程语言领域。对于 `shell` 变量而言，如果一个变量在命令或 `shell` 程序启动时被传递，则认为它是全局的。全局变量通常也称为环境变量。

请注意，所有通过简单赋值创建的变量都被视为局部变量。如果你想定义一个全局变量，必须调用 `export` 或使用 `declare -x`。

有很多命令用于管理 `shell` 内的变量，其中一些命令的功能是重叠的。因此，要定义全局变量，你可以同时使用 `export` 和 `declare -x` 等。通过下表，我们将尝试减少相似命令带来的混淆：

```
a=3 let 的简写，a 是局部变量
declare a=3 给局部变量 a 赋值（等同于 let）
declare -x a=3 给全局变量 a 赋值（等同于 export）
export 显示所有全局变量
export a 转换为全局变量
export a=3 给全局变量 a 赋值
let a=3 给局部变量 a 赋值
local a=3 将 a 定义为局部（仅在 shell 函数中）
printenv 用于 export，显示所有全局变量
set 显示所有（局部和全局）变量
unset a 删除变量 a
```
