
CGI 本身并不是一种编程语言，而是一个运行脚本的接口；如你所知，你可以使用任何语言编写 CGI 脚本，包括 `C`、`Java`、`Tcl`、`Shell` 脚本或 `Python`。当然，`Perl` 是最流行的，而且 `Perl` 的许多特性使其成为在安全意识环境中进行编程的理想选择。

为了探索这些特性，我们将简要介绍一个简单脚本的，允许网站访问者通过电子邮件请求产品的更多信息。这看起来似乎是一项毫无意义的任务，因为信息很容易通过 `HTML` 页面提供给用户；但它之所以流行，是因为它允许网站所有者建立潜在客户的电子邮件列表。

首先是请求部分的代码：

```html
<html>
<body>

<form method=post action=request.pl>
您的电子邮箱地址： <input type=text name="email"><br>
您的姓名： <input type=text name="name"><br>
请选择您想要获取技术规格的产品：
<select name=document>
<option value="dvd.txt">DVD 播放器</option>
<option value="vcr.txt">VCR</option>
<option value="tv_widescreen.txt">宽屏电视</option>
<option value="tv_flatscreen.txt">平板电视</option>
</select>
<br><br>
<input type=submit>
</form>

</body>
</html>
```

该脚本会打开传递给它的文件名，将内容读取到 `$content` 中，打开一个管道发送到 `sendmail`，然后向给定的地址编写电子邮件。我们假设 `dvd.txt`、`vcr.txt`、`tv_widescreen.txt` 和 `tv_flatfullscreen.txt` 文件都存在 `/var/www/html/docs/` 目录下，并且可能包含产品的技术规格列表。

## 服务加固

你可能会惊讶地发现，此脚本有两种被破坏的方法，允许攻击者查看 Web 服务器上任何执行脚本的用户可读的任何内容（通常是如 `www` 或 `nobody` 的特殊用途账户）。这两种方法都是程序员忽略“永远不要信任用户输入”这一黄金准则的直接结果。

第一个问题出现在 `$document` 变量中。虽然 `HTML` 表单仅为该变量定义了四种可能的值，但没有什么能阻止恶意用户将 `HTML` 代码保存到本地磁盘，编辑表单以包含其他值，然后提交。如果表单使用 `GET` 方法——即数据通过查询字符串传递给脚本——攻击者可以选择不使用表单，而是通过浏览 URL 来手动提交数据，例如：

```
http://www.example.com/cgi-bin/request.pl?name=test&email=evil@cracker.org&document=../../etc/passwd
```

这样做的结果是 `$document` 变量可能包含任何文件名——它不仅限于 `HTML` 表单中提供的四个选项。因为没有对此变量进行任何检查，黑客可能会强制脚本尝试读取（并邮寄内容）系统上的任何文件。即使在 `open()` 调用中将文件名指定为 `/var/www/html/docs/$document` 也不起保护作用：黑客可以很容易通过 `../` 语法请求 `/var/www/html/docs` 目录之外的文件，例如：

```
http://www.example.com/cgi-bin/request.pl?name=test&email=evil@cracker.org&document=../../etc/passwd
```

由于我们想要的文件格式都是 `.txt`，我们本可以使用一系列正则表达式来过滤掉包含 `../` 或不以 `.txt` 结尾的用户输入；但预测用户可能传递的所有恶意字符串是繁琐且容易出错的。消除的一种简单方法是重写脚本，使 `$document` 变量永远不会传递给 `open()`：

```perl
#!/usr/bin/perl

use CGI;

$q = new CGI;
$name = $q->param("name");
$email = $q->param("email");
$document = $q->param("document");

if ($document eq 'dvd.txt') {
  $filename = 'dvd.txt'
} elsif ($document eq 'vcr.txt') {
  $filename = 'vcr.txt'
} elsif ($document eq 'tv_widescreen.txt') {
  $filename = 'tv_widescreen.txt'
} else {
  $filename = "tv_flatscreen.txt"
}

open (IN, "< /var/www/html/docs/$filename");
# ... (省略后续处理逻辑) 
```

