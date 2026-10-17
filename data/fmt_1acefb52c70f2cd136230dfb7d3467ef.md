
# 这里是 `"$yesterday"` 的内容：Sun Feb 11 09:48:15 PST 2007

`'cut'` 命令能够为我们进行切片和处理。

```
# 254
# "yesterday" 包含 6 个字段；每个字段由空格分隔。（分隔符 "-d" 是一个“字段分隔符”）
```

`year=$(echo $yesterday | cut -d '-' -f6)` #第6个字段包含年份。
`month=$(echo $yesterday | cut -d '-' -f2)` #第2个字段包含月份。
`day=$(echo $yesterday | cut -d '-' -f3)` #第3个字段包含日期。

```
if [ "$month" == "Jan" ];
elif [ "$month" == "Feb" ];
then month_2_digits='02'
elif [ "$month" == "Mar" ];
then month_2_digits='03'
elif [ "$month" == "Apr" ];
then month_2_digits='04'
elif [ "$month" == "May" ];
then month_2_digits='05'
elif [ "$month" == "Jun" ];
then month_2_digits='06'
elif [ "$month" == "Jul" ];
then month_2_digits='07'
elif [ "$month" == "Aug" ];
then month_2_digits='08'
elif [ "$month" == "Sep" ];
then month_2_digits='09'
elif [ "$month" == "Oct" ];
then month_2_digits='10'
elif [ "$month" == "Nov" ];
then month_2_digits='11'
elif [ "$month" == "Dec" ];
then month_2_digits='12'
else print "错误：$month 包含错误值：$month 正在退出。\n"
fi
```

`yesterday_yyymymdd=$year$month_2_digits$day`
`print yesterday_yyymymdd=$year$month_2_digits$day`

# 函数 `get_yesterdays_date_SHORT_VERSION` 结束
###########################################

## `function get_yesterdays_date`

`# $MM` 是昨天的两位月份；`$DD` 是今天的两位数日期。
```
case $dd in
'01') # 如果今天是本月的 1 号，则确定昨天的 dd（日期）：
# 以下的 L-O-N-G 代码（跨 2 行）包含 11 个字符：
if [ "$MM" == "11" ] || [ "$MM" == "09" ] || [ "$MM" == "08" ] || [ "$MM" == "06" ] || [ "$MM" == "04" ] || [ "$MM" == "03" ] || [ "$MM" == "01" ]; then
then yesterday_dd=31
elif [ "$MM" == "12" ] || [ "$MM" == "10" ] || [ "$MM" == "07" ] || [ "$MM" == "05" ]; then
then yesterday_dd=30 # 如果昨天是 1 号，
elif [ "$leap_year_or_n" == 'y' ] && [ "$MM" == "03" ]; then
then yesterday_dd=29
elif [ "$leap_year_or_n" == 'n' ] && [ "$MM" == "03" ]; then
then yesterday_dd=28
fi

'02') yesterday_dd=01;
'03') yesterday_dd=02;
'04') yesterday_dd=03;
'05') yesterday_dd=04;

'06') yesterday_dd=05;
'07') yesterday_dd=06;
'08') yesterday_dd=07;
'09') yesterday_dd=08;
'10') yesterday_dd=09;
'11') yesterday_dd=10;
'12') yesterday_dd=11;
'13') yesterday_dd=12;
'14') yesterday_dd=13;
'15') yesterday_dd=14;
'16') yesterday_dd=15;
'17') yesterday_dd=16;
'18') yesterday_dd=17;
'19') yesterday_dd=18;
'20') yesterday_dd=19;
'21') yesterday_dd=20;
'22') yesterday_dd=21;
'23') yesterday_dd=22;
'24') yesterday_dd=23;
'25') yesterday_dd=24;
'26') yesterday_dd=25;
'27') yesterday_dd=26;
'28') yesterday_dd=27;
'29') yesterday_dd=28;
'30') yesterday_dd=29;
'31') yesterday_dd=30;
* ) print "错误：yesterday_dd 有无效值：$yesterday_dd"
exit 1;
} # get_yesterday_dd 结束
######################
esac
```

######################

## `function get_yesterday_date_LONG_VERSION`

# 开始执行 `get_yesterday_date_LONG_VERSION`：

`print "现在执行 get_yesterday_date_LONG_VERSION"`

`MM=$((m))` 当前月份（两位）

`DD=$((d))` 当前日期（两位）

`YYYY=$((y))` 当前年份（四位）

### 任务任务 #1：判断当前是否为闰年。

# （二月）在闰年有 29 天。

# 如果两位年份除以 4 的余数为 0，则是闰年。

# 示例 1：

# 如果年份是 2008，08 除以 4 余数为 0；（闰年）。

# 示例 2：如果年份是 2009，09 除以 4 余数为 1。

```
if [[ $((y % 4)) -eq 0 ]]; then '%' 是取模运算符
then y_or_n=y
else y_or_n=n
fi
```

### 任务 #2：确定昨天的两位日期：
`get_yesterday_dd = "执行命名函数 get_yesterday"`
# 变量 `"$yesterday_dd"` 现在包含一个两位数；
# 如果今天是26 号，`$yesterday_dd` 是 25。
# 如果今天是 4 号，`$yesterday_dd` 是 03（而不是 "3"）。

### 任务 #3：确定昨天的两位月份：
`yesterday_mm::`
# 如果今天是1 号，我们想要确定上个月是几月。
# `$MM` 是今天的两位月份。
# `$DD` 是今天的两位数日期。
```
if [[ "$MM" = "01" && "$DD" = "01" ]]; # 如果今天是 1 月 1 号，
then yesterday_mm="12";

elif "$DD" = "01" # 如果是本月的 1 号，那么
then (( yesterday_mm = MM - 1 )) # $MM 是当前月份
else yesterday_mm=$MM
fi
```

# 数学计算结果不会保留前导零；
# 如果月份是 03（三月），"month - 1" 的结果将是 2 而 02。
# 我们需要查看 `$yesterday_mm` 是 1 位数还是 2 位数
# 注意：# 有一个确定字符串长度的内置变量：`${#__}`
`LENGTH=${yesterday_mm}`
```
if [ $LENGTH -eq 1 ]; then
yesterday_mm=$yesterday_mm # 强制月份（mm）为两位。
fi
```

### 任务 #4：确定昨天的两位年份 YYY
```
if [ "$MM" = "01" ] && [ "$DD" = "01" ]; then (( yesterday_yyyy = yyy - 1 )) $YYYY 是当前四位年份。
else yesterday_yyyy=$yyyy
```

`yesterday_dd=$yesterday_dd`

# 函数 `get_yesterday_date` 结束

#####################

## `function process_yesterdays_files`
