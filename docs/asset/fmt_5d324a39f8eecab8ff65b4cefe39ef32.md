
| -A radix, --address-radix=radix | 使用 `radix` 作为文件偏移量。对于 `radix`，您可以使用 `d` 表示十进制，`o` 表示八进制，`x` 表示十六进制，或 `n` 表示无。 |

| --help | 显示可用选项。 |

| -J n, --skip-bytes=n | 在每个文件开头跳过 `n` 个字节。 |

| -N n, --read-bytes=n | 每个文件处理不超过 `n` 个字节。 |

| -s [n], --strings[=n] | 输出 `n` 个图形字符组成的字符串。 |

| -t type, --format=type | 使用指定的输出格式类型（参见本节中的输出类型表）。 |

| --traditional | 接受预 POSIX 形式的参数。 |

| -V, --output-duplicates | 抑制使用星号标记行抑制功能。 |

| --version | 输出版本信息并退出。 |

| -w n, --width[=n] | 每输出行写入 `n` 个字节。 |

#### 输出类型

| 名称 | 描述 |
|---|---|
| a | 命名字符 |
| c | ·ASCII 字符或反斜杠转义 |
| d \| n \| | 每整数 `n` 字节的有符号十进制 |
| f \| n \| | 每整数 `n` 字节的浮点数 |
| o \| n \| | 每整数 `n` 字节的八进制 |
| u \| n \| | 每整数 `n` 字节的无符号十进制 |
| x \| n \| | 每整数 `n` 字节的十六进制 |

### paste

```
paste [ 选项 ] [ filename1 filename2 ]
```

将 `*filename1*` 和 `*filename2*` 的对应行合并为制表符分隔的列。如果您愿意，可以合并两个以上的文件。如果未指定 `*文件名*`，该实用程序从标准输入接受输入。

##### 选项

| 使用此选项 | 执行此操作 |
|:----------------|:-----------|
| `-d list, --delimiters=list` | 使用 `*list*` 中的字符代替制表符 |
| `-s, --serial` | 一次粘贴一行 |
| `--help` | 显示可用选项 |
| `--version` | 显示版本号 |

#### 示例

| 此命令 | 执行以下操作 |
|:-------------|:-----------------|
| `paste first.txt second.txt > combined.txt` | 将两个文件 (`*first.txt*` 和 `*second.txt*`) 合并为一个文件 (`*combined.txt*`) 并将输出写入磁盘。 |

### pdf2ps

```
pdf2ps filename output file
```

将便携式文档文件 (`*filename*`) 转换为 PostScript (`*outputfile*`)。

#### 示例

| 此命令 | 执行以下操作 |
|:-------------|:-----------------|
| `pdf2ps resume.pdf resume.ps` | 将 PDF 文件 (`*resume.pdf*`) 翻译为 PostScript 文件 (`*resume.ps*`) 并将结果写入磁盘。 |

### pdftotext

```
pdftotext [ 选项 ] [ 文件名 [ 输出文件 ] ]
```

将便携式文档文件 (`filename`) 转换为纯文本。除非您指定了输出文件，否则写入标准输入。

#### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `pdftotext resume.pdf resume.txt` | 将 PDF 文件 (`resume.pdf`) 翻译为文本文件 (`resume.txt`) 并将结果写入磁盘。 |

### pr

```
pr [ 选项 ] [ 文件名 ]
```

通过添加分页和列来格式化文本文件，以便进行打印。您可以在空格分隔的列表中指定多个文件名，或使用 shell 模式（参见第 4 章中“Shell 模式”一节）。

##### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| --pages=first:last | 从第一页开始打印，可选地在最后一页停止。 |
| -a, --across | 横向打印列，而非纵向。 |
| -c, --show-control-chars | 显示控制字符。 |
| -n, --columns=n | 每页使用 `n` 列。 |
| -d, --double-space | 输出双行间距。 |
| -a[_字符_(_n_)], --expand-tabs[=_字符_(_n_)] | 将 `_字符_` 的宽度扩展到默认制表位宽度 (8 个空格) 或 `_n_` 个空格。 |
| -F, _f_, --form-feed | 使用换页符代替换行符来分隔页面。 |
| --help | 显示可用选项。 |
| -h _字符串_, --header=_字符串_ | 使用 `_字符串_` 作为居中标题，而不是文件名。 |
| -l[_字符_(_n_)], --output-tabs[=_字符_(_n_)] | 用 `_字符_` 替换空格，达到默认制表位宽度 (8 个空格) 或 `_n_` 个空格。 |
| -J, --join-lines | 合并完整行。 |
| -l _n_, --length=_n_ | 将页长设置为 `_n_` 行。 |
| -m, --merge | 并排打印所有文件。 |
| -n[_字符_(_n_)], --number-lines[=_字符_(_n_)] | 对行进行编号。可选地，使用 `_字符_` 代替制表符，并使用 `_n_` 个空格代替默认的八个空格。 |
| -N _n_, --first-line-number=_n_ | 从 `_n_` 开始计数。 |
| -o _n_, --indent=_n_ | 每行缩进 `_n_` 个空格。 |
| -r, --no-file-warnings | 当文件无法打开时省略警告。 |
| -s[_字符_], --separator[_字符_] | 使用 `_字符_` 分隔列。 |
| -S[_字符串_], --sep-string=[_字符串_] | 使用 `_字符串_` 分隔列。 |
| -t, --omit-header | 省略页眉和页脚。 |
| -T, --omit-pagination | 省略页眉和页脚。 |
| -V, --show-nonprinting | 显示非打印字符。 |
| --version | 显示版本号。 |
| -W _n_, --page-width=_n_ | 将页面宽度设置为 `_n_` 个字符。 |
| -w _n_, --width=_n_ | 仅针对多列输出将页面宽度设置为 `_n_` 个字符。 |

#### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `pr magic.txt > lpr` | 准备指定文件 (`magic.txt`) 进行打印，并将输出发送到默认打印队列。 |
| `pr -2 magic.txt > lpr` | 准备指定文件 (`magic.txt`) 以双列文本格式进行打印，并将输出发送到默认打印队列。 |

### ptx

```bash
ptx [ 选项 ] [ 文件名 ]
```

读取输入文件名并生成*置换索引*（显示在上下文中的关键词列表，也称为关键词上下文 [KWIC]）。除非使用 `-G` 选项，否则您可以通过使用 shell 模式指定多个文件名（参见第 4 章中“Shell 模式”一节）。

##### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `-A, --auto-reference` | 在每行开头显示文件名和行号 |
| `-b` *filename*, `--break-file=*filename*` | 从 `*filename*` 获取单词断字符 |
| `-C, --copyright` | 显示程序许可协议 |
| `-F, --flag-truncation=*string*` | 使用 `*string*` 标记行截断 |
| `-i, --ignore-case` | 合并大写和小写以便排序 |
| `-g` *n*, `--gap-size=*n*` | 在输出的列之间使用 `*n*` 个空格 |
| `-G, --traditional` | 禁用 GNU 扩展 |
| `--help` | 显示可用选项 |
| `-i *filename*`, `--ignore-file=*filename*` | 从 `*filename*` 读取忽略词列表 |
| `-M *string*`, `--macro-name=*string*` | 使用 `*string*` 作为宏名称，而不是 `xx` |
| `-O *off*`, `--format=*off*` | 生成 `*off*` 指令的输出 |
