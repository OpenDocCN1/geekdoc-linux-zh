

# Linux  Java

Java 工具在 Linux 上是可用的。事实上，由 Java 的创建者 Sun 提供的完整 Java 开发包（JDK）已包含在本书 CD-ROM 的 `/contrib` 目录中。

目前 Linux 上还没有很多可以运行 Java 应用程序的产品。在 Netscape 产品方面，FastTrack Server（参见第 12 章）可以在 Web 服务器上运行 Java 应用程序（这些被称为服务器端 applet）。Netscape Navigator 浏览器可以在客户端运行 Java 应用程序（这些被称为客户端 applet），或者运行它下载的 HTML 页面中包含的 JavaScript。

用于 Linux 的其他 Java 开发工具以及在 Linux 平台上运行 Java 应用程序的系统正在开发中，在你读到这里时可能已经可以使用了。

# 使用 JavaScript

我先提到使用 JavaScript 是因为它更容易供你尝试——你可以使用现有网页内的文本编辑器开始。但 JavaScript 就像一种真正的编程语言，如果你具备一些编程背景，那么你在示例中看到的内容将会更容易理解。

# 对象和属性

JavaScript 使用了许多面向对象编程的思想。如果你对这些思想并不熟悉，它们看起来可能很奇怪，但经过一些练习后，在你编写 JavaScript 时它们将变得非常有用。

JavaScript 使用对象来存储你的脚本使用的数据。一个对象可以包含许多属性，每个属性包含一个与该对象相关的数据。例如，如果你的网站包含有关医疗程序的信息，你可能会为每种程序创建一个对象。对象的属性可以是某些项目，如程序名称、保险代码、成本以及与该程序相关的医生。

你必须将“对象类型”的概念（例如“医疗程序”）与“实际对象”（例如“阑肠切除术”）区分开来。实际对象被称为对象定义的实例。在 JavaScript 中，你使用 `new` 命令来创建对象的新实例。这是一个一个可以包含供你使用数据的实际对象。一行用于创建新变量并为其分配初始值的 JavaScript 示例代码可能如下：

```
todays_procedure = new CreateProcedure( appendectomy , 563779 ,
4290 , Devries );
```

# 第 15 章：使用 Java 和 JavaScript 395

当你在 JavaScript 代码中引用对象的属性时，在对象名称后使用一个点（`.`）。与对象一样，你必须将属性的概念与该属性中包含的值区分开。例如，下面这行 JavaScript 代码打印其中一个医疗程序：

```
document.write( Procedure: + todays_procedure.procedure_name + <BR> );
```

对象的属性也可以是另一个对象。例如，医疗程序示例中的医生可以是一个 `Doctor` 对象，而不仅仅是医生的名字。你定义的 `Doctor` 对象可能包含名称、医院和电话号码等属性。你可以像下面这样引用其中一个属性：

```
document.write( Doctor: + todays_procedure.doctor.name + <BR> );
```

# 函数和方法

面向对象编程最好的思想之一是对象持有了与一组信息相关的所有内容，包括操作该数据的代码。在这方面，JavaScript 允许你创建一个函数，定义对未命名对象的属性如何进行操作，这意味着相加、打印、存储或任何可能的操作。然后你可以作为特定对象的一部分来调用该函数。当你这样做时，该操作被称为方法（method），因为应用于应用于特定数据。这里有一个简单的示例。你可以创建一个小函数，用于打印它接收到的任何行文本。它可能如下所示：

```
function PrintLine(string) {
document.write(string + <P> );
}
```

现在你可以将该函数整合到现有的对象类型中。当你完成后，每当你引用该对象的 `PrintLine` 方法时，从该对象传递的文本将由该函数打印。你不需要为每个需要此功能的对象重写该函数。注意，上一个示例中的 `document` 对象是一个预定义对象，允许你向浏览器窗口发送信息。`document` 对象的预定义方法之一是 `write`，它向浏览器发送字符串。`document` 对象的其他属性和其他命令允许与其他浏览器窗口交互。

