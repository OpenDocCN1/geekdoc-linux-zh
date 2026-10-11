
仪表是一个显示百分比进度的温度计条形图。新的百分比值会逐个从标准输入读取，直到到达文件末尾为止。`~gauge` 开关需要提供一个文本消息、高度、宽度以及一个可选的起始百分比（参见列表 13.2）。百分比可以通过命名管道发送给仪表，这将在第 11 章“文本文件基础”中讨论。

假设你希望显示一个显示打印发票系列文件进度的温度计图形，这些发票文件存储在一个名为 `invoices` 的目录中。下面的演示在发票被发送给另一个名为 `print_invoice` 的脚本时显示发票。

## 列表 13.2 `gauge_demo.sh`

```bash
#!/bin/bash
#
# gauge_demo.sh: a thermometer graph demo

shopt -s -o nounset

declare -rx SCRIPT=$0
declare -rx QUEUE=/status_fifo
declare -rx INVOICES_DIR="invoices"
declare -ix TOTAL_INVOICES=0
declare -ix NUM_INVOICES=0
declare -ix PERCENT=0

# count the invoices waiting to print
TOTAL_INVOICES=$(ls -1 $INVOICES_DIR | wc -l)

# create the pipe
mkfifo $QUEUE
if [ $? -ne 0 ] ; then
    printf "%s\n" "$SCRIPT:$LINENO: unable to create $QUEUE" >&2
    exit 192
fi

# print the invoices in a background subshell
# print the progress to the pipe
(
    cd $INVOICES_DIR
    ls -1 | (
        while read INVOICE ; do
            let "NUM_INVOICES++"
            print_invoice "$INVOICE"
            PERCENT=100*$NUM_INVOICES/$TOTAL_INVOICES
            printf "%d\n" "$PERCENT"
        done
    )
) > $QUEUE &

# display the progress.  dialog will stop when nothing
# more is printed by the subshell
dialog --gauges "Printing invoices" 7 70 0 < $QUEUE

wait          # wait for the subshell to finish
rm $QUEUE     # delete the pipe
sleep 1       # make sure results can be read by user

exit 0
```

*信息框* 是向用户显示的状态消息。它没有按钮，并且 `dialog` 命令立即完成。`--infobox` 开关需要一个文本消息，以及高度和宽度。

```bash
$ dialog --infobox "Connecting to server" 7 70
```

*输入框* 允许用户键入响应。`--inputbox` 开关需要提示文本、高度、宽度以及一个可选的用户默认响应。

```bash
$ dialog --print-size --inputbox "Connect to which host?" 7 70 0  2> size.txt
$ cat size.txt
Size: 7, 70
$ rm size.txt
$ dialog --print-size --no-shadow --nocancel --inputbox \
    "Connect to which host?" 7 70
```

剩余的对话框与前面讨论的类似。

-   *菜单* 是一个用户可以选择选项的列表。`--menu` 开关需要菜单标题文本、高度、宽度和菜单高度。每个项目都由一个标签名和菜单项文本指定。
-   *消息框* 向用户显示一条消息，带有一个单一的**确定**按钮。`--msgbox` 开关需要一个文本消息，以及高度和宽度。
-   *密码框* 类似于输入框，但用户输入的内容不会显示。`--passwordbox` 需要一个文本消息、高度和宽度，以及一个可选的默认密码。
-   *单选列表* 显示一个选项列表，用户只能选择其中一项。`--radiolist` 开关需要标题文本、高度、宽度和列表高度。每个项目的指定方式与复选列表相同。
-   *尾部框* 显示文件中的最后文本，仿佛使用了 `tail -f` 命令。`--tailbox` 开关需要文件名，以及高度和宽度。
-   *文本框* 在对话框中显示文本文件的内容。用户可以浏览该文件。`--textbox` 开关需要文件名、高度和宽度。
-   *背景文本框* 是尾部框和文本框的组合。文本显示效果仿佛使用了 “tail -f” 命令，但用户也可以自由浏览内容。`--textboxbg` 开关需要一个文件名、高度和宽度。
-   *时间框* 允许用户选择时间。`--timebox` 开关需要提示文本、高度、宽度，以及以小时、分钟和秒为单位的初始时间。
-   *日历框*，如图 13.3 所示，显示一个日历并允许用户选择日期。`--calendar` 开关需要提示文本、高度、宽度，以及起始的日、月和年。

![](img/7da864b222941ec315ee1c456ff472dd_264_0.png)

图 13.3 日历对话框。

