
| Z | 零终止的 ASCII 字符串，将用零填充。 |
| b | 位字符串，位升序顺序，类似于 `vec()`。 |
| B | 位字符串，位降序顺序。 |
| h | 十六进制字符串（低半字节组在前）。 |
| H | 十六进制字符串（高半字节组在前）。 |
| c | 有符号字符值。 |
| C | 无符号字符值。 |
| s | 有符号短型值。 |
| S | 无符号短型值（恰好 16 位）。 |
| i | 有符号整数值。 |
| I | 无符号整数值（至少 32 位）。 |
| l | 有符号长型值。 |
| L | 无符号长型值（恰 32 位）。 |

表 B.3 续: `pack` 和 `unpack` 的代码

| 代码 | 含义 |
| :--- | :--- |
| n | 网络字节（大端序）下的短整数（恰 16 位）。 |
| N | 网络字节（大端序）下的短整数（恰 32 位）。 |
| v | 网络字节（大端序）下的短整数（16 位）。 |
| V | 网络字节（大端序）下的短整数（32 位）。 |
| q | 有符号四字节型（64 位）。 |
| Q | 无符号四字节型（64 位）。 |
| f | 单精度浮点数。 |
| d | 双精度浮点数。 |
| p | 指向字符串。 |
| P | 指向字符串。 |
| u | 无符号整数。 |
| w | 无符号整数。 |
| x | 有符号字节。 |
| X | 无符号字节。 |
| y | 有符号短型。 |
| z | 无符号短型。 |

## `pop`

### `pop @array`

移除并返回 `@array` 的最后一个元素。如果 `@array` 为空，返回 `undef`。

## `pos`

### `pos $scalar`

返回在 `$scalar` 上执行上次搜索的偏移量。如果省略 `$scalar`，则使用 `$_`。

## `print`

### `print FILEHANDLE LIST`

### `print LIST`

将 `LIST` 的内容打印到输出。如果指定了 `FILEHANDLE`，则发送到文件。默认使用当前输出设备（`STDOUT`）。如果省略 `LIST`，`print()` 函数打印 `$_`。

## `printf FILEHANDLE format, LIST`

### `printf $format, LIST`

类似于 C 语言的 `printf` 函数。解析 `$format` 并用 `LIST` 中的值替换 `%` 标记。最常见的标记是用于字符串的 `%s` 和用于整数的 `%d`。还有其他选项；详情请参考 C 参考。

与 `print()` 类似，如果指定了 `FILEHANDLE`，输出到文件。如果省略 `FILEHANDLE`，输出到当前输出设备。通常，`print()` 比 `printf()` 更高效。

## `push @array, LIST`

将 `LIST` 中的元素附加到 `@array` 末尾，返回数组的新元素数量。

## `quotemeta $string`

返回 `$string` 的副本，其中所有非字母数字字符都带有反斜杠。如果省略 `$string`，则使用 `$_`。

## `rand`

### `rand $number`

返回 0 到 `$number` 值之间的随机小数。`$number` 必须为正数，如果省略，则使用 1。

## `read FILEHANDLE, $scalar, $length`

### `read FILEHANDLE, $scalar, $length, $offset`

从 `FILEHANDLE` 读取 `$length` 字节数据到变量 `$scalar`。

返回实际读取的字节数，在发生错误时返回 `undef`。`$scalar` 将根据读取长度增长或缩小。如果没有指定 `$offset`，则假设其为 0。

## `readdir DIRHANDLE`

返回由 `opendir()` 打开的目录的下一个目录项。

如果作为列表上下文中使用，则返回目录的剩余项。如果没有更多项，在标量上下文中返回 `undef`，在列表上下文中返回空列表。

# 目录 B

## `readlink`

### `readlink EXPR`

如果实现了符号链接，则返回符号链接的值。如果没有实现符号链接，则产生致命错误。如果发生系统错误，则返回未定义的值并设置 `$!` (`errno`)。如果省略了 `EXPR`，则使用 `$_`。

## `recv SOCKET, $scalar, $len, $flags`

在 `socket` 上接收消息。数据从指定的 `SOCKET` 文件句柄读取到变量 `$scalar` 变量中，最多读取 `$len` 字节。`flags` 标志定义在 `recvfrom()` Unix 系统调用中。

