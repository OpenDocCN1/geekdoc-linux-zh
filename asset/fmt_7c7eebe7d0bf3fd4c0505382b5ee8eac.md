
```
16580

$ $ echo((-15928 & -32500))

-32504

$ $ echo((-15928 | -32500))

-15924

$ $ echo((-15928 ^ -32500))

16580
```

# 练习 3-11. 位移：

以下是位移的结果：

# 练习答案

* `25649 >> 3` = `0110 0100 0011 0001 >> 3` = `0110 0100 0011 0` = `0000 1110 1000 0110` = `3206`

* `25649 << 2` = `10 0101 0011 0001 -> 1001 1000 0110 0100 -> 1111 1111 1100 1100` = `-28476`

* `-9154 >> 4` = `1101 1100 0011 1110 >> 4` = `1101 1100 0011 -> 1111 1101 1111 1000 0010 0011 1101` = `-573`

* `-9154 << 3` = `1101 0011 0011 1110 << 3` = `1 1101 0011 1110 -> 1001 1101 0011 0000` = `-7696`

这些 Bash 命令应该计算出：

```
$ echo $((25649 >> 3))

3206

$ echo $((25649 << 2))

102596

$ echo \$((-9154 >> 4))

-573

$ echo \$((-9154 << 3))

-73232
```

Bash 对第二和第四种情况给出了不同的结果。这是因为 Bash 将所有整数存储在八字节中。

使用在线计算器检查你的计算。

# 练习 3-12. 循环结构

玩家有七次猜数字的机会。相同的算法处理每次尝试。因此，我们可以应用带有多次迭代的循环。以下是玩家操作算法：

1. 使用 `read` 命令读取输入。
2. 将输入的数字与脚本选择的数字进行比较。
3. 如果玩家出错，打印提示并返回到第 1 步。
4. 如果玩家猜中了，结束脚本。

脚本可以使用 `RANDOM` 变量来选取随机数。该变量每次在你读取它时都会返回一个 0 到 32767 之间的随机值。我们需要一个 1 到 100 之间的数字。以下算法将其：

1. 获取一个 0 到 99 之间的随机数。为此，使用以下公式将 `RANDOM` 变量除以 100：`number=$((RANDOM % 100))`
2. 获取一个 1 到 100 之间的数字。为此，在之前的结果加 1。这是计算 1 到 100 之间随机数的完整公式：`number=$((RANDOM % 100 + 1))`

列表 5-6 显示了实现游戏算法的脚本。列表 5-6 关于“大”或“小”的脚本：

```bash
#!/bin/bash

number=$((RANDOM % 100 + 1))

for i in {1..7}
do
	echo "请输入数字:"
	read input
	if (( input < number )); then
		echo "$input 小"
	elif (( input > number )); then
		echo "$input 大"
	else
		echo "你猜对了"
		exit 0
	fi
done

echo "你没猜中"
```

背后的思想是将一旦游戏开始，我们有一个 1 到 100 之间的数字。这个范围的中间值是 50。输入这个值。脚本将给你第一个提示。假设脚本打印 50 小于你要找的数字。这意味着你应该在 50 到 100 的范围内搜索。输入这个范围的中间值，即 75。答案同样小于你要找的数字。结论是你要找的数字在 75 到 100 之间。你可以用这种方法计算这个范围的中间：75 + (100 - 75) / 2 = 87.5。向上取整还是向下取整没有关系。向下取整得到数字 87。如果数字还没猜中，保留范围。这样你有足够的步骤找到正确的数字。

# 练习 3-13. 函数

我们在“脚本中的函数”部分考虑了 `code_to_error` 函数。让我们将 `print_error` 和 `code_to_error` 函数合并到一个文件中。我们将得到列表 5-7 的脚本。列表 5-7 用于打印错误消息：

```bash
#!/bin/bash

code_to_error()
{
	case $1 in
	1)
		echo "未找到文件"
		;;
	2)
		echo "拒绝访问文件"
		;;
	esac
}

print_error()
{
echo "$(code_to_error $1)" >> debug.log
}

print_error 1 "readme.txt"
```

现在 `code_to_error` 函数打印英文消息。让我们将其重命名为 `code_to_error_en`。这样可以通过函数名看出语言。让我们向脚本添加一个 `code_to_error_de` 函数。它根据接收到的错误代码打印德语消息。函数如下：

