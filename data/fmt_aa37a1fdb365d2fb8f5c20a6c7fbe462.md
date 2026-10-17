
```
+   1 Kookaburra sits in the old gum tree
2 Merry merry king of the bush is he
3 Laugh, kookaburra, laugh, kookaburra
4 Gay your life must be.
5
6 Kookaburra sits in the old gum tree
7 Eating all the gumdrops he can see
8 Stop, kookaburra, stop, kookaburra
9 Leave some there for me.
```

以下示例使用 `-b` 选项显示行号，但省略空行的行号。将结果与 `-n` 命令的结果进行比较。
`castle% cat -b kookaburra`

```
+   1 Kookaburra sits in in the old gum tree
2 Merry merry king of the bush is he
3 Laugh, kookaburra, laugh, kookaburra
4 Gay your life must be.

+   5 Kookaburra sits in the old gum tree
6 Eating all the gumdrops he can see
7 Stop, kookaburra, stop, kookaburra
8 Leave some for me.
```

以下示例显示三个文件的内容，其中前两个文件不存在。它使用 `-s` 选项抑制关于不存在文件的错误信息。
`castle% cat file1 file2 kookaburra`
`cat: cannot open file1`
`cat: cannot open file2`

Kookaburra sits in the old gum tree
Merry merry king of the bush is he
Laugh, kookaburra, laugh, kookaburra
Gay your life must be.

Kookaburra sits in the old gum tree
Eating all the gumdrops he can see
Stop, kookaburra, stop, kookaburra
Leave some for me.

`castle% cat -s file1 file2 kookaburra`
Kookaburra sits in the old gum tree
Merry merry king of the bush is he
Laugh, kookaburra, laugh, kookaburra
Gay your life must be.

Kookaburra sits in the old gum tree
Eating all the gumdrops he can see
Stop, kookaburra, stop, kookaburra
Leave some for me.

以下示例使用 `-v` 选项显示文件 `kookaburra` 中的所有非打印字符。该文件中唯一的非打印字符是每行末尾的换行符，它们被显示为美元符号 (`$`)。
`castle% cat -v kookaburra`

Kookaburra sits in the old gum tree$
Merry merry king of the bush is he$
Laugh, kookaburra, laugh, kookaburra$
Gay your life must be.$
$

Kookaburra sits in the old gum tree$
Eating all the gumdrops he can see$
Stop, kookaburra, stop, kookaburra$
Leave some for me.$
`castle%`

## 环境变量

请参阅 `environ(5)` 获取以下影响 `cat` 执行的环境变量的描述：`LC_TYPE`、`LC_MESSAGES` 和 `NLPATH`。

## 退出状态

- `0` 所有输入文件均成功输出。
- `> 0` 发生错误。

### 属性

请参阅 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNWcsu Enabled |

### 相关

`touch(1)`, `environ(5)`, `attributes(5)`, `largefile(5)`

## cc — C 编译器

### 概要

```
/usr/ucb/cc [options]
```

### 描述

`/usr/ucb/cc` 是 BSD 兼容包 C 编译器的接口。它是一个查找指向 C 编译器的链接 `/usr/ccs/bin/ucbcc` 的脚本。`/usr/ccs/bin/ucbcc` 在 SPROcc 包中可用，其默认位置为 `/opt/SUNWspro`。`/usr/ucb/cc` 与 `/usr/ccs/bin/ucbcc` 相同，不同在于它使用 BSD 头文件并在基础库之前链接 BSD 库。`/opt/SUNWspro/man/man/acc.1` 手册页仅在 SPROcc 包中可用。

### 选项

- `/usr/ucb/cc` 接受与 `/usr/ccs/bin/ucbcc` 相同的选项，但有下述例外。
- `-Idir` 在搜索常规目录之前，搜索名称不以斜杠 (`/`) 开头的包含文件。按指定的顺序使用多个 `-I` 选项。预处理器首先在包含源文件的目录中搜索 `#include` 文件，然后是在带有 `-I` 选项命名的目录（如果有），然后是 `/usr/ucinclude`，最后是 `/usr/include`。

`-Ldir` 将目录添加到 `/usr/ccs/bin/ubcc` 搜索库的目录列表中。将此选项传递给 `/usr/ccs/bin/ld` 和 `/usr/ccs/lib`。在 `/usr/ccs/lib` 之前搜索用此选项指定的目录。

`-Ydir` 更改默认目录。注意，此选项可能会产生意外结果，不应使用。

## 退出状态

- `0` 编译成功或链接成功。
- `> 0` 发生错误。

## 文件

- `/usr/ccs/bin/ld`
- `/usr/lib/cc`
- `/usr/ucinclude`
- `/usr/lib/libcc`
- `/usr/lib/socket`
- `/usr/lib/nsl`
- `/usr/lib/elf`
- `/usr/lib/aio`

### 属性

参阅以下：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNWcpu |

### 相关

`ld(1)`, `a.out(4)`, `attributes(5)`

## cd, chdir, pushd, popd, dirs — 工作目录

### 概要

```
/usr/bin/cd [directory]
```
