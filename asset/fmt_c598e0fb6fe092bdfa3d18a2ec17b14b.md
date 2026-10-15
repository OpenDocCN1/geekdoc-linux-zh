
```
delentry

$CLEAR ;;

"修改日历条目")

checkdate

changeentry

$CLEAR ;;

"查找日历条目")

checkdate

findentry

$CLEAR ;;

"列出所有日历条目")

formatentry $CALFILE

$CLEAR ;;

"列出今日日历条目")

DATE=$(date +%m-%d-%y)

findentry

$CLEAR ;;

"退出")

exit ;;

* )

print "\a无效的选择 \c"

read TMP?- 按 <Return> 继续"

$CLEAR ;;

continue ;;

esac

done

done
```

# 附录 E：Korn Shell 手页

`ksh`, `rsh` - Korn shell, 一标准/受限制命令和编程语言

## 语法

```
ksh [+/-abcefhikmnopprstuvxCD] [-R] [/-o option] [-arg]
rsh [+/-abcefhikmnopprstuvxCD] [-R] [/-o option] [-arg]
```

## 描述

`ksh` 是一种从终端或文件读取并执行命令的命令和语言。`Rsh` 是标准命令解释器 `ksh` 的限制版本；它用于设置登录名和执行环境，其功能比标准的 Korn shell 更受控制。请参见“调用”以了解 shell 参数的含义。

## 定义

元字符是以下字符之一：

- `;` `&` `(` `)` `|` `<` 换行 空格 制表符

空白是指制表符或空格。标识符是字母、数字或下划线的序列，以字母或下划开头。标识符用于变量名的组成部分。名称是由一个或多个由 `.` 分隔的标识符组成的，可选前缀 `.` `.` `Vnames` 用于函数名和变量名。

# Korn Shell 用户与编程手册

`for identifier [ in word ... ]; do list ; done`

每次执行 `for` 命令时，`identifier` 被设置为单词列表中的下一个单词。如果省略了 `[in word ...]`，则 `for` 命令将为每个已设置的位置参数执行一次 `do list` 列表（参见“参数替换”下方）。当列表中没有更多单词时执行结束。

`for (( [ expr1 ] ; [ expr2 ] ; [ expr3 ] )); do list : done`

首先评估算术表达式 `expr1`（参见“算术求值”下方）。重复评估算术表达式 `expr2` 直到其结果为零，当结果为非零时，执行 `list` 并评估算术表达式 `expr3`。如果任何表达式被省略，其行为等于评估为 `1`。

`select identifier [ in word ... ]; do list ; done`

`select` 命令在标准错误（文件描述符 `2`）上打印一组单词，每个单词前面都有一个数字。如果省略了 `[in word ...]`，则改用位置参数（参见“参数替换”下方）。打印 `PS3` 提示并从标准输入读取一行。如果此行包含列出的单词之一的数字，则参数 `identifier` 的值将被设置为该数字对应的单词。如果此行为空，则再次打印选择列表。从标准输入读取的内容的内容保存在参数 `REPLY` 中。对于每次选择执行 `list`，直到遇到 `break` 或文件结束。

`case word in | ([pattern] [ | pattern ] ... ) list ;; esac`

`case` 命令执行与

# 附录 E: Korn Shell 手页

第一个匹配的模式。模式的格式与文件名生成使用的格式相同（见下文“文件名生成”）。

```
if list ; then list elif list ; then list ... ; else list ; fi
```

执行 `if` 之后的 `list`，如果它返回退出状态为零（成功），则执行第一个 `then` 之后的列表。
否则，执行 `elif` 之后的列表，如果其值为零，则执行下一个 `then` 之后的列表。
如果都不满足，则执行 `else` 列表。如果没有执行 `else list` 或 `then list`，则 `if` 命令返回退出状态零（成功）。

```
while list ; do list ; done

until list ; do list ; done
```
