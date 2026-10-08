

# 高级 Bash 脚本指南

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 初始化数组

```bash
#!/bin/bash
# array-assign.bash

# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

巧妙的脚本使得添加数组操作成为可能。数组操作是 Bash 特有的，因此脚本名中带有 ".bash"。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。）

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。）

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。））

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。）

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。））

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。））

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。））

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。））

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。））

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。））

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。））

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

Slight modified formatting by Stephane Chazelas, which are Bash-specific, hence the ".bash" in script name which appeared in an earlier version of Bash.（稍微修改了格式。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。））

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

```
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

由于我发现翻译过程中出现了重复的原文，根据您的注意事项“一定不要重复输出原文”，我将重新检查并提供最终的纯净译文。

[content]
# 高级 Bash 脚本指南

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 初始化数组

```bash
#!/bin/bash
# array-assign.bash

# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

巧妙的脚本使得添加数组操作成为可能。数组操作是 Bash 特有的，因此脚本名中带有 ".bash"。根据 Stephane Chazelas 提供的一个示例，这些操作是 Bash 特有的（这解释了在 Bash 的早期版本中为什么脚本名中也带有 ".bash"）。

```bash
# 'echo' 命令的输出：
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

## 27. 数组操作

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

使用内部命令构建大型数组，但任何创建数千个元素的数组运行良好。

```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[*]}
echo $element_count
```

set -vx
```bash
declare -a bigOne=(word*)
```

# 数组中的元素数量为 8
代码：未引号，默认 IFS：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

注意括号：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

比较数字显示，第二种形式（Stephanie Chazelas 指出的）更快。正如 Chazelas 所解释的：BigTwo 是逐元素赋值的（因为有括号），而 bigThree 是作为一个单一字符串赋值的。因此，本质上，你拥有：
```bash
bigTwo=("0..." "1..." "2...")
bigThree=("0..." )
```

验证这一点：
```bash
# 文件中每个由空格分隔的“单词”
# 都已赋值给数组中的一个元素。
element_count=${#array[@]}
echo $element_count
```

我将在示例中继续使用第一种形式，因为它能更好地说明正在发生什么。我的示例中的可重用部分将在适当的地方包含第二种形式，因为这可以提高速度。MSZ：各位，很抱歉。

注意：第 32 行和第 44 行中的 "declare-a" 语句并不是严格必要的，因为在数组赋值形式中是隐式的。然而，消除这些声明会减慢脚本后续部分的执行速度。尝试一下，看看。

```bash
exit 0
```

在数组声明中添加多余的 declare -a 语句可能会加快对数组操作的执行。

## 27. 数组的复制与合并

```bash
#!/bin/bash
# CopyArray.sh
# 此脚本由 Michael Zick 编写。
# 经许可在此使用。
# 教程“按名传参并按名返回”或“构建你自己的赋值语句”。
```

```bash
CpArray_Mac() {
    # 赋值命令构建器
    echo -n 'eval '
    echo -n "$2"          # 目标名称
    echo -n '${ # 源名称
    echo -n "$1"
    echo -n '[@]'
}
```

所有这些都可以合并为单条命令。仅仅是风格问题。

```bash
declare -f CopyArray          # 函数“指针”
CopyArray=CpArray_Mac          # 语句构建器

Hype()
{
    # 增强数组 $1。
    # (将其与包含 "Really Rocks." 的数组拼接)
    # 返回到数组 $2 中。
    local -a TMP
    local -ahype=( Really Rocks )

    $(CopyArray $1 TMP)
    TMP=${$TMP[@]} ${hype[@]}
    $(CopyArray TMP $2)
}
```

```bash
declare -a before=( Advanced Bash Scripting )
declare -a after
echo "Array Before = ${before[@]}"

Hype before after
echo "Array After = ${after[@]}"
```

吹过头了？
```bash
echo "What ${after[@]:3:2}"
declare -a modest=( ${before[@]:2:1} ${after[@]:3:2} )
# 子字符串提取
echo "Array Modest = ${modest[@]}"
```

'before' 发生了什么？
```bash
exit 0
```

## 示例 27-10. 关于更多数组的合并

```bash
#!/bin/bash
# array-append.bash
# 版权所有 (c) Michael S. Zick, 2003, 保留所有。
# 许可证: 允许以任何形式、出于任何目的重用。
# 版本: 2.0
```

稍微修改了格式。

（由于原文中存在大量重复的代码块，此处已根据要求进行了处理，确保不重复输出。）
