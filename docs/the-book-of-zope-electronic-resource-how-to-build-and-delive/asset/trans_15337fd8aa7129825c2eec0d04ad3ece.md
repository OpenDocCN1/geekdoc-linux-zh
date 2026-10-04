

# DTML 与内置属性

## A.1 var 标签

下表列出了所有的 var 属性以及示例和相应的屏幕输出。标记有星号 (*) 的属性至少需要一个参数。这是表 4.1 中陈述信息的更完整版本。

### var 标签的属性

| 属性 | 功能 | 示例 | 输出 |
| --- | --- | --- | --- |
| name* | 参见表 4.1 中的“name 属性”。 | | |
| expr* | 参见表 4.1 中的“expr 属性”。 | | |
| fmt* | 参见表 4.1 中的“fmt 属性”。 | | |
| null | 定义一个字符串，输出时将使用该字符串而非 "null" 值。如果省略了 null 的值，则不插入任何文本。 | null="The result" returns an empty list. | The result returns an empty list. |

### var 标签的属性（续）

| 属性 | 功能 | 输出 |
| --- | --- | --- |
| missing | 如果由 name 引用的变量不在命名空间中，则定义一个要插入的字符串。如果省略了 missing 的值，则不插入任何文本。 | missing="Not found" | Not found |
| lower | 将所有字母转换为小写。 | title_id_lower | testpage |
| upper | 将所有字母转换为大写。 | title_id_upper | TESTPAGE |
| capitalize | 将首字母大写。 | AUTHENTICATED_USER capitalize | Manager |
| specify | 将下划线字符 [] 转换为空格。 | id specify (id="index_html") | index html |
| thousands_comma | 在仅由数字组成的字符串的千分位插入逗号。 | teststring thousands_comma (teststring="12000") | 12,000 |
| html_quote | 将 HTML 中有意义的字符替换为相应的 HTML 实体。 | teststring html_quote (teststring="<") | &lt; |
| url_quote | 对 URL 中不法的字符进行正确转义，以便插入 href 值中。 | teststring url_quote (teststring="<") | %3c |
| url_quote_plus | 功能类似于 url_quote，但为了插入 href URL 的 CGI 查询，将空格转换为加号 (+)。 | teststring url_quote_plus teststring="two words" | two+words |
| sql_quote | 对 SQL 有意义的字符（如单引号）进行正确转义（对于 SQL 方法非常重要）。 | Teststring sql_quote (teststring="How're you?") | How're you |

### var 标签的属性（续）

| 属性 | 功能 | 示例 | 输出 |
|---|---|---|--|
| newline_to_br | 在源代码中字符串值的每个新换行处插入 HTML 换行标签 <br>。 | teststring_newline_to_br (teststring="Hello\nYou") | Hello<br>You |
| size | 仅从字符串中显示指定数量的字符。 | teststring size=6 (teststring="How're you?") | Haw're... |
| else | 指定一个字符串，代替被省略的字符（与 size 使用）。 | teststring size=6 etc="--" (teststring="How're you?") | How're - |

## 标准 fmt 属性格式

| 名称 | 描述 |
|---|---|--|
| AMPM | 返回包含秒的时间。 |
| AMMinutes | 返回不包含秒的时间。 |
| aCommon | 以格式 Mar 1, 2002 1:45 pm 显示时间。 |
| aCommonZ | 以格式 Mar 1, 2002 1:45 pm US/Eastern 显示时间。 |
| aDay | 返回星期几的缩写名称。 |
| aMonth | 返回月份的名称。 |
| ampm | 返回后缀 am 或 pm。 |
| Date | 返回对象的日期字符串。 |
| Day | 返回星期几的全名称。 |
| DayOfWeek | 与 Day 相同：返回星期几的全名称。 |
| day | 返回数字格式的日子。 |
| dayOfYear | 返回对象所在时区的年份。 |
| dd | 返回两位数字格式的日子。 |
| fCommon | 以格式 March 1, 1997 1:45 pm 显示时间。 |
| fCommonZ | 以格式 March 1, 1997 1:45 pm US/Eastern 显示时间。 |
| h_12 | 返回 12 小时格式的时间。 |
| h_24 | 返回 24 小时格式的时间。 |

### 标准 fmt 格式（续）

