
```
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
...
</VirtualHost>
```

如果要改用基于 IP 的动态虚拟主机，则将 UseCanonicalName 设置为 DNS 而不是 Off。

```
UseCanonicalName DNS
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

## 插值字符串

mod_vhosts_alias 模块支持各种插值字符串，每个字符串都以 % 符号开头，后跟一个数字。如你所见，%0 引用整个 Web 地址。%1 仅引用第一个段，%2 引用第二个段，%-1 引用最后一部分，而 %2+ 则从第二部分开始引用。例如，如果你只想使用 Web 地址的第二部分作为目录名，则可以使用以下指令：

```
VirtualDocumentRoot /var/www/hosts/%2/html
VirtualScriptAlias /var/www/hosts/%2/cgi-bin
```

在这种情况下，对 www.mygolf.com/html/mypage 发出的请求将仅使用 Web 地址的第二部分。这在 www.mygolf.com 中为 "mygolf"，并会求值为

```
/var/www/hosts/mygolf/html/mypage
```

如果你改用 %2+，例如 /var/www/hosts/%2/html，则对 www.mygolf.com/html/mypage 的请求会求值为

```
/var/www/hosts/mygolf.com/html/mypage
```

同样的方法也适用于 IP 地址，其中 %1 引用第一个 IP 地址段，%2 引用第二个，以此类推。

## 虚拟主机的日志

动态虚拟主机的一个缺点是，你只能为所有主机设置一个日志。不过，你可以创建自己的 shell 程序，以便从该日志中仅提取不同主机的条目。

```
LogFormat "%V %h %l %u %t \"%r\" %>s %b" vcommon
CustomLog logs/access_log vcommon
```

## IP 地址

以前面所示的标准方式实现动态虚拟主机将会减慢处理速度，因为服务器必须执行 DNS 查找，使用其 IP 地址来发现服务器的名称。你可以通过简单地使用 IP 地址作为虚拟主机的目录来避免此步骤。因此，对于 IP 虚拟主机 192.198.1.6，你将创建目录 /var/www/hosts/192.198.1.6，并为该主机的文档根目录创建一个 html 子目录。你可以使用 VirtualDocumentRootIP 和 VirtualScriptAliasIP 指令将 IP 地址用作目录名。现在 IP 地址可以直接映射到文档根目录名，不再需要 DNS 查找。另请确保在日志中包含 IP 地址，%A。

```
UseCanonicalName DNS
LogFormat "%A %h %l %u %t \"%r\" %>s %b" vcommon
CustomLog logs/access_log vcommon
VirtualDocumentRootIP /var/www/hosts/%0/html
VirtualScriptAliasIP /var/www/hosts/%0/cgi-bin
```

你可以根据需要将这些命令与其他虚拟主机条目混合使用。例如，要为非动态基于名称的虚拟主机指定文档根目录，你可以简单地使用 **VirtualDocumentRoot** 指令。换句话说，你可以为动态和非动态虚拟主机简单地使用相同的目录。你仍然可以根据需要为不同的非动态虚拟主机指定其他目录。在以下示例中，**www.mypics.com** 基于名称的虚拟主机使用动态虚拟主机指令 **VirtualDocumentRoot** 来设置其文档根目录。它现在使用 **/var/www/www.mypics.com/html** 作为其文档根目录。然而，CGI 目录则被设置为非动态目录，**/var/www/mypics/cgi-bin**。

```
UseCanonicalName Off

NameVirtualHost 192.168.1.5

