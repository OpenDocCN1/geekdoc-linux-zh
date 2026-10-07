
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

7. `<xsl:output method="xml" indent="yes" />`

8. `<xsl:strip-space elements="*" />`

9.

10. `<xsl:template match="*">`

11. `<vml version="2.0">`

**Listing 8.20** 创建链接模板。（续上）

```xml
12. <xsl:apply-templates />
13. </vml>
14. </xsl:template>
15.
16. <xsl:template match="quiz">
17. <xsl:apply-templates/>
18. </xsl:template>
19.
20. <xsl:template match="link">
21. <link next="next">
22. <xsl:apply-templates select="grammar"/>
23. </link>
24. </xsl:template>
25.
26. <xsl:template match="grammar">
27. <grammar><xsl:value-of select="."/></grammar>
28. </xsl:template>
29.
30. </xsl:stylesheet>
```

Listing 8.20 创建链接模板。（继续）

XSLT 语法不允许将模板匹配插入到属性的值。为了在值中插入输入，可以使用大括号 `{}` 创建属性值模板（attribute value templates），并包含要作为值插入的元素或属性的名称。第 21 行使用属性值模板插入了 XML 文件中 `<next>` 元素的值。

Listing 8.20 的第 22 行使用 `<xsl:apply-templates>` 指令的 `select` 属性，将 `<next>` XML 文件的值作为属性值模板放置。语法处理器会将处理过程转移到该模板。语法模板输出字面量的 `<grammar>` 元素，并使用点语法（dot syntax）插入语法 XML 文件的文本。作为 `select` 属性值的点 `.` 指定处理器应输出当前节点内的文本。在这种情况下，它输出起始短语作为 `<link>` 的语法。

## 输出

Listing 8.21 显示了对更新后的 XSLT 样式表运行 `quiz-starttrek.xml` 数据文件后的输出。第 3 行到第 5 行包含作为字面量输出的 `<link>` 元素，带有一个 `next` 属性，其值为当前文件名。

第 4 行包含将激活链接并强制重新加载 VoiceXML 文档的语法。输出其余部分是 XML 文档的文本，随着我们向样式表中添加更多模板，这些文本将会被格式化。

```xml
1. <?xml version="1.0" encoding="UTF-8"?>
2. <xml version="2.0">
3. <link next="quiz-startrek.vxml">
4. <grammar>(start over)</grammar>
5. </link>
6. startrek-help.wav2000
7. 听听星际迷角色的引言。
8. 说出角色的名字。
9. 你的三个选择是 Spock、Kirk 或 McCoy。
10. startrek-theme.wavstartrek-welcome.wav2000
11. 欢迎来到星际迷航引言游戏。
12. startrek-noinpoint1.wav1000
13. 我什么都没听到。请重试。
14. startrek-noinpoint2.wav1000
15. 你必须说 Spock、Kirk 或 McCoy 才能参与。
16. startrek-noinpoint3.wav1000
17. 这是你最后的机会了，伙计。
18. 你最好说点什么。
19. startrek-noinpoint3.wav1000
20. 噢，那是你的损失。
21. startrek-instructions.wav1000
22. 你将听到一段星际迷航角色的引言。
23. 你必须回答 Spock、Kirk
24. 或 McCoy。
25. startrek-confirm.wav1000
26. 这是第一个。
27. 这里是医生。
28. 逻辑如此。
29. 船长。
30. 坚持引擎。
31. 伙计。
32. 朋友。
33. 这样。
34. startrek-thankyou.wav1000
35. 感谢参与星际迷航引言。
36. startrek-long.wav1000
37. 万岁。
38. </link>
```

**Listing 8.21** 运行 XSLT 样式表后的输出。

## 链接模板

在 XML 文件 `<quiz>` 块中遇到的第一个元素是 `<link>` 元素。从第 20 行开始，Listing 8.20 显示了一个向 VoiceXML 文件输出 `<link>` 元素的模板。`<link>` 元素将作为字面量文本输出。

（注：此处翻译根据要求，由于原文文本中存在部分乱码或重复，译文已根据逻辑进行了处理，并保留了 Markdown 结构。）

## 278 项目 8

30. `<audio fetchtimeout="1000" src="startrek-instructions.wav">`
31. 你将听到一段来自《星际迷航》角色的引用。你必须回答 Spock（史波）、Kirk（柯克）或 McCoy（麦考）。
32. `</audio>`
33. `<audio fetchtimeout="1000" src="startrek-confirmbeginning.wav">`
34. 这是第一句引用。
35. `</audio>`
36. 我是个医生，不是瓦工。
mccoydcbonesdoctormccoy
据说，他和 Spock 处得不好。

