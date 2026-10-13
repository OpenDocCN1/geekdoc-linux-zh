
## 描述

使用 `nl` 命令为文件行编号。`nl` 命令将页面划分为逻辑段，并在每个新页的顶部重新开始计数。一个逻辑页面由头部（header）、正文（body）和页脚（footer）组成。空部分是有效的。

`nl` 命令从指定的文件（如果没有指定文件，则从标准输入）读取行，并将行复制到标准输出。根据指定的命令行选项，在左侧对行编号。

头部、正文和页脚可以独立使用不同的行计数选项。例如，`-bt`（默认值）对正文部分的非空行进行编号，不对头部和页脚部分的任何行进行编号。逻辑页部分的开始由仅包含分隔符字符的输入行来指示。

| 行内容 | 开始于 |
|---|---|
| `::` | 头部 (Header)。 |
| `::` | 正文 (Body)。 |
| `:` | 页脚 (Footer)。 |

除非另有规定，`nl` 假设读取的文本位于单个逻辑页文中。

### 注意

POSIX 和 C 区域使用国际化正则表达式。在其他区域中，如果满足以下两个条件，也会使用国际化正则表达式：

- `/usr/lib/locale/locale/LC_COLLATE/CollTable` 存在，且
- `/usr/lib/locale/locale/LC_COLLATE/coll.so` 不存在；
否则，使用简单正则表达式。国际化正则表达式的解释见 `regex(5)`。简单正则表达式的解释见 `regex(5)`。

## 选项

你可以以任何顺序指定选项，并将它们与可选的文件名混合使用。你只能命名一个文件。当命令行上没有输入选项时，将使用指定的默认值。`/usr/xpg4/bin/nl` 选项需要选项参数。空格字符可以分隔选项和参数。`/usr/bin/nl` 选项可以带有参数。如果你没有为 `/usr/bin/nl` 指定参数，则使用默认选项。

- `-btype` 指定哪些逻辑页文行需要编号。识别的类型及其含义为：
  - `a` 对所有行编号。
  - `t` 对所有非空行编号。
  - `n` 不编号。
  - `pexp` 仅对包含 `exp` 中指定的正则表达式的行编号。逻辑页文的默认类型为 `t`（文本行编号）。

- `-ftype` 与 `-btype` 相同，页脚除外。逻辑页脚的默认类型为 `n`（不编号）。
- `delim` 将指定逻辑页段开始的两个分隔符从默认字符（:）更改为用户指定的字符。如果你只输入一个字符，第二个字符将保持默认字符（.）。在 `-d` 和分隔符之间不要包含空格。要输入反斜杠，请使用两个反斜杠。

- `-htype` 与 `-btype` 相同，头部除外。逻辑页头的默认类型为 `n`（不编号）。
- `iincr` 指定用于逻辑页行计数的递增值。
  默认 `incr` 为 `1`。

- `-lnum` 指定将多少空行视为一个。例如，`-12` 导致第二个相邻的空行被编号（如果设置了相应的 `-ha,-ba,或 -fa` 选项）。默认 `num` 为 `1`。

- `-nformat` 指定行号格式。识别的值为：
  - `ln` 左对齐，抑制前导零。
  - `rn` 右对齐，抑制前导零。
  - `rz` 右对齐，保留前导零。默认格式为 `rn`（右对齐）。

- `-p` 不在逻辑页分隔符处重新编号。
- `ssep` 指定用于分隔行号和相应文本行的字符。默认 `sep` 为制表符。

- `-vstartnum` 指定用于逻辑页行计数的初始值。默认 `startnum` 为 `1`。

### 941

- `-wwidth` 指定用于行号的字符数。
  默认宽度为 `6`。

### 操作数

`file` 要行编号的文本文件的路径名。

## 示例

以下示例使用默认选项为 `kookaburra-1` 文件添加行号。

```
castle% nl kookaburra-1

1 Kookaburra sits in the old gum tree

2 Merry merry king of the bush is he.

3 Laugh, kookaburra, laugh, kookaburra

4 Gay your life must be.

5

6 Kookaburra sits in the old gum tree

7 Eating all the gumdrops he can see.

8 Stop, kookaburra, stop, kookaburra

9 Leave some there for me.

castle%
```

以下命令将页文的第一行编号为 10，页文的第二行编号为 20，第三行为 30，以此此类推。逻辑分隔符为。

```
castle% -v10 -i10 -d+ kookaburra-2

10 Kookaburra sits in the old gum tree

20 Merry merry king of the bush is he.

30 Laugh, kookaburra, laugh, kookaburra

40 Gay your life must be.

50

60 Kookaburra sits in the old gum tree

70 Eating all the gumdrops he can see.

80 Stop, kookaburra, stop, kookaburra

90 Leave some there for me.

castle%
```

## 环境变量

参见 `environ(5)` 以获取以下影响 `nl` 执行的变量的描述：`LC_COLLATE`, `LC_TYPE`, 和 `NLPATH`。

## 退出状态

```
0 成功完成。

>0 发生错误。
```

# 942 nm

## 文件

`/usr/lib/locale/locale/LC_COLLATE/CollTable`
包含字符串转换的共享对象。
`/usr/lib/locale/locale/LC_COLLATE/coll.so`
由 local 生成排序表。

## 属性

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| SUNW | |
| SUNWx | |

## 参见

`pr(1)`, `attributes(5)`, `regex(5)`, `regexp(5)`

# nm — 打印对象符号列表

## 语法

```
/usr/ccs/bin/nm [-ACDhlnPRsTuVv] [-efox] [-u] [-t format] file...
```
