

# 高级 Bash 脚本指南

# 这在脚本中混淆代码的一种诡计方法。
另参见示例 A-56

当同一个函数的多个版本出现在脚本中时会发生什么？

```bash
# 如 Yan Chen 所出，
# 当一个函数被定义多次时，
# 调用的的是最后一个版本。
# 然而，这并不有用。

func () {
  echo "First version of func ("
}

func () {
  echo "Second version of func ("
}

func # 第二 version of func ()

exit $?
```

## 24.1. 复杂函数与函数复杂度

函数可以处理传递给它们的参数，并向脚本返回一个退出状态以便后续处理。

`function_name $arg1 $arg2`

函数通过位置（就像位置参数一样）来引用传递的参数，即 $1, $2 等类推。

示例 24-2. 接收参数的函数

```bash
#!/bin/bash
# 函数与参数

DEFAULT=default
func2 () {
  if [ -z "$1" ];
  then
    echo "-Parameter $1 is zero length." # 无参数值。
  else
    echo "-Parameter $1 is \$1-" # 参数 #1 是否长度为零？
  fi
}

variable=${1-$DEFAULT}
echo "-variable = $variable"
# 参数替换显示了什么？
# 它区分了
```

第 24 章. 函数
402

# 高级 Bash 脚本指南

```bash
#+ 无参数以及一个空参数。

if [ "$2" ]
then
    echo "-Parameter #2 is \$2-"
fi

    return 0
)
echo
echo "Nothing passed."
func2 # 不带参数调用
echo

echo "Zero-length parameter passed."
func2 "" # 带零长度参数调用
echo

echo "Null parameter passed."
func2 "$uninitialized_param" # 带未初始化参数调用
echo

echo "One parameter passed."
func2 first # 带一个参数调用
echo

echo "Two parameters passed."
func2 second # 带两个参数调用
echo

echo "\"second passed."
func2 "" second # 带零长度第一个参数调用
echo # 且是 ASCII 字符串作为第二个。
```

`shift` 命令作用于传递给示例 36-18 的参数。
但是，传递给脚本的命令行参数呢？函数能看到它们吗？嗯，让我们消除这种困惑。

# 示例 24-3. 函数与传递给脚本的命令行参数

```bash
#!/bin/bash
# func-cmdlinearg.sh
# 使用命令行参数调用此脚本，
# 类似于 $0 arg1。

func() {
    echo "$1" # 回显传递给函数的第一个参数。
    # 命令行参数符合条件吗？
}
echo "First call to function: no arg passed.".
```

第 24 章. 函数

# 高级 Bash 脚本指南

与某些编程语言不同，shell 脚本通常向函数传递值参数。变量名（即指针）如果作为参数传递给函数，将被视为字符串字面量。函数会按字面意思解释它们的参数。

间接变量引用（参见示例 37-2）提供了一种笨拙的机制，用于向函数传递变量指针。

# 示例 24-4. 向函数传递间接引用

下一个问题是参数在传递给函数*之后*是否可以被解引用。

# 示例 24-5. 对传递给函数的参数进行解引用

第 24 章. 函数

# 高级 Bash 脚本指南

```bash
x=`eval \expr \"$y\"`
echo $1=$x
eval $1="Some Different Text \"" # 分配新值。
}
```

```bash
Junk=Some Text
echo $Junk #before Some Text before
dereference Junk
echo $Junk #after Some Different Text after
```

```bash
exit 0
```

# 示例 24-6. 再次对传递给函数的参数进行解引用

```bash
#!/bin/bash
# ref-params.sh: 对传递给函数的参数进行解引用。
# (复杂示例)
```

```bash
ITERATIONS=3 # 获取输入的次数。
icount=1
```

```bash
my_read() {
# 带有 my_read varname 调用，
# 输出括号之间的之前的值作为默认值，
# 然后为新值留出空间。
```

```bash
local local_var
echo -n "Enter a value " # 之前的值。
eval 'echo -n "${[$1]}" ' # 更容易理解，
eval echo -n "${[$1]}" # 在用户提示中丢失了尾随空格。
```

```bash
read local_var
[ -n "$local_var"] && eval $1=$local_var
```

```bash
# "与列表"：如果 "local_var" 则将 "$1" 设置为其值。
```

```bash
echo
```

```bash
while [ "$icount" -le "$ITERATIONS" ]
do
my_read var
echo "Entry \$icount = $var"
let icount += 1
```

```bash
echo
done
```

```bash
# 感谢 Steph Chazelas 提供的这个启发性示例。
```

```bash
exit 0
```

# 退出与返回

退出状态

# 高级 Bash 脚本指南

函数返回一个值，称为退出状态。这比比命令返回的退出状态。退出状态可以通过 `return` 语句显式指定，否则它是函数中最后一个命令的退出状态（成功为 0，非零为错误代码）。可以通过引用 `$` 在脚本中使用退出状态。这种机制允许脚本函数具有类似于 C 函数的返回值。

`exit` 终止函数。`return` 命令 [109] 可选接受一个整数参数，该参数作为函数的“退出状态”返回给调用脚本，此退出状态被赋值给变量 `$?`。

# 示例 24-7. 两个数字的最大值

```bash
#!/bin/bash
# max.sh 两个整数的最大值。

E_PARAM_ERR=251 # 如果传递给函数的参数少于2 个
EQUAL=2 # 如果两个参数相等。
# 错误值超出可能输入函数的
# 参数的范围。

max2 (2) # 返回两个数字中较大的一个。
{
```
