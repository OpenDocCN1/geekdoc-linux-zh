

## 声明书籍

最后，如果有多个人同时在编写一本书，实施集中式版本控制系统是一个好主意。这种系统允许人们在维护原始文件的同时提取（checkout）和提交（check）材料，允许多人在同一文件上工作，同时保留原始文件以供以后参考。你可能会发现你想撤销编辑器或其他作者所做的某些更改。拥有文件的旧版本会让这变得容易得多。你可以在第 7 章“协作工作”中了解更多关于版本控制系统和自由软件 CVS 程序。

有很多版本控制系统，但 CVS 是可用的最流行的版本之一。它还具有自由软件的优点，以及几个 GUI 前端，可以为那些不喜欢命令行的人让生活变得更简单。

![](img/81f56bf497dbf7f7582072400d12cb42_90_0.png)

## 声明书籍

在 DocBook 中，制作书籍或任何 DocBook 文档的第一步是声明你的文档类型。我在第 1 章“入门”中详细介绍了文档类型，所以如果你对文档声明不熟悉，你可能想回到第 1 章复习一下。这是一个带有前言、四章、索引、术语表、附录和参考文献的书的简单声明（见图 4.2）。你将把文件命名为 book.sgml，或者如果你在使用 XML，则命名为 book.xml。

```xml
<!DOCTYPE book "-//OASIS//DTD DocBook V4.1//EN">
<!ENTITY preface SYSTEM "preface.sgml">
<!ENTITY chapter2 SYSTEM "chapter2.sgml">
<!ENTITY chapter3 SYSTEM "chapter3.sgml">
<!ENTITY chapter4 SYSTEM "chapter4.sgml">
<!ENTITY index SYSTEM "index.sgml">
<!ENTITY glossary SYSTEM "glossary.sgml">
<!ENTITY appendix SYSTEM "appendix.sgml">
<!ENTITY bibliography SYSTEM "bibliography.sgml">

<book>
&preface;
&chapter1;
```

## 第 4 章：使用 DocBook 准备书籍

&chapter2;
&chapter3;
&chapter4;
&index;
&glossary;
&appendix;
&bibliography;
&</book>

这是一个针对 SGML DocBook 书籍的有效声明。请注意，它本身内部不包含任何文本。

将其分解来看，第一行是文档声明本身。在这里，你正在告诉任何解析该文件的应用程序这是什么种类型的文档，以及预期是什么。接下来的行被包含在括号内并以 <ENTITY 开头，为解析器声明实体。这些不是 DocBook 实体；而是引用你系统上文件的实体。这允许你在 Book 元素下引用下的实体

![](img/81f56bf497dbf7f7582072400d12cb42_91_0.png)

```xml
<!DOCTYPE book PUBLIC "-//DTD//DocBook V4.1//EN// >
  <!ENTITY preface SYSTEM "preface.sgml">
  <!ENTITY chapter1 SYSTEM "chapter1.sgml">
  <!ENTITY chapter2 SYSTEM "chapter2.sgml">
  <!ENTITY chapter3 SYSTEM "chapter3.sgml">
  <!ENTITY index SYSTEM "index.sgml">
  <!ENTITY glossary SYSTEM "glossary.sgml">
  <!ENTITY appendix SYSTEM "appendix.sgml">
  <!ENTITY bibliography SYSTEM "bibliography.sgml">
```

图 4.2 Vim 中的书籍声明

## 声明书籍

使用和符号 (&) 和分号 (;) 来引用所声明的实体。与其将书籍的全部文本包含在一个文件中，不如将其分成若干文件，并将它们声明为实体，然后从主 book.sgml 中调用。例如，你不是包含前言的文本，而是包含对前言的引用。当文档被解析时，解析器将 &preface; 读取为“包含系统文件.sgml 并解析它”。

XML 声明几乎相同。图 4.3 显示了 XML 文档的声明。

```xml
<xml version="1.0"?>
<!DOCTYPE book PUBLIC "-//OASIS//DTD DocBook V4.1//EN"
  "//file:///user/share/xml/docbook/4.1/docbookx.dtd"> [
  <!ENTITY preface SYSTEM "preface.xml">
  <!ENTITY chapter1 SYSTEM "chapter1.xml">
  <!ENTITY chapter2 SYSTEM "chapter2.xml">
  <!ENTITY chapter3 SYSTEM "chapter3.xml">
  <!ENTITY chapter4 SYSTEM "chapter4.xml">
  <!ENTITY index SYSTEM "index.xml">
  <!ENTITY glossary SYSTEM "glossary.xml">
  <!ENTITY appendix SYSTEM "appendix.xml">
  <!ENTITY bibliography SYSTEM "bibliography.xml">
]

<book>
  &preface;
  &chapter1;
  &chapter2;
  &chapter3;
  &chapter4;
  &index;
  &glossary;
  &appendix;
  &bibliography;
</book>
```

这就是 Book 文档类型声明的全部内容。Book 元素和示例中 Book 元素内部调用的实体并不是声明本身，但它们是为了展示 DocBook 书籍的样式。

### 4.3 XML 的声明

### BookInfo 元素

### 声明书籍

### 为什么你会想要包含章节号？

### 在 HTML 中渲染的信息

![](img/81f56bf497dbf7f7582072400d12cb42_94_0.png)

- 书
- 目录
- 手册
- 作者
- 客户名称
- 编辑
- 客户地址
- 促销

