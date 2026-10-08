
```php
<?
// 连接
$sybase = sybase_connect();

// 使用存储数据库
$sybase_dbuse("store", $sybase);

// 获取所有项目
$result = sybase_query("SELECT * FROM item ");

// 查找返回的行数
$nrows = sybase_numrows();
print("<TABLE BORDER=1\n");

// 数据行
while($row = sybase_fetch_row($result)) {
    print("<TR>\n");

    for($index = 0; $index < $fields; $index++) {
        print("<TD\n");
        print($row[$index]);
        print("</TD>\n");
    }

    print("<TR>\n");
}
print("</TABLE>\n");

sybase_close($sybase);
?>
```

## 相关函数

`sybase_fetch_array`, `sybase_fetch_row`

### object sybase_fetch_field(integer result, integer field)

`sybase_fetch_field` 函数返回一个描述结果集中字段的对象。`field` 参数是可选的。如果省略，则返回后续字段。该对象包含了图 13–10 中描述的属性。

## 示例

参见 `sybase_result` 示例。

## 相关函数

### object sybase_fetch_object(integer result)

`sybase_fetch_object` 函数返回一个包含下一行每个字段属性的对象。每次调用 `sybase_fetch_object` 都会获取结果集中的下一行，如果没有剩余行，则返回 false。

## 示例

```php
<?
// 连接
$sybase = sybase_connect();

// 使用存储数据库
$sybase_dbuse("store", $sybase);

// 获取所有项目
$result = sybase_query("SELECT * FROM item ");

// 查找返回的行数
$nrows = sybase_numrows();

print("<TABLE ORDER=\"1\">\n");

// 数据行
while($row = sybase_fetch_object($result))
{
    print("<TR>\n");
    print("<TD>\n");
    print($row->name);
    print("</TD>\n");

    print("<TD>\n");
    print($row->Price);
    print("</TD>\n");

    print("<TR>\n");
}

print("</TABLE>\n");

sybase_close($sybase);
?>
```

```php
}
print("</TR>\n");
print("</TABLE>\n");
sybase_free_result($result);
sybase_close($sybase);
?>
```

## 相关函数

`sybase_fetch_array`, `sybase_fetch_object`, `sybase_fetch_row`

### boolean sybase_select_db(string database, integer connection)

`sybase_select_db` 函数用于选择在数据库服务器上使用的数据库。如果省略 `connection` 参数，将使用最后创建的连接。

## 示例

请参考 `sybase_result` 示例。

## 相关函数

无

## Velocis

Raima 的 Velocis 是数据库领域的新生力量，但 Raima 并如此。自 1982 年以来，他们一直提供流行的数据库软件。Velocis 的重点在于速度和灵活性。它将 SQL 前端与更快的基于指针的后端结合。它适用于所有主要的 UNIX 版本以及 Windows NT。更多信息可以在 <http://www.raima.com/products/vlds.cfm> 处查得。

### boolean velocis_autocommit(integer connection)

`velocis_autocommit` 函数导致给定连接的每个查询都自动提交。

## 示例

```php
<?php velocis_autocommit($connection);?>
```

## 相关函数

`velocis_off_autocommit`

### boolean velocis_close(integer connection)

使用 `velocis_close` 关闭与数据库的连接。

## 示例

请参考 `velocis_exec` 示例。

## 相关函数

`velocis_connect`

### boolean velocis_commit(integer connection)

`velocis_commit` 函数提交给定连接上的所有事务。

## 示例

```php
<?php velocis_commit($connection);?>
```

## 相关函数

`velocis_rollback`

### integer velocis_connect(string server, string user, string password)

`velocis_connect` 函数返回指向给定服务器的连接标识符。必须提供 `user` 和 `password` 参数。

## 示例

请参考 `velocis_exec` 示例。

## 相关函数

`velocis_close`

### integer velocis_exec(integer connection, string query)