37. 船长，我建议使用瓦肯脑波探测。
spockthe vulcan
詹姆斯·T·柯克的最好的朋友。他极度逻辑化。

38. 斯科特，把我送上去。
kirkpatrickain kirkjames kirkjames t kirkjim
那个大汉。独一无二。
39. `<audio fetchtimeout="1000" src="startrek-thankyou.wav">`
40. 感谢参与《星际迷航》引用游戏。
41. `</audio>`
42. `<audio fetchtimeout="1000" src="startrek-spock-livelong.wav">`
43. 长寿且繁荣。
44. `</audio>`
</xml>

**Listing 8.23** 模板处理。（继续）

## 问候模板

遍历 Listing 8.15 的 XML 文件，下一个要处理的元素是第 26 行的 `greeting`。这就是导致 Listing 8.22 中输出问题的那个元素。数据中有两个 `audio` 字段，其中一个包含的是 `fetchhint` 而不是 `fetchtimeout`。我们将更新音频模板以处理这些变化。

Listing 8.24 包含一个从第 18 行开始的 `greeting` 模板。XSLT 样式表中的模板不需要处于特定顺序。该模板将输出格式化为字面上的 `<form>` 元素，其中包含一个 `<block>` 元素。对 `<xsl:apply-templates>` 的调用激活了音频模板。

```xml
1. <xsl:template match="audio">
2. <xsl:choose>
3. <xsl:when test="fetchhint">
4. <audio src="soundSource">
5.     fetchhint="(fetchhint)"
6.     <xsl:value-of select="textPrompt"/>
7. </audio>
8. </xsl:when>
9. <xsl:otherwise>
10. <audio src="soundSource">
11.     fetchtimeout="(timeout)"
12.     <xsl:value-of select="textPrompt"/>
13. </audio>
14. </xsl:otherwise>
15. </xsl:choose>
16. </xsl:template>
17.
18. <xsl:template match="greeting">
19. <form id="greeting">
20. <div>
21.     <xsl:apply-templates/>
22.     <goto next="#questions"/>
23. </div>
24. </form>
25. </xsl:template>
```

**Listing 8.24** 问候模板和更新后的音频模板。

用于 `<audio>` 元素的更新模板使用 `<xsl:choose>` 语句来处理条件处理。通过 `<xsl:choose>`，使用 `<xsl:when>` 的 `test` 属性测试多个条件。第 3 行测试是否从 XML 文件的当前上下文中访问 `<fetchhint>` 元素。如果当前处理的节点中可用 `<fetchtimeout>`，则输出一个带有 `src` 和 `fetchhint` 属性的 `<audio>` 元素，其值通过属性值模板插入。第 9 行的 `<xsl:otherwise>` 元素处理任何其他 `<audio>` 元素，将 `fetchhint` 属性替换为 `fetchtimeout` 属性。

当音频模板完成后，处理返回到 Listing 8.24 的第 21 行。`greeting` 元素中没有更多需要处理的模板，跳转到样式表的下一行，输出 `<goto>` 元素。

## 280 项目 8

将问候模板插入样式表并更新音频模板。重新构建应用并验证每个 `<audio>` 元素的正确输出。

## ErrorNoInput 模板

`<errorNoInput>` 元素位于 XML 文件的后续。它仅用作消息列表的容器。将消息封装在容器标签中，XML 提供的内容不受限于特定数量的消息。

Listing 8.25 显示了 `<errorNoInput>` 元素的模板。第 2 行的 `<xsl:comment>` 元素构建了一个注释。注释从 `<xsl:comment>` 元素的内容创建，输出了 `ERROR MESSAGES`。第 3 行的 `<apply-templates>` 调用访问了 `<errorNoInput>` 元素的所有子节点。后续部分创建一个模板来格式化该输出。

```xml
1. <xsl:template match="errorNoInput">
2. <xsl:comment>ERROR MESSAGES</xsl:comment>
3. <xsl:apply-templates />
4. </xsl:template>
```

**Listing 8.25** errorNoInput 模板。创建一个模板来处理 `<errorNoInput>` 元素并将其插入你的 quizFormatter。

## NoInput 模板

在 `<errorNoInput>` 元素中，第 3 行的 `<xsl:apply-templates>` 调用访问了 `<errorNoInput>` 元素的所有子节点。后续部分创建一个模板来格式化该输出。

（注：原文 OCR 文本末尾存在重复/乱码，已根据提供的内容提供清晰的逻辑流）。

