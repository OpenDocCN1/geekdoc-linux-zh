
This module does not really exist, it was made for the sole purpose of demonstrating how POD works.

## Methods

=over 12

=item `C<new>`

Returns a new `My::Module` object.

=item `C<as_string>`

Returns a stringified representation of the object. This is mainly for debugging purposes.

=back

# LICENSE

This is released under the Artistic License. See `L<artistick>`.

# AUTHOR

Juerd - `L<http://juerd.nl/>`

# SEE ALSO

`L<perlpod>`, `L<perlpodspec>`

=cut

![](img/8556abcb353c0991f12099420ec28735_531_0.png)

### 14.5.1 pod 文件

如果在标准 Perl 库中查找，你会发现模块包含文档，说明模块应该做什么以及如何使用它。（在命令行上，输入 `perldoc perlpod`。）文档要么嵌入在程序中，要么放置在程序末尾的特殊字面量 `_END_` 之后。这种文档称为 `pod`，是 Plain Old Documentation 的缩写。`pod` 文件只是一个嵌入特殊命令的 ASCII、utf-8 或 Unicode 文本文件，这些命令可以通过 Perl 的特殊解释器之一进行转换，如 `pod2html`、`pod2latex`、`pod2text` 或 `pod2man`。目的是创建格式化的文档，可以用多种方式表示。UNIX man 页面就是一个例子，它是使用 nroff 指令格式化的文档。现在可以轻松地在脚本中嵌入一组 `pod` 格式指令，以提供以下四种格式之一的文档：文本、HTML、LaTeX 或 nroff。

`pod` 文档的第一行以等号（`=`）开头。每个以等号开头的 `pod` 指令都是 `pod` 转换器的格式指令。每个格式指令都必须以一个空白行结尾。

## 示例 14.26

（标准 Perl 库，位于子目录 Math 下。）

```pod
=head1 NAME

Math::BigFloat - Arbitrary length float math package

=head1 SYNOPSIS

use Math::BigFloat;

$f = Math::BigFloat->new($string);
```

- `$f->fadd(NSTR)` 返回 NSTR 加法
- `$f->fsub(NSTR)` 返回 NSTR 减法
- `$f->fmul(NSTR)` 返回 NSTR 乘法
- `$f->fdiv(NSTR[, SCALE])` 返回 NSTR 除以 SCALE 位
- `$f->fneg()` 返回 NSTR 取反
- `$f->fabs()` 返回 NSTR 绝对值
- `$f->fcmp(NSTR)` 返回 CODE 比较 undef, <0, =0, >0
- `$f->fround(SCALE)` 返回 NSTR 舍入到 SCALE 位
- `$f->fround(SCALE)` 返回 NSTR 舍入到 SCALE 位
- `$f->fnorm()` 返回 (NSTR) 归一化
- `$f->fsqrt([SCALE])` 返回 NSTR 平方根到 SCALE 位

（这是在 `BigFloat.pm` 模块末尾找到的文档）

```pod
=head1 DESCRIPTION
```

如果你声明你的大浮点数，所有基本数学运算都被重载

```pod
$float = new Math::BigFloat "2.123123123123123123123123123123123123";
=over 2
=item number format
```

规范字符串具有形式 `/([+]\d+E[+-]\d+/`。输入值可以包含嵌入的空格。

## 示例 14.26（续）

=item 错误返回 'NaN'

输入参数为“非数字”（Not a Number），或发生了除以零，或对负数开平方。

=item 除法默认计算至

`C<max($div_scale, length(dividend)+length(divisor))>` 位数字。
这也用于默认的平方根精度。

=back

## 缺陷

本模块的当前版本是真实版本的预研版，目前（截至 Perl 5.002）正在开发中。

## 作者

Mark Biggar

=cut

## 说明

上述文本是一个 *pod 文件*。它由以等号开头并跟随一个 *pod 命令* 的行组成，随后是一个空白行和文本。Perl 提供了一个专门的翻译程序，用于读取 *pod* 文件并将其转换为可读的纯文本、HTML 格式、*nroff* 文本或 LaTeX 文件。下一节将介绍如何使用 *pod* 过滤程序来为你完成翻译。

### 14.5.2 pod 命令

在文本文件中嵌入 *pod* 指令非常简单。命令位于行首，以 `=pod`（或任何其他 *pod* 命令）开头，以 `=cut` 结尾。从第一个 `=pod` 指令到 `=cut` 指令之间的所有内容都会被编译器忽略，就像注释被忽略一样。使用这些命令的好处是，它们允许你创建粗体、*斜体* 或普通文本，进行缩进，创建标题等。表 14.3 列出了一系列指令。

**检查你的 pod 命令。** 为了检查你文件中的 *pod* 指令是否正确，可以使用 Perl 的 *podschecker* 命令。首先，要找到你的模块路径，请在提示符下输入：

```
perldoc -I Module.pm
```

然后，

```
podchecker path/Module.pm
```

希望它显示以下内容：

```
path/Module.pm pod syntax OK.
```

#### 表 14.3 pod 命令

**段落命令**

| 命令 | 作用 |
| :--- | :--- |
| `=pod` | 标记 pod 的开始，但任何以等号开头的 pod 指令都会开始文档。 |
| `=cut` | 标记 pod 的结束。 |
| `=head1 heading` | 创建一级标题。 |
| `=head2 heading` | 创建二级标题。 |
| `=item *` | 开始一个项目符号列表。 |
| `=over N` | 向右移动 N 个空格，通常设为 4。 |
| `=back` | 将缩进恢复为默认值，即无缩进。 |

**格式化命令**

| 命令 | 作用 |
| :--- | :--- |
| `I<text>` | 创建斜体文本。 |
| `B<text>` | 创建粗体文本。 |
| `S<text>` | 包含文本非断空格。 |
| `C<code>` | 包含打字文本，即字面源代码。 |
| `L<name>` | 创建一个指向名称的链接（交叉引用）。 |
| `F<file>` | 用于列出文件名。 |
| `X<index>` | 一个索引项。 |
| `Z<>` | 一个零宽度字符。 |

**过滤器特定命令**

| 命令 | 作用 |
| :--- | :--- |
| `=for` | 用于 HTML 特定命令；例如，`=for html <IMG SRC=file.gif> <B>Figure a.</B>` |
| | 用于文本特定命令；例如，`=for text` |
| | 用于手册页特定命令；例如，`=for man_ce 3 <center next three lines>` |

### 14.5.3 如何使用 pod 解释器

*Pod* 解释器随 Perl 发行版提供，位于主 Perl 目录下的 *bin* 目录中；例如，在 *usr/bin/perl5/bin* 中。

这四个解释器分别是

- *pod2html*（翻译为 HTML）
- *pod2text*（翻译为纯文本）
- *pod2man*（翻译为 *nroff*，类似于 UNIX *man* 页面）
- *pod2latex*（翻译为 LaTeX）

使用解释器最简单的方法是将其复制到你自己的目录中。例如：

```
$ cp /usr/bin/perl5/bin/pod2text
```

你还可以将库例程复制到你的目录中：

```
$ cp /usr/bin/perl5/lib/BigFloat.pm
```

现在，当你列出目录内容时，你应该同时拥有 *pod* 解释器和库模块。

```
$ ls

BigFloat.pm

pod2text
