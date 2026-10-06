

$ 执行 new.hire，并将 new.hire 作为参数
请求 ID 为 laserl24 (标准输入)
$

每当你执行该程序时，无论命令行后面跟着什么单词，它都会被 shell 存储在第一个位置参数中，并传递给程序。在第一个示例中，new.hire 将存储在此参数中。

位置参数的替换与其他类型的变量替换完全相同，因此当 shell 看到

$1 时会将 $1 替换为提供给程序的第一个参数：new.hire。

再举一个例子，以下名为 `ison` 的程序可以让你知道指定的用户是否已登录：

```
$ ison
who | grep $1
$ who
root console t 7 Jul 8 12:37
barney tty03 Jul 8 12:28
fred tty04 Jul 8 13:24
joanne tty07 Jul 8 09:35
tony tty19 Jul 8 08:30
lulu tty23 Jul 8 09:55
$ ison
tony tty19 Jul 8 08:30
$ ison pat
```

> 查看谁在在线
> 未登录

## $ 变量

除了位置变量外，特殊 shell 变量 $$ 会被设置为在命令行上输入的参数数量。正如你将在本章中看到的，变量经常被程序用于测试，以确定用户是否指定了正确数量的参数。

下一个名为 `args` 的程序是为了让你更熟悉参数传递给 shell 程序的方式。学习每个示例的输出，并确保你理解了它：

```
$ args
echo $$ arguments passed
echo arg 1 = $1; arg 2 = $2; arg 3 = $3;
$ args a b c
3 arguments passed
arg 1 = :a; arg 2 = :b; arg 3 = :c;
$ args a b
```

> 查看该程序
> 执行
> 尝试使用两个参数

## $ 变量

2 个参数传递
arg 1 = :a arg 2 = :b arg 3 = 
未分配的参数为空

如你所见，shell 在执行你的 shell 程序时会进行正常的命令行处理。这意味着在为你的程序指定参数时，你可以利用正常的便利特性，例如文件名替换和变量替换。

## $ 变量

该特殊变量引用所有传递给程序的参数。这在接收不确定或可变数量参数的程序通常有用。你稍后会看到更多示例。这是一个说明其用法的程序：

```
$ cat args2
echo $* arguments passed
echo they are $*
$ args2 a b c
3 arguments passed
they are :a b c:
$ args2 one two
2 arguments passed
they are :one two:
$ args2
0 arguments passed
they are ::
$ args2 * arguments passed
they are :args args2 names nu phonebook stat xact xtra
$
```

## 一个在电话录中查找某人的程序

这里是之前示例中的电话录文件：

```
$ cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
$
```

你已经如何使用 grep 在文件中查找某人：

```
$ grep Cheb phonebook
Alice Chebbe 973-555-2015
$
```

你也知道，如果你想按全名查找某人，需要在单词周围加上引号以保持参数的整体：

```
$ grep "Susan T" phonebook
Susan Topple 212-555-4932
$
```

如果能写一个可以用来查找某人的脚本就好了。我们将程序命名为 `lu`，并将要查找的名字作为其参数：

```
$ cat lu
# 在电话录中查找某人
#
grep $1 phonebook
$
```

这里是 `lu` 的示例用法：

```
$ lu Alice
Alice Chebbe 973-555-2015
$ lu Susan
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
$ lu "Susan T"
grep: can't open T
phonebook:Susan Goldberg 201-555-7776
phonebook:Susan Topple 212-555-4932
$
```

在前面的示例中，我们足够地将 Susan T 包在双引号中；那么发生了什么？再次查看 `lu` 程序中 `grep` 的调用：

```
grep $1 phonebook
```

## 一个向电话录添加某人的程序

发现问题了吗？将 Susan 包在双引号内会导致它作为一个参数传递给 `lu`，但当 shell 在程序内的 grep 命令中将此值替换为 $1 时，它将其作为两个参数传递。

你可以通过在 `lu` 程序中将 $1 包在双引号内来解决这个问题：

```
$ cat lu
# 在电话录中查找某人 -- 版本 2
$ grep "$1" phonebook
$
```

在这种情况下，单引号不起作用。为什么？现在让我们再次尝试该调用：

```
$ lu Tony Iannino 973-555-1295
$ lu "Susan T"
Susan Topple 212-555-4932
```

## 一个向电话录添加某人的程序

让我们继续开发处理电话录文件的程序。你可能在某个时刻想向文件中添加某人，因为我们的电话录文件很小，所以让我们写一个名为 `add` 的程序，接受两个参数：要添加的名字和他们的号码。`add` 程序简单地将用制表符分隔的名字和号码追加到电话录文件的末尾：

```
$ cat add
# 向电话录中添加某人
echo "$1"$2" >> phonebook
```

尽管你看不出来，在上面的 echo 命令中，有一个制表符分隔了 $1 和 $2。这个制表符必须被引用以防止被 shell 替换掉。试试我们的程序：

```
$ add 'Susan T' 212-555-4932
cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
Susan T 212-555-4932
```

## 参数传递

2 个参数传递
arg 1 = :a arg 2 = :b arg 3 = 
未分配的参数为空

如你所见，shell 在执行你的 shell 程序时会进行正常的命令行处理。这意味着在为你的程序指定参数时，你可以利用正常的便利特性，例如文件名替换和变量替换。

## $ 变量

特殊变量引用所有传递给程序的参数。这在接收不确定或可变数量参数的程序通常有用。你稍后会看到更多示例。

cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295

## 第 6 章 参数

```
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
$ 973-555-978

## 电话录中的查找

```
$ add "$1" /2/phonebook
$ Billy Bach' 201-555-718
cat phonebook
$
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
Billy Bach 201-555-718
```

## 从电话录中删除某人

```
$ rem
# 从电话录中删除某人
grep -v "$1" phonebook > /tmp/phonebook
$
```

（提示：/tmp 是 Unix 系统中临时文件的目录，通常在系统重启时会被清空。）在 grep 命令完成后，电话录文件将被 /tmp 中的新文件替换。

```
$ rem 'Stromboli Pizza'
cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
$
$ rem Susan
cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Liz Stachiw 212-555-2298
Tony Iannino 973-555-1295
$
```

> 删除此条目

第一个案例在删除 Stromboli Pizza 时运行正常。但在另一种情况下，两个 Susan 的条目都被删除了，因为它们匹配了模式。这不妙！你可以使用 add 程序将它们重新添加电话录：

```
$ add 'Susan Goldberg' 201-555-7776
$ add 'Susan Topple' 212-555-4932
$
```

