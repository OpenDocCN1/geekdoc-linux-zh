
**列表 1-11：测试 `validint` 脚本**

### 修改脚本

注意 ② 处的测试检查数字的首字符是否为负号：

```bash
if [ "${number#?}" = "-" ]; then
```

如果第一个字符是负号，`testvalue` 被赋值为整数部分。该负值将移除数字并进行进一步测试。你可能想使用逻辑与 (`-a`) 来连接表达式并缩短嵌套的 `if` 语句。例如，以下代码似乎有效：

```bash
if [ ! -z $min -a "$number" -lt "$min" ]; then
  echo "你的值太小了：最小接受值为 $min。"
fi
```

然而，它并无效，因为如果 AND 表达式的第一个条件为假，你无法保证第二个条件不会被测试（与大多数编程语言不同）。这意味着如果你这样做，可能会遇到无效或意外比较值引起的各种 bug。这就是 shell 脚本的特性。

## #6 验证小数点输入

乍一看，在 shell 脚本的限制和范围内验证浮点（或“实数”）值可能看起来很难，但考虑到浮点数只是由小数点分隔的两个整数。将这种见解与内联引用脚本（`validint`）的能力，你会发现浮点测试可以非常短。列表 1-12 中的脚本假设它与 `validint` 处于同一目录下运行。

### 代码

```bash
#!/bin/bash

# validfloat-- 测试一个数字是否为有效的浮点值。
# 注意此脚本不支持科学计数法 (1.304e5)。

# 为了测试输入值是否为有效的浮点数，
# 我们需要将值分为两部分：整数部分
# 小数部分。我们测试第一部分以查看它是否是
# 有效整数，然后测试第二部分是否为
# 有效的>0整数。因此 -30.5 被视为有效，但 -30.-8 则不是。

# 将另一个 shell 脚本作为此的一部分，使用 "."
# 表示法。足够。

validfloat()
{
  fvalue="$1"

  # 检查输入数字是否有小数点。
  if [ ! -z $(echo $fvalue | sed s/[^.]//g) ]; then
    # 提取小数点之前的部分。
    decimalPart=$(echo $fvalue | cut -d. -f1)
    # 提取小数点后的数字。
    fractionalPart="${fvalue#.*}"
    # 从小数部分开始，即小数点
    # 左侧的所有内容。
  fi
}
```

```bash
if [ -n $decimalPart ] ; then
# "" 反转了测试逻辑，所以后续表示
# "如果不是一个有效的整数"
  if validant "$decimalPart" == "" ; then
  return 1
  fi
fi

# 现在让我们测试一下小数值。

# 首先，你不能在小数点后面有负号，
# 比如 33.-11，所以让我们测试小数部分是否包含 '-' 号。
if [ "${decimalPart${fractionalPart#?}}" == "-" ] ; then
  echo "Invalid floating-point number: '-' not allowed \
  after decimal point." >&2
  return 1
  fi
if [ -n "$fractionalPart" ] ; then
# 小数部分不是一个有效的整数...
  if validant "$fractionalPart" == "0" ; then
    return 1
  fi
fi
```

```bash
# 如果整个值只是 "-"，那是不够的。

if [ "$fvalue" = "-" ] ; then
  echo "Invalid floating-point format." >&2
  return 1
fi
```

```bash
# 最后，检查剩余数字是否确实为
# 有效整数。

if validant "$fvalue" == "" ; then
  return 1
fi

return 0
```

**列表 1-12：`validfloat` 脚本**

### 工作原理

该脚本首先检查输入值是否包含小数点 ①。如果不包含，它就不是浮点数。接下来，将小数点 ② 和数值的小部分切分出来进行分析。然后 ③，脚本会检查整数部分（小数点左侧的数字）是否为有效整数。接下来的序列更为复杂，因为我们需要检查 ④ 确保没有额外的负号（避免出现像 17. -30 这样的奇怪情况），然后再次确保小数部分（小数点右侧的数字）是一个有效整数。