您可以使用 `--and-widget` 开关组合连续的对话框。

```bash
$ dialog -inputbox "Connect to which host?" 7 70 "" -and-widget -inputbox \
"And what TCP/IP port?" 7 70
```

您必须为输入框提供初始字符串参数（如果没有则使用 `""`），否则 *dialog* 会认为 `-and-widget` 是可选字符串。

有许多用于自定义框的外观和行为的开关。这些列在本章的参考部分中。

## 参考部分

### showkey 命令开关

-   -scancodes（或 -s）— 扫描码转储模式
-   -keycodes（或 -k）— 键码转储模式（默认）
-   -ascii（或 -a）— ASCII 转储模式

### setleds 命令开关

-   -caps—清除大写锁定
-   +caps—设置大写锁定
-   -D—更改控制台标志和 LED
-   -F—更改控制台标志（默认）
-   -L—更改 LED
-   -num—清除数字锁定
-   +num—设置数字锁定
-   -scroll—清除滚动锁定
-   +scroll—设置滚动锁定

### dumpkeys 命令开关

-   -charset=c（或 -c C）—根据字符集 c 解释字符代码值
-   -compose-only—仅显示组合键组合
-   -full-table（或 -f）—以规范形式显示按键绑定
-   -funcs-only—显示功能键字符串定义
-   -keys-only—显示按键绑定，不带字符串定义
-   -long-info（或 -1）—打印有关键盘驱动器的详细信息
-   -numeric（或 -n）—以十六进制格式显示值
-   -short-info（或 -i）—打印有关键盘驱动器的摘要信息

### setterm 命令开关

-   -append [ c ]—将控制台屏幕（默认为当前）转储到文件，如果文件存在则追加
-   -appcursorkeys [on|off]—设置光标键应用程序模式为开或关
-   -background c—将背景文本颜色设置为颜色 c
-   -blank [ 0-60 ]—屏幕变黑之前的分钟数（默认为 0，即不变黑）
-   -blength [ n ]—控制台蜂鸣器持续时间（毫秒）（默认为 0）
-   -bfreq h—控制台蜂鸣器频率（音高）（赫兹）（默认为 0）
-   -blink [on|off]—开启或关闭闪烁文本打印。如果不处于控制台，关闭闪烁文本也会关闭所有其他属性
-   -bold [on|off]—开启或关闭粗体打印。如果不处于控制台，关闭粗体也会关闭所有其他属性
-   -clear [ all|rest ]—清除屏幕并将光标移到起始位置。rest 清除至屏幕末尾
-   -clrtabs [ tab1 tab2 tab2 ... ]—清除制表位
-   -cursor [on|off]—开启或关闭控制台光标
-   -defaultc—将渲染选项恢复为默认值
-   -dump [ c ]—将控制台屏幕（默认为当前）保存到文件
-   -file f—设置 -dump 或 -append 的文件名
-   -foreground c—将前景文本颜色设置为颜色 c
-   -half-bright [on|off]—开启或关闭暗淡打印。如果不处于控制台，关闭暗淡也会关闭所有其他属性
-   -hcolor c—设置半亮字符的颜色
-   -initialize—将绘制特性恢复为默认值
-   -inversescreen [on|off]—反转屏幕颜色
-   -linewrap [on|off]—开启或关闭自动换行
-   -msg [on|off]—启用或禁用 printk 内核消息
-   -msglevel n—将 printk 消息级别设置为 n
-   -reset—将屏幕恢复为开机状态
-   -reverse [on|off]—开启或关闭反色文本打印。如果不处于控制台，关闭反色文本也会关闭所有其他属性
-   -softscroll [on|off]—开启或关闭软键盘滚动
-   -store—将当前渲染选项保存为默认值
-   -tabs [tab1 tab2 tab3 . . . ]—设置制表位位置
-   -term terminal_name—使用 terminal_name 代替 TERM 变量的值
-   -ulcolor c—设置下划线字符的颜色
-   -underline [on|off]—开启或关闭下划线打印。如果支持下划线，则使用 ulcolor

### dialog 命令开关

-   -aspect r—基于提示字符串长度相对于对话框的比例 r，作为强制换行过长行的指南（默认为 9）
-   -backtitle b—要在屏幕顶部的背景上显示的字符串 b
-   -beep—每次屏幕重绘时发出蜂鸣声
-   -beep-after—如果输入中断则发出蜂鸣声
-   -begin y x—对话框左上角的位置，而不是居中
-   -clear—退出时清除屏幕

