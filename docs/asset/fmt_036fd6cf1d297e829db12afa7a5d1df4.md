
![](img/e259ba2750941fa3d146eda78c65e89d_315_0.png)

## 10.8.7 switch, case 和 break (仅 C Shell)

`switch`语句将脚本流导向特定的`case`标签，即脚本中匹配`switch`语句定义的可能条件点。不要将 C shell 中用于 case 标签的`case`与 bash 或 Korn shell 的`case`语句（第 10.8.8 节）混淆！如果没有任何`switch`语句匹配 case 标签，你可以定义一个`default`条件。`break`语句将流导向`endswitch`语句之后的语句。如果没有`break`，C shell 将继续向下遍历 case 标签列表以寻找额外的匹配项。如果没有满足条件且没有定义默认条件，执行将从`endswitch`语句后继续。听起来很困惑？下面的这个简单示例有助于澄清 switch 的用法。

### OpenVMS UNIX (C shell)

**格式：**

```c
switch (string1)

  case string2:

    ...

    break

  case string3:

    ...

    break

  default:

    ...

endswitch
```

**示例：**

```bash
$ TYPE TEST.COM

$ Select a printer

$ ON WARNING THEN GOTO WRONG

$ WRITE SYS$OUTPUT "Select a printer"

$ INQUIRE PR "Enter 1 or <cr> for laser - 2 for plotter; 3 for character printer"

$ IF ($1 .EQS. "") THEN GOTO 1

endswitch
```

```csh
% cat test_script.csh

# Select a printer

echo "Select a printer"

echo "Enter 1 or <cr> for laser \n2 for plotter;\n3 for character printer"

set p : $?

if ( -z $p ) then

  set p : "i"

endif

switch $p
```

## 10.8 Flow控制

335

```perl
$ GOTO 'PI' 
$ i: 
**$ PRINT/QUEUE **: **LASER 'PR' 
$ GOTO DONE 
$ 2: 
$ PRINT/QUEUE = PLOTTER 'mR' 
$ GOTO DONE 
$ 3: 
$ PRINT/QUEUE = CHARACTER 'PI' 
$ DONE: 
$ EXIT 
$ WRONG: 
$ WRITE SYS$OUTPUT "Invalid Entry" 
$ EXIT 
```

**Perl**
**示例:**

```perl
#!/usr/bin/perl 
-w
# 选择一个打印机
# 
print "Select a printer\n";
print "Enter 1 or <cr> for laser\n",
"2 for plotter; 
3 for character printer\n";
$p : <STDIN>;
chomp($p);
$p = 1 if (not defined($p));
SWITCH
{
    if ($p :- m/^1$/)
    {
        system("ipr -Plaser $ARGV[0]");
        last SWITCH;
    } 
    if ($p :- m/^2$/)
    {
        system("ipr -Pplotter $ARGV[0]") ;
        last SWITCH;
    } 
    if ($p :- m/^3$/)
    {
        system("pr -Pcharacter $ARGV[0]");
        last SWITCH;
    } 
    print "Invalid entry\n";
} 
exit;
```

```
case i:
    ipr -Plaser $i
    breaksw
case 2:
    ipr -Pplotter $i
    breaksw
case 3:
    pr -Pcharacter $i
    breaksw
default:
    echo "Invalid entry"
    endsw
exit
```

在这个示例中，`switch`语句将文件的打印重定向到`特定的打印机队列`。用户输入 1、2、3 或 `<or>` 来`选择打印机`。脚本根据用户的响应将流引导到相应的 case 标签。`lpr`命令将文件入队并将控制权交给`endsw`语句。如果用户输入默认条件 `<cr>` 或除 1、2、3 以外的任何字符，控制权将传递到默认语句标签，该标签会在默认打印队列上打印文件。与 OpenVMS 相比，在 OpenVMS 中，要自动转移到处理器，必须引入一个`ON WARNING`条件来处理错误字符。脚本也具有错误处理能力，正如我们在第 10.8.12 节中看到的。

注意，嵌套的`if-then-else`结构也可以实现相同的流控制。然而，当 case 标签是常量时，`switch`更加方便且通常更易理解。奇怪的是，Perl 没有提供`case`语句，尽管有几种方法可以模拟它。上面的示例只是许多常用方法之一。`m//`是 Perl 的正则表达式匹配运算符。

I 第 10 章

![](img/e259ba2750941fa3d146eda78c65e89d_317_0.png)

336

10.8 Flow控制

#### 10.8.8

#### 10.8.9

### case (bash 和 Korn Shell)

Korn 和 bash shell 的`case`命令在概念上与 C shell 的`switch`命令相似，但有一个重要的区别：一旦找到模式匹配并执行了随后的语句，它就不会继续寻找匹配项。这就像在匹配模式随后的语句中自动内置了一个 C shell 的`breaksw`命令一样。

另一个不那么显著但极大地增强了`case`命令能力的区别是，每个单独的可能性都是一个表达式，允许具有完全的通用性和复杂性。下面是打印机选择示例的 Korn 版本。我们重复了 OpenVMS 示例，以便你可以更直接地看到等效性。

此`case`命令不需要像 C shell `switch`命令那样的显式默认语句。由于 shell 正在寻找模式，你可以用 `*`。设置默认值。

Korn 和 bash shell 的模式匹配允许我们扩展允许的响应，包括打印机名称单词以及选择数字。与其使用`if`命令来设置合法的默认值，我们可以包含空字符串作为默认打印机的选择。

### select (bash 和 Korn Shell)

`select`命令执行`case`语句的一种简单且特殊的版本，特别适用于菜单选择，例如用于`switch`和`case`的打印机示例。给定一组作为可能的回复单词列表，

![](img/e259ba2750941fa3d146eda78c65e89d_318_0.png)

337

10.8 Flow控制

**OpenVMS**
**示例:**

```
$ TYPE TEST.COM
! 选择一个打印机
$ ON WARNING THEN GOTO WRONG
$ WRITE SYSOUTPUT "Select a printer"
$ INQUIRE PROC "Enter 1 or <cr> for laser 2 for plotter; 3 for character printer"
$ IF (PROC="") GOTO 1
$ PRINT/QUEUE = LASER 'PR'
2:
$ PRINT/QUEUE = PLOTTER 'mR'
3:
$ PRINT/QUEUE = CHARACTER 'PI'
DONE:
$ EXIT
WRONG:
$ WRITE SYS$OUTPUT "Invalid Entry"
```

**case** (bash 和 Korn Shell) 格式：

```bash
case $p in
    1 )
        ipr -Plaser $i
        ;;
    2 )
        ipr -Pplotter $i
        ;;
    3 )
        pr -Pcharacter $i
        ;;
    *)
        print "Invalid entry"
        ;;
esac
```
