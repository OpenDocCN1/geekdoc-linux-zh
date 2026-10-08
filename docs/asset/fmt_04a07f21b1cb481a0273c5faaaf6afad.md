
`print "<P>Project Cost Last Year was $projectcost dollars.";`

`print "<P>We completed $projects during the year works out to an average of $average cost per project.";`

`print "<P>Our annual Project Revenue was $revenue dollars. We made a gross profit of $grossprofit dollars.";`

看到网页的工作原理，你就可以创建自己的页面了。

## 创建 Dominion 网页

Dominion Consulting 目前为所有酒店管理客户提供三个应用程序的促销价格。公司希望提供一个让客户可以在互联网上订购促销项目的网页。规划网页如图 27 所示。你现在将创建该页面。

![](img/6ed9bb33c68863516b7a954081187e3b_373_0.png)

**图 27：** Dominion Consulting 销售页面

创建一个网页：

1. 使用你任选的编辑器创建 `software.html` 文档。输入以下 HTML：

```html
<!-- Program Name: software.html -->
<HTML><HEAD><TITLE>Dominion Consulting</TITLE></HEAD>
<BODY BGCOLOR=WHITE>
<CENTER><H1>Dominion's Fall 2000 Specials</H1></CENTER>
<FORM METHOD=POST ACTION="http://localhost/cgi-bin/your name/software.cgi">
<BR>
<H2><PRE>Special Prices Qty/</PRE></H2>
<FONT SIZE=5><PRE>Front Desk Management<INPUT TYPE=text NAME=frontdk SIZE=5></PRE>
<PRE>Reservation Express <INPUT TYPE=text NAME=reserve SIZE=5></PRE>
<PRE>Convention Management <INPUT TYPE=text NAME=convmg SIZE=5></PRE>
<HR><INPUT TYPE=submit NAME=submit VALUE=Submit>
<INPUT TYPE=reset NAME=reset VALUE="Start over">
</FORM></body></HTML>
```

2. 将文件保存到你的 `cgi-bin/用户名` 目录下，并退出编辑器。

3. 现在使用编辑器创建 CGI Perl 脚本 `software.cgi`。输入以下代码：

```perl
#!/usr/bin/perl
# Program name: software.cgi

require "subparseform.lib";
&Parse_Form;
$frontdk = $formdata{'frontdk'};
$reserve = $formdata{'reserve'};
$convmgmt = $formdata{'convmgmt'};

$gtotal = $frontdk+$reserve+$convmgmt;
$frontdk*=200;
$reserve = $reserve*150;
$convmgmt = $convmgmt*180;
$total = $frontdk+$reserve+$convmgmt;

print "Content-type: text/html\n";
print "

print "</FONT><CENTER><B><CENTER SIZE=20>Dominion Special</CENTER></P><P ALIGN=LEFT></FONT><FONT SIZE=3 PTSIZE=10"
print "<CENTER></FONT><FONT SIZE=5 PTSIZE=16>
<U>Thank you for your order.</U></FONT><FONT SIZE=3 PTSIZE=10></CENTER>\n";
print "
"

print "<TABLE ORDER=1 BCOLOR=CYAN ALIGN=CENTER WIDTH=300 CELLACING=5">
print "<TR><TH ALIGN=CENTER>Qty</TH>"
print "<TH ALIGN=CENTER>Software</TH>"
print "<TH ALIGN=CENTER>Total</TH>"
print "<TR><TD ALIGN=CENTER>$frontdk</TD>
print "<TD ALIGN=CENTER>Front Desk Management</TD>
print "<TD ALIGN=CENTER>$$frontdk</TD>
print "<TR><TD ALIGN=CENTER>$reserve</TD>
print "<TD ALIGN=CENTER>Reservation Express</TD>
print "<TD ALIGN=CENTER>$$reserve</TD>
print "<TR><TD ALIGN=CENTER>$convmgmt</TD>
print "<td><td>Convention Management</td><td>> *"
```

## 第9章，B节

