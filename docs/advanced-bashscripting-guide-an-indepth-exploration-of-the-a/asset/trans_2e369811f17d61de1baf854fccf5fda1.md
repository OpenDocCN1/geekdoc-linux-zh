

## 进阶 Bash 脚本指南

```bash
exit 0
```

另请参见示例 10–27。

函数返回的最大正整数是 256。`return` 命令与退出状态（exit status）的概念紧密相关，而这一概念导致了这种特定的限制性。坦率地说，对于那些需要函数返回大整数值的情况，有多种变通方法。

## 23–5. 在函数中测试大返回值

```bash
#!/bin/bash
# return-test.sh

# 函数可以返回的最大正值是 256。

return_test ()      # 返回传递给它的任何值（作为退出状态）。
{
    return $1
}

return_test 27      # o.k.
echo $?               # 返回 27。

return_test 256     # 仍然 o.k.
echo $?               # 返回 256。

return_test 257     # 错误！
echo $?               # 返回 1（各种错误的返回代码）。

return_test -151896  # 然而，大的负数可以工作。
echo $?               # 返回 -151896。

exit 0
```

正如我们所见，函数可以返回一个大的负值。通过一些技巧，这同时也允许返回大的正整数。

实现此点的另一种方法是简单地将“返回值”赋值给全局变量。

```bash
Return_Val=      # 用于保存函数超范围返回值的全局变量。

alt_return_test ()
{
    fvar=$1
    Return_Val=$fvar
    return              # 返回 0（成功）。
}

alt_return_test 1   # 0
echo $?               
echo "return value = $Return_Val"  # 1
```

## 23.1. 复杂函数与函数复杂度

## 进阶 Bash 脚本指南

```bash
alt_return_test 256
echo "return value = $Return_Val"    # 256

alt_return_test 257
echo "return value = $Return_Val"    # 257

alt_return_test 25701
echo "return value = $Return_Val"    # 25701
```

## 示例 2-6. 比较两个大整数

```bash
#!/bin/bash
# 大整数的最大值
# max2.sh: 两个大整数的最大值

# 这是之前的 "max.sh" 示例，
# 经过修改允许比较大整数。

EQUAL=0                              # 两个参数都相等。
MAXRETVAL=256                      # 函数返回的最大正值。
E_PARAM_ERR=-99999                  # 参数错误。
E_NPARAM_ERR=-9999999              # “归一化”的参数错误。

max2()\                              # 返回两个数中较大的。
if [ -z "$2" ]
then
    return $E_PARAM_ERR
fi

if [ "$1" -eq "$2" ]
then
    return $EQUAL
else
    if [ "$1" -gt "$2" ]
then
    retval=$1
else
    retval=$2
fi

# 这是一个允许从此函数返回大整数的变通方法。
if [ "$retval" -gt "$MAXRETVAL" ]    # 如果超出范围，
then
    let retval=$(( 0 - $retval ))     # 调整为负值。
    # (( 0 - $VALUE )) 改变值的符号。
fi

# 幸运的是，允许大的“负”返回值。
#
    return $retval
}

max2 33001 33997
return_val=$?

#
if [ "$retval" -lt 0 ]              # 如果是“调整过的”负数，
then
    # then
```

## 23.1. 复杂函数与函数复杂度

## 进阶 Bash 脚本指南

```bash
let "return_val = (( 0 - $return_val ))" # 归一化为正数。
fi # $return_val 的“绝对值”。

if [ "$return_val" -eq $E_PARAM_ERR ]; # 参数错误“标记”也会被改变。
then
echo "Error: 参数太少。"
elif [ "$return_val" -eq $EQUAL ];
then
echo "两个数字相等。"
else
echo "两个数字中较大的是 $return_val。"
fi

exit 0
```

另请参见示例 A–7。

**练习：** 使用我们刚刚学到的知识，扩展之前的罗马数字示例以接受任意大小的输入。

## 重定向

*重定向函数的标准输入*

函数本质上是一个代码块，这意味着它的标准输入可以重定向（如示例 4–1）。

## **示例 23–7. 从用户名获取真实名**

```bash
#!/bin/bash

# 从用户名从 /etc/passwd 获取“真实名”。
ARGCOUNT=1  # 期望一个参数。
EWRONGARGS=65

file=/etc/passwd
pattern=$$

if [ $# -ne "$ARGCOUNT" ];
then
    echo "用法: `basename $0` USERNAME"
    exit $E_WRONGARGS
fi

file_excerpt () {
    # 扫描文件中的模式，打印行的相关部分。
    while read line; do # while line 并不一定需要 "[condition"
        echo "$line" | grep "$pattern" | awk -F":" '{print $5}' # 让 awk 使用 ":" 分隔符
    done < "$file" # 文件重定向到标准输入。
}

file_excerpt $pattern

# 是的，整个脚本可以简化
```

## 23.1. 复杂函数与函数复杂度

## 进阶 Bash 脚本指南

```bash
# grep PATTERN /etc/passwd | awk -F:"' '{ print $5 )
# or awk -F:/PATTERN/ (print $5 )
# or or awk -F:{$1 == "username" { print $5 } # 从用户名
# 然而，它可能没有那么有意义。

exit 0
```

另一种可能不那么混乱的重定向函数输入的方法是将标准输入重定向到函数内部嵌入的括号代码块。

```bash
# 代替：
Function ()
{
  ...
} < file

# 尝试这个：
Function ()
{
  ...
} < file

# 同样，
Function () # 这可以工作。
{
  ...
} <
```

## 23.1. 复杂函数与函数复杂度

## 进阶 Bash 脚本指南

## 23.2. 局部变量

什么让变量变为局部？

声明为局部的变量仅在它所在的块中可见。在调用函数之前，函数内部声明的所有变量在函数体外部都是见的。

## 23.2. 局部变量

## 进阶 Bash 脚本指南

```bash
func ()
{
  local_var=37      # 声明为局部。
  echo $local_var   # 在函数内部可见
}
func
echo $local_var       # 此处可见
```

## 23.2.1. 局部变量

局部变量使得递归可能，但这种做法通常涉及大量的开销且执行缓慢，因此通常不适合在脚本中使用。

## 示例 23–9. 使用局部变量的递归

```bash
#!/bin/bash
factorial
--------
```

