
# 266

## 退出状态
- `0` 成功完成。
- 非 `0` 发生错误。

## 选项
- `-c num`
  打印每个页面的 `num` 份。默认情况下，只打印一份。
- `-e num`
  将文本编码级别设置为 `num`。可识别的值为 `0`、`1` 和 `2`。输出文件的大小和打印时间应随 `num` 的增加而减少。级别 `2` 的编码通常比级别 `0`（默认值）快约 `20%`，且产生的输出与之前 `dpost` 的版本在本质上是相同的。
- `-m num`
  按因子 `num` 放大每个逻辑页。围绕原点进行等比例缩放，原点位于每个页面左上角附近。默认放大倍数为 `1.0`。
- `-n num`
  每张纸上打印 `num` 个逻辑页，其中 `num` 可以是任何正整数。默认情况下，`num` 设置为 `1`。
- `-o list`
  打印逗号分隔列表中给出的数字对应的页面。列表包含数字 `N` 和 `N1–N2`。缺失 `N1` 表示最低编号的页，缺失 `N2` 表示最高编号。页码范围是逻辑页的表达式，而不是纸张页数。例如，如果你正在将逻辑页打印到纸张上，并指定打印两张纸，包含四个页面布局。如果你在请求将逻辑页打印到纸上时指定页范围为 `3–4`，则只有第 `3` 页和第 `4` 页布局会打印在一个物理纸上。
- `-p mode`
  以 `p`（竖向）或 `l`（横向）模式打印文件。模式的首字符有效。默认模式为竖向。
- `-w num`
  将用于实现绘图命令的宽度设置为 `num` 磅，其中 `1` 磅约为英寸的 `1/72`。默认情况下，`num` 设置为 `0.3` 磅。
- `-x num`
  沿 `x` 轴平移 `num` 英寸。默认坐标系的原点固定在页面左上角附近，正 `x` 轴向右，`y` 轴向下向下。正 `x` 会移动所有内容。默认偏移量为 `0` 英寸。
- `-y num`
  沿 `y` 轴平移 `num` 英寸。正 `y` 会将文本向上移动。默认偏移量为 `0`。
- `-F dir`
  使用 `dir` 作为字体目录。默认 `dir` 为 `/usr/lib/font`，`dpost` 从目录 `/usr/lib/font/devpost` 读取二进制字体文件。
- `-H dir`
  使用 `dir` 作为宿主机驻字体目录。此目录中的文件应该是完整的 PostScript 字体描述。它们必须分配一个与相应的双字符 troff 字体名称对应的名称。每个字体文件仅在需要时才复制到输出文件中，且每个作业期间最多复制一次。没有默认目录。
- `-L`
  使用文件作为 PostScript 导言（prologue）。默认为 `/usr/lib/lp/postscript/dpost.ps`。
- `-O`
  禁止 PostScript 图片包含。在网络环境中，建议通过打印队列（spooler）运行 `dpost`。
- `-T name`
  使用 `name` 指定字体设备作为可用 PostScript 字体的描述。默认情况下，`name` 设置为 `post`，`dpost` 从 `/usr/lib/font/devpost` 读取二进制文件。

## 示例
如果你的系统中安装了 `eqn` 和 `pic` 的旧版本，你可以通过执行类似下面的命令获得外观最好的输出：

```
castle% pic -T720 file | tbl | eqn -r720 | troff -mm -Tpost | dpost
```

否则，以下命令应该产生最好的结果。

```
castle% pic file | tbl | eqn | troff -mm -Tpost | dpost
```

## 退出状态
- `0` 成功完成。
- 非零 发生错误。

## 文件
```
/usr/lib/font/devpost/*.out
/usr/lib/font/devpost/charlib/
/usr/lib/lp/postscript/color.ps
/usr/lib/lp/postscript/draw.ps
/usr/lib/lp/postscript/forms.ps
/usr/lib/lp/postscript/ps.requests
/usr/lib/macros/pictures
/usr/lib/macros/color
```

## 属性
参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可性 | SUNwpsf |

## 参见
```
download(1)postdaisy(1)postdmd(1)postio(1)postma(1),postprint(1),
postreverse(1),posttek(1),troff(1),attributes(5)
```

# 总结磁盘使用情况

### 概要
```
/usr/ucb/du
/usr/ucb/du [-a][-s][filename]
```

## 描述
`/usr/ucb/du` 命令为了兼容 BSD，用于显示每个指定目录或文件名内所有文件以及递归目录包含的千字节数。如果不指定 `filename`，则使用当前目录。
具有多个链接的文件只计算一次。
在没有使用选项的情况下，仅为每个目录生成条目。
除非使用 `-a` 选项，否则不是目录名的 `filename` 参数将被忽略。

> 注意 — 如果有太多不同的链接文件，`du` 会多次计算多余的文件。

## 选项
- `-a` 为每个文件生成一个条目。
- `-s` 仅显示每个指定文件名的总计。

## 示例
以下使用 `du` 识别每个指定文件名的总计。

```
castle% du -s /home
castle% du -a /home
castle% du -s /home1 /home2
```

## 环境变量
如果未设置以下 `LC_*` 变量（`LC_COLLATE`, `LC_MONETARY`, `LC_NUMERIC`, `LC_TIME`）（见 `environ(5)`），将使用 C 语言。如果设置了 `LC_ALL`，它将覆盖 `LANG` 和其他 `LC_*` 变量。
- `LC_TYPE` 决定 `du` 处理字符。
- `LC_MESSAGES` 决定诊断和信息的呈现方式。在 ISO8859-1。

| 属性类型 | 属性值 |
|---|---|
| 可性 | SUNscpu |

## 参见
`pwd(1)`, `df(1M)`, `quot(1M)`, `attributes(5)`, `environ(5)`

# dumpplot — 各种绘图器的过滤器

### 概要
```
/usr/ucb/plot [-Tterminal]
```

## 描述
参见 `plot(1)`。

# dump — 用于脚本导出文件部分

### 概要
```
/usr/ccs/bin/dump [-aCCDfghLrstV] [-T index [, indexn] filename ...
/usr/ccs/bin/dump [-aforstl [v]] filename ...
/usr/ccs/bin/dump [-hsr [-d number [, number]] filename ...
/usr/ccs/bin/dump [-hsrt -n name] filename ..
```