## 服务安全 405

这在大型脚本中是一个问题。为了辅助这个问题，`Perl` 提供了自己的安全机制，称为`污染模式 (taint mode)`。在污染模式下运行时，`Perl` 会将所有外部数据（包括环境变量、命令行参数和 `CGI` 输入）视为“受污染的”，并且在对这些数据进行清洗之前，拒绝对它们执行任何潜在的不安全操作。被认为是潜在不安全的操作包括写入文件、`exec()`、`system()` 以及任何其他可能影响外部文件或进程的操作。

受污染变量的一个有趣特性是，它们会污染它们所使用的任何其他变量；因此，在下面的示例中，`$fullname`（因为是用户提供的而被认为是污染的）导致导致变量 `$firstname` 和 `$surname` 也变为受污染状态：

```
$fullname = $q->param("fullname");
($firstname, $surname) = split (/ /, $fullname);
# 使用空格作为分隔符分割字符串 $fullname。
```

污染不会扩散的唯一表达式是正则表达式，而这就是清洗受污染数据的方法：`Perl` 假设你的表达式足够健壮，能够使数据变得安全。

通过调用带有 `-T` 标志的 `Perl` 解释器启用污染模式（即 `#!/usr/bin/perl -T`）。

## CGIWrap

`CGI` 脚本的问题之一在于，它们是以 Web 服务器的权限运行的，而不是创建它们的用户的权限。想象你经营着一家 Web 托管公司。用户 `Adele` 在这里托管她的公司网站，并使用一个 `CGI` 脚本，允许员工通过交互式日历选择下周的可工作班次。员工选择的班次被存放在由 `CGI` 脚本创建的文本文件中，而该文件由运行服务器的用户账户所有——通常是 `www` 或 `nobody`。心怀不满的员工 `Tara` 注册了一个账户，并创建了自己的恶意 `CGI` 脚本，该脚本尝试删除她传递过去的文件名。由于该脚本也将以服务器运行的用户身份执行，因此，无论如何如何使用 `chmod`，都无法阻止 `Tara` 删除 `Adele` 的文本文件。

这可能是一个稍显刻意的例子，但它确实说明了所有 `CGI` 脚本都以相同用户身份运行的基本问题。解决方案是 `[CGIWrap](CGIWrap)`，它是一个用于 `CGI` 脚本的封装程序，使它们以创建者的身份执行，而不是 Web 服务器。你可以认为这仅仅是用另一个问题取代了另一个问题——毕竟，现在使得不安全的 `CGI` 脚本能够删除用户自己的文件；然而，意识到他们自己的个人文件可能面临风险，往往会使用户具有更强的安全意识。

## 406 Linux 网络安全

## PHP

恶意用户输入的问题也会影响像 `PHP` 这样的脚本语言；尽管 `PHP` 的正则表达式远没有 `Perl` 强大，但它们仍然可以用于检查用户提交的数据。如果你理解了之前关于 `Perl` 中数据检查的章节，将相同的原理应用于 `PHP` 将是毫不费力的。

`PHP` 的一个有趣特性是 `CGI` 变量的可访问方式。在 `Perl` 中，你必须先读取查询字符串并将其分成组成部分，将数据保存到你的变量中（通过 `CGI .pm` 模块使此任务变得简单）。`PHP` 提供了自动变量赋值选项（称为注册全局变量——这是一个有用但相当不安全的特性），其中会自动创建变量来存储传递给脚本的数据。这些变量通过查询字符串传递。考虑以下 URL：

```
http://example.com/feedback.php?name=peter&email=peteexample.org&message=great%20site
```

如果启用了注册全局变量，当脚本执行时：`$name`、`$email` 和 `$message`。然而，由于攻击者可以向查询字符串添加所需的任何数据，他可以将任何变量注入脚本中。下面的脚本片段说明了这种危险性：

```
if ($password eq "letmein") {
    $authenticated = "yes"
}
....
```

```
if ($authenticated eq "yes") {
    // 显示数据或提供仅限管理员访问的功能
}
```
