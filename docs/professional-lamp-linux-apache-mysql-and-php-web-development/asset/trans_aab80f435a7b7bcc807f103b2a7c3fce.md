

## 第 9 章

试一试：

```php
<?php
// If any processing involving HTTP headers is required,
// now would be a good time to do it.
?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>A page buffered in chapters</title>
<?php

ob_start(); // HTML <head> content
// Construct <meta> tags, and select some CSS and Javascript to include. E.g.,
echo "<meta name=\"author\" content=\"${Page_author}\">
"
;
ob_end_flush(); // Output the HTML head chapter

?>
</head>
<body>
<?php

ob_start(); // Strapline and breadcrumb trail.
?>
<div id="topmatter">
<!-- HTML and PHP for constructing this chapter -->
</div>
<?php
ob_end_flush(); // Output the strapline chapter

ob_start(); // Side navigation list
// ... 
ob_end_flush(); // Output the side navigation chapter

?>
... 
</body>
</html>
```

在这个示例中，展示了六个部分：从 `<!DOCTYPE>` 声明开始，到 `<title>` 元素结束的部分；`<head>` 元素其余内容对应的部分；完成 head 并开启 body 的小部分；随后是组成页面布局的两个部分（假设还有其他部分）；最后是 `</body></html>` 以结束页面。每个部分都会作为一个完整的块输出，从而为 Apache 提供最佳条件，使其能够尽可能高效地填充其发送的数据包。

### **echo 还是 print？**

哦不，又来了。*echo* 和 *print* 之间值得注意的速度差异（除了打字速度外）主要在于你需要依次输出多个字符串时。如果使用 *print*，你需要将它们全部拼接在一起，然后输出生成的字符串。使用 echo 也可以这样做，但你不必这么做，只需使用逗号 (,) 而不是点号 (.) 来分隔字符串即可。

在进行字符串拼接时，PHP 需要为正在构建的字符串分配内存，并且每次执行拼接操作时都要重新分配内存。这会引入延迟。此外，在构建整个字符串完成之前，字符串的任何部分都无法输出，因此如果被拼接的项之一是函数，那么一切都必须等待该函数执行完毕。请比较运行以下语句的结果：

```php
print "This string takes ".sleep(15)."too long to display.";
echo "This string takes ".sleep(15)."too long to display.";
echo "This string takes ", sleep(15), "too long to display.";
```

这种方法适用于输出，但对于需要拼接到变量中的字符串，也可以采用类似的方法：启动一个输出缓冲区，使用 echo 输出字符串的所有片段，将缓冲区内容读取到变量中，最后结束并清理缓冲区。例如：

```php
ob_start();
for($i=0; $i<100; $i++) echo $i,' ';
$zero_to_ninetynine = ob_end_clean();
```

### for($i=0; $i<count($array); $i++)

不要这样做。这样做意味着 PHP 必须在每次迭代后检查数组的大小。没错，数组的大小是与其内容一起维护的，因此实际上不需要*计数*其元素，但仍需查询大小——以防数组在循环过程中发生了变化。如果你知道它不会变化，请使用以下方法：

```php
for($i=0, $count_array=count($array); $i<$count_array; $i++)
```

这就既有效又节省了额外的查找。如果数组元素遍历的顺序不重要，则可以使用中间变量来避免这种情况：

```php
for($i=count($array)-1; $i>=0; $i--)
```

如果你这样做，请记住 -1 和 >=。

### 临时变量

特别是当你使用关联数组时，如果你要多次查看同一个数组元素，将其值放入局部变量中（如果你打算修改它，则按引用分配）可以节省查找 $array['foo'] 实际指向哪个数组元素所涉及的开销。数组属性也是如此。考虑以下代码：

```php
$this->p_consts->Delta[$i][$k] = $this->p_consts->Delta[$i]($this->p_consts->s[$i]-1);
$this->n[$i][$k] = $this->n[$i]($this->p_consts->s[$i]-1);
```

$this->p_consts 使用频率相当高；特别是其 *Delta* 和 *s* 属性。你可以创建临时变量来存储这两个属性的值（因为你要修改其值，所以按引用分配 *Delta*），从而避免每次都需要通过 $this->p_consts 进行查找：

```php
$p_Delta = &$this->p_consts->Delta;
$ps = $this->p_consts->s[$i]-1;
$p_Delta[$i][$k] = $p_Delta[$i][$ps];
$this->n[$i][$k] = $this->n[$i][$ps];
```

显然，这也可以使程序更易读。

### if...else if 测试和 Switch 案例的顺序

