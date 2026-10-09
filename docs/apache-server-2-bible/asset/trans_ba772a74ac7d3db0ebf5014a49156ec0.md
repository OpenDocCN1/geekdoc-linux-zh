

8.  等待几天，让互联网服务提供商（ISP）作出回应。如果你没有收到其回复，请尝试通过其网站与 ISP 取得联系。如果问题依然存在，请联系法务部门，以确定你可以采取哪些法律手段来要求 ISP 采取行动。

## 保护你的 CGI 实现

大多数 Web 安全专家认为，最大的安全风险因素是在 Web 服务器上运行的、用于生成动态内容的脚本或应用程序。由于 CGI 脚本通常负责创建动态内容，因此它们往往造成了最大的损害。本节重点讨论与 CGI 脚本相关的安全风险，并展示如何降低这些风险。

### 通过智能编程防范 CGI 风险

根据 SANS（www.sans.org）的说法，CGI 脚本相关的安全风险在其十大互联网安全问题分析中排名第二。然而，CGI 本身并不是不安全的；编写拙劣的 CGI 脚本才是 Web 安全漏洞的主要来源。实际上，CGI 规范的简单性使得许多没有经验的程序员也能编写 CGI 脚本。这些缺乏经验的程序员由于不了解互联网络的安全方面，创建了一些能正常工作的应用程序或脚本，同时也无意中在系统中留下了后门和漏洞。

接下来的章节将首先讨论 CGI 应用程序或脚本所构成的风险类型，然后讨论解决这些风险的方法。

> 术语*CGI 应用程序*和*CGI 脚本*可以互换使用。

### 信息泄露

许多 CGI 脚本会被破坏者诱导，从而泄露关于用户或 Web 服务器上可用资源的信息。此类泄露有助于破坏者入侵系统。破坏者掌握的系统信息越多，其入侵系统的能力就越强。例如，如果使用以下 URL 通过 *showpage.cgi* 脚本显示 /doc/article1.html 页面：

```http://unsafe-site.com/cgi-bin/showpage.cgi?pg=/doc/article1.html```

破坏者可能会尝试如下操作：

```http://unsafe-site.com/cgi-bin/showpage.cgi?pg=/etc/passwd```

这将显示整个系统的 /etc/passwd（用户密码文件）。只有当 *showpage.cgi* 的作者没有保护该脚本免受此类泄露时，这种情况才会发生。

编写拙劣的 CGI 脚本可能被破坏者利用，使服务器消耗系统资源，从而导致服务器几乎无响应。例如，以下 URL 允许网站访客查看网站上分类广告的列表：

`http://unsafe-site.com/cgi-bin/showlist.pl?start=1&stop=15`

`start=1` 和 `stop=15` 参数用于控制显示记录的数量。如果 `showlist.pl` 脚本仅依赖提供的 start 和 stop 值，那么破坏者可以编辑 URL，并为 stop 参数提供更大的数值，使 `showlist.pl` 显示比平时更大的列表。这会怎样？破坏者可以利用这一知识，通过发送处理时间更长的请求来使 Web 服务器过载，这会让真实用户等待，并可能导致他们转向竞争对手的网站。

## 通过 CGI 脚本伪造系统命令

在许多情况下，破坏者已成功诱导基于 HTML 表单的邮件脚本运行系统命令或泄露机密系统信息。例如，假设你有一个 Web 表单，用户可以使用它来注册你的服务或提供反馈。拥有此类 Web 表单的大多数网站都会通过电子邮件向用户发送一封感谢信。使用 CGI 脚本处理该表单。该脚本可能执行类似以下操作来发送电子邮件：

`system("/bin/mail -s $subject $emailAddress < $thankYouMsg");`

系统调用运行 `/bin/mail` 邮件程序，并将变量 `$subject` 的值作为主题头，将变量 `$emailAddress` 的值作为用户的电子邮件地址，并重定向由 `$thankYouMsg` 变量指定的文件的内容。这可以正常工作，通常不应该有人知道你的应用程序使用了这样的系统调用。然而，破坏者总是试图破坏系统，因此，对破坏你的网站感兴趣的破坏者可能会调查破坏者可以访问的一切，并尝试为你的 Web 表单输入不寻常的值。例如，如果破坏者输入 `vandal@emailaddr < /etc/passwd;` 作为电子邮件地址，脚本将被欺骗，将 `/etc/passwd` 文件发送到破坏者指定的电子邮件地址！

