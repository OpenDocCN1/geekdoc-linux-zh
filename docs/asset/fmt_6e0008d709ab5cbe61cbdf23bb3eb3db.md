
```xml
107. <prompt>
108.     据称他与斯波克相处得并不愉快。
109.   </prompt>
110. </nomatch>
111. <nomatch count="2">
112.   <audio src="startrek-tryagain.wav">
113.     fetchtimeout="1000">
114.     再试一次
115.   </audio>
116. </nomatch>
117. <nomatch count="3">
118.   <audio src="startrek-incorrect.wav">
119.     fetchtimeout="1000">
120.     错误。
121.   </audio>
122.   <prompt>
123.     答案是“麦伊”。
124.   </prompt>
125.   <assign name="question1" expr="'incorrect'/>
126. </nomatch>
127.   <filled>
128.     <audio src="startrek-correct.wav">
129.       fetchtimeout="1000">
130.       正确！
131.     </audio>
132.   </filled>
133.   <!-- 确认下一段引言 -->
134.   <block>
135.     <audio src="startrek-nextquotation.wav">
136.       fetchtimeout="1000">
137.     这是你的下一段引言。
138.     </audio>
139.   </block>
140.   <!-- 问题 2 -->
141.   <field name="question2">
142.     <audio src="startrek-spock-mindprobe.wav">
143.       fetchtimeout="1500">
144.     船长，我建议使用瓦肯脑波探测。
145.     </audio>
146.   <grammar>
147.     <![CDATA[
148.       [ (?mister spock) ]
149.     ]]
150.   </grammar>
```

**列表 8.4** 完成的测验生成器脚本。（续）

```xml
154.  <!-- 无匹配处理处理器 -->
155.  <nomatch count="1">
156.    <audio src="startrek-incorrect.wav">
157.      fetchtimeout="1000">
158.      错误。
159.    </audio>
160.    <audio src="startrek-hint.wav">
161.      fetchtimeout="1000">
162.      这里有一个提示。
163.    </audio>
164.    <prompt>
165.      他是一个极其逻辑严密的生物。
166.    </prompt>
167.  </nomatch>
168.  <nomatch count="2">
169.    <audio src="startrek-tryagain.wav">
170.      fetchtimeout="1000">
171.      再试一次
172.    </audio>
173.  </nomatch>
174.  <nomatch count="3">
175.    <audio src="startrek-incorrect.wav">
176.      fetchtimeout="1000">
177.      错误。
178.    </audio>
179.    <prompt>
180.     答案是“斯波克”。
181.    </prompt>
182.    <assign name="question2" expr="'incorrect'/>
183.  </nomatch>
184.   <filled>
185.     <audio src="startrek-correct.wav">
186.       fetchtimeout="1000">
187.       正确！
188.     </audio>
189.     <audio src="startrek-encouragement.wav">
190.       fetchtimeout="1000">
191.       做得好。
192.     </audio>
193.   </filled>
194.   <!-- 确认下一个引言 -->
195.   <block>
196.     <audio src="startrek-nextquotation.wav">
197.       fetchtimeout="1000">
198.     这是你的下一段引言。
199.     </audio>
200. 
```

**列表 8.4** 完成的测验生成器脚本。（续）

```xml
203. </block>
204. <!-- 问题 3 -->
205. <field name="question3">
206.   <audio src="startrek-beamup.wav">
207.     fetchtimeout="1000">
208.     柯克，传输。
209.   </audio>
210.   <grammar>
211.     <![CDATA[
212.       [ (captain kirk) ]
213.     ]]
214.   </grammar>
215. <!-- 无匹配处理器 -->
216. <nomatch count="1">
217.   <audio src="startrek-incorrect.wav">
218.     fetchtimeout="1000">
219.     错误。
220.   </audio>
221.   <audio src="startrek-hint.wav">
222.     fetchtimeout="1000">
223.     这里有一个提示。
224.   </audio>
225.   <prompt>
226.     大家伙。独一无二的。
227.   </prompt>
228. </nomatch>
229. <nomatch count="2">
230.   <audio src="startrek-tryagain.wav">
231.     fetchtimeout="1000">
232.     再试一次
233.   </audio>
234. </nomatch>
235. <nomatch count="3">
236.   <audio src="startrek-incorrect.wav">
237.     fetchtimeout="1000">
238.     错误。
239.   </audio>
240.   <prompt>
241.     答案是“柯克”。
242.   </prompt>
243.   <assign name="question3" expr="'incorrect'/>
244. </nomatch>
245.   <filled>
246.     <audio src="startrek-correct.wav">
247.       fetchtimeout="1000">
248.       正确！
249.     </audio>
```

**列表 8.4** 完成的测验生成器脚本。（续）

```xml
252.      </filled>
253.   </field>
254. 
255.   <block>
256.     <audio src="startrek-finalquotation">
257.       那是你的最后一段引言
258.     </audio>
259.     <goto next="#goodbye"/>
260.   </block>
261.   </form>
262. 
263.   <form id="goodbye">
264.     <block>
265.       <audio src="startrek-thankyou.wav">
266.         fetchtimeout="1000">
267.         感谢参加《星际迷航》引言游戏。
268.     </audio>
269.     </block>
270. 
271.     <field name="exit">
272.       <audio src="startrek-spock-lifelong.wav">
273.         fetchtimeout="1000">
274.         长寿且荣昌。
275.       </audio>
276.     <catch event="noinput nomatch">
277.       <exit/>
278.     </catch>
279.     </field>
280. </form>
281. 282. </xml
```

