
图 14-2（续）

当发现两个位置错误的元素时，它们会被交换。当左右指针相遇时，每个部分都会被传回`quicksort`函数。

## 内置排序函数

通常不需要自己编写排序函数。PHP 提供了几个排序函数。最基础的是`sort`。

`sort`函数将数组中的所有元素从低到高排序。如果数组包含字符串，这意味着按照 ASCII 码进行排序。如果数组只包含数字，则按它们值进行排序。

注意一点，尽管我使用一些数字来索引数组，但在`sort`之后，所有元素都被标记为零到四。这是图 14–3 展示的一个重要效果。

另一个值得注意的是输出顺序：Apple, Blueberry, Watermelon, apple。字典可能会将 "apple" 列在 "Apple" 之前，但 "A" 的 ASCII 码是 65。"a" 的 ASCII 码是 97。附录 B 列出了所有 ASCII 码。如果你想要不区分大小的排序，请查看自定义比较函数的章节（第440页）。

`sort`函数与`sort`完全相同，只是它以相反的方向排序元素。尝试将图 14–3 中的代码`sort`改为`rsort`。

其他排序函数`asort`和`ksort`工作方式略不同。它们保留了索引和元素之间的关系。

图 14-3 使用`sort`函数

```php
<?php
/*
用随机值填充 fruit 数组 */
$fruit[1] = "Apple";
$fruit[13] = "apple";
$fruit[64] = "Blueberry";
$fruit[0] = "pear";
$fruit["last"] = "Watermelon";
sort($fruit);
for($index = 0; $index < count($fruit); $index++)
{
    print($fruit[$index] . "<BR>\n");
}
?>
```

图 14-3 继续

当你有一个关联数组时，这非常有用。如果数组是由数字索引的，你可能不想保留它们的索引。另一方面，如果你这样做呢？图 14–4 阐释了这一点。这里我使用了`reset`将数组指针放在第一个元素上。然后使用`next`函数获取后续的每个元素。这里的顺序是

## 图 14-4 使用 as 函数

```php
<? 
/*
** 按照偏好顺序填充数组
*/
$pasta = array("ravioli",
  "spaghetti",
  "vermicelli",
  "lasagna",
  "gnocchi",
  "rigatoni");
```
```php
/*
** 对数组进行排序，保留索引
*/
asort($pasta);
```
```php
/*
** 按字母顺序打印数组
*/
for($name = reset($pasta); $name; $name = next($pasta))
{
  $rank = key($name);
  print($name);
  print(" was ranked number ");
  print($rank);
  print("<BR>\n");
}
?>
```

**图 14–4**（续）

元素存在于内存中，但它们保留了原始索引，这些索引是在元素添加到数组时使用的从零开始的数字。

如果我用的是`rsort`，顺序将完全相反。图 14–5 可能是这些函数更典型的用法。保留`getdate`返回的数组中的元素与其索引关联是非常重要的。图 14-5 按元素值反序对数组进行排序。这可能没有特别有用，但说明了该用法。

在本节中，我想要讨论的最后一个排序函数是`ksort`。该函数根据索引的值对数组进行排序。我修改了图 14–6 中的代码，用`ksort`代替`asort`。注意，现在所有元素都按照它们的索引（或键）顺序排列。

## 图 14-5 - Netscape

![](img/490647a2fc8fbc7034b6e56593c58845_462_0.png)

```php
/*
** 从 getdate 获取数组
*/
$today = getdate();
/*
** 反序排序数组，保留索引
 */
arsort($today);
/*
** 打印数组
*/
for($value = reset($today); $value;
    $value = next($today);
{
    print(key($today));
    print(" is ");
    print($value);
    print("<BR\n");
}
?>
```

**图 14–5** 使用`arsort`函数

`ksort`函数可能在您拥有关联数组且无法对内容进行完全控制的情况下最有用。在图 14–6 中，脚本获取了由`getdate`函数生成的数组。如果你在注释掉`ksort`那行的情况下运行它，你会发现顺序是随机的。它仅仅是编写函数代码时选择的顺序。你可能为每个元素输入了数行代码，因为第 11 章中对函数的描述列出了返回数组中的所有元素。一个更具可读性的解决方案是按键排序并在循环中打印每个元素。

## 使用比较函数进行排序

在大多数情况下，内置排序函数都是合适的。如果你的问题需要比内置函数使用的排序性能更好的排序，那么你就面临编写自己的代码了。如果你的问题是需要比较复杂元素（如对象或多维数组），解决方案是编写一个比较函数并将其插入`usort`函数中。

`usort`允许你使用自定义比较函数对数组进行排序。你的比较函数必须接受两个值并返回一个整数。对两个参数进行比较，如果返回负数，则认为这些值是有序的；如果返回零，则认为它们是相等的；正数表示这些数字（*此处原文缺失/未完*）。

图 14–6 使用`ksort`函数

![](img/490647a2fc8fbc7034b6e56593c58845_463_0.png)

```php
<?php
/*
** 从 getdate 获取数组
 */
$today = getdate();
/*
** 按键排序数组
 */
ksort($today);
/*
** 打印数组
*/
for($value = reset($today); $value; 
$value = next($today)) 
{
    print($today);
    print(" is is ");
    print($value);
    print("<BR\n");
}
?>
```

