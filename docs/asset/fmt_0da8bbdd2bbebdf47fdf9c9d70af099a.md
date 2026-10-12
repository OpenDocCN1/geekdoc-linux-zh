
然而，如果任之不管，这些日志文件将继续增长并达到巨大的体积。随着体积增大，由于处理包含的数据量变得越来越困难，它们的价值随之降低。

因此，建立日志轮转计划是明智的。轮日志意味着将现有版本保存到存档中并从新的空日志开始。根据你接收的访问次数，日志轮转的理想频率可以是每月一次、每周一次或每天。

为了轮转日志，你使用 Apache 分发自带的 `rotatogs` 工具。默认情况下，Red Hat Linux 将其安装在 `/usr/sbin/rotatogs`。要使用该程序，你需要在 `httpd.conf` 中添加条目：

```
TransferLog |/usr/sbin/rotatogs /some/location/file time
```

条目`/some/location/file`为轮转日志提供基础文件名。文件名后会附加一个指示日志开始时的系统时间数字。`time`参数以秒指定轮转日志的频率。

# 构建网站

现在你的网站已经配置好并运行良好，让我们创建一个小型示例网站，展示如何为 Web 部署内容。

你将要构建的网站将是一家名为 "On The Web Publishers" 的小型出版公司的信息。该网站将提供标题列表、关于出版者的通用信息、联系表单以及一个专门供与出版商签订合同的作者使用的密码保护区域。

总而言之，这将让你创建一个包含 HTML 和图像、使用 CGI 编程并为网站的密码保护区域实现访问控制的站点。首先，你需要确定网站的结构，如图 32.2 所示。

## 图 32.2: 你网站的结构

![](img/bc3027047bbbcc0b55a71a4b67c60968_796_0.png)

完成此操作后，你需要创建必要的文件来实现这种结构。假设使用本章之前章节中的配置，HTML 文件的根文档树位于`/var/www/html`，CGI 目录位于`/var/www/cgi-bin`。因此，你网站的目录和文件树可能包含以下文件：

*   `/var/www/html/index.html`
*   `/var/www/html/about.html`
*   `/var/www/html/books.html`
*   `/var/www/html/contact.html`
*   `/var/www/html/authors.html`
*   `/var/www/cgi-bin/form.html`

除了最后一个文件（稍后将讨论）外，所有这些图像都可以放在同一个目录中。为了保持整洁，网站管理员倾向于将图像放在另一个目录中。由于本章之前章节使用的配置，HTML 文件的根文档树位于`/var/www/html`，CGI 目录位于`/var/www/cgi-bin`。因此，你网站的目录和文件树可能包含以下文件：

（注：原始 OCR 中的文件列表严重损坏，我已根据上下文和可能的意图重建了逻辑结构）。

## 图 32.24：联系表单

![](img/bc3027047bbbcc0b55a71a4b67c60968_800_0.png)

此页面的特殊之处在于它包含一个表单，以及一个用于处理表单数据的 CGI 程序的引用。在此例中，你使用的程序被称为`formmail`，它是一个用 Perl 编写的免费提供的 CGI 脚本，用于获取表单内容并将其发送到预定义的邮件地址。事实上，表单中的联系信息可以通过电子邮件发送到书店的主邮箱地址。

`formmail` 由 Matthew M. Wright 编写，可以在 `http://www.worldwidemart.com/scripts/formmail.html` 获得。尽管本章没有讨论 Perl 或 CGI 编程，但此处展示了其源代码，以便你看到如何用较少的力气就能创建基础的 CGI 程序：

```perl
#!/usr/bin/perl
######################################################################
# Formmail Version 1.6 #
# Copyright 1995-1997 Matt Wright mattw@worldwidemart.com #
# Created 06/09/95 Last Modified 05/02/97 #
# Matt's Script Archive, Inc.: http://www.worldwidemart.com/scripts/#
######################################################################
```

```perl
# COPYRIGHT NOTICE
# Copyright 1995-1997 Matthew M. Wright All Rights Reserved.
#
# FormMail may be used and modified free of charge by anyone so long as this %
# copyright notice and the comments above remain intact. By using this %
# code you agree to indemnify Matthew M. Wright from any liability that %
# might arise from its use.
#
# # Selling the code for this program without prior consent is #
# expressly forbidden. In other words, please ask first before you try and %
# money off of my program.
#
# Obtain permission before redistributing this software over the Internet or %
# in any other medium. In all cases copyright and header must remain intact %
#############################################################################
# Define Variables
# Detailed Information Found In README File.

# $mailprog defines the location of your sendmail program on your unix
# system.

$mailprog = '/usr/lib/sendmail';

# @referers allows forms to be located only on servers which are defined 
# in this field. This security fix from the last version allowed 
# anyone on any server to use your FormMail script on their web site.

@referers = ('linux.juxta.com');

# Done
#############################################################################

# Check Referring URL
&check_url;

# Retrieve Date
&get_date;

# Parse Form Contents
&parse_form;
```

## 检查必填字段

`&check_required;`

## 返回 HTML 页面或重定向用户

`&return_html;`

## 发送邮件

`&send_mail;`

```perl
sub sub_check_url {

    # 本地化 check_referer 标记，确定用户是否有效。
    local($check_referer) = 0;

    # 如果指定了引用 URL，对于每个有效的 referer，确保
    # 传递了一个有效的引用 URL 给 FormMail。
    if ($_ENV['HTTP_REFERER']) {
        foreach $referer (@referers) {
            if ($_ENV['HTTP_REFERER'] =~ m|https?://([^/]*)$referer|i) {
                $check_referer = 1;
            }
        }
    }
    else {
        $check_referer = 1;
    }
}

# 如果 HTTP_REFERER 无效，则返回错误。
if ($check_referer != 1) { &error('bad_referer')}

sub sub_get_date {
```
