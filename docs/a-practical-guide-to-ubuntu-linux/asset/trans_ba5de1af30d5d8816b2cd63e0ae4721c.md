

```
$ perl sort4.pl
22 188 44 2 12
2 12 22 44 188
188 44 22 12 2
```

# 子程序 (SUBROUTINES)

所有的变量都是包变量（第 1045 页），除非你使用 `my` 函数将它们定义为局部变量（第 1045 页）。在子程序中定义的局部变量对该子程序可见。

以下程序包含一个主部分和一个 `add()` 子程序。该程序使用了名为 `$Some`、`$two` 和 `$ans` 的变量，它们都是包变量：它们在主程序和子程序中可用。对子程序的调用没有向子程序传递值，且子程序没有返回任何值。这种风格并不典型：它说明了除非你使用 `my` 将它们声明为局部变量，否则所有变量都是包变量。

`subroutine1.pl` 给两个变量赋值并调用了一个子程序。该子程序将两个变量的值相并将结果赋值给另一个变量。程序的主部分显示了结果。

```
$ cat subroutine1.pl
$Some = 1;
$two = 2;
add();
print "Answer is $ans\n";
```

```
sub add {
$ans = $Some + $two
}
```

```
$ perl subroutine1.pl
Answer is 3
```

下一个示例与上一个相似，区别在于子程序利用 `return` 语句向主程序返回一个值。程序将子程序返回的值赋值给变量 `$ans` 并显示该值。再次，所有的变量都是包变量。

```
$ cat subroutine2.pl
$Some = 1;
$two = 2;
$ans = add();
print "Answer is $ans\n";
```

```
sub add {
return ($Some + $two)
}
```

```
$ perl subroutine2.pl
Answer is 3
```

在许多情况下，将变量保持在子程序局部是非常重要的。下一个示例中的子程序通过声明和使用局部变量改变变量的值，并保护调用程序免受这些变化的影响。这种设置更为典型。

当你向子程序传递值时，Perl 会将这些值在子程序中名为 `@` 的数组中可用。虽然 `@` 是子程序局部的，但它的元素是调用该子程序的参数的别名。在 `@` 数组中更改值会改变底层变量的值，这可能不是你想要的。下一个程序通过将传递给子程序的值赋值给局部变量来避免这一陷阱。

`subroutine3.pl` 程序带有两个变量调用 `addplusone` 子程序，并将子程序返回的值赋值给一个变量。子程序声明了两个局部变量并将它们赋值为来自 `@` 数组的值。（参见第 1050 页关于局部变量和包变量的提示）。虽然你可以在不给声明变量赋值的情况下使用，但示例中的语法是最常见的。这两个语句增加了局部变量 `lcl_one` 和 `lcl_two`。`print` 语句显示了子程序内部 `lcl_one` 的值。`return` 语句返回两个增加后的局部变量之和。

```
sub subroutine3.pl
$lcl_one = 1;
$two = 2;
$ans = addplusone($lcl_one, $two);
print "Answer is $ans\n";
print "Value of $lcl_one in main: $lcl_one\n";
print "Value of $one in main: $one\n";
```

```
sub addplusone {
my ($lcl_one, $lcl_two) = @;
$lcl_one++;
$lcl_two++;
print "Value of $lcl_one in sub: $lcl_one\n";
return ($lcl_one + $lcl_two);
}
```

```
$ Perl subroutine3.pl
Value of $lcl_one in sub: 2
Answer is 5
Value of $lcl_one in main: 
Value of $one in main: 1
```

在显示由子程序返回的结果后，主程序中的 `print` 语句证明 `$lcl_one` 在主程序中没有定义（它是子程序的局部的），并且 `$one` 的值没有改变。下一个示例说明了处理传递给子程序的参数另一种方法。该子程序没有使用传递它的 `@_` 之外的变量，也没有更改任何元素的值。

# 正则表达式 (REGULAR EXPRESSIONS)

```
$ cat subroutine4.pl
$one = 1;
$two = 2;
$ans = addplusone($one, $two);
print "Answer is $ans\n";
sub addplusone {
    return ($[0] + $_[1]);
}
Answer is 5
```