## 创建数据文件 (XML)

创建一个壮的 XML 应用需要将数据与数据的格式分离。在测验生成器（Quiz Generator）应用程序中，每个测验的数据存储在一个 XML 文件中。它使用一组预定义的标签进行标记，这些标签定义了数据的内容。查看列表 8.4 中的测验应用时，可以发现一个特定的结构。每个问题（在我们的案例中是引言）都包含以下元素：一个引言、一组答案和一个提示。答案项将用作我们寻找用户的正确响应，换句话说，就是语法（grammar）。

让我们遍历从现有数据源构建 XML 文件的过程。我们正尝试构建一个通用应用程序，通过将数据与其格式分离，来处理任何测验或调查数据源。XML 文件将持有数据，而 XML 文件将持有格式。

> 为了简单起见，本项目中的数据存储在文本文件中。它也可以从数据库或多个数据源的组合中动态生成。

## 分析数据

“星际迷航”引言游戏（Star Trek Quotation Game）的数据嵌入在项目第一部分创建的 VoiceXML 文件中。列表 8.5 是文件中各种元素和属性的大纲，以及它们如何在层级结构中相互关联。查看层级结构的价值在于，它可以帮助定义 XML 文档的结构，而无需担心数据。

`<xml>` 元素包含子级元素：`<link>`、`<help>` 和 `<form>`。文件中的所有内容都是这三个元素之一的子级或后代。`<link>` 和 `<help>` 是相对简单的元素。`<link>`有一个属性和一个语法，用于定义哪些语音会激活链接。`<help>` 元素基本上是音频输出，当源文件无法及时获取时则显示文本。

文档结构的大部分位于 `<form>` 元素中。`<form>` 有三个子元素，这些元素包含了多个层级的其他元素。我们将在下一节开发 XSLT 样式表时，详细拆解每个主元素。

```
1. <xml>
2.
3. <link>
4.    src (attribute)
5.    <grammar>
6.
7. <help>
8.    <audio>
9.    src (attribute)
10.  fetchtimeout (attribute)
11. text (content)
12. <reprompt>
13.
14. <form>
15.
16. id (attribute)
17.
18. 块 
19. <audio>
20. src (attribute)
21. fetchtimeout (attribute)
22. text (optional content)
23. <goto> (optional)
24. next (attribute)
25.
26. <noinput>
27. count (attribute)
28. <audio>
29. src (attribute)
30. text (content)
31. <goto> (optional)
32. next (attribute)
33.
34. <field>
35. name (attribute)
36.
37. <audio>
38. src (attribute)
39. text (content)
40.
41. <grammar>
42.
43. <nomatch>
44. count (attribute)
45. <audio>
46. fetchtimeout (attribute)
47. src (attribute)
48. text (content)
49. <prompt> (optional)
50. text (content)
51. <assign> (optional)
52. name (attribute)
53. expr (attribute)
54. <goto> (optional)
55. next (attribute)
56. <catch> (optional)
57.
58. event (attribute)
59. <exit>
60. <filled>
61. <audio>
62. src (attribute)
63. fetchtimeout (attribute)
64. text (content)
```

**列表 8.5** 测验游戏数据的层级结构。（续）

## 创建 XML 骨架

创建 XML 文件的第一步是创建一个用于存储数据的基本骨架。列表 8.6 显示了一个包含 XML 声明作为第一行的骨架。根元素通过一个 `quizFileName` 属性进行声明。`quizFileName` 将被 XSLT 样式表用于创建起始链接。第 5 行关闭 XML 文档。XML 文件中的所有内容都将包含在测验根元素中。

```
1. <?xml version="1.0">
2.
3. <quiz quizFileName="quiz-startrek.vxml">
4.
5. </quiz>
```

**列表 8.6** XML 骨架。

> 在你的本地硬盘上创建一个新的 Projects 文件夹。构建列表 8.6 所示的 XML 骨架，并将其保存为 `quiz-startrek.xml` 放在 Projects 目录中。

## 定义链接

分析列表 8.4 中的 VoiceXML 文件可知`<link>` 元素是 `<xml>` 根元素的第一个子元素。XML 数据文件可以像列表 8.7 从第 5 行开始定义 `<link>` 元素的结构。`<link>` 必须包含一个 `<next>` 元素，用于持有激活后链接跳转位置的 URI。`<grammar>` 元素持有激活链接的简单语法。

```
1. <?xml version="1.0"?>
2.
3. <quiz quizFileName="quiz-startrek.vxml">
4.
5. <link>
6. <next>quiz-startrek.vxml</next>
7. <grammar>start over</grammar>
8. </link>
9. 10. </quiz>
```

**列表 8.7** 定义 `<link>`。

## 定义帮助信息

VoiceXML 文件包含一个帮助信息，必须在列表 8.8 中定义。查看列表 8.5，我们可以看到`<help>` 元素包含了 `<audio>` 元素。`<help>` 元素位于 `<form>` 元素中。`<help>` 元素基本上是音频输出，当源文件无法及时获取时则显示文本。
