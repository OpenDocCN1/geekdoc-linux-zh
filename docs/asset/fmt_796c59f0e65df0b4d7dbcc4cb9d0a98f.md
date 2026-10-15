
| 表 2.1 数字条件的符号 |
| 符号 | 含义 | 示例 |
| :--- | :--- | :--- |
| > | 大于 | if ( `variable` > `value` ) |
| < | 小于 | if ( `variable` < `value` ) |
| >= | 大于等于 | if ( `variable` >= `value` ) |
| <= | 小于等于 | if ( `variable` <= `value` ) |
| == | 等于 | if ( `variable` == `value` ) |
| != | 不等于 | if ( `variable` != `value` ) |
| 表 2.1 续 |
| 符号 | 含义 | 示例 |
| :--- | :--- | :--- |
| && | 与 | if( `condition` && `condition` ) |
| || | 或 | if( `condition` || `condition` ) |
| ! | 非 | if( `condition` ) 等同于 if( `condition` == false ) |

### 字符

使用代表字符的变量创建的条件遵循与数字相同的规则。这是因为正如我们在第 1 章中讨论过的（参见“C 编译器”，第 18 页），计算机并不理解字母 A。字母是以计算机理解的数字方式来表示的。

字母 *A*（如表 1.2 所示）在编译成机器语言时与数字 65 相同，使得用于数字的相同约定可以应用于构建测试条件的字符。

为了说明这一点，考虑以下条件：

```c
if( character > 'A' )
```

或者

```c
if( character < 'Z' )
```

或者

```c
if( character > 'A' && character < 'Z' )
```

> 将字符像数字一样处理需要你了解语言放置它们的正确顺序。这确保了条件的语义符合预期。

由于字母 A 是十进制的 65，Z 是 65+25 或 90，因为字母 Z 距离字母 A 25 个位置。但 a 到 z 位于哪里呢？是小于还是大于 A？此外，还有哪些不是字母的可打印字符，例如标点符号？标准 ASCII 定义了字符的数字表示以便计算机处理。

要查看完整的 ASCII 字符表以及所有打印（和不可打印）字符的位置，请使用 `man` 命令：

```bash
man ascii
```

图 2.2 显示了 ASCII 表 man 手页的一部分。

## 探究

## 绝对零度

### ASCII（美国信息交换标准代码）

ASCII 是计算机和互联网上常见的文本文件格式。

在 ASCII 文件中，每个字母、数字或特殊字符都用 7 位二进制数（七个零或 1 的字符串）表示。ASCII 定义了 128 个可能的字符。

基于 UNIX 和 DOS 的操作系统（Windows NT 除外）使用 ASCII 处理文本文件。Windows NT 使用较新的代码 Unicode。IBM 的 System 390 服务器使用一种名为 EBCDIC 的专用位代码。

转换程序允许不同的操作系统将文件从一种转换为另一种。美国国家标准协会 (ANSI) 开发了 ASCII。

> ASCII 一词的读音类似于字母 ask-ee。

图 2.2 ASCII 表 man ascii。

### 字符串

字符串与字符的区别在于它们是字符的组合。尽管这看起来显而易见，但处理字符串需要一套全新的启发式方法。

ASCII 表不适用于字符组。如果测试条件考虑的是组成字符串的单个字符，那么应用你所学的内容是可以。然而，当将字符组作为一个整体进行评估时，你必须使用其他方法。

```
FIG = 70 + 73 + 71 = 214
SAB = 83 + 65 + 66 = 214
```

## if else 语句

到目前为止，我们只考虑了真 (if) 和假 (else)。如果正在测试的条件有很多值呢？例如，如果用户从 a 中选择了一个选项呢？

为了测试所有输入，你可以使用一系列 if 语句：

```c
if( input == '1' )
   action
if( input == '2' )
   action
if( input == '3' )
   action
if( input == '4' )
   action
if( input == '5' )
   action
```

然而，这种方法的缺点不仅在于性能，还涉及到用户漏掉数字时缺乏默认处理。简单地在列表中添加一个 else：

```c
if( input == '1' )
   action
if( input == '2' )
   action
if( input == '3' )
   action
if( input == '4' )
   action
if( input == '5' )
   action
```

这种做法是的，因为不仅当用户输入无效内容时执行错误操作，当他输入除5以外的任何有效响应时也会执行。这当然忽略了无论输入如何都会评估每个语句的事实。

使用 if 语句解决了这两个问题：

```c
if( input == '1' )
    open action
else if( input == '2' )
    close action
else if( input == '3' )
    delete action
else if( input == '4' )
    rename action
else if( input == '5' )
    print action
else
    error action
```

评估结果为真后，不再考虑其他的 if 语句。此外，只有在没有找到输入匹配时，才会执行错误操作。

注意在 if else 示例中，if 语句的放置与使用 else 语句的规则相似。第一个 if else 之前必须有一个语句，并紧跟与 if 相关的动作。在第一个 if 之后，后续的 if else 语句可以紧跟在前一个 if 动作之后的链中。

if 语句总是启动一个新链并必须是第一个。if 语句结束链；因此，它必须是 if、if else 语句系列中的最后一个语句。

## case 语句

另一种解决图 2.3 所示输入评估的方法是采用 case 语句。case 语句为这类问题提供了比 if else 更优雅且灵活的替代方案。

case 语句的操作原理是根据数值或字符变量的值，对你想要考虑的每个条件进行切换：

```
switch( input ) {
  case '1':
    open action
    break
  case '2':
    close action
    break
  case '3':
    delete action
    break
  case '4':
    rename action
    break
  case '5':
    print action
    break
  default:
    error action
}
```

在 switch 语句的每个条件中，case 语句相当于该条件的入口点，而 break 定义了退出结构的位置。这种方式提供的灵活性在于，case 语句可以分组以共享操作。

> 注意，示例正变得越来越接近 C 编程语言的语法。switch 语句要求主体的开始和结束标记显示在以下内容中值入口点的开始和结束位置：

```
switch( var ) {
  case 1:
    break;
  case 2:
    break;
}
```

在 C 语言中，大括号（`}` 和 `}`）用于标记代码体的开始和结束。我们将在第 3 章看到更多内容。

再次考虑解决菜单问题的 if else 方案。如果你决定接受 1、0 或 o 作为调用 `open` 操作的输入值，你将不得不把 `if ( input == '1')` 的测试扩展为明显更复杂的条件。

## 绝对零度

case 语句的灵活性只需要我们为新输入添加一个条件（入口点）：

```
case 'o':
case 'O':
case i:
  open action
  break
```

case 语句提供了一个清晰、简洁且易于维护的决策结构。

在离开 case 语句之前，请注意前几个示例中的 `default` 条件。正如预期的那样，这是在未找到匹配项时执行的 case。

## 循环

无论你是在尝试寻找某项的匹配项、统计数据库中的客户数量，还是无尽地显示菜单，在计算机程序中，多次执行通常是必要的。一种使重复成为可能的结构是循环。共有四种执行循环的方法，当然，选择哪一种取决于所解决的问题。

### for 循环

面对必须在固定长度的数组中查找空位的问题，你应该立即考虑 `for` 循环。

> 数组并不住在海洋中

数组被看作是一种档案柜的存储机制。档案柜在创建时具有固定数量的抽屉。数组的每个抽屉都是一个称为“元素”的存储位置，元素的数量组数组的长度。就像柜子里的抽屉一样，数组中的元素数量在创建后无法更改。数组的索引始终从零开始：`array[0]` 是第一个元素。因此，如果数组有四个元素，`array[0]` 是第一个，`array[3]` 是最后一个。
