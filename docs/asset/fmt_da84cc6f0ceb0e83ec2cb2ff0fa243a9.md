
# 循环关联数组与排序

跟在 `END` 模式后的动作是用于循环关联数组元素的特殊结构。管道将输出发送到 `sort`，以生成按字母排序的汽车列表和库存数量。由于这是一个 shell 脚本而不是 `awk` 程序文件，你必须同时拥有 `manuf` 文件的读取和执行权限才能执行它。

```
$ manuf
awk '{manuf[$1]++}
END
for (name in manuf) print name, manuf[name]}'
cars |
sort
```

```
$ manuf
bmw 1
chevy 3
ford 4
honda 1
plym 1
toyota 1
volvo 1
```

## 通用 shell 脚本 `manuf.sh`

下一个名为 `manuf.sh` 的程序是一个更通用的 shell 脚本，包含了错误检查。该脚本列出文件中某一列的内容，并在命令行指定列名和文件名。第一个动作（`$1` 处）在 `awk` 程序中使用 shell 变量 `$1` 来指定数组索引。由于引号是成对的，引号内部的 `$1` 实际上被引用了：因为这是一个 shell 脚本，shell 会替换 `awk` 命令调用前的第一个参数 `$1`（第 48 页）。该行开头的美元符号会导致 `gawk` 将 shell 替换的内容解释为字段号。

```
$ cat manuf.sh
if [ $# -ne 2 ]
then
    echo "Usage: manuf.sh file"
    exit 1
fi
gawk -v field=$1 '
  {count[$field]++}
  END
  for (item in count) printf "%-20s%20s\n",
    item, count[item]}'
```

```
$ manuf.sh
Usage: manuf.sh file
```

```
$ manuf.sh 1 cars
bmw 1
chevy 3
ford 4
honda 1
plym 1
toyota 1
volvo 1
```

```
$ manuf.sh 3 cars
1965 1
1970 1
1985 2
1998 1
2999 1
2000 1
2001 1
2002 1
2003 2
2004 1
```

## 使用 `-v` 选项传递字段号

在 `awk` 程序中使用引号允许扩展的技巧是使用命令行上的 `-v` 选项将字段号传递给 `gawk` 变量。这种变化使得阅读和调试脚本更容易。调用 `manuf2.sh`：

```
$ cat manuf2.sh
if [ $# -ne 2 ]
then
    echo "Usage: manuf2.sh file"
    exit 1
fi
gawk -v field=$1 '
  {count[$field]++}
  END
  for (item in count) printf "%-20s%20s\n",
    item, count[item]}'
```

## 单词使用统计 `word_usage`

`word_usage` 脚本显示你在命令行指定的文件的用法列表。`tr` 工具（第 804 页）从标准输入列出单词，每行一个。`sort` 工具对文件进行排序，将使用次数最多的单词排在前面。该脚本按字母顺序对相同次数的单词进行分组。

```
$ cat word_usage

tr -cs 'a-zA-Z' '[\n*]' < $1 |

gawk

	count[$1]++

	END

	for (item in count) printf "%-15s%3s\n", item, count[item]'

sort -1nr +1
```

```
$ word_usage textile

the 42

file 29

fsck 27

system 22

you 22

it 17

SIZE 14

and 13

MODE 13
```

## 单词计数 `word_count`

下面是不同格式的类似程序。这种风格模仿了 C 程序，可能更容易阅读和处理复杂的 `awk` 程序：

```
$ cat word_count

tr -cs 'a-zA-Z' '[\n*]' < $1 |

gawk {

	count[$1]++

	END

	for (item in count)

	{

		if (count[item] > 4)

		{

			printf("%-15s%3s\n", item, count[item]

		}' sort -1nr +1
```

`tail` 工具显示输出的最后十行，说明了出现少于五次的单词没有列出：

```
$ word_count textfile | tail

directories 5

if 5

information 5

NODE 5

more 5

no 5

on 5

response 5

this 5

will 5
```

## 生成带日期的报告 `report`

下一个示例显示了在报告中放置日期的方法。`g` 程序的第一行输入来自 `date`。程序将此行读取为第 1 条记录 (`NR == 1`)，进行相应处理，并处理所有与后续模式相关的后续行 (`NR > 1`)。

```
$ cat report

if [ $# -eq 0 ]; then

  echo "You must supply a filename."

  exit 1

fi

(date; cat $1) |

gawk

NR == 1 {print "Report for", $1, $2, $3 " ", $6}

NR > 1 {print $5 "\t" $1'}
```

```
$ report cars

Report for Mon Jan 31, 2005

2500 plym

3000 chevy

10000 ford

9850 volvo

10500 ford

3500 bmw
```

## 汇总文件列 `tally`

下一个示例汇总了文件的每一列；在 `gawk` 调用之前解释了字段号。它使用 `numbers` 文件（第 135 页）来跳过包含非数字条目的行。在程序结束时，`gawk` 显示文件的总和。

```
$ cat tally

gawk ' BEGIN {

  ORS = ""

}

 first ==

 1 {

 (item in

)

  printf("%-20s%3s\n",

, count[

]

1
```

