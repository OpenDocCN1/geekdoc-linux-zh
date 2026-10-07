

# 元素引用

## 329

BeginPage 元素除了通用属性外，还接受 Pagenum 属性。

示例：

```xml
<beginpage pagenum="300">
```

## BlockQuote（块引用）

BlockQuote 元素表示应与其他文本区分的引用。通常，任何三行或以上的引用都应该包含在 BlockQuote 中。

BlockQuote 元素使用通用属性。

示例：

```xml
<para>引用自《人月神话谭》：</para>
<<blockquote><attribution>Frederick Brooks Jr.</attribution>
<para>随着系统的启动，组件构建者会随着时间的推移而出现，带着他们组件的热门版本——更快、更小、更完整，或者被认为有缺陷。用新组件替换运行良好的组件需要与添加新组件相同的系统化测试程序，尽管所需的时间更短，因为通常会有更完整、更高效的测试用例。</para>
</blockquote>
```

## BridgeHead（桥头）

BridgeHead 元素创建一个没有关联文本的标题。

BridgeHead 元素除了通用属性外，还使用此属性。

- RenderAs。标识如何渲染 BridgeHead。

示例：

```xml
<chapter>
<bridgehead rederas="sect1"> 头部</bridgehead>
<para>...</para>
</chapter>
```

## Callout（注/提示）

Callout 元素表示某种类型的提示。

## 附录 B：DocBook 元素引用

Callout 元素除了通用属性外，还使用此必需属性。

- AreaRefs

示例：

```xml
<Calloutlist>
<title>我的注释</title>
<callout arearefs="opinion1">
<para>这家伙是个呆瓜</para>
</callout>
</CALLOUTLIST>
```

## Calloutlist（提示列表）

CalloutList 元素包含 Callout 元素的列表。

CalloutList 元素使用通用属性。

示例：

参见 Callout 元素示例。

## Caution（注意）

Caution 元素表示应与其他文本区分的文本块，以引起对其内容的注意。在大多数格式系统中，Caution 元素还会导致随该元素显示某种警告图形。

Caution 元素使用通用属性。

示例：

```xml
<caut>
<para>不要拿着剪刀跑步</para>
</caut>
```

## CO（行内提示）

CO 元素表示行内提示的位置。

CO 元素使用通用属性。

示例参见 MediaObjectCO 元素。

## 元素引用

## 31

## Emphasis（强调）

Emphasis 元素表示应以某种方式强调的文本。这比 HTML 等标记语言更好，因为 HTML 允许直接调用斜体或粗体文本。当文本通过文本转语音设备读取或被渲染为纯文本时，斜体和粗体都会丢失。

Emphasis 元素使用通用属性。

示例：

```xml
<para>我<emphasis>真的</emphasis>累了。</para>
```

## Equation（公式）

Equation 元素表示一个公式。

Equation 元素除了通用属性外，还接受以下属性：

- Label。接受 CDATA 值，没有默认值，且不是必需。

示例：

```xml
<equation><title>毕哥哥定理</title>
<alt>a^2 + b^2 = c^2</alt>
<graphic fileref="equations/pythagorean.gif"></graphic>
</equation>
```

## Important（重要）

与 Caution 元素类似，Important 元素表示应从正文中区分出来的重要文本。

Important 元素使用通用属性。

示例：

```xml
<important>
<para>永远不要以表看人。</para>
</important>
```

## InlineEquation（行内公式）

InlineEquation 元素表示应在文本正文中显示的元素。

InlineEquation 元素使用通用属性。

## 附录 B：DocBook 元素引用

示例：

```xml
<para>毕哥哥定理是：
<inlineequation>
<alt>a^2 + b^2 = c^2</alt>
<graphic fileref="equations/pythagorean.gif*"></graphic>
</inlineequation>
</para>
```

## ItemizedList（无序列表）

ItemizedList 元素包含一个用符号或其他指定标记标记的项目列表。这与 OrderedList 元素有所不同，后者包含一个按顺序标记的列表。

