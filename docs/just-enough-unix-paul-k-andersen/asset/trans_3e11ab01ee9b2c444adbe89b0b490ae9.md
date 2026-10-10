

## 9.6 使用 sort

### 反转测试的逻辑

`-v` 选项会使 grep 列出不*包含*模式的行。例如，

```bash
$ grep -v dark out3.tmp<Return>
```

There once was a fellow named Frank,
who drove around town in a tank.
and quite hard to park.
But it got him good rates at the bank.

### 基本用法

正如你所预期的，sort 对文件或文件集合中的行进行排序。它还可以在不排序的情况下合并两个或更多文件。sort 命令的一般格式为：

```bash
sort [-bcdfimMnortuyz] [±field] [filelist]
```

如你所见，sort 接受相当数量的选项，但本节只会讨论其中少数几个。*字段*是由空白符界定的一段字符序列。（例如，文本行中的各个单词可以被视为字段。）排序通常根据每行的第一个字段进行，但你可以指定检查其他字段。

### 对文件的第一个字段执行简单排序

以下命令行将列出 out1.tmp、out2.tmp 和 out3.tmp 的内容：

```bash
$ sort *.tmp<Return>
          1
May 1999
Oh, bring back my Bonnie to me!
The contents she wanted to see.
and quite hard to park.
who drove around town in a tank.
2   3   4   5   6   7   8
9 10 11 12 13 14 15
S  M Tu  W Th  F  S
/home/yourlogin
16 17 18 19 20 21 22
23 24 25 26 27 28 29
30 31
But it got him good rates at the bank.
I lit a match to assist her:
It was noisy and dark,
My Bonnie looked into the gas tank,
There once was a fellow named Frank,
Thu  May  6  13:12:46 EST  1999
```

排序顺序也称为*排序序列*。在你理解 **sort** 实用程序所采用的排序顺序之前，这可能会显得有些奇怪。这因系统而异，但以下是一个典型的顺序：

1. 控制字符
2. 空白字符（即空格和制表符）
3. 数字
4. 大写字母
5. 小写字母

你可以应用各种选项来修改排序顺序。以下是一些可能性：

- **sort -b**：忽略前导空格
- **sort -f**：将大写字母和小写字母折叠在一起（忽略大小写）
- **sort -n**：数字排序
- **sort -r**：反转常规顺序（例如，Z 在 a 之前）

### 按第一个字段排序，忽略前导空格和大小写

指定字段偏移量 `+0` 将使 sort 检查每行的第一个字段：

```bash
$ sort -bf +0 *.tmp<Return>
/home/yourlogin
1
16 17 18 19 20 21 22
2 3 4 5 6 7 8
23 24 25 26 27 28 29
30 31
9 10 11 12 13 14 15
and quite hard to park.
But it got him good rates at the bank.
I lit a match to assist her:
It was noisy and dark,
May 1999
My Bonnie looked into the gas tank,
Oh, bring back my Bonnie to me!
S M Tu W Th F S
The contents she wanted to see.
There once was a fellow named Frank,
Thu May 6 13:21:46 EST 1999
who drove around town in a tank.
```

### 按文件的第二个字段排序

指定字段偏移量 `+1` 将使 sort 跳过每行的第一个字段并检查第二个字段。请在 out3.tmp 文件上尝试此操作：

```bash
$ sort -bf +1 out3.tmp<Return>
    who drove around town in a tank.
    But it got him good rates at the bank.
    There once was a fellow named Frank,
      and quite hard to park.
    It was noisy and dark.
```

sort 实用程序的功能远不止我们在此能详细说明的范围。如果你想知道更多，请查阅 UNIX 手册。

## 9.7 管道与分流器（PIPES AND TEES）

管道将一个实用程序的标准输出连接到另一个实用程序的标准输入。分流器（tee）允许你获取命令的输出，并将其同时定向到一个文件和另一个命令。在本节中，你将练习使用管道和分流器。

- **每页查看 2000 年和 2001 年的日历。** 以下命令行之一可以做到：

```bash
$ (cal 1999; cal 2000; cal 2001) | more<Return>
```

或者：

```bash
$ (cal 1999; cal 2000; cal 2001) | pg<Return>
```