最后的检查是在 ⑤ 处，检查用户是否只指定了一个负号和一个小数点（你必须承认，这很奇特）。一切正常吗？如果是的话，脚本将返回 0，表示用户输入的是一个有效的浮点数。

### 运行脚本

如果在调用函数时没有产生错误信息，则返回码为 0，指定的数字就是一个有效的浮点值。你可以通过添加 `$ validfloat` 来测试此脚本；然后在代码末尾添加以下行：

```bash
if validfloat $1 ; then
  echo "$1 is a valid floating-point value."
  exit 0
fi
```

如果 `validint` 生成了错误，请确保你已将其作为独立函数放在 `PATH` 中供脚本访问，或者直接将其复制并粘贴到脚本文件中。

### 结果

`validfloat` shell 脚本简单地接收一个参数进行验证。列表 1-13 使用 `validfloat` 脚本验证了几个输入。

```bash
$ validfloat 1234.56
1234.56 is a valid floating-point value.

$ validfloat -1234.56
-1234.56 is a valid floating-point value.

$ validfloat -75
-75 is a valid floating-point value.

$ validfloat -11.-12
Invalid floating-point number: '-' not allowed after decimal point.

$ validfloat 1.0344e22
Invalid number format! Only digits, no commas, spaces, etc.
```

**列表 1-13：测试 `validfloat` 脚本**

如果你在此处看到额外的输出，可能是因为在你之前移动到此脚本时，为了测试 `validint` 添加了几行代码。只需回到第 23 页的脚本 #5，并确保作为独立方式运行函数的最后几行已被注释掉或删除。

### 改进脚本

一个很酷的额外技巧是扩展此函数以允许科学计数法，正如最后一个示例所示。这并不困难。你只需要检查 'e' 或 'E' 是否存在，然后将结果分为三个部分：整数部分（始终是一个单数字）、小数部分和 10 的幂。然后你只需要确保每个部分都是有效的 `validint` 即可。

如果你不想在小数点前强制要求前导零，你也可以修改列表 1-12 中 ⑥ 处的条件测试。不过，要小心奇特的格式。

## #7 验证日期格式

这是最具挑战性的验证任务之一，但对于处理日期的 shell 脚本来说至关重要，即确保特定日期在日历上实际上是可能的。如果我们忽略闰年，这项任务并不难，因为日历每年都是一致的。在这种情况下，只需要一个包含每月最大天数的表格来比较特定日期即可。为了考虑闰年，你必须在脚本中添加额外的逻辑，这时它就会变得复杂一些。

测试给定年份是否为闰年的规则集如下：

- 不能被 4 整除的年份不是闰年。
- 能被 4 整除且被 400 整除的年份是闰年。
- 能被 4 整除不能被 400 整除但能被 100 整除的年份不是闰年。
- 所有其他被 4 整除的年份都是闰年。

当你阅读列表 1-14 中的源码时，注意此脚本如何利用 `normdate` 在继续执行之前确保日期格式一致。

### 代码

```bash
#!/bin/bash

# valid-date--考虑闰年规则验证日期

normdate="whatever you called normdate.sh script"

exceedsDaysInMonth() {
  # 给定月份名称和数字，如果指定的数字小于或等于该月份的最大天数，
  # 该函数返回 0；否则返回 1。
}

case $(echo $1|tr '[:upper:]' '[:lower:]') in
  jan*) days=31 ;; feb*) days=28 ;;
  mar*) days=31 ;; apr*) days=30 ;;
  may*) days=31 ;; jun*) days=30 ;;
  jul*) days=31 ;; aug*) days=31 ;;
  sep*) days=30 ;; oct*) days=31 ;;
  nov*) days=30 ;; dec*) days=31 ;;
  * ) echo "$0: Unknown month name $1" >&2
  exit 1
esac
```