<VirtualHost 192.168.1.5>
ServerName www.mypics.com
ServerAdmin webmaster@mail.mypics.com
VirtualDocumentRoot /var/www/%0/html
ScriptAlias /var/www/mypics/cgi-bin
...
</VirtualHost>
```

## 服务器端包含

服务器端包含（SSIs）旨在提供对网站内容的更精细控制，即 Web 页面本身。服务器端包含是放置在特定 Web 页面 HTML 代码中的 Apache 指令。你可以配置 Apache Web 服务器在特定 Web 页面中查找 SSI 指令并执行它们。首先，你必须使用带有 include 选项的 Options 指令来允许 SSI 指令。

### 包含选项

你需要指示服务器解析特定的 Web 页面。启用解析的最简单方法是指示 Apache 解析具有指定扩展名的 HTML 文件：通常，扩展名 .shtml 用于具有 SSI 指令的 Web 页面。事实上，在默认的 Apache 配置文件中，你可以找到以下条目以启用对 HTML 文件中 SSI 指令的解析。此处的 AddType 指令将 .shtml 类型添加为 HTML 文件类型，而 AddHandler 指令则指定 .shtml 文件将被解析（服务器解析）。

```
# To use server-parsed HTML files
AddType text/html .shtml
AddHandler server-parsed .shtml
```

与其创建单独的文件类型，你可以使用 XBitHack 指令让 Apache 解析任何可执行文件以查找 SSI 指令。换句话说，任何具有执行权限的文件（参见第 28 章）都将被解析以查找 SSI 指令。

SSI 指令的操作方式与编程语言中的语句非常相似。你可以定义变量、创建循环，并使用测试来选择替代指令。SSI 指令由一个元素后跟可赋值的属性组成。SSI 指令的语法如下所示：

```
<!--#element attribute=value ... -->
```

你可以将元素视为与编程语言中的命令类似地运行，而将属性视为其参数。例如，要为变量赋值，你使用 set 元素并将变量赋值作为其属性。if 指令会显示给定 Web 页面上的任何后续文本。if 指令将其属性 expr 用作要测试的表达式。测试能够使用标准比较运算符（如 <=、!= 或 =）比较两个字符串。测试中使用的变量将使用 $ 运算符进行求值。

```
<!--#set myvar="Goodbye" -->
<!--#if expr="$myvar = Hello" -->
```

其他有用的 SSI 元素有 exec，它执行 CGI 程序或 shell 命令，将文件内容读入 Web 页面并执行 CGI 文件。echo 元素显示诸如日期、文档名称和页面 URL 等值。使用 config 元素，你可以配置某些值，例如日期或文件大小。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_533_0.png)

## ABC Amber CHM 转换器试用版

请注册以移除此横幅。

http://www.processestext.com/abcchm.html

## PHP

PHP（PHP 超文本预处理器）是一种专为 Web 页面设计而成的脚本语言。启用 PHP 的页面允许你创建动态 Web 页面，使其能够执行任务而不仅仅是显示数据。PHP 是 Apache 软件基金会的官方项目。你可以在 www.php.net 了解更多关于 PHP 的信息。

与 CGI 程序不同，CGI 程序是与 Web 页面分开执行的，PHP 命令作为标签嵌入在页面本身中，就像 SSI 命令一样。对这些命令的解释和执行支持由 Web 服务器直接提供。这种嵌入式支持在 Apache 中通过 mod_php 模块（`/etc/httpd/conf.d/php.conf` 配置文件）启用。与必须单独构建程序以在 Web 服务器外部调用和运行不同，使用 PHP，这样的命令嵌入在 Web 页面中并由 Web 服务器运行。只要执行任务，Web 服务器始终保持完全控制。然而，也可以在 CGI 模式下实现 PHP，其中 PHP 页面被构建为单独的程序，由 Web 页面调用，就像基于 Perl 的 CGI 程序一样。

PHP 具有灵活且强大的编程能力，与 C 和 Perl 同级。如同这些语言一样，你可以创建诸如 if 语句和循环之类的控制结构。此外，PHP 还具有专门适用于 Web 页面任务的功能。PHP 可以直接与 Oracle、MySQL 和 IBM DB2 等数据库交互。它可以轻松与所有标准协议交互，例如 IMAP、LDAP、HTTP 和 POP3。它甚至具有文本处理能力，例如解释正则表达式和显示 XML 文档。还有用于搜索、压缩工具如 gzip 和语言翻译的扩展。PHP 支持大量可能的运算。请查看其网站以获取完整列表，以及在线手册和教程。
