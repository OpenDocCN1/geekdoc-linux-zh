

本章及后续两章将更详细地介绍 Linux 下可用的 shell。大多数 Linux 系统都附带多个 shell，包括 **bash**、**pdksh** 和 **tcsh**。我们将从 **bash**（Bourne Again Shell）开始，因为它是 Linux 的默认 shell，也是新用户最流行的 shell。我们还将介绍最常用 bash 命令以及 bash 使用的环境变量。读完本章后，你应该能够更快速、更高效地使用 bash。

## Shell 简史

什么是 shell？在 Linux 中，这个词似乎被频繁使用，但对于许多新用户（甚至一些老手）来说，其确切含义仍然模糊。本节将解释什么是 shell 程序，以及为什么它在 Linux 使用中如此重要。

### 什么是 Shell？

Shell 是一个用于在你（用户）和 Linux（或更准确地说，你和 Linux 内核）之间进行交互的程序。图 11.1 说明了用户、shell 和 Linux 内核之间的关系。你在屏幕提示符处输入的每条命令都会由 shell 解释，然后传递给 Linux 内核。

![](img/e8e6b47ac20475e23d48b4c476f5d891_241_0.png)
![](img/e8e6b47ac20475e23d48b4c476f5d891_241_1.png)

**注意**
如果你熟悉 MS-DOS，你会意识到这种关系与 DOS 用户和 COMMAND.COM 程序之间的关系几乎相同。唯一的实质区别在于，在 DOS 世界中，没有对 COMMAND.COM 程序和 DOS（或更准确地说，DOS 内核）进行区分。

Shell 是一个命令语言解释器。它拥有一套内置的 shell 命令。Shell 还可以利用系统中所有可用的 Linux 实用程序和应用软件。

每当你输入一条命令时，它都会由 Linux shell 进行解释。例如，在前面的章节中，当你开始了解 Linux 文件和目录操作命令时，在命令提示符处输入的所有示例命令都是由你所使用的 Linux shell 进行解释的。

有些命令，如打印工作目录（pwd）命令，是内置于 Linux bash shell 中的。其他命令，如复制命令（cp）和删除命令（rm），则是作为独立的可执行程序存在于文件系统的某个目录中。作为用户，你并不关心（或可能不关心）该命令是内置于 shell 的还是一个独立的程序。图 11.2 展示了 shell 如何执行这种命令解释。

**图 11.2.**
*Shell 的命令解释。*

![](img/e8e6b47ac20475e23d48b4c476f5d891_242_0.png)

图 11.2 说明了 shell 决定如何处理用户命令（如 *cd* 或 *pwd*）所执行的步骤。如果该命令不属于这些内置项之一，shell 会检查它是否是一个应用程序。应用程序可以是 Linux 自带的实用程序，如 *ls* 和 *rm*，也可以是作为商业软件（如 *xv*）或公共领域软件（如 *ghostview*）发行的应用程序。

Shell 通过搜索所有位于搜索路径中的目录来尝试查找这些应用程序。正如我们在前面章节中提到的，*path*（路径）是一个列出了可找到可执行程序的目录列表。如果输入的命令既不是内部 shell 命令，也不是路径中的可执行文件，系统会显示类似的错误信息：

```bash
$ doit
doit: not found
```

在成功执行命令的最后一步，shell 的内部命令和所有应用程序最终会被分解为系统调用，并传递给 Linux 内核。

Shell 的另一个重要方面是它包含一个非常强大的解释型编程语言。这种语言在功能上类似于 MS-DOS 的解释语言，但灵活得多。Shell 编程语言支持高级语言中常见的大多数编程结构，如循环、函数、变量和数组。

### Shell 如何启动

在本章前面，你已经了解到，shell 是用户与 Linux 内核交互的主要方式。但此程序是如何初始化的呢？shell 在你成功登录系统后启动，并持续作为用户与内核之间交互的主要方式，直到你注销。

