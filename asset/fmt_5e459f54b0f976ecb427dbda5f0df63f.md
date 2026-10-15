
```c
  } else {

    return fibonacci(n - 1) + fibonacci(n - 2);

  }

}
```

`indent` 在输出重格式化时相当激进，它会根据自己的需要合并和断行。有几十个选项可以控制这些细节，所以你通常可以从一种基本样式开始，并用额外的选项进行微调。例如：

```bash
$ indent -kr -bl -blio0 -nce
```

这采用了 K&R 样式，并告诉 `indent` 将大括号单独放在一行 (`-bl`) 且不进行额外的缩进 (`-blio0`)。最后，它告诉 `indent` 将 `else` 保持单独一行 (`-nce`)。这些选项可以组合在文件名 `.indent.pro` 中，该文件可能存在于当前目录或你的主目录。例如：

```text
-kr -bl -blio0 -nce
```

如果该文件位于你的主目录，那么每当你运行 `indent` 时，这些将成为默认选项。或者，如果你参与了具有不同缩进样式的多个项目，可以在每个项目目录中放置一个唯一的 `.indent.pro`。

### 4.4.2 Astyle 艺术风格

另一个很有前景的开源格式化工具叫做 `astyle`¹12。像 `indent` 一样，`astyle` 理解 C 和 C++，但也理解 Java 和（惊呆！）C#。在这里，`astyle` 不支持 Emacs 支持的所有格式，但它确实为 K&R、GNU 和 Linux 样式提供了定义的格式，以及它称为 ANSI 样式的格式。

> 12. http://sourceforge.net/projects/astyle

`astyle` 在重格式化方面没有 `indent` 激进。除非你明确告诉它它可以断开什么类型的行，否则它不会断行。它不会将跨多行的语句合并为单行。例如，这对于列表 4-1 效果并不好。列表 4-4 显示了列表 4-1 用 `astyle` 处理后的结果。

#### 列表 4-4 使用 astyle 的 ANSI 样式示例

```c
unsigned int fibonacci(unsigned int)
{
    if ( n < 2 ) {
        return n;
    } else {
        return
            fibonacci( n - 1)
            fibonacci( n - 2);
    }
}
```

注意这种样式与上一节创建的修改版 K&R 样式几乎相同，只是第二个返回语句仍然占据了三行。

### 4.4.3 使用 cflow 分析代码

POSIX `cflow` 命令将你的源代码转换为调用图，允许你看到程序流的概述。这对于查看未知代码非常有用。GNU 有一个 POSIX `cflow`¹ 命令的版本，虽然不完全符合 POSIX 标准，但仍然非常有用。让我们以列表 4-5 为例。

> 13. www.gnu.org/software/cflow

#### 列表 4-5 ex4-5.c

```c
1 void zfunc(void) { afunc(); }
2
3 void xfunc(void) { zfunc(); }
4
5 void afunc(void) { afunc(); }
6
7 void recurs(void) { recurs(); }
8
9 void mainfunc() {
10
11 xfunc();
12
13 recurs();
14 }
```

这个模块足够简单可以说明 `cflow` 的工作原理。使用 `cflow` 的 POSIX 格式，你得到以下内容：

```bash
$ cflow --format=posix ex4-5.c
1 afunc: void (void), <ex4-5.c 5>      afunc calls itself
2 afunc: 1
3 mainfunc: void (), <ex4-5.c 9>      mainfunc calls xfunc()
4 xfunc: void (void), <ex4-5.c 3>      xfunc calls zfunc()
5 zfunc: void (void), <ex4-5.c 1>      zfunc calls afunc()
6 afunc: 1
7 recurs: void (void), <ex4-5.c 8>
```

（注：由于原文文本在后续出现了极其严重的重复和乱码，此处已根据逻辑停止重复翻译。）

## 4.4 源代码格式化工具与浏览器

### 4.4.5 使用 cscope 浏览代码

`cscope` 是一个用于查看代码的文本模式浏览器。它根据你提供的源文件列表创建自己的数据库，然后进入一个 ncurses 文本菜单系统。使用 `cscope` 需要一个终端模拟器。图 4-14 所示。

屏幕被分为两半。屏幕上半部分的每一行都显示一行匹配最近查询的代码。屏幕下半部分包含几种支持的查询类型的输入字段，例如“查找此 C 符号”。大多数程序员应该觉得这些查询是通俗易懂的。`Tab` 键可以让你在屏幕的上下半部分之间切换，上下方向键则可以在每个部分的行之间移动。在屏幕下半部分的相应字段中输入查询，结果将出现在上半部分。将光标移动到上半部分的某一个匹配项上，`cscope` 就会调用你喜欢的编辑器并带你到该行代码。

不用多说，这是一个非常有交互性的工具。`cscope` 的静态输出功能有限。`>` 字符会将当前的匹配列表保存到文件中，你还可以对其进行追加操作。没搞错——`cscope` 的设计初衷就是为了交互式使用。

![](img/9c04dc9e840dfb086a38289961386a14_237_0.png)

图 4-14 Cscope 菜单系统

### 4.4.6 使用 Doxygen 浏览和记录代码

`Doxygen` 是一个优秀的工具，主要用于为软件项目生成文档。它能够解析你的 C 和 C++ 代码并生成超链接文档（通常是 HTML）供浏览。此外，你可以在代码中添加一些轻量级标记，`Doxygen` 将将其包含在文档中。以下是函数的充分文档示例：

```c
/**
 * 这是一个函数。
 */
 void func(void)
{
```

Java 程序员会熟悉这种 javadoc 语法。事实上，`Doxygen` 在很大程度上借鉴了 javadoc。这是一种轻量级标记语法，允许你编写可以在文本编辑器中的注释，并为文档生成高质量的排版输出。

`Doxygen` 可以生成 HTML、LaTeX、PDF、RTF 甚至 man 页面（例如 troff）。它还可以使用 Graphviz 工具 (`dot`) 为 C++ 类生成复杂的 UML 图。这是验证使用 UML 语法的设计的极佳工具。如果你从 UML 设计开始，你应该能够从源代码生成相同的图表。

使用 `Doxygen` 的第一步是创建一个 `Doxyfile`，该文件包含了你对特定项目的所有偏好设置。一个极简的 `Doxyfile` 如下：

```
INPUT              =
FILE_PATTERNS = *.cpp
```

这告诉 `Doxygen` 选取当前目录下的所有 `.cpp` 文件。默认情况下，它会在单独的子目录下生成 HTML 和 LaTeX 输出。创建 `Doxyfile` 更常用的方法是使用程序通过 `-g` 选项创建骨架文件，如下所示：

```bash
$ doxygen -g
```
