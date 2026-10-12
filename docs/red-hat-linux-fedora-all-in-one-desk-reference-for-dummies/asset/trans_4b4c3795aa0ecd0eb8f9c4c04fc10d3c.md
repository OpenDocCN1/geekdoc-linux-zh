
## 表 2-3（续）

| 操作符组 | 操作符名称 | 表示法 | 结合性 |
|---|---|---|---|
| 一元 | 后自增 | x++ | 从右到左 |
| 一元 | 后自减 | x-- |  |
| 一元 | 前自增 | ++x |  |
| 一元 | 前自减 | --x |  |
| 一元 | 取地址 | &x |  |
| 一元 | 间接寻址 | *x |  |
| 一元 | 正号 | +x |  |
| 一元 | 负号 | -x |  |
| 一元 | 按位非 | ~x |  |
| 一元 | 逻辑非 | !x |  |
| 一元 | sizeof | sizeof x |  |
| 一元 | 类型转换 | (type)x |  |
| 乘法 | 乘法 | x*y | 从左到右 |
| 乘法 | 除法 | x/y |  |
| 乘法 | 取余 | x%y |  |
| 加法 | 加 | x+y | 从左到右 |
| 加法 | 减 | x-y |  |
| 移位 | 左移 | x<<y | 从左到右 |
| 移位 | 右移 | x>>y |  |
| 关系 | 大于 | x>y | 从左到右 |
| 关系 | 大于等于 | x>=y |  |
| 关系 | 小于 | x<y |  |
| 关系 | 小于等于 | x<=y |  |
| 相等 | 等于 | x==y | 从左到右 |
| 相等 | 不等于 | x!=y |  |
| 按位 | 按位与 | x&y | 从左到右 |
| 按位 | 按位异或 | x^y |  |
| 按位 | 按位或 | x|y |  |
| 逻辑 | 逻辑与 | x&&y | 从左到右 |
| 逻辑 | 逻辑或 | x||y |  |
| 条件 | 条件运算符 | z?x:y | 从右到左 |
| 赋值 | 赋值 | x=y | 从右到左 |
| 赋值 | 乘法赋值 | x *= y |  |
| 赋值 | 除法赋值 | x /= y |  |
| 赋值 | 取余赋值 | x %= y |  |
|  | 加法赋值 | x += y |  |
|  | 减法赋值 | x -= y |  |
|  | 左移赋值 | x <<= y |  |
|  | 右移赋值 | x >>= y |  |
|  | 按位与赋值 | x &= y |  |
|  | 按位异或赋值 | x ^= y |  |
|  | 按位或赋值 | x |= y |  |
| 逗号 | 逗号 | x , y | 从左到右 |

回到解释 *iptr[4] 的问题，快速查看表 2-3 可知 [] 运算符的优先级高于 * 运算符。因此，当编译器处理表达式 *iptr[4] 时，它首先计算 iptr[4]，然后应用间接运算符，从而得到 iptr[4] 中地址的 int 值。

## 语句

你使用语句来表示 C 函数将执行的操作并控制 C 程序中的执行流程。语句由关键字、表达式和其他语句组成。每个语句以分号（;）结束。

特殊类型的语句——复合语句——是一组用一对大括号（{ ... }）括起来的语句。函数的体是一个复合语句。此类复合语句（也称为块）可以包含局部变量。

在以下按字母顺序排列的部分中，我简要描述了 C 中可用的语句类型。

### break 语句

你使用 break 语句跳到最内层的 do、for、switch 或 while 语句之后的语句。它也用于从 switch 语句中退出。以下示例使用 break 退出 for 循环：

```c
for(i = 0; i < ncommands; i++)
{
    if(strcmp(input, commands[i]) == 0) break;
}
```

### case 语句

case 语句在 switch 语句中标记标签。以下是一个示例（此处 interrupt_id 是一个整数变量）：

```c
switch (interrupt_id)
{
    case XMIT_RDY:
        transmit();
        break;
    case RCV_RDY:
        receive();
        break;
}
```

### 复合语句或块

复合语句或块是一组声明后跟语句，全部用一对大括号（{ ... }）括起来。典型的复合语句是函数的体以及 if 语句后面的代码块。在以下示例中，大括号内出现的所有内容——声明和语句——构成一个复合语句：

