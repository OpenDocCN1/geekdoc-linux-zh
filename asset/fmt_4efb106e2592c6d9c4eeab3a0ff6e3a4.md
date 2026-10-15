
# 记录都被读取后会失败

```perl
while (read (GUEST_LOG, $buffer, $GuestEntrySize)
{
```

注意 `read` 的 `LENGTH` 参数使用了 `$GuestEntrySize` 而不是硬编码数字；这是另一个将常量（即非变量）值放置在一个地方的智慧示例，在那里可以轻松更改。从文件中读取的每个记录都已解包到一个数组中，正如你之前学的那样。

## for 循环、空字符

调用 `unpack` 后的代码块引入了 Perl 的 `for` 语句，`for` 类似于 `foreach`，因为它建立了一个循环。但虽然 `foreach` 适合从数组中提取元素直到为空，而 `for` 对许多数据结构提供了比 `foreach` 大得多的控制。（实际上，`for` 和 `foreach` 是相同的；这里描述的差异仅仅是事实标准用法。）

`for` 使用计数器变量（在本例中为 `$n`）和一个终止条件来决定何时结束。`for` 的规范如下：

- for (起始计数; 终止条件);

对计数执行某些操作

```perl
{
  执行此代码块;
}
```

`for` 特别适合遍历订阅数组，就像你在 `guestbook.pl` 的 `for` 块中做的那样。此例的目的是遍历 `@InfoArray` 的每个字符串成员，并去除在通过 `pack` 时用于填充它们的尾 NULL 字符。`for` 的计数器 `$n` 从 0 开始。它在 `$n` 等于 `NumElements -1` 时终止，这是数组中除最后一个（表示留言板条目创建时间的长整数值）之外的所有元素。每次循环，都会执行 `$n++`，使其递增。

元素在循环体中通过正则表达式替换：

```perl
$InfoArray[$n] ~ s\/0//;
```

在这种情况下，替换运算符全局搜索（注意结尾的 `g`）所有 `\0`（NULL 字符）的出现处并将其替换为空，从而从字符串中移除 NULL 字符。

## 记录时间

`guestbook.pl` 中最后一个新内容是 Perl 函数 `localtime`。

表示从某个纪元以来数十亿秒的 4 字节整数

### 为你的网站创建一个留言板 395

本地 `time` 的规范如下：

```perl
($sec, $min, $hour, $mday, $mon, $year, $wday, $yday, $isdst) = localtime(time);
```

其中

- `$sec` 是超过分钟的秒数
- `$min` 是超过小时的分钟数
- `$hour` 是午夜后的小时数
- `$mday` 是月份中的几天，从 0 开始，而不是 1
- `$mon` 是数字月份，同样从 0 开始
- `$year` 是从 1900 年以来的年份（例如 2002 年为 102）
- `$wday` 是星期，从 0 开始
- `$yday` 是一年中的几天
- `$isdst` 是一个指示是否为夏令时间的标志
- `time` 是被添加到 `GuestBook.pm` 的本地时间值的 4 字节整数

```perl
print "WeekDay[$wday],Month[$mon] $mday, ",
print " at $hour";
print "0" if $min < 10;
print "$min";
print "0" if $sec < 10;
print "$sec<BR>\n";
```

分隔符。以下内容是等价的：

```perl
@stooges = ( "Larry", "Moe", "Curly" );
```

```perl
@stooges = qw( Larry Moe Curly );
```

`qw()` 版本更易读和维护，因为你不需要处理引号和逗号。

启动你的网络浏览器并连接到 `guestbook.html`。填入几次虚假或真实的条目。你应该看到与图 14.5 所示类似的内容。

![](img/6e99147f217994f89499215b2cff677f_419_0.png)

**图 14.5：** 填写表单。

## TIPS

如果你在提交表单后点击浏览器的返回按钮，你将回到表单页面。点击“清除表单”获取一个空白表单并再次操作。

最后，点击感谢页面上调用显示脚本（`guestbook.pl`）的链接。你会看到与图 14.6 类似的内容。

### 为你的网站创建一个留言板 393

![](img/6e99147f217994f89499215b2cff677f_420_0.png)

图 14.6：显示留言板条目

## 解析显示程序

让某个东西运行起来真是令人兴奋，不是吗？现在到了棘手的部分：理解你所做的工作。

实际上，`guestbook.pl` 中并没有多少你还没有做过的东西。从文件中获取记录的 Perl `read` 函数设置在一个 `while` 循环中，该循环在 `read` 到文件末尾时终止：

# 读取记录并在 while 循环中显示它们。while 块顶部的测试 # 在所有

# 记录都被读取后会失败。

```perl
while (read (GUEST_LOG, $buffer, $GuestEntrySize)
{
```
