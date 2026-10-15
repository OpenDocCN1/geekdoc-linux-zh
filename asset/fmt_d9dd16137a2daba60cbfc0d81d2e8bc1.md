
### 允许 awk 使用变量

大多数版本的 `awk` 无法直接访问 shell 中设置的环境变量。为了让 `awk` 使用这些变量，必须将它们转换为 `awk` 变量。在命令行设置变量的 `set` 语法如下：

```
awk 'script' var1=value var2=value
```

在这里，`script` 是你想要执行的脚本，`var1`、`var2` 是你想要设置的变量名。通常，`files` 是文件列表。假设你想生成 `fruit_prices.txt` 中小于某个数字 `x` 的水果列表，其中 `x` 由用户提供。为了实现这一点，你需要将 `x` 的值传递给脚本。你可以进行如下更改：

```sh
#!/bin/sh

FRUIT="$1"

if [ -n "$FRUIT" ]; then
  awk -v FRUIT="$FRUIT" '$3 <= FRUIT { print }' fruit_prices.txt
fi
```

在这里，你只打印小于指定数量的项目。假设此脚本名为 `reorder.sh`，执行脚本如下：

```
$ ./reorder.sh 25
```

产生输出：

```
Kiwi $1.50 22
```

## 流控制

`awk` 有三种主要的流控制形式：

- `if` 语句
- `while` 语句
- `for` 语句

`if` 和 `while` 语句与 shell 中的版本相似，而 `for` 语句更接近 C 语言。你将依次查看这些语句。

## if 语句

`if` 语句允许你在执行某些 `awk` 命令之前进行测试。你在之前的示例中使用的模式匹配和表达式本质上都是 `if` 语句，但 `if` 语句应该在 `action` 内部而不是主输入循环中使用。`if` 语句的基本语法如下：

```awk
if (expression1) {
    action1
} else if (expression2) {
    action2
} else {
    action3
}
```

在这里，`expression1` 和 `expression2` 使用运算符创建。它们与你在本章节早期看到的表达式相同。`expression` 周围的括号是必须的。`action`——`action1`、`action2` 和 `action3`——可以是有效的 `awk` 命令序列。这些 `action` 周围的大括号在 `action` 包含多个语句时才需要，但为了清晰性和维护性，我建议始终使用它们。

`else if` 和 `else` 语句是可选的。可以提供的 `else if` 语句数量没有限制。执行过程如下：

- 求值 `expression1` (`if`)。如果 `expression1` 为真，执行 `action1` 并退出 `if` 语句。
- 如果 `expression1` 为假，评估 `expression2` (`else if`)。如果 `expression2` 为真，执行 `action2` 并退出 `if` 语句。
- 如果 `expression2` 为假，执行 `action3` 并退出 `if` 语句 (`else`)。

作为一个简单的示例，编写一个脚本打印 `fruit_prices.txt` 中的水果列表，并突出以下事实：

- 项目价格是否大于美元
- 是否需要重新订单该项目

大于美元的水果用 `*` 字符标记。数量小于 75 需要重新订单的水果用 `REORDER` 字符串标记。使用 `if` 语句，脚本变为：

```sh
#!/bin/sh

awk '{
  printf "%s\t", $0;
  if ($2 ~ /\$[1-9][0-9]*\.[0-9][0-9]/) {
    printf " *";
    if ($3 <= 75 ) {
      printf "REORDER\n";
    } else {
      printf "\n";
    }
  } else {
    if ($3 < 75 ) {
      printf " REORDER\n";
    } else {
      printf "\n";
    }
  }' fruit_prices.txt;
```

输出看起来所示：

| Fruit | Price/lbs | Quantity |
| :--- | :--- | :--- |
| Banana | $0.89 | 100 |
| Peach | $0.79 | 65 |
| Kiwi | $1.50 | 22 REORDER |
| Pineapple | $1.29 | 35 REORDER |
| Apple | $0.99 | 78 |

这个示例还展示了如何测试 `if` 语句。

### while 语句

`while` 语句在表达式为真时执行 `awk` 命令。基本语法是：

```awk
while (expression) {
    actions
}
```

在这里，`expression` 是使用运算符创建的表达式。它与你在本章节早期看到的表达式相同。`expression` 周围的括号是必须的。所执行的操作——`actions`——是任何有效的 `awk` 命令序列。`actions` 周围的大括号在 `action` 包含多个语句时才需要，但为了清晰性和维护性，我建议始终使用它们。

这是一个 `while` 循环的示例，从一数到五：

```awk
awk 'BEGIN{ x=0; while (x < 5) { x+=1; print x ; } }'
```

输出如下：

1
2
3
4
5

### do 语句

`while` 语句的一种变体是 `do` 语句。它在表达式为真时也执行某些操作。

## 基础语法如下

```
do {
    actions
  while (expression)
}
```

这里的 `expression` 是使用条件运算符创建的表达式。它与你在本章较早看到的表达式相同。`expression` 外围的括号是必须的。

应该执行的操作 `actions`，是任何有效 `awk` 命令的序列。`actions` 外围的大括号仅在操作包含多个语句时是必须的，但为了清晰和可维护性，我建议你始终使用它们。

主要的区别在于 `do` 语句至少执行一次，而 `while` 语句可能完全不执行。例如，你可以将上一个示例中的 `while` 循环写为 `do` 循环。

```
$ awk 'BEGIN { BEGIN{ x=0; do { x+=1; print x; } while (x < 5) } }'
```

`nawk`、`gawk` 和 `awk` 在 `do` 语句方面存在细微差异。如果你想使用该语句，应该坚持使用 `nawk` 或 `gawk`，因为旧版本的 `awk` 可能会对其出现问题。如果你担心对 UNIX 版本的移植性，应该避免使用 `do` 语句。

### for 语句

`for` 语句允许重复命令指定的次数。`awk` 中的 `for` 循环与 C 语言中的 `for` 循环相似。

`for` 循环背后的思想是保持一个计数器并在循环的每次迭代中进行测试。每次执行循环时，计数器都会加增。这与 shell 中的 `for` 循环非常不同，后者会对列表中的每个项目执行一组命令。

`for` 循环的基础语法：

```
for (initialize_counter; test_counter; increment_counter) {
    action
}
```

这里 `initialize_counter` 初始化计数器变量，`test_counter` 是一个测试计数器值的表达式，`increment_counter` 增加计数器的值。`for` 循环所使用的表达式外围的括号是必须的。

应该执行的操作 `action`，是任何有效 `awk` 命令的序列。`action` 外围的大括号仅在操作包含多个语句时是必须的，但为了清晰和可维护性，我建议你始终使用它们。

`for` 循环的一个常见用途是遍历记录中的字段并输出它们，可能在此过程中修改每条记录。以下 `for` 循环打印记录中的每个字段，并用两个空格分隔：

```bash
#!/bin/sh

awk '{n  for (x=1;x<=NF;x+=1) {
    printf "%s", $x
  }
  printf "\n"
}' fruit_prices.txt
```
