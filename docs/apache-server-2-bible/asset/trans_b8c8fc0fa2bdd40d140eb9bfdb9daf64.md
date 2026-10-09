

这将映射以下示例 URL 请求：

```
http://www.domain.com/~joe/cgi-bin/search.cgi?author=kabir
```

到以下物理文件：

```
/home/joe/cgi-bin/search.cgi?author=kabir
```

当然，如果你不喜欢将用户子目录设置为全局可读（即 public_html），你可以通过为用户创建一个 Web 分区（或目录）并为他们提供独立的目录来托管他们的个人主页，从而解决此问题。以下是一个示例：

```
ScriptAliasMatch ^~([a-z]!+)/cgi-bin/(.*) /www/$1/cgi-bin/$2
```

这匹配针对 www/username/cgi-bin/scriptname 的请求。由于此目录不在用户的家庭目录（/home/username）中，作为系统管理员，你可能能够对其进行更好的控制。

## 使用 AddType 创建新的 CGI 扩展名

如果你想在特定目录中创建新的 CGI 程序扩展名，也可以使用 .htaccess（或 AccessFileName 指令指定的文件）。

在你能使用基于目录的访问控制文件（.htaccess）添加新扩展名之前，必须如下创建 <Directory> 容器：

```
<Directory "/path/to/your/directory">  
  Options ExecCGI -Indexes  
  AllowOverride FileInfo  
</Directory>
```

目录容器内的第一条指令告诉 Apache，你希望在此目录中启用 CGI 程序执行，并出于安全考虑禁用目录列表功能。第二条指令告诉 Apache 在基于目录的访问控制文件（.htaccess）中启用 FileInfo 功能。此功能允许你在基于目录的访问控制文件中使用 AddType 指令。

要添加一个新的 CGI 程序扩展名（.wizard），你需要做的就是在目录中创建一个 .htaccess（或你在 AccessFileName 指令中指定的任何名称）文件，内容如下：

```
AddType application/x-http-cgi .wizard
```

然后，将该目录中现有的 CGI 程序重命名为带有 .wizard 扩展名，并通过浏览器请求它。请确保目录和 CGI 程序的所有文件权限设置都配置为允许 Apache 读取和执行。

## 运行 CGI 程序

如果你是一位 Apache 管理员，你很可能需要设置 CGI 程序，甚至可能知道如何编写它们。在本节中，我将讨论创建非常简单的 CGI 程序的基础知识。由于这不是一本 CGI 编程书，我不提供关于 CGI 编程的深入覆盖。我的重点在于揭示有关 CGI 程序的内容，以帮助 Apache 管理员更好地管理其支持 CGI 的网站。

本节中的许多示例使用 Perl。如果你的系统上没有 Perl，你可以从 **www.perl.com** 获取源代码，或者可能获取二进制文件。尽可能为系统编译二进制文件，而不是信任由他人创建的二进制文件，这是一种好的做法。

## 使用 Perl 编写 CGI 脚本

CGI 脚本编写等同于 Perl 脚本编写；依我拙见，Perl 是各种脚本语言中的王者，正是 Perl 推广了 CGI 脚本编写，因为它因 Perl 而广受欢迎。作为又一名 Perl 黑客，自 1995 年以来我一直在编写基于 Perl 的 CGI 脚本，并且我仍继续使用 Perl 来处理中小型的 Web 解决方案。由于这不是一本 Perl 编程书，我不会介绍如何一般性地编写 Perl 脚本。相反，我将讨论如何使用 Perl 编写 CGI 脚本。如果你不熟悉 Perl，我建议尽快阅读一本 Perl 编程书籍。

在使用 Perl 编写 CGI 脚本时，应遵循以下一系列准则或编程风格。具体如下：

