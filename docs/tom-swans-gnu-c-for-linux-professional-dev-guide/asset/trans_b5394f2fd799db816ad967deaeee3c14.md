

## Do-Forever for 循环

更实用的是 Do-Forever for 循环，即永不结束的循环——直到某个外部条件发生为止。该条件可能是硬件中断，或在 Linux 和 UNIX 中，仅仅是用户按下 C-c（Ctrl-C）的结果。循环通常写成这样：

```c
for (;;) ; // Loop "forever"
```

这个 for 循环不初始化控制变量，不指定控制条件，也不执行表达式。它也没有语句。执行时，该语句会挂起程序，直到发生中断循环锁定的外部事件。再次说明，右括号与分号之间的空白表示这不是错误，而是故意为之。如果你尝试在测试程序中运行它，请按 C-c（Ctrl-C）退出。

尽管看起来似乎很无聊，Do-Forever for 循环还是很有用的。例如，参见下一节“the switch Statement”，了解如何使用 Do-Forever for 循环创建程序菜单。Do-Forever for 循环有时也用于执行多个任务的线程代码中，以及在 X 程序中响应服务器事件，如第六部分“X Window Development”所述。

## The switch Statement

深层嵌套的 if-else 语句看起来可能像老建筑里的管道一样扭曲。通过用 switch 替换 if-else 语句，可以得到更清晰、更易维护的代码。例如，考虑以下一系列 if-else 语句，每个语句都将一个表达式与一个值进行比较：

```c
if (expression == value1)
    statement1;
else if (expression == value2)
    statement2;
else if (expression == value3)
    statement3;
else
    defaultStatement; // Optional
```

通常称为多路决策树，该结构根据一系列条件从多个语句中选择。嵌套的 if-else 语句并没有什么问题，但使用 switch 通常会产生更清晰的代码。使用 switch，你可以这样写前面的 if-else 语句：

```c
switch (expression) {
    case value1:
        statement1;    // Executes if expression == value1
        break;         // Exit the switch statement
    case value2:
        statement2;    // Executes if expression == value2
        break;         // Exit the switch statement
    case value3:
        statement3;    // Executes if expression == value3
        break;         // Exit the switch statement
    default:           // Optional
        defaultStatement; // Executes if no values match expression
}
```

乍一看，等价的 switch 语句可能看起来同样复杂，但在熟悉其结构后，你会发现 switch 语句比深层嵌套的 if-else 语句更容易管理。switch 关键字后面跟着一个要与一组值进行比较的表达式。这通常只是变量的名称——例如，程序用户输入的字符，或从计算中获得的整数值。在 switch 的块内，case 选择器将表达式与指定的值进行比较。表达式

```c
case value1:
```

将 value1 与 switch 语句的表达式进行相等性比较。如果表达式与此 case 值匹配，则执行以下语句。如果表达式不等于此 case 的值，则评估下一个 case。末尾的 default: 选择器指定如果没有 case 与表达式匹配时的可选操作。

> **Tip**  case 和 default 表达式以冒号结尾。很容易忘记这一点，编译器“解析”错误的一个常见原因是 switch case 选择器末尾缺少冒号。

请注意，在前面的示例代码中，每个 case 都以 break 语句结束。break 在其他类型的语句中也是如此，它会立即结束 switch 语句。要理解 break 在 switch case 中的作用，请查看第一个 case：

```c
case value1:
    statement1;
    break;
```

如果 switch 语句的表达式等于 value1，程序将执行 statement1。之后，break 退出 switch 语句，程序继续执行 switch 语句闭合大括号之后的代码。但是，如果某个 case 没有以 break 结束，则会执行下一个 case 的语句。被称为“贯穿 case”，缺少 break 可能是错误，但有时是故意的。例如，考虑这个 switch 语句：

```c
switch (expression) {
    case value1:
        statement1;    // Fall through to statement2
    case value2:
        statement2;
        break;         // Exit switch statement
    case value3:
        statement3;
        break;         // Not needed but okay
}
```

如果 expression 等于 value1，则执行 statement1。由于没有跟随的 break 语句，程序继续执行 statement2，之后 break 结束 switch 语句。最好对故意的“贯穿”添加注释。在另一次迭代中，如果 expression 等于 value2，则只执行 statement2，之后 break 结束 switch 语句。如果 expression 等于 value3，则只执行 statement3。statement3 之后的 break 并不是严格必需的，因为这是 switch 语句的末尾，但仔细
