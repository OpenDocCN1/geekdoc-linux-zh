

## 脚本改造

这种“删掉有效字符，看看剩下什么”的方法很不错，因为它很灵活，尤其是当你记得把输入变量和匹配模式（或者根本不写匹配模式）都用双引号包裹起来，以避免空输入错误时。空模式是脚本编程中经常遇到的问题，因为它们会把有效的条件测试变成一条出错的语句，并产生错误信息。始终牢记：一个零字符的带引号短语与一个空白短语是不同的。想要要求只能使用大写字母，但也允许空格、逗号和句点吗？只需把①处的替换模式改成下面所示的代码：

```
sed 's/[^\[:upper:] ,.]//g'
```

你也可以使用下面这样的简单测试来验证电话号码输入（允许整数值、空格、括号和短划线，但不允许前导空格或连续多个空格）：

```
sed 's/[^ -[:digit:]\(\)]/g'
```

但如果你想把输入限制为整数，就必须当心一个陷阱。举个例子，你可能会忍不住尝试这样写：

```
sed 's/[^[:digit:]]//g'
```

这段代码对正数是有效的，但如果你想允许输入负数呢？如果只是把负号加到有效字符集中，那么 `-3-4` 也会被视为有效输入，尽管它显然不是合法的整数。第25页的脚本#5讨论了如何处理负数。

## #3 规范化日期格式

shell 脚本开发面临的一个问题是数据格式繁多且不一致；将这些格式规范化可能从稍显棘手到相当困难不等。日期格式是最难处理的格式之一，因为日期可以用很多不同的方式来指定。即使你提示用户使用特定格式，例如月-日-年，也很可能收到不一致的输入：可能是月份数字而不是月份名称，可能是月份名称的缩写，甚至可能是全大写字母的完整月份名称。因此，一个规范化日期的函数虽然本身很基础，但对后续的脚本编写工作，尤其是第29页上的脚本#7，会被证明是一个非常有用的构建模块。

## 代码

清单1-5中的脚本会将满足一组相对简单条件的日期格式规范化：月份必须以名称或1到12之间的数字给出，年份必须以四位数字给出。

规范化后的日期由月份名称（三字母缩写）、日和四位年份依次组成。

```
#!/bin/bash
# normdate--Normalizes month field in date specification to three letters,
# first letter capitalized. A helper function for Script #7, valid-date.
# Exits with 0 if no error.

monthNumToName()
{
  # Sets the 'month' variable to the appropriate value.
  case $1 in
    1 ) month="Jan"  ;;  2 ) month="Feb"  ;;
    3 ) month="Mar"  ;;  4 ) month="Apr"  ;;
    5 ) month="May"  ;;  6 ) month="Jun"  ;;
    7 ) month="Jul"  ;;  8 ) month="Aug"  ;;
    9 ) month="Sep"  ;; 10 ) month="Oct"  ;;
   11 ) month="Nov"  ;; 12 ) month="Dec"  ;;
    * ) echo "$0: Unknown month value $1" >&2
        exit 1
  esac
  return 0
}

# BEGIN MAIN SCRIPT--DELETE OR COMMENT OUT EVERYTHING BELOW THIS LINE IF
# YOU WANT TO INCLUDE THIS IN OTHER SCRIPTS.
# ====================
# Input validation
if [ $# -ne 3 ] ; then
  echo "Usage: $0 month day year" >&2
  echo "Formats are August 3 1962 and 8 3 1962" >&2
  exit 1
fi
if [ $3 -le 99 ] ; then
  echo "$0: expected 4-digit year value." >&2
  exit 1
fi

# Is the month input format a number?
if [ -z $(echo $1 | sed 's/[^[:digit:]]//g') ] ; then
  monthNumToName $1
else
  # Normalize to first 3 letters, first upper- and then lowercase.
  month="$(echo $1 | cut -c1 | tr '[:lower:]' '[:upper:]')"
  month="$month$(echo $1 | cut -c2-3 | tr '[:upper:]' '[:lower:]')"
fi

echo $month $2 $3

exit 0
```

清单 1-5：normdate shell 脚本

## 工作原理

注意脚本中①处的第三个条件判断。它会剥离第一个输入字段中的所有数字，然后用 -z 测试判断结果是否为空。如果结果为空，就说明输入只包含数字，因此我们可以直接用 `monthNumToName` 将其映射为月份名称，该函数同时也会验证这个数字是否代表一个有效的月份。否则，我们假设第一个输入是月份字符串，并通过两次子shell调用（即由 `$(` 和 `)` 包围的序列，其中被包围的命令会被执行，并用其输出替换）配合一系列复杂的 `cut` 和 `tr` 管道来规范化它。

第二个子shell序列（②处）提取输入的第一个字符，并用 `tr` 将其转为大写（虽然序列 `echo $1 | cut -c1` 也可以用 POSIX 风格写成 `${1:0:1}`，如前所述）。第二个子shell序列（③处）提取第2和第3个字符，并强制将其转为小写，从而得到首字母大写的三字母月份缩写。请注意，与传入月份数字的情况不同，这种字符串处理方法不会检查输入实际上是否为有效月份。

## 运行脚本

为了确保未来的脚本整合 `normdate` 功能时具有最大的灵活性，本脚本被设计为接受命令行中输入的三段字段，如清单1-6所示。如果你只想在交互方式下使用这个脚本，可以让脚本提示用户输入这三个字段，但这会使得从其他脚本中调用 `normdate` 更加困难。

## 运行结果

```
$ normdate 8 3 62
normdate: expected 4-digit year value.
$ normdate 8 3 1962
Aug 3 1962
$ normdate AUGUST 03 1962
Aug 03 1962
```

清单 1-6：测试 normdate 脚本

注意，这个脚本只规范化月份的表示方式；日格式（例如带前导零的日格式）和年份保持不变。

## 脚本改造

