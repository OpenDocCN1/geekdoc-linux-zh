
`$curr_dir = 'pwd'`;

`@listing = 'ls -al'`;

`print "Listing for $curr_dir\n"`;

```
foreach $file (@listing) {
    print "$file";
}
```

## 注意

`` ` `` 符号使用的是 Tab 键上方的反引号（在大多数键盘上），而不是单引号。

你也可以使用 `Shell` 模块来访问 shell。`Shell` 是 Perl 自带的标准模块之一；它允许创建和使用类似 shell 的命令行。查看下面的代码示例：

```
use Shell qw(cp);
cp ("/home/httpd/logs/access.log",
:/tmp/httpd.log");
```

这段代码看起来几乎是直接将命令行函数导入到 Perl 中。虽然实际上并没有这样发生，但你可以假装代码类似于命令行，并在你的 Perl 程序中使用这种方法。

访问 shell 的第三种方法是通过通过 `system` 函数调用：

```
$rc = 0xffff & system('cp
/home/httpd/logs/access.log /tmp/httpd.log');
if ($rc == 0) {
    print "system succeeded";
} else {
    print "system failed $rc";
}
```

该调用也可以配合 `or die` 子句使用：

```
system('cp /home/httpd/logs/access.log /tmp/httpd.log') == 0
or die "system failed: $?";
```

然而，你无法捕获通过 `system` 函数执行的命令输出。

# 模块和 CPAN

Perl 社区（以及 Linux 社区）的一大优势是它是一个开源社区。通过全面 Perl 存档网络 `CPAN` 支持 Perl，`CPAN` 是代码镜像网络。大多数 `CPAN` 由模块组成，这些模块是可重用的代码块，可以执行有用操作，就像程序员的函数一样。这些模块在构建 Perl 程序时有助于加速开发并避免重复造轮子。

Perl 自带了一套标准模块。这些模块包含了你最初使用 Perl 需要的大部分功能。如果你需要使用 Ubuntu 未安装的模块，可以使用 `CPAN`（标准模块之一）将其他模块下载并安装到你的系统中。在 `www.perl.com` 上，可以使用 `CPAN`（标准模块之一）下载并安装其他模块到你的系统中。

虽然将一个字符串替换为另一个似乎是一项相当细微的任务，但在另一种语言（例如 C）中实现相同功能所需的代码除非有外部库的额外子程序支持，否则是相当困难的。

# 使用 Perl 安装 CPAN 模块

你可以使用 Perl 交互式地从 `CPAN` 存档下载并安装 Perl 模块，使用 `-M` 和 `-e` 命令。通过如下方式使用 Perl 开始：

```
# perl -CPAN -e shell
```

当你按下回车时，你会看到一些介绍信息，并被要求选择初始自动或手动配置，这在下载或安装之前是必须的。输入 `no` 并按回车让 Perl 自动配置下载和安装过程；或者如果你愿意，直接按回车手动配置下载和安装。如果你使用手动配置，必须回答关于路径、缓存、终端设置、程序位置等的问题。设置保存在当前目录下的 `.cpan` 目录中。

完成后，你会看到 `CPAN` 提示符：
`cpan>`