`velocis_exec` 函数在数据库连接上执行查询。返回一个结果标识符。

## 示例

```php
// // 连接到数据库
$connection = velocis_connect("localhost", "leon", "secret");

// 执行查询
$query = "SELECT * FROM item ";
$result = velocis_exec($connection, $query);

// 获取字段数量
$fields = velocis_fieldnum($result);
print("<TABLE BORDER=\"\n");
```

```php
// 创建表头行
print("<TR\n");
for($index = 0; $index < $fields; $index++) {
    print("<TH\n");
    print(velocis_fieldname($result, $index));
    print("</TH\n");
}
print("</TR\n");
```

```php
while(velocis_fetch($result)) {
    print("<TR\n");
    for($index = 0; $index < $fields; $index++) {
    print("<TD\n");
    print(velocis_result($result, $index));
    print("</TD\n");
    }
    print("</TR\n");
}
print("</TABLE\n");
```

```php
// 释放结果
velocis_freeresult($result);
```

```php
// 关闭连接
velocis_close($connection);
```

## 相关函数

`velocis_result`

### boolean velocis_fetch(integer result)

使用 `velocis_fetch` 将结果集中的下一行获取到内存中。在下次调用 `velocis_fetch` 之前，`velocis_result` 将始终返回此行的值。如果集合中没有剩余行，则返回 false。

## 示例

请参考 `velocis_exec` 示例。

## 相关函数

无

```php
string velocis_fieldname(integer result, integer field)
```

使用 `velocis_fieldname` 获取结果集中字段的名称。字段从 0 开始编号。

## 示例

请参考 `velocis_exec` 示例。

## 相关函数

```php
velocis_fieldnum
```

### integer velocis_fieldnum(integer result)

`velocis_fieldnum` 函数返回结果集的字段数量。

## 示例

请参考 `velocis_exec` 示例。

## 相关函数

`velocis_fieldnum`

```

### boolean velocis_freeresult(integer result)

使用 `velocis_freeresult` 释放与结果集相关的内存。这并不是绝对必要的，因为 PHP 在脚本结束时会清理这些内存。

## 示例

请参考 `velocis_exec` 示例。

## 相关函数

`velocis_exec`

```

### boolean velocis_off_autocommit(integer connection)

`velocis_off_autocommit` 函数关闭给定连接的任何查询自动提交。

## 示例

```php
<?php velocis_off_autocommit($connection);
?>
```

## 相关函数

`velocis_autocommit`

```php
string velocis_result(integer result, string field)
```

`velocis_result` 函数返回结果集中字段的值。值取自当前行，当前行由 `velocis_fetch` 控制。可以使用数字（从0开始）或名称指定字段。

## 示例

请参考 `velocis_exec` 示例。

## 相关函数

`velocis_exec`

```

### boolean velocis_rollback(integer connection)

使用 `velocis_rollback` 回滚所有事务。

## 示例

```php

<?php velocis_rollback($connection);

?>
```

![](img/490647a2fc8fbc7034b6e56593c58845_454_0.png)

图 14-1 冒泡排序

# 第14章 排序、搜索与随机数

```php

<?php

function BubbleSort($input_array) {

  $limit = count($input_array);

  for($bubble = 1; $bubble < $limit; $bubble++) {

    for($position = $limit-1; $position >= $bubble; $position--) {

      if($input_array[$position-1] > $input_array[$position]) {

        //交换元素
        $temp = $input_array[$position-1];

        $input_array[$position-1] = $input_array[$position];

        $input_array[$position] = $temp;

      }
    }
  }
}

/*

** 带有 HTML 换行符的文本

*/

function println($text) {
  print("$text<BR>\n");
}

$some_numbers = array(6, 13, 99, 2, 33, 19, 84);

// 打印数组
print("<H3>未排序</H3>\n");
array_walk($some_numbers, "println");

// 排序数组
BubbleSort(&$some_numbers);