**图 14-6**（续）

在图 14-7 中，我创建了一个包含三个元素的多维数组：姓名（name）、职位（title）和工资（wage）。有时我想按姓名列出员工，但其他时候我可能想按职位或每小时薪水列出他们。为了解决这个问题，我写了三个比较函数。`ByByName`函数是`strcmp`的简单封装。姓名将按 ASCII 码排序。`ByTitle`函数为每个职位分配一个整数值，然后返回这些整数的比较结果。`BySalary`函数比较工资元素，但如果两个员工的每小时薪水相同，则比较他们的姓名。

## 搜索

排序将信息组织成一种形式，这种形式有助于找到我们正在查找的确切部分。如果你需要查找电话号码，很容易翻阅页面直到找到大致的区域。只需进行一点扫描——

## 图 14-7 - Netscape

| 未排序 | Smith, John (Programmer) 20.00/Hour |
| | Doe, Jane (Programmer) 20.00/Hour |
| | Mann, Joe (Manager) 35.00/Hour |

*(注：由于原文文本在此处出现大量逻辑重复和混乱，后续搜索章节已根据上下文逻辑整合翻译)*

```php
usort($employee, "byName");
/*
** 选取目标
*/
$Name = "Doe, Jane";
$lower_limit = 0;
$upper_limit = count($employee) - 1;
while($lower_limit < $upper_limit) {
  /*
  ** 选取中间点
  */
  $index = intval(($lower_limit + $upper_limit)/2);
  if (strcmp($employee[$index][1], $Name) > 0) {
    /*
    ** 目标在上半部分
    */
    $lower_limit = $index + 1;
  } elseif (strcmp($employee[$index][1], $Name) < 0) {
    /*
    ** 目标在下半部分
    */
    $upper_limit = $index - 1;
  } else {
    /*
    ** 找到目标
    */
    $lower_limit = $index;
    $upper_limit = $index;
  }
}
/*
** 打印结果
*/
print("Position $index<BR>\n");
```

**图 14-8**（续）

当然，数据库为数据管理提供了更强大的解决方案。在大多数情况下，依赖数据库来存储大量数据是最好的，因为它们拥有专门用于搜索和排序的代码。数据库将在第 16 章中讨论。

## 随机数

随机数的生成与排序和搜索紧密相关。随机数通常被用于让列表乱序。它们提供了创造惊喜的机会。通过为每个请求随机选择内容，你可以在单个页面上挤更多的信息。你每天在 Web 上都能看到，例如每日名言、横幅广告和会话标识。

PHP 提供了`rand`函数来生成随机数。在使用它之前，你必须为生成器种子。`rand`函数接受一个整数，用于生成第一个随机数。种子值会反复生成相同的数字序列。真相大白了！计算机等确定性设备是不可能产生真正的随机数的。相反，正确的公式可以产生模式长度足够的数字，使其看起来是随机的。这些被称为伪随机数。`rand`生成的伪随机数对于大多数应用来说足够随机了。

```php
<?
/**
** 为随机数生成器种子
 */
srand(time());
/**
** 获取 1 到 100 的十个随机数
 */
for($index = 0; $index < 10; $index++) {
    $number = (rand()%100)+1;
    print("$number<BR>\n");
}
?>
```

**图 14-9** 获取随机数

![](img/490647a2fc8fbc7034b6e56593c58845_471_0.png)

图 14-10 随机数函数

```php
/*
 ** 返回一个随机数
 */
function RandomNumber($new_seed="")
{
    static $seed;
    $constant = bcadd(bcpow("2", "13"), "1");
    $prime = 37;
    $max_value = bcpow("2", "50", $scale);
    /*
 ** 如果提供了新种子，则使用它
 * */
    if($new_seed != "") {
        $seed = $new_seed;
    }
    /*
 ** 如果没有种子，使用时间戳
 * */
    if($seed == "") {
        $seed = strval(time());
    }
    /*
 ** 获取下一个值
 * */
    $seed = bcmul($constant, $seed);
    $seed = bcadd($seed, $prime);
    $seed = bcmod($seed, $max_value);
    return($seed);
}
/*
 ** 设置 BC Math 函数仅使用整数
 * */
bcscale(0);
/* */
 ** 获取 100 个数字
 * */
for($index = 0; $index < 100; $index++) {
    print(RandomNumber() . "<BR>\n");
}
?>
```

**图 14-10**（续）

```php
<?
/*
 ** 生成会话 ID
 */
function SessionID($length=16)
{
    /*
     ** 设置可能的字符池
     */
    $Pool = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    $Pool .= "abcdefghijklmnopqrstuvwxyz";
    for($index = 0; $index < $length; $index++) {
        $sid .= substr($Pool, (rand()%strlen($Pool)), 1);
    }
    return($sid);
}
/*
 ** 为生成器种子
 */
srand(time());
if($sid != "") {
    print("Old Session ID was $sid<BR>\n");
}
$sid = SessionID();
print("<A href=\"14-11.php?sid=$sid\">");
print("Get Another Session ID ID");
print("</A>\n");
?>
```
