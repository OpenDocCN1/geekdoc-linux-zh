
在编写 CGI 程序时，始终指定绝对路径。这可以防止攻击者欺骗你的脚本去执行同名的备用程序。

例如，永远不要编写这样的代码：

```
# 设置一个目录变量
DIR='pwd';nchop($DIR);
# 然后稍后使用...
sub some_function() {
open(EXTERNAL_SCRIPT, "$DIR/myprogram.pl");
}
```

也不要使用相对路径。相对路径指向相对于当前目录的位置。考虑下面这个脚本：

```perl
open(DATABASE, "search/data/clients.dat!");
while(<DATABASE>) {
    if($/ <@/contents{'search_term'}/gi) {
        $Count++;
        print("$fields[5] $fields[6] $fields[7]<br\n");
    }
}
close(DATABASE);
if($count < 1) {
    print("No matches!\n");
}
```

这无法识别硬路径。如果你移动了这个脚本，指向 `clients.dat` 的路径就会改变：

- 在 `/var/http` 中，脚本指向 `/var/http/search/data/clients.dat`。
- 在 `/etc/http` 中，脚本指向 `/etc/http/search/data/clients.dat`。

相反，请指向绝对路径，如下：

```perl
open(DATABASE, "/var/http/ourcompany.net/search/data/clients.dat");
while(<DATABASE>) {
    if($/ <@/contents{'search_term'}/gi) {
        $Count++;
        print("$fields[5] $fields[6] $fields[7]<br\n");
    }
}
close(DATABASE);
if($count < 1) {
    print("No matches!\n");
}
```

这样，就不会有歧义。脚本只指向一个文件：

`/var/http/ourcompany.net/search/data/clients.dat`。

永远不要偏离这条规则，即使在启动简单程序时也是。例如，假设你这样做了：

```perl
system("date");
```

# 安全 Web 开发

第 16 章

453

甚至是这样：

```perl
$mydate='date';
```

如果攻击者可以修改 `$PATH` 并指向备选的 `date`，你的脚本将执行它。如果你执意以这种方式执行程序，请尝试以下替代方案：

```perl
system("/bin/date");
```

或者这个：

```perl
$mydate='/bin/date';
```

此外，考虑在启动时硬编码你的初始工作目录。为此，请使用 `chdir`。

## `chdir()`

`chdir()` 在 C 语言中来自 `unistd.h`，也是一个原生的 Perl 函数，它用于更改当前目录。它可以返回许多错误，可能会向你提示问题，例如目标实际上是否存在。作为额外措施，考虑在调用 `chdir()` 之后使用 `lstat()`。这将验证目标实际上是目录而不是符号链接。

## 文件

如果你的 CGI 程序创建或打开了文件，请遵循以下规则：

- 始终包含错误处理代码，以便在文件实际上不是文件、无法创建或打开、已存在、不存在、需要不同权限等情况下警告你。
- 注意你使用哪些目录来创建或打开文件。永远不要向世界可写或世界可读的目录写入文件。
- 始终显式设置文件的 `UMASK`。
- 将权限限制到尽可能。如果文件是用户输入的转储（例如访客列表），该文件应仅允许处理该文件的进程读取。
- 确保文件名中不包含元字符，如果文件是动态生成的，请包含一个筛选过程以剔除此类字符。

## 其他有趣的安全编程和测试工具

最后，表 16.3 列出了一些可以帮助你测试工作的的有趣工具。

### Linux 网络安全

第四部分

| 表 16.3 有趣编程和测试工具 |
| 变量 | 用途 |
| --- | --- |
| `lclint` | 适用于 ANSI C 的类似 lint 的检查器，检查危险的数据共享、忽略的返回值、空值、内存管理错误等许多。有关 `lclint` 的描述，请访问 http://www.doc.ic.ac.uk/lab/cplus/lclint/guide.html 或访问 http://ftp.sds.lcs.mit.edu/pub/lclint/guide.tar.gz。 |
| `mem_test` | 一个用于查找 C 程序内存泄漏的库。在 http://members.iquest.net/-jbuchae/mem_test.html 获取。 |
| `C Inside` | 一个源代码查看器，允许选择性地检查预处理结果，以确定哪些宏自由展开。在 http://www.thinkage.on.ca/share/ 获取。 |
| `GNU Nana` | 一个免费库，为 C 和 C++ 提供改进的断言检查和日志支持。更多信息请访问 http://www.cs.ntu.edu/au/homepages/pjm/nana-home/。 |
| `Plumber` | 一个用于识别 C 程序内存泄漏的工具。更多信息请访问 http://home.earthlink.net/-wenalley/plumber.html。 |
| `ObjectManual` | 为你的 C++ 程序动态生成 HTML 文档（如果你正在进行专业开发，此工具非常有用）。http://www.obsoft.com/Product/ObjMan.html |
| `DOC++` | 一个用于为 C++/Java 程序动态生成 HTML 文档的工具（如果你正在进行专业开发或对代码负责，此工具非常有用）。 |
| `cgihtml` | 一个从 C 程序写入 HTML 的库（当你不想费心编写 HTML 解析例时非常有用）。要获取它，请访问 http://www.eekim.com/software/cgihtml/。 |
| `MIME++` | 一个用于解析、创建和反序列化消息的 C 类库。更多信息请访问 http://www.sourceforge.net/projects/mime++。 |
| `Latro` | 一个用于识别 C 程序内存泄漏的工具。更多信息请访问 http://home.earthlink.net/-wenalley/plumber.html。 |
| `SCAT` | 一个用于识别 C 程序内存泄漏的工具。更多信息请访问 http://home.earthlink.net/-wenalley/plumber.html。 |
| `msystem` | 一个用于识别 C 程序内存泄漏的工具。更多信息请访问 http://home.earthlink.net/-wenalley/plumber.html。 |

# 安全 Web 开发

第16 章

453

| 变量 | 用途 |
| --- | --- |
| `crashme` | 适用于 ANSI C 的类似 lint 的检查器，检查危险的数据共享、忽略的返回值、空值、内存管理错误等许多。有关 `lclint` 的描述，请访问 http://www.doc.ic.ac.uk/lab/cplus/lclint/guide.html 或访问 http://ftp.sds.lcs.mit.edu/pub/lclint/guide.tar.gz。 |
| `mem_test` | 一个用于查找 C 程序内存泄漏的库。在 http://members.iquest.net/-jbuchae/mem_test.html 获取。 |
| `C Inside` | 一个源代码查看器，允许选择性地检查预处理结果，以确定哪些宏自由展开。在 http://www.thinkage.on.ca/share/ 获取。 |
| `GNU Nana` | 一个免费库，为 C 和 C++ 提供改进的断言检查和日志支持。更多信息请访问 http://www.cs.ntu.edu/au/homepages/pjm/nana-home/。 |
| `Plumber` | 一个用于识别 C 程序内存泄漏的工具。更多信息请访问 http://home.earthlink.net/-wenalley/plumber.html。 |
| `ObjectManual` | 为你的 C++ 程序动态生成 HTML 文档（如果你正在进行专业开发，此工具非常有用）。http://www.obsoft.com/Product/ObjMan.html |
| `DOC++` | 一个用于为 C++/Java 程序动态生成 HTML 文档的工具（如果你正在进行专业开发或对代码负责，此工具非常有用）。 |
| `cgihtml` | 一个从 C 程序写入 HTML 的库（当你不想费心编写 HTML 解析例时非常有用）。要获取它，请访问 http://www.eekim.com/software/cgihtml/。 |
