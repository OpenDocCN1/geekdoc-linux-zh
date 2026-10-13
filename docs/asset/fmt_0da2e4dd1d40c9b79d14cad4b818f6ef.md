
### 描述

`diff3` 比较文件的三个版本，并发布用这些代码标记的不一致文本范围：

```
=== 所有文件都不同。
===1 filename1 不同。
===2 filename2 不同。
===3 filename3 不同。
```

将文件的给定范围转换为其他某些范围的更改类型通过以下方式之一指示：

```
f : n1 a    在文件 f 的行号 n1 之后追加文本，其中 f = 1, 2 或
             3。
f : n1 , n2 c  更改行 n1 到行 n2 范围内的文本。如果 n1 = n2，
               范围可以缩写为 n1。
```

范围的原始内容紧随 `c`（更改）指示之后。当两个文件的内容相同时，将抑制编号较低的文件内容。
以下命令将生成的脚本应用于 `filename`。

```
(cat script; echo '1,$sp') | ed - filename
```

> 注意 - 由单个点 (`.`) 组成的文本行会使 `-e` 失效。大于 64 Kbytes 的无效。

### 选项

- `-3` 生成一个仅包含标记为 `====3` 更改的脚本。
- `-e` 为编辑器 `ed(1)` 生成脚本，将 `filename2` 和 `filename3` 之间的所有更改合并到 `filename` 中，即通常标记为 `==== ====3` 的更改。
- `-E` 生成一个包含 `filename2` 和 `filename3` 之间所有更改的脚本，但以不同方式处理重叠更改（即在列表中标记为 `====` 的更改）。两个文件的重叠行由编辑脚本插入，并用 `<<<<<<n` 包围。
- `-x` 生成一个仅包含标记为 `=====` 更改的脚本。
- `-X` 生成一个仅包含标记为 `====` 更改的脚本，但以 `-E` 选项处理这些更改。

### 示例

以下示例比较了三个文件。`test1` 文件是由命令 `deroff deroff.1` 生成的。`test2` 文件是由命令 `deroff -mm deroff.1` 生成的。`test3` 文件是由命令 `deroff -ml deroff.1` 生成的。

```
castle% diff3 test1 test2 test3
===1
1:6,10c
NAME
deroff remove nroff/troff, tbl, and eqn constructs
SYNOPSIS
deroff
[
2:5a
3:5a
==1
1:25,26c
DESCRIPTION
deroff command deroff remove nroff troff tbl and eqn
constructs
2:19a
3:19a
==1
1:72,73c
OPTIONS
2:64a
3:64a
==1
1:140,141c
ATTRIBUTES
See
2:130a
3:130a
==1
1:145,149c
ATTRIBUTE TYPE ATTRIBUTE VALUE
=
Availability SUNdoc
SEE ALSO
eqn
2:133a
3:133a
==1
1:154,160c
NOTES
deroff
is is not a complete
troff
interpreter,
so it can be confused by subtle constructs.
Most such errors result in too much
the
2:137a
3:137a
castle%
```

### 用法

请参阅 `largefile(5)` 了解 `diff` 在遇到大于或等于 2 Gbytes 文件时的行为。

## 文件

- `/tmp/d????` 用于比较的临时文件。
- `/usr/lib/diff -h` 选项的可执行文件。

### 属性

请参阅 `attributes(5)` 了解以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| Availability CSI | SUNMes Enabled |

## 另请

`diff(1)`, `cmp(1)`, `comm(1)`, `dircmp(1)`, `ed(1)`, `pr(1)`, `sdiff(1)`, `attributes(5)`, `environ(5)`, `largefile(5)`

## diff3 — 三路差异比较

## 摘要

```
/usr/bin/diff3 [-eEX3] filename1 filename2 filename3
```

### 描述

`diff3` 比较文件的三个版本，并发布用这些代码标记的不一致文本范围：

```
=== 所有文件都不同。
===1 filename1 不同。
===2 filename2 不同。
===3 filename3 不同。
```

将文件的给定范围转换为其他某些范围的更改类型通过以下方式之一指示：

```
f : n1 a    在文件 f 的行号 n1 之后追加文本，其中 f = 1, 2 或
             3。
f : n1 , n2 c  更改行 n1 到行 n2 范围内的文本。如果 n1 = n2，
               范围可以缩写为 n1。
```

范围的原始内容紧随 `c`（更改）指示之后。当两个文件的内容相同时，将抑制编号较低的文件内容。
以下命令将生成的脚本应用于 `filename`。

```
(cat script; echo '1,$sp') | ed - filename
```

> 注意 - 由单个点 (`.`) 组成的文本行会使 `-e` 失效。大于64 Kbytes 的无效。

### 选项

- `-3` 生成一个仅包含标记为 `====3` 更改的脚本。
- `-e` 为编辑器 `ed(1)` 生成脚本，将 `filename2` 和 `filename3` 之间的所有更改合并到 `filename` 中，即通常标记为 `==== ====3` 的更改。
- `-E` 生成一个包含 `filename2` 和 `filename3` 之间所有更改的脚本，但以不同方式处理重叠更改（即在列表中标记为 `====` 的更改）。两个文件的重叠行由编辑脚本插入，并用 `<<<<<<n` 包围。
- `-x` 生成一个仅包含标记为 `=====` 更改的脚本。
- `-X` 生成一个仅包含标记为 `====` 更改的脚本，但以 `-E` 选项处理这些更改。

### 示例

以下示例比较了三个文件。`test1` 文件是由命令 `deroff deroff.1` 生成的。`test2` 文件是由命令 `deroff -mm deroff.1` 生成的。`test3` 文件是由命令 `deroff -ml deroff.1` 生成的。

```
castle% diff3 test1 test2 test3
===1
1:6,10c
NAME
deroff remove nroff/troff, tbl, and eqn constructs
SYNOPSIS
deroff
[
2:5a
3:5a
==1
1:25,26c
DESCRIPTION
deroff command deroff remove nroff troff tbl and eqn
constructs
2:19a
3:19a
==1
1:72,73c
OPTIONS
2:64a
3:64a
==1
1:140,141c
ATTRIBUTES
See
2:130a
3:130a
==1
1:145,149c
ATTRIBUTE TYPE ATTRIBUTE VALUE
=
Availability SUNdoc
SEE ALSO
eqn
2:133a
3:133a
==1
1:154,160c
1
)
```

## 环境变量

参见 `environ(5)` 以获取影响 `direcmp` 执行的以下环境变量的描述：`LC_COLLATE`、`LC_TYPE`、`LC_MESSAGES` 和 `NLPATH`。

## 退出状态

- `0` 成功完成。
- `>0` 发生错误。（目录内容之间的差异不不被被视为错误。）

### 属性

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
|---|---|
| 可用性 | SUNmesu |

### 相关

`cmp(1)`, `diff(1)`, `attributes(5)`, `environ(5)`, `largefile(5)`

# dirname — 交付路径名称的部分

### 概要

```
/usr/bin/dirname string
```

### 描述

参见 `basename(1)`。

# dirs — 修改工作目录

### 概要
```
csh
dirs [-1]
```

### 描述

参见 `cd(1)`。

# dis — 对象代码反汇编器

### 概要

```
/usr/ccs/bin/dis [-C] [-o] [-V] [-L] [-d sec] [-D sec] [-F function]
[-l string] [-t sec] file...
```

### 描述