```c
if(theEvent.xexpose.count == 0)
{
    int i;
    /* Clear the window and draw the figures
     * in the "figures" array
     */
    XClearWindow(theDisplay, dWin);
    if(numfigures > 0)
        for(i=0; i<numfigures; i++)
            draw_figure(theDisplay, dWin, theGC, i);
}
```

### continue 语句

continue 语句开始其所在的最内层 do、for 或 while 语句的下一次迭代。当你想跳过循环的执行时，可以使用 continue。例如，要将 1 到 10 的数字相加，但排除 5，可以使用一个在循环索引（i）为 5 时跳过循环体的 for 循环：

```c
for(i=0, sum=0; i <= 10; i++)
{
    if(i == 5) continue;  /* Exclude 5 */
    sum += i;
}
```

### default 标签

你使用 default 作为 switch 语句中的标签来标记当没有任何 case 标签匹配 switch 表达式时将执行的代码。

### do 语句

do 语句与 while 结合形成具有以下结构的迭代循环：

```
do
  statement
  while(expression);
```

其中 statement（通常是复合语句）执行直到 while 语句中的表达式求值为 0。表达式在每次执行语句后求值——因此 do-while 块至少执行一次。例如，要将 1 到 10 的数字相加，可以使用以下 do 语句：

```c
sum = 0;
do
{
    sum += i;
    i++;
}
while(i <= 10);
```

### 表达式语句

表达式语句根据其副作用进行求值。表达式语句的典型用途包括调用函数、递增变量以及为变量赋值。以下是一些示例：

```c
printf("Hello, World!\n");
i++;
num_bytes = length * sizeof(char);
```

### for 语句

使用 for 语句执行语句任意次数（该次数基于表达式的值）。语法如下：

```
for (expr_1; expr_2; expr_3) statement
```

其中 expr_1 在循环开始时求值一次，并且语句执行直到表达式 expr_2 求值为 0。第三个表达式 expr_3 在每次执行语句后求值。三个表达式都是可选的，如果省略 expr_2，则其值假定为 1。以下示例使用 for 循环将 1 到 10 的数字相加：

```c
for(i=0, sum=0; i <= 10; sum += i, i++);
```

在此示例中，实际的加法工作在第三个表达式中完成，并且由 for 循环控制的语句是一个空语句（单个 ;）。

### goto 语句

goto 语句将控制转移到语句标签。以下示例提示用户输入一个值，如果该值不可接受则重复请求：

```c
ReEnter;
printf("Enter offset: ");
scanf("%d", &offset);
if(offset < 0 || offset > MAX_OFFSET)
{
    printf("Bad offset: %d Please reenter:\n", offset);
    goto ReEnter;
}
```

### if 语句

你可以使用 if 语句测试一个表达式，并且仅当表达式不为零时执行语句。if 语句采用以下形式：

```
if ( expression ) statement
```

if 之后的语句仅在括号中的表达式求值为非零值时执行。该语句通常是复合语句。以下是一个示例：

```c
if(mem_left < threshold)
{
    Message("Low on memory! Close some windows.\n");
}
```

### if-else 语句

if-else 语句是 if 语句与 else 子句结合的一种形式。语句的语法为

```
if ( expression )
    statement_1
else
    statement_2
```

其中如果括号内的表达式不为零，则执行 statement_1。否则，执行 statement_2。以下示例使用 if 和 else 选择两个变量中较小的一个：

```c
if ( a <= b)
    smaller = a;
else
    smaller = b;
```

### 空语句

空语句由单个分号表示，不执行任何操作。当所有处理都在循环表达式中完成而不是在循环体中完成时，你在循环中使用空语句。例如，要定位标记字符串末尾的零字节，可以使用以下语句：

```c
char str[80] = "Test";
int i;

for (i=0; str[i] != '\0'; i++)
    ; /* Null statement */
```

### return 语句

return 语句停止执行当前函数并将控制返回给调用函数。语法是

```
return expression;
```

其中表达式的值作为函数的值返回。对于不返回值 的函数，使用以下方式不带表达式的 return 语句：

```
return;
```

### switch 语句

switch 语句根据表达式的值执行多分支。它具有以下语法：

```
switch (expression)
{
    case value1:
        statement_1
        break;
    case value2:
