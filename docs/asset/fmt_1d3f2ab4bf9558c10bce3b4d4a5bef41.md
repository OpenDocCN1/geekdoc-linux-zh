
整个计算本可以使用发送给 `bc` 的单一长输入流来解决，因为该程序也支持变量。然而，仅靠 `bc` 命令本身并不足以在脚本内部操作中间值。此外，坦率地说，将方程拆分为多个中间方程⑧也有助于调试。例如，这里是将计算出的月还款额拆分为美元和美分并确保其以正确格式的货币值呈现的代码：

```
dollars="$(echo $M | cut -d . -f1)"
cents="$(echo $M | cut -d . -f2 | cut -c1-2)"
```

`cut` 命令在这里证明很有用⑨。这段代码的第二行抓取月还款值小数点后的部分，然后截断第二个字符之后的内容。如果你更愿意将该数字四舍五入到最接近的下一美分，只需在截断美分为两位数字之前向该值添加 `0.005` 即可。

还请注意，在⑨处，脚本库通过脚本中的 `. library.sh` 命令被整洁地包含在内，确保所有函数（就本脚本而言，第 1 章的 `nicenumber()` 函数）随后都可以供脚本访问。

## Running the Script

这个极简脚本期望三个参数：贷款金额、利率和贷款期限（以年为单位）。

## The Results

假设你一直在关注一辆新的 Tesla Model S，并且好奇如果你买这辆车每月还款会是多少。Model S 起价约为出厂价 $69,900，而最新的汽车贷款利率约为 4.75%。假设你目前的汽车价值约为 $25,000 并且你可以用该价格置换，那么你将为差额 $44,900 融资。如果你还没有改变主意，你想看看四年和五年汽车贷款的总还款额之间的差异——使用此脚本很容易，如 Listing 3-11 所示。

```
$ loancalc 44900 4.75 4
A 4-year loan at 4.75% interest with a principal amount of 44,900
results in a payment of $1028.93 each month for the duration of
the loan (48 payments).
$ loancalc 44900 4.75 5
A 5-year loan at 4.75% interest with a principal amount of 44,900
results in a payment of $842.18 each month for the duration of
the loan (60 payments).
```

Listing 3-11: Testing the `loancalc` shell script

如果你能负担得起四年贷款的较高还款额，汽车将更快还清，你的总还款额（月还款额乘以还款次数）将显著减少。要计算确切的节省额，我们可以使用第 82 页脚本 #23 中的交互式计算器，如下所示：

```
$ calc '(842.18 * 60) - (1028.93 * 48)'
1142.16
```

这似乎是一笔值得的节省：$1,142.16 可以买一台不错的笔记本电脑！

## Hacking the Script

如果用户没有提供任何参数，此脚本确实需要一种提示每个字段的方法。更实用的版本将允许用户指定四个参数中的任意三个（本金、利率、还款次数和月还款额），并自动求解第四个值。这样，如果你知道你只能负担每月 $500 的还款额，并且 6% 汽车贷款的最长期限为 5 年，你就可以确定你能借到的最大本金。你可以通过实现用户可用于传入所需值的标志来实现此计算。

## #26 Keeping Track of Events

这实际上是一对脚本，它们共同实现了一个简单的日历程序，类似于我们第 80 页脚本 #22 中的提醒实用程序。第一个脚本 `addagenda`（见 Listing 3-12）使你能够指定一个重复事件（每周事件使用星期几，或年度事件使用日和月）或一次性事件（使用日、月和年）。所有日期都经过验证，并连同一行事件描述一起保存在你主目录中的 `.agenda` 文件中。第二个脚本 `agenda`（见 Listing 3-13）检查所有已知事件以显示哪些事件安排在当前日期。

这种工具对于记住生日和纪念日特别有用。如果你记不住事件，这个方便的脚本可以为你节省很多麻烦！

## The Code

```
#!/bin/bash

# addagenda--Prompts the user to add a new event for the agenda script

agendafile="$HOME/.agenda"

isDayName()
{
# Return 0 if all is well, 1 on error.
```

```
case $(echo $1 | tr '[:upper:]' '[:lower:]') in
  sun*|mon*|tue*|wed*|thu*|fri*|sat* ) retval=0 ;;
  * ) retval=1 ;;
esac
return $retval
}

isMonthName()
{
  case $(echo $1 | tr '[:upper:]' '[:lower:]') in
    jan*|feb*|mar*|apr*|may*|jun*)  return 0    ;;
    jul*|aug*|sep*|oct*|nov*|dec*)  return 0    ;;
    * ) return 1    ;;
  esac
}

normalize()
{
  # Return string with first char uppercase, next two lowercase.
  /bin/echo -n $1 | cut -c1 | tr '[:lower:]' '[:upper:]'
  echo $1 | cut -c2-3 | tr '[:upper:]' '[:lower:]'
}

if [ ! -w $HOME ] ; then
  echo "So: cannot write in your home directory ($HOME)" >&2
  exit 1
fi

echo "Agenda: The Unix Reminder Service"
/bin/echo -n "Date of event (day mon, day month year, or dayname): "
read word1 word2 word3 junk

if isDayName $word1 ; then
  if [ ! -z "$word2" ] ; then
    echo "Bad dayname format: just specify the day name by itself." >&2
    exit 1
  fi
  date="$(normalize $word1)"
else
  if [ -z "$word2" ] ; then
    echo "Bad dayname format: unknown day name specified" >&2
    exit 1
  fi
  if [ ! -z "$(echo $word1|sed 's/[[::digit:]]//g')" ] ; then
    echo "Bad date format: please specify day first, by day number" >&2
    exit 1
  fi
  if [ "$word1" -lt 1 -o "$word1" -gt 31 ] ; then
    echo "Bad date format: day number can only be in range 1-31" >&2
    exit 1
  fi
```
