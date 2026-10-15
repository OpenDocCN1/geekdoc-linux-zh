
or hippopotamus, but then she remembered how small she was now, and she soon made out that it was only a mouse that had slipped in like herself.

```
$
```

很酷的技巧，不是吗？

哦！要获取压缩归档，命令看起来与之前的调用非常相似（但请注意，你需要将下载的数据重定向到一个文件中）：

```
$ GET http://www.intuitive.com/tyu24/alice.tgz > alice.tgz
```

一旦你开始思考如何以命令行的方式处理 Web 内容，你就会意识到这种能力确实是 Unix 成为一个极佳工作环境的原因之一。想想看：任何你能从 Web 上获取的文件、数据、HTML，你都可以将其纳入 shell 脚本中，或通过 `grep` 等方式查找关键的显著数据。从股票报价到天气，从词典查询到 RSS Feed 解析，`lynx`、`curl` 或 `GET` 与数千个 Unix 命令的组合是无与伦比的！

## Summary

本小时首先探索了功能强大的 `find` 命令，它是 Unix 中最强大的命令之一。它有许多晦涩的选项，要充分发挥 `find`、`xargs` 和 `grep` 的威力，你需要进行实验。然后你学习了如何使用 Unix 命令访问 Internet 数据，无论是可访问的 FTP 服务器、网站，甚至是安全的网站。

## Workshop

本工作坊提出了一些关于本小时所介绍主题的问题。它还为你提供了下一小时将学习内容的预览。

## Exercises

- 1. 使用 `find` 和 `wc -l` 来统计你有多少个文件。务必包含 `-type f` 选项，这样就不会将目录计入总数。
- 2. 使用必要的命令列出以下内容：
  - 所有包含 `abc` 的文件名
  - 所有包含 `abc` 的文件
- 3. “hookah” 这个词在《爱丽丝梦游仙境》中出现了多少次？

## Preview of the Next Hour

下一小时将向你介绍 Unix 的强大瑞士军刀：Perl 编程语言。从简单的单行命令到数千行的程序，它是所有现代 Unix 用户必备的知识。

## 第23小时. 在 Unix 中使用 Perl 编程

## 本小时的目标

在本小时，你将学习

- 关于 `Exchange`，一款用 Perl 编写的演示货币转换器
- 如何使用 `-w` 检查代码质量
- 关于在线 Perl 文档和信息
- 关于其他有用的 Perl 命令

在本小时，我向你介绍 Perl 脚本和编程语言。Perl 是一种解释型语言，因此它不需要你像 C 和 Java 那样使用编译器作为中间步骤来运行它。Perl 的工作方式更类似于 shell 脚本，这使得它成为一种更易于使用的开发工具。

无论你是否计划参与 Unix 编程，我都强烈鼓励你阅读更多关于 Perl 的内容。除了是优雅而强大的 Unix 工具构建器之外，Perl 也是 Web 专业人士的首选经典编程语言之一。想要更深入地探索 Web 开发吗？那么明智的做法是学习 PHP 和 Python。两者都绝对对 Unix 友好，而且越来越多的代码是用这些语言编写的，同时还有 Ruby。

在本小时，你将学习标准 Perl 发行版提供的工具，它们可以帮助你开发智能、快速的程序。本课描述了一个程序，它使你能够轻松进行货币转换，以便为出国旅行做准备。

## 注意

令人惊讶的是，并非每个 Unix 实现都包含 Perl。如果没有它，或者你的 Perl 版本早于 5.0（尝试 `perl -v` 来查看你拥有的版本），那么请访问 `http://www.perl.org` 了解下载更新版本的信息。

### 灵活而强大：Perl

用 C 编程，C 语言是与 Unix 操作系统一起开发的，提供相当大的灵活性。C 是 Unix 操作系统本身的核心语言，但它最初是为系统级编程任务而设计的。相比之下，Perl 是为字符串或单词处理而设计的一种功能强大的语言。你可以通过探索一个编程任务最容易看到这种差异，所以这就是我们在本书本小时要做的。

