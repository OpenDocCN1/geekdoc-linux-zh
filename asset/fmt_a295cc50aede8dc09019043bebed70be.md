
## `tbl` [ -Cv ] [ files... ]

此命令将表格描述编译为 troff 命令。示例：通常由 `groff` 自动调用。要编译文件 `tbl.src`：

```
tbl tbl.src
```

- `-C` 即使在紧跟非空格或换行符的字符时也识别 `.TS` 和 `.TE` 文件。
- `-v` 显示版本号。

## 命令

### `tex`

`tex` 命令将（某种）TeX 源文件编译为可移动且可打印的设备无关 (dvi) 文件。

示例：将文件 `example.tex` 编译为设备无关的中间文件 `example.dvi`：

```
tex example.tex
```

- `-ipc`, `-ipc-start` 将输出写入套接字以及 `.dvi` 文件。使用 `-ipc-start` 还会打开一个服务器程序来读取输出。
- `-mktex=FILETYPE`, `-no-mktex=FILETYPE` 开启或关闭与 `FILETYPE` 相关的 `mktex` 脚本。对于 `FILETYPE`，有意义的值是 `tex` 和 `tmf`。
- `-mlitex` 如果为 `INITEX`，则启用 MLTeX 扩展（如 `charsubdef`）。如果程序名为 `mltex`，则隐式设置。
- `-output-comment=STRING` 使用指定的字符串作为 DVI 文件的注释。
- `-shell-escape` 启用 `\write18{SHELL-COMMAND}` 功能。

```
troff [-abivzCER ] [ -name] [ -Wname ] [ -dcs ] [ -tfam ] [ -mname ] [-nnum] [ -olist ] [ -rcn ] [ -Tname ] [ -Fdir ] [ -Mdir ] [ files... ]
```

`troff` 命令用于格式化文档。通常由 `groff` 调用（见上文）。

- `-a` 生成 ASCII 输出。
- `-b` 在每个警告或错误时显示回溯。
- `-i` 告诉 `tro` 在处理完文件后从标准输入读取。
- `-v` 显示版本信息。

## 文档格式

- `-wname` 启用指定的警告。
- `-W` 禁用指定的警告。
- `-E` 禁用错误消息。
- `-z` 抑制格式化后的输出。
- `-C` 启用兼容模式。
- `-dcs`, `-dname=s` 将 `c` 或 `name` 定义为字符串 `s`；`c` 必须是单字母名称。
- `-ffam` 指定 `fam` 为默认字体族。
- `-mname` 读取文件 `tmac name`，而不是在 `/usr/lib/groff/tmac` 中搜索它。
- `-R` 不加载 `troffrc`。
- `-nnum` 指定起始页码。
- `-olist` 仅输出列表中指定的页面，逗号分隔的页范围列表。
- `-rcn`, `-rname=n` 将数字寄存器 `c` 或 `name` 设置为 `n`。
- `-Tdevice` 告诉 `troff` 为指定的设备准备输出而非 `ps`。
- `-Fdir` 在指定的指定的目录中搜索子目录 `devname`、`DESC` 文件和字体文件，然后再搜索默认目录（`/usr/lib/groff/font`）。
- `-Mdir` 在常规的 `/usr/lib/groff/tmac` 之前搜索目录中的宏文件。

```
xdvi [+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]
```

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。

`[+page] [-s shrink] [-S density] [-nogrey] [-gamma g] [-p pixels] [-margins dimen] [-sidargin dimen] [-topmargin dimen] [-offsets dimen] [-xoffset dimen]`

`xdvi` 在指定的的分率下显示。