```perl
print "<TR ALIGN=CENTER>$tconmgt</TD></TR>"
print "<TR><TD ALIGN=CENTER>$qtotal</TD>"
print "<TD ALIGN=CENTER>Total:</TD>"
print "<TD ALIGN=CENTER>$$total</TD></TR></TABLE>";
```

- 4. 将文件保存到你的 `cgi-bin/<username>` 目录，并退出编辑器。

- 5. 使用 `chmod` 命令赋予该文件执行权限。

现在你已经输入了 Web 页面和 CGI 脚本的代码，你应该测试你的工作成果。请记住，在 Linux Red Hat 6.0 中，你可以使用 `localhost` 来进行新页面的测试和开发。

### 测试 Web 页面：

- 1. 在 X-Window 中，通过打开终端窗口来启动 Netscape Communicator，在命令行中输入 `netscape` 然后按回车。

- 2. 在位置框中，输入 `file:/home/httpd/cgi-bin/<your username>/software.html`。按回车。

- 3. 为产品输入数量 10、15 和 20，然后点击提交按钮。你的屏幕现在应该看起来与图 9-28 相似。

图 9-28：从 `software.cgi` 返回浏览器的 Web 页面

## Perl 和 CGI 编程

你已经利用对 Perl 编程的知识成功为 Dominion Consulting 创建了 Web 页面。

## 总结

- 一个 HTML 文档包含两个部分：头部（head）和主体（body）。头部包含标题，显示在浏览器窗口的顶部栏上。主体定义了浏览器窗口内显示的内容。

- CGI（通用网关接口）是一种规定浏览器和服务器之间如何通信的协议或一组规则。任何向服务器发送或从服务器接收信息的脚本都需要遵循 CGI 规范的标准。

- 要运行你的 Web 页面，你需要处于 X-Window 环境，并能够使用 Netscape Communicator 和 Apache 等 Web 服务器访问 Web 浏览器。在 UNIX 中，你也可以使用 `localhost` 功能来测试你的 Web 页面。

## 复习题

- 1. 正确或错误：HTML 标签是封装在方括号 `[]` 里的特殊代码。

- 2. 正确或错误：大多数标签成对使用：一个标记部分的开始，另一个相应的标签标记部分的结束。

- 3. HTML 文档的哪个部分包含标题？

   a. `HEAD`

   b. `BODY`

   c. `PARAGRAPH`

   d. `BLOCKQUOTE`

- 4. 标签之间的文本将居中显示。

   a. `[CENTER]` 和 `[/CENTER]`

   b. `<CENTER>` 和 `</CENTER>`

   c. `<ALIGN=center>` 和 `</ALIGN>`

   d. `<JUSTIFY=center>` 和 `</JUSTIFY>`

- 5. 在 UNIX 或 Linux 中运行 Netscape，你：

   a. 不需要处于 X-Window 中

   b. 应该在 X-Window 中

   c. 必须在 X-Window 中

   d. 必须安装 Apache 服务器

- 6. 一个基础 HTML 文档有一个：

   a. `head` 和 `body`

   b. `title` 和 `body`

   c. 一组标签

   d. 指向其他 Web 页面的链接

- 7. HTML 脚本中的按钮用于将数据传输到 Web 服务器，服务器将其传递给 CGI 脚本。

   a. `Transfer`（传输）

   b. `Accept`（接受)

   c. `Go`（跳转）

   d. `Submit`（提交）

- 8. 以下哪项不是常用的 CGI 编程语言？

   a. Perl 是用于 CGI 编程的唯一语言。

   c. CGI 脚本不需要 `.cgi` 脚本以外的任何语言。

   d. Perl CGI 脚本由 Web 页面调用。

- 9. 在 Perl 中，数组变量前的字符是：

   a. `$`

   b. `#`

   c. `%`

   d. `@`

## 练习题

- 1. 创建一个个人 Web 页面，包含你的姓名、地址、电话号码以及一段描述你爱好和兴趣的简短段落。你的名字应该在大号标题中居中。

