
注意在生成的标题中使用 LaTeX 控制序列。有许多可用的控制序列，包括大多数数学符号、相关的希腊字母以及标准字字符号。LaTeX 保留了以下符号：`$`, `#`, `^`, `_` ，在正常打字过程中必须在它们前面加斜杠。

## 文档类

文档具有类（例如 `letter`, `article`, `book`），必须在文档头部用 

`\documentclass{}`

`\end{document}`

指定符来定义。

## 示例方程

在本节中，我们将看到如何创建一个示例方程。通常你将使用函数指定符：

```
\sqrt{}
```

## 选项

- `--help` 显示关于如何操作的帮助消息。
- `--version` 显示你正在使用的哪个版本的信息。

## 缺陷

偶尔会出现问题。

## 参见

## 图 19-2 文件 example.man

Groff 源文件使用 `groff` 命令编译，并显示在 ASCII 显示器或 X 显示器（`gxditview`）上。详情参见命令示例。

Ghostscript 是 Linux 版本的 Postscript 排 排版系统。Postscript 是一种基于向量的语言，这意味着图像被分解为数学表示的弧、线等。结果文件是系统无关且可扩展的。

本节涵盖的命令包括：

| `colert` | 在图形显示器上显示表格下划线 |
| `eng` | Groff 方程格式化 |
| `gs` | Ghostscript 排版语言 |
| `grog` | 猜测 groff 选项 |
| `gxditview` | 在 X 终端显示 groff 文件 |
| `tbl` | Groff 表格格式化 |
| `tex` | 编译 TeX 源文件 |
| `troff` | 文档格式化（见 groff） |
| `xdvi` | 在 X 窗口显示 .dvi 文件（见 tex） |

## 相关文件

| `/usr/local/share/ghostscript/M.N/*` | 启动文件、工具、字体定义。 |
| `/usr/local/share/ghostscript/fonts/*` | 额外的字体定义。 |
| `/usr/local/share/ghostscript/M.N/examples/*` | 示例文件。 |
| `/usr/local/share/ghostscript/M.N/doc/*` | Ghostscript 文档。 |

## 命令

`colcrt [-] [-2] [file ...]`

此命令是一个用于在无法显示下划线的终端上显示下划线、表格和其他半密集输出的技巧。它的工作原理是通过输出输出双倍行距，并在需要下划线的单词下方空行上放置连字符来实现。

示例：Colcrt 可按如下方式显示 `tbl.n` 表格文件：

`tbl tbl.n | noroff -ms | colcrt - less`

- `-` 不下划线。通常用于显示表格。
- `-2` 打印所有半行，无论其是否为空。这会产生外观的一致性，但会占用空间。

```
eqn [ -rvCNR ] [ -dcc ] [ -Tname ] [ -Mdir ] [ -IF ] [ -sn ] [ -pn ] [ -mn ] [ files... ]
```

`eqn` 配合 `troff` 使用，将方程描述编译为 `troff` 格式。

## 示例：要编译文件 eqn.src：

| `-C` | 允许 `eqn` 识别 `.EQ` 和 `.EN`，即使后面跟着的是非空格或非换行的字符 |
| `-N` | 不允许在分隔符内进行换行 |
| `-v` | 显示版本信息 |
| `-r` | 限制为一次尺寸缩放 |
| `-mn` | 指定最小字号 |
| `-Tname` | 指定输出发送到的设备名称 |
| `-Mdir` | 告诉 `eqn` 在默认目录之前在目录中搜索 `eqnrc` |
| `-R` | 告诉 `eqn` 不要加载 `eqnrc` |
| `-fF` | 等于字体 F 命令 |
| `-sn` | 等于 `gsize n` 命令 |
| `-pn` | 告诉 `eqn` 使上标和下标比周围文本小 `n` 磅，而不是默认的占周围文本大小的 70% |

## `gs [ options ] [ files ] ...`

`gs` 代表 `ghostscript`。Ghostscript 是 PostScript (tm) 排版语言的 Linux 版本。该程序可用于打印或在显示器上显示文档。初始输入来自命令行指定的源文件，但你也可以选择交互式地输入更多命令。

## 命令

示例：将 ghostscript 文件 `example.gs` 打印到打印机 `hplj`：

```
gs -sDEVICE=hplj example.gs
```

