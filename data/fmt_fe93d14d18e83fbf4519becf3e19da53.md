
## 程序流控制

一个良好的程序不仅要存储数据，还要以高效的方式使用数据。在应用程序中设计良好的执行流是创建更小、更有组织且更易于维护的代码的关键。本节描述了程序流的一些元素并演示了它们的用法。

## 决策结构

应用程序使用决策结构在执行过程中进行逻辑选择。程序经常需要用户输入或预先未知的特定值来选择执行路径。程序员编写代码来处理每种情况（除非他们非常聪明，如果是那样，他们将编写能够成功且准确处理多种情况的通用代码）。

## If 语句

编程中最常用的结构是 `if` 语句。`if` 语句可以短简单，也可以长复杂，并且有无限种形式。它根据布尔表达式的值选择执行路径。`if` 语句的基本结构是：

```
if <conditional expression> then

  <statement>

else

  <statement>;
```

正如我们已经提到的，Pascal 不关心换行符或空格。我们可以随心所欲地格式化 语句，某些开发者将 `then` 放在第二行并与其语句一起，或者简单地将 `else` 放在任何位置。

注意第一个 `<statement>` 后面没有分号。`if` 语句是 Pascal 中少数可以在语句末尾不加分号的地方之一。这是因为编译器将整个结构视为一个语句。Pascal 像 Visual Basic 那样有 `endif`。它依赖于语句块的分号是不计数的！你可以看到语句可以非常简单。上面的结构并不是 `if` 语句的最简单形式。`else` 子句完全是可选的。

```
if (UserCount > 10) then

ShowMessage('Too many users');
```

相反，`if` 语句可以非常复杂，如下：

```
if(UserGender = 'male') then

UserGreeting := 'Hello, Mr. ' + UserName

else

  if(UserStatus = 'Single') then

    UserGreeting := 'Hello, Ms. ' + UserName

  else

    if(UserStatus = 'Divorced') then

      UserGreeting := 'Hello, Mrs. ' + UserName

    else

      UserGreeting := 'Hello, ' + UserName
```

在这个示例中，`else` 子句使用了它的语句。尽管第二个语句本身带有 `else`，但编译器仍然将其视为仅仅一个语句。悬空 `else`（注：此处原文为 "Dangling" 且 "itself" 与 "by its own" 处逻辑可能有翻译语境差异）

有时需要一个编译器无法通过自身解释的 `if` 语句。考虑以下情况：

```
var
  FirstName,
LastName,
FullName:String;
```

```
begin
  if (FirstName <> '') then
    if (LastName <> '') then
      FullName := FirstName + LastName;
  else ShowMessage('You must enter your name');
```

在这种情况下，`if` 语句的 `else` 子句属于谁？根据其格式化方式，`else` 子句看起来属于第一个语句。Pascal 不关心空格，但编译器会假设由于 `else` 子句紧跟在第二个后面，它们属于同一个。这种情况的逻辑要求第一个语句有一个 `else` 子句。

通常建议的解决方案是在第二个语句末尾放置分号。这将导致编译错误。因为 Pascal 没有 `else` 的终止标记（如 Basic 的 `ENDIF`），编译器解释从第一个开始到第一个分号的整个语句。在第二个语句后放置分号会让编译器认为下一个语句以 `else` 开始（这是非法的）。解决问题的办法是在第一个语句中添加 `begin/end` 对来包含第二个语句。现在 `else` 被放置在语句内部，编译器将该块视为单个语句（某种），并将 `else` 子句分配给逻辑层级相同的语句。

```
if (FirstName <> '') then
begin
  if (LastName <> '') then
    FullName := FirstName + LastName;
end
else ShowMessage('You must enter your full name');
```

## Case 语句

在应用程序中另一种决策的方法是使用 `case` 语句。`case` 语句将值与一组互斥的“情况”进行比较。如果该值落在某个情况列表中，则执行该情况的对应的语句或语句块。`case` 语句的格式如下：

```
case <expression> of
  <value list> : <statement(s)>;
  <value list> : <statement(s)>;
  else <statement(s)>;
```

### Kylix 2 开发

# 第 5 章：Object Pascal

# 101

`case` 语句的值列表可以包含任何序数类型（整数、布尔值、用户定义类型等）。它不能包含无序性质的元素，例如字符串和浮点数。

`else` 子句允许在未找到合适 `case` 的情况下声明默认情况。请注意，与 C++ 和 Java 中的 `switch` 语句不同，`case` 语句在 `case` 之间不需要 `break`。当某个特定 `case` 的语句执行完毕，执行流将跳转到 `case` 语句之后的第一行代码。

![](img/d784fa8294cae585d61ec86b987ea212_115_0.png)

> 提示：当使用 `case` 语句来区分一组组件时，如果没有其他区分特征，通常会使用 `tag` 属性（当然，不能使用名称，因为它是字符串）。`tag` 属性定义在 `TComponent` 类中，并供开发者在认为合适的地方使用。每当使用 `tag` 属性区分组件时，使用注释尤为重要，以提醒团队成员该 `case` 语句的特殊用途。

```pascal
case tbtmMainToggleButton.Tag of
0 : DataTable.First; // 移动到第一记录
1 : DataTable.Prior; // 移动到上一记录
2 : DataTable.Next; // 移动到下一记录
3 : DataTable.Last; // 移动到最后记录
end; // case 语句
```

## With 语句

默认情况下，每当直接引用对象属性或方法（而没有显式引用对象）时，都会对 `Self` 进行隐式引用。`Self` 指你正在操作的对象。例如，在下面的代码中，表单类方法由表单本身调用。这实际上意味着 `Self`。由于我们正在使用 `TrmMain` 类的 `btnClose` 方法，因此 `Self` 指向 `TrmMain`。

```pascal
procedure TrmMain.btnClose(Sender: TObject);
begin
  Close; // 实际上引用 TrmMain.Close 或 Self.Close
end;
```

`with` 语句临时重定向 `Self` 指特定对象或代码块的方法。它允许开发者引用对象的多个属性和方法，而无需每次都显式命名对象。

```pascal
with Self,ListBoxCustomer do
begin
  // 引用 Self（表单）
  Caption := 'Searching';
  WindowState := wsMaximized;
```

![](img/d784fa8294cae585d61ec86b987ea212_115_1.png)

```pascal
// 引用列表框
MultiSelect := True;
Items.add('Customer Name');
Items.add('Customer ID');
```

```pascal
// 引用上一个项目（列表框）
Color := cBlack;
Font.Color := cWhite;
end;
```