- 2. 设计一个 Web 页面，允许用户输入年龄。该页面应该有一个提交按钮，点击后会调用 CGI 脚本。脚本应该以天的单位显示用户的年龄。（不用担心闰年。）

- 3. 设计一个 Web 页面，允许用户输入矩形的宽度和长度。该页面应该有一个提交按钮，点击后会调用 CGI 脚本。脚本应该显示矩形的面积（宽度 × 长度）。

### 发现性练习

- 1. 创建一个 HTML 和 CGI 脚本，创建一个交互式 Web 页面以接受你的姓和名，并将其传递给 CGI 脚本，由脚本显示“Hello,”后面接你的姓和名。

- 2. 创建一个 Perl 程序来读取学生文件和列表。按他们出现的字母顺序显示学生的姓名。

- 3. 设计一个作为简单加法计算器的 Web 页面。它应该允许用户输入两个值。当用户点击提交按钮时，CGI 脚本返回两个数字之和。

## 第10 章：使用 C 和 C++ 开发 UNIX

### 介绍 C 语言

Dominion Consulting 的客户对数据隐私和保护日益关注。主管要求你写一个简单的程序，来演示加密是如何工作的。加密是将文件内容混乱成秘密代码的操作；解密操作则将文件恢复到原始状态。

C 是编写和完善原始 UNIX 系统的语言。汇编语言提供了对计算机设备的最大访问。C 是编写和完善原始 UNIX 系统的语言。汇编语言提供了对计算机设备的最大访问。C 是编写和完善原始 UNIX 系统的语言。汇编语言提供了对计算机设备的最大访问。C 是编写和完善原始 UNIX 系统的语言。汇编语言提供了对计算机设备的最大访问。C 是编写和完善原始 UNIX 系统的语言。汇编语言提供了对计算机设备的最大访问。 (注：原文此处存在大量文本重复，翻译已按原文意图进行逻辑处理)

C 是编写和完善原始 UNIX 系统的语言。汇编语言提供了对计算机设备的最大访问。C 是编写和完善原始 UNIX 系统的语言。汇编语言提供了对计算机设备的最大访问。 (此处同样存在原文重复问题)

### 课程目标

- 创建简单的 C 程序

- 使用 `make` 工具修订维护源码

- 识别并修复程序错误

- 创建完整的应用程序

### C 编程

Dominion Consulting 的客户对数据隐私和保护日益关注。主管要求你写一个简单的程序，来演示加密是如何工作的。加密是将文件内容混乱成秘密代码的操作；解密操作则将文件恢复到原始状态。主管要求你写一个简单的程序，来演示加密是如何工作的。加密是将文件内容混乱成秘密代码的操作；解密操作则将文件恢复到原始状态。

C 是编写和完善原始 UNIX 系统的语言。汇编语言提供了对计算机设备的最大访问。C 是编写和完善原始 UNIX 系统的语言。汇编语言提供了对计算机设备的最大访问。 (此处存在重复)

在本章中，你不仅学习如何编写 C 程序，还学习如何使用其他开发工具，例如 `make` 工具。`make` 工具是一种在你进行更改和添加时使用的 UNIX 程序。

### 创建 C 程序

一个程序由单独的代码块组成，这些被称为函数。在其他语言中，代码块被称为子程序或过程。这些代码块中的每一个设计是为了完成单一任务。你将这些函数组合在一起，它们就成了程序。在程序内部，函数根据需要相互调用，并解决最初旨在解决的问题。

创建程序从来不是一步到完成的。作为程序员，在程序运行之前你需要完成许多阶段。第一阶段是创建程序的源码。与 shell 脚本和 Perl 程序一样，你使用文本编辑器（如 `vi` 或 `Emacs`）创建。

下一个阶段是执行预处理器和编译器。预处理器会对你的程序进行修改，包括其他文件的内容和创建常量。在预处理器准备好你的程序后，编译器会将源代码翻译成机器码。如果你犯错，编译器可以发现其中的许多。当这种情况发生时，你使用文本编辑器纠错并重新编译程序。

