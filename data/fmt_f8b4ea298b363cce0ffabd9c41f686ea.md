
- 1. 搜索模式 `Blenheim` 用前斜杠定界，替换模式 `Dobbins` 也用前斜杠定界。
    *注：OCR 文本在下方说明的第 2 点中写的是“用括号定界”，但代码使用的是 `/`。OCR 说明文本为：“2. 搜索模式 `Blenheim` 用括号定界，替换模式 `Dobbins` 用前斜杠定界。”这与代码 `s/Blenheim/Dobbins/` 相矛盾。然而，前文提到了“如果你使用成对的括号...”。这个例子可能是意图使用括号，如 `s{Blenheim}{Dobbins}` 或 `s(Blenheim)Dobbins/`？不，代码显示的是 `/`。我将坚持使用 OCR 代码块中显示的 `/`。如果文本解释括号，这可能是不同的例子或文本中的 OCR 错误。让我们再看一遍 OCR 说明：“2. 搜索模式 `Blenheim` 用括号定界...”。这很可能是*文本*或*源代码*中的 OCR 错误。鉴于我必须输出处理后的文本，我将按源文中写的那样保留说明，但我可能需要小心。提示说“更正明显的 OCR 错误”。代码和文本之间的矛盾是语义错误，不仅仅是 OCR。除非是像“括号”代替“斜杠”这样的明显笔误，否则我保留文本原样。“括号”是一个具体的词。为了避免过度更正语义内容，我会保留它，但我会确保代码可读。*
- 2. 搜索模式 `Blenheim` 用括号定界，替换模式 `Dobbins` 用前斜杠定界。
- 3. 替换结果在打印输出中显示。`Blenheim` 被替换为 `Dobbins`。
- 4. `DATA` 文件句柄从 `__DATA__` 标记后面的行获取数据。

## 替换修饰符

你可以通过一些特殊修饰符来控制替换执行的方式；例如，你可以关闭大小写敏感性、评估替换侧、进行全局替换等等。表 8.4 列出了这些修饰符。

**表 8.4** 替换修饰符

| 修饰符 | 含义 |
| :--- | :--- |
| `e` | 将替换侧作为表达式求值。 |
| `i` | 关闭大小写敏感性。 |
| `m` | 将字符串视为多行。* |
| `o` | 仅编译模式一次。用于优化搜索。 |
| `s` | 当嵌入换行符时将字符串视为单行。 |
| `x` | 允许在正则表达式中包含空白和注释。 |
| `g` | 全局替换；即，查找所有出现。 |

*m、s 和 x 选项仅在 Perl 5 中定义。

*注：OCR 表格中对应“评估替换侧...”使用的是 `*c*`。用于评估替换侧的正确 Perl 修饰符是 `e`，而不是 `c`。在此上下文中，`c` 不是标准的替换修饰符。我将把 `c` 更正为 `e`。*

## g 修饰符——全局替换

`g` 修饰符用于执行全局替换；也就是说，会替换掉该行中模式的所有出现位置。如果没有 `g`，则每行只替换模式的第一次出现。

### 格式

```
s/搜索模式/替换字符串/g;
```

### 示例 8.20

**脚本**

```perl
# 不使用 g 选项

use warnings;

while (<DATA>) {
    print if s/Tom/Christian/;    # 将每行中第一个 Tom 替换为 Christian
                                   # 仅替换每行中 Tom 的第一次出现
}

__DATA__

Tom Dave Dan Tom

Betty Tom Henry Tom

Igor Norma Tom Tom
```

**输出**

```
Christian Dave Dan Tom

Betty Christian Henry Tom

Igor Norma Christian Tom
```

### 解释

- 2. 对于读取的每一行，`Tom` 的第一次出现将被替换为 `Christian`。
- 3. `DATA` 文件句柄获取其数据自 `__DATA__` 标记后的那些行。

### 示例 8.21

**脚本**