- **分离内容与逻辑——将内容排除在脚本之外。** 使用 HTML 或 XML 模板来确保 CGI 脚本的界面方面不在脚本本身中。这将确保非程序员用户（例如图形或 HTML 专家）可以轻松地更改界面。
- **使用配置文件——切勿在脚本中硬编码可自定义信息。** 使用配置文件来读取信息。这将使你的脚本更具灵活性。
- **规范化用户数据——在收集用户数据以供将来使用时，确保在将数据存储在文件或数据库中之前规范化数据。** 例如，如果你收集访问者的电子邮件地址，将每个电子邮件地址规范化为指定的大小写（大写或小写），并修复用户遗漏和数据输入错误是个好主意。我见过许多案例，AOL 用户在网络表单中书写电子邮件地址时漏掉了 .com，或者在 @ 和名称或主机名之间多加了空格。我还见过数千个案例，用户将他们的名字输入为大写或小写。试想一下，当你使用未规范化的名字（用户自己在你的网络表单中输入的）来定制时事通讯时，会给他们留下什么样的印象，或者当你的邮件列表系统发现数千个“@AOL”或“user @ aol”类型的数据错误时，你会收到多少退信。
- **对用户数据进行合理性检查——CGI 脚本经常是许多安全攻击的目标。** 如果你的 CGI 脚本接受用户输入，请确保在使用用户数据之前对其进行验证。

**提示**：在你开始重新发明轮子之前，检查综合 Perl 档案网络（CPAN）网站 http://cpan.perl.com 以查找现有的 Perl 模块，你可以使用它们来解决当前问题，或通过重用现有 CPAN 模块来减少开发工作量。在本节中，我使用了许多 CPAN 模块来构建 CGI 脚本。每当你在本文讨论的任何脚本中看到列出的模块时，你可以使用随标准 Perl 一起发布的 CPAN 模块将该模块添加到你的系统中。

**注意**：Windows 版的 Apache 用户应查阅 Perl 文档了解如何使用 CPAN 模块，因为这不同于本文讨论的标准方法。有关详细信息，请参阅本书中 Windows 特定部分。

例如，假设你看到一个脚本列出了一个名为 HTML::Template 的模块，你希望安装此模块以便运行使用它的脚本。要安装 CPAN 模块，请以 root 用户身份从命令行提示符运行 `perl -MCPAN -e shell`。

**注意**：如果你是第一次运行 `perl -MCPAN -e shell` 命令，系统将要求你配置当前的 CPAN.pm 模块，该模块用于安装其他 CPAN 模块。只需按照说明和提示配置 CPAN.pm 模块，然后继续以下讨论。

在到达 CPAN 提示符后，运行 `install HTML::Template` 命令来安装该模块。CPAN 模块将为你安装此模块。如果它对依赖性发出警告，你可能需要在安装依赖其他 CPAN 模块的模块之前先安装其他一些模块。完成后，从 CPAN 提示符运行 `quit` 返回 shell。

**提示**：如果你不想使用 `perl -MCPAN -e shell` 运行交互式 CPAN shell 来安装模块，可以改为运行 `perl -MCPAN -e ‘CPAN::Shell->install(module_name)’`。例如，`perl -MCPAN -e shell ‘CPAN::Shell->install(HTML::Template)’` 将安装 HTML::Template 模块。你也可以从 shell 脚本中运行此命令。

## 分析一个简单的 CGI 脚本

CGI 脚本通常用于获取用户输入并根据输入执行一个或多个操作，然后在 HTML 页面中返回结果。在本节中，我将向你展示如何创建一个简单脚本来入门并理解 CGI 脚本编写的概念。我们将在这里开发的脚本将执行单一任务：它将获取用户的完整姓名，正确地格式化它，并返回个性化的问候消息。列表 12-2 展示了执行上述功能的 greetings.pl 脚本。

## 列表 12-2: greetings.pl

```
#!/usr/bin/perl
#
#    Name: greetings.pl
#
#    Purpose:
#
#    Show a greeting message
#
######################################################

use strict;
use CGI;

#
# Get user data
#
my $query = new CGI;
my $name = $query->param('name');

#
# Process data
#
$name         = lc($name);
my @strArray = ();


foreach my $str (split(/ ,.$name)) {
    push(@strArray, ucfirst($str));
}

my $formattedName = join(' ', @strArray);

#
# Display results
#
print $query->header;
print $query->start_html('Greetings');
print $query->p('Hello ' . $formattedDName . ',');
print $query->p('Thanks for coming to our Web site.');
print $query->end_html;

#
# Terminate
#
exit 0;
```