ItemizedList 元素除了通用属性外，还使用这些属性。

- Spacing。接受 Compact 或 Normal 作为值，没有默认值，且不是必需。
- Mark。接受符号、破折号或其他符号，不是必需。

示例：

```xml
<listitemized mark=dash>
<listitem><para>HTML</para></listitem>
<listitem><para>SGML</para></listitem>
<listitem><para>XML</para></listitem>
</listitemized>
```

## literallayout（原样输出）

LiteralLayout 元素表示应按原样显示的文本。LiteralLayout 标记标签之间的空白和换行应完全按照其渲染。

LiteralLayout 元素使用通用属性。

示例：

```xml
<literallayout>
如果你想在任何你想的地方设置
带有间距和换行的章节，
你就使用 literallayout。
</literallayout>
```

## Note（注释）

Note 元素表示应从正文中区分出来的作为注释文本。

Note 元素使用通用属性。

示例：

```xml
<note>
<para>这是一个注释。</para>
</note>
```

## OrderedList（有序列表）

OrderedList 元素包含一个按顺序标记的项目列表。这与 ItemizedList 元素不同，后者包含一个带有符号或其他指定标记的列表。

OrderedList 元素除了通用属性外，还使用这些属性：

- Continuation。接受两个值之一：
  - Continues
  - Restarts
默认值是 Restarts。
- Inherit。接受 Ignore 或 Inherit。默认是 Inherit。
- Numeration。接受以下内容之一：
  - Arabic
  - LowerAlpha
  - LowerRoman
  - UpperAlpha
- Spacing。接受 Compact 或 Normal 作为值，没有默认值，且不是必需。

示例：

```xml
<orderedlist numeration="Upperroman">
  <item><para>第一章</para></item>
  <item><para>第二章</para></item>
</orderedlist>
```

## Sidebar（侧边栏）

Sidebar 元素表示 Sidebar 标记中包含的信息应作为侧边栏显示，如果处理系统允许的话。

Sidebar 元素使用通用属性。

示例：

```xml
<para>...</para>
<sidebar><title>我的侧边栏</title>
<para>这是一个侧边栏。</para>
</sidebar>
<para>...</para>
```

## SimpleList（简单列表）

SimpleList 元素包含一个包含简单列表的列表。

SimpleList 元素除了通用属性外，还使用这些属性。

- Columns。接受显示的列数。默认值为 1。
- Type。设置列类型：垂直、水平、行内。默认是 Vertical。

示例：

```xml
<para>我的手机键盘看起来像这样：
<simplelist type=horiz columns=3>
<member>1</member>
<member>2</member>
<member>3</member>
<member>4</member>
</simplelist>
</para>
```

## Tip（提示）

Tip 元素表示应从正文中区分出来的作为提示的信息。

Tip 元素使用通用属性。

示例：

```xml
<tip>
<para>如果我对你有实用的建议，我会把它放在这里。</para>
</tip>
```

## Warning（警告）

Warning 元素表示应从正文中区分出来作为给读者的警告文本。

Warning 元素使用通用属性。

示例：

```xml
<warning>在 <application>vi</application>中使用 <command>:q</command>
将不会保存你的文本文件的更改并退出！warning>
```

## 索引元素

DocBook 包含一套丰富的索引元素，适用于任何想要使用 DocBook 标记创建自己的索引的人，或者如果使用正确且处理系统支持，让处理系统自动生成索引。

## Index（索引）

Index 元素持有 DocBook 索引的标记。

Index 元素使用通用属性。

示例：

```xml
<index><title>索引</title>
<indexdiv><title>Cc</title>
<indexentry>
  <primaryye>类网络, 65</primaryye>
  <secondary>A, 65, 80</secondary>
  <secondary>B, 65, 66, 80</secondary>
</indexentry>
</indexdiv>
</index>
```

## IndexDiv（索引分区）

IndexDiv 元素表示索引中的划分。

IndexDiv 元素使用通用属性。

示例：

参见 Index 元素示例。

