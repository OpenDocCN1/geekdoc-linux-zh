
返回时间值 `time` 的小时数值，范围从 0 到 23。

```
HOUR('12:31:58') → 12
HOUR(123158) → 12
```

### LAST_DAY(`date`)

返回参数所属月份最后一天的日期。`date` 应为日期或日期和时间值。

```
LAST_DAY('2003-07-01') → '2003-07-31'
LAST_DAY('2003-07-01 12:30:00') → '2003-07-31'
```

### LOCALTIME()

### LOCALTIMESTAMP()

这些函数是 `NOW()` 的同义词。括号是可选的。

### MAKEDATE(`year`, `day_of_year`)

给定年份和一年中的第几天，返回一个日期值。如果 `day_of_year` 小于 1，结果为 `NULL`。

```
MAKEDATE(2010, 365) → '2010-12-31'
MAKEDATE(2010, 367) → '2011-01-02'
MAKEDATE(2010, 0) → NULL
```

### MAKETIME(`hour`, `minute`, `second`)

返回由给定的小时、分钟和秒构建的时间值，如果参数超出范围则返回 `NULL`。分钟和秒值应在 0 到 59 的范围内。小时可以超出该范围。如果小时为负数，结果也为负数。

```
MAKETIME(0, 0, 0) → '00:00:00'
MAKETIME(12, 59, 59) → '12:59:59'
MAKETIME(12, 59, 60) → NULL
MAKETIME(-12, 59, 59) → '-12:59:59'
```

### MICROSECOND(`expr`)

返回给定时间或日期和时间值的微秒部分。返回值的范围为 0 到 999999。

```
MICROSECOND('00:00:00.000001') → 1
MICROSECOND('2004-06-30 23:59:59.5') → 500000
```

### MINUTE(`time`)

返回时间值 `time` 的分钟数值，范围从 0 到 59。

```
MINUTE('12:31:58') → 31
MINUTE(123158) → 31
```

### MONTH(`date`)

返回日期值 `date` 在一年中的月份数值，范围从 0 到 12（没有月份部分的非完整日期为 0）。

```
MONTH('2002-12-01') → 12
MONTH(20021201) → 12
MONTH('2002-00-01') → 0
```

### MONTHNAME(`date`)

返回包含日期值 `date` 月份名称的字符串，对于没有月份部分的非完整日期，返回 NULL。

```
MONTHNAME('2002-12-01') → 'December'
MONTHNAME(20021201) → 'December'
MONTHNAME('2002-00-01') → NULL
```

### NOW()

以 `CCYY-MM-DD hh:mm:ss` 格式返回连接时区中的当前日期和时间（作为 DATETIME 值）。

```
NOW() → '2008-05-01 18:36:09'
```

`NOW()` 返回其所在语句开始执行时的日期和时间，无论该语句执行多长时间。如果 `NOW()` 出现在存储过程或触发器中，则返回该过程或触发器开始执行时的时间。（请比较此行为与 `SYSDATE()` 的行为。）

### PERIOD_ADD(`period`, `n`)

将 `n` 个月加到期间值 `period` 上并返回结果。返回值的格式为 CCYYMM。期间参数的格式可以是 CCYYMM 或 YYYY（两者都不是日期值）。

```
PERIOD_ADD(201002, 12) → 201102
PERIOD_ADD(0802, -3) → 200711
```

### PERIOD_DIFF(`period1`, `period2`)

取两个期间值的差，并返回它们之间的月数。参数的格式可以是 CCYYMM 或 YYYY（两者都不是日期值）。

```
PERIOD_DIFF(200302, 200202) → 12
PERIOD_DIFF(200711, 0802) → -3
```

### QUARTER(`date`)

返回日期值 `date` 在一年中的季度数值，范围从 1 到 4。

```
QUARTER('2008-12-01') → 4
QUARTER('2009-01-01') → 1
```

### SECOND(`time`)

返回时间值 `time` 的秒数值，范围从 0 到 59。

```
SECOND('12:31:58') → 58
SECOND(123158) → 58
```

### SEC_TO_TIME(`seconds`)

给定秒数 `seconds`，以 ‘hh:mm:ss’ 格式返回对应的 `TIME` 值。

```
SEC_TO_TIME(29834) → ‘08:17:14’
```

### STR_TO_DATE(`str`, `format_str`)

使用格式化参数 `format_str` 解释字符串参数 `str`，并根据 `format_str` 中存在的格式化规范符返回 `TIME`、`DATE` 或 `DATETIME` 值。您可以使用此函数解释非 ISO 格式的时间值。`STR_TO_DATE()` 执行 `DATE_FORMAT()` 的逆操作，并且 `DATE_FORMAT()` 描述中列出的格式规范符对于 `STR_TO_DATE()` 也是合法的。如果 `str` 是非法的，或者无法使用给定的格式字符串进行解释，则结果为 `NULL`。

```
STR_TO_DATE('3/16/1960', '%m/%d/%Y') → 1960-03-16
STR_TO_DATE('12.20.32', '%H.%i.%s') → 12:20:32
STR_TO_DATE('3/16/1960 12:20:32', '%m/%d/%Y %H:%i:%s') → 1960-03-16 12:20:32
STR_TO_DATE('3/16/1960', '%m-%d-%Y') → NULL
```

### SUBDATE(`date`, INTERVAL `expr` `interval`)

### SUBDATE(`date`, `expr`)

对于第一种语法，`SUBDATE()` 接受一个日期或日期和时间值 `date`，从中减去一个时间间隔，并返回结果。这是 `DATE_SUB()` 的同义词。

```
SUBDATE('2009-12-01', INTERVAL 1 MONTH) → 2009-11-01
```

对于第二种语法，`SUBDATE()` 接受一个日期或日期和时间值 `date`，从中减去一个表示天数的时间值，并返回结果。这与 `ADDDATE()` 的相应语法类似。

```
SUBDATE('2009-12-01', 30) → 2009-11-01
```

### SUBTIME(`expr1`, `expr2`)

从第一个表达式中减去第二个表达式并返回结果。`expr1` 应为时间或日期和时间值，`expr2` 应为时间值。这些值可以包含微秒部分。

```
SUBTIME('06:30:00.5', '12:30:00.5') → ‘-06:00:00.000000’
SUBTIME('2009-01-01 00:00:00', '12:30:00') → ‘2008-12-31 11:30:00’
```

### SYSDATE()

返回连接时区中的当前日期和时间，作为 `CCYY-MM-DD hh:mm:ss` 格式的 DATETIME 值。此函数类似于 `NOW()`，不同之处在于，从 MySQL 5.0.13 开始，`SYSDATE()` 返回调用时的日期和时间，而 `NOW()` 返回其所在语句的开始执行时间。（更多详情请参见 `NOW()` 的说明。）要使 `SYSDATE()` 表现得像 `NOW()` 一样，请启动服务器时使用 `--sysdate-is-now` 选项（该选项从 5.0.20 版本起可用）。

### TIME(`expr`)

返回 `expr` 的时间部分，其中 `expr` 应为时间值或日期时间值。

- `TIME('16:15:00')` → '16:15:00'
- `TIME('2005-03-12 16:15:00')` → '16:15:00'

### TIME_FORMAT(`time`, `format`)

根据格式化字符串 `format` 对时间值 `time` 进行格式化，并返回生成的字符串。此函数也接受 DATETIME 或 TIMESTAMP 参数。格式化字符串类似于 `DATE_FORMAT()` 使用的字符串，但只允许使用与时间相关的说明符。其他说明符将导致结果为 NULL 值或 0。
