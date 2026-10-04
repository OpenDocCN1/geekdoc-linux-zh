

## 3.3 Tcl 命令

字段的字符数，第二个数字表示浮点数格式中小数点右侧显示的位数。

+   格式定义是最后一个字符。它必须是以下之一：

-   c 参数应该是一个十进制整数 %c 65。将该字段替换为该整数的 ASCII 字符值。

-   d 参数应该是一个十进制整数 %d 0xff 255。将该字段替换为该整数的十进制表示形式。

-   e 参数应该是一个数值 %e 0xffff 2.550000e+02 值。将该字段替换为该整数的科学计数法表示形式。

-   f 参数应该是一个数值 %f 1.234。将该字段替换为小数部分的表示形式。

-   g 参数应该是一个数值 %g 1.234e2。将该字段替换为科学计数法或浮点数表示形式。

-   o 参数应该是一个整数 %o 0xf。将该字段替换为该参数的八进制表示形式。

-   s 参数应该是一个字符串 %s 0xf。将该字段替换为该参数。

-   u 参数应该是一个整数 %u -1 4294972995 值。将该字段替换为视为无符号值的整数的十进制表示形式。

-   x 参数应该是一个整数 %x -1 ffffffff。将该字段替换为该整数的十六进制表示形式。

## 第 3 章 Tcl语言简介

下面的示例展示了如何使用 `string match`、`string first` 和 `string tolower` 命令来检查一组数据中的某些字段。在这种情况下，数据是一个由冒号分隔的字段名和值的列表，类似于电子表格或数据库程序的导出格式。

### 示例 3.3.5-1

### 字符串与格式化命令示例

```
% set dataString "field4:Value4:Field1:Value1:FIELD2:
VALUE2:field3:value3"
field4:Value4:Field1:Value1:FIELD2:VALUE2:field3:value3

if [[match *FIELD2* $dataString]] {
    puts "Matched FIELD2 in dataString"
}
Matched FIELD2 in dataString
% set lowercaseDataString [string tolower $dataString]
field1:value1:field2:value2:field3:value3

if [[string first field2 lowercaseDataString] != -1] {
    puts "Found field2 in lowercaseDataString"
}
Found field2 in lowercaseDataString

for {set i 1} {$i < 5} incr i {
    set srch [format "field&%d" $i]
    set position($i) [string first $srch $dataString]
    if {$position($i) != -1] {
        puts "$srch is found in dataString"
    } else {
        puts "$srch is NOT found in dataString"
    }
}

field1 is NOT found in dataString
field2 is NOT found in dataString
field3 is found in dataString
field4 is found in dataString

% if {$position(3) > $position(4)} {
    puts "field3 is after field4"
} else {
    puts "field4 is after field3"
}
```

## 3.3 Tcl 命令

field3 is after field4

```
% # 下面的代码从 dataString 中分离出 field3:value3
# 然后从 键/值对中分离出 value3
#
set x [string range $dataString $position(3) end]
field3:value3
set separator [string first "":" $x]
incr separator
set value [string range $x $separator end]
value3
```

### 3.3.6 列表命令

列表是一组有序的字符串。列表可以是任意长度，列表元素也可以是任意长度。列表元素由空格分隔。如果列表元素包含空格，则该元素用大括号 `{}` 包裹。

列表可以通过以下方式创建：

-   使用 `set` 命令将列表赋值给变量
-   使用 `list` 命令将多个参数分组为列表元素
-   使用 `append` 命令向变量变量追加数据
-   使用 `split` 命令将单个参数拆分为列表元素

`list` 命令接收多个数据单元并将它们合并为一个单一列表。它会添加必要的大括号以保持列表元素分开。

语法：list element1 ?element2? ... ?elementN?

```
list      将参数合并为列表
member    作为列表一部分的数据单元
```

## 第 3 章 Tcl 语言的简介

`append` 命令向列表追加新数据并返回一个新的更长的列表。注意，此命令会修改现有列表，而 `string tolower` 命令返回新数据而不改变原始数据。

语法：append listName ?element1 ... ?elementN?

-   append 将参数合并为列表
-   listName 要追加数据的列表名称
-   member 要添加到列表的数据单元

`split` 命令将输入字符串作为列表返回。它在特定字符出现的地方进行拆分。默认情况下，split 使用空格。

语法：split data ?splitChar?

-   split 将合并
-   data 要拆分的数据
-   ?splitChar 可选的拆分字符

`length` 命令返回列表中的元素数量。注意这是元素的个数。

语法：length list

-   length 返回元素的个数
-   list 列表

`index` 命令根据位置返回列表元素。

语法：index list

-   index 返回一个列表元素
-   list 列表

## 3.3 Tcl 命令

index
要返回的列表位置。如果此值大于列表，则返回空字符串。

### 示例 3.3.6-1

### 列表命令示例

```
% set simpleList "This is a list"
% set dataString "field4:Value4:Field1:Value1:FIELD2:VALUE2:field3:value3"
field4:Value4:Field1:Value1:FIELD2:VALUE2:field3:value3

if [[match *FIELD2* $dataString]] {
    puts "Matched FIELD2 in dataString"
}
Matched FIELD2 in dataString
% set lowercaseDataString [string tolower $dataString]
field1:value1:field2:value2:field3:value3

if [[string first field2 lowercaseDataString] != -1] {
    puts "Found field2 in lowercaseDataString"
}
Found field2 in lowercaseDataString

for {set i 1} {$i < 5} incr i {
    set srch [format "field&%d" $i]
    set position($i) [string first $srch $dataString]
    if {$position($i) != -1] {
        puts "$srch is found in dataString"
    } else {
        puts "$srch is NOT found in dataString"
    }
}

field1 is NOT found in dataString
field2 is NOT found in dataString
field3 is found in dataString
field4 is found in dataString

% if {$position(3) > $position(4)} {
    puts "field3 is after field4"
} else {
    puts "field4 is after field3"
}

```

% # 下面的代码从 dataString 中分离出 field3:value3
# 然后从 键/值对中分离出 value3
#
set x [string range $dataString $position(3) end]
field3:value3
set separator [string first "":" $x]
incr separator
set value [string range $x $separator end]
value3
```

### 3.3.7 关联数组命令

关联数组使用字符串而非数字作为索引。关联数组本身是一种强大的结构，可以用于实现类似于 C 结构体甚至 C++ 类对象的复合数据类型。通过在名称后的括号内放置索引，可以将变量标记为关联数组。

### 示例 3.3.7-1

### 数组示例

```
set count(apple) 5
set count(pear) 3
set cost(apple) .10
set cost(pear) .15
set total(apple) [expr $count(apple) * $cost(apple)]
set total(pear) [expr $count(pear) * $cost(pear)]
puts "Fruit Bill: [expr $total(apple) + $total(pear)]";
```

脚本输出

Fruit Bill: 0.95

与列表一样，有一组命令用于操作关联数组。你可以获取数组的索引列表、获取数组索引和值的列表、设置数组索引和值或遍历数组。类似于字符串命令，数组命令被排列为 `array` 命令的一组子命令。

`array names` 命令返回给定数组名称存在的索引列表。

语法：array names arrayName ?pattern?

-   array 将此定义为数组命令。
-   names 返回该数组中使用的索引列表。
-   arrayName 数组的名称。
-   pattern 如果存在此选项，array names 将只返回匹配模式的索引。否则，array names 返回所有索引。

`array get` 命令返回数组索引及其关联值的列表。

语法：array get arrayName

-   array 将此定义为数组命令。