// 再次打印数组
print("<H3>已排序</H3>\n");
array_walk($some_numbers, "println");

?>

```

图 14-1（续）

## 排序 433

最层的 for 循环设置了允许泡上升的限制。第一次运行时时，这个限制是1，因为数组的第一个元素索引为0。在运行一次内层循环后，我们可以确定最小数字位于数组第一个的位置。这是因为内层循环会将最后一个元素与前面的元素进行比较，如果顺序错误则交换它们，然后向上移动一位。最终将找到最小元素并将其向上交换。

如果 n 是数组中元素的数量，冒泡排序将始终进行 (n-1) 次比较，然后是 (n-2) 次，依此类推。在图 14-1 中，这意味着 7 个元素在第一次迭代中需要 21 次比较（6+5+4+3+2+1）。无论数组是有序的还是无序的都是如此。如果数组已经有序，不会进行任何交换。如果它是反序的，则每次比较都会进行交换。

很容易看出冒泡排序效率非常低，但如果你运行了图 14-1 中的示例，你可能并没有这种印象。对于少于一百个元素的微型列表，冒泡排序很慢。如果你必须自己编写排序算法，冒泡排序的优点是容易记忆且简单到第一次就能写对。

## 快速排序

快速排序由 C.A.R. Hoare 教授于1961年发明，被证明是最好的通用排序算法。许多计算机语言提供了库版本，PHP 的内置排序函数也使用了它。它基于相同的元素交换思想，但增加了分区的概念。在大多数实现中，它依赖于递归，这是第4章讨论的话题。

快速排序算法选择一个基准元素，并根据所有元素大于或小于基准来分划分。每个子部分以类似的方式进一步划分。当粒度变得足够小时，元素会被比较并可能被交换，就像冒泡排序一样。

当我们第一次调用图 14-2 中的 `quicksort` 函数时，我们首先将数组的第一个和最后一个元素作为左右边界。这将导致数组被排序。为了获得最佳性能，所有数字的中位数是最好的。这会将数组精确地分为两部分。然而，找到中位数需要花费精力。为了不增加这种开销，我选择了选取中间的数字。

下一步是将列表一分为两半。从外部开始，检查元素是否大于或小于基准。

# 第14章 排序、搜索与随机数

```php

<?php

/*
** 快速排序
** input_array 是一个整数数组
** left 是要考虑的最左侧的元素
** right 是要考虑的最右侧的元素
*/

function Quicksort($input_array, $left_limit, $right_limit)
{
    // 初始化指针
    $left = $left_limit;
    $right = $right_limit;
    // 选择中间元素作为基准
    $pivot = intval(($left + $right)/2);
    $pivot = $input_array[$pivot];
    do
        while(($input_array[$left] < $pivot) AND
            ($left < $right_limit))
        {
            $left++;
        }
        while($pivot < $input_array[$right]) AND
            ($right > $left_limit))
        {
            $right--;
        }
        if($left <= $right)
        {
            // 交换元素
            $temp = $input_array[$left];
            $input_array[$left] = $input_array[$right];
            $input_array[$right] = $temp;
            $left++;
            $right--;
        }
    } while($left <= $right);
```

图 14-2 快速排序

## 排序 435

```php

<?php

if($input_array[$left] < $pivot) {
    Quicksort($input_array, $left_limit, $right_limit);
}
if($left < $right) {
    Quicksort($input_array, 0, count($input_array)-1);
}

/*
** 带有 HTML 换行符的文本
*/

function println($text) {
    print("$text<BR>\n");
}

$some_numbers = array(6, 13, 99, 2, 33, 19, 84);

//

print("<H3>未排序</H3>\n");
array_walk($some_numbers, "println");

// 排序数组
BubbleSort(&$some_numbers);

// 再次打印数组
print("<H3>已排序</H3>\n");
array_walk($some_numbers, "println");
?>
```
