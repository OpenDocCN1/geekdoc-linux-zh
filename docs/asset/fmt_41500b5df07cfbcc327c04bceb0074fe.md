
# 128

## cd, chdir, pushd, popd, dirs

`cdir` 只是 `cd` 的另一种调用方式。

## C Shell

如果不指定 `dir`，C Shell 内置的 `cd` 使用 shell 参数 `HOME` 的值作为新工作目录。

如果 `dir` 指定了以 `/` 或 `..` 开头的完整路径，则 `dir` 将成为新工作目录。如果 `dir` 不以 `/` 或 `..` 开头，则 `cd` 尝试相对于 `CDPATH` 变量指定的任一路径来查找指定的目录。`CDPATH` 的语法与命令相同，并且与 `PATH` 变量有许多相似之处。`cd` 必须在 `dir` 中具有执行（搜索）权限。由于执行每条命令时都会创建一个新进程，如果将 `cd` 写成普通命令，它将是无效的；因此，它被 C shell 识别并是其内部命令。
（参见 `pwd(1)`, `csh(1)` 和 `chdir(2)`）。

`chdir` 将 shell 的目录更改为 `dir`。如果没有提供参数，则切换到用户的主目录。如果 `dir` 是在当前目录未找到的相对路径名，则在 `cdpath` 变量列出的目录中检查。如果 `dir` 是一个值以 `/` 开头的 shell 变量名，则切换到该值命名的目录。

`pushd` 将目录推入目录栈中。如果没有参数，它会交换前两个元素。你可以使用以下参数：

- 将第 n 个条目旋转到栈顶并使用 `cd` 切换到该目录。
- `dir` 将当前目录推入栈并切换到 `dir`。
- `popd` 弹出目录栈并切换到新的栈顶目录。目录元素从栈顶开始编号为0。你可以使用以下参数：

- 丢弃栈中的第 n 个条目。
- `dirs` 打印目录栈，最近的在左侧；显示的第一个目录是当前目录。使用 `-l` 参数可以生成未缩写的输出；抑制对 `~` 的使用。

## Korn Shell

Korn 内置的 `cd` 命令可以是两种形式之一。在第一种形式中，`cd` 将当前目录更改为 `arg`。如果 `arg` 为空，则切换到上一个目录。shell 变量 `HOME` 是默认 `arg`。变量 `PWD` 是当前目录。shell 变量 `CDPATH` 定义了包含 `arg` 的目录的搜索路径。用冒号（`:`）分隔备选目录名。默认路径为空（指定当前目录）。注意，当前目录是由路径名指定的，它可以紧跟在等号后面或出现在路径列表任何地方冒号分隔符之间。如果 `arg` 以 `/`、`..` 或 `..` 开头，则不使用搜索路径。否则，将在路径中的每个目录中搜索 `arg`。

第二形式的 `cd` 将当前目录名 `PWD` 中的字符串 `old` 替换为字符串 `new`，并尝试切换到此新目录。
`cd` 命令可能由 `rsh` 执行。由于执行每条命令时都会创建一个新进程，如果将 `cd` 写成普通命令，它将是无效的；因此，它被 Korn shell 识别并是其内部命令。（参见 `pwd(1)`, `ksh(1)` 和 `wdir(2)`）。

### 操作数

- `directory` 成为新工作目录的目录的绝对或相对路径名。`cd` 对相对路径名的解释取决于 `CDPATH` 环境变量。

## 环境变量

参见 `environ(5)` 以获取有关影响 `cd` 执行的以下环境变量的描述：`LC_TYPE`, `LC_MESSAGES` 和 `NLSPATH`。

- `CDPATH` 一个用冒号分隔的路径名列表，指向目录。如果目录操作数不以斜杠（`/`）字符开头且第一个组件不是点（`.`）或双点（`..`），则 `cd` 将按照 `CDPATH` 变量中列出的顺序相对于每个目录搜索目录。新工作目录设置为找到的第一个匹配目录。用空字符串代替路径名表示当前目录。如果没有设置 `CDPATH`，则将其视为空字符串。
当定义 `CDPATH` 时，Korn 和 Bourne shell 的 `cd` 命令会将新目录的绝对路径输出到标准输出。如果没有设置 `CDPATH`，则没有输出。

