
这列出了包含允许访问此目录的用户名和密码组合的文件名称。当然，出于安全原因，此文件不应放置在 Web 服务器可以访问的目录结构中的任何位置。

```
Require
```

这告诉 Apache 应如何对用户进行身份验证。它可以包含关键字 valid-user，这意味着 AuthUserFile 中存在的任何用户都将被验证（假设他们输入了正确的密码）。它也可以包含用户名列表。

以下是用于通过用户名和密码控制目录访问的示例 .htaccess 文件：

```
AuthType Basic
AuthName 'Top Secret Stuff'
AuthUserFile /usr/local/www/.htpasswd
Require valid-user
```

保存 .htaccess 文件后，您需要创建密码数据库。

## 创建密码数据库

htpasswd 命令用于创建和更新 Apache 密码数据库（顺便说一下，这不应与 FreeBSD 用户数据库 /etc/master.passwd 混淆）。第一次运行 htpasswd 时，您需要使用 -c 选项告诉它创建尚不存在的新密码数据库文件。我还建议您使用 -n 选项，这将使用 MD5 加密。MD5 比默认的基于 crypt() 的加密形式更强。以下是该命令首次运行的示例：

```
htpasswd -cm /usr/local/www/.htpasswd foobar
```

然后系统会要求您提供用户 foobar 用于访问受限目录的密码。

![](img/ba0161b65b37e94cffc801ecbacaba5e_381_0.png)

> 您需要了解的两个安全问题。第一个是 .htpasswd 文件不应放置在您试图保护的同一目录中，也不应放置在 Web 服务器可以访问的目录树中的任何其他位置。这样做可能会允许网站访问者通过将其作为 URL 请求来获取该文件。当然，将您的密码文件发送给网站访问者可能不是您想要做的。
> 
> 您需要了解的第二件事是这种保护形式相当原始。首先，使用此系统通过 Internet 发送的密码仅使用哈希序列进行混淆，对于嗅探您网站流量以获取密码的人来说相对容易破解。此外，
> 用户经过身份验证后传输的文档在发送时未加密，从而可能允许他人拦截它们。这意味着这种身份验证形式仅提供基本级别的安全性，不能信任其保持敏感文档安全。对于更适合电子商务等更高级别的保护，您需要研究 SSL，这超出了本书的范围。它以及 FreeBSD 下 Apache 的其他更高级配置，可以在 Sams Publishing 出版的《FreeBSD Unleashed》中找到，也可以在许多专门针对 Apache 的其他书籍中找到，例如 O'Reilly 的《Apache: The Definitive Guide》。

## 摘要

在本小时中，我们研究了如何配置适用于简单 Web 主机的基本 Web 服务器。然而，Apache Web 服务器高度复杂，能够实现远不止我们在此涵盖的内容。诸如虚拟主机和安全站点等高级主题未涵盖。有关 Apache 高级功能的更多信息，请参阅项目网站（www.apache.org）上的在线文档，或查阅专门介绍 Apache 的书籍之一。

## 问答

Q 我在 Linux 和其他 UNIX 平台上使用过 Apache；文件在 FreeBSD 下似乎都在不同的位置。这是为什么？

A 这是不同 UNIX 系统变体中的常见问题：每个系统似乎都有自己关于文件放在何处的想法。例如，一些 Linux 发行版将 Apache 安装放在 /var/lib/httpd 下的单个目录结构中。FreeBSD 试图遵循严格的概念布局；Web 内容和可执行文件不放在 /var 中，/var 应该包含可变文件（如 PID 文件、数据库和日志）。相反，Apache 的二进制文件放在 /usr/local/sbin 和 /usr/local/bin 中（取决于它们是否改变系统行为），日志保存在 /var/log 中，文档位于 /usr/local/share/doc/apache，Web 内容放在 /usr/local/www，配置文件放在 /usr/local/etc/apache。这意味着安装分散在整个系统中，但文件都是按功能组织的。ports 保留一个打包清单，以便它们都可以干净地卸载。

Q 您只谈到了 Apache 2.0。那 Apache 1.3 呢？我以为那是标准版本。

A Apache 1.3 刚刚达到其生命周期的终点；Apache 现在已经在 1.x 系列中存在了近七年，从 1.x 到 2.0 作为稳定平台的过渡现在已经足够完整，以至于如果您是 Apache 新手，就没有理由学习 1.3。了解 1.3 如何工作唯一的理由是如果您正在管理一个遗留安装。无论如何，这两个版本的配置实际上非常相似，并在 Apache 网站上完全记录。

Q 如何在普通用户目录中启用 CGI（例如，不在 cgi-bin 中）？

A 使用 Options +ExecCGI 指令为 <Location> 或 <Directory> 块中指定的位置或目录启用 ExecCGI 选项。您还需要使用 AddHandler cgi-script .cgi 将所有以 .cgi 结尾的可执行文件映射到 CGI 脚本处理程序。

Q 那服务器端包含呢？

A 您可以使用 AddType 和 AddHandler 指令启用“解析 HTML”——在发送之前由服务器处理的 HTML 文件，执行嵌入的程序调用。请查阅 Apache 网站以获取有关如何执行此操作的完整文档。启用 SSI 后，您可以执行诸如将程序输出嵌入 HTML 文件或使用基本流程控制更改页面外观之类的操作。它就像 PHP 的内置前身。

Q 哪个是正确的——.html 还是 .htm？

A 原始扩展名是 .html，它完全反映了 HTML（超文本标记语言）的缩写。.htm 存在为有效扩展名的唯一原因是 Windows，在 Web 变得流行时，它不支持超过三个字符的文件名扩展名。（许多 Windows 应用程序仍然不支持。）这就是为什么 UNIX 支持 .html 变体，如 .shtml 和 .phtml，而 Windows 则被困在 .stm 和 .ptm 等无意义的缩写版本中。您使用的是 UNIX；使用较长的扩展名，只是因为您可以。

## 工作坊

本交互部分包含测验问题和练习，旨在测试您对 Apache Web 服务的理解，并指引您进行更深入的主题探索。

## 测验

+   1. 您用来启动和停止 Apache 服务器的程序是
+      A. apache
+      B. httpd
+      C. apachectl
+      D. htserv
+   2. 包含限制目录访问的选项的文件名称是
+      A. htaccess
+      B. .htpasswd
+      C. htsecure
+      D. None of the above
+   3. 控制 Apache 配置选项的主要文件是
+      A. /usr/local/etc/apache.conf
+      B. /usr/local/etc/httpd.conf
+      C. /usr/local/etc/apache/apache.conf
+      D. /usr/local/etc/apache/httpd.conf
+   4. Apache 模块的目的是什么？

## 测验答案

+   1. 正确答案是 C。
+   2. 正确答案是 D。答案 A 不正确，因为它没有以前导句点开头。答案 B 不正确，因为它是存储用户名和密码的文件的名称，而不是包含限制目录访问的选项的文件的名称。
+   3. 正确答案是 D。
+   4. 模块的目的是将 Apache 的功能扩展到正常的基础服务器之外。例如，mod_php 提供了一种嵌入式脚本语言，可用于创建动态网页和访问数据库。