> 提示
> 如果你在 CGI 脚本中使用 `system()` 函数，你应该在 `#!/path/to/perl` 行中使用 `-T` 选项来启用 Perl 的污点检查模式。你还应使用 `set $ENV{PATH} = '/path/to/commands:/you/call/via/system'` 设置 `PATH`（环境变量）以增加安全性。

## 用户输入使某些系统调用不安全

某些系统调用在 CGI 脚本中使用是不安全的。例如，在 Perl（一种广泛使用的 CGI 编程语言）中，可以使用 `system()`、`exec()`、`piped open()` 和 `eval()` 函数进行此类调用。类似地，在 C 语言中，`popen()` 和 `system()` 函数也是潜在的安全隐患。所有这些函数/命令通常都会调用一个子进程（如 `/bin/sh`）来处理用户命令。

即使使用 `system()` 或 `exec()` 调用的 shell 脚本也可能会为破坏者打开一个入口。shell 解释器和 Perl 中可用的反引号引号（用于将程序的输出捕获为文本字符串）也是危险的。

为了说明仔细使用系统调用的重要性，请考虑以下看似无害的 Perl 代码段：

```perl
#!/usr/bin/perl -w
#
# 目的：演示编写拙劣的 CGI 脚本中的安全风险。
#
# 从查询字符串获取域名
# 环境变量。
#

my $domain = $ENV{'QUERY_STRING'};

# 打印适当的内容类型。
# 因为 whois 输出是纯文本，
# 我们在这里选择使用 text/plain 作为内容类型。
#
print "Content-type: text/plain\n\n";

# 这里是不好的系统调用：
system("/usr/bin/whois $domain");

# 这里是用反引号进行的另一个不好的系统调用：
#
# my $output = `/usr/bin/whois $domain`;
#
# print $output;

exit 0;
```

这个小 Perl 脚本旨在成为一个基于 Web 的 WHOIS 网关。如果这个脚本名为 `whois.pl`，并且存储在名为 `unsafe-site.com` 的网站的 `cgi-bin` 目录中，用户可以按如下方式调用该脚本：

`http://unsafe-site.com/cgi-bin/script.pl?domain=anydomain.com`

该脚本将通过 `QUERY_STRING` 变量将 `anydomain.com` 作为 `$domain` 变量，并以 `$domain` 值作为参数启动 `/usr/bin/whois` 程序。这会返回 InterNIC 维护的 WHOIS 数据库中的数据。这看起来非常无辜且良好，但该脚本是一个等待发生的灾难。考虑以下行：

`http://unsafe-site.com/cgi-bin/script.pl?domain=nitec.com;ps`

这会对名为 `nitec.com` 的域名执行 WHOIS 查询，并提供 Unix `ps` 实用程序（显示进程状态）的输出。这揭示了本不应该提供给请求方的系统信息。使用这种技术，任何人都可以了解你的大量系统信息。例如，用 `df`（一个常见的 Unix 实用程序，打印磁盘空间摘要）替换 `ps` 命令，任何人都可以确定你有哪些分区以及它们有多满。这个安全漏洞可能带来巨大危险。

教训是什么？不要信任任何输入，并且不要让系统调用成为容易被滥用的目标。如何实现这些目标是下一节要讨论的主题。

## 用户可以修改 HTML 页面中的隐藏数据

你可能已经知道，HTTP 是一个无状态协议。许多 Web 开发者将状态信息或其他重要数据保存在 cookies、临时文件中，或者使用所谓的隐藏标签中。因为用户可以关闭 cookies，而且为每个用户创建唯一的临时文件很麻烦，所以隐藏标签通常被使用。隐藏标签看起来类似于以下内容：

`<input type="hidden" name="dataKey" value="dataValue">`

例如：

`<input type="hidden" name="state" value="CA">`

这里，隐藏标签存储了 "state=CA"，可以在后续调用中由同一应用程序检索。隐藏标签在多屏 Web 应用程序中很常见。因为用户可以手动更改隐藏标签，所以它们不应该被信任。保护被篡改数据有两种方式：开发人员可以在每次使用前验证隐藏数据，或者开发人员可以使用安全方案来确保数据没有被用户篡改。列表 18-2 中显示的 CGI 脚本演示了使用 RSA Data Security MD5 消息摘要算法来保护隐藏数据。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_550_0.png)

MD5 算法的细节定义在 RFC 1321 中。

## 列表 18-2: hidden-md5,eg

```perl
#!/usr/bin/perl -w
#
# 目的：此脚本演示了在多屏幕
# Web 应用程序中使用
# MD5 消息摘要。
#
# CVS: $Id$
# #####################################################################################
use strict;
```

