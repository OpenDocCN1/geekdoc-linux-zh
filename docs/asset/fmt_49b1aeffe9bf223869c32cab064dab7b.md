
注意：

- 运算符和表达式之间必须有空格，例如 `2+2` 是错误的，而应该写成 `2 + 2`。
- 完整的表达式应该包含在双引号 `“”` 之间。

### 算术运算符

以下是 Bourne Shell 支持的算术运算符。

假设变量 `a` 存储 `10`，变量 `b` 存储 `20`，那么——

示例，使用所有算术运算符——

```sh
#!/bin/sh
a=10
b=20
val=`expr $a + $b`
echo "$a + b: $val"
```

```sh
val=`expr $a - $b`
echo "$a - b: $val"
```

```sh
val=`expr $a \* $b`
echo "$a * b: $val"
```

```sh
val=`expr $b / $a`
echo "$b / a: $val"
```

```sh
val=`expr $b % $a`
echo "$b % a: $val"
```

```sh
if [ $a == $b ]
then
echo "$a is equal to b"
```

```sh
if [ $a != $b ]
then
echo "$a is not equal to b"
```

这产生了以下结果——

a + b : 30
a - b : -10
a * b : 200
b / a : 2
b % a : 0
a is not equal to b

注意：

- 运算符和表达式之间必须有空格，例如 `2+2` 是错误的，而应该写成 `2 + 2`。
- 完整的表达式应该包含在双引号 `“”` 之间。
- 你应该使用 `*` 符号进行乘法。
- `if...then...fi` 语句是一个判断语句，将在下一章解释。

| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| + | 加法 - 将运算符两侧的值相加 | `expr + $b` 将得到30 |
| - | 减法 - 从左操作数减去右操作数 | `expr - $b` 将得到-10 |
| * | 乘法 - 将运算符两侧的值相乘 | `expr \* $b` 将得到200 |
| / | 除法 - 将左操作数除以右操作数 | `expr / $a` 将得到2 |
| % | 取模运算 - 将左操作数除以右操作数并返回余数 | `expr % $a` 将得到0 |
| = | 赋值 - 将右值赋给左变量 | - |
| == | 等于 - 比较两个值是否相等 | - |
| != | 不等于 - 比较两个值是否不等 | - |

### 关系运算符

Bourne shell 支持以下关系运算符，这些运算符主要用于数值比较。假设变量 `a` 存储 `10`，变量 `b` 存储 `20`，那么——

示例，使用所有的关系运算符——

```sh
#!/bin/sh
a=10
b=20
if [ $a -eq $b ]
then
echo "$a is equal to b"
else
echo "$a is not equal to b"
fi
```

```sh
if [ $a -ne $b ]
then
echo "$a is not equal to b"
else
echo "$a is equal to b"
fi
```

```sh
if [ $a -gt $b ]
then
echo "$a is greater than b"
else
echo "$a is not greater than b"
fi
```

```sh
if [ $a -lt $b ]
then
echo "$a is less than b"
else
echo "$a is not less than b"
fi
```

```sh
if [ $a -ge $b ]
then
echo "$a is greater than or equal to b"
else
echo "$a is not greater than or equal to b"
fi
```

```sh
if [ $a -le $b ]
then
echo "$a is less than or equal to b"
else
echo "$a is not less than or equal to b"
fi
```

Bourne shell 并不原生支持任何执行简单算术运算的机制，但它使用外部程序，即 `awk` 或更简单的 `expr` 程序。

需要特别注意的是，所有的条件表达式都应该放在方括号内，并且周围各有一个空格，例如 `[ $a <= $b ]` 是正确的，而 `[$a <= $b]` 是错误的。

### 布尔运算符

Bourne Shell 支持以下布尔运算符。假设变量 `a` 存储 `10`，变量 `b` 存储 `20`，那么此示例使用了所有的布尔运算符 –

```bash
#!/bin/sh
a=10
b=20
if [ $a != $b ]
then
  echo "$a != $b : a is not equal to b"
else
  echo "$a = $b : a is equal to b"
fi
```

```bash
if [ $a -lt 100 $b -gt 15 ]
then
  echo "$a -lt 100 -a $b -gt 15 : returns true"
else
  echo "$a -lt 100 -a $b -gt 15 : returns false"
fi
```

```bash
if [ $a -lt 100 -o $b -gt 100 ]
then
  echo "$a -lt 100 -o $b -gt 100 : returns true"
else
  echo "$a -lt 100 -o $b -gt 100 : returns false"
fi
```

```bash
if [ $a -lt 5 -o $b -gt 100 ]
then
  echo "$a -lt 100 -o $b -gt 100 : returns true"
else
  echo "$a -lt 100 -o $b -gt 100 : returns false"
fi
```

这产生了以下结果 –

```
10 != 20 : a is not equal to b
10 -lt 100 -a 20 -gt 15 : returns true
10 -lt 100 -o 20 -gt 100 : returns true
10 -lt 5 -o 20 -gt 100 : returns false
```

注意：

- 运算符和表达式之间必须有空格 - 例如 `2+2` 是不正确的，而应该写成 `2 + 2`。

| 运算符 | 描述 | 示例 |
| --- | --- | --- |
| ! | 逻辑取非。将真条件反转为假，反之亦然。 | [ ! false ] 为真。 |
| -o | 逻辑或 OR。如果操作数之一为真，则条件即为真。 | [ $a -lt 20 -o $b -gt 100 ] 为真。 |
| -a | 逻辑与 AND。如果两个操作数都为真，则条件为真，否则为假。 | [ $a -lt 20 -a $b -gt 100 ] 为假。 |

### 字符串运算符

Bourne Shell 支持以下字符串运算符。
假设变量 `a` 存储 `"abc"`，变量 `b` 存储 `"efg"` –
此示例使用了所有的字符串运算符 –

```bash
#!/bin/sh
a="abc"
b="efg"
```

```bash
if [ $a = $b ]
then
  echo "$a = $b : a is equal to $b"
else
  echo "$a = $b : a is not equal to $b"
fi
```

```bash
if [ $a != $b ]
then
  echo "$a != $b : a is not equal to b"
else
  echo "$a = $b : a is equal to b"
fi
```

```bash
if [ -z $a ]
then
  echo "-z $a : string length is zero"
else
  echo "-z $a : string length is not zero"
fi
```

```bash
if [ -n $a ]
then
  echo "-n $a : string length is not zero"
else
  echo "-n $a : string length is not zero"
fi
```

```bash
if [ $a ]
then
```
