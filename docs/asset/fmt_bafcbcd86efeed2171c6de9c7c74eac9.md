
# 第 9 章 编写 Shell 脚本

Linux 广泛使用 Shell 脚本在启动时启动系统服务。你应该查看 `/etc/rc.d/init` 目录。该目录包含了启动和停止各种系统服务所需的脚本。你可能已经根据要求启动、停止或重启其中某些服务。如果你没有使用 TurboService 来执行这些操作，那么你很可能使用了以下 init 脚本之一：

```bash
/etc/rc.d/init/httpd restart
```

这条单条命令实际上执行了一个为你执行了许多操作的脚本。在本章稍后的部分，我将逐步解析一个真实的系统脚本，它包含了许多你应该熟悉的常用脚本功能。

## 基础形式

Shell 脚本的基础形式如列表 9-1 所示。示例的大部分使用了纯英语说明，并解释了脚本的关键元素。

列表 9-1：`Example09-01.sh`

```bash
#!/bin/sh

# 此文件的第一行指示了使用什么 shell
# 来解释此文件中的命令。
# 在此示例中，/bin/sh 是要使用的命令解释器。
# 你应该注意 /bin/sh 仅仅是 /bin/bash 的符号链接
# 你也可以同样方便地指定 #/bin/bash 或 #/bin/tcsh
# 取决于你的 shell 好
```

除第一行外，`#!` 右侧的所有内容都会被命令解释器忽略。这就是你向脚本添加注释的方法。它们让理解脚本在做什么变得容易得多。

最后，你脚本的主体将出现在文件第一行 `/bin/sh` 下方的某个位置。主体应该包含符合命令 shell 规范的正确命令。你可以在脚本中执行任何你在提示符处执行的命令。

对于此示例，我将简单地使用 `echo` 命令输出一个强制性的 "Hello World" 脚本。

```bash
echo "Hello World" # 打印 "Hello World"

#--End Of Script--
```

前面的脚本在文本窗口中打印了“Hello World”。虽然这并不有用，但它演示了一个功能性脚本。在运行此脚本之前，必须赋予它必要的权限：

- `chmod +x example.sh`
- `./example.sh`
- Hello World

搞定！“Hello World。”

本章的其余部分介绍了可以在 Shell 脚本中进行的其他操作，以帮助自动化你的工作。到结束时，你应该能够查看现有的 Shell 脚本，理解它们，甚至根据你的需求修改它们。

## 变量和数组

变量是存储存储的键值对。定义变量的语法如下：

```bash
name=value
```

使用 `$` 或 `${}` 来引用变量。注意不要在等号两边留空格。

```bash
name="Hello World"
echo $name
```

你还可以使用局部变量：

```bash
my_function() {
    local var="local"
    echo $var
}
```

数组允许存储多个值。定义数组的语法如下：

```bash
array=(val1 val2 val3)
```

访问数组元素的方法：

```bash
echo ${array[@]}   # 获取所有元素
echo ${array[0]}   # 获取第一个元素
```

你可以向数组添加元素：

```bash
array+=("new_val")
```

删除数组元素：

```bash
unset array[1] # 删除索引为1的元素
unset array   # 删除整个数组
```

遍历数组：

```bash
for i in "${array[@]}"; do
    echo $i
done
```

关联数组（Associative Arrays）需要`Bash` 4.0+：

```bash
declare -A my_map
my_map[key1]="value1"
my_map[key2]="value2"
echo ${my_map[@]}   # 获取所有值
echo ${!my_map[@]}  # 获取所有键
```

## 算术运算

使用 `(( ))` 进行算术运算：

```bash
a=$((1 + 2)) # 加法
a=$((a - )) # 减法
a=$((a * 2)) # 乘法
a=$((a / b)) # 除法
a=$((a % b)) # 取模
```

自增自减：

```bash
((a++))
((a--))
```

## 条件

使用 `[ ]` 或 `[[ ]]` 进行条件判断：

```bash
if [ $a -gt 10 ]; then
    echo "Greater than 10"
elif [ $a -eq 10 ]; then
    echo "Equal to 10"
else
    echo "Less than 10"
fi
```

`[[ ]]` 更强大，支持通配符和：

```bash
if [[ $str == *pattern* ]]; then
    echo "Matched!"
fi

if [[ $str =~ ^[0-9]+$ ]]; then
    echo "Is a number"
fi
```

定义和调用函数：

```bash
my_function() {
    echo "Argument 1: $1"
}
my_function "Hello"
```

## 循环

`for` 循环：

```bash
for i in 1 2 3; do
    echo $i
done
```

`while` 循环：

```bash
i=1
while [ $i -le 3 ]; do
    echo $i
    ((i++))
done
```

## 示例

```bash
#!/bin/bash
# 简单的脚本示例
echo "Enter your name:"
read name
echo "Hello, $name!"
```

```bash
echo "Give me the second number, num2: "
read num2
echo "The sum of num1 and num2: $(($num1 + $num2))"
```