许多编译器将源代码翻译成汇编代码。这需要调用汇编器将汇编代码翻译成目标代码。编译器会自动调用汇编器，因此你不需要额外的命令。某些编译器直接从源代码翻译成目标代码，跳过汇编步骤。无论你使用哪种编译器，此阶段的结果都是创建一个包含目标代码的文件。最后阶段需要使用另一个称为链接器的工具。该程序链接程序的所有目标文件，以及程序可能使用的任何库函数。结果是一个可执行文件。整个过程如图 10-1 所示。

### C 关键字

C 语言像所有编程语言一样，包含了关键字。这些关键字有特殊含义，因此你不能将它们作为变量或函数的名称。表 10-1 列出了 C 关键字。

## 第 10 章，A 节

![](img/6ed9bb33c68863516b7a954081187e3b_381_0.png)

源文件

预处理器

编译器

编译器实际上在此输出一个汇编版本，然后将其翻译成对象代码（二进制文件）。

对象文件

链接器

可执行程序

图 10-1：C 程序的编译过程

## C 标准库

如表 10-1 所示，C 语言非常小。它本身没有作为语言的一部分提供输入或输出功能。所有的 I/O 操作都是通过 C 标准库完成的。C 标准库由用于执行文件、屏幕和键盘操作的函数以及许多其他任务组成。例如，某些函数执行字符串操作、内存分配和控制、数学运算，当您需要在程序中执行这些操作之一时，在所需的位置放置一个函数调用。链接器将库函数的代码与您的程序对象代码合并，创建可执行文件。

## 使用 C 和 C++ 开发 UNIX 应用程序

| `auto` | `double` | `int` | `struct` |

| `break` | `else` | `long` | `switch` |

| `case` | `enum` | `register` | `typedef` |

| `char` | `extern` | `return` | `union` |

| `const` | `float` | `short` | `unsigned` |

| `continue` | `for` | `signed` | `void` |

| `default` | `goto` | `sizeof` | `volatile` |

| `do` | `if` | `static` | `while` |

**表 10-1：**C 关键字

## 程序格式

```c
int main()
{
}
```

如前所述，C 程序由一个或多个函数组成。每个函数都必须有一个名称，并且每个 C 程序都必须有一个名为 `main` 的函数。这是一个非常简单的 C 程序：

此程序实际上什么都不做，但它包含了一个有效 C 程序所需要的所有元素。接下来的两个段落将检查最基本的内容。

注意单词 "`main`" 后面跟着一组括号。（接后的章节“指定数据类型”定义了第一个项目-`int`.）这是一个函数的名称。如前所述，所有 C 程序都必须有一个名为 `main` 的函数。括号表示这是一个函数名。

下一行是一个左括号。在 C 程序中，这表示一个代码块的开始。下一行的右括号表示代码块的结束。所有函数都必须有左括号和右括号。通常组成函数的语句出现在两个括号之间。在示例程序中没有语句；因此，该函数什么都不做。其他部分仍然是。

## 包含注释

`/*` 符号表示注释的开始，`*/` 符号表示注释的结束。编译器忽略之间的所有内容。这个示例显示了一个 C 程序的注释：

```c
/* Here is a program that does nothing. */
int main()
{}
```

## 第 10 章，A 节

在示例中，注释“Here is a program that does nothing”出现在程序的顶部。注释的开始用 `/*` 标记，结束用 `*/` 标记。编译器认为这个程序与之前没有注释的版本没有区别。

## 使用预处理器 #include 指令

这里有一个执行一个执行输出操作的示例程序：

```c
/* A simple C program */
#include <stdio.h>
int main()
{
    printf("Hello from the Linux World!\n");
}
```

图 10-2 显示了程序的输出。

![](img/6ed9bb33c68863516b7a954081187e3b_383_0.png)

图 10-2：C 程序输出

在上面的程序中，您看到了语句：

`#include <stdio.h>`