- **查看 2000 年和 2001 年的日历，并创建一个包含这些日历的文件。** 这需要用到一个 tee 和两个管道：

```bash
$ (cal 2000; cal 2001) | tee calfile | more<Return>
```

- **每页列出根目录子目录中的文件。** 以下命令之一均可将 ls 的输出通过管道传递给 more 或 pg 实用程序：

```bash
$ ls -a /* | more<Return>
```

或者：

```bash
$ ls -a /* | pg<Return>
```

- **列出根目录子目录中的文件，并创建一个包含此列表的文件。** 这可以使用两个管道和一个 tee 来完成：

```bash
$ ls -a /* | tee root.list | more<Return>
```

这将根目录及其子目录的列表放入文件 `root.list` 中，同时该列表也会显示在终端屏幕上。

- **统计根目录子目录中的文件数量。** 这可以通过以下命令行完成：

```bash
$ ls -a /* | wc -l <Return>
```

- **按大小对根目录子目录的长列表进行打印。** 长文件列表中的第五个字段通常显示文件大小。要按第五个字段排序，请跳过前四个字段（+4）：

```bash
$ ls -al /* | sort -nr +4 | more<Return>
```

- **准备根目录子目录的长列表；按大小排序；并将其发送到标准输出和一个文件中。** 长文件列表中的第五个字段通常显示文件大小。要按第五个字段排序，请跳过前四个字段（+4）：

```bash
$ ls -al /* | sort -nr +4 | tee list.by.size | more<Return>
```

- **在根目录的子目录中查找一个文件。** 因此，要查找文件 passwd，请输入命令行：

```bash
$ ls -a /* | grep passwd<Return>
```

## 9.8 睡眠

sleep 不是一个过滤器。

sleep 命令创建一个进程，该进程“睡眠”指定的时间段。换句话说，sleep 在返回到 shell 之前等待指定的秒数。其一般格式为：

```bash
sleep n
```

其中 `n` 是一个非负整数，表示进程要睡眠的秒数。

- **运行 sleep 命令。** 要睡眠 15 秒，请输入：

```bash
$ sleep 15<Return>
```

- **使用 sleep 延迟另一个命令的执行。** 这是 sleep 实用程序的一个常见应用。例如：

```bash
$ (sleep 60; echo I am awake now)<Return>
```

- **等待进程结束。** 当 sleep 结束时，echo 将打印一条消息：

I am awake now

## 9.9 中断前台进程

如果你以通常的方式（即在前台）启动一个长时间运行的进程，如 `sleep`，那么在该进程结束之前，你无法处理任何其他命令。如果由于某种原因你不想等待那么久，你必须中断该进程。这是通过 **Ctrl**-**C** 键组合完成的。

1. **启动进程。** 例如：
   ```bash
   $ (sleep 120; echo I am awake now) [Return]
   ```
2. **中断进程。** 输入：
   ```bash
   [Control] - C
   ```
   这将中断 `sleep` 并调用 `echo` 命令：
   ```bash
   ^C I am awake now
   $
   ```

## 9.10 运行后台进程

正如我们之前所说，UNIX 允许你“后台”运行一个进程，同时你在前台处理另一个任务。这对于长时间运行的进程非常有用，尤其是那些不需要你注意的进程。作为此类长时间运行进程的一个例子，我们将再次使用 `sleep` 命令。

1. **在后台启动一个长时间运行的进程。** 例如：
   ```bash
   $ (sleep 60; echo I am awake now)& [Return]
   ```
   如果你正在运行 Bourne shell，你应该会看到类似以下内容：
   ```bash
   3271
   ```
   在这个例子中，shell 分配了一个进程标识符（PID）号 3271。（你系统上的实际 PID 可能不同。）

   如果你正在运行 C Shell 或 Korn Shell，你应该会看到类似以下内容：
   ```bash
   [1]     3271
   ```
   在这里，[1] 是作业号，3271 是 PID。

   shell 将显示一个提示符，让你知道它已准备好接受更多命令：
   ```bash
   $
   ```

2. **检查进程状态。** 输入 `ps`（“process status”，进程状态）命令以查看正在发生的事情：
   ```bash
   $ ps [Return]
   ```

