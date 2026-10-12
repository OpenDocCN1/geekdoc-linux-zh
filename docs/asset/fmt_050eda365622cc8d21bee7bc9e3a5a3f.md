
`inputbox` 用于接收用户输入。在这个示例中，我们将用户的姓名作为输入。但我们将输入的名称存储在哪里呢？答案是通过 `dialog` 命令末尾的语句 `2>/tmp/input.$` 将输入重定向到文件，这意味着将屏幕输出发送到名为 `/tmp/input.$` 的文件中，随后可以通过以下方式检索输入的名称并存储到变量中：`na=cat /tmp/input.$`。输入框的退出状态参考下表：

| 输入退出状态 | 含义 |
|---|---|
| 0 | 命令执行成功 |
| 1 | 用户点击了取消按钮 |
| 255 | 用户点击了 `Escape` 键 |

### 使用 `dialog` 实用工具创建确认框 (`yesno`)
### 使用 `dialog` 实用工具的用户界面 - 整合演示
### 使用 `dialog` 实用工具创建消息框 (`msgbox`)
### 使用 `dialog` 实用工具创建输入框 (`inputbox`)

## 使用 `dialog` 实用工具创建输入框 (`inputbox`)

```bash
$ cat > dia4
dialog --title "输入框 - 接收你的输入" --backtitle "Linux Script Tutorial" --inputbox "请输入你的名字" 8 60 2>/tmp/input.\$

ssel=$?

na=$(cat /tmp/input.\$.
case $sel in
0) echo "Hello $na" ;;
1) echo "点击了取消" ;;
255) echo "按了 [ESCAPE] 键" ;;
esac

rm -f /tmp/input.\$
```

如下所示运行：

```bash
$ chmod +x dia4
$ ./dia4
```

![](img/219cb7c6e1c9c4c56d73838282f4b69b_101_0.png)

| 3 | `quit` |
| 9 | `kill` (无法被捕获) |

要在上面的脚本中捕捉信号，请在调用 `Take_input1` 函数之前放置 `trap` 语句：`trap del_file .. .`。当发生 2 号中断（即 `CTRL+C`）时，`trap` 命令会调用 `del_file()`。在编辑器中打开上述脚本并进行修改，使其结尾如下所示：

```bash
$ vi testsignal1
#
# 捕捉信号以删除临时文件，版本 2
del_file()
{
  echo "* * CTRL + C Trap Occurs (removing temporary file)* * *"
  rm -f /tmp/input0.*
  exit 1
}

Take_input1()
{
  recno=0
  clear
  echo "Appointment Note keeper Application for Linux"
  echo -n "Enter your database file name : "
  read filename
  if [ ! -f $filename ]; then
    echo "Sorry,$filename does not exit, Creating $filename database"
    echo "Appointment Note keeper Application database file" > $filename
  fi
  echo "Data entry start data: `date` >/tmp/input0.*"
#
# 设置无限循环
#
while :
do
  echo -n "Appointment Title:"
  read na
  echo -n "time :"
  read ti
  echo -n "Any Remark :"
  read remark
  echo -n "Is data okay (y/n) ?"
  read ans
  if [ $ans = y -o $ans = Y ]; then
    recno=`expr $recno + 1`
    echo "recno. $na ti $remark" >> /tmp/input0.*
  fi
  echo -n "Add next appointment (y/n)?"
  read isnext
  if [ $isnext = n -o $isnext = N ]; then
    cat /tmp/input0.* $filename
    rm -f /tmp/input0.*
    return # 终止循环
  fi
done # 结束循环
}
# 设置捕捉 CTRL+C 中断，即安装我们的错误处理器
# 当其发生时，它首先调用 del_file() 然后退出
trap del_file 2
#
#
# 调用我们的用户自定义函数：Take_input1
#
Take_input1
```

运行脚本如下：

```bash
$ ./test1
```

在输入数据库名称并在输入预约标题后按下 `CTRL+C`，在这里我们已经捕捉到了这个 `CTRL+C` 信号（中断），因此首先调用函数 `del_file()`，它会输出消息 "*** `CTRL` + `C` `Trap` `Occurs` `(removing` `temporary` `file)` ***"，然后删除我们的临时文件并以状态 1 退出。现在按照如下方式检查 `/tmp` 目录：

```bash
$ ls /tmp/*
```

`Shell` 将报告没有此类文件。

## `Linux` 脚本编写教程 (`LSST`)
第 4 章：高级脚本命令

## `shift` 命令

`shift` 命令将存储在位置参数（命令行参数）中的值向左移动一个位置。例如，如果当前位置参数的值为：`$1 = foo $2 = bar`，并且你执行了 `shift` 命令，则位置参数将变为：`$1 = bar $2 =`

例如，编写以下 `shell` 脚本来理清你的思路：

```bash
$ shift.sh

echo "command line args are: $1, $2, $3"

shift

echo "After shift command the args are: $1, $2, $3"

```

你也可以通过为 `shift` 命令指定一个数字来将位置参数移动超过一个位置。以下命令将位置参数移动两个位置：`shift 2`

### 但何时可以使用 `shift` 命令？

你可以使用 `shift` 命令来解析命令行（参数）选项。例如，考虑以下 `shell` 脚本：

```bash
$ convert

while [ "$1" != "" ]; then

do

    if [ "$1" = "-b" ]; then

        ob="$2"

        case $ob in

            16) basesystem="Hex";

            8) basesystem="Oct";

            2) basesystem="bin";

            *) basesystem="Unknown";

        esac

        shift 2

    elif [ "$1" = "-n" ]; then
```
