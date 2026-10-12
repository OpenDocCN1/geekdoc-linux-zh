

这一切值得吗？将操作写成乘法需要多长时间，写成位移又需要多长时间？验证你所写内容的正确性需要多久？修复因极端情况下的不同行为或忘记优先级差异等问题而产生的 bug 需要多长时间？未来修改代码（例如，将乘以 8 改为乘以 9）又需要多少时间呢？（你不能只搜索 8 的实例；你还必须搜索 3 的实例，而且你为什么没有使用命名常量？）该操作需要执行多少次，才能节省下与你花费确保使用更快选项的时间相同的成本——这里一纳秒，那里一纳秒？而在该操作被执行那么多次之前，还要经过多长时间？

关键在于**你的**时间比**计算机的**时间更有价值。比你的时间更有价值的在线时间是访问你网站的访客的时间。因此，不要浪费时间试图从页面处理时间中省下一纳秒：即使是在异常高负荷使用下，网站访客也察觉不到这种差异。

## 比较字符串速度 —— 基准测试示例

PHP 提供了多种方式组合字符串字面量和变量，以及三种引用字符串的方法。这三种引用方法是使用单引号、双引号以及 heredoc 语法。将变量插入字符串可以通过使用连接运算符、双引号或 heredoc 字符串中的变量插值，以及 C 风格的字符串格式化函数来实现。时不时地，会有好奇的程序员询问哪种方法更“好”。“好”的定义方式不止一种：它更快吗？它使源代码更易读吗？它更简单且更少出错吗？就可读性和简洁性而言，争论双方旗鼓相当：如果其中一种方法*明显*优于其他方法，那么自然选择会让大型应用程序中的资深开发人员 exclusively 使用这种优越方法。多年来，似乎没有发生这种选择，这表明差异并不足以出现在行业范围内的最佳实践文档或编码标准中。

单引号字符串是否*比*双引号字符串*更快*，则更容易量化。如果你被迫给出肯定或否定的答案，那么最安全的说法是“是”，但现实中事情比这复杂得多。

就像关于现实世界的任何问题一样，不先获取一些事实就无法回答。作为一个初步实验，你可以编写以下内容：

```php
$variable = 'string';

$start = microtime(true);
for($i=0; $i<1000000; ++$i) {
    $string = "this string has a $variable embedded into it";
}
$elapsed = microtime(true);
for($i=0; $i<1000000; ++$i) {
    $string = "this string has a "."$variable." inserted into it";
}
$finish = microtime(true);

echo "Variable interpolation required ",$finish-$start," seconds for one million iterations.\n";
echo "Variable concatenation required ",$finish-$1sttime," seconds for one million iterations.\n";
```

第一次运行此脚本时，我得到的插值和连接时间分别为 6.81 秒和 1.72 秒。然而第二次运行，时间却为 6.58 秒和 1.71 秒。这种变异性是由于我运行的计算机不仅仅是在运行该脚本。它还有其他时间需求，而这些其他需求所花费的时间也被计入该脚本完成所需的时间。当脚本第一次运行时，操作系统必须为 PHP、脚本及其数据组织内存空间，其中一些组织是在脚本运行期间发生的（然而，大部分组织会在脚本开始执行之前完成，因此不会体现在计时中）。但紧随其后的第二次运行，环境里已经有一个合适的空闲空间块，因此启动速度要快得多。

结果是你不能只信任一次运行的结果；计时波动的方式太多了，其中许多是你无法控制的。需要的是运行该脚本——从头到尾——多次，并取结果的平均值。对于插值，10 次运行的时间在 6.57 到 6.86 秒之间，平均为 6.77 秒；而对于连接，范围在 1.65 到 1.71 秒之间，平均为 1.70 秒。如果你愿意，可以对数据施加更多的统计火力，但似乎很明显，连接比插值快大约四倍。

但这还不是全部。如果时间取决于字符串的长度，或者被连接或插值的变量数量呢？难道我们不应该测试这些方面的变化吗？

以下是一个用于运行此类测试的命令行 PHP 程序。它不是测量连接或插值变量时的时间本身，而是写入一个单独的 PHP 脚本，然后通过命令行调用它，从而不仅测量脚本本身的时间，还包括启动 PHP、加载脚本和关闭所花费的时间。它对一系列初始字符串大小（64 到 26176 个字符，步长为 512）和插值/连接数量（0 到 100）执行此操作。每个实验执行五次，并将平均运行时间写入单个日志文件。如果两万五千个独立实验太多了（可能需要大约四个小时），那么可以根据喜好缩小范围，但应保持对每个大小/数量组合的多次测试并取平均值。如代码所示，它测量的是变量插值——取消注释第 59 行并注释掉第 58 行（即 str_replace() 调用）将其改为测量连接：

```php
<?php
function generate_test($string)
{
    $code = '<?php
$interpolated="badgers!";

for($i=0; $i<100; ++$i)
    $string = "".$string."";
?>';
    $temp_file = tempnam('', 'xx_test');
    $fp = fopen($temp_file, 'wb');
    fwrite($fp, $code);
    fclose($fp);
    return $temp_file;
}

function run($file)
{
    $average_runtime = 0;
    for($runs=0; $runs<5; ++$runs)
    {
        $start = microtime(true);
        shell_exec("php -f $file"); // If necessary, supply path information here
        $end = microtime(true);
        $average_runtime += $end-$start;
    }
    return $average_runtime/5;
}

$log = fopen('logfile.txt','wb');
for($string_size=1<<6; $string_size<=26176; $string_size+=512)
{
    $generic_string = str_repeat("wibble splunge!\n", $string_size);
    $real_string_size = 16*$string_size;
    $all_positions = range(0,$real_string_size-1);
    for($num_variable_interpolations=0; $num_variable_interpolations<=100;
        ++$num_variable_interpolations)
    {
        echo $string_size,"\t",$num_variable_interpolations,"\n";
        $string = $generic_string;
        if($num_variable_interpolations==0)
            $positions = array();
        else
            $positions = array_rand($all_positions,$num_variable_interpolations);
        if(count($positions)==1) $positions = array($positions);
        foreach($positions as $position)
        {
            $string = substr($string,0,$position).'${'.substr($string,$position);
        }
        $string = str_replace('${','${interpolated}', $string);
        $string = str_replace('$','*.interpolated.*', $string);
        $file = generate_test($string);
        $runtime = run($file);
        unlink($file);
        fwrite($log,
            $string_size,"\t",$num_variable_interpolations,"\t",$runtime,"\n");
    }
}
fclose($log);
?>
```

从代码中最后一个 `fwrite()` 调用，你可以推断出保存数据的格式：每个实验一行，包含字符串的大小（插入变量之前）、被插入的变量数量以及秒数。然后你可以将此数据读取到你喜欢的数据分析或绘图软件中进行探索。

