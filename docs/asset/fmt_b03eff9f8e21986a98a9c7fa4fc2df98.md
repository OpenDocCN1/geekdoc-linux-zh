
我们将使用 `rm` 删除该目录
完成：`./mkdir.ksh`

### 程序：`money.ksh`
`#!/bin/ksh`
# 程序：`money.ksh`
# 目的：
# 1. 读取包含金额的文件，然后显示总计。
# 2. 打印包含金额的变量。
# 3. `math.ksh` 显示如何进行金额计算。
# 注意：`money.ksh` 也显示如何进行金额计算。
# 程序员：Larry Smith。修订于 `__date__`
# 难度：中等
# 用法：`./money.ksh`
# 注意：
# 我们知道计算器擅长处理。
# `shell` 和 `bash` 在处理
包含小数点的数字（如 `$5.95`）方面都很糟糕，
# 除非使用 `bc` 帮助。
# `bc` ("基础计算器") 处理金额的
语法是显而易见的。
# 使用 `bc` 时：
# `0` 是假的。`1` 是真的。
# `scale` 指小数点后的位数。
# `2.91` 的 `scale` 为 2；`12` 的 `scale` 为 3。
# 示例：
# `result=$(echo "scale=2; $15 - $22" | bc)`
`print "$15 减 $22 是 $result"`
# 遗憾，`bc` 不是“强大的计算器。”
# 除非你使用高级版本的 `bc`，
# 它不会四舍五入；而是直接截断。（参见 `math.ksh`）。
# 在双括号内进行数学比较时，
# 不需要在变量名前使用美元符号。
# 以下语句在大多数操作系统上正常工作：
# `if (( record_counter > 100 ));`
# `if (( record_counter > 100 ));`
# 然而，在某些系统中，变量上使用美元符号
会导致难以发现的错误。

# 参见：`calculate_percentage.ksh`

### 参见：`math.ksh`
### 注意结束。
`clear` # 清空用户屏幕。

#### 初始化：
`today=$(date +%b%d)`

`INPUT=/home/library/ROSETTA/INPUT_FILES/$today`

`quantity=0`

`SUBTOTAL_quantity=0`

`unit_price=0`

`SUBTOTAL_purchase_price=0`

`DEFAULT_IFS=" "` # 保存默认字段分隔符（空格）。

## 初始化结束。

```
print "# 注释：这是脚本 0。\n"
```

```
print "目的："
```

```
print "1：读取包含金额的文件，然后显示总计。"
```

```
print "2：打印包含金额的变量。"
```

```
print "3 math.ksh 显示如何进行金额计算。"
```

```
# 首先，创建一个包含销售交易的小型输入文件。
```

```
# 字段 #1：客户购买物品描述。
```

```
# 字段 #2：数量（购买了多少）。
```

```
# 字段 #3：单价（物品的价格）。
```

```
# 字段 #4：金额（数量乘以单价）。
```

```
# 字段由冒号 (:) 分隔。
```

```
print "milk:2:38:7.96" >>INPUT
```

```
print "bread:1:39.59:3.57" >>INPUT
```

```
print "chocolate:4:2.98:11.92" >>INPUT
```

```
# 验证 INPUT 文件是否存在
if [ ! -f "$INPUT" ] && [ -s "$INPUT" ]; then
  则；什么都不做；继续
else
  print "# 错误：INPUT 不存在、为空或无法读取。"
  exit
fi
```

```
IFS=':' # 字段由冒号分隔。IFS 是内部字段分隔符。
```

```
#######################
## 开始循环。
while read -r description quantity unit_price purchase_price
do
  ((SUBTOTAL_quantity += quantity))
  # L-O-N 组（跨行）包含 91 个字符：
  SUBTOTAL_purchase_price=$(printf "scale=2;%s" $purchase_price + SUBTOTAL_p
done <$INPUT
# 结束结束。
```

```
print "#######"
```

```
print "我们刚刚读取了一个包含今天销售交易的文件，"
```

```
print "来自 Mom and Pop's Corner Grocery Store。"
```

```
print "嗯。看起来今天是个淡的日子！"
```

