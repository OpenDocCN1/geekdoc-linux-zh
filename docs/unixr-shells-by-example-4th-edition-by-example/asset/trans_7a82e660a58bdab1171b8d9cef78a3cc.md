

# 表 2.2 Bourne Shell 语法和结构（续）

| 算术 | Bourne shell 不支持算术。必须使用 UNIX/Linux 命令来进行计算。 |
| 运算符 | Bourne shell 使用内置 test 命令运算符来测试数字和字符串。 |
| 条件语句 | if 结构后面跟着一个命令。如果要测试一个表达式，则将其用方括号括起来。then 关键字放在闭合括号之后。if 必须以 fi 结束。 |

**示例**
```
n= `expr 5 + 5`
echo $n
```

**示例**
相等：
=      string
!=     string
-eq    number
-ne    number

逻辑：
-a     and
-o     or
!      not

关系：
-gt    greater than
-ge    greater than, equal to
-lt    less than
-le    less than, equal to

**示例**
The if construct is:                     The if/else construct is:
if command                              if [ expression ]
then                                    then
block of statements                     block of statements
fi                                      else
                                        block of statements
                                        fi

if [ expression ]
then
  block of statements
fi

# 表 2.2 Bourne Shell 语法和结构（续）

| 条件语句（续） | if/else/else if 结构是： |
| case 命令结构是： |

The if/else/else if construct is:
if command
then
  block of statements
elif command
then
  block of statements
elif command
then
  block of statements
else
  block of statements
fi
-------------------------------
if [ expression ]
then
  block of statements
elif [ expression ]
then
  block of statements
elif [ expression ]
then
  block of statements
else
  block of statements
fi

The case command construct is:
case variable_name in
  pattern1)
    statements
  ;;
  pattern2)
    statements
  ;;
  pattern3)
    statements
  ;;
  *) default value
    ;;
esac

case "$color" in
  blue)
    echo $color is blue
  ;;
  green)
    echo $color is green
  ;;
  red|orange)
    echo $color is red or orange
  ;;
  *) echo "Not a color" # default
esac

## 循环

有三种类型的循环：while、until 和 for。

while 循环后面跟着一个命令或用方括号括起来的表达式、do 关键字、语句块，并以 done 关键字终止。只要表达式为真，do 和 done 之间的语句体就会被执行。

until 循环与 while 循环类似，只是只要表达式为假，循环体就会被执行。

for 循环用于遍历一系列单词，处理一个单词然后将其移出，以处理下一个单词。当所有单词都从列表中移出时，它结束。for 循环后面跟着变量名、in 关键字、单词列表，然后是语句块，并以 done 关键字终止。
循环控制命令是 break 和 continue。

# 示例

```
while command
do
  block of statements
done

while [ expression ]
do
  block of statements
done
```

# 表 2.2 Bourne Shell 语法和结构（续）

| 结构 | 语法 |
|---|---|
| 循环 *(续)* | `until command`<br>`do`<br>&nbsp;&nbsp;&nbsp;&nbsp;block of statements<br>`done`<br><br>`until [ expression ]`<br>`do`<br>&nbsp;&nbsp;&nbsp;&nbsp;block of statements<br>`done` |
|  | `for variable in word1 word2 word3 ...`<br>`do`<br>&nbsp;&nbsp;&nbsp;&nbsp;block of statements<br>`done` |

**文件测试**  Bourne shell 使用 test 命令来评估条件表达式，并内置了一组用于测试文件属性的选项，例如它是否是目录、普通文件（不是目录）、可读文件等等。参见示例 2.3。

# 示例

- `-d` — 文件是目录
- `-f` — 文件存在且不是目录
- `-r` — 当前用户可以读取文件
- `-s` — 文件大小非零
- `-w` — 当前用户可以写入文件
- `-x` — 当前用户可以执行文件

```sh
#!/bin/sh

1  if [ -f file ]
   then
       echo file exists
   fi

2  if [ -d file ]
   then
       echo file is a directory
   fi

3  if [ -s file ]
   then
       echo file is not of zero length
   fi

4  if [ -r file -a -w file ]
   then
       echo file is readable and writable
   fi
```
