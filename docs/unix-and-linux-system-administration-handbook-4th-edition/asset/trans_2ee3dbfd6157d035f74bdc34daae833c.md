

事实上，任何以空白字符分隔的事物列表，包括变量的内容，都可以作为 for...in 的目标。

bash 也拥有传统编程语言中更常见的 for 循环，你可以通过它指定起始、递增和终止子句。例如：

```
for ((i=0; i < $CPU_COUNT ; i++)); do
  CPU_LIST="$CPU_LIST $i"
done
```

下一个示例演示了 bash 的 while 循环，它对于处理命令行参数和读取文件中的行非常有用。

```
#!/bin/bash
exec 0<$1
counter=1
while read line; do
  echo "$counter: $line"
  $((counter++))
done
```

以下是输出的样子：

```
ubuntu$ sh whileexample /etc/passwd
1: root:x:0:0:Superuser:/root:/bin/bash
2: bin:x:1:1:bin:/bin/bash
3: daemon:x:2:2:Daemon:/sbin:/bin/bash
...
```

这个脚本片段有几个有趣的功能。exec 语句将脚本的标准输入重新定义为来自第一个命令行参数所指定的文件。8 该文件必须存在，否则脚本会产生错误。

while 子句中的 read 语句实际上是一个 shell 内建命令，但它的行为类似于外部命令。你也可以将外部命令放在 while 子句中；在这种形式下，当外部命令返回非零退出状态时，while 循环终止。

$((counter++)) 表达式确实是个异类。$((...)) 记号强制进行数值求值。它还使得用于标记变量名的 $ 成为可选项。++ 是来自 C 和其他语言中常见的后置递增运算符。它返回其所附着变量的值，但同时也有将该变量值递增的副作用。

$((...)) 的这些把戏在双引号内也能生效，因此循环体可以压缩为一行。

```
while read line; do
    echo "$(counter++) $line"
done
```

## 数组与算术

复杂的数据结构和计算并不是 bash 的强项。但它至少提供了数组和算术运算。

所有 bash 变量都是字符串值，因此 bash 在赋值时不区分数字 1 和字符串 "1"。区别在于变量的使用方式。下面的代码说明了这种区别：

```
#!/bin/bash

a=1
b=$((2))

c=$a+$b
d=$(( $a + $b ))

echo "$a + $b = $c \(plus sign as string literal\)"
echo "$a + $b = $d \(plus sign as arithmetic addition\)"
```

该脚本产生以下输出

```
1 + 2 = 1+2 (plus sign as string literal)
1 + 2 = 3 (plus sign as arithmetic addition)
```

注意，赋值给 $c 时，加号甚至不作为字符串的连接运算符。它只是一个字面字符。那一行等价于

```
c="$a$b"
```

要强制进行数值求值，你需要将表达式包含在 $((...)) 中，如上面赋值给 $d 所示。但即使采取这种预防措施，$d 接收到的也不是数值；该值仍然以字符串 "3" 的形式存储。

bash 拥有常见的各类算术、逻辑和关系运算符；详细信息请参见 man 手册页。

bash 中的数组有点奇怪，而且并不常用。不过，如果你需要的话，它们仍然可用。数组字面量用括号括起来，元素之间用空白字符分隔。你可以使用引号在元素中包含字面空格。

```
example=(aa 'bb cc' dd)
```

使用 ${array_name[subscript]} 来访问单个元素。下标从零开始。下标 * 和 @ 表示整个数组，特殊形式 ${#array_name[@]} 和 ${#array_name[@]} 会得出数组中的元素个数。不要把这些误记成看起来更合乎逻辑的 ${#array_name}；后者实际上是数组第一个元素的长度（等同于 ${#array_name[0]}）。

你可能会认为 $example[1] 是对数组第二个元素的明确引用，但 bash 会把这个字符串解析为 $example（即 $example[0] 的简写引用）加上字面字符串 [1]。引用数组变量时，一定要包含花括号——没有任何例外。

下面是一个快速脚本，演示了 bash 中数组管理的一些特性和陷阱：

```
#!/bin/bash

example=(aa 'bb cc' dd)
example[3]=ee

echo "example[@] = ${example[@]}"
echo "example array contains ${#example[@]} elements"

for elt in "${example[@]}"; do
    echo "  Element = $elt"
done
```

其输出为

```
$ sh arrays
example[@] = aa bb cc dd ee
example array contains 4 elements
  Element = aa
  Element = bb cc
  Element = dd
  Element = ee
```

这个例子看起来简单明了，但这仅仅是因为我们把它构建得很规范。陷阱正等待着粗心大意的人。例如，把 for 那一行替换为

```
for elt in ${example[@]}; do
```

（数组表达式不带引号）同样可以正常工作，但得到的不是四个数组元素，而是五个：aa、bb、cc、dd 和 ee。

根本问题在于，所有 bash 变量本质上仍然是字符串，因此数组的幻象充其量也不稳固。关于字符串在何时以及如何被分割为元素的细微之处比比皆是。你可以使用 Perl 或 Python，或者搜索 Mendel Cooper 的《高级Bash脚本编程指南》来探究这些细微差别。

## 2.3 正则表达式

大多数现代语言都支持正则表达式，尽管有些语言对它们的重视程度超过其他语言。UNIX 命令（如 grep 和 vi）也使用它们。它们如此普遍，以至于这个名字通常被缩写为 "regex"。关于如何驾驭其威力，已经出版了整本整本的著作，而且它们也已成为众多博士论文的主题。

