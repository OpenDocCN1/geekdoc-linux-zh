

Glossary 元素除常用属性外，还接受以下属性：

- Status. 接受 CDATA 值，没有默认值，且不是可选的。

示例：

```xml
<!DOCTYPE glossary PUBLIC //OASIS//DTD DocBook V4.1//EN">
<glossary><title>我的词表</title>
<glossentry id="foo"><glossterm>foo</glsterm>
<glossdef>
<para>一个通用示例名称或术语</para>
</glossdef>
</glossary>
</glossary>
```

## Part（部分）

Part 元素开始一本书的一部分。一个部分通常是几个章节的集合。如果你有需要包含的介绍性，请参见 PartIntro 元素。

Part 元素除常用属性外，还接受以下属性：

- Label. 接受 CDATA 值，没有默认值，且不是可选的。
- Status. 接受 CDATA 值，没有默认值，且不是可选的。

示例：

```xml
<!DOCTYPE part PUBLIC "//OASIS//DTD DocBook V4.1//EN" [
<!ENTITY chapter4 SYSTEM "chapter4.sgml">
<!ENTITY chapter5 SYSTEM "chapter5.sgml">
]
<part status="draft" label="Neat">
<partintro>
<para>这是 DocBook Part 的介绍</para>
</partintro>
&chapter4;
&chapter5;
</part>
```

## Partintro（部分介绍）

PartIntro 元素持有书籍部分的介绍性文本。Part 元素不允许直接包含 Part 元素。

## 附录 B：PartIntro 元素

PartIntro 元素除常用属性外，还接受以下属性：

- Label. 接受 CDATA 值，没有默认值，且不是可选的。

## Preface（前言）

Preface 元素持有书籍的前言文本。请注意，Preface 元素在书籍中只能出现一次。Preface 元素除常用属性外，还接受以下属性：

- Status. 接受 CDATA 值，没有默认值，且不是可选的。

示例：

```xml
<!DOCTYPE book PUBLIC //OASIS//DTD DocBook V4.1//EN>
<book>
  <preface>
    <title>前言</title>
    <para>这是前言的内容</para>
  </preface>
</book>
```

## Set（集合）

Set 元素可以包含多个元素。Set 元素除常用属性外，还接受以下属性：

- Label. 接受 CDATA 值，没有默认值，且不是可选的。
- Status. 接受 CDATA 值，没有默认值，且不是可选的。

示例：

```xml
<!DOCTYPE set PUBLIC //OASIS//DTD DocBook V4.1//EN>
<set>
<title>集合</title>
<para>这是集合的内容</para>
</set>
```

## Document Structure（文档结构）

Set 元素用于处理文档结构。

## FormalPara（正式段落）

FormalPara 元素用于带有标题的段落。

```xml
<!DOCTYPE formalpara PUBLIC //OASIS//DTD DocBook V4.1//EN>
<formalpara>
  <title>正式段落标题</title>
  <para>这是正式段落的内容</
</formalpara>
```

## Para（段落）

Para 元素用于段落。请注意，如果你想要段落带有标题，必须使用 FormalPara 元素。

示例：

```xml
<!DOCTYPE para PUBLIC //OASIS//DTD DocBook V4.1//EN>
<para>
  <para>这是段落的内容</para
</para>
```

## Sect1（第一节）

Sect1 元素开始文档中的第1节。Sect1 元素不允许直接包含 Sect2 元素。

Sect1 元素除常用属性外，还接受以下属性：

- Label. 接受 CDATA 值，没有默认值，且不是可选的。
- RenderAs. 接受以下值：
- Sect2
- Sect3
- Sect4

RenderAs 属性由处理系统使用，没有默认值，且不是可选的。

Status. 接受 CDATA 值，没有默认值，且不是可选的。

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

Sect2 元素开始文档中的第2节。Sect2 元素不允许直接包含 Sect3 元素。

Sect2 元素除常用属性外，还接受以下属性：

- Label. 接受 CDATA 值，没有默认值，且不是可选的。
- RenderAs. 接受以下值：
- Sect1
- Sect3
- Sect4

RenderAs 属性由处理系统使用，没有默认值，且不是可选的。

Status. 接受 CDATA 值，没有默认值，且不是可选的。

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

Sect3 元素开始文档中的第3节。Sect3 元素不允许直接包含 Sect4 元素。

Sect3 元素除常用属性外，还接受以下属性：

- Label. 接受 CDATA 值，没有默认值，且不是可选的。
- RenderAs. 接受以下值：
- Sect1
- Sect2
- Sect4

RenderAs 属性由处理系统使用，没有默认值，且不是可选的。

Status. 接受 CDATA 值，没有默认值，且不是可选的。

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

Sect4 元素开始文档中的第4节。Sect4 元素允许直接包含 Sect5 元素。

Sect4 元素除常用属性外，还接受以下属性：

- Label. 接受 CDATA 值，没有默认值，且不是可选的。
- RenderAs. 接受以下值：
- Sect1
- Sect2
- Sect3

RenderAs 属性由处理系统使用，没有默认值，且不是可选的。

Status. 接受 CDATA 值，没有默认值，且不是可选的。

## Sect5（第五节）

Sect5 元素开始文档中的第5节。Sect5 是 DocBook 层次结构中最低层级的节——DocBook 没有任何更低级节的规定。

## Section（章节）

Section 元素是 DocBook 中不希望使用编号章节时使用的未命名元素。Section 元素可以嵌套超过五层，与 Sect1–Sect5 元素不同。