```xml
1. <xsl:template match="noInput">
2. <form id="greeting">
3. <div>
4.     <xsl:apply-templates/>
5.     <goto next="#questions"/>
6. </div>
7. </form>
8. </xsl:template>
```

```
1. <xsl:template match="question">
2.   <audio src="${recording}" fetchhint="prefetch">
3.   <xsl:apply-templates />
4.   </audio>
5. </xsl:template>
```

**Listing 8.30** 问题模板。

第 3 行的 `<xsl:apply-templates/>` 输出 XML 文件 `<question>` 元素存储的字面文本，如果没有可用的模板进行处理，这就是默认输出内容。

## 答案模板 (Answers Template)

`<answer>` 元素包含一组子 `<answer>` 标签，这些标签将用于构建问题正确答案的语法结构。Listing 8.31 使用方括号包裹由 XSLT `<xsl:apply-templates/>` 指令插入的答案。

```
1. <xsl:template match="answer">
2.   <grammar>
3.     [xsl:apply-templates />]
4.   </grammar>
5. </xsl:template>
```

**Listing 8.31** 答案模板。

## 答案模板 (Answer Template)

XML 文件中 `<answer>` 元素存储的每个值都需要在括号内输出，强制让成对的值视为单个话语（utterance）。Listing 8.32 用字面元素包裹了 `<xsl:apply-templates>`。XSLT 的 `<xsl:text>` 元素强制在括号之间产生一个空格。

```
1. <xsl:template match="answer">
2.   (<xsl:apply-templates />)</xsl:text> </xsl:text>
3. </xsl:template>
```

**Listing 8.32** 答案模板。

查看 Listing 8.15 的 XML 数据可以发现`<incorrect>` 标签包含一个使用正确答案的提示。该提示在通过 `<xsl:apply-templates />` 元素的第一次匹配输出。第二个 `<match>` 包含“再次尝试”（Try again），第三个 `<match>` 则确认答案错误并给用户正确答案。正确答案是通过从该字段的答案列表中提取第一个答案生成的，如第 12 行所示。

## 测验生成器 (Quiz Generator) 285

Listing 8.33 的第 14 和 15 行使用 `generate-id()` 函数将 *incorrect* 的值赋值给 *name* 属性，就像 Listing 8.29 中一样。在第 14 行，访问当前节点的父节点，生成与其所在的 `<field>` 相同的 id。

第 14 行的 `<call:template>` 指令调用样式表中的命名模板。命名模板用于创建不与 XML 文件中任何元素名称关联的模板。当我们需要一个在 VoiceXML 对话框中创建 `<field>` 元素的 `<template>` 时。

从第 20 行开始的正确模板全是字面文本。它是对输入了正确答案的用户的简单确认。当模板完成后，处理将返回到第 18 行，那里 `<if>` 条件会检查这是否是系列中的最后一个问题。如果是，`<block>` 元素将把控制权移交给 `<goodbye>`。

## 退出模板 (Goodbye Template)

退出模板为 VoiceXML 脚本创建退出 `<form>`。Listing 8.33 的第 2 行以 `<form>` 开始，该表包含一个用于接收来自 `<xsl:apply-templates>` 指令音频内容的字段。第 5 到 7 行通过隐藏提示（prompt）让熟悉操作的用户访问重新开始的链接。如果链接未被激活，应用程序将终止。

```
1. <xsl:template match="goodbye">
2. <form id="goodbye">
3. <field>
4. <xsl:apply-templates/>
5. <catch event="noinput notch">
6. <exit/>
7. </catch>
8. </field>
9. </form>
10. </xsl:template>
```

Listing 8.34 退出模板。

## 测试完成的 XSLT 样式表

上述内容了处理 XML 数据文件所需的所有模板。8.35 显示了完整的样式表。每当你想要创建一个新的测验或调查时，构建一个 XML 数据文件并使用 `quizFormatter.xsl` 样式表对其进行处理。

要创建一个构建其他 XML 数据文件的模板，请从 Listing 8.15 开始，删除所有模板和对声音文件的引用。这个基础的、空的骨架可以多次使用以构建各种测验、调查和游戏。要测试它，向 XML 骨架中放入一些数据，并针对样式表运行。确保更改了 `quizFormatter.bat` 中的输出文件名。

```xml
<?xml version="1.0"?>
<xsl:stylesheet
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform
    version="1.0">
  <xsl:output method="xml" indent="yes" />
  <xsl:strip-space elements="*" />
  <xsl:template match="">
    <xml version="2.0">
      <xsl:apply-templates />
    </xml>
  </xsl:template>
  <xsl:template match="quiz">
    <xsl:apply-templates/>
  </xsl:template>
  <xsl:template match="link">
```
