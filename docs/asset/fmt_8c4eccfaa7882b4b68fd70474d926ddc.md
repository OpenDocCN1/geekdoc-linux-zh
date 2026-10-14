
语法：`SEARCH(find_text; source_text; start_num)`

`SEARCH` 在另一个字符串 (`source_text`) 中查找指定的文本 (`find_text`)，与 `FIND` 不同，此函数不区分大小写；例如，

```
=SEARCH("Office"; "StarOffice")
```

返回 5，"Office" 的起始位置。

## `SUBSTITUTE`

语法：`SUBSTITUTE(source_text; substring; new_text; occurrence)`

这类似于 `REPLACE`，在这里你可以选择替换哪次文本；例如，

```
=SUBSTITUTE("StarOffice Is Cool!"; "Is"; "Way"; 2)
```

返回 "StarOffice Cool!"

# 条件函数

条件函数用于为你的工作表添加一些内置的“智能”。它们比较文本字符串，其结果（真或假）可以更改工作表的显示或计算方式。

## `EXACT`

语法：`EXACT(text_1; text_2)`

`EXACT` 比较两个字符串，如果它们完全相同则返回 1，否则不相同。例如

```
=EXACT("StarOffice"; "StarOffice")
```

返回 1，而

```
=EXACT("StarOffice"; "staroffice")
```

返回 0。

# 工具函数

工具函数用于各种格式化工作并返回有关文本字符串的有用信息。

## `CHAR`

语法：`CHAR(number)`

此函数根据代码 0到255 返回字符。这些代码符合标准 ASCII 表，但返回的字符取决于 StarOffice 的语言版本；例如，

```
=CHAR(64)
```

返回字符 "@"。

## `CODE`

语法：`CODE(text)`

此函数返回字符串中第一个字符的代码；例如，

```
=CODE("StarOffice")
```

返回 32。

## `LEFT`

语法：`LEFT(text; number_of_chars)`