- `HOME` 主目录名称，用于未指定目录操作数的情况。

- `PWD` 当前工作目录的路径名，在 `cd` 切换到该目录后设置。

## 退出状态

- `0` 成功切换目录。
- `>0` 错误。

## 属性

`attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 | SUNWcsu |

## cdc, sccs-cdc

另见
`ncsh(1)`, `ksh(1)`, `pwd(1)`, `sh(1)`, `chdir(2)`, `attributes(5)`, `environ(5)`

## cdc, sccs-cdc — 修改 SCCS Delta 的差异注释

概要
`/usr/ccs/bin/cdc -rsid [-mmr-list] [-y [comment]] s.filename ...`

描述
参见 `sccs-cdc(1)`。

## chdir — 修改工作目录

概要
```
sh
chdir [argument]
sh
chdir [dir]
```

描述
参见 `cd(1)`。

## checkeq — Typeset 数测试

概要
`/usr/bin/checkeq [file] ...`

描述
参见 `eqn(1)`。

## checknr — 检查 nroff troff 输入文件错误

### 概要

`/usr/bin/checknr [-fs] -a`

`checknr` 检查 nroff 和 troff 输入文件的错误。它寻找常见错误，如缺失标签、嵌套错误和无效引用。

## 选项

- `-f` 检查文件和交叉错误。
- `-s` 检查语法错误。
- `-a` 显示发现的所有错误。

# Bug

`checknr` 有一些 bug，例如无法检测复杂文档中的某些类型错误。

## 示例

以下示例了对 `/usr/share/man` 目录下的 `checknr.1` 手页运行 `checknr` 命令。

```
castle$ checknr checknr.1
```

以下示例使用了 `-a` 选项来抑制 `.BI` 和 `.BR` 的“未知命令”消息。

```
castle% checknr -a.BI.BR checknr.1

62: Unknown command: .SB

64: Unknown command: .SB

54: Unmatched \f3

54: Unmatched \f2

54: Unmatched \f1

54: Unmatched \f3

54: Unmatched \f1

57: Unmatched \f3

57: Unmatched \f2

57: Unmatched \f1

57: Unmatched \f3

57: Unmatched \f1

120: Unknown command: .SB

131: Unknown command: .SB

135: Unknown command: .RB

137: Unmatched \f1

116: Unmatched \f1

castle%
```

## 属性 (Attributes)

后续属性的描述请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 | SUNdoc |

## 参见 (See Also)

`eqn(1)`, `nroff(1)`, `troff(1)`, `attributes(5)`, `me(5)`, `ms(5)`

## chgrp — 修改文件组所有权

## 语法概要 (Synopsis)

```
/usr/bin/chgrp [-fhR] group file
```

### 描述 (Description)

你可以使用 `chgrp` 命令更改文件的所属组，前提是你是文件的所有者并且是该文件所属组的成员。`chgrp` 命令会将每个文件操作数所命名文件的组 ID 设置为组操作数所指定的组 ID。

## chgrp

对于每个文件操作数，`chgrp` 执行的操作等同于调用带有以下参数的 `chown(2)` 函数：

- 操作数 `file` 被用作路径参数使用。
- 文件的用户 ID 用作 `owner` 参数。
- 指定的组 ID 用作 `group` 参数。

除非 `chgrp` 是由具有适当权限的进程调用的，否则普通文件的设置用户 ID (set-user-ID) 和设置组 ID (set-group-ID) 位在完成后会被清除；其他文件类型的设置用户 ID 和设置组 ID 位也可能被清除。

操作系统有一个配置选项 `{POSIX_CHOWN_RESTRICTED}`，用于限制所有权的更改。当此选项生效时，文件所有者只能将文件的组更改为其所属的组。无论此选项是否生效，只有超级用户可以任意更改用户 ID。要设置此配置选项，请在 `/etc/system:` 中包含以下行：

```
set rchstown = 1
```

要禁用此选项，请在 `/etc/system:` 中包含以下行：

```
set rchstown = 0
```
