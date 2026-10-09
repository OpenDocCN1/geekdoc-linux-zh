
3. 前导字符（*）出现零次或多次，后跟
4. 一个右花括号，后跟
5. 一个空格。

（在字符类的第一个位置使用脱字符指定所有不匹配后续字符的字符类，因此 [`^]`] 匹配任何不是右花括号的字符。）

```
$ cat re5b.pl
$string = "A line {remove me} may have two {keep me} pairs of braces.";
$string =~ s/([^\]`*}.*}}/ ;;
print "$string\n";

$ perl re5b.pl
A line may have two {keep me} pairs of braces.
```

Perl 提供了一种快捷方式，允许你指定非贪婪匹配。在下面的示例中，[`.*?\]` 中的问号使得正则表达式匹配以左花括号开头、后跟任意字符字符串、再以右花括号结尾的最短字符串。

```
$ cat re5c.pl
$string = "A line {remove me} may have two {keep me} pairs of braces.";
$string =~ s/.[\*?] ;;
print "$string\n";

$ perl re5c.pl
A line may have two {keep me} pairs of braces.
```

# 括号表达式

如第 1094 页所述，你可以将正则表达式的部分用括号括起来，并在替换字符串中引用这些部分。大多数 Linux 实用工具使用带引号的括号（即 `\(` 和 `\)`）来括起正则表达式。在 Perl 正则表达式中，括号是特殊字符。Perl 省略了反斜杠，并使用不带引号的括号来括起正则表达式。要在 Perl 正则表达式中指定括号作为普通字符，你必须将其加引号（第 1093 页）。

下一个示例使用不带引号的括号在正则表达式中括起表达式的部分。然后，它将括号表达式匹配的字符串部分赋值给原本持有 Perl 最初搜索正则表达式的字符串的变量。

首先，程序将字符串 *My name is Sam* 赋值给 `$stg`。下一条语句在 `$stg` 持有的字符串中查找正则表达式 `/. *My name is .*/` 的匹配。由括号括起的正则表达式部分匹配 *Sam*；替换字符串中的 `$1` 匹配正则表达式的第一部分（在此例中也是唯一部分）括号括起的内容。结果是，`$stg` 中持有的字符串被字符串 *Sam* 替换。

```
$ cat re11.pl
$stg = "My name is Sam";
$stg =~ s/My name is (.*)/$1/;
print "Matched: $stg\n";

$ perl re11.pl
Matched: Sam
```

下一个示例使用正则表达式解析字符串中的数字。初始化两个变量以包含两个数字的字符串。程序的第三行使用正则表达式隔离字符串中的第一个数字。`\D` 匹配零个或多个不包含数字的字符字符串：`\D` 特殊字符匹配任何单个非数字字符。末尾的星号使正则表达式的这部分执行贪婪匹配，且不包含数字（它匹配 **What** is ）。括号括起的正则表达式 `\d+` 匹配一个或多个数字的字符串。括号不影响正则表达式匹配的内容；它们允许替换字符串中的 `$1` 匹配括号括起的正则表达式所匹配的内容。最后的 `.*` 匹配字符串的剩余部分。这一行将字符串中第一个数字的值赋值给 `$string`。

下一行类似，但将字符串中的第二个数字赋值给 `$string2`。print 语句显示这些数字以及从第一个数字中减去第二个数字的结果。

```
$ cat re8.pl
$string = "What is 488 minus 78?";
$string2 = $string;
$string =~ s/\D+(\d+).*\$1/;
$string2 =~ s/\D+(\d+)\D+(\d+).*\$1/;

print "$string\n";
print "$string2\n";
print $string - $string2, "\n";