```
print "今天是 $(date +"%b %d")"
```

```
print "今天购买的物品总数：$SUBTOTAL_quantity"
```

```
print "今天的总销售额：${{SUBTOTAL_purchase_price}"
```

```
print "\n\n######"
```

```
print "最后，让我们展示如何打印包含金额的变量。"
```

```
print "让我们假设我欠 Ravi 33.34 美元。"
amount_owed=33.3333
```

```
print "如果我直接使用 printf 打印这个金额，它看起来是这样的："
print("amount owed: ${amount_owed}")
print("使用 printf 和 %d (整数) 打印是一个糟糕的主意：")
print("amount owed: $%d", $amount_owed 2>/dev/null)
print("现在让我们使用 printf 和 %.2f (浮点数) 正确地打印该金额：")
print("%.2f 意味着两位小数的精度。")
print("amount owed: $%.2f\n", $amount_owed)
```

```
# 恢复系统默认。（不是必须，但这样做很好！）
IFS="$OLDIFS. Script: $0\n"
```

```
# 输出:money.ksh,OUTPUT
```

脚本是如何执行的: `./money.ksh`
OUTPUT 随后的内容：

注释：这是脚本 `./money.ksh`。

- 目的：
1. 显示如何读取包含货币金额的文件，然后显示总计。
2. 显示如何打印包含货币金额的变量。
(`math.ksh` 也展示了如何进行涉及货币金额的计算。)

######

我们刚刚读取了一个包含来自 Mom and Pop's Corner Grocery Store 今日销售交易记录的文件。
嗯，看起来是淡的一天！

今天是 3 月 18 日
购买的物品总数：7
今日总销售额：$23.45

######

最后，让我们展示如何打印包含货币金额的变量。
让我们假设我欠 Ravi 33.33 美元。
如果我们不使用 printf 打印该金额，它看起来是这样的：
欠金额: $33.333333。

使用 printf 和 %d (整数) 打印是一个糟糕的主意：
欠金额: $33

现在让我们使用 printf 和 %.2f (浮点数) 正确地打印该金额：
（"%.2f" 意味着两位小数的精度。）
欠金额: $33.33

完成。`./money.ksh`

文件: `move.ksh`
目的：指向脚本 "`rename.ksh`".

文件: `mv.ksh`
目的：指向脚本 "`rename.ksh`".

### 程序: `nested_if.ksh`
`#!/bin/ksh`
# 程序: `nested_if.ksh`
# 目的：显示如何设置嵌套 if 语句。
# 程序员: Larry Smith. 由 `__date__` 修订
# 难度级别：中等
# 用法示例：`./nested_if.ksh`
### 注意：

# 让我们仔细观察一下这行代码
# 以防你不理解所有的细节。

```
# if [ $(ps -ef | grep -v grep) -eq 0 ]; then
```

# 以下操作具有相同的功能（使用反引号）：

```
# if [ `ps -ef | grep -v grep` -eq 0 ]; then
```

# `ps` 命令列出了服务器上运行的所有进程：

# 我们正在寻找一个名为 'applicationZZ' 的应用程序，这就是我们 grep 查找的；

# `-c` grep 选项允许我们统计包含 'applicationZZ' 的行数。

# 从命令行执行以下命令：

```
# ps -ef grep applicationZZ
```

# 在这里我发现的是：

# 但请注意进程 applicationZZ 本身就是 grep

# 换句话说，applicationZZ 目前没有在这台服务器上运行。

# 现在尝试此命令：grep -c --grep applicationZZ

# 我们看到的计数是 '1'；当 applicationZZ 实际上在服务器上运行时，

# 我们看到的计数是 2（1 是因为 grep，第二个是因为 applicationZZ 处于激活状态）。

# 我们通过使用 grep 的 -v 选项也解决了这个困惑：

# grep -c -v grep - 统计包含 'applicationZZ' 的行数

# 以忽略 (-v) 任何包含 'grep' 的行。

# 因此，这一行被忽略了：14:06/00 00:00:00 grep applicationZZ

# 当 applicationZZ 激活时，我期望看到计数为 1。
