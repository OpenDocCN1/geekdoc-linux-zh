

## 使用字符串

Visual Basic .NET 包含许多可用于操作字符串数据的方法。你使用这些命令执行诸如将字符串切分为片段、获取字符串长度以及搜索子字符串等操作。

String 类的 Length 方法可让你确定字符串的长度。Length 不接受参数，并返回一个 Integer，表示字符串中字符的数量，包括空格和任何其他特殊字符。

PadLeft 会取其字符串的内容并使用空格将字符串右对齐到作为方法参数指定的长度。例如，如果 x = "dog" 且你调用 x.PadLeft(5)，该方法会在单词前面返回两个空格。PadRight 具有相同的功能，只是在单词右侧添加空格。

你可以使用 Insert 方法在特定位置插入字符串。该方法的格式为 Insert(startPosition, stringToInsert)。例如，如果 a = "John is a boy" 且 b = "bad"，则 a.Insert(10, b) 返回 "John is a bad boy"。

你可以使用 Remove 从字符串中删除已知长度的字符。该方法的格式为 Remove(startPosition, length)。在前面的示例中，假设 Insert 命令保存到字符串 c，c.Remove(10, 4) 会删除子字符串。

ToUpper 和 ToLower 分别将字符串转换为大写和小写字符串。它们不接受参数。

String 类中可用的方法不会更改类所代表的字符串；相反，每个方法都会返回一个新字符串。例如，要将 ToLower 返回的小写字符串保存回调用该方法的字符串中，可以使用此行：a = a.ToLower()。

![](img/d6f772854306e15fb6df39b861a7b541_109_0.png)

- 1 创建一个新项目或打开现有项目。
- 2 打开要进行字符串操作的[content]

## 使用字符串

Visual Basic .NET 包含许多可用于操作字符串数据的方法。你使用这些命令执行诸如将字符串切分为片段、获取字符串长度以及搜索子字符串等操作。

String 类的 Length 方法可让你确定字符串的长度。Length 不接受参数，并返回一个 Integer，表示字符串中字符的数量，包括空格和任何其他特殊字符。

PadLeft 会取其字符串的内容并使用空格将字符串右对齐到作为方法参数指定的长度。例如，如果 x = "dog" 且你调用 x.PadLeft(5)，该方法会在单词前面返回两个空格。PadRight 具有相同的功能，只是在单词右侧添加空格。

你可以使用 Insert 方法在特定位置插入字符串。该方法的格式为 Insert(startPosition, stringToInsert)。例如，如果 a = "John is a boy" 且 b = "bad"，则 a.Insert(10, b) 返回 "John is a bad boy"。

你可以使用 Remove 从字符串中删除已知长度的字符。该方法的格式为 Remove(startPosition, length)。在前面的示例中，假设 Insert 命令保存到字符串 c，c.Remove(10, 4) 会删除子字符串。

ToUpper 和 ToLower 分别将字符串转换为大写和小写字符串。它们不接受参数。

String 类中可用的方法不会更改类所代表的字符串；相反，每个方法都会返回一个新字符串。例如，要将 ToLower 返回的小写字符串保存回调用该方法的字符串中，可以使用此行：a = a.ToLower()。

![](img/d6f772854306e15fb6df39b861a7b541_109_0.png)

- 1 创建一个新项目或打开现有项目。
- 2 打开要进行字符串操作的代码模块。
- 3 声明一个字符串并设置其内容。
- 4 声明一个字符串用于存储操作后的字符串。

注意：有关字符串的更多信息，请参阅“Create a String”部分。

## 应用它

Join & Split 方法是 String 类的一部分，可分别让你连接字符串数组或将其拆分。你可以使用这些方法轻松地将一组信息存储在单个字符串中，并在必要时将其拆分。有关创建和使用数组的更多信息，请参阅本章后面的“Create an Array”。要合并字符串数组，请将用作分隔符的字符串和字符串数组传递给 String.Join 方法。你在数组中相邻的每个项目之间放置一个分隔符。常用的字符串是逗号后跟空格。要将一组单词合并为一个句子，只需使用空格作为分隔符即可。Split 函数拆分字符串并返回字符串数组。将字符串后跟分隔符传递给 Split 函数。如果未传递分隔符，Split 使用空格。

```
Dim words() As String = {"The", "car", "is", "going", "fast."}
Dim sentence As String
sentence = String.Join(" ", words)
Console.WriteLine(sentence)
Dim splitSentence() As String = Split(sentence, " ")
Dim word As String
For Each word In splitSentence
Console.Write(word & " ")
Next
```

The car is going fast.
The car/is/going/fast./

![](img/d6f772854306e15fb6df39b861a7b541_110_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_110_1.png)

- 5 在新的一行，输入 myStringChanges = myString.Insert(14, "TONS OF ")，将 myString 替换为要操作的字符串的名称，Insert 替换为操作方法，并将 14、"TONS OF " 替换为适当的 arguments。
- 6 输入代码以使用操作后的字符串。
- 7 按 F5 运行你的项目。

String 类更改字符串数据，你的程序使用这些更改。

## 通过方法传递信息

许多方法需要外部数据才能运行，并且必须能够将数据发送回调用方。你可以使用 arguments 创建一个通道，将任何类型的变量传递给方法。返回值可让你将变量传回调用该方法的代码。

要定义方法接受的参数列表，你在方法名称后的括号内括起变量名列表。当你放置参数时，你在参数的变量名前放置 ByVal 或 ByRef 关键字，并使用 As 关键字在参数后指定参数的变量类型。指定 ByVal 以传递变量的值，并指定 ByRef 以传递原始变量的内存位置。如果未指定参数传递方法，VB.NET 会自动添加 ByVal。

通过用逗号分隔列出多个参数。你使用在参数列表中分配的变量名

作为方法的局部变量，因此你必须使用与方法中局部变量不同的名称。

要将值返回给调用方法的代码，请使用 Function 关键字定义方法而不是 Sub。使用 Function 关键字时，你必须指定函数返回的变量或对象的类型。有关创建和调用方法的更多信息，请参阅“Add a Method”部分。

要设置要返回的信息，请使用 Return 关键字。在关键字后放置返回的变量或对象。确保变量与方法头中指定的类型匹配。

对于返回值的函数，请在其他代码中将该方法用作变量名，或将其分配给变量，例如 test = TestNumber(number)。

![](img/d6f772854306e15fb6df39b861a7b541_111_0.png)

### 传递参数

- 1. 打开方法的类或模块
- 2. 创建一个新方法或使用现有方法。
- 3. 单击括号之间。

注意：要创建方法，请参阅“Add a Method”部分。

- 4. 输入 ByVal number1 As Integer 将 number1 替换为参数的变量名，并将 Integer 替换为变量的类型。你可以根据需要重复步骤 4，用逗号分隔每个参数。
- 5. 编辑方法代码以使用参数。
- 6. 要调用方法，请输入 Add(5, 10)，将 Add 替换为你的方法名称，并将 5、10 替换为与参数列表匹配的值。