$ perl re8.pl
488
78
410
```

接下来的几个程序展示了在正则表达式中不使用引号括起部分时，若不希望括起正则表达式部分的某些陷阱。其中第一个程序试图在字符串中使用正则表达式里的不带引号的括号来匹配括号，但失败了。正则表达式 `ag( ed)` 匹配与正则表达式 `ag` 相同的字符串，因为括号是特殊字符；正则表达式不匹配字符串 `ag(ed)`。

```
$ perl -le 'if ("ag(ed)") {print "true";} else {print "false";}'
false
```

下一个示例中的正则表达式在每个括号前加反斜杠对括号加引号，使 Perl 将其解释为普通字符。匹配成功。

```
$ perl -le 'if ("ag(ed)" =~ /ag\(ed\)/) {print "true";} else {print "false";}'
true
```

接下来，Perl 在正则表达式中发现未配对的括号：

```
$ perl -le 'if ("ag(ee" =~ /ag(e/) {print "true";} else {print "false";}'
Unmatched ( in regex; marked by <-- HERE in m/ag/( <-- HERE e/ at -e line 1.
```

当你给括号加引号时，一切正常，Perl 找到了匹配：

```
$ perl -le 'if ("ag(ed)" =~ /ag\(ed\)/) {print "true";} else {print "false";}'
true
```

# CPAN 模块

CPAN（Comprehensive Perl Archive Network，全面 Perl 归档网络）在其网站（www.cpan.org）上提供 Perl 文档、常见问题解答、模块（第 1045 页）和脚本。它持有超过 16,000 个发行版（第 1045 页），并提供链接、邮件列表以及编译为在各种操作系统下运行的 Perl 版本（Perl 移植版）。查找模块的一种方式是访问 search.cpan.org 并使用搜索框，或点击该页面列出的模块类别之一。

本节解释如何从 CPAN 下载模块以及如何安装和运行模块。Perl 为模块提供了分层命名空间，使用双冒号（::）分隔名称组件。本节的示例使用名为 **Timestamp::Simple** 的模块，你可以在 search.cpan.org/dist/Timestamp-Simple 上阅读和下载该模块。时间戳是 **YYYYMMDDHHMMSS** 格式下的日期和时间。

要使用 Perl 模块，你首先下载包含该模块的文件。对于这个示例，search.cpan.org/~shoop/Timestamp-Simple-1.01/Simple.pm 网页右侧有一个标记为 **Download** 的链接。点击此链接并将文件保存到你想要工作的目录中。在该过程的最后一步安装模块之前，你不需要以特权用户身份工作。

大多数 Perl 模块以压缩的 **tar 文件**（第 176 页）形式提供。将下载的文件放入工作目录后，解压该文件：

```
$ tar xzvf Timestamp-Simple-1.01.tar.gz
Timestamp-Simple-1.01/
Timestamp-Simple-1.01/Simple.pm
Timestamp-Simple-1.01/Makefile.PL
Timestamp-Simple-1.01/README
Timestamp-Simple-1.01/test.pl
Timestamp-Simple-1.01/Changes
Timestamp-Simple-1.01/MANIFEST
Timestamp-Simple-1.01/ARTISTIC
Timestamp-Simple-1.01/GPL
Timestamp-Simple-1.01/META.yml
```

新创建目录中的 **README** 文件通常提供构建和安装模块的说明。大多数模块遵循相同的步骤。

```
$ cd Timestamp-Simple-1.01
$ perl Makefile.PL
Checking if your kit is complete...
Looks good
Writing Makefile for Timestamp::Simple
```

如果你正在构建的模块依赖于本地系统未安装的其他模块，运行 `perl Makefile.PL` 将显示一个或多个关于未找到先决条件的警告。即使缺少模块，此步骤也会写出 makefile。在这种情况下，下一步将失败，你必须在继续之前构建并安装缺失的模块。

下一步是对刚才创建的 makefile 运行 **make**。运行 **make** 后，运行 **make test** 以确保模块正常工作。

```
$ make
cp Simple.pm blib/lib/Timestamp/Simple.pm
Manifying blib/man3/Timestamp::Simple.3pm
```

```
$ make test
PERL_DL_NONLAZY=1 /usr/bin/perl "-Iblib/lib" "-Iblib/arch" test.pl
1..1
# Running under perl version 5.10.0000 for linux
# Current time local: Fri Sep 3 18:20:41 2010
# Current time GMT: Sat Sep 4 01:20:41 2010
# Using Test.pm version 1.25
ok 1
ok 2
ok 3
```

最后，以 root 权限运行安装模块：

```
$ sudo make install
Installing /usr/local/share/perl/5.10.0/Timestamp/Simple.pm
Installing /usr/local/man/man3/Timestamp::Simple.3pm
Writing /usr/local/lib/perl/5.10.0/auto/Timestamp/Simple/.packlist
Appending installation info to /usr/local/lib/perl/5.10.0/perllocal.pod
```

一旦你安装了模块，你可以使用 **perldoc** 显示告诉你如何使用该模块的文档。第 1043 页有一个示例。

某些模块包含 **SYNOPSIS** 部分。如果你安装的模块包含这样的部分，你可以通过将 **SYNOPSIS** 部分中的代码放入文件并将其作为 Perl 程序运行来测试该模块：

```
$ cat times.pl
use Timestamp::Simple qw{stamp};
print stamp, "\n";

$ perl times.pl
20100904182627
```
