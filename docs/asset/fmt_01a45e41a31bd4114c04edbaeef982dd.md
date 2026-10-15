
| 输入: | | | |
|---|---|---|---|
| 1 | clothing | 3141 | |
| 1 | computers | 9161 | |
| 1 | textbooks | 21312 | |
| 2 | clothing | 3252 | |
| 2 | computers | 12321 | |
| 2 | supplies | 2242 | |
| 2 | textbooks | 15462 | |

# 决策语句

决策语句是关于做出的。我们一直在通过模式匹配隐式地做出决策，但 `awk` 也提供了动作语句来显式地做出决策。然而，无论决策有多复杂，所有的计算机决策都必须还原为二进制决策：一个表达式要么为真，要么为假。当为真时，执行真动作；当为假时，执行假动作。基本的决策语句是 `if-else` 语句。

## if-else 语句

`if-else` 动作语句在所有编程语言中都是通用的。在其中，我们评估一个表达式并采取适当的动作。真动作是必须的，尽管它可以是一个空语句（不带动作的分号）。假动作是可选的，但如果使用，则紧跟在 `else` 动作语句之后。任何可以简化为真或假的表达式都可以使用，但逻辑表达式是最常见的。基本的决策格式见图 12.14。

![](img/6e4cdc423ec40606ea72b32fdafff220_465_0.png)

当 `if-else` 中的动作语句是另一个 `if-else` 时，我们就有了所谓的嵌套 `if` 动作语句。在使用嵌套 `if` 语句时必须非常小心，以确保 `else` 动作正确地关联到正确的 `if`。每个 `else` 语句都与最近的未关联的 `if` 语句匹配。规则很简单，但很容易编写代码。当代码编写错误时，我们称之为“悬空 else”问题（`dangling else problem`）。

| 嵌套 else 规则 |
|---|
| 每个 `else` 语句都与上一个未关联的 `if` 语句关联。 |

图 12.15 展示了悬空 else 问题。本意是嵌套的 `if` 没有 `else` 语句；`else` 语句正确地关联到第一个动作。然而，使用 `awk` 的关联规则，`action2` 会关联到嵌套的 `if` 表达式。

### 第 12.6 节 • 动作 445

![](img/6e4cdc423ec40606ea72b32fdafff220_466_0.png)

图 12.15 悬空 else

要解决这个问题，我们只需要像在第 12.15 节那样将嵌套的 `if` 放在复合语句（大括号）中。

### 第 12.15 节 避免悬空 else

```
if (expression1)

{

    if (expression2)

        action1

    } # 嵌套 if 结束

else

    action2

} # 外部 if 结束
```

现在让我们写一个计算计算机部门平均销售额的章节。如果他们超过了我们的目标（`$10,000`），我们就打印一条销售额良好的消息。如果低于我们的目标，我们就打印一条该谈话的消息。为了充分测试此脚本，我们需要运行它，第一次使用一个可以打印良好销售额的目标，另一次使用一个打印谈话的目标。我们在第 12.16 节中展示良好的销售额。

### 第 12.16 节 打印部门平均值

```
$ awk -f compSalesAvg.awk sales1.dat

# compSalesAvg.awk

{

    if ($2 == "computers")

        compSales += $3

        numMons++

}
```

### 第 12.16 节 打印部门平均值——继续

```
END {

  if (compSales / numMons > 10000)

    print "Good sales"

  else

    print "Time for talk"

}
```

# 控制动作

有三个语句可以控制脚本的执行：`next`、`getline` 和 `exit`。

## Next

`next` 语句终止当前记录的处理并开始处理记录。如果没有记录待处理，它将控制权转移到末尾。在第 12.17 节中，我们计算销售平均值，跳过任何销售额 (`$3`) 为零的记录。

### 第 12.17 节 跳过零销售额

```
awk -f averageSales.awk sales1.dat

# averageSales 脚本

$3 == 0 (next)

# 有非零销售

{

  total += $3

  count++

}

# 非零销售

END (avg = total / count)

  printf("Total sales: %9.2f\n", total)

  printf("Number of sales: %7d\n", count)

  printf("Average sales: %9.2f\n", avg)

}
```

| | | |
|---|---|---|
| 1 | clothing | 3141 |
| 1 | computers | 9161 |
| 1 | textbooks | 21312 |
| 2 | clothing | 3252 |
| 2 | computers | 12321 |
| 2 | supplies | 2242 |
| 2 | textbooks | 15462 |

## 获取行

与 `next` 类似，`getline` 读取记录（行）。与 `next` 不同，它继续执行脚本；而不是回到开头。`getline` 之后的动作和语句适用于刚刚读取的记录。其格式如下所示：

```
getline
```

## 会话 12.18 文件中的行交换 (awk)——续

```awk
if ((getline evenLine) == 1) {
  print evenLine
  print $0
} else if getline
else
  print $0
```

| 输入: | 输出 |
|---|---|
| line 1 | line 2 |
| line 2 | line 1 |
| line 3 | line 4 |
| line 4 | line 3 |
| line 5 | line 5 |

会话 12.18 分析：该脚本演示了 `getline` 的两种功能。首先，我们将偶数行读入变量 `evenLine`。其次，我们使用返回值来检测文件末尾。当 `getline` 返回成功结果 (`1`) 时，我们打印 `evenLine` 然后打印 `$0`。如果它没有返回，我们假设已经到了文件末尾，并仅打印 `$0` 中的奇数行。从技术上讲，这是一个潜在漏洞，因为结果可能是错误而不是文件末尾。

## 退出 (Exit)

`next` 跳到脚本末尾并读取下一个记录，而 `exit` 则终止脚本。如果指定了结束模式，它将执行 `exit` 语句然后退出。如果没有指定结束模式，它将立即退出脚本。当 `exit` 使用于结束模式时，脚本将立即终止，而不执行剩余的结束语句。

`exit` 应该预留给错误情况。在会话 12.19 中，我们在除法之前通过测试计数器来防止除零。请注意，我们使用 `100` 作为 `exit` 语句的一个属性。此值可以与用户进行通信。我们将在学习 shell 脚本时更详细地讨论这一概念。

## 会话 12.19 使用 exit 防止除零

```awk
$ awk -f salesZeroDiv.awk zeroSales.dat

# salesZeroDiv.awk 脚本

# 使用取反的比较进行测试

$3 == 0 {next}

total += $3

print $1 $2 $3

count++

} # 非零销售

END {

  if (count == 0) {

    printf("No sales to average\n")

    exit 100

  }

  avrg = total / count

  printf("Total sales : $%9.2f\n", total)

  printf("Number of sales: %7d\n", count)

  printf("Average sales : $%9.2f\n", avrg)

} # END 块结束
```