`LEFT` 返回字符串 `text` 的第一个字符，或从左侧开始指定数量的字符 (`number_of_chars` 参数）；例如，

```
=LEFT("StarOffice")
```

返回 "S"，以及

```
=LEFT("StarOffice"; 4)
```

返回 "Star"。

另请参见 `MID` 和 `RIGHT`。

## `LEN` (字符串长度)

语法：`LEN(text)`

此函数返回给定字符串的长度；例如，

```
=LEN("StarOffice")
```

返回 10。

## `MID`

语法：`MID(text; start; number_of_chars)`

`MID` 返回字符串 (`text`) 的子字符串，从指定位置 (`start`) 开始并包含给定数量的字符 (`number_of_chars`)。例如，

```
=MID("StarOffice"; 2; 6)
```

返回 "tarOff"。

另请参见 `LEFT` 和 `RIGHT`。

## `REPT` (重复字符串)

语法：`REPT(text; repetitions)`

此函数创建一个由给定字符串 (`text`) 重复次数 (`repetitions`) 组成的字符串；例如，

```
=REPT("Star"; 4)
```

返回 "StarStarStarStar"。

## `RIGHT`

语法：`RIGHT(text; number_of_chars)`

`RIGHT` 返回字符串 `text` 的最后一个字符，或从右侧开始的指定数量的字符 (`number_of_chars`)，例如，

```
=RIGHT("StarOffice")
```

返回 "e"，并且

```
=RIGHT("StarOffice"; 6)
```

返回 "Office"。

另请参见 `LEFT` 和 `MID`。

## `ROT13` (凯撒密码，旋转 13 位)

语法：`ROT13(text)`

此函数使用简单算法加密文本，其中字母表中的每个字母旋转 13 位。再次对加密后的文本旋转 13 位即可返回原始字符串；例如，

```
=ROT13("StarOffice")
```

返回 "FgneBssvpr", 而

```
=ROT13("FgneBssvpr")
```

返回 "StarOffice".

> 此函数仅在您按照附录 A 中的说明安装插件包后才可用。

## `T`

语法：`T(value)`

`T` 函数返回函数参数引的文本；例如，

```
=T(A1)
```

返回 "StarOffice", 但

```
=T(A2)
```

返回 "" 因为 `A2` 不包含文本字符串。

此函数已过时，之所以存在仅是为了满足与旧电子表格软件的兼容性。

## `VALUE`

语法：`VALUE(text)`

此函数将文本字符串形式的数字转换为数值；例如，

```
=VALUE("$1,000,000")
```

返回 1000000。

# 日期函数

与许多人的认知不同，日期函数在业务中非常重要。没有它们，将很难判断计划中的业务投资盈利能力、抵押贷款的成本或投资的未来价值。许多财务函数受益于日期函数的使用，因为这使我们能够自动化许多计算，最终节省您的时间与金钱。

日期函数列在 `DateTime` 类别下，但我们在这里不讨论时间函数，因为它们与对应的日期函数非常相似，只是针对更短的时间段（日期毕竟是在所有更长时间的时间段之后）。

StarCalc 中的所有日期和时间计算都基于一个分数，称为序列号（`serial number`），它存储了自某个时刻以来已经过的秒数。该时刻被称为纪元（`epoch`）（请参见第 16 章侧边栏“StarCalc 与 2000 年问题”获取更多信息），可以由您设置（选择 `工具 > 选项`，并在电子表格分支下选择 `计算` 以显示一个对话框，您可以在其中选择三个纪元之一）。通常，您应该使用 `1899/12/30` 的标准纪元，但如果您想让计算与从其他电子表格导入的数据兼容，也可以选择其他。无论选择哪种纪元，计数都从午夜开始（`00:00:00`，或者如果您选择两位年份，则从 19xx 到 20xx-1，xx 可以在系统对话框中选择作为纪元）。这些设置允许 StarCalc 将指定范围内的两位年份解释为四位数；例如，`12/06/99` 被解释为 1999 年 12 月 12 日。在通过 `选项` 显示主选项对话框后，可以在常规分支下的项目对话框中进行设置。

- 当您选择纪元时，请在打开或创建工作表之前进行，以确保日期的一致性。

日期函数可分为以下组：

- 返回序列号的函数
- 根据序列号返回日期的函数
- 根据文本返回日期的函数
- 计算两个日期差值的函数

## 返回序列号的函数

日期和时间在 Linux 系统上以整数形式存储，称为序列号或序列日期。序列号是 Linux 系统创建者选择的某个时刻以来经过的秒数。与我们习惯日期或时间相比，在序列号上进行所有日期时间计算都要快得多。例如，求两个日期之间的差值只需相减两个序列号，而不是比较六个数字（年、月的日）。

### `DATE`

语法：`DATE(year; month; day)`

`DATE` 函数返回给定年、月、日的序列号；例如，将以下公式放入单元格中：

```
=DATE(2000; 01; 01)
```

### `DATEVALUE`

语法：`DATEVALUE(text)`

`DATEVALUE` 函数将日期字符串转换为序列号。

### `TODAY`

语法：`TODAY()`

`TODAY` 函数返回当前日期的序列号。

### `WEEKDAY`

语法：`WEEKDAY(serial_number; day)`

`WEEKDAY` 函数返回给定序列号的星期几。

### `WEEKNUM`

语法：`WEEKNUM(serial_number; day)`

`WEEKNUM` 函数返回给定日期的周数。

### `YEAR`

语法：`YEAR(serial_number)`

`YEAR` 函数从序列号返回年份。

### `MONTH`

语法：`MONTH(serial_number)`

`MONTH` 函数从序列号返回月份。

### `DAYSINMONTH`

语法：`DAYSINMONTH(serial_number)`

`DAYSINMONTH` 函数返回给定日期的月份数。

### `DAYSINYEAR`

语法：`DAYSINYEAR(serial_number)`

`DAYSINYEAR` 函数返回给定日期的天数。

### `WEEKSINYEAR`

语法：`WEEKSINYEAR(serial_number)`

此函数返回以序列号形式提供的日期所在年份的周数；例如，

```
=DAYSINYEAR(DATE(2000; 02; 16))
```

返回 52。

这些函数位于加载项（`Add-Ins`）包中，你需要按照附录 A 中的描述进行安装。

## 计算两个日期之间差值的函数

另一组实用的函数是计算两个日期之间差值的函数，这在财务计算中通常需要用于计算利息或折扣。

### `DAYS`

语法：`DAYS(serial_number_1; serial_number_2)`

此函数计算以日历年序列号形式提供的两个日期之间的天数；例如，
