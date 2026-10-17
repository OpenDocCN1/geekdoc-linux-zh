
CGI 程序最常见的应用之一是在 Web 与其他 Internet 服务之间架起桥梁。实现这一点的简单方法是为 UNIX 命令行程序提供一个简单的 CGI 包装器，该程序可以执行请求所需的实际工作。这非常符合 UNIX 哲学，即组合简单的工具来完成复杂的任务。当你可以在他人的工作基础上进行构建时，通常不需要网关程序去发明轮子并完全重造一个服务。

HTML 和 CGI 标准共同努力，通过 `<ISINDEX>` 标签使这种方法尽可能简单。当浏览器在 HTML 文档中注意到 `<ISINDEX>` 标签时，它会将文档标记为可搜索索引，并允许用户输入术语进行搜索。当用户提交回复时，客户端检索与包含 `<ISINDEX>` 标签的文档相同的 URL，并如下如下添加用户的搜索术语：

```
http://www.vpizza.com/cgi-bin/isindex.pl?arg1+arg2+arg3
```

用户在搜索框中输入的单词紧随搜索标记之后；浏览器会将空格替换为加号。此外，非字母数字字符经过特殊编码；虽然这种编码在 `perl` 中相对容易还原，但在其他语言（如 C 或 Bourne shell）中进行解码可能会非常烦恼。为了让 `<INDEX>` 脚本更易开发，服务器会将从客户端 `<INDEX>` 查询中接收的信息转换为 CGI 脚本的命令行参数；输入的每个单词都是一个不同的参数。例如，这个愚蠢的 Bourne shell 脚本简单地回显了用户输入的术语：

```
#!/bin/sh
echo Content-type: text/plain
echo
echo $@
```

如你所见，此功能让 `<INDEX>` 脚本变得相当简单且直接；为了创建更复杂的应用程序，大多数人使用 HTML 表单。因为它们很简单，`<INDEX>` 脚本通常写得很快且略有些草率。你应该记住，所有的 CGI 脚本都有成为安全隐患的可能，在编写 `<INDEX>` 脚本时请务必遵循这些指南：

- 检查脚本是否带有命令行参数运行。如果是，则应该打印搜索指令，包括 `<INDEX>` 标签。
- 在执行操作之前检查参数的有效性（如果你使用像 `perl` 或 `shell` 脚本这样的解释型语言，这一点很重要，因为某些字符对解释器具有特殊含义）。
- 执行适当的操作并返回结果，且结果前要正确地带有 `Content-type` 头部。

### 示例 11-1：finger.pl，一个使用 `<INDEX>` 标签的 WWW finger 网关。

```
#!/usr/local/bin/perl
#
## finger.pl 一个指向 finger 服务的 <INDEX> 网关
#
```

```perl
if ( $$ARGV < 0 ) {
  &print_header("Finger2Web Gateway");
  &print_form;
  &print_footer;
  exit;
}
elsif ( $$ARGV > 0 ) {
  &print_header("Finger2Web Error");
  &print_form;
  print "The Finger Gateway takes only a single argument.";
  print "Please try again.\n";
  &print_footer;
  exit;
} else {
  $user = ARARG[0];
  if (! &safety_check($user)) {
    &print_header("Finger2Web Error");
    &print_form;
    print "You've submitted a request with an illegal character.";
    print "Please try again.\n";
    &print_footer;
    exit;
  }
  unless(open(FINGDATA,\$finger $user|)) {
    &print_header("Finger2Web Error");
    &print_form;
    print "Fatal Error executing the finger command.\n";
    &print_footer;
    exit;
  }
  &print_header("Finger2Web Results for $user");
  &print_form;
  print "<PRE>\n";
  while (<FINGDATA>) {
    print $$;
  }
  print "</PRE>\n";
  close(FINGDATA);
  &print_footer;
}
```

```perl
################################################
## 子例程序
################################################

# 确保参数是安全的
sub safety_check {
    local ($tocheck) = @_;
    $tocheck =~ /^[a-zA-Z0-9_\+\.\-]+;
}

# 打印头部
sub print_header {
    local ($title) = @_;
    print "Content-type: text/html\n\n";
    print "<html><head><title>$title</title></head>\n";
}

# 打印表单
sub print_form {
    print "<ISINDEX>\n";
    print "<p>Enter a username:\n";
    print "<input type='text' name='user'>\n";
    print "<input type='submit' value='Search'>n";
}

# 结束 HTML
sub print_footer {
    print "</body>\n";
    print "</html>\n";
}
```

# 第11 章：面向程序员的高表单

当你检查 11-1 中的代码时，可以看到它会检查参数以找到是如何被调用的。这些参数可以通过两种方式提供。你可以将网关的 URL 链接到文档并允许用户使用搜索输入框，如下：

我们提供 `<A href="cgi-bin/finger.pl">finger 网关</A>`

你也可以将它们添加到超链接的 URL 中：

```
<a href="cgi-bin/finger.pl?jem@sunsite.unc.edu">Finger me</a>
```

每当它返回结果或错误消息时，网关都会重新打印 `<ISINDEX>` 标签和搜索指令，并用水平线与其他正文隔开。这使用户可以方便地检查多个地址，而无需使用浏览器的后退按钮返回搜索页面。

## 处理 HTML 表单

在第 10 章“简单表单”中，你学习了如何使用 `<FORM>` 标签在 HTML 页面中创建交互区域。虽然你可以使用预写的 CGI 程序（如 `gform`）来处理结果，但这些程序受限于其简单性。通过“自己编写” CGI 脚本来处理你创建的表单，你可以获得更大的灵活性。

### 表单结构与 CGI

浏览器可以通过两种方式将 HTML 表单中的数据传递到服务器：GET 和 POST。你通过 `<FORM>` 标签的 `METHOD` 属性指定它们，如下：

```html
<HTML>
<HEAD>
<TITLE>Sample Guestbook</TITLE>
</HEAD>
<BODY>
<H1>Sample Guestbook</H1>
<FORM METHOD=POST ACTION="/cgi-bin/guest.pl">
Full name:
<INPUT TYPE=TEXT SIZE=30 NAME="fullname"><BR>
E-mail address:
<INPUT TYPE=TEXT SIZE=20 NAME="e-mail"><BR>
<P>
Comments:<BR>
<TEXTAREA COLS=60 ROWS=15 NAME="comments"></TEXTAREA>
<BR>
<INPUT TYPE=SUBMIT VALUE="Sign Guestbook">
<HR>
You can see <A HREF="/guests/guestbook.txt">
what other people have written</A>
</BODY>
</HTML>
```

## 第 11 章：面向程序员的高级表单 395

![](img/71cea268c234ed25390a8ed93b74a136_420_0.png)