| 名称 | 描述 |
| --- | --- |
| hour | 返回 24 小时格式的时间。 |
| isCurrentHour | 如果对象 Date/Time 与当前时区相同，则返回 True。 |
| isCurrentMonth | 如果对象 Date/Time 在当前月份，则返回 True。 |
| isFuture | 如果对象 Date/Time 处于未来，则返回 True。 |
| isLeapYear | 如果对象所在时区的年份是闰年，则返回 True。 |
| isPast | 如果对象 Date/Time 处于过去，则返回 True。 |
| Mon_ | 返回月份的全名称。 |
| Mon | 与 aMonth 相同：返回月份的缩写名称。 |
| Manth | 返回月份的全名称。 |
| minute | 返回两位数字格式的分钟。 |
| month | 返回数字格式的月份。 |
| natEqualTo(t) | 将 DateTime 对象与由 time 模块返回的数字对象进行比较。 |
| PreciseAMPM | 返回对象的格式化字符串。 |
| PreciseTime | 返回对象的格式化字符串。 |
| pCommon | 以格式 Mar 1, 2002 1:45 pm 显示时间。 |
| pCommonZ | 以格式 Mar 1, 2002 1:45 pm US/Eastern 显示时间。 |
| pDay | 返回缩写格式的日子。 |
| pMonth | 返回缩写格式的月份。 |
| rfc822 | 返回 RFC822 格式（用于 HTTP Header）。 |
| second | 返回秒。 |
| TimeMinutes | 返回不带秒的对象格式化字符串。 |
| Time | 返回带秒的对象格式化字符串。 |
| timezone | 返回对象显示的时区。 |
| year | 返回对象的公历年份。 |
| yy | 返回两位数字格式的公历年份。 |

## A.1.1 特殊格式 |这些特殊格式可以与其他数据类型的 fmt 属性一起。

| 特殊格式 | 描述 |
| --- | --- |
| whole-dollars | 显示带有美元符号的数值。 |
| dollars-and-cents | 显示带有美元符号和两位小数的数值。 |
| collection-length | 返回对象集合的长度。 |
| structured-text | 将值渲染为结构化文本，生成 HTML 数据。 |

### fmt 属性的 C 格式

| 代码 | 描述 | 示例 | 结果 |
| --- | --- | --- | --- |
| d | 带有符号号的整数 | fmt="%.3d" | -020 |
| e | 科学计数法 | fmt="%.3e" | -2.000E+001 |
| E | 科学计数法 | fmt="%.3E" | -2.000E+001 |
| f | 实 | fmt="%.3f" | -20.000 |
| g | e 或 f 的缩写 | fmt="%.3g" | -20 |
| G | E 或 F 的缩写 | fmt="%.3G" | -20 |
| i | 带有符号号的整数 | fmt="%.3i" | -020 |
| o | 不带符号号的八进制 | fmt="%.3o" | 3777777754 |
| s | 字符串 | fmt="%.2s" | -2 |
| u | 不带符号号的整数 | fmt="%.3u" | 4294967276 |
| x | 带有小写字母且不带符号的十六进制 | fmt="%.3x" | ffec |
| X | 带有大写字母且不带符号的十六进制 | fmt="%.3X" | FFFFFEC |

## A.2 命名空间变量

### 命名空间属性变量

| 属性 | 功能 | 示例 | 输出 |
|---|---|---|---|
| abs(number) | 计算数字的绝对值。 | _.abs(-3) | 3 |
| chr(number) | 返回与 ASCII 值关联的字符。 | _.chr(97) | a |
| divmod(number 1, number 2) | 计算两个数除法的整数商和余数。 | _.divmod(20, 3) _.divmod(12, 3) | (6, 2) (4, 0) |
| float(number) | 将值转换为浮点数。 | _.float(4) | 4.0 |
| getitem(name,call]) | 在命名空间（帧实例，[...]）中查找名称，但也接受一个可选参数，决定是否调用返回的对象。如果省略参数，则不调用对象，这与 [...] 的行为相反。 | _.getitem('some_name') | Content of some_name |
| hash(object) | 返回对象的哈希值。 | _.hash(index.html) | 504824376 |
| hex(number) | 将数字转换为十六进制。 | _.hex(5) _.hex(8) | 0x5 0x10 |
| int(number) | 将转换为整数。小数部分截断，不进行四舍五入。 | _.int(4.25) _.int('4.85') | 4 4 |
| len(seq) | 计算序列中元素的个数。 | _.len('Hello') _.len(['I', 'You']) | 5 2 |