# 了解更多关于 JavaScript

显然，在进行大量的 JavaScript 编程之前你想学习更多。你可以从《Netscape JavaScript 编写指南》（参见 http://home.netscape.com）开始，然后通过 IDG Books Worldwide 出版的《JavaScript For Dummies》（第二版）等书籍学习更多。

# Linux Web 服务器工具包

互联网上有数百个 JavaScript applet 示例供你下载和尝试。查看这些示例的代码是学习如何实现你对自己的网站设想的最佳方式之一。

# 使用 Java

如上所述，Java 是启发 JavaScript 的语言，它仍然是周围最大的技术项目之一。由于 Java 开发包（JDK）包含在本书的 CD-ROM 中，你可以立即开始开发 Java 应用程序。

当然，在你进展太远之前，你需要一个可以执行 Java 应用程序的浏览器或服务器。JDK 将你写的源代码编译成一种特殊的字节码（byte-code），支持 Java 的浏览器或服务器可以理解它。

所有 OpenLinux 的 Netscape Navigator 浏览器以及 OpenLinux 的 Netscape FastTrack 服务器都能理解 Java applet。客户端 applet 运行在用户的浏览器中，作为其下载的 Web 页面的一部分。服务器 applet 在服务器上的脚本调用时（通常作为表单响应的一部分）运行在你的 Web 服务器上。

# 应用程序和 applet

使用 Java 时一个重要的区别是 Java 应用程序和 Java applet。如果你编写一个 Java 应用程序，它可以作为一个独立应用程序运行，就像你的文字处理器一样。但它必须有一个 Java 虚拟机（JVM）才能运行。例如，如果你有一个安装了 Java 虚拟机的 Sun Solaris 系统，那么在任何平台上编写的任何 Java 应用程序都将在 Solaris 系统上运行。这就是 Java 跨平台设计的威力。（如果你熟悉编程术语，Java 应用程序有一个 `main()` 函数并必须初始化整个环境）。

相反，applet 不是完整的应用程序。它们被编写运行在另一个应用程序内部。一旦它们加载，就成了该应用程序的一部分，并受其施加的某些限制。因此，服务器 applet 主要用于 Web Master想要使用的功能，正如 Perl 脚本分发各种功能一样。但由于 Java 被编译成字节码，商业应用程序可以使用 Java 进行开发，而无需为每个平台迁移。

# 第 15 章：使用 Java 和 JavaScript

# 面向对象语言

Java 是一种像 Smalltalk 或 C++ 一样的面向对象语言，但它不是纯面向对象的，因为它的某些数据类型是在对象之外实现的。尽管如此，对面向对象编程越熟悉，学习 Java 就越容易。

Java 使用与上述 JavaScript 类似的面向对象结构：类、对象、方法、继承、子类等。

# 安装 JDK

从本书 CD-ROM 安装 JDK 非常简单。只需如下使用 rpm 工具：

- 1. 使用如下命令挂载你的 CD-ROM：
   mount /mnt/cdrom
2. 进入 JDK 所在的 contrib 目录：
   cd /mnt/cdrom/contrib
3. 使用 rpm 命令安装 JDK：
   rpm -i JDK_static-1.0.2.pl2-1386.rpm

# 总结

在本章中，你学习了 Java 和 JavaScript 这些流行技术，以及你如何在你的 Web 服务器上使用它们为网站访问者添加功能。你学习了它们之间的区别以及何时使用每一种。

在本章中你学习了以下内容：

- Java 是一种编译语言。从 Java 编译的二进制文件需要一个特殊环境才能运行。它是跨平台的，这意味着同一个 Java 应用程序可以在支持 Java 的系统上运行。
- JavaScript 是一种解释型语言，与 Java 相似但更简单。JavaScript 程序作为 HTML 页面的一部分包含，并在下载包含 JavaScript 的 HTML 页面时由 Netscape 浏览器执行。

