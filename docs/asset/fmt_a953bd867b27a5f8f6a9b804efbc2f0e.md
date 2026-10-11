
图 9-26：最终的 Perl/CGI 脚本响应屏幕

以下是用于生成此 Web 页面的源代码。

```perl
#!/usr/bin/perl
# Program name: project.cgi
require "subparseform.lib;"

&Parse_Form;
$projcost = $formdata{'projcost'};
$projects = $formdata{'projects'};
$revenue = $formdata{'revenue'};

$average = $projcost / $projects;
$average = sprintf("%.2f", $average);
$grossprofit = $revenue - $projcost;

print "Content-type: text/html\n\n";
print "<P>Project Cost Last Year was $projcost dollars. ";
print "<P>We completed $projects projects during the year.
That works out to an average of $average cost per
project.";
print "<P>Our annual Project Revenue was $revenue dollars.
We made a gross profit of $grossprofit dollars";
```

现在你已经看到了使用 UNIX 处理 Web 页面工作原理的演示，你可以开始创建自己的 Web 页面了。

# 创建 Dominion 咨询公司 Web 页面

Dominion 咨询公司为酒店管理层客户提供针对三项定制应用程序的特别促销价格。该公司希望展示一个 Web 页面，让客户有机会通过互联网订购这些促销项目。计划的 Web 页面如图 9-27 所示。你现在将创建该页面。

![](img/6d8286a85e2d8ad63e16f1801102da59_373_0.png)

图 9-27：计划的 Web 页面

## 创建 Web 页面

1. 使用你选择的编辑器创建 HTML 文档 `software.html`。输入此 HTML 代码：

```html
<!-- Program Name: software.html-->
<HTML><HEAD><TITLE>Dominion Consulting</TITLE></HEAD>
<BODY BGCOLOR=WHITE>
<CENTER><H1>U>Dominion's Fall 2000 Specials</H1></CENTER>
<FORM METHOD=POST ACTION="http://localhost/cgi-bin/<your user name>/software.cgi">
<BR>
<H2><U><PRE>Special Prices                       Qty</PRE></U></H2>
<FONT SIZE=5>
<PRE>Front Desk Management <INPUT TYPE=text NAME=frontdk
Size=5></PRE>
<PRE>Reservation Express     <INPUT TYPE=text NAME=reserve
SIZE=5</PRE>
<PRE>Convention Management <INPUT TYPE=text NAME=convmgt SIZE=5></PRE>
<HR><INPUT TYPE=submit NAME=submit VALUE=Submit>
<INPUT TYPE=reset NAME=reset VALUE="Start over">
</FORM></BODY></HTML>
```

2. 将该文件保存在你的 `cgi-bin/<your user name>` 目录中，并退出编辑器。

3. 现在使用编辑器创建 CGI Perl 脚本 `software.cgi`。输入此代码：

```perl
#!/usr/bin/perl
# Program name: software.cgi

require "subparseform.lib"; &Parse_Form;
$frontdk = $formdata{'frontdk'};
$reserve = $formdata{'reserve'};
$convmgt = $formdata{'convmgt'};

$qtotal = $frontdk+$reserve+$convmgt;
$tfrontdk = $frontdk*200;
$treserve = $reserve*150;
$tconvmgt = $convmgt*180;
$total = $tfrontdk+$treserve+$tconvmgt;

print "Content-type: text/html\n\n";
print "";
print "</FONT><FONT SIZE=6 PFSIZE=20>
</P><P ALIGN=CENTER><B><CENTER> Dominion Special</CENTER>
</P><P ALIGN=LEFT></FONT><FONT SIZE=3 PT SIZE=10>
";
print "<CENTER></FONT><FONT SIZE=5 PT SIZE=16>
<U>
Thank you for your order.</U>
</FONT><FONT SIZE=3 PFSIZE=10></CENTER>";
print "
";
print "<TABLE BORDER=1 BGCOLOR=CYAN ALIGN=CENTER
WIDTH=300 CELLSPACING=5>
";
print "<TR><TH ALIGN=CENTER>Qty</TH>";
print "<TH ALIGN=CENTER>Software</TH>";
print "<TH ALIGN=CENTER>Total</TH></TR>";
print "<TR><TD ALIGN=CENTER>$frontdk</TD>";
print "<TD ALIGN=CENTER>Front Desk Management</TD>";
print "<TD ALIGN=CENTER>$tfrontdk</TD></TR>";
print "<TR><TD ALIGN=CENTER>$reserve</TD>";
print "<TD ALIGN=CENTER>Reservation Express</TD>";
print "<TD ALIGN=CENTER>$treserve</TD></TR>";
print "<TR><TD ALIGN=CENTER>$convmgt</TD>";
print "<TD ALIGN=CENTER>Convention Management</TD>";
print "<TD ALIGN=CENTER>$convmgt</TD></TR>";
print "<TR><TD ALIGN=CENTER>$total</TD>";
print "<TD ALIGN=CENTER>##TOTAL:</TD>";
print "<TD ALIGN=CENTER>$total</TD></TR></TABLE>";
```

4. 将该文件保存在你的 `cgi-bin/<your user name>` 目录中，并退出编辑器。

5. 使用 `chmod` 命令授予文件执行权限。

现在你已输入了 Web 页面和 CGI 脚本的代码，你应该测试你的工作。回想一下，在 Linux Red Hat 6.0 中，你可以使用本地主机进行新 Web 页面的测试和开发。

## 测试 Web 页面

1. 在 X-Window 中，通过打开终端窗口，在命令行键入 `netscape`，然后按 `Enter` 来启动 Netscape Communicator。

2. 在位置框中键入 `file:/home/httpd/cgi-bin/<your user name>/software.html`。按 `Enter`。

3. 为产品输入数量 **10**、**15** 和 **20**，然后点击**提交**按钮。你的屏幕现在应该看起来类似于图 9-28。

![](img/6d8286a85e2d8ad63e16f1801102da59_375_0.png)

图 9-28：从 `software.cgi` 返回给浏览器的 Web 页面

您已成功运用 Perl 编程知识，为 Dominion Consulting 创建了网页。

### 摘要

- HTML 文档包含两部分：头部 `head` 和主体 `body`。头部包含标题，该标题显示在浏览器窗口的顶部栏上。主体部分定义了显示在浏览器窗口内的内容。
- CGI `通用网关接口` 是一种协议或规则集，用于规范浏览器与服务器之间的通信方式。任何向服务器发送或接收信息的脚本都必须遵循 CGI 指定的标准。