```perl
# 使用 g 选项

use warnings;

while (<DATA>) {
    print if s/Tom/Christian/g;    # 将每行中所有的 Tom 替换为 Christian
                                    # 替换每行中 Tom 的所有出现
}

__DATA__

Tom Dave Dan Tom

Betty Tom Henry Tom

Igor Norma Tom Tom
```

**输出**

```
Christian Dave Dan Christian

Betty Christian Dick Christian

Igor Norma Christian Christian
```

### 解释

- 2. 使用 `g` 选项时，替换是全局的。读取的每一行中，`Tom` 的**每一次**出现都会被替换为 `Christian`。
- 3. `DATA` 文件句柄获取其数据自 `__DATA__` 标记后的那些行。

## i 修饰符——不区分大小写

Perl 在执行匹配时区分大写字母和小写字母。如果要关闭大小写敏感性，则在匹配或替换操作符的最后一个分隔符后附加 `i`（不敏感），此时搜索模式将不区分大小写，但这不影响替换端。

### 格式

```
s/搜索模式/替换字符串/i;
```

### 示例 8.22

**脚本**

```perl
# 使用 i 选项进行匹配

use warnings;

while(<DATA>){
    print if /norma cord/i; # 关闭大小写敏感性
}

__DATA__

Steve Blenheim

Betty Boop

Igor Chevsky

Norma Cord

Jon DeLoach

Karen Evich
```

**输出**

```
Norma Cord
```

### 解释

- 2. 如果没有 `i` 选项，正则表达式 `/norma cord/` 将不会匹配，因为作为输入读取的行中，并非所有字母都是小写的。`i` 选项关闭了大小写敏感性。
- 3. `DATA` 文件句柄获取其数据自 `__DATA__` 标记后的那些行。

### 示例 8.23

**脚本**

```perl
use warnings;

while(<DATA>){
    print if s/Igor/Daniel/i;  # 将 Igor 替换为 Daniel
}

__DATA__

Steve Blenheim

Betty Boop

Igor Chevskey

Norma Cord

Jon DeLoach

Karen Evich
```

**输出**

```
Daniel Chevskey
```

### 解释

- 2. 由于 `i` 选项，替换中的正则表达式也是不区分大小写的。如果匹配到 `Igor` 或 `IgOr`（或大小写的任何组合），它将被替换为 `Daniel`。
- 3. `DATA` 文件句柄获取其数据自 `__DATA__` 标记后的那些行。

## e 修饰符——求值表达式

在替换操作的替换端，可以求值一个表达式或函数。搜索端将被替换为求值的结果。

### 格式

```
s/搜索模式/替换字符串/e;
```

### 示例 8.24

**脚本**

```perl
use warnings;

# e 和 g 修饰符

while(<DATA>){
    s/6/6 * 7.3/eg;             # 用 6 * 7.3 的乘积替换 6
    print;
}

__DATA__

Steve Blenheim   5

Betty Boop       4

Igor Chevskey    6

Norma Cord       1

Jon DeLoach      3

Karen Evich      66
```

**输出**

```
Steve Blenheim   5

Betty Boop        4

Igor Chevskey     43.8

Norma Cord        1

Jon DeLoach       3

Karen Evich       43.843.8
```

### 解释

- 2. 如果 `$` 标量包含数字 6，则替换的右侧会被求值。换句话说，6 会被乘以 7.3（`e` 修饰符）；乘法的结果（43.8）每次找到数字 6 时都会替换该数字（`g` 修饰符）。
- 3. 每行都会被打印。最后一行包含两个 6，导致每个 6 都被替换为 43.8。

### 示例 8.25

**脚本**

```perl
use warnings;

# e 修饰符

my $number = 5;

s/5/6 * 4 - 22/e;

print "The result is: $number\n";

$number = 51055;

s/5/3 * 2/e;

print "The result is: $number\n";
```

**输出**

```
