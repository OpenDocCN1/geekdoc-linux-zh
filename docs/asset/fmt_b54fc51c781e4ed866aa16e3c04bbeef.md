
```
<!ENTITY % trademark.module INCLUDE>
[ % trademark.module;
<!ENTITY % local.trademark.attrib " ">\n<!ENTITY % trademark.role.attrib "%role.attrib;">
]
<!!ENTITY % trademark.element INCLUDE>
[ % trademark.element;
<!ELEMENT Trademark - ((#PCDATA
  |link.char.class;
  |tech.char.class;
  |base.char.class;
  |other.char.class;
  |InlineGraphic
  |InlineMediaObject
  |Emphasis))+>
<!---end of trademark.element->]>
```

```
<!ENTITY % trademark.attlist INCLUDE>
[ % trademark.attlist;
<!ATTLIST Trademark
```

Class：更精确地标识元素名称

| Class | Service |
| --- | --- |
| Trade | Registered |
| Copyright | Trade %common.attrib; %trademark.role.attrib; %local.trademark.attrib; |

```
<-end of trademark.attlist->>
<-end of trademark.module->
```

这看起来可能很令人困惑，但它只是冗长。我会将其拆解开，让它看起来更有意义。

```
<!ENTITY trademark.module "INCLUDE">
[: %trademark.module; [
<!ENTITY local.trademark.attrib "%role.attrib;">
```

这是实体声明，它告诉解析器存在一个名为 `Trademark` 的实体，并且应该包含它。第三行和第四行为 `Trademark` 元素声明了一个属性。接下来的几行让解析器知道哪些元素作为 `Trademark` 元素的子元素出现。某些元素被声明为组，例如 `tech` 元素组。其他元素（如 `InlineGraphic`）被显式声明。`Trademark` 声明的最后部分定义了 `Trademark` 的属性，包括 `Class` 属性的可接受值。所有这些信息的实际用途是让 Jade 或你使用的任何解析工具在你在使用无效属性时，能够给你提供一个类似图 10.1 所示的错误消息。如你在图 10.1 所示，DocBook DTD 是非常复杂的。并不是说这些东西很复杂，它们显然比说英语并不更困难。然而，正如我们所知，英语由许多规则组成，在你说出明智的话之前，必须先理解这些规则。当你编写 DTD 时，这与创建一个语言非常相似，所以如果你尝试修改语言，必须非常小心。

## DocBook 层级结构

尽管 DocBook 中的大多数元素包含在信息池模块 `dbpool.mod` 中，但 DocBook 中所有的层级元素都包含在层级模块 `dbhier.mod` 中。如果你想获取 DocBook 中任何层级元素的信息（例如 `Section` 或 `Book` 元素），请查看此文件。文件的结构和语法与其他文件相同，但为了组织目的，DocBook 技术委员会将层级内容分离到了此文件中。

## 自定义 DocBook DTD

![](img/81f56bf497dbf7f7582072400d12cb42_234_0.png)

图 10.1 Jade 对无效属性的错误

## DocBook 字符实体

DocBook 字符实体文件是 `dbent.mod`。该文件没有包含很多信息；而是调用了包含 ISO 字符实体的各种文件。如果你在解析 DocBook 文档时系统中没有 ISO 实体，你将得到大量的错误。

## DocBook 目录

所有的 DocBook 信息都包含在 `docbook.cat` 中，用于构建你自己的目录文件。如果你有与目录文件相关的 Jade/OpenJade 错误，这里的信息在调试时有用。

## DocBook SGML 声明

`docbook.dtd` 文件包含了 DocBook 的所有 SGML 声明。当你看到像图 10.2 所示的错误（抱怨缺少标签但其声明不允许省略标签）时，这就是省略标签的声明所在。

```
book-patron:/Writing/Prima/SQL$ tools -b html Test.m
/usr/bin/jade:OSD:016:409:E: end tag for "ACRONYM" omitted, but its declaration does net syntax error
/usr/bin/jade:OSD:016:300: start tag was here
book-patron:/Writing/Prima/SQL$ $
```

![](img/81f56bf497dbf7f7582072400d12cb42_235_0.png)

图 10.2 一个 Jade 错误

## DocBook 符号（Notations）

`dbnot.mod` 文件包含了 DocBook 的符号。这包括对大多数类型二进制图形文件的引用。

## 自定义样式表

如果你想从 DocBook 获得不同的外观和感受，没有必要更改 DTD。输出的外观和感受是由样式决定的，而不是 DTD。正如前面提到的，DocBook 的妙处在于允许结构与内容的分离。事实上，通过切换样式，你可以在不重新格式化文档的情况下完全改变显示方式。这是 DocBook 相比 Microsoft Word 等 GUI 工具的一个优势。尽管 Word 具有许多精妙的格式化功能，但无法根据文档中包含的信息来重新格式化它。例如，使用 DocBook，你可以创建一个只显示 `Author` 和 `Editor` 元素的样式表。Word 会对这种请求感到困惑。

> 我一直认为多年来 Word 包含了一些没有人使用的功能，以及大多数人不知道的功能。

![](img/81f56bf497dbf7f7582072400d12cb42_236_0.png)

## 理解 DSSSL

好了，你可能正看着这个缩写，认为阅读一个五个字母缩写（FLA）比标准的三个字母缩写（TLA）难得多。别担心，文档样式语义规范语言（Document Style Semantics and Specification Language）比起你看过的其他技术并不差，它只是很冗长。

DSSSL 是一种样式语言。它是 Scheme 和 Lisp 编程语言的派生物，这就是为什么它有这么多括号。

> 我认识的一位老程序员曾说过，Lisp 实际上应该是大量阴险的括号（Lots of Insidious Parentheses）。如果你用 Lisp 程序，你会发现自己一直在敲括号键，至少是这样。

![](img/81f56bf497dbf7f7582072400d12cb42_236_1.png)

对 DSSSL 的全面概述远超本书的范围。DSSSL 是一个功能非常强大的语言。然而，我将提供一些自定义样式表的示例来帮助你开始。

## 修改现有的样式表

通常，修改现有的样式表比从头开始编写要好。记住，DocBook 拥有 300 多个元素，你不想从头开始编写一个支持 300 多个元素及其属性的样式表。

## 第 18 章：自定义 DocBook

### 其他样式表

除了 DocBook 自带的样式表外，还有几种样式表可以免费获取。KDE、GNOME、Debian、FreeBSD 以及网络上的其他几个项目都提供了自定义的 DocBook 样式表。虽然你可能仍然需要对它们进行进一步自定义（特别是如果你编写的内容不是这些项目之一的话），但你可能会发现其中某个组织提供的外观和感觉比默认的 DocBook 样式表更佳。查看它们的源代码也会让你比只看 DocBook 样式表更清晰地理解这些概念。

## 编写本地样式表

自定义 DocBook 样式表，你可以直接修改现有样式表，也可以创建一个本地化的驱动文件，通过该文件进行你的修改，并依赖未修改的 DocBook 默认样式表来处理其余部分。

编写本地样式表要明智得多，因为它更容易管理。你不需要费力研究包含在内的样式表，只需编写一个与样式表配合的插件即可，这个文件要小得多，也更容易管理。

开始之前，你需要一个文档声明，就像普通的 DocBook 文档一样。它看起来应该像这样：

```
<DOCTYPE style-sheet PUBLIC "-//Zonker's Stylish Sheet//EN" [
  <ENTITY dbstyle PUBLIC "-//Norman Walsh//DOCUMENT DocBook Print
Stylesheets//EN" CDATA DTD>
```
