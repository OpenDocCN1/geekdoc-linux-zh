
Perl 令是告诉编译器以非默认方式运行。在 `use` 语句中，我们告诉编译器使用一个特定的 Perl 模块，告诉 Perl 找到模块文件并执行某些 OOP 魔法，使得所有的方法或对象可用。例如，在 CGI 模块中定义了一个方法，因为我们告诉 Perl 要使用 CGI 模块，我们可以调用这个方法。

一旦我们使用了一个模块，通常可以通过执行 `new` 来创建该类型的对象：

```perl
$obj = new CGI;
```

一旦创建了对象，可以使用箭头符号调用方法：

```perl
$obj->header();
$obj->pre();
$obj->b();
```

这种语法意味着使用名为 `$obj` 的对象来执行 `header()`（或 `pre()` 或 `b()`），它是一个 CGI 类的对象。

有许多模块供 Perl 使用。你可以从综合 Perl 存档网络（CPAN）——`www.cpan.org/` 找到它们。我们建议你检查那里。你可能会发现你正在尝试解决或将来需要解决的问题，已经有人写好了模块可以让你的生活变得更轻松。

安装模块非常简单。首先，在 `www.cpan.org/` 找到你需要的模块。假设我们需要 Nifty 模块。我们找到 Nifty 的最新版本，假设是 1.03。从 CPAN 下载压缩包。

# 106 第一部分 结构

与大多数 Perl 工具一样，安装模块也有更更好的方法——使用 CPAN 模块。在本书中，我们演示了如何通过显式的方法安装 Perl 模块（正如前文所示），以防你无法通过 CPAN 安装所需的模块。如果你感兴趣，可以查看 `perl CPAN`。这里是安装前述模块的快速示例：

```
# perl -MCPAN -e shell
cpan> install Nifty
```

就这些了！像切饼一样简单。

下载命名为 `Nifty-1.03.tar.gz` 的文件并将其保存到方便的地方，比如 `/tmp`。然后，我们只需要做这些操作：

```
# cd /tmp
# tar xzvf Nifty-1.03.tar.gz
# cd Nifty-1.03
# perl Makefile.PL
# make
# make test
# make install
```
