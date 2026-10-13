
# truss — 跟踪系统调用和信号

## 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 | `SUNWcsu` |

## 参见

`sh(1)`, `attributes(5)`

### 概要

...（此处略）

- `-u` 指定用户级函数调用。

`-u [!]lib,...::[ :`

指定用户级函数调用。指定 `lib...` 作为逗号分隔的动态库列表，排除 `.so` 后缀。指定 `func...` 作为逗号分隔的函数列表。在两种情况下，名称都可以包含具有相同含义的名称匹配元字符 `*`, `?`, `[`

# truss 1379

类似于 `sh` 的用法，但应用于库/函数命名空间，而不是文件。空的库或函数列表默认为 `*`，即跟踪库中的所有库或所有函数。在任一列表开头加 `!` 表示指定一个排除列表，即不进行跟踪的库或函数名称。排除一个库会排除该库中的所有函数；忽略库排除列表之后的任何函数列表。

用单个冒号 `:` 将库列表与函数列表隔开，意味着跟踪从库外部进入库的调用，但省略来自同一库内其他函数对该库中函数的调用。双冒号 `::` 意味着跟踪所有调用，无论源自何处。库模式不会修补可执行文件或动态链接器，除非存在精确匹配（例如 `l*` 不匹配 `ld.so(1)`）。要跟踪这些对象中的函数，你必须精确指定名称，例如 `truss -a .out -u ld...`。在此使用 `a` 作为此目的的字面名称。它并不代表可执行文件。跟踪 `a.out` 函数意味着所有调用（默认为 `::`）。

你可以指定 `-u` 选项，它们按从左到右的顺序处理。如果进程通过 `-thread` 链接，执行函数调用的线程 ID 将包含在跟踪输出中。`truss` 会搜索每个库中的动态符号表以查找函数名称，如果符号未被剥离，还会搜索标准符号表。

- `-U [!]lib,...{}[!]func,`

指定会停止进程的用户级函数调用。将指定的函数添加到由 `-u` 指定的集合。如果调用了指定的函数之一，将让进程停止并遗弃（参见 `-T` 选项）。

- `-v [!]syscall,`

显示任何通过地址传递给指定系统调用（如果已跟踪）的结构体内容。显示输入值以及操作系统返回的数值。对于任何既作为输入又作为输出的字段，仅显示输出值。默认是 `-vall`。

- `-w [!]fd,,`

显示对任何自有文件描述符执行 `write()` 的 I/O 缓冲区内容（参见 `-r`）。默认是 `-wall`。

- `-x [!]syscall,`

以原始形式（通常是十六进制）而非符号形式显示指定系统调用（如果已跟踪）的参数。此选项用于那些必须看到原始位才能感到满意的极客。默认 `!` 是 `-xall`。

# 1380

参见 `intro(2)` 获取 `-t`、`-v` 和 `-x` 选项接受的系统调用名称。也接受系统调用号。

如果你使用 `truss` 启动并跟踪指定的命令，并且使用了 `-o` 选项或标准错误被重定向到非终端文件，则 `truss` 运行期间将忽略挂起（hang）、中断（interrupt）和退出（quit）信号。这种行为便于对那些会捕获终端中断和退出信号的交互式程序进行跟踪。

如果跟踪输出仍指向终端，或者正在跟踪现有进程（使用 `-p` 选项），则 `truss` 将拒绝处理挂起、中断和退出信号，而是释放所有进程并退出。这种行为允许你终止跟踪输出并释放之前存在的进程。释放的进程将正常继续，就像它们从未被碰过一样。

## Usage

参见 `largefile(5)` 获取 `truss` 在遇到大于或等于 2 GB（**31 亿字节**）的文件时的行为描述。

## Examples

以下示例显示了终端上 `find(1)` 命令跟踪的前几行输出。

