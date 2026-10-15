
```
- sh
popd [+n]
```

### 描述

查看 `cd(1)`。

# postdaisy — 针式打字机 PostScript 转换器

### 概要

```
/lib/lp/postdaisy [-c num] [-f num] [-h num] [-m num] [-n num] [-o list] [-p mode] [-r num] [-s num] [-v num] [-x num] [-y num] [file...]
/lib/lp/postscript/postdaisy
```

### 描述

`postdaisy` 过滤器将针式打字机文件转换为 PostScript 并将结果写入标准输出。如果你未指定文件或 `-`，则从标准输入读取。

### 选项

- `-c num` 打印每页的副本。默认只打印一份。
- `-f name` 使用字体名称打印文件。
- `-h num` 设置初始水平索引。默认为 8。
- `-m num` 使用点大小代替初始索引设置的值。
- `-n num` 打印逗号分隔列表中的页码。
- `-o list` 打印逗号分隔范围列表中的页码。
- `-p mode` 以竖向（p）或横向（1）模式打印文件。模式的第一个字符有效。默认模式为竖向。
- `-r num` 选择回车和换行行为。如果 `num` 为 1，换行产生回车；如果 `num` 为 2，回车产生换行。将 `num` 设置为 3 开启模式。
- `-s num` 设置垂直移动索引。默认为 12。
- `-v num` 按因子放大每页。
- `-x num` 沿 x 轴移动 `num` 英。默认坐标系原点位于页面左上角，x 向右，y 向下。正 `num` 向右移动。默认偏移为 0.25 英寸。
- `-y num` 沿 y 轴移动 `num` 英。正 `num` 向上。默认偏移为 -0.25 英寸。

## 退出状态

- `0` 成功。
- 非零 发生错误，例如无进程、权限被拒绝或无效选项。

## 文件

```
/lib/lp/postscript/forms.ps
/lib/lp/postscript/ps
```

### 属性

查看 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUNpsf |

## 另请

`download(1)`, `dpost(1)`, `postdmd(1)`, `postio(1)`, `postmd(1)`, `postprint(1)`, `postreverse(1)`, `posttekk(1)`, `attributes(5)`

# postdmd — 位图文件 PostScript 转换器
（根据概要内容修正为 postdaisy）

### 描述

`postdaisy` 过滤器将位图文件转换为 PostScript 并将结果写入标准输出。如果你未指定文件或 `-`，则从标准输入读取。

### 选项

- `-c num` 打印每页的副本。默认只打印一份。
- `-f name` 使用字体名称打印文件。
- `-h num` 设置初始水平索引。默认为 8。
- `-m num` 使用点大小代替初始索引设置的值。
- `-n num` 打印逗号分隔列表中的页码。
- `-o list` 打印逗号分隔范围列表中的页码。
- `-p mode` 以竖向（p）或横向（1）模式打印文件。模式的第一个字符有效。默认模式为竖向。
- `-r num` 选择回车和换行行为。如果 `num` 为 1，换行产生回车；如果 `num` 为 2，回车产生换行。将 `num` 设置为 3 开启两种模式。
- `-s num` 设置垂直移动索引。默认为 12。
- `-v num` 按因子放大每页。
- `-x num` 沿 x 轴移动 `num` 英。默认坐标系原点位于页面左上角，x 向右，y 向下。正 `num` 向右移动。默认偏移为 0.25 英寸。
- `-y num` 沿 y 轴移动 `num` 英。正 `num` 向上。默认偏移为 -0.25 英寸。

# postdmd

## 1069

### Options

- `-b num` 使用 `num` 个字节模式在输出文件中打包位图。`num` 设置为 0 则关闭输出文件的所有打包功能。默认情况下，`num` 为 6。
- `-c num` 打印每页的副本。默认情况下，只打印一份。
- `-f` 在打印位图之前翻转文件中位的方向。
- `-m num` 按因子 `num` 放大每个逻辑页。关于原点进行等比例缩放，原点默认位于页面的中心。默认放大倍数为 1.0。
- `-n num` 在每张纸上打印 `num` 个逻辑页，`num` 可以是任何正整数。默认情况下，`num` 设置为1。
- `-o list` 打印逗号分隔列表中给出的页码。列表包含单个数字和范围 `N1-N2`。缺失 `N1` 表示最低编号的页面，缺失 `N2` 表示最高编号。页面范围是逻辑页的扩展，而不是物理纸张的扩展。例如，如果你在一张纸上打印两个逻辑页并指定了范围为 4，则会打印两张包含四个布局的纸。如果你在请求每张纸打印两页时指定范围为 3-4，则只会打印第 3 和 4 页的布局，它们将出现在一张物理纸张上。
- `-p mode` 以 p（纵向）或 l（横向）模式打印。`mode` 的第一个字符有效。默认模式为纵向。
- `-x num` 沿正 x 轴移动原点 `num` 英寸。默认坐标系的原点固定在页面中心，x 向右，y 向上。正 `num` 将所有内容向右移动。默认偏移量为 0 英寸。
- `-y num` 沿正 y 轴移动原点 `num` 英寸。正 `num` 将所有内容向上移动。默认偏移量为 0。

每个逻辑页只打印一个位图，且每个输入文件必须包含至少一个位图的内容。通过 `-b` 选项减小模式大小有助于具有快速处理器的打印机（如 PS-810s）的吞吐量，而在较旧型号（如 PS-800s）上，增加页面大小通常是正确的做法。

## Exit Status

- `0` 成功完成。
- 非零 发生错误。

# Files

```
/usr/lib/lp/postscript/forms.ms/usr/lib/lp/postscript/ps.requests
```

## 1070

# postio

## Attributes

有关以下属性的描述请参见 `attributes(5)`：

| 属性类型 | 属性值 |
|---|---|
| Availability | SUNwps |

## See Also

- `download(1)`, `dpost(1)`, `postdaisy(1)`, `postio(1)`, `postmd(1)`, `postprint(1)`, `postreverse(1)`, `posttek(1)`, `attributes(5)`

# postio — 用于 PostScript 打印机的串口接口

### Synopsis

```
/usr/lib/lp/postio -l line [-i] [-q] [-t] [-S] [-B speed] [-B num] [-L file] [-P string] [-R num] [file...]
/usr/lib/lp/postscript/postio
```
