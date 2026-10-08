

# 选项

- -b 假设使用的输出设备不支持退格键。在这种情况下，两个或多个字符将出现在同一位置，仅输出最后读取的字符。

- -f 包含正向半行换行符（Esc-9），但不包含反向行移动。通常，半行输入移动会在下一行完整行显示。

- -p Esc-7。

- -x Esc-8。

# 示例

以下示例通过 `tbl` 和 `nroff` 运行文件，然后通过 `col` 和 `more` 过滤并在屏幕上输出。

```
castle# tbl file | nroff | col | more
```

以下示例通过 `col` 处理来自 VDT 的 nroff 输出。

```
castle# nroff -cm -r08 -kW79 document | col
```

以下示例从 DOS 文本文档移除 '^M'。

```
castle# filename | col output-file
```

在执行 `col` 命令之前，文件内容如下：
od 命令按顺序将每个输入文件复制到标准输出，并根据 `-or -bCCDfOoSvxx` 选项指定的输出类型转换输入数据。^M
如果指定了输出类型，默认输出等同指定了 `-t02`。可以使用多个 `-bCCDfOoSvtxx` 选项指定多种类型。按照 `-M` 类型指定的顺序为每种指定的类型写入输出行。如果没有指定文件，则使用标准输入。[offset_string] 操作数与 -A、-j、-N 和 -t 选项互斥。为了本描述的起见，使用了以下术语：^M

^M
M
M
MM

执行 `col` 命令后，文件内容如下：

od 命令按顺序将每个输入文件复制到标准输出，并根据 `-or -bCCDfOoSvxx` 选项指定的输出类型转换输入数据。^M
如果指定了输出类型，默认输出等同指定了 `-t02`。可以使用多个 `-bCCDfOoSvtxx` 选项指定多种类型。按照以下顺序为每种指定的类型写入输出行：

# col

类型指定的顺序。如果没有指定文件，则使用标准单元。[-offset_string] 操作数与 -A、-j、-N 和 -t 选项互斥。为了本描述的起见，使用了以下术语：

该示例过滤了输入中的反向换行符，以打印不带格式的手册页。
castle% man od | col -b lpr

在不使用 `col` 命令的情况下，输出如下：
名称
od - 十进制转储

摘要

```
/usr/bin/od [ -bcCDdFfOsvXx ] [- ] [ _f_i_l_e ]
[ _o_f_f_s_e_t__s_t_r_i_n_g ]
/usr/bin/od [ -bcCDdFfOsvXx ] [ -A_a_d_d_r_e_s_s__b_a_s_e ]
[ -j_s_k_i_p ] [ -N_c_o_u_n_t ] [ -t_t_y_p_e ]
[ -t ] [ _f_i_l_e ]
```

```
/usr/xpg4/bin/od [ -bcCDdFfOsvXx ] [- ] [ _f_i_l_e ]
[ _o_f_f_s_e_t__s_t_r_i_n_g ]
/usr/xpg4/bin/od [ -bcCDdFfOsvXx ] [ -A_a_d_d_r_e_s_s__b_a_s_e ]
[ -j_s_k_i_p ] [ -N_c_o_u_n_t ] [ -t_t_y_p_e ]
[ -t ] [ _f_i_l_e ]
```

`col` 剥离了格式，使得输出像这样的普通文本文件：
名称
od - 十进制转储

摘要

```
/usr/bin/od [ -bcCDdFfOsvXx ] [- ] [ file ]
```

# 154

# comb, sccs-

```
[ offset_string ]
```

```
/usr/bin/od [-bcCDdFfOoSvXx ] [-A address_base ]
```

```
 [-N count ] [ -t type_string ]
```

```
 [- ] file
```

```
/usr/xpg4/bin/od [-bcCDdFfOoSvXx ] [ - ] file
 [ offset_string ]
```

```
/usr/xpg4/bin/od [-bcCDdFfOoSvXx ] [-A address_base ]
```

```
 [- skip ] [-N count ] [ -t type_string ]
```

```
 [- ]
```

nroff 格式化器为打印机和 CRT 显示器产生输出。要加粗字符，它会打印字符后跟一个退格，然后再次打印相同的字符。下划线通过打印下划线、退格、然后要下划线的字符来实现。有时你可能需要去除这些特殊效果，例如当你想使用 `grep` 命令在格式化的手册页中搜索特定字符串时。以下示例使用 `col` 来消除这些特殊效果。

```
castle$% col -b nroff-stripped-output
```

# 环境变量

参考 environ(5) 获取影响 `col` 执行的环境变量描述：LC_CTYPE、LC_MESSAGES 和 NLPATH。

# 退出状态

- 0成功完成。
- >0 发生错误。

# 属性

参考 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNMesu |
| CSI | 已启用

# 另参

nroff(1), tbl(1), ascii(5), attributes(5), environ(5)

# comb, sccs-comb — 合并 SCCS 增量

# 摘要

```
/usr.ccs/bin/comb [-os] [-csid-list] [-psid] s.filename.
```

# comm

# 155

# 描述

参考 sccs-comb(1)。

# comm — 选择或拒绝两个文件的共同行

# 摘要

```
/usr/bin/comm [-123] file1 file2
```

# 描述

使用 `comm` 命令比较两个排序后的输入文件。输出由三列组成：file1 和 file2 共同行、file1 特有的行以及 file2 特有的行。输出根据当前语言环境排序。

# 选项

- -1 两个文件的共同行。
- -2 file1 特有的行。
- -3 file2 特有的行。

# 操作数

- file1 待比较第一个文件的路径。
- file2 待比较第二个文件的路径。

# 用法

参考 comm(5) 了解 `comm` 的行为。

# 示例

以下示例了如何比较两个文件：

```
castle% comm -1 file1 file2
```

