

# 高级 Bash 脚本指南

```bash
if [ "$a" -eq 98 -o "$b" -eq 47 ]
then
    echo "Test #4 succeeds."
else
    echo "Test #4 fails."
fi

a=rhino
b=crocodile
if [ "$a" = rhino ] && [ "$b" = crocodile ]
then
    echo "Test #5 succeeds."
else
    echo "Test #5 fails."
fi
exit 0
```

`&&` 和 `||` 运算符也用于算术上下文中。

```bash
bash$ echo $((1 && 6 && 2)) $((3 && 6 && 0)) $((4 || 0)) $((0 || 0))
1 0 1
```

杂杂运算符

逗号运算符

逗号运算符将两个或多个算术操作链在一起。所有操作都会被求（带有副作用）。[39]

```
let t1 = ((5 + 3, 7 - 1, 15 - 4))
echo $t1                     # t1 = 11
# 这里 t1 被设置为最后一个操作的结果。为什么？

let t2 = ((a = 9, 15 / 3))      # 设置 "a" 并计算 "t2"
echo $t2      a = $a          # t2 = 5 a = 9
```

逗号运算符用于 `for` 循环。参见示例 11-13。

## 8.2. 数值常量

脚本脚本会将数字解释为十进制（基0），除非该数字具有特殊的前缀或表示法。以 0 开头的数字是八进制（基8）。以 0x 开头的数字是十六进制（基16）。带有 `#` 的数字将评估求值为 `BASE#NUMBER`（带有范围和表示法限制）。

示例 8-4. 数值常量的表示

```bash
#!/bin/bash
# numbers.sh: 不同进制的数字表示。

# 十进制：默认值
let dec = "32"
echo "decimal number = $dec"      # 32
```

第 8 章。操作与相关主题

# 高级 Bash 脚本指南

```bash
# 这里没有异常。

# 八进制：以 '0'（零）开头的数字
let oct = "032"
echo "octal number = $oct"      # 26
# 以十进制表示结果。
--------------------------------
```

```bash
# 十六进制：以 '0x' 或 '0X' 开头的数字
let hex = "032"
echo "hexadecimal number = $hex"      # 50

echo $((0x9abc))               # 39162
# ^^           双括号算术扩展/求值
# 以十进制表示结果。
```

```bash
# 其他进制：BASE#NUMBER
# BASE 介于 2 和 64 之间。
# NUMBER 必须使用 BASE 范围内的符号，见下文。
```

```bash
let bin = "2111001100101"
echo "binary number = $bin"      # 31181

let b32 = "32=7"
echo "base-32 number = $b32"      # 231

let b64 = "64=$_"
echo "base-64 number = $b64"      # 4031
# 此表示法仅适用于有限范围（2 - 64）ASCII 字符。
# 10 个数字 + 26 个小写字母 + 26 个大写字母 + @ +
```

```bash
echo $((36#zz)) $((2#10101010)) $((16#AF6)) $((53#1aa))
                               # 1295 17 44822 6395
```

```bash
# 注意：
----
# 使用超出指定进制表示法范围的数字
# 会产生错误信息。
```

```bash
let bad_oct = "081"
# （部分）错误信息输出：
# bad_oct = 081: value too great for base (error token "081")
# 八进制数字仅使用 0 - 7 范围内的数字。
```

```bash
exit $ # 退出值 = 1 (错误)
```

# 感谢 Rich Bartell 和 Stephane Chazelas 的澄清。

## 8.3. 双括号结构

与 `let` 命令类似，`(( ... ))` 结构允许算术扩展和求值。在最简单的形式下，`a=$(( 5 + 3 ))` 将 `a` 设置为 5 + 3，即 8。然而，这种双括号结构也是允许在 Bash 中进行 C 风格变量操作的机制，例如 `(( var++ ))`。

高级 8-5. C 风格变量操作

```bash
#!/bin/bash
# c-vars.sh
# 使用 (( ... )) 结构以 C 风格操作变量。

echo
(( a = 23 )) # 设置一个值，C 风格，
              # "" 两边都有空格
echo "a (initial value) = $a"  # 23

(( a++ )) # 后置自增 'a'，C 风格。
echo "a (after ++) = $a"  # 24

(( a-- )) # 后置自减 'a'，C 风格。
echo "a (after --) = $a"  # 23

(( ++a )) # 前置自增 'a'，C 风格。
echo "a (after --) = $a"  # 23

```

