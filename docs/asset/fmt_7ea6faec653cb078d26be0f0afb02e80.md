
```perl
$file ||
die "Agrpdelu: Utility for deleting users from Apache group files.\n"
"Usage: Agrpdelu group username filespec\n";
```

# 提取文件名：

```perl
$file =~ /(.+)/;
$safefile = $1;
```

# 将当前的组成员读取到关联数组：

```perl
%groups = &GetGroupMembers($safefile);
```

# 检查用户是否在组内：

```perl
$groups($group) =~ /\b$user\b/ ||
die "User \"$user\" is not a member of group \"$group\.\n";
```

# 首先为此列表的所有成员创建一个数组：

```perl
(@oldmembers) = $groups($group) =~ /(\w+)/g;
```

# 清空该组当前的成员列表：

```perl
$groups($group) = "";
```

```perl
# 将除要删除成员以外的所有成员添加到新字符串：

foreach $member (@oldmembers) {
    if ($member ne $user) {
        $groups{$group} .= "$member";
    }
}

# 将数组写入组文件：
&SetGroupMembers($safefile, %groups);

# 结束
```

以下列表显示了基本步骤：

- 1. 脚本将组定义文件读取到 `%groups` 关联数组中。
- 2. 脚本使用语句 `(@oldmembers) = $groups{$group} ~ /(\w+)/g;` 将新组的成员身份存储在 `@oldmembers` 数组中。该语句可以工作。`$groups{$group}` 是包含所有由空格分隔的组名的字符串。应用 `/(\w+) /g` 运算符对名称进行模式匹配，将所有内容保存到 `$1`、`$2`，然后存储在 `@oldmembers` 中。
- 3. 脚本通过将新组的成员身份设置为空字符串来强制初始化。
- 4. 脚本通过遍历 `@oldmembers` 数组的元素重建新组的成员列表： `$groups{$group}`，将每个元素添加到 `$groups{$group}`，直到它与要删除的用户名匹配。
- 5. 脚本将 `%groups` 关联数组写回组定义文件。

再次，你可以复用 `GetGroupMembers()` 和 `SetGroupMembers()` 函数。

## 从这里...

本章描述了用户验证如何将用户验证与访问限制相结合，以确保你的服务器在需要的范围内保持开放，且不再开放。本书关于服务器安全和 Perl 还有很多精彩内容：

- 第 9 章“理解 CGI 安全”提到你可以在多个 perl 脚本之间维持已身份验证会话的状态。
- 第 10 章“网站管理”包含了关于如何使用 Perl 辅助管理你的 Web 服务器的信息。

![](img/13bc4258f89bbca754b8ea331d6f5de2_531_0.png)

## 第 10 章

## 网站管理

作者 Shelley Powlers

## 目录

- 处理 Web 服务器日志文件
- 从日志文件生成 HTML 输出
- 审查 AccessWatch 日志分析器
- 理解文件维护
- 理解机器人和机器人排除标准
- 配置常用的 Web 服务器
  - O'Reilly 的 WebSite
  - NCSA httpd
  - Apache
- 检查其他文件和网站管理问题
- 从这里

之前的章节也描述了静态和动态内容的创建。从这些文件的创建产生了两个事实：文件被生成了，如果你的网站要保持最高效率运行，就必须对其进行维护。

取决于你的 Web 服务器，你需要在安装服务器时进行某些配置，并需要进行定期维护。涉及内容的详细描述是本书的范畴，但某些维护任务可以通过 Perl 程序完成。本章讨论了 Apache 服务器（来自 Apache）和 NCSA httpd 服务器。

了解如何以及何时访问你的网页和应用程序的最有用工具是你的 Web 服务器日志文件。该日志文件可以显示哪些页面被访问，由谁访问（通常是泛义的），以及何时。如果你的网站运行通用网关接口 (CGI) 或其他应用程序，你可能需要从读取器中删除孤立进程。你的网站可能会被搜索引擎访问，例如 WebCrawl (http://www.webcrawler.com)，将网站添加到它们的集合中。这些访问者会快速查看一眼并离开，有时则不。

## 处理 Web 服务器日志文件

每个 Web 服务器都提供某种日志文件。该日志文件可以显示哪些页面被访问，由谁访问（通常是泛义的），以及何时。如果你的网站运行通用网关接口 (CGI) 或其他应用程序，你可能需要从读取器中删除孤立进程。你的网站可能会被搜索引擎访问，例如 WebCrawl (http://www.webcrawler.com)，将网站添加到它们的集合中。这些访问者会快速查看一眼并离开，有时则不。

使用以下代码可以获取行内容，这与之前的代码示例相同，只是添加了 `split`

```perl
open(LOG_FILE, "<", $file_name) || die "Could not open log file.";
foreach $line(<LOG_FILE>) {
    // do some processing
    n($dns, $rfucser, $autouser, $dt1, $dt2, $cmethod, $comnd, $stat, $lnth) = split('', $line);

}
```

前面的代码拆分了本章前面“处理 Web 服务器日志文件”部分所示两个日志文件示例中的访问日志条目。你也可以如下将条目元素直接加载到数组中：

```perl
open(LOG_FILE, "<", $file_name) || die "Could not open log file.";
foreach $line(<LOG_FILE>) {
    // do some processing
    ($dns, $rfucser, $autouser, $dt1, $dt2, $cmethod, $comnd, $stat, $lnth) = split('', $line);

}
```

当你访问日志条目时，可以根据几个因素使用这些值生成 HTML。如果你想生成一个列出按文档访问次数的 HTML 文件，可以编写下面的代码：

```perl
#!/usr/local/bin/perl

use CGI;
$query = new CGI;

open(LOG_FILE, "<", $file_name) || die "Could not open log file."

```

Site line(<LOG_FILE>) {

foreach $line {

  // do some processing

  ($dns, $rfecuser, $auther,$dt1,$dt2,$commethod,$comnd,$stat,$lnth) = split('\n',$line);

  if (index($comnd, "somedoc.html") >= 0) {

    $counter++;

  }

}

}

```

然后你可以使用标准的 HTML 输出程序输出变量，如下：

```perl

print $query->header;

print $query->start_html('The Access Page');

print $query->hl('Accesses Per Page');

print "<p> Page somedoc.html was accessed " . $counter . " times";

```

另一种可以提供一些图形输出的方法是为每次访问打印一个星号 (*)。这种方法提供的输出与图 10.2 类似。

**图 10.2**：此图显示日志文件分析结果。

为了创建一个基于文本的图形，你应该修改代码使用 HTML 表格输出结果，如下例：

```perl

print $query->header;

print $query->start_html('The Access Page');

print $query->hl('Accesses Per Page');

print "<table cellpadding=5";

```

```perl

print "<td>somedoc.html </td>";

for (i = 1; $i <= $counter; i++) {

    print "*</td>";

}

print "</</td></tr></tr>";

print "</table>";
```
