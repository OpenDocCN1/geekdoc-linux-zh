
### 图 22.6

搜索失败后`mcdui`的状态。

正如在讨论`mccli`时提到的，获取（`get`）操作是查找特定的键，而不是在整个数据库中搜索匹配项。从用户的角度来看，产生的屏幕显示是完全相同的。

列出数据库中所有记录的代码是`mcdui.c`中最有趣的代码。再次，它在交互式应用程序中的功能与命令行客户端中的对应功能几乎相同。它首先获取数据库中记录的数量。如果数量为零，程序会在状态行上写入相应消息。否则，`mcdui.c`首先调整指向键和值的指针表的大小，然后调整两个表中每个指针的大小。

> **提示**
>
> 同样，一种有价值的改进是动态调整每个表元素的大小，而不是静态调整它们的大小。

`list_recs`调用填充`keys`和`values`表。下一个代码块使用`list`辅助例程将数据库中的所有`CD`显示在屏幕上。图 22.7 显示了`list`更新状态行以指示已显示最后一条记录后的屏幕状态。

![](img/be588b36b489136ce784030a08a1d3d4_541_0.png)

列出`CD`数据库中的所有记录。

`mcdui.c`的`list`操作在列出数据库中的所有`CD`方面做得不错。如果你想增强其功能，请修改它以允许在列表中前后滚动。

## 接下来是什么？

接下来是什么？当然是合上书，成为一名著名的`Linux`程序员！严肃地说，你在本书中已经涵盖了大量材料，并为进一步的编程打下了坚实的基础。剩下的只是编写许多使用你所学知识的程序。除了通过实践，并没有其他途径能成为熟练的`Linux`黑客。虽然书籍可以向你展示基本原理和惯用法，但经验才是最好的老师。去编程吧！

# 第六部分—附录

- A **额外资源**
- B **额外的编程工具**

# A—额外资源

## 参考书目注释

*Advanced Programming in the UNIX Environment*（UNIX 环境高级编程），W. Richard Stevens（Addison-Wesley，1993），ISBN 0-201-56317。这是 UNIX 编程的经典著作。虽然它不专门针对 Linux（事实上，它甚至从未提及 Linux），但它完全涵盖了关于 POSIX 合规性的所有问题。由于 Linux 是 UNIX 的克隆，其中提到的大多数技术也适用于 Linux。Stevens 目前正在修订 APUE（它的常规名称）。

*The Art of Computer Programming, Volume 1: Fundamental Algorithms*（计算机程序设计艺术，第 1 卷：基本算法），第 3 版，Donald Knuth（Addison-Wesley，1997），ISBN 0-201-89683-4。

*The Art of Computer Programming, Volume 2: Seminumerical Algorithms*（计算机程序设计艺术，第 2 卷：半数值算法），第 3 版，Donald Knuth（Addison-Wesley，1998），ISBN 0-201-89684-2。

*The Art of Computer Programming, Volume 3: Sorting and Searching*（计算机程序设计艺术，第 3 卷：排序与搜索），第 3 版，Donald Knuth（Addison-Wesley，1998），ISBN 0-201-89685-0。这三卷是软件开发领域的经典著作。它们与工具和语言无关，但其中蕴含的 30 年编程的精华知识以及数千种算法非常值得投入（三卷套装的价格超过 125.00 美元）。

*Beginning Linux Programming*（Linux 编程入门），Neil Matthewes 和 Rick Stones（Wrox Press，1996）。这本书虽然现在已经过时，但涵盖了基本的 Linux/UNIX 编程技术。然而，它的标题有些误导，因为它也涵盖了 UNIX 编程。

*The C Answer Book: Solutions to Exercises in the C Programming Language*（C 语言参考答案：C 语言程序设计习题解答），第 2 版，Clovis L. Tondo，Scott E. Gimpel（Prentice Hall，1989），ISBN 0-13-109653-2。这本书包含了 Kernighan 和 Ritchie 在其著作 *The C Programming Language*（C 编程语言）中提出的每个练习的解答。不幸的是，这些解答假设读者已经掌握了尚未介绍的语言特性。

*《C 程序设计：现代方法》*，K. N. King（W. W. Norton and Company, 1996）。King 的这本书通常被推荐给那些觉得 *《C 程序设计语言》* 过于简略的初学者，作为 C 语言的教程入门读物。

*《C 程序设计语言》*，第二版，Brian W. Kernighan, Dennis M. Ritchie（Prentice Hall, 1988），ISBN 0-393-96945-2。这是一本关于 C 语言的简明但完整的参考手册，符合 ANSI 和 ISO 标准，由 C 语言的两位创造者撰写。

*《使用 GTK+ 和 GDK 开发 Linux 应用程序》*，Eric Harlow（New Riders, 1999），ISBN 0-7357-0021-4。GTK+ 和 GDK 提供了位于 GNOME、Enlightenment 窗口管理器以及流行的 GIMP 图像编辑程序（Adobe PhotoShop 的克隆版）下方的工具包和库。

*《GNU Make：用于指导重新编译的程序》*，Richard M. Stallman 和 Roland McGrath（Free Software Foundation, 1998），ISBN 1-882114-80-9。本书由 GNU make 的创造者撰写，全面涵盖了 make 的所有内容。如果这本书没有涵盖某项内容，你就得去查看源代码了。

*《计算机图形学导论》*，James D. Foley, Andries van Dam, Steven K. Feiner, John F. Hughes, Richard L. Phillips（Addison-Wesley, 1993），ISBN 0-201-60921-5。这是计算机图形学的经典之作。实际上，这一版本是 *《Computer Graphics: Principles and Practice》* 的删节版。如果你想理解计算机图形学，这本书或者它更庞大的姊妹篇是你必须拥有的。

*《学习 bash Shell》*，第二版，Cameron Newham, Bill Rosenblatt（O'Reilly, 1998），ISBN 1-56592-347-2。这是一本关于 bash shell 的教程入门书，包含若干专门介绍 bash shell 脚本编程的章节。

*《学习 Korn Shell》*，Bill Rosenblatt（O'Reilly, 1993），ISBN 1-56592-054-6。这是一本关于 Korn shell 的教程入门书，包含若干关于 Korn shell 脚本编程的章节。书中所有内容都应适用于 pdksh，即 Korn shell 的公共领域版本。

*《学习 Perl》*，第二版，Randal L. Schwartz & Tom Christiansen（O'Reilly, 1997），ISBN 1-56592-284-0。如果你想学习 Perl，这就是你要读的书。

*《Linux 应用程序开发》*，Michael K. Johnson, Erik W. Troan（Addison-Wesley, 1998），0-201-30821-5。本书由 Red Hat Software 的两位顶级应用程序程序员编写，出色地解释了编写 Linux 应用程序的细微之处。不过，它没有涵盖内核开发。

*《Linux 设备驱动程序》*，Alessandro Rubini（O'Reilly, 1998），ISBN 1-56592-292-1。这是关于如何为 Linux 编写设备驱动程序的*那本*书；它包含几个完整的实用示例。

*《Linux 内核书》*，Remy Card, Eric Dumas, Franck Mével（John Wiley and Sons, 1998），ISBN 0-471-98141-0。该书由法语翻译而来，Card 和他的合著者解释了 2.0.x 内核中几乎每一行代码。当然，由于 2.2 内核的发布，现在它已经过时了，但它仍然是一个极佳的入门读物。翻译质量粗糙且不均匀。这本书只知树木，不见森林。