```
# $ tally

跳过 3 条记录：
30 xyz 50 70

跳过 6 条记录：
60 30 45.0 66.1

跳过 11 条记录：
110 123 50 57.5

# $ cat tally.out

10.00 20.00 30.30 40.50
20.00 30.00 45.70 66.10
40.00 75.00 107.20 55.60
50.00 20.00 30.30 40.50
70.00 1134.70 50.00 70.00
80.00 75.00 107.20 55.60
90.00 176.00 30.30 40.50
100.00 1027.45 45.70 66.10
120.00 75.00 107.20 55.60

580.00 2633.15 553.90 490.50

总计 4257.55
```

## 检查 `passwd` 文件

下一个示例读取 `passwd` 文件，列出没有密码的用户以及 ID 号重复的用户（`pwk` 工具执行了类似的检查）。

```
# $ cat /etc/passwd

bill:102:100:ext 123:home/bill:/bin/bash
roy:104:100:ext 475:home/roy:/bin/bash
tom:105:100:ext 476:home/tom:/bin/bash
ynn:166:100:ext 500:home/lynn:/bin/bash
mark:x127:107:ext 112:home/mark:/bin/bash
sales:x108:100:ext 102:m/market:/bin/bash
anne:x100:100:ext 355:home/anne:/bin/bash
tomi:x164:100:ext 357:home/tom:/bin/bash
ginny:x115:100:ext 109:home/ginny:/bin/bash
chuck:x116:100:ext 146:home/chuck:/bin/bash
eil:x164:100:ext 159:home/neil:/bin/bash
rmi:x118:100:ext 178:home/rmi:/bin/bash
vern:x119:100:ext 201:home/vern:/bin/bash
bob:x120:100:ext 227:home/bob:/bin/bash
Janet:x122:100:ext 229:home/janet:/bin/bash
maggie:x124:100:ext 244:home/maggie:/bin/bash
dave:x126:100:ext 427:home/dave:/bin/bash
mary:x129:100:ext 303:home/mary:/bin/bash
```

```
# $ cat passwd_check

gawk < /etc/passwd {

  uid[void] = ""

  # 告诉 gawk uid 是一个数组

  # 无模式表示处理所有记录

  # 初始化重复标志位

  dup = 0

}

split($0, field, ":")  # 以 ":" 分隔为字段

if ($field[2] == "")  # 检查密码字段是否为空

{

    if ($field[5] == "")  # 检查信息字段是否为空

    {

        print field[1] "没有密码。"

    }

    else

{

        print field[1] ("$field[5] ") 没有密码。"

    }

}

for (name in uid)  # 遍历数组

{

    if (uid[name] == $field[3])  # 检查 UID 是否重复使用

    {

        print field[1] " 与 " name " 相同"

        dup = 1 # 设置重复标志位

    }

}

if (!dup)  # 等于 if (dup == 0)

{

    uid[field[1]] = $field[3]

}

'
```

`passwd_check`
bill ( 123) 没有密码。
ton (ext 357) 没有密码。
Neil 与 ton 相同： UID = 164
dave 没有密码。
dave 与 sales 相同： UID = 108

## 交互式价格范围报告 `list_cars`

下一个示例展示了一个完整的交互式 脚本，它使用 `awk` 根据价格范围对 `cars` 文件生成报告：

```
$ cat list_cars

trap 'echo $0 >> /dev/null;exit 1' INT

echo -n "价格范围 (例如, 5000-7500):"

read lowrange
```

```
gawk < cars \

$5 >= lowrange && $5 <= lowrange {

  if ($1 ~ /ply/) $1 = "plymouth"

  if ($1 ~ /chev/) $1 = "chevrolet"

  printf "%-10s %2d %8.2f\n", $1, $2, $5

}

}' | sort -n +5 >> list_cars.

cat list_cars
```

| 品牌 | 型号 | 年份 | 里程 | 价格 |
|---|---|---|---|---|
| | | | | $0. |

# 可选：GNU `gawk` 高级功能

本节讨论了 GNU 开发人员在重写 `gawk` 时添加的一些高级功能。它涵盖了如何使用 `getline` 语句控制输入、如何使用协进程在 `gawk` 和后台运行程序之间交换信息，以及通过网络交换数据。

## `getline`：读取输入

`getline` 语句比其他输入方法让你对数据的读取有更多控制。当你将变量名作为参数传递 `getline` 时，它会将数据读入该变量。`gl` 程序的 `BEGIN` 块使用 `getline` 从标准输入读取一行：

```
$ cat gl
BEGIN {
  getline aa
  print aa
}
```

```
$ echo aaaa | gawk -f g1
aaaa
```

`alpha` 文件用于以下几个示例：

```
$ cat alpha
aaaaaaaa
bbbbbb
cccccc
```

即使 `g g1` 提供了多行输入，它也处理第一行：

```
$ awk -f g1 < alpha
aaaaaaaa
```

当 `getline` 没有参数时，它读入 `$0` 并修改字段变量 (`$1`, `$2`, ...)：

```
$ awk 'BEGIN {getline;print $1}' < alpha
aaaaaaaa
```

`g2` 程序在 `BEGIN` 块中使用 `while` 循环遍历标准输入行。`getline` 语句将每行读入 `holdme` 并输出 `holdme` 的每个值。

```
$ cat g2
BEGIN {
  while (getline holdme)
    print holdme
}
$ awk -f g2 < alpha
aaaaaaaaaa
bbbbbbb
cccccc
ddddddddd
```

`g3` 程序证明了当其主体（而不仅仅是 `BEGIN` 块）中有语句时，`gawk` 会将每行输入读入 `$0`。此程序输出记录数 (`NR`)，
