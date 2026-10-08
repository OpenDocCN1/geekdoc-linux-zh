

# postprint

# postprint — 文本文件的 PostScript 翻译器

# 概要

```
/usr/lib/lp/postprint [-c num] [-f name] [-l num] [-m num] [-n num]
[-o list] [-p mode] [-r num] [-s num] [-t num] [-x num] [-y num]
[file...]
/usr/lib/lp/postscript/postprint
```

# 描述

postprint 过滤器将文本文件转换为 PostScript 并将结果写入标准输出。如果您未指定任何文件，或者 - 是输入文件之一，则读取标准输入。

# 选项

- -c num 每页打印 num 份。默认情况下只打印一份。
- -f name 使用指定的字体名称文件。您可以使用 PostScript 字体，尽管使用等宽字体效果获得最佳。默认字体为 Courier。
- -l num 设置每页长度为 num 行。默认情况下，num 为 66。允许将 num 设为 0，此时 postprint 将根据页面尺寸估计一个值。
- -m num 通过因子 num 放大每个逻辑页面。关于位于每个页面左上角的原点均匀缩放页面。默认放大倍数为 1.0。
- -n num 在每张纸上打印 num 个逻辑页面，num 可以任意正整数。默认情况下，num 设为 1。
- -o list 打印逗号分隔列表中给出的页码。列表包含多个数字范围 N1-N2。缺失 N1 表示最低页码，缺失 N2 表示最高页。页面范围是逻辑页面的表达式，而不是物理纸张。例如，如果您在每张纸上打印两个逻辑页面并指定范围为 4，则会打印两张包含四个布局的纸。如果您在请求每页纸打印一个逻辑页面时指定页码范围为 3-4，则只会打印第 3 和第 4 页布局，它们将出现在一张物理纸上。
- -p mode 以 p（竖向）或 l（横向）模式打印文件。模式的第一个字符有效。默认模式为竖向。
- -r num 选择换行符行为。如果 num 为 0 则忽略换行符，如果 num 为 1 则跳转到第 1 列，如果 num 为 2 则生成新行。默认 num 为 0。
- -s num 使用字号 num 打印文件。在横向模式下打印时，将根据设备成像区域的因子缩放 num。竖向模式的默认大小为 10。注意，增大字号会增大虚拟图像尺寸，因此您需要加载较大的纸张或使用 -l 选项来调整每页行数。
- -t num 假设制表符每 num 列设置一次，从第一列开始。默认情况下，制表符每 8 列设置一次。
- -x num 沿正 x 轴平移原点 num 英。默认坐标系的原点固定在页面左上角，x 向右，y 向下。正数 num 将所有内容向右移动。默认偏移量为 0.25 英寸。
- -y num 沿正 y 轴平移原点 num 英。正数 num 将文本向上移动。默认偏移量为 -0.25 英寸。

当前页打印 66 行或每读取到一个 ASCII 字符时，将开始新页面。您可以使用 -l 选项更改每页行数。不可打印的 ASCII 字符会被忽略，过长的行会被打印机静默截断。

# 示例

以下示例以横向模式打印 file1 和 file2。
```
lpr postprint -pl file2
```

以下示例在竖向模式下每张物理页上打印三个逻辑页面。
```
lpr postprint -n3 file
```

# 退出状态

- 0 成功完成。
- 非零 发生错误。

# 文件

```
/usr/lib/lp/postscript/forms.ps
/usr/lib/lp/postscript/ps.requests
```

# 属性

参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | numpsf |

# 参见

```
download(1), dpost(1), postdaisy(1), postmd(1), postio(1), postreverse(1), posttek(1), attributes(5)
```

# postreverse

# postreverse — 反转 PostScript 文件中的页顺序

# 概要

```
/usr/lib/lp/postreverse [-o list] [-r] [file]
/usr/lib/lp/postscript/postreverse
```

# 描述

postreverse 过滤器反转符合 Adobe 版本 1.0 或版本 2.0 文件结构规范文件的页顺序，并将结果写入标准输出。只允许一个输入文件，如果未指定文件，则读取标准输入。

postreverse 过滤器可以处理一类违反页面独立性的文件，前提是全局定义被 %%BeginGlobal 和 %%EndGlobal 包围；标签顺序命令也会使用 %%EndPage 标记每页的结束，只要可以找到序言（prologue）和尾部（trailer）部分即可。如果 postreverse 未找到 %%Prolog 或 %%EndSetup，则整个文件将原封不动地复制到标准输出。

由于全局定义是从单个页面中提取并放入序言的，如果输入文件不符合标准，输出文件也可以尽可能地符合标准。

> 注意 — 系统未尝试重新定义全局变量或过程。

# 选项

- -o list 打印逗号分隔列表中给出的页码。列表包含单个数字 NI 和范围 NI-NJ。缺失 NI 表示最低页码，缺失 NJ 表示最高页。如果使用标准输入，则反转所有页面。
- -r 反转文件。

# 示例

以下示例反转第 1 到 100 页。
```
lpr postreverse -ol100 file
```

以下示例在每张物理页上反转四个逻辑页面。
```
lpr postreverse -n4 file
```

以下示例通过标准输出生成反转后的页面。
```
dpost file | postreverse
```

# 退出状态

- 0 成功完成。
- 非零 发生错误。

# 属性

参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNpsf |

# 参见

download(1), dpost(1), postdaisy(1), postmd(1), postio(1), postreverse(1), posttek(1), attributes(5)

# posttek

# posttek — 用于 Tektronix 4014 文件的 PostScript 翻译器

# 概要

```
/usr/lib/lp/posttek [-c num] [-f name] [-m num] [-n num] [-o list]
[-p mode] [-w num] [-x num] [-y num] [file...]
/usr/lib/lp/postscript/posttek
```

# 描述

posttek 过滤器将 Tektronix 4014 图形文件转换为 PostScript 并结果写入标准输出。如果您未指定任何文件，或者 - 是输入文件之一，则读取标准输入。

> 注意 — 对于像 PS-2400 这样的引擎，线宽太小。

# 选项

- -c num 每页打印 num 份。默认情况下打印一份。
- -f name 使用字体名称打印文本。您可以使用 PostScript 字体，尽管使用等宽字体效果获得最佳。默认字体为 Courier。
- -m num 通过因子 num 放大每个逻辑页面。关于位于每个页面左上角的原点均匀缩放页面。默认放大倍数为 1.0。
- -n num 在每张纸上打印 num 个逻辑页面，num 可以任意正整数。默认情况下，num 设为 1。
- -o list 打印逗号分隔列表中给出的页码。列表包含单个数字 NI 和范围 NI-N2。缺失 NI 表示最低页码，缺失 N2 表示最高页。页面范围是逻辑页面的表达式，而不是物理纸张。例如，如果您在每张纸上打印两个逻辑页面并指定范围为 4，则会打印两张包含四个布局的纸。
- -p mode 以 p（竖向）或 l（横向）模式打印文件。模式的第一个字符有效。默认模式为竖向。
- -w num 将图形线宽设置为 num 点，点约为 1/72 英寸。默认情况下，num 设为 0 点，这会强制线条为 1 像素宽。
- -x num 沿正 x 轴平移原点 num 英。默认坐标系的原点固定在页面中心，正 x 向右，正 y 向上。正数 num 将所有内容向右移动。默认偏移量为 0.0 英寸。
- -y num 沿正 y 轴平移原点 num 英。正数 num 将所有内容向上移动。