本节的最后一个示例展示了一个更典型的子程序。`max()` 子程序可以用任意数量的参数调用并返回最大参数的值。它使用 `shift` 函数将第一个参数的值赋值给 `$biggest`。`shift` 之后，参数 2 变成参数 1，参数 3 变成参数 2，参数 4 变成参数 3。接下来，`foreach` 遍历剩余的参数 (`@`)。

```
$ cat subroutine5.pl
$ans = max (16, 8, 64);
print "Maximum value is $ans\n";
```

```
sub max {
    my $biggest = shift; # 先赋值并移动剩余参数
    foreach (@_) { # 遍历剩余参数
        $biggest = $_ if $_ > $biggest;
    }
    return ($biggest);
}
```

```
$ perl subroutine5.pl
Maximum value is 64
```

# 正则表达式 (REGULAR EXPRESSIONS)

附录 A 定义并讨论了正则表达式，你可以在许多工具中使用它们。除非另有说明，否则附录 A 中的所有材料都适用于 Perl。除了附录 A 中描述的功能外，Perl 还提供了允许你执行复杂字符串处理的正则表达式功能。本节回顾了附录 A 中涵盖的一些正则表达式，并描述了 Perl 中提供的某些额外功能。它还介绍了 Perl 用于处理正则表达式的语法。

# 语法与 ~= 运算符 (SYNTAX AND THE ~= OPERATOR)

-l 选项。 Perl -l 应用于输入的每一行，并在每行输出末尾放置 `\n`。本节中的示例使用了 Perl 的 -l 和 -e（第 46 页）选项。由于程序必须指定为单个参数，示例将 Perl 程序封装在引号内。shell 会解释引号而不会将其传递给 Perl。

# 与 -e 使用其他选项

当你配合 -e 使用另一个选项时，该程序必须在命令行中紧跟在 -e 之后。像许多其他工具一样，Perl 允许你合并单个连字符后面的选项；如果 -e 是选项列表之一，它必须出现在最后。默认情况下，perl 使用斜杠 (/) 定界正则表达式。你可以使用 -le 而不是 -el。

默认情况下，perl 使用斜杠 (/) 定界正则表达式。使用 ~= 运算符在字符串 aged 中搜索模式 ge。在示例中，表达式为真，Perl 执行了 print 语句。

```
$ perl -le 'if ("aged" =~ /ge/) { print "true"; }
true
```

你可以通过使用 if 语句实现相同的功能：

```
$ perl -le 'print "true" if "aged" =~ /ge/'
true
```

~! 运算符的作用与 ~= 相反。示例中的表达式为真，因为正则表达式 xy 不匹配 aged 的任何部分：

```
$ perl -le 'print "true" if "aged" ~ /xy/'
true
```

如第 191 页所示，点匹配任何单个字符，因此正则表达式 a..d 匹配字符串 aged：

```
$ perl -le 'print "true" if "aged" =~ /a..d/'
true
```

你可以使用变量来持有正则表达式。以下语法作为正则表达式：

```
qr/string/
```

# 正则表达式 (REGULAR EXPRESSIONS)

下一个示例使用此语法将正则表达式 /a..d/（包括定界符）赋值给变量 `$re`，然后将其作为正则表达式：

```
$ perl -le '$re = qr/a..d/; print "true" if ("aged" ~ $re)'
true
```

如果你想在正则表达式中包含定界符，你需要对其转义。在下一个示例中，默认定界符 / 出现在正则表达式中。为了防止 Perl 将 /usr 解释为正则表达式的结束，正则表达式 / 通过在其前面加上反斜杠 (\) 进行转义。更多信息请参阅第 193 页。

```
$ perl -le 'print "true" if ("/usr/doc" ~ /\/usr/)'
true
```

通过反斜杠转义多个字符会让复杂的正则表达式更难以阅读。相反，你可以使用 m 和一对字符（如 {}）来定界正则表达式。在以下示例中，脱字符 (^) 将正则表达式锚定到行首（第 192 页）：

```
$ perl -le 'print "true" if ("/usr/doc" ~ m{/usr/)'
true
```

你可以在将正则表达式赋值给变量时使用该语法：

```
$ perl -le '$Spn = qr{/usr/doc}; print "true" if ("/usr/doc" = $Spn)'
true
```

