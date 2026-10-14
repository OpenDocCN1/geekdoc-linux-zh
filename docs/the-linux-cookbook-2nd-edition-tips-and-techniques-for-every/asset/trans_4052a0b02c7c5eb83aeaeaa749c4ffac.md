

- `states` `states` 的定义文件
- `synopsys` Synopsys dc shell 脚本语言
- `tcl` TCL 编程语言
- `tcsh` Tcsh shell 脚本语言
- `vba` Microsoft 的 Visual Basic for Applications 语言
- `verilog` Verilog 硬件描述语言
- `vhdl` VHDL 硬件描述语言 (VHDL)
- `vrml` Virtual Reality Modeling Language (VRML97)
- `zsh` Zsh 编程语言

要美化打印一个文件，请将要使用的过滤器的名称作为 -E 选项的参数给出，且选项与参数之间不要有任何空白。

⇒ 以下是一些使用方法。

- 要美化打印 HTML 文件 `index.html`，输入：
  `$ enscript -Ehtml index.html [RET]`
- 要美化打印保存到文件 `important-mail` 中的电子邮件消息，并将其无头输出到名为 `important-mail.ps` 的文件，输入：
  `$ enscript -B -Email -p important-mail.ps important-mail [RET]`
- 要美化打印保存到文件 `important-mail` 中的电子邮件消息，并使用花哨的页眉打印到默认打印机，输入：
  `$ enscript -G -Email important-mail [RET]`

使用特殊的 `--help-pretty-print` 选项来列出你所拥有的 `enscript` 副本支持的语言。

⇒ 要浏览当前支持的语言列表，输入：
`$ enscript --help-pretty-print | less [RET]`

## 15.2.5 使用底纹输出文本

你可以指定一个文本 *underlay*，这是一种印刷水印，会出现在文本页上。要做到这一点，请将文本作为 -u 选项的参数给出，确保选项与文本之间不要跳过任何空格。如果文本多于一个词，请将其引用。

⇒ 要使用默认的 enscript 格式打印文件 intelligence.report，并带有“TOP SECRET”的底纹，输入：

```
$ enscript -u"TOP SECRET" intelligence.report [RET]
```

有许多选项用于指定底纹的属性，如下表所述。

| Option | Description |
|---|---|
| --ul-angle=angle | 指定底纹的角度，单位为度（默认为两个变量的反正切：负的页面高度和其宽度）。 |
| --ul-font=name | 指定底纹的字体和磅值（默认为 200 磅的 Times Roman）。 |
| --ul-gray=number | 指定用于着色底纹的灰度值，取值范围在 0 到 1 之间（默认为 0.8）。 |
| --ul-position=position | 指定底纹的起始位置，以 PostScript 坐标表示。X 位置给出，其前面加上“+”或“-”，后面跟随 Y 位置，Y 位置以同样方式给出（例如，左上角为“+0-0”）。 |
| --ul-style=style | 指定文本样式，要么是“outline”仅打印字符轮廓（默认值），要么是“filled”，字符用灰色填充。 |

## 15.2.6 使用花哨页眉输出文本

要使用花哨的图形页眉输出文本，其中页眉文本以不同灰度块设置，请使用 -G 选项运行 enscript。

⇒ 以下是两种使用方法。

- 要将文本文件 saved-mail 的内容打印到 PostScript 打印机，输入：
  $ enscript -G saved-mail [RET]
- 要制作一个名为 saved-mail.ps 的 PostScript 文件，其中包含文本文件 saved-mail 的内容，并带有花哨页眉，输入：
  $ enscript -G -p saved-mail.ps saved-mail [RET]

没有 -G 选项时，enscript 会输出带有纯文本页眉的文本，页眉以粗体文本打印文件名和最后修改时间。-B 选项，如前所述，会省略所有页眉。

你可以通过将想要使用的文本引用后作为 -b 选项的参数来自定义页眉文本。使用特殊符号 "$%" 在页眉文本中指定当前页码。

⇒ 要打印文本文件 saved-mail 的内容，并在自定义页眉标签中包含当前页码，输入（全部在一行）：

```
$ enscript -b "Page % of the saved email archive" saved-mail [RET]
```

NOTES: 目前没有选项可以将页眉放在除第一页之外的所有页面上，因此如果你需要以这种常见方式格式化文本，首先使用 enscript 输出到没有页眉的文件，然后使用 enscript 输出另一个带页眉的文件，并使用 psselect 将前者的第一页与后者的剩余页面合并（参见 Recipe 20.1.2 [Extracting Pages from a PostScript File], page 452）。

你也可以创建自己的自定义花哨页眉——这在 enscript 手册页的 "CUSTOMIZATION" 部分有描述。

## 15.2.7 以横向方向输出文本

要以横向方向输出文本，即文本逆时针旋转 90 度，请使用 -r 选项。

⇒ 要将文本文件 saved-mail 的内容打印到 PostScript 打印机，并将文本设置为 28 磅 Times Roman 且为横向方向，输入：

```
$ enscript -f "Times-Roman28" -r saved-mail [RET]
```

-r 选项对于通过将 figlet 工具的输出传递给 enscript 来制作水平横幅很有用（参见 Recipe 16.4.1 [Horizontal Text Fonts], page 401）。

⇒ 要以 figlet 字体输出文本 "Quite a long banner" 并将其写入默认打印机，文本设置为 18 磅 Courier 且为横向方向，输入：

```
$ figlet "Quite a long banner" | enscript -B -r -f "Courier18" [RET]
```

## 15.2.8 以垂直切片输出文本

当文本超出右边界时，除非你使用 -c 选项指定在右边界处截断，否则 enscript 会将其换行到下一行。你还可以指定要输出的垂直区域；这些区域称为切片，每个切片从页面的左侧延伸到右侧边界，在此点开始下一个切片。Use --slice=

