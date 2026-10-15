
## 环境变量

参见 `environ(5)` 以了解以下影响 `nohup` 执行的环境变量的描述：`LC_TYPE`, `LC_MESSAGE`, `PATH` 和 `NLSPATH`。

`HOME` 确定用户主目录的路径。如果无法在当前目录下创建输出文件 `nohup.out`，则 `nohup` 命令将使用 `HOME` 指定的目录创建该文件。

## 退出状态

- `126` 找到了命令但无法调用。
- `27` `nohup` 发生错误，或未找到命令。

否则，`nohup` 的退出值是命令操作数的退出值。

## 文件

`nohup.out` 如果标准输出是终端且当前目录可写，则为 `nohup` 执行的输出文件。

`$HOME/nohup.out` 如果标准输出是终端且当前目录不可写，则为 `nohup` 执行的输出文件。

### 属性

参见 `attributes(5)` 以了解以下属性的描述：

```
/usr/bin/nohup
```

| 属性类型 | 属性值 |
| 可用性 | SUNwcsu |
| CSI | Enabled |

```
/usr/xpg4/bin/nohup
```

| 属性类型 | 属性值 |
| 可用性 | SUNwxcu4 |
| CSI | Enabled |

## 参见

`batch(1)`, `chmod(1)`, `csh(1)`, `ksh(1)`, `nice(1)`, `sh(1)`, `shell_builtins(1)`, `signal(3C)`, `attributes(5)`, `environ(5)`, `xpg4(5)`

# notify — 控制进程执行

概览

```
csh
notify [%@job-id]...
```

描述

参见 `jobs(1)`。

# nroff — 为显示或行打印机格式化文档

概览

```
/usr/bin/nroff [options] [file]
```

描述

`nroff` 为显示或行打印机格式化文本。参见 `troff(1)`。

`nroff` 处理文件并产生格式化输出。如果没有指定文件，`nroff` 从标准输入读取。如果未指定输出文件，输出发送到标准输出。

`nroff` 的输出可以定向到文件、打印机或终端。

选项

`nroff` 选项控制格式的各个方面：

- `-e` 使用默认字体集。
- `-h` 不打印页眉。
- `-f` 使用指定的字体。
- `-i` 在耗尽输入文件后读取标准输入。
- `-m` 将宏文件附加到输入文件前面。
- `-nW` 为前 N 个页面编号。
- `-q` 不打印来自 `.rd` 请求的输出。
- `-raN` 将寄存器 a（字符）设置为 M。
- `-sN` 每 N 页停止（默认 N1）以便加载或更改页面。
- `-Tname` 为指定的名称设备准备输出。已知名称有：

| 37 | Teletype Corporation Model 37 终端（默认） |
| lp | tn300 | 不具备半行能力的任意行打印机或终端。 |
| 300 | DASI-300。 |
| 300-12 | DASI-300–12pt。 |
| 300S | DASI-300S。 |
| 300S-1 | DASI-300S。 |
| 382 | DASI-382（fancy DTC 382）。 |
| 450 | DASI-450（Diablo Hyterm）。 |
| 450-12 | DASI-450（Diablo Hyterm）12pt。 |
| 832 | AJ 832。 |

注意

`nroff` 命令是 `troff` 套件的一部分。它用于为显示或行打印机格式化文档。`troff` 命令用于更高级的格式化。参见 `troff(1)`。

### 示例

以下示例格式化 `user.guide`，使用 `-me` 宏包并每4页停止一次。

```
castle@ nroff -s4 -me users.guide
```

# 996 nroff

## 环境变量

查看 `environ(5)` 以了解以下影响 `nroff` 执行的环境变量的描述：`LC_CTYPE`、`LC_MESSAGES` 和 `NLSPATH`。

## 文件

- `/usr/tmp/rtmp*` 临时文件。
- `/usr/share/lib/tmac/tmac.*` 标准宏文件。
- `/usr/share/lib/nterm/*n` 用于 `nroff` 的终端驱动表（driving tables）。
- `/usr/share/lib/nterm/README` 终端描述文件的索引。

> 注意 — `/usr/tmp` 目前是指向 `/var/tmp` 的符号链接。

### 属性

查看 `attributes(5)` 以了解以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability (可用性) | 已启用 SUNdoc |

### 另参

`checknr(1)`, `col(1)`, `eqn(1)`, `man(1)`, `tbl(1)`, `traff(1)`, `attributes(5)`, `environ(5)`, `me(5)`, `ms(5)`, `term(5)`

# od — 八进制转储

### 概要

```
/usr/bin/od [-bcCCDdFooSsvxX] [] [file] [-offset_string]
/usr/bin/od [-bcCCDdFooSsvxX] [-A address-base] [-j skip] [-N count] [-t type-string...] [-] [file]
/usr/xpg4/bin/od [-bcCCDdFooSsvxX] [] [file] [-offset_string]
/usr/xpg4/bin/od [-bcCCDdFooSsvxX] [-A address-base] [-j skip] [-N count] [-t type-string...] [-] [file...]
```

### 描述

`od` 命令顺序将每个输入文件复制到标准输出，并根据 `-t` 或 `-bcCCDdFooSsvxX` 选项指定的输出类型转换输入数据。如果你未指定输出类型，默认输出将与你指定的 `-t o2` 相同。你可以使用多个 `-bcCCDdFooSsvxX` 选项指定多种类型。输出行将按照指定的类型顺序为每种类型写入。如果未指定文件，则使用标准输入。`[offset_string]` 操作数与 `-A`、`-j`、`-N` 和 `-t` 互斥。为了本描述，使用了以下术语：

- `word`：16位单位，与系统的字长无关。
- `long word`（长字）：32位单位。
- `double word`（双字）：64位单位。

### 选项

- `-A address-base` 指定输入偏移基。`address-base` 参数必须是一个字符。字符 `d`、`o` 或 `x` 指定偏移基以十进制、八进制或十六进制格式写入。字符 `n` 指定不写出偏移量。除非指定了 `-A`，否则输出行之前将显示输入偏移量（跨多个输入文件的累加），即下一个要写入的字节。此外，最后一个字节之后的字节的偏移量将在处理完所有输入数据后显示。在不使用 `-A address-base` 选项和 `[offset_string]` 操作数的情况下，输入偏移基将以八进制显示。

- `-b` 以八进制解释字节。此选项等同于 `-t ol`。

# /usr/bin/od

- `-c` 以 C 语言解释单字节字符。某些非图形字符将显示为 C 语言转义序列：

- `\0` 空字符。
- `\b` 退格。
- `\f` 换页符。
- `\n` 换行。
- `\r` 回车。
- `\t` 制表符。

其他将以三位八进制数显示。例如：

```
echo "hello world" | od -c
000000 hello world
000001
```
