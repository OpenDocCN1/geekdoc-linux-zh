
```xml
<!DOCTYPE formalpara PUBLIC //OASIS//DTD DocBook V4.1//EN>
<formalpara>
  <title>正式段落标题</title>
  <para>这是正式段落的内容</
</formalpara>
```

## Para（段落）

`Para`元素用于段落。请注意，如果你想要段落带有标题，必须使用`FormalPara`元素。

示例：

```xml
<!DOCTYPE para PUBLIC //OASIS//DTD DocBook V4.1//EN>
<para>
  <para>这是段落的内容</para
</para>
```

## Sect1（第一节）

`Sect1`元素开始文档中的第1节。`Sect1`元素不允许直接包含`Sect2`元素。

`Sect1`元素除常用属性外，还接受以下属性：

- `Label`. 接受`CDATA`值，没有默认值，且不是可选的。
- `RenderAs`. 接受以下值：
  - `Sect2`
  - `Sect3`
  - `Sect4`
`RenderAs`属性由处理系统使用，没有默认值，且不是可选的。
`Status`. 接受`CDATA`值，没有默认值，且不是可选的。

示例：

```xml
<!DOCTYPE chapter PUBLIC //OASIS//DTD DocBook V4.1//EN>
<chapter>
  <title>第一章</title>
  <sect>
    <title>第一节</title>
    <para>这是第一节的内容</para
  </sect>
</chapter>
```

## Sect2（第二节）

`Sect2`元素开始文档中的第2节。`Sect2`元素不允许直接包含`Sect3`元素。

`Sect2`元素除常用属性外，还接受以下属性：

- `Label`. 接受`CDATA`值，没有默认值，且不是可选的。
- `RenderAs`. 接受以下值：
  - `Sect1`
  - `Sect3`
  - `Sect4`
`RenderAs`属性由处理系统使用，没有默认值，且不是可选的。
`Status`. 接受`CDATA`值，没有默认值，且不是可选的。

示例：

```xml
<!DOCTYPE chapter PUBLIC //OASIS//DTD DocBook V4.1//EN>
<chapter>
  <title>第一章</title>
  <sect>
    <title>第二节</title>
    <para>这是第二节的内容</para
  </sect>
</chapter>
```

## Sect3（第三节）

`Sect3`元素开始文档中的第3节。`Sect3`元素不允许直接包含`Sect4`元素。

`Sect3`元素除常用属性外，还接受以下属性：

- `Label`. 接受`CDATA`值，没有默认值，且不是可选的。
- `RenderAs`. 接受以下值：
  - `Sect1`
  - `Sect2`
  - `Sect4`
`RenderAs`属性由处理系统使用，没有默认值，且不是可选的。
`Status`. 接受`CDATA`值，没有默认值，且不是可选的。

示例：

```xml
<!DOCTYPE chapter PUBLIC //OASIS//DTD DocBook V4.1//EN>
<chapter>
  <title>第一章</title>
  <sect>
    <title>第三节</title>
    <para>这是第三节的内容</para
  </sect>
</chapter>
```

## Sect4（第四节）

`Sect4`元素开始文档中的第4节。`Sect4`元素允许直接包含`Sect5`元素。

`Sect4`元素除常用属性外，还接受以下属性：

- `Label`. 接受`CDATA`值，没有默认值，且不是可选的。
- `RenderAs`. 接受以下值：
  - `Sect1`
  - `Sect2`
  - `Sect3`
`RenderAs`属性由处理系统使用，没有默认值，且不是可选的。
`Status`. 接受`CDATA`值，没有默认值，且不是可选的。

## Sect5（第五节）

`Sect5`元素开始文档中的第5节。`Sect5`是 DocBook 层次结构中最低层级的节——DocBook 没有任何更低级节的规定。

## Section（章节）

`Section`元素是 DocBook 中不希望使用编号章节时使用的未命名元素。`Section`元素可以嵌套超过五层，与`Sect1`–`Sect5`元素不同。

示例：

```
<section>
<para>This is a section</para>
<section>
<para>And this is a section within a section</para>
</section>
</section>
```

## SimPara

`SimPara`元素类似于`Para`元素，但对可以嵌套其中的元素类型限制更严格。

`SimPara`元素使用通用属性。

示例：

```
<!DOCTYPE simpara PUBLIC "//OASIS//DTD DocBook V4.1//EN">
<simpara>This is simple, huh?</simpara>
```

## SimpleSect

`SimpleSect`元素是 DocBook 文档中的一个章节，其没有子章节。

`SimpleSect`元素使用通用属性。

示例：

```
<!DOCTYPE sect1 PUBLIC "//OASIS//DTD DocBook V4.1//EN">
<sect1><title>Our Elements</title>
<para>There are lots and lots of DocBook elements.</para>
<simplesect><title>Structure Elements</title>
<para>FormalPara is a Structure Element.</para>
</simplesect>
</sect1>
```

## ToC

`TOC`元素用于 DocBook 文档的目录。

除了通用属性外，`TOC`元素还接受以下属性：

- `PageNum`. 接受`CDATA`值，没有默认值，且不是必填。

## 示例：

```
<!DOCTYPE toc PUBLIC "//OASIS//DTD DocBook V4.1//EN">
<toc>
<tocfront>Introduction</tocfront>
<tocchap>
  <tocentry>Getting Started with DocBook</tocentry>
  <toclevel1>
    <tocentry>Creating DocBook Documents</tocentry>
    <toclevel2>
      <tocentry>SGML or XML</tocentry>
    </toclevel2>
  </toclevel1>
</tocchap>
<tocback>Appendix</tocback>
</toc>
```

## ToBack

`ToBack`元素包含文档后文（如词表或附录）的目录项。

`ToBack`元素除了通用属性外，还接受以下属性：

- `Label`. 接受`CDATA`值，没有默认值，且不是必填。
- `Linkend`. 接受`IDREF`值，没有默认值，且不是必填。
- `Pagenum`. 接受`CDATA`值，没有默认值，且不是必填。

示例：

参见`ToC`元素示例。

## ToCChap

`ToCChap`元素包含目录中的章节项。

`ToCChap`元素除了通用属性外，还接受以下属性：

- `Label`. 接受`CDATA`值，没有默认值，且不是必填。

示例：

参见`ToC`元素示例。

## ToEntry

`ToEntry`元素用于目录中的任何项。

`ToEntry`元素除了通用属性外，还接受以下属性：

- `Linkend`. 接受`IDREF`值，没有默认值，且不是必填。
- `Pagenum`. 接受`CDATA`值，没有默认值，且不是必填。

示例：

参见`TOC`元素示例。

## ToCfront

`ToCfront`元素包含目录中指向前文（如前言或引言）的引用。

`ToCfront`元素除了通用属性外，还接受以下属性：

- `Label`. 接受`CDATA`值，没有默认值，且不是必填。
- `Linkend`. 接受`IDREF`值，没有默认值，且不是必填。
- `Pagenum`. 接受`CDATA`值，没有默认值，且不是必填。

示例：

参见`TOC`元素示例。

## ToClevel1

`ToClevel1`元素包含目录中指向 1 节的引用。

`ToClevel1`元素使用通用属性。

示例：

参见`TOC`元素示例。

## ToClevel2

`ToClevel2`元素包含目录中指向 2 节的引用。

`ToClevel2`元素使用通用属性。

示例：

参见`TOC`元素示例。

## ToLevel3

`ToLevel3`元素包含目录中指向 3 节的引用。