```
castle# truss find -print >find.out

execve("/usr/bin/find", 0FFFF53C, 0FFFF54C) argc = 3

open("/dev/zero", O_RDONLY) = 3

map(0x00000000, 4096, PROT_READ|PROT_WRITE|PROT_EXEC,MAP_PRIVATE,MAP_PRIVATE, 3, 0) = 0xEF7C0000

open("/usr/lib/libc.so.1", O_RDONLY) = 4

stat(4, 0xFFFFFF0D4) = 0

map(0x00000000, 4096, PROT_READ|PROT_EXEC,MAP_PRIVATE, 4, 0) = 0xEF7B00D0

map(0x000007186, 76828, PROT_READ|PROT_EXEC,MAP_PRIVATE,MAP_PRIVATE, 4, 0) = 0xEF762000

munmap(0xEF771000, 29252, PROT_READ|PROT_EXEC,MAP_PRIVATE|MAP_FIXED, 659456) = 0xEF771000

map(0xEF779000, 2968, PROT_READ|PROT_WRITE|PROT_EXEC,MAP_PRIVATE|MAP_FIXED, 3, 0) = 0xEF779000

close(4) = 0

open("/usr/lib/libd.so.1", _) = 4

stat(4, 0xFFFFFF0D4) = 0

map(0xEF7B0000, 4096, PROT_READ|PROT_EXEC,MAP_PRIVATE|MAP_FIXED, 4, 0) = 0xEF7B0000

close(4) = 0

... (显示更多信息)
```

以下示例显示了 `open`, `close`, `read` 和 `write` 系统调用跟踪的前几行。

# truss 1381

```
castle# truss -t open,close,read,write >find.out

open("/dev/zero", O_RDONLY) = 3

open("/usr/lib/libc.so", O_RDONLY) = 4

close(4) = 0

open("/usr/lib/libld.so", O_RDONLY) = 4

close(4) = 0

open("/usr/lib/libc.so", O_RDONLY) = ENOENT

close(3) = 0

open("./", O_RDONLY|NDAY) = 3

close(3) = 0

... (显示更多信息)
```

以下示例在 `truss.out` 中产生了 `spell(1)` 命令的跟踪。

```
castle% truss -f -o spell.out

execve("/usr/bin/spell", 0xFFFF534, 0xFFFF534) argc = 3

open("/dev/zero", O_RDONLY) = 3

map(0x00000000, 4096, PROT_READ|PROT_WRITE|PROT_EXEC,MAP_PRIVATE, 3) = 0xEF7C0000

open("/usr/lib/socket.so", O_RDONLY) = 4

fstat(4) = 0

map(0x00000000, 4096, PROT_READ|PROT_EXEC,MAP_PRIVATE, 4, 0) = 0xEF7B0000

close(4) = 0

map(0x00000000, 4096, PROT_READ|PROT_WRITE|PROT_EXEC,MAP_PRIVATE, _FIXED, 0) = 0xEF7A0000

close(4) = 0

map(0x00000000, 4096, PROT_READ|PROT_WRITE|PROT_EXEC,MAP_PRIVATE, _FIXED, 28 72 =70000000

close(4) = 0

map(0x00000000, 4096, PROT_READ|PROT_WRITE|PROT_EXEC,MAP_PRIVATE, _FIXED, 4) = 0xEF7A0000

munmap(0xEF771000, 29252, PROT_READ|PROT_EXEC,MAP_PRIVATE|MAP_FIXED, 659456) = 0xEF771000

... (显示更多信息)
```

`spell` 是一个脚本，因此你需要 `-f` 选项来不仅跟踪 shell，还有由 shell 创建的进程（`spell` 运行一个八成员流水线）。注意——多多一个进程时，`truss` 作为每个被跟踪进程的控制进程。在 `spell` 命令示例中，`spell` 本身使用 9 个槽（一个给 shell，八给流水线），而 `truss` 又增加了 9 个进程，总共 18 个。

在以下（无聊的）示例中，97% 的输出报告了 `lseek()`、`read()` 和 `write()` 系统调用。

```
$ truss nroff -document >nroff.out
```
