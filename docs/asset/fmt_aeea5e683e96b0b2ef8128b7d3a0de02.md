
`WildcardedString` :=

| **

| `String`

| (`String` "***)+ [`String`]

| ("*** `String`)+ [***"]

```
（即 `String` 和 ** 的交替序列）
```

`String` :=="" `Char`* ""

| "%s"

```
```

`Ext` :=="name' ('WildcardedString "")

| 'retype' ('Identifier "")

| 'addtype' ('Identifier "')

```
```

`Identifier` :=="" `Char`* ""

| "%i"

```
```

`Char` :==可便携字符集 (ASCII) 中的一个元素

| 字符串表示范围中的一个字符

```
> 注意：如果过滤表达式为空，则其评估为真（所有对象均满足条件）。

如果过滤表达式中任何子表达式的标识符不存在对象的属性，则包含该标识符的最内层逻辑表达式评估为假。

## 退出状态

- 0 操作执行成功。
- 1 操作失败。

## 属性

请参阅 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNWfns |

### 另请

`printf(1)`, `FN_search_control_t(3N)`, `FN_search_filter_t(3N)`, `f_attr_ext_search(3N)`, `fn_attr_search(3N)`, `attributes(5)`, `fns(5)`

# `fnunbind` — 从 FNS 名称上解除引用

### 概要

`/usr/bin/fnunbind` `composite-name`

## 描述

`fnunbind` 解绑 `composite-name` 的联邦命名服务 (FNS) 引用。
例如，以下命令解绑了名称所绑定的引用。

```
castle$ fnunbind user/jsmith/fs/
```

> 注意 — 对上下文执行 `fnunbind` 会失败，因为除非先使用 `fndroy` 命令销毁该上下文，否则无法解绑。

## 属性

请参阅 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNwfns |

### 另请

`fnbind(1)`, `fnlist(1)`, `fnlookup(1)`, `fnrename(1)`, `fncreate(1M)`, `fndroy(1M)`, `attributes(5)`, `fns(5)`

# `fold` — 折叠行的过滤器

### 概要

`/usr/bin/fold` `[-bs]` `[-w width][-width][file ...]`

## 描述

`fold` 命令是一个过滤器，用于对输入文件的行进行折叠，将行折断以使其最大具有 `width` 列位置（如果指定了 `-b` 选项，则为字节）。通过插入换行符来折断行，使得每个输出行（在本节后文中称为“段”）在不超过指定列位置（或字节）的情况下达到最大长度。行不会在字符中间折断。如果 `width` 小于输入中任何单个字符占据的列数，则行为未定义。

如果在输入中遇到回车（Return）、退格（backspace）或制表符（Tab），且你没有指定 `-b` 选项，则对这些字符进行特殊处理，如下所示：

- 退格（Backspace）：当前行宽计数减 1，尽管计数永远变为负数。在任何退格键字符前后都不立即插入换行符。
- 回车（Return）：将当前行宽计数置为 0。在任何回车字符前后都不立即插入换行符。
- 制表符（Tab）：对于遇到的每个制表符，将当前列指针移动到下一个制表位。制表位位于每个列位置上，因此 n 模 8 等于 1。

> 注意 — 你可以使用 `fold` 和 `cut(1)` 从任意长度的文件创建文本文件。当你需要保持长行的内容连续性时，使用 `fold`。当你需要保持行数（或记录数）不变时，使用 `cut`。

`fold` 常用于将文本文件发送到行式打印机，打印机会截断（trunc）而不是折叠超出打印机打印宽的行（通常为 80 或 132 列宽）。

如果存在下划线，`fold` 可能无法正常工作。

## 选项

- `-b`: 按字节计算宽度而非列位置。
- `-s`: 如果行的某段在第一个 `width` 列位置（或字节）内包含空白字符，则在满足宽度限制的最后一个空白字符后折断行。如果没有满足要求的空白字符，则 `-s` 选项对输入行的该输出段无效。
- `-w width|-width`: 指定最大行长度，以列位置（或你指定的 `-b` 字节）计算。如果 `width` 不是正整数，则返回错误。默认值为 80。

### 操作数

- `file`: 要折叠的文本文件的路径名。如果未指定文件操作数，则使用标准输入。

## 示例

以下示例将文件 `kookaburra` 按每 10 个字符折叠行。

```
castle% fold -w 10 kookaburra
ookaburra
sits in the old gum
tree
Merry merr
y king of i
the bush i
s he
Laugh, koo
kaburra, 1
augh
Gay your l
ife must b
e.
Kookaburra
sits in the old gum
tree
Eating all
the gum
```

以下示例将文件 `kookaburra` 按每 10 个字符折叠行。

```
castle% fold -w 10 kookaburra
ookaburra
sits in the old gum
tree
Merry merr
y king of i
the bush i
s he
Laugh, koo
kaburra, 1
augh
Gay your l
ife must b
e.
Kookaburra
sits in the old gum
tree
Eating all
the gum
```

以下示例将文件 `kookaburra` 按每 10 个字符折叠行。

```
castle% fold -w 10 kookaburra
ookaburra
sits in the old gum
tree
Merry merr
y king of i
the bush i
s he
Laugh, koo
kaburra, 1
augh
Gay your l
ife must b
e.
Kookaburra
sits in the old gum
tree
Eating all
the gum
```

以下示例将文件 `kookaburra` 按每 10 个字符折叠行。

```
castle% fold -w 10 kookaburra
bush i
s he
Laugh, koo
kaburra, 1
augh
Gay your l
ife must b
e.
Kookaburra
sits in the old gum
tree
Eating all
the gum
```

以下示例将文件 `kookaburra` 按每 10 个字符折叠行。

```
castle% fold -w 10 kookaburra
ookaburra
sits in the old gum
tree
Merry merr
y king of i
the bush i
s he
Laugh, koo
kaburra, 1
augh
Gay your l
ife must b
e.
Kookaburra
sits in the old gum
tree
Eating all
the gum
```

以下示例将文件 `kookaburra` 按每 10 个字符折叠行。

```
castle% fold -w 10 kookaburra
ookaburra
sits in the old gum
tree
Merry merr
y king of i
the bush i
s he
Laugh, koo
kaburra, 1
augh
Gay your l
ife must b
e.
Kookaburra
sits in the old gum
tree
Eating all
the gum
```

以下示例将文件 `kookaburra` 按每 10 个字符折叠行。

```
castle% fold -w 10 kookaburra
ookaburra
sits in the old gum
tree
Merry merr
y king of i
the bush i
s he
Laugh, koo
kaburra, 1
augh
Gay your l
ife must b
e.
Kookaburra
sits in the old gum
tree
Eating all
the gum
```

以下示例将文件 `kookaburra` 按每 10 个字符折叠行。

```
