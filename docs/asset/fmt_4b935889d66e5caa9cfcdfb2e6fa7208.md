
注意所有变量都在脚本顶部设置的。当你需要对变量进行微调时，这可以节省时间并避免错误。你所有的编辑都留在脚本顶部，而不是翻遍整个脚本。

```bash
$ pg whileread_file
!/bin/sh
# whileread_file
# initialise variables
SAVEDIFS=$IFS
IFS=$'\t'
HOLD_FILE=hold_file
NAME_MATCH="James Lenod"
INPUT_FILE=names.txt
```

```bash
# create a new HOLD_FILE each time, in case script is continuously running
>$HOLD_FILE
```

```bash
while read DEPT ID
do
# 使用重定向将所有信息写入临时文件
echo $NAME $DEPT ID >>$HOLD_FILE
# 匹配了吗？
if [ "$NAME" = "$NAME_MATCH" ]; then
    # 是的话则退出
    echo "包含 $NAME_MATCH 在内的之前所有条目都在 $HOLD_FILE 中"
    exit 0
fi
done < $INPUT_FILE
# 恢复 IFS
IFS=$SAVEDIFS
```

我们可以更进一步，列出属于每个部门的员工人数。我们保持相同的读取格式，将每个字段赋值给变量名。然后使用 `case` 语句并简单地使用 `expr` 来累加每个匹配项的值。如果发现未知部门，会将其输出到标准错误；如果发现无效部门，无需终止程序。

```bash
$ pg whileread_cond
#!/bin/sh
# whileread_cond
# 初始化变量
ACC_LOOP=0; CUS_LOOP=0; PAY_LOOP=0;
```

```bash
SAVEDIFS=$IFS
IFS=
while read NAME DEPT ID
do
    # 为每个匹配的部门计数器加1
    case $DEPT in
        ACC_LOOP=`expr $ACC_LOOP + 1`
            ACC="Accounts"
            ;;
        Customer) CUS_LOOP=`expr $CUS_LOOP + 1`
            CUS="Customer"
            ;;
        Payroll) PAY_LOOP=`expr $PAY_LOOP + 1`
            PAY="Payroll"
            ;;
        *) echo "`basename $0`: Unknown department $DEPT" >&2
            ;;
    esac
done < names.txt
IFS=$SAVEDIFS
echo "there are $ACC_LOOP employees assigned to $ACC dept"
echo "there are $C_LOOP employees assigned to $CUS dept"
echo "there are $PAY_LOOP employees assigned to $PAY dept"
```

## 278 控制流结构

运行脚本输出如下：

```
$ whileradcond
there are 2 employees assigned to Accounts dept
there are 1 employees assigned to Customer dept
there are 2 employees assigned to Payroll dept
```

### 18.7.6 累计总和

一个常见的任务是读取文件并对某些包含数字的列进行累计总和。下面的文件包含了 `STAT` 和 `GIFT` 部门销售的项目数量。

```
$ pg total txt
STAT 3444
GIFT 233
GIFT 252
GIFT 932
STAT 212
STAT 923
GIFT 129
```

我们的任务是为 `GIFT` 部门的所有项目提供总数。为了保持累计总和，我们使用 `expr`。查看下面的 `expr` 语句，变量 `LOOP` 和 `TOTAL` 在循环外部最初被赋值为零。随着脚本循环，`ITEMS` 被加上 `TOTAL`。循环的第一次迭代仅包含第一个项目，但随着过程继续，`ITEMS` 将被累加到 `TOTAL` 中。

下一个 `expr` 语句会增加计数器。

```bash
LOOP=0
TOTAL=0

while...
TOTAL=`expr TOTAL + ITEMS`
ITEMS=`expr ITEMS + 1`
done
```

使用 `expr` 时一个常见的错误是忘记先初始化变量。

```bash
LOOP=0
TOTAL=0
```

如果你忘记初始化，`expr` 错误就会出现在你的屏幕上。

如果你愿意，可以在循环内部初始化变量：

```bash
TOTAL=`expr ${TOTAL:-} + ${ITEMS}`
```

如果变量不包含值，上述操作将变量 `TOTAL` 赋值为零。你会发现第一个例子更常见。此外，记住在循环外部使用 `expr` 输出初始化变量以及最终的总和值。

这里是脚本。

```bash
$ pg total
#!/bin/sh
# total
# 初始化变量
LOOP=0
TOTAL=0
COUNT=0

echo "Items Dept"
echo ""
while read DEPT ITEMS
do
  # 记录总记录数
  COUNT=expr $COUNT + 1
  if [ "$DEPT" = "GIFT" ]; then
    # 保持累计总和
    TOTAL=expr $TOTAL + $ITEMS
    ITEMS=expr $ITEMS + 1
    echo -e "$ITEMS\t$DEPT"
  fi
  # echo $DEPT $ITEMS
done < total.txt
echo "===================="
echo "There were $COUNT entries altogether in the file"
```

当我们运行脚本时，得到：

```
$ total
Items Dept
234 GIFT
253 GIFT
933 GIFT
130 GIFT
==============
1546

There were 7 entries altogether in the file
```

### 18.7.7 一次读取一对记录

在某些情况下，你可能希望一次处理两条记录，也许是为了比较这两条记录中的不同字段。一次读取两条记录非常简单，在第一个 `while read` 之后，我们只需要在它后面跟一个 `do` 和另一个 `read` 即可。使用这种技术时，如果确实有偶数条记录需要读取将会有帮助，所以不要忘记检查这一点。

这是一个包含六条记录的文件，记录 1，记录 2 等。

```
$ pg record.txt
record 1
record 2
record 3
record 4
record 5
record 6
```

我们将一次读取两个记录，在本示例中没有对记录进行任何实际测试。

这里是完成此工作的脚本。

```bash
$ pg readpair
#!/bin/sh
# readpair
# 第一条记录
while read rec1
do
  # 第二条记录
  read rec2
  # 在此处进行进一步的处理/测试以测试或比较两条记录
  echo "This is record one of a pair :$rec1"
  echo "This is record two of a pair :$rec2"
  echo "--------------------------------"
done < record.txt
```

让我们先使用 `wc` 命令检查记录数是否为偶数。

```
$ cat record.txt | wc -l
6
```

由于我们有六条记录，所以让我们处理吧。

```bash
$ pgreadpair
This is record one of a pair :record 1
This is record two of a pair :record 2
```

```
This is record one of a pair :record 3
This is record two of a pair :record 4
```

```
This is record one of a pair :record 5
This is record two of a pair :record 6
```

### 18.7.8 忽略 # 字符

在读取文本文件时，你可能想要忽略或跳过你遇到的任何注释行。这是一个典型的例子。

假设你希望使用普通循环读取配置文件。你会读取每一行，这在大多数情况下都是你想要的。

然而，要忽略以特定字符开头的行，你需要使用 `case` 语句。由于 `#` 符号是一个特殊字符，最好先用反斜杠对其进行转义；然后我们在哈号后加上星号，以包含哈号后的任何字符。

这是一个典型的配置文件。

```
$ pg config
# (此处未提供具体配置内容，但根据上下文应为配置示例)
```