系统中的每个用户都有一个默认 shell。每个用户的*默认 shell*在系统密码文件（称为 */etc/passwd*）中指定。*系统密码文件*包含（除其他内容外）每个用户的用户 ID、每个用户密码的加密副本，以及用户登录系统后立即运行的程序名称。密码文件中指定的程序不一定是 Linux shell，但几乎总是如此。

## 最常见的 Shell

Linux 和 UNIX 系统上有几种不同的 shell。最常见的是 Bourne shell（称为 sh）、C shell（csh）和 Korn shell（ksh）。这三种 shell 各有其优缺点。

*The Bourne shell* 由 Steven Bourne 编写。它是原始的 UNIX shell，在现有的每个 UNIX 系统上都可用。Bourne shell 被认为非常适合 UNIX shell 编程，但它处理用户交互的能力不如其他一些可用的 shell。

*The C shell* 由 Bill Joy 编写，对用户交互的反应更加灵敏。它支持 Bourne shell 中没有的功能，例如命令行补全。许多人认为 C shell 的编程接口不如 Bourne shell 好，但由于其编程语言的语法与 C 语言相似，因此被许多 C 程序员使用。这也是它被称为 C shell 的原因。

*The Korn shell (ksh)* 由 Dave Korn 编写。他提取了 C shell 和 Bourne shell 的最佳特性，并将它们结合成一个与 Bourne shell 完全兼容的版本。ksh 高效，既拥有良好的交互界面，也拥有良好的编程接口。

**注意**

关于 Bourne、C 和 Korn shell 有许多高质量的参考书籍。如果你想使用这些 shell 而不是本章及后续两章中讨论的三个 shell，你可能需要找到一本关于你偏好的特定 shell 的好参考书。由于 Linux 自带的 shell 是大多数人使用的，我们将重点介绍这些 shell。

除了这些 shell，许多其他 shell 程序从一个或多个现有 shell 中提取了基本特性，并将它们组合成一个新版本。本书中讨论的三种较新的 shell 是 tesh（csh 的扩展）、Bourne Again Shell（bash，sh 的扩展）和 Public Domain Korn Shell（pdksh，ksh 的扩展）。bash 是大多数 Linux 系统的默认 shell。

## Bourne Again Shell

Bourne Again Shell（bash），顾名思义，是 Bourne shell 的扩展。bash 与 Bourne shell 完全向后兼容，但包含了许多 Bourne shell 中没有的增强功能和额外特性。bash 还包含 C shell 和 Korn shell 中许多最佳特性。bash 拥有一个非常灵活且强大的编程接口，以及用户友好的命令接口。

为什么使用 bash 而不是 sh（原始的 Bourne shell）？Bourne shell 最大的缺点在于它处理用户输入的方式。在 Bourne shell 中输入命令可能非常繁琐，特别是如果你经常使用它并输入大量命令。bash 提供了若干功能，使输入命令变得更加容易。

## 命令行补全

通常，当你在 bash（或任何 shell）中命令时，并不一定需要输入命令的完整文本，shell 就能确定你想让它做什么。例如，假设当前工作目录包含以下文件和子目录：

```text
News/ bin/ games/ mail/ samplefile test/
```

如果你想从当前工作目录切换到 test 子目录，请输入命令：

```bash
cd test
```

虽然这条命令工作得很好，但 bash 允许你以一种略有不同（且更快）的方式完成同样的事情。由于 test 是目录中唯一以字母 *t* 开头的文件，bash 应该能够在你只需输入 *t* 后就弄清楚你想做什么：

```bash
cd t
```

在输入字母 *t* 后，你可能指的是唯一的 *test* 子目录。为了让 bash 帮你完成命令，请按 Tab 键：

```bash
cd t<tab>
```

执行此操作时，bash 会完成命令并将其显示在屏幕上。命令不会实际执行，直到你按下回车键，以确认 bash 生成的命令确实是你打算执行的命令。

对于这样短的命令，你可能看不到使用命令行补全的很大价值。对于短命令，使用此功能起初可能会降低你的速度。但是，当你习惯了使用命令行补全，并且你输入的命令稍长一些时，你会想知道没有这个功能时别人是怎么生活的。

