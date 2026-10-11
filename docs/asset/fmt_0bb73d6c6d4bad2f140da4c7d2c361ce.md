
```
echo ""

cd $1 # 切换到搜索目录

grep -n "$2" $3 # 在 $3 中搜索 $2

echo " " # 打印行

endif
```

# 第 23 章 Shell 编程简介

![](img/6969df54e516231f8e64fd1177ac1127_1587_0.png)

`grep` 用于在文件中搜索模式并打印找到该模式的行。之前介绍过的 `awk` 可以用于提取行中的特定字段。

![](img/6969df54e516231f8e64fd1177ac1127_1587_1.png)

这里是搜索程序的示例：

```bash
martyp $ search /home/martyp/shellprogs awk ifstat

12:# 使用冒号作为一条命令，这样可以方便地传递给 awk。

18:awk 'BEGIN { printf "%10s%10s%10s%10s\n", "ipks",

38:' # awk 程序结束。

martyp $
```

在例例中，我们在 `/home/martyp/shellprogs` 目录下运行 `search`，在 `ifstat` 文件中查找 `awk` 模式。该搜索结果显示了 `ifstat` 文件中三行出现 `awk` 的内容。这些行分别是第 12、18 和 38 行。

在下一节中，我们将稍微扩展此程序，包含测试和分支。

## 测试与分支

你的 shell 程序可以执行许多类型的决策。`if` 提供了做出决策并采取相应行动的灵活性。让我们扩展搜索脚本，以验证是否已提供了三个参数：

```csh
#!/bin/csh

# search

# Usage: search directory pattern files

if ($argv != 3) then                        # 如果提供的参数少于 3 个

    echo "Usage: search directory pattern files"

else                                        # 否则打印用法信息
```

```csh
echo " "                  # 否则打印行并

cd $1                       # 切换到搜索目录

grep -n "$2" $3             # 在 $3 中搜索 $2

echo " "                  # 打印行

endif
```

这个程序被称为 `search1`。我们使用与 `search` 程序相同的参数运行此程序；但是，`search1` 经过了增强，如果我们在运行时没有提供参数，它会提供一条用法信息。下面的示例展示了 `search1`：

```bash
martyp $ search

Usage: search directory pattern files

martyp $ search1 /home/martyp/shellprogs
```

在第一次尝试运行 `search1` 时，我们没有提供任何参数。程序检查我们提供的参数是否少于三个，并产生了用法信息。看到用法信息后，如何使用该程序变得一目了然，我们在下一次尝试运行程序时提供了所需的参数。在此例中，我们在 `/home/martyp/shellprogs` 目录下运行 `search1`，在 `ifstat` 文件中查找 `awk` 模式。该搜索结果产生了 `ifstat` 文件中的三行出现 `awk` 的内容。这些行是第 12、15 和 18 行。

![](img/6969df54e516231f8e64fd1177ac1127_1588_0.png)

这里有四种常见的 `if` 形式：

- 1) `if ... then ... endif`
- 2) `if ... then ... else ... endif`
- 3) `if ... then ... else if ... then ... endif`
- 4) `if ... then ... else if ... then ... else ... endif`

# Shell 编程

## 1549

![](img/6969df54e516231f8e64fd1177ac1127_1592_0.png)

以下名为 `netcheck` 的程序按照指定的间隔运行 `netstat`，并打印一次标题以及共九次 `le0` 的状态：

这里是 `netcheck` 程序的运行示例：

| Name | Mtu | Net/Dest | Address | Ipkts | Oerrs | Opktis | Collis | Queue |
|---|---|---|---|---|---|---|---|---|
| le0 | 1500 | sunys | sunys | 314374989 0 | 17252200 | 52135 | 7580906 | |
| le0 | 1500 | sunys | sunys | 314375038 0 | 17252203 | 52135 | 7580906 | |
| le0 | 1500 | sunys | sunys | 314375185 0 | 17252209 | 52135 | 7580906 | |
| le0 | 1500 | sunys | sunys | 314375257 0 | 17252212 | 52135 | 7580906 | |
| le0 | 1500 | sunys | sunys | 314375364 0 | 17252215 | 52135 | 7580906 | |
| le0 | 1500 | sunys | sunys | 314375444 0 | 17252218 | 52135 | 7580906 | |
| le0 | 1500 | sunys | sunys | 314375508 0 | 17252221 | 52135 | 7580906 | |
| le0 | 1500 | sunys | sunys | 314375588 0 | 17252224 | 52135 | 7580906 | |

计数已达到 9，再次运行 netcheck 以查看 le0 状态。
martyp 9

`netcheck` 的输出在我们指定的每三秒间隔内生成了九次 `netstat` 输出。请记住，当在你的系统上使用此程序时，可能需要修改如局域网接口名称等信息。

该程序通过以下方式增加表达式的值：

```
@count++
```

如果该表达式为真，则将执行命令。`@count++` 是如下形式的赋值运算符：

```
@variable_name operator expression
```

在这种情况下，变量首先被赋值为 "="，随后自动递增 `((++))`。在变量上可以执行若干种操作，如表 23-2 所示：

### 表 23-2 赋值运算符

| 操作 | 符号 | count = 100 的示例 | 结果 |
| --- | --- | --- | --- |
| 存储值 | = | `@count=100` | 100 |
| 自动递增 | ++ | `@count++` | 101 |
| 自动递减 | -- | `@count--` | 99 |
| 加值 | += | `@count+=50` | 150 |
| 减值 | -= | `@count=50` | 50 |
| 乘值 | *= | `@count*=2` | 200 |
| 除以值 | /= | `@count/2` | 50 |

还有比较运算符（例如示例中使用的 "`<`"），以及算术、位运算和逻辑运算符。当你编写 C Shell 脚本并制作越来越多的 Shell 脚本时，你将想要使用所有的运算符。

在编写使用文件的 Shell 脚本时，一组与文件相关的测试条件非常有用。使用 `- operator filename` 格式，你可以使用表 23-3 中的测试项。

### 表 23-3 运算符文件名测试

| 运算符 | 含义 |
|---|--|
| r | 可读权限 |
| w | 可写权限 |
| x | 执行权限 |
| o | 所有权 |
| z | 零长度 |
| f | 文件，不是目录 |
| d | 目录，不是文件 |

以下名为 `filetest` 的程序使用这些运算符测试 `.profile` 文件。因为 `.profile` 不是可执行文件、长度为零或目录，我预计 `filetest` 会发现这些结果为假。

以下是 `.profile` 的详细列表：

```
martyp $ ls -al .profile

-rw-r--r-- 1 martyp staff 594 May 21 09:29 ../profile

marty $
```

![](img/6969df54e516231f8e64fd1177ac1127_1594_0.png)

以下是 Shell 脚本 `filetest` 的列出：

```csh
#!/bin/csh

# 测试文件的程序

if (-e $1) then
```
