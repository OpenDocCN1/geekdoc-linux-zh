
| :--- | :--- |

| `mkfontdir` | 创建列出工作目录中 Type 1 位图文件的 `fonts.dir` 文件。 |

| `mkfontdir -e /usr/share/enscript` | 创建列出指定目录（`/usr/share/enscript`）中发现的所有字体编码的 `encodings.dir` 文件。 |

### t1ascii

```
t1ascii [ input [ output ]]
```

将 `input` 指定的 Type 1 PFB 字体转换为 PFA（ASCII）格式的字体文件（`output`）。此实用程序是 Type 1 Utilities 包的一部分，可从 <http://www.lcdf.org/~eddtwo/type/> 获取。

另见 `t1binary`。

#### 选项

| 使用此选项 | 执行此操作 |

|:---|:---|

| `--line-length=n`, `-l n` | 将输出中加密行的最大长度设置为 `n` |

### t1asm

```
t1asm [ input [ output ] ]
```

将指定的输入文件（人类可读形式的 Type 1 字体程序）转换为 PFA（十六进制）或 PFB（二进制）格式的输出文件。此实用程序是 Type 1 Utilities 包的一部分，可从 <http://www.lcdf.org/~eddtwo/type/> 获取。

另见 `t1disasm`。

#### 选项

| 使用此选项 | 执行此操作 |

| :--- | :--- |

| `--block-r*=num, -l num` | 将最大输出块长度设置为 `n`（仅限 PFB 文件）。 |

| `--line-length*=n, -l *n*` | 将输出中加密行的最大长度设置为 `n`（仅限 PFA 文件）。 |

| `--pfa, -a` | 以 PFA（ASCII）格式输出。 |

| `--pfb, -b` | 以 PFB（二进制）格式输出。这是默认设置。 |

### t1binary

```
t1binary [ 选项 | [ input.pfa [ output.pfb ] ] ]
```

将由 `input.pfa` 指定的 Type 1 PFA（ASCII）字体转换为 PFB（二进制）格式的字体文件（`output.pfb`）。此实用程序是 Type 1 Utilities 软件包的一部分，该软件包可在 http://www.1cdf.org/~eddtwo/type/ 获取。另请参阅 `tlascii`。

#### 选项

| 使用此选项 | 执行此操作 |

| :--- | :--- |

| `--block-length*=n, -l *n*` | 将 PFB 输出中部分的最大长度设置为 `n`。默认设置为尽可能大地输出部分。 |

#### 示例

| 此命令 | 执行以下操作 |

| :--- | :--- |

| `t1binary myfont.pfa myfont.pfb` | 将 `myfont.pfa`（ASCII 格式）转换为 `myfont.pfb`（二进制格式）。 |

### t1disasm

```
t1disasm [ input [ output ] ]
```

将指定的输入文件（PFA 或 PFB 格式的 Type 1 字体文件）转换为包含人类可读字体程序的输出文件。此实用程序是 Type 1 Utilities 软件包的一部分，该软件包可在 `http://www.1cdf.org/~eddi2/tpc` 获取。

另请参阅 `t1asm`。

### t1unmac

```
t1unmac macintosh font [ output ]
```

转换 Macintosh 字体（以下任一格式的 Macintosh Type 1 字体文件：MacBinary I 或 II、AppleSingle、BinHex、AppleDouble，或原始资源分支）。该实用程序创建 PFA（十六进制）或 PFB（二进制）格式的输出文件。默认输出为 PFB。此实用程序是 Type 1 Utilities 软件包的一部分，该软件包可在 `http://www.1cdf.org/~eddi2/tpc/` 获取。

#### 选项

| 使用此选项 | 执行此操作 |

|---|---|

| `-a, --pfa` | 以 PFA（ASCII）格式输出。 |

| `--appledouble` | 指示输入是 AppleDouble 文件。 |

| `--applesingle` | 指示输入是 AppleSingle 文件。 |

| `-b, --pfb` | 以 PFB（二进制）格式输出。 |

| `-binhex` | 指示输入是 BinHex 文件。 |

| `-macbinary` | 指示输入是 MacBinary 文件。这是默认设置。 |

| `-r, --raw` | 指示输入是原始资源分支。 |

### ttf2pt1

```
ttf2pt1 [ 选项 | truetype font type] font
```

将指定的 TrueType 字体转换为 Type 1 字体文件（PFA 或 PFB 格式）。要获取 `ttf2pt1`，请访问 http://www.netspace.net.au/~mheath/ttf2pt1。

#### 选项

| 使用此选项 | 执行此操作 |

| :--- | :--- |

| `-A` | 创建字体度量（AFM）文件。 |

| `-b` | 创建 PFB 文件。 |

| `-e` | 创建 PFA 文件。 |

| `-f` | 跳过尝试猜测 ForceBold 参数。 |

| `-h` | 禁用提示（hints）的自动生成。 |

| `-l language` | 提取指定语言的字符。您可以使用以下选项：latin1, latin2, latin4, latin5, bulgarian, and russian。 |

| `-o` | 禁用轮廓代码优化。 |

| `-r` | 禁用轮廓 di_action 反转。 |

| `-s` | 禁用轮廓平滑。 |

| `-t` | 禁用自动缩放。 |

| `-v n` | 将字体重新缩放到指定大小（`n`）的大写字母。 |

| `-w` | 尝试更正字形宽度。 |

#### 示例

| 此命令 | 执行以下操作 |

| :--- | :--- |

| `ttf2pt1 myfont.ttf myfont.pfa` | 将指定的 TrueType 字体（`myfont.ttf`）转换为 Type 1 字体（`myfont.pfa`）。 |

### ttmkfdir

```
ttmkfdir [ 选项 ] –o fonts.scale
```

创建 `fonts.scale` 文件，列出当前工作目录中可用的 TrueType 字体。TrueType 字体文件名不得包含大写字母。使用此实用程序后，请运行 `mkfontdir`。XFree86 无法直接处理 TrueType 字体。要在系统中使用 TrueType 字体，必须安装并运行 TrueType 字体服务器。如果不想安装 TrueType 兼容的字体服务器，可以通过将 TrueType 字体转换为 Type 1（PostScript）字体来使用它们。

另请参阅 `ttf2pt1`。

#### 选项

| 使用此选项 | 执行此操作 |

| :--- | :--- |

| `–c` | 对编码表使用较不严格的完整性测试。 |

| `–d directory` | 扫描指定目录中的 TrueType 文件，如果未指定目录，则扫描当前工作目录。 |

| `–f name` | 对未知字体供应商使用指定的 foundry 名称。默认为 misc。 |

| `–m n` | 指定每个编码的最大缺失字符数（`n`）。默认为 5。 |

| `–o filename` | 将输出写入指定的文件名。使用 `fonts.scale`。 |

| `–P` | 使用 panose 信息。 |

#### 示例

| 此命令 | 执行以下操作 |

| :--- | :--- |

| `ttmkfdir –o fonts.scale` | 创建包含当前工作目录中 TrueType 字体信息的 `fonts.scale` 文件。 |

### type1inst

```
type1inst [ 选项 ]
```

在包含可缩放 Type 1 字体的目录中运行时，创建 X 服务器所需以处理这些字体的 `fonts.scale` 文件。此实用程序还生成 `fonts.dir` 文件。您可以从该实用程序的官方分发站点获取 `type1inst` 的副本，该站点位于 http://metalab.unc.edu/pub/Linux/X11/utls。

另请参阅 `mkfontdir`, `ttmkfdir`。

#### 选项

| 使用此选项 | 执行此操作 |

|---|---|

| `-no` | 跳过创建 `fontmap` 文件 |
