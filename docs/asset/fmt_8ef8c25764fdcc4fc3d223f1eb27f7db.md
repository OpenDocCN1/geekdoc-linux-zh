
显示选项摘要。

- `-V`

  显示程序版本并退出。

####### 参见

`fc-cache`(1) `fc-list`(1) `fc-match`(1) `fc-pattern`(1) `fc-query`(1) `fc-scan`(1)

fontconfig 用户指南，HTML 格式：`/usr/share/doc/fontconfig/fontconfig-user.html`。

###### 作者

本手册页由 Patrick Lam <plam@mit.edu> 编写。

### 名称

`fc-list` - 列出可用字体

### 概要

```
fc-list [ -vVh ] [ --verbose ] [ [ -f format ] [ --format format ] ] [ [ -q ] [ --quiet ] ] [ --version ] [ --help ]
[ pattern [ element... ] ]
```

### 描述

`fc-list` 列出系统上可供使用 fontconfig 的应用程序使用的字体和样式。如果指定了任何元素，则仅打印这些元素。否则，除非请求详细输出，否则将打印家族（family）和样式（style）。

### 选项

此程序遵循常规的 GNU 命令行语法，长选项以两个破折号（`--`）开头。选项摘要如下所示。

- `-v`

  对于每个匹配项，打印整个字体模式的详细输出，如果提供了 `elements`，则打印 `elements`。

- `-f`

  根据格式说明符 `format` 格式化输出。

- `-q`

  抑制所有正常输出。如果没有匹配的字体，则返回 1 作为错误代码。

- `-V`

  显示程序版本并退出。

- `-h`

  显示选项摘要。

- `pattern`

  如果设置此参数，则仅显示匹配 `pattern` 的字体。

- `element`

  如果设置，则显示匹配字体的 `element` 属性。

### 示例

`fc-list`

列出所有字体字面（font faces）。

`fc-list :lang=hi`

列出覆盖印地语（Hindi）的字体字面。

`fc-list : family style file spacing`

列出每个字体字面的文件名和间距值。“:” 是一个空模式，匹配所有字体。

### 参见

`fc-match`(1) `FcFontList`(3) `FcPatternFormat`(3) `fc-cat`(1) `fc-cache`(1) `fc-pattern`(1) `fc-query`(1) `fc-scan`(1)

fontconfig 用户指南，HTML 格式：`/usr/share/doc/fontconfig/fontconfig-user.html`。

### 作者

本手册页由 Keith Packard <keithp@keithp.com> 和 Josselin Mouette <joss@debian.org> 编写。

### 名称

`fc-match` - 匹配可用字体

### 概要

`fc-match` [ -asvVh ] [ --all ] [ --sort ] [ --verbose ] [ [ -f format ] [ --format format ] ] [ --version ] [ --help ]

[ `pattern` [ `element...` ] ]

### 描述

`fc-match` 使用正常的 fontconfig 匹配规则匹配 `pattern`（默认为空模式），以找到可用的最佳字体。如果给出 `--sort`，则显示最佳匹配字体列表的排序结果。`--all` 选项的作用类似于 `--sort`，但对字体列表不进行修剪。

如果指定了任何元素，则仅打印这些元素。否则，除非请求详细输出，否则将打印短文件名（short file name）、家族（family）和样式（style）。

### 选项

此程序遵循常规的 GNU 命令行语法，长选项以两个破折号（`--`）开头。选项摘要如下所示。

- `-a`

  显示最佳匹配字体列表的排序结果，但不进行任何修剪。

- `-s`

  显示最佳匹配字体列表的排序结果。

- `-v`

  对于每个匹配项，打印整个字体模式的详细输出，如果提供了 `elements`，则打印 `elements`。

- `-f`

  根据格式说明符 `format` 格式化输出。

- `-V`

  显示程序版本并退出。

- `-h`

  显示选项摘要。

- `pattern`

  显示匹配 `pattern` 的字体（默认为空模式）。

- `element`

  如果设置，则显示匹配字体的 `element` 属性。

### 参见

`fc-list`(1) `FcFontMatch`(3) `FcFontSort`(3) `FcPatternFormat`(3) `fc-cat`(1) `fc-cache`(1) `fc-pattern`(1) `fc-query`(1) `fc-scan`(1)

fontconfig 用户指南，HTML 格式：`/usr/share/doc/fontconfig/fontconfig-user.html`。

### 作者

本手册页由 Patrick Lam <plam@csail.mit.edu> 更新。

### 名称

`fc-pattern` - 解析并显示模式

### 概要

```
fc-pattern [ -cdVh ] [ --config ] [ --default ] [ [ -f format ] [ --format format ] ] [ --version ] [ --help ]
[ pattern [ element... ] ]
```

### 描述

`fc-pattern` 解析 `pattern`（默认为空模式）并显示解析结果。如果指定了 `--config`，则在对模式进行显示之前执行配置替换。如果指定了 `--default`，则在对模式进行显示之前执行默认值替换。

如果指定了任何元素，则仅打印这些元素。

### 选项

本程序遵循通常的 GNU 命令行语法，长选项以两个短划线（`--`）开头。下方列出了选项的摘要。

- `-c` 对模式执行配置替换。

- `-d` 对模式执行默认值替换。

- `-f` 根据格式说明符 `format` 格式化输出。

- `-V` 显示程序版本并退出。

- `-h` 显示选项摘要。

- `pattern` 解析并显示 `pattern`（默认使用空模式）。

- `element` 如果设置，则显示解析模式的 `element` 属性。

### 参见

`FcNameParse(3)` `FcConfigSubstitute(3)` `FcDefaultSubstitute(3)` `FcPatternPrint(3)`

`FcPatternFormat(3)` `fc-cat(1)` `fc-cache(1)` `fc-list(1)` `fc-match(1)` `fc-query(1)` `fc-scan(1)`

fontconfig 用户指南（HTML 格式）：`/usr/share/doc/fontconfig/fontconfig-user.html`。

### 作者

本手册页由 Behdad Esfahbod <behdad@behdad.org> 更新。

### 名称

`fc-query` - 查询字体文件

### 概要

```
fc-query [ -Vh ]
```

```
[ [ -b ] [ --ignore-blanks ] [ [ -i index ] [ --index index ] ] [ [ -f format ] [ --format format ] ] [ --version ] [ --help ] font-file...
```

### 描述

`fc-query` 使用标准的 fontconfig 规则查询 `font-file`（文件），并打印出每个找到的字体的字体模式。如果指定了 `--index`，则仅查询每个文件的一个字面（face），否则查询所有字面。

### 选项

本程序遵循通常的 GNU 命令行语法，长选项以两个短划线（`--`）开头。下方列出了选项的摘要。

- `-b` 忽略空白以计算语言

- `-i` 仅查询每个文件索引为 `index` 的字面。

- `-f` 根据格式说明符 `format` 格式化输出。

- `-V` 显示程序版本并退出。

- `-h` 显示选项摘要。

- `font-file` 查询 `font-file` 中的字体字面。
