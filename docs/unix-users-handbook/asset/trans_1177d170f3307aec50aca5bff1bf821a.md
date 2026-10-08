
此代码片段的输出为：

```
A
b b b
A
b b b
A
b b b
A
b b b
```

注意，外层循环执行一次，然后内层循环执行完毕。外层循环再次执行一次，内层循环重新开始并执行完毕。当最外层循环的循环条件为 FALSE 时，嵌套循环即告完成。

# 选择

做出决策的能力是编程所需的另一种基本属性。本节介绍的控制语句允许通过决策来修改程序的执行流程。

## if 语句

提供通用决策能力的编程结构之一是 if 语句。if 语句的格式如下：

```
if ( expression )
statement;
```

如果需要执行多条语句，可以使用花括号（{}）来表示 if 语句的主体。

```
if ( expression )
{
    statement_1;
    statement_2;
}
```

if 语句可以翻译为诸如“如果汽车价格是 100 美元，那么我会买它。”这样的语句。这可以写为：

```
if ( car == 100 )
    printf( "I’ll buy it!\n" );
```

printf() 函数仅在表达式求值为 TRUE 时执行。如果求值为 FALSE，则不采取任何操作。

## if...else 语句

if...else 语句允许在表达式求值为 TRUE 时执行一个操作，并在表达式求值为 FALSE 时执行另一个操作。该结构的语法如下：

```
if ( expression )
    statement;
else
    statement;
```

如果需要执行多条语句，可以使用花括号（ { } ）：

```
if ( expression )
{
    statement_1;
    statement_2;
}
else
{
    statement_1;
    statement_2;
}
```

if...else 语句的一个示例如下：

如果汽车价格在 100 美元或以下，我想买这辆汽车。如果汽车价格超过 100 美元，我想与卖家谈判。这可以表示为：

```
if ( car <= 100 )
    printf( "I'll take it!\n" );
else
    printf( "Let's talk about the price.\n" );
```

# 嵌套 if、if...else 和 else if 语句

嵌套的 *if* 和 *if...else* 语句可以通过将一个 *if* 或 *if...else* 语句放在另一个语句内部来构建。请务必正确管理语句的缩进。如果 *if* 的缩进与其对应的 *else* 不匹配，可能会造成混淆。以下是一个构建正确的示例：

```
if ( expression_1 )
{
    if ( expression_2 )
        statement_1;
}
else
{
    if ( expression_3 )
        statement_2;
}
```

只有当外层 *if...else* 语句中的 expression_1 及其嵌入的 *if* 语句中的 expression_2 求值为 TRUE 时，才会执行到 Statement_1。

当外层 *if* 语句中的 expression_1 求值为 FALSE，且外层 *else* 中嵌入的 *if* 语句中的 expression_3 求值为 TRUE 时，会执行到 Statement_2。

*else if* 语句有助于简化上述嵌套结构：

```
if ( expression_1 )
{
    if ( expression_2 )
        statement_1;
    else if ( expression_3 )
        statement_2;
}
```

else 及其嵌套的 if 语句合并在一行中。

### 逻辑运算符

迄今为止使用的 if 语句建立了两个值之间的简单关系测试。可以使用逻辑运算符创建复合关系测试，如本章前文“循环”部分中的“逻辑运算符”所述。一个示例如下：

```
if ( car <= 100 && car_year > 1992)
    printf ("I'll take it!\n");
```

当两个表达式都为 TRUE 时，汽车会被购买：汽车价格在 100 美元或以下，且汽车是 1992 年之后制造的。

### switch 语句

switch 语句是创建多分支结构时 if...else 语句的替代方案。其通用格式为：

```
switch ( expression )
{
   case value_1:
      statement;
      statement;
      . . .
      break;

   case value_2:
      statement;
      statement;
      . . .
      break;

   case value_n:
      statement;
      statement;
      . . .
      break;

default:
    statement;
    statement;
    ...
    break;
}
```

括号内的表达式将与 *value_1*、*value_2* 直至 *value_n* 进行比较，这些值必须是常量或常量表达式。如果找到与表达式值匹配的值，则执行与其关联的语句。如果未找到匹配项，控制流将转向 *default* 并执行其语句。

如果我愿意根据汽车制造年份支付车款，可以使用以下 switch 语句：

```
switch ( car_year )
{
    case 1999:
        printf("I'll offer you $8,000 for the car.\n");
        break;
    case 1998:
        printf("I'll offer you $6,000 for the car.\n");
        break;
    case 1997:
        printf("I'll offer you $3,500 for the car.\n");
        break;
    case 1996:
        printf("I'll offer you $2,100 for the car.\n");
        break;
    case 1995:
        printf("I'll offer you $1,000 for the car.\n");
        break;
    case 1994:
        printf("I'll offer you $800 for the car.\n");
        break;
    case 1993:
        printf("I'll offer you $400 for the car.\n");
        break;
    default:
        printf("No thank you, the car is too old.\n");
        break;
}
```

当找到匹配项时，与匹配项关联的语句会被执行。如果汽车年份早于 1993 年，则找不到匹配项，switch 语句将执行 default 分支。

# 函数

函数是 C 程序的基本构建模块。我们已经遇到过一些函数，例如用于向屏幕打印的 *printf()* 和从键盘读取数据到程序中的 *scanf()*。我们也知道每个 C 程序必须以一个名为 *main()* 的函数开始。

什么时候使用函数？如果操作已经作为函数创建并经过测试，请使用它。没有必要重新创建它。

什么时候创建函数？有几种情况。首先，如果一个操作在程序中的两个或更多地方被使用，它就有成为函数的候选资格。其次，如果一个操作在两个或更多程序之间被使用，应该创建函数。第三，如果一个操作产生单一结果，它可以成为函数。第四，如果一个操作是独立或独特的任务，即使只使用一次，它也应该是一个函数。第五，如果一个程序太长，为了提高可读性，应该将其分解为函数。

当在程序中使用函数时，首先定义然后调用函数。函数通过将其作为独立的源代码片段编写来定义，并通过在其他函数中引用其名称来调用。

许多有用的函数已经是随 C 编译器提供的标准库的一部分。你需要熟悉它们。它们会使编程更容易。

## 函数调用

调用函数的语法为：

```
function_name ( arg_1, arg_2, ... )
```
当一个函数（被调用函数）中包含的操作作为另一个函数（调用函数）操作的一部分被需要时，就会从调用函数中调用被调用函数。

要调用函数，需要使用函数的名称作为调用格式的一部分。函数名称使用与变量命名相同的规则。函数名称以字母开头，仅包含字母、数字或下划线。函数名称后的括号中包含参数。参数是对值的引用，这些值被传入函数以供使用。参数由逗号分隔，可以是常量、变量或表达式。如果函数不需要传入任何值，则可以省略参数。

一个函数通过引用函数名称并在括号中包含必要的参数来调用另一个函数。函数调用实现了两件事。首先，函数被执行。其次，一个值返回给调用函数。

## 定义函数

定义函数的语法为：

```
return_type function_name( parameter list )
{
    statement(s);
}
```

函数有四个要素：

- 1. 返回类型：因为函数可以返回一个值，所以必须指定该值的数据类型。如果函数不返回任何值，则使用数据类型 void。数据类型位于函数名称之前，作为类型声明。例如：

```
int price_service ( int service_type, float cost_per_service )
{
    /* Statements to calculate the price of a service */
}
```
