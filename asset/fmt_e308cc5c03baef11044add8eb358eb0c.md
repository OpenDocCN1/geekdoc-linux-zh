
## 代码片段

```bash
jan|feb|mar|apr|may|jun*) return 0;;
jul|aug|sep|oct|nov|dec*) return 0;;
*) return 1;
esac
}
```

```bash
normalize() {
  # 将输入转换为大写并保留前三位
  echo $1 | cut -c1-3 | tr '[:lower:]' '[:upper:]'
}
```

```bash
if [ ! -w "$HOME" ]; then
  echo "无法写入 $HOME" >&2
  exit 1
fi

echo "Agenda"
echo -n "日期 (月, 日, 年): "
read month day year

if [ -z "$month" ]; then
  echo "月份不能为空" >&2
  exit 1
fi

# 验证月份
if ! isMonthName "$month"; then
  echo "无效月份: $month" >&2
  exit 1
fi

# 验证日期
if [ "$day" -lt 1 ] || [ "$day" -gt 31 ]; then
  echo "日期必须在 1-31 之间" >&2
  exit 1
fi

# 验证年份
if [ -z "$year" ]; then
  echo "年份不能为空" >&2
  exit 1
fi

# 格式化并保存
date=$(date -d "$year-$month-$day" +%Y-%m-%d" 2>/dev/null)
if [ $? -ne 0 ]; then
  echo "无效日期: $month $day $year" >&2
  exit 1
fi

echo -n "事件描述: "
read description
echo "$date $description" >> "$agendafile"
echo "事件已添加。"
```

（以下是 `agenda` 脚本的对应部分）

```bash
# agenda--扫描 agenda 文件以显示今日安排的事件
agendafile="$HOME/.agenda"

if [ ! -f "$agendafile" ]; then
  echo "未找到 $agenda 文件。"
  exit 0
fi

# 获取今天的日期
eval $(date +'weekday=%U' month="%b" day="%e" year="%G")
day="$(echo $day|sed 's/ //g')"
echo "今日的日程："
while read -r date description; do
  if [ "$date" == "$day"* ]; then
    echo "- $description"
  fi
done < "$agendafile"
```

## 工作原理

`addagenda` 和 `agenda` 脚本支持三种周期性事件：每周事件（如每周三）、年度事件（每年 8 月 5 日）和一次性事件（2017 年 1 月 1 日）。在将项目添加到 `agenda` 文件时，指定的日期会被规范化并压缩，使得 `August` 变成 `Aug`，`Thursday` 变成 `Thu`。这是通过 `addagenda` 中的 `normalize` 函数实现的。

该函数将任何输入值截取为三个字符，并确保第一个字母大写，后两个字母小写。这种格式与命令输出的标准缩写日期和月份值匹配，这对于 `agenda` 脚本的正确运行至关重要。`addagenda` 脚本的其他部分没有特别复杂的逻辑；其大部分代码用于对数据格式进行错误测试。

最后，② 我们注意到错误检查代码与实际功能代码的比例是良好程序的典型：在输入时清理数据，这样你就可以放心地对后续格式做出假设。

`agenda` 脚本通过将当前日期转换为三种可能的日期字符串格式（日、日+月、日+月+年）来检查事件 ③。它将这些日期字符串与 `.agenda` 数据文件中的每一行进行比较。如果匹配，则显示该事件。

这对脚本中最酷的黑科技可能是使用一个 `eval` 将所需的四个日期值分别赋值给每个变量。

```bash
eval($date "weekday=\%a" month=\%b" day=\%e" year=\%g")
```

逐个提取值是可行的（例如 `weekday="$(date+)"`），但在极少数情况下，如果日期在四次 `date` 调用中间跨越到了新的一天，这种可能会可能会，因此简洁的单次调用更为理想。此外，这看起来就是很酷。

由于 `date` 返回的日期数字带有前导零或前导空格，而这两者都不是我们想要的，因此下一行代码在继续之前会从值中去除这两者（如果存在的话）。看一看它是如何运作的！

## 运行脚本

`addenda` 脚本会提示用户输入新事件的日期。然后，如果接受该日期格式，脚本会提示输入事件的单行描述。

配套的 `addenda` 脚本没有参数，调用时会生成一个当前日期安排的所有事件列表。

### 运行结果

为了查看这对脚本的工作原理，让我们如列表 3-14 所示，向数据库添加一些新事件。

```bash
$ addagenda
Agenda: The Unix Reminder Service
Date of event (day mon, month year, or dayname): 31 October
One-line description: Halloween

$ addagenda
Agenda: The Unix Reminder Service
Date of event (day mon, month year, or dayname): 30 March
One-line description: Pentultimate day of March

$ addagenda
Agenda: The Unix Reminder Service
Date of event (day mon, month year, or dayname): Sunday
One-line description: sleep late (hopefully)

$ addagenda
Agenda: The Unix Reminder Service
Date of event (day mon, month year, or dayname): march 30 17
Bad date format: please specify day first, by day number

$ addagenda
Agenda: The Unix Reminder Service
Date of event (day mon, month year, or dayname): 30 march 2017
One-line description: Check in with Steve about dinner
```

列表 3-14：测试 `addenda` 脚本并添加多个日程项目

现在 `agenda` 脚本提供了关于今天发生事情的快速方便的提醒，详见列表 3-15。

```bash
$ agenda
On the agenda for today:
Penultimate day of March
sleep late (hopefully)
Check in with Steve about additional dinner
```

列表 3-15：使用 `agenda` 脚本查看我们今天的日程项目

注意，它匹配了格式为时间、日+月以及日+月+年的条目。为了完整起见，列表 3-16 显示了相关的 `.agenda` 文件，包含一些额外的条目：

```text
$ cat /~/.agenda
14Feb|Valentine's Day
25Dec|Christmas
3Aug|Dave's birthday
4Jul|Independence Day (USA)
31Oct|Halloween
30Mar|Penultimate day of March
Sun|sleep late (hopefully)
30Mar2017|Check in with Steve about dinner
```
