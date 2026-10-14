

变量可以包含字符串值（常见的文本字符，如字母、数字和特殊字符）或数值。单个变量在任何时候只能保存其中一种类型（因此，PHP 与一些强制你在程序开始时声明变量类型的编程语言不同）。

下面是一个简单的示例，演示在 PHP 中使用变量的不同数据类型：

```
<html>
<body>
<?php
$name = "Rich";
echo "<h2>Hello, $name, how are you?</h2>\n";
$name = "Joe Bob";
echo "<h2>Oh, so now your name is $name, huh?</h2>\n";
$name = 4.2;
$name = $name * 2;
echo "<h2>That's tricky, now the variable is equal to $name!</h2>\n";
?>
</body>
</html>
```

让我们仔细看看这里发生了什么。首先，程序将字符串值 "Rich" 分配给变量 $name：

```
$name = "Rich";
```

请注意，当你分配字符串时，必须用双引号将其括起来（以标记分配的字符串值的开始和结束）。

下一条语句通过回显包含该变量的 HTML 编码文本字符串来使用变量值：

```
echo "<h2>Hello, $name, how are you?</h2>\n";
```

与某些其他编程语言不同，PHP 允许你在 echo 语句中插入变量。它会根据数据类型自动确定如何显示变量值。

echo 语句末尾的 \n 字符是表示标准换行符的代码。换行符会强制光标在显示时开始新的一行。虽然不是绝对必要的，但它有助于在 HTML 代码中分隔输出行。

## 数组变量

数组允许你使用单个变量名将相似的值分组到一个列表中。然后你可以通过引用变量名来整体处理这些值，或通过引用其在数组列表中的位置来单独处理数组中的每个值。当你从 MySQL 数据库访问数据时，你需要使用数组。因此，尽早掌握它们很有帮助。

PHP 根据单个数据记录将数据库结果分组到数组中。当你查询数据库时，PHP 会将返回的数据推送到一个数组中。然后你必须从数组中提取单个数据元素，以便在网页的适当位置显示它们。

你可以在使用 array() 函数的普通赋值语句中定义数组变量。array() 函数创建的值列表而不是单个值：

```
$family = array("Rich", "Barbara", "Katie", "Jessica");
```

此赋值语句创建了一个字符串值的数组。你必须列出数组中的每个元素并用逗号分隔。虽然此示例对数组中的元素使用了字符串值，但你也可以使用数字。

PHP 使用位置编号引用数组中的每个元素。数组中的第一个元素是元素 0，第二个是元素 1，以此类推。因此，例如，在上面的赋值语句中，Rich = 0，Barbara = 1，Katie = 2，Jessica = 3。（PHP 数组始终从数字 0 开始计数数组元素。）

要引用数组中的单个元素，你将所需的元素编号（用方括号括起来）添加到变量名：

```
<html>
<body>
<?php
$family = array("Rich", "Barbara", "Katie", "Jessica");
echo "The first person is $family[0]<br>";
echo "The last person is $family[3]<br>";
?>
</body>
</html>
```

PHP 提供了 count() 函数来确定数组中有多少个元素：

```
$count = count($family);
```

这让你知道需要遍历数组多少次才能检索所有数据元素。

## 关联数组变量

PHP 还支持关联数组（有时也称为哈希），它将数组值与文本键关联起来。看一下这个例子：

```
$favorite = array("fruit" => "banana", "vegetable" => "carrot");
```

数组定义将键值 fruit 分配给数据值 banana，并将键值 vegetable 分配给数据值 carrot。现在，如果你使用其中一个键值引用数组，PHP 会自动检索数据值。这条代码语句：

```
echo "My favorite fruit is a {$favorite['fruit']}";
```

