
```bash
#!/bin/bash

# validfloat--Tests whether a number is a valid floating-point value.
# Note that this script cannot accept scientific (1.304e5) notation.

# To test whether an entered value is a valid floating-point number,
# we need to split the value into two parts: the integer portion
# and the fractional portion. We test the first part to see whether
# it's a valid integer, and then we test whether the second part is a
# valid >=0 integer. So -30.5 evaluates as valid, but -30.-8 doesn't.

# To include another shell script as part of this one, use the "." source
# notation. Easy enough.

. validint

validfloat()
{
 fvalue="$1"

 # Check whether the input number has a decimal point.
 if [ ! -z $(echo $fvalue | sed 's/[^\.]//g') ]; then

 # Extract the part before the decimal point.
 decimalPart="$(echo $fvalue | cut -d . -f1)"

 # Extract the digits after the decimal point.
 fractionalPart="${fvalue#*.}"

 # Start by testing the decimal part, which is everything
 # to the left of the decimal point.
 if [ ! -z $decimalPart ] ; then
# "!" reverses test logic, so the following is
# "if NOT a valid integer"
if ! validint "$decimalPart" "" "" ; then
return 1
fi

# Now let's test the fractional value.
# To start, you can't have a negative sign after the decimal point
# like 33.-11, so let's test for the '-' sign in the decimal.
if [ "${fractionalPart%${fractionalPart#?}}" = "-" ] ; then
echo "Invalid floating-point number: '-' not allowed \
after decimal point." >&2
return 1
fi
if [ "$fractionalPart" != "" ] ; then
# If the fractional part is NOT a valid integer...
if ! validint "$fractionalPart" "0" "" ; then
return 1
fi
fi
else
# If the entire value is just "-", that's not good either.
if [ "$fvalue" = "-" ] ; then
echo "Invalid floating-point format." >&2
return 1
fi

# Finally, check that the remaining digits are actually
# valid as integers.
if ! validint "$fvalue" "" "" ; then
return 1
fi
fi

return 0
}
```

### 清单 1-12：`validfloat` 脚本

#### 工作原理

脚本首先检查输入值是否包含小数点 ①。如果没有，它就不是一个浮点数。接下来，值的十进制 ② 和分数 ③ 部分会被切出来进行分析。然后在 ④ 处，脚本检查十进制部分（小数点左侧的数字）是否是一个有效整数。下一个序列更复杂，因为我们需要在 ⑤ 处检查是否没有额外的负号（以避免像 `17.-30` 这样的奇怪情况），然后再次确保分数部分（小数点右侧的数字）是一个有效整数。

最后的检查，在 ⑨ 处，是用户是否只指定了一个减号和小数点（这会相当奇怪，你必须承认）。一切正常？那么脚本返回 `0`，表示用户输入了一个有效的浮点数。

#### 运行脚本

如果在调用函数时没有产生错误消息，则返回代码为 `0`，并且指定的数字是有效的浮点值。你可以通过将以下几行附加到代码末尾来测试此脚本：

```
if validfloat $1 ; then
 echo "$1 is a valid floating-point value."
fi

exit 0
```

如果 `validint` 产生错误，请确保你已将其作为脚本可访问的独立函数放在你的 `PATH` 中，或者直接将其复制并粘贴到脚本文件中。

#### 结果

`validfloat` shell 脚本只是接收一个参数来尝试验证。清单 1-13 使用 `validfloat` 脚本来验证一些输入。

```
$ validfloat 1234.56
1234.56 is a valid floating-point value.
$ validfloat -1234.56
-1234.56 is a valid floating-point value.
$ validfloat -.75
-.75 is a valid floating-point value.
$ validfloat -.12
Invalid floating-point number: '-' not allowed after decimal point.
$ validfloat 1.0344e22
Invalid number format! Only digits, no commas, spaces, etc.
```

清单 1-13：测试 `validfloat` 脚本

如果此时你看到额外的输出，可能是因为你在之前测试 `validint` 时添加了一些行，但在转到此脚本时忘记删除它们。只需返回第 23 页的脚本 #5，并确保用于将函数作为独立运行的最后几行已被注释掉或删除。

#### 脚本黑客

一个很酷的额外黑客是扩展此函数以允许科学计数法，如最后一个示例所示。这不会太困难。你需要测试是否存在 `'e'` 或 `'E'`，然后将结果拆分为三个
segments: 小数部分（始终为一位数字）、分数部分和 10 的幂。然后你只需要确保每个都是有效的 `int`。

如果不想要求小数点前必须有前导零，你也可以修改第 1-12 节清单中 ⑥ 处的条件测试。但请注意处理奇特的格式。

## 7 验证日期格式

最具挑战性的验证任务之一，但对于处理日期的 shell 脚本而言至关重要，就是确保特定日期在日历上确实存在。如果忽略闰年，这一任务并不太困难，因为日历每年都是一致的。在这种情况下，我们只需要一个表格，将每个月的最大天数与指定的日期进行比较即可。要考虑闰年，你必须在脚本中添加一些额外的逻辑，这时就会变得稍微复杂一些。

判断给定年份是否为闰年的一组规则如下：

- 不能被 4 整除的年份不是闰年。
- 能被 4 整除且能被 400 整除的年份是闰年。
- 能被 4 整除、不能被 400 整除但能被 100 整除的年份不是闰年。
- 所有其他能被 4 整除的年份都是闰年。

在阅读第 1-14 节清单中的源代码时，请注意该脚本如何利用 `normdate` 在继续之前确保日期格式一致。

## 代码