## 任务 23.1：Exchange，一款用 Perl 编写的演示货币转换器

当我的一些朋友从世界各地的长途旅行归来时，他们评论说他们对如此多种多样的货币感到困惑。他们当然不是第一个注意到这一点的人，但我想“这是一个很棒的 Perl 程序可以编写！”

一旦掌握了公式和汇率，货币转换就很简单。在美国，货币价值通常相对于单一美元来表示，因此欧元可能估值为 0.9100，这意味着你兑换的每一美元价值略低于 €1。兑换 20 美元，你将获得 20×0.9100，即 €18.2。

`Exchange` 程序最初的生命是从读取六种主要世界货币（美元、日元、欧元、瑞士法郎、印度卢比和英镑）的当前汇率，提示输入美元金额，然后显示这些其他货币中的等值金额。然而，更有用的功能是可以从这些货币中的任何一种转换为另外五种。此外，互联网上存在显示每日汇率的网站，因此确保汇率是最新的也是另一个理想的程序功能。

于是 `Exchange` 诞生了。它是一个程序，让你能够在六种主要世界货币之间快速转换，使用单独的 shell 脚本来确保转换率是最新的。本任务展示了我如何用 Perl 和 Unix 将其构建出来。

1. `Exchange` 程序的基本逻辑流程（如果你想技术化一点的话就是算法）如下：

Click here to view code image

```
Read current exchange rates

Repeat

  Ask user for an amount and currency

  Translate that into US dollars

  Show the equivalent value in the other five currencies

Until done
```

2. Perl 支持子程序来帮助开发干净、可读的程序，所以让我们来看看程序中的主要代码：

Click here to view code image

```
printf("%2.2f USD, ", $baseval * $rateof{'U'});

printf("%2.2f Euro, ", $baseval * $rateof{'E'});

printf("%2.2f Rupee, ", $baseval * $rateof{'R'});

printf("%2.2f Swiss Franc, ", $baseval * $rateof{'F'});

printf("%2.2f Yen, and ", $baseval * $rateof{'Y'});

printf("%2.2f Pounds.\n\nAmount: ", $baseval * $rateof{'P'});
```

第一行需要指向你的 Perl 解释器；一个简单的方法是在命令行中使用 `which perl` 来查找。

我通过 `print` 语句添加了一些花哨的输出格式，但除此之外，这段代码与你已经看到的算法非常相似。请注意，数组 `rateof` 使用货币的首字母作为索引，并返回相对于美元的当前汇率（也就是说，`$rateof{'E'}` 实际上是 0.9100）。

Perl 的一个巧妙之处在于子程序可以返回一个变量列表，就像在对 `breakdown` 子程序的调用中所展示的那样，它同时返回 `$amnt` 和 `$curr`。

3. 本程序中包含两个子程序，`read_exchange_rate` 和 `breakdown`。我们按相反的顺序来考虑它们。

`breakdown` 子程序接收用户输入的货币金额并将其拆分为两部分：数值和货币指示符的首字母（如果有的话，默认货币为美元）：

Click here to view code image

```
sub breakdown {

    @line = split("", $_);        # split at space

    $amnt = $line[0];

    if ($#line == 1) {

        $curr = $line[1];

        $curr =~ tr/a-z/A-Z/;       # normalize to uppercase

        $curr = substr($curr, 0, 1); # extract first char only

    } else { $curr = "U"; }

    return ($amnt, $curr);

}
```

我在这里不会过多展开——Perl 在你刚开始使用时可能会有点让人不知所措——但如果子程序得到诸如 34.5 yen 这样一个值，它将返回 `$amnt = 34.5` 和 `$curr = 'Y'`。

4. 当前汇率从关联的数据文件 `exchange.txt` 中读取，该文件包含六种货币的汇率（尽管美元的汇率始终为 1，当然！）：

Click here to view code image

```
sub read_exchange_rate {

    open(EXCHRATES, "exchange.txt") ||
```