```bash
code_to_error_de()
{
    case $1 in
        1)
            echo "Datei wurde nicht gefunden"
            ;;
        2)
            echo "Berechtigung zum Lesen der Datei verweigert"
            ;;
    esac
}
```

现在我们需要在 `print_error` 中选择调用哪个 `code_to_error` 函数。我们可以检查区域设置。环境变量 `LANG` 存储了这些设置。如果变量的值匹配 `de_DE*` 模式，则调用 `code_to_error_de`。否则，调用 `code_to_error_en`。

列表 5-8。脚本的完整代码。列表 5-8。打印错误消息的脚本：

```bash
#!/bin/bash

code_to_error_de()
{
    case $1 in
        1)
            echo "Datei wurde nicht gefunden"
            ;;
        2)
            echo "Berechtigung zum Lesen der Datei verweigert"
            ;;
    esac
}

code_to_error_en()
{
    case $1 in
        1)
            echo "File not found"
            ;;
        2)
            echo "Permission to read the file denied"
            ;;
    esac
}

print_error()
{
  if [[ "$LANG" == de_DE* ]]
  then
    echo "$(code_to_error_de $1)" "$2" >> debug.log
  else
    echo "$(code_to_error_en $1)" "$2" >> debug.log
  fi
}
```

你可以用 `case` 替换 `print_error` 函数中的 `if` 语句。例如，可以这样写：

```bash
print_error()
{
  case $LANG in
    de_DE*)
      echo "$(code_to_error_de $1)" "$2" >> debug.log
      ;;
    en_US*)
      echo "$(code_to_error_en $1)" "$2" >> debug.log
      ;;
    *)
      ;;
  esac
}
```

当需要支持两种语言时，`case` 语句非常方便。

# 练习解答

结合 `LANGUAGE` 变量的值和错误代码。如列表 5-9 所示的 `print_error` 函数。

列表 5-9. 打印错误消息的脚本

```bash
#!/bin/bash

print_error()
{
  declare -A messages
  messages["de_DE",1]="Datei wurde nicht gefunden:"
  messages["de_DE",2]="Berechtigung zum Lesen der Datei verweigert"
  messages["en_US",1]="File not found"
  messages["en_US",2]="Permission to read the file denied"
  echo "${messages[$LANGUAGE,$1]}" >> debug.log
}

print_error 1 "readme.txt"
```

# 练习 3-14. 变量作用域

列表 33-37 中的脚本打印以下文本：

```
main1: var var =
foo1: var = foo_value
bar1: var = foo_value
bar2: var = bar_value
foo2: var = bar_value
main2: var =
```

让我们从 "main1" 和 "main2" 字符串的输出开始。`var` 变量在 `foo` 函数中声明为局部变量。它只在 `foo` 和 `bar` 函数中可用。因此，bash 支持在未声明 `var` 之前调用 `foo` 函数。

当我们从 `foo` 函数的开始打印 `var` 的值时，我们它等于 "foo_value"。
接下来是 "bar1" 的输出。`var` 变量在 `foo` 函数中声明。该函数调用了 `bar`。因此，`bar` 函数体是 `var` 的作用域。

然后我们将新值 "bar-value" 赋值给 `var`。注意，我们并没有声明一个名为 `var` 的新全局变量，而是重写了一个现有的局部变量。我们在 "bar2" 和 "foo2" 输出中都得到了它的值 "bar_value"。

# 有用链接

## 通用信息

- 电子计算机的历史$^{490}$
- 苹果操作系统历史$^{491}$
- 关于静态类型和动态类型的文章$^{492}$

## Bash

- Machtelt Garrels 编写的《初学者 Bash 指南》$^{493}$
- Mendel Cooper 编写的《高级 Bash 脚本指南》$^{494}$
- Bash Shell 查表$^{495}$
- Bash 参考手册$^{496}$
- Bash Hackers Wiki$^{497}$
- Bash 陷阱$^{498}$
- 徒劳用 Cat 奖 (Useless Use of Cat Award)$^{499}$
- 带有示例的 grep 正表达式$^{500}$
- Bash 最佳实践$^{501}$
- 基于 mywiki.wo.org 的 Bash 风格指南$^{502}$
- Google 编写的 Shell 风格指南$^{504}$
- 在线 Bash 命令分析器$^{505}$
- Bash 脚本本地化指南$^{506}$

# Unix 环境

- Eric S. Raymond 编写的《Unix 编程艺术》$^{507}$

$^{507}$http://www.catb.org/~esr/writings/taoup
