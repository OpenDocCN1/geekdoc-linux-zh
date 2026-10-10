
22      /* 22 */        if(a[j].key > a[j+1].key) {

23      /* 23 */          t = a[j];

24      /* 24 */          a[j] = a[j+1];

25      /* 25 */          a[j+1] = t;

26      /* 26 */          s++;

27            }

```

`list` 命令显示当前位置周围的代码部分。例如：

```
(gdb) list

18      /* 18 */      int s = 1;

19      /* 19 */      for(i = 0; i < n; i++) {

20      /* 20 */      s = 0;

21      /* 21 */      for(j = 0; j < n; j++) {

22      /* 22 */        if(a[j].key > a[j+1].key) {

23      /* 23 */          t = a[j];

24      /* 24 */          a[j] = a[j+1];

25      /* 25 */          a[j+1] = t;

26      /* 26 */          s++;

27      }
```

## 设置断点

为了找到程序失败的地方，我们需要能够看到它在运行时在做什么。我们可以通过设置断点在任何点停止程序。这些会导致程序停止并将控制权返回给调试器。我们将能够检查变量然后允许程序继续。

`sort` 函数中有两个循环。外层循环变量 `i` 为数组中的每个元素运行一次。内层循环交换列表中后面的元素。这具有将较小元素泡到顶部的效果。在每次运行外层循环后，最大的元素应该已经到达底部。我们可以通过在外层循环处停止程序并检查数组的状态来确认这一点。

许多命令用于设置断点。这些通过 `gdb help breakpoint` 列出：

```
gdb help breakpoint

让程序在特定点停止。
```

- `watch` - 为表达式设置监视点
- `break` - 在指定行或函数设置断点
- `catch` - 设置捕获事件
- `clear` - 清除指定行或函数的断点
- `commands` - 设置命中断点时执行的命令
- `condition` - 指定仅当 `COND` 为真时中断断点 `N`
- `delete` - 删除某些断点或自动显示表达式

| 行 | 调试 | 代码 / 操作 |
| :--- | :--- | :--- |
| 25 | /* 25 */ | `a[j] = a[j+1];` |
| 26 | /* 26 */ | `a[j+1] = t;` |
| 27 | /* 27 */ | `s++;` |
| (gdb) | | |

我们从第 22 行看到循环被设置为 `n`。在这种情况下，`n` 是 5，所以 `j` 的最终值为 4，这超出了一个。值 4 导致了 `[4]` 与 `s` 的比较。解决这个特定问题的一种方法是将循环终止改为 `n-1`。

让我们进行该更改，调用新的程序 `debug4.c`，重新编译并再次尝试。

```
$ cc -g -o debug4 debug4.c

$ ./debug4

array[0] = {john, 2}

array[1] = {alex, 1}

array[2] = {bill, 3}

array[3] = {neil, 4}

array[4] = {rick, 5}
```

程序仍然无法工作，因为它打印了一个排序不正确的列表。让我们使用 `gdb` 单步执行程序。

# 第 10 章

- `disable` - 禁用某些断点
- `enable` - 启用某些断点
- `hbreak` - 设置一个硬件辅助断点
- `ignore` - 设置断点 `N` 的忽略计数为 `COUNT`
- `break` - 为匹配 `REGEXP` 的所有函数设置断点
- `watch` - 为表达式设置读取监视点
- `tbreak` - 设置一个临时断点
- `catch` - 设置临时捕获点以捕获事件
- `thbreak` - 设置一个临时辅助断点
- `watch` - 为表达式设置监视点

输入命令名加 `"help"` 可查看完整文档。在不歧义的情况下，允许使用命令缩写。

让我们在第 20 行设置一个断点并运行程序：

```
$ gdb debug4

(gdb) break 20

Breakpoint 1 at 0x804835d: file debug4.c, line 20

(gdb) run

Starting program: /home/bill/BLP3/chapter10/debug4
```

```
Breakpoint 1, sort (a=0x8049580, n=5) at debug4.c:20

20 /* 20 */; for( i < n && s != 0; i++) {
```

我们可以通过命令打印数组，然后允许程序继续。这允许程序一直运行到遇到下一个断点，在本例中，它会执行到第 20 行。我们任何时候都可以激活多个断点。

```
(gdb) print array[0]

$ 1 = "bill", '\u000' <repeats 4091 times>, key = 3
```

为了打印多个连续的项，我们可以使用构造符号 `@<number>` 让 `gdb` 打印指定数量的数组元素。要打印数组的所有元素，我们可以使用：

```
(gdb) print array[0]@5

$ 2 = {data = "bill", '\u000' <repeats 4091 times, key = 3},
data = "nil", '\u000' <repeats 4091 times, key = 4},
data = "john", '\u000' <repeats 4091 times, key = 2},
data = "rick", '\u000' <repeats 4091 times, key = 5},
data = "alex", '\u000' <repeats 4091 times, key = 1}}
```

注意，输出经过了微调的整理以便于阅读。由于这是第一次循环，数组还没有变化。当我们允许程序继续执行时，可以看到随着执行的进行，数组发生了连续的变化：

```
(gdb) cont

Continuing.
```

```
Breakpoint 1, sort (a=0x8049580, n=4) at debug4.c:20

20 /* 20 */ for( i < n && s != 0; i++) {
```

```
(gdb) print array[0]*@5

$ 3 = {data = "bill", '\u000' <repeats 4091 times>, key = 3},
  data = {"john", '\u000' <repeats 4091 times, key = 2},
  data = {"neil", '\u000' <repeats 4091 times, key = 4},
  data = {"alex", '\u000' <repeats 4091 times, key = 1},
  data = {"rick", '\u000' <repeats 4091 times, key = 5}}

(gdb)
```

我们可以使用 `display` 命令让 `gdb` 在程序在断点处停止时自动显示数组：

```
(gdb) display array[0]@@5

1: array[]@ 5 = {{data = "bill", '\u000' <repeats 4091 times, key = 3},
  data = {"john", '\u000' <repeats 4091 times, key = 2},
  data = {"neil", '\u000' <repeats 4091 times, key = 4},
  data = {"alex", '\u000' <repeats 4091 times, key = 1},
  data = {"rick", '\u000' <repeats 4091 times, key = 5}}
```

此外，我们可以更改断点，使其不再停止程序，而是简单显示我们记录的数据并继续。要做到这一点，我们使用命令来指定在命中断点时执行哪种调试器命令。由于我们已经设置了 `display`，所以只需要将断点命令设置为继续执行即可。

```
(gdb) commands

Type commands for breakpoint 1 is hit, one per line.

End with a line saying "end".

> cont

> end
```

现在，当我们允许程序继续时，它将运行到完成，并在外层循环附近的时间打印数组的值。

```