- `-` filename arg1 ... 使用此选项时，指定的文件名被视为参数（如常一样），但所有剩余参数将立即定义为 `userdict` 中名为 `ARGUMENTS` 的数组。
- `-Dname=token`, `-dname=token` 向 `systemdict` 添加一个带有给定定义的名称。
- `-Dname`, `-dname` 允许用户在 `systemdict` 中定义一个值为=`null` 的名称。
- `-Sname=string`, `-sname=string` 允许用户向 `systemdict` 添加一个带有指定字符串作为值的名称。
- `-q` 静默操作。
- `-gnumber1xnumber2` 指定设备宽度。
- `-rnumber`, `-rnumber1xnumber2` 指定设备分辨率。
- `-ldirectories` 告诉 `ghostscript` 指定目录是库文件搜索路径的一部分。
- `-` 指定从文件或管道获取标准输入。
- `-dDISKFONTS` 告诉 `ghostscript` 在遇到单个字符时从磁盘加载单个字符轮廓，而不是在加载字体时加载。运行速度较慢，但你可以在内存中放入更多字体。
- `-dNOCACHE` 禁用字符缓存。用于调试。
- `-dNOBIND` 禁用“bind”操作符。仅对调试有用。
- `-dNISPLAY` 禁用显示。
- `-dDISKFONTS` 告诉 `ghostscript` `-dNOCACHE` 禁用。

## 文档格式

- `-dNOPAUSE` 禁用暂停并提示。
- `-dSAFER` 安全模式。
- `-dWRITES` 允许写入。
- `-dYSTEMDICT` 覆盖 `systemdict`。
- `-sOutputFile` 告诉 `ghostscript` 访问指定的设备。
- `-sDEVICE=filename` 输出到指定的文件。

```
groff -tpesivhbENRSXZ [-name] [-Wname ] [-mname ] [-Fdir ] [-Tdev ] [ -ffam ] [-Mdir ] [ -dcs ] [-rcn ] [ -nnum ] [ -olist ] [-Parg ]
```

此命令是 `groff` 的前端。它调用 `troff` 和某些后处理器。可能的设备有：

| `ps` | PostScript (默认) |
| `dvi` | TeX |
| `X75` | 75 dpi |
| `X100` | 100 dpi |
| `ascii` | 打字机设备 |
| `latin1` | 打字机设备 |
| `lj4` | LaserJet4 |

## 命令

**示例：** 为 `groff` 命令猜测所需的选项。`grog` 将查看文件并猜测打印文件需要哪些选项。

```
grog [ files... ]
```

- `-h` 显示帮助。
- `-e` 使用 `eqn` 处理。
- `-t` 使用 `tbl` 处理。
- `-p` 使用 `pic` 处理。
- `-s` 使用 `so` 处理。
- `-v` 显示版本信息。
- `-w` 启用指定的警告。
- `-W` 禁用指定的警告。
- `-z` 抑制输出。
- `-C` 启用兼容模式。
- `-dname=s` 为 `c` 定义一个名称；`c` 必须是字母。
- `-ffam` 指定默认字体。
- `-R` 不加载 `troffrc`。
- `-nnum` 指定起始页码。
- `-olist` 输出列表中的页面，逗号分隔。
- `-rcn`, `-rname=n` 将寄存器设置为 `n`。
- `-Tdev` 告诉 `troff` 为指定的设备准备输出。
- `-Fdir` 在搜索默认 `/usr/lib/groff/font` 之前在指定的目录中搜索 `devname`、`DESC` 文件和字体文件。
- `-Mdir` 在常规 `/usr/lib/groff/tmac` 之前在目录中搜索宏文件。

272

文档格式

`-resolution res` 在指定的的分率下显示。

`-filename string` 指定一个默认文件名。

## X Toolkit 选项

- `-bg color` 指定背景颜色。
- `-bd color` 指定边框颜色。
- `-bw number` 指定边框宽度。
- `-fg color` 指定前景色（文本）颜色。
- `-fn font` 指定字体。
- `-rv` 反转视频——交换前景色和背景设置。
- `-geometry geometry` 指定对窗口大小的偏好设置。
- `-display host:display` 指定宿主机 X 服务器。
- `-xrm resourcestring` 使用指定的资源字符串。