首先，如果你有一系列连续的 *if* 语句，并且在任何给定时间只有一个可能为真，那么除了第一个之外，你应该对所有其他语句使用 *else if*。否则，在找到匹配项后，PHP 将继续测试剩余部分。*你知道它们都将为假，但真正执行工作的人不是你。* PHP 必须继续测试，以防被测变量在处理成功语句期间发生了变化。

如果你有一系列 *if...else if* 语句或 *switch* 语句，请将更常见的情况放在顶部，将罕见情况移到底部。除了向读者提供代码功能的更清晰视图（通过先说明典型情况，之后再处理复杂的边缘情况）之外，这意味着 PHP 平均需要执行更少的测试才能找到一个成功的测试。

即使你最常用的情况由最后的 *else* 或 *default* 案例满足，也请显式提供它们，并将它们的测试放在顶部（*每个测试都会在 PHP 处理此类剩余部分之前进行检查*）。

### 使用正确的字符串函数

手册反复指出，如果你没有实际使用正则表达式语法的任何功能，那么 PHP 的其他字符串函数可能比正则表达式函数快得多。当你可以说 *explode( " /", $path)* 时，不要说 *split( " /", $path)*。

### 正则表达式语法

说到正则表达式，谨慎的设计也能提高其性能。整本书甚至多本书都可以且已经写过关于正则表达式及其编写方法的论述；目前，只需记住，PCRE 函数 *preg_match()* 等提供了比 *ereg()* 等 POSIX 函数更丰富的语法和更智能的引擎。

### unset()

好吧，PHP 会在变量*超出作用域*时立即清理变量；要么是函数末尾的局部变量，要么是脚本末尾的*其他所有内容*。一般来说，这意味着你不必担心这个问题。

但如果你有一个巨大的结构（例如包含成千上万个元素的数组），你不再会再次使用它，特别是如果你马上就要处理更多的大数据，那么你应该在完成工作后立即 *unset()* 该结构。由此产生的大块空闲内存可以立即用于其他用途。在繁忙的服务器上，在可能的情况下释放大块内存，可能会决定是让所有东西都装入 RAM 还是 resort 到磁盘上的虚拟内存。

### 释放资源和持久数据库连接的危险

同样，如果你正在使用诸如 MySQL 数据库连接之类的资源，并且你已完成使用但仍有大量工作要做，不要为了脚本执行的剩余时间而独占它：关闭它。

持久数据库连接（例如由 `mysql_pconnect()` 创建的连接）有时被建议作为加速性能的手段。这是因为在连接第一次建立后，创建它的 httpd 进程在建立该连接的脚本结束后仍会保留该连接，以便在下一次运行需要数据库连接的脚本时使用。由于连接数据库涉及一些工作，持久连接可能会节省一点时间。但在节省的时间变得明显之前，可能会出现故障。

问题在于，即使已连接的 httpd 进程可能位于请求之间，它仍会保持该数据库连接打开，直到它死于服务器指定的死亡。数据库连接是有限的资源（`mysql_close()` 对持久连接没有效果）。很可能发生的是，如果情况变得繁忙，脚本可能尝试连接数据库，但会收到错误消息而被拒绝，说最大允许的连接数已经分配。如果所有连接都在使用中，那就不会那么糟糕：你只需稍微加强数据库服务器即可。但如果最大连接数是因为空闲的 httpd 进程占据可用连接（以防出现需要其中之一的请求）而达到，那就麻烦了。

### `ob_gzhandler()`

如果你打算使用输出缓冲来批量处理页面输出，使用 `ob_start('ob_gzhandler')` 启动缓冲区意味着，当你收集缓冲输出时，会发现它已被压缩。回调函数礼貌地检查请求头，以确保输出前往的浏览器确实能够阅读 gzip 压缩的数据。

作为使用该回调处理器的*替代方案*（不要试图同时使用两者），考虑在 `php.ini` 中设置 `zlib.output_compression`。事实上，这是 PHP 开发人员推荐的方法。

### 总结

在阅读这里的建议和指导时，你无疑会注意到有些似乎相互矛盾。这是不可避免的：什么有效取决于具体情况，而不同的情况可能需要做出不同的决定。大量操作大型数据库的网站与主要以文件存储为目的的网站需求不同。

作为开发人员，你的时间比计算机作为 Web 服务器的时间更有价值。从经济角度或工作满意度角度来看，将时间浪费在那些最好只能带来微小改进且对网站访客不可见的更改上，完全是没有意义的。相反，将时间投资于规划与测试。在查看单行代码之前，退一步看大局。

你的硬件是否合格，还是它会限制软件改进的效果有多大？你的 Web 服务器是如何配置的；是否可以进行调整？有多少冗余计算被执行：一个地方的结果是否可以在其他地方预期有用时进行缓存？