## `redo`

### `redo LABEL`

重新启动循环块，而不重新评估条件。如果存在条件，则不执行。如果省略了 `LABEL`，该命令将指向最内层包围的循环。

## `ref`

### `ref EXPR`

如果 `EXPR` 是一个引用则返回 `true`，否则返回 `false`。如果未指定 `EXPR`，则使用 `$_`。如果返回的值为真，它将根据所引用的类型而变化。内置类型有 `SCALAR`、`ARRAY`、`HASH`、`CODE`、`REF`、`GLOB` 和 `LVALUE`。如果 `EXPR` 指向一个经过修饰（blessed）的对象，则返回该对象的包名。

## `rename $oldname, $newname`

将文件 `$oldname` 的名称更改为 `$newname`。成功返回 `true`，失败返回 `false`。此函数无法跨越文件系统边界工作。

## `reset`

### `reset EXPR`

清除名称以 `EXPR` 字母开头的变量的值。可以使用范围指定多个字母。如果未指定 `EXPR`，则使用特殊变量 `??`（两个问号）。`reset()` 函数始终返回 `true`。如果你使用 `return`，你将重置所有的环境变量变量 `ENV` 和 `ARGV`，这可能不是你想要的。

## `return`

### `return EXPR`

在子程序执行结束时返回参数的列表。如果没有找到 `return` 语句，子程序将始终返回其最后一个表达式的结果。

## `reverse @list`

### `reverse $string`

反转 `@list` 中元素的顺序，或者反转 `$string` 中字符的顺序。

## `rewinddir DIRHANDLE`

将当前位置设置为目录的开头，供在 `DIRHANDLE` 上的 `readdir()` 函数使用。

## `index $str, $substring`

### `index $str, $substring, $position`

获取 `$substring` 在 `$str` 中最后一次出现的位置。除非指定了位置，否则从 `$string` 的末尾开始搜索。如果指定了位置，函数将从字符串末尾的位置开始搜索。

## `rmdir`

### `rmdir $filename`

删除由 `$filename` 指定目录，但仅当该目录为空时。如果未指定 `$filename`，则使用 `$_`。成功返回 `true`，失败返回 `false`，错误代码包含在 `$!` 中。

## `s/PATTERN/REPLACEMENT/egimosx`

在字符串中搜索 `PATTERN` 并将其替换为 `REPLACEMENT`。返回替换的次数，或一个假值。

`s///` 运算符的功能类似于 `//` 运算符。如果左侧没有用 `~` 指定其他变量，它对 `$_` 操作，如果你不喜欢斜杠，可以使用不同的分隔符。以下是一些示例：

- # 替换 `$_` 中第一个 `dogs` 为 `cats`

  `s/dogs/cats/`

- # 忽略大小写，将 `$str` 中所有的 Python 或 PHP 替换为 Perl。

  `$str ~ s/P(ython|HP)/Perl/ig;`

表 B.4 提供了选项的完整列表。

| 选项 | 定义 |
| --- | --- |
| e | 将 `REPLACEMENT` 作为代码求值。 |
| g | 替换字符串中的所有出现项。如果没有 `/g`，则仅替换第一个匹配项。 |
| I | 执行不区分大小写的匹配。 |
| m | 将字符串视为多行。 |
| o | 仅编译一次模式。这仅在模式为变量时才有意义。 |
| s | 将字符串视为单行。 |
| x | 使用扩展正则表达式。忽略空格，并在模式中允许注释。这使得记录复杂的表达式变得更容易。 |

## `scalar EXPR`

强制将 `EXPR` 解释为标量语境（`scalar` context），并返回 `EXPR` 的值。

## `seek FILEHANDLE, $position, $startingpoint`

类似于 `seek()` 和 `fseek()` Unix 系统调用；设置 `FILEHANDLE` 的文件指针。`$startingpoint` 的值为 0，表示从文件开头开始设置位置；1，表示相对于文件中的当前位置设置位置；2，表示相对于文件末尾设置位置。成功返回 1，失败返回 0。

## `seekdir DIRHANDLE, $position`

将 `DIRHANDLE` 上 `readdir()` 的当前位置移动到 `$position`，该值必须由 `telldir()` 返回。

## `select FILEHANDLE`
