
```
8. <var name="confirmedReporterId"/>
9. <var name="nameOfRecording"/>
10. <form id="validation">
11. <var name="phoneNumber"/> expr="session"/>
12. <var name="phoneType"/> expr="session"/>
13. <var name="accessAttempts" expr="1"/>
14. <field name="reporterName">
15. <grammar>
16. <![CDATA[
17. <hawaii> <reporterId>1234
18. <california> <reporterId>4321
19. ]]>
20. </grammar>
21. <audio src="speak-name.wav">
22. Speak your name.
23. </audio>
24. </field>
25. <!-- CATCH -->
26. <catch event="nominput" count="1">
27. I missed that.
28. </catch>
29. <catch event="nominput" count="2">
30. There seems to be a problem with login. Please contact the administrator.
31. <disconnect>
32. <submit next="security.cgi" namelist="phoneType"/>
33. </catch>
34. </field>
35. <!-- AUTHENTICATION -->
36. <filled>
37. <if cond="reporterName == reporterId">
38. <assign name="confirmedReporterId" expr="reporterId"/>
39. <audio src="welcome-back.wav">
40. Welcome back, <value expr="reporterName$.utterance"/>
41. </audio>
42. <goto next="#recordReport"/>
43. </if>
44. <!-- INVALID COMBINATION -->
45. <elseif cond="accessAttempts > 1">
46. Please contact the admin to confirm you have access to this system.
47. <disconnect>
48. <submit next="security.cgi" namelist="phoneType"/>
49. </disconnect>
50. </elseif>
```

列表 7.12 完成的录音脚本（*继续*）

## 报告记录器 231

```
106. reporterName
107. reporterId/>
108. <else/>
109. <audio src="invalid-login.wav">
110. That Reporter Name and ID was not valid. Try it again.
111. </audio>
112. <assign name="accessAttempts" expr="accessAttempts+1"/>
113. <clear namelist="reporterNameId">
114. </if>
115. </filled>
116. </field>
117. </form>
118.
119. <form id="recordReport">
120. <field name="beachName">
121. <audio src="which-beach.wav">
122. Which beach are you making a report for
123. </audio>
124. <grammar expr="beachnames.grammar#" + 
125. confirmedReporterId/>
126. <nomatch count="1">
127. Please repeat the beach name.
128. </nomatch>
129. <nomatch count="2">
130. Please contact surfline to confirm your reporter status
131. <|exit|>
132. </nomatch>
133. </field>
134. <!-- MAKE THE RECORDING -->
135. <record name="theReport">
136. beep="false"
137. maxtime="30s"
138. finalsilence="1.5s"
139. type="thirty-seconds.wav">
140. <audio src="thirty-seconds.wav">
141. You will have 30 seconds to record your report
142. for <value expr="beachName$.utterance"/>
143. Start speaking the tone.
144. </audio>
145. </record>
```

```
155.
156. <!-- PLAYBACK --
157. <field name="confirm" type="boolean">
158.   <audio src="playback.wav">
159.     让我回放你录制的内容：
160.   </audio>
161.   <prompt>
162.     <value expr="theReport"/>
163.   </prompt>
164. 
165. <!-- CONFIRMATION FROM USER --
166.   <audio src="keep.it.wav">
167.     你想保留它吗？
168.   </audio>
169.   <filled>
170.   <if cond="confirm">
171.     <assign name="nameRecording" expr="beachName + .wav"/>
172.     <audio src="saved.wav">
173.       请稍候，正在保存您的报告。
174.       录音名称将为 <value nameOfRecording/>
175.     </audio>
176.   <else>
177.     <audio src="re-record.wav">
178.       让我们重新开始。
179.     </audio>
180.   </clear>
181. </if>
182. </filled>
183. </filled>
184. 
185. <subdialog name="saveMessage"
186.   src="http://your-server/cgi-bin/recording.cgi"
187.   method="post"
188.   enctype="multipart/form-data"
189.   namelist="theReport nameRecording"
190.   <filled>
191.     <audio>您的报告已保存。</audio>
192.   </filled>
193. </subdialog>
194. 
195. <!-- ANOTHER REPORT? --
196. <field name="anotherReport" type="boolean">
197.   <audio src="another-report.wav">
198.     你还想为另一段演讲提交报告吗？
199.   </audio>
200.   <filled>
201.     <if cond="anotherReport" (continues)
```

**Listing 7.12** 完成的报告记录器脚本。（续）

```
202. <clear/>
203. <goto next="#recordReport"/>
204. </if>
205. </filled>
206. </field>
207.
208. <-- EXIT/DISCONNECT -->
209. <field name="goodbye">
210. <audio src="thank-you.wav">
211. 感谢您的帮助。
212. 下次见。
213. </audio>
214. <catch event="nomatch">
215. <|exit|>
216. </catch>
217. </field>
218. </form>
219. <|xml|>
```

**Listing 7.12** 完成的报告记录器脚本。（续）

## 结语

报告记录器正朝着成为一个多功能录音服务迈进。不再仅仅是报告员，调用者可以请求特定的部门或留言。Listing 7.12 可以作为创建动态报告列表的模板。用户调用该服务，请求名称并收听报告。查看之前项目中的枚举列表，以了解如何使用项目列表创建菜单。不要输出到 Web 页面，而是输出到 VoiceXML 并即时创建。该项目的列表可以从 Beocal 网站 cafe.beocal.com/wiley/10projects 下载。它们被保存为文本文件，作为创建您自己的 VoiceXML 脚本的模板。加入我们的在线论坛并告诉我们您将如何使用。如果你创建一个能让它更好的表单，它可能会被整合到他人可以使用的代码中。下一个项目将使用 XML 和 XSLT 来生成问卷和测验。请记住报告记录器作为每个问卷录制指令的可能工具。

# 项目 8 测验生成器

电话测验和冒险提示是在线游戏的自然扩展。当我发现互联网上有一个包含超过 18,000 个《星际迷战》系列音频文件的网站时，测验生成器诞生了。我想在游戏中插入一些声音并让人们猜是哪个角色在说话会很有趣。特别感谢《星际迷战》的 Dave 为此项目提供音频文件。

| 问题 | 解决方案 |
|---|---|
| 大多数公司有多组存储在结构化格式中的数据，需要输出到不同的格式。数据被硬编码到预设模板中，导致输入错误并浪费时间。一旦数据输入模板中，它就再无法供其他应用程序使用。 | 将数据与格式分离。将数据存储在非专有格式中（如 XML）。使用 XSLT 作为通用机制，即时输出 VoiceXML，同时保持数据源不变。 |

## 项目描述

此项目创建了一个名为“星际迷战引言”的游戏。用户拨打电话，听听来自原始《星际迷战》剧集的引言，并猜是谁在说话。此项目中的技术展示了如何将录音集成到 VoiceXML 输出中、创建错误消息、通过复制将多个语法集成到单一格式中，以及从 XML 数据源动态生成内容。数据与格式完全分离，因此任何数量的测验、问卷或游戏都可以从同一个 XML/XSL 处理脚本运行。虽然运行项目的先进部分需要 Java 环境，但不需要 Java 经验。XML/XSLT 编程也是如此。

创建此项目将涉及：

1. 创建一个简单的测验。
2. 为测验添加问题。
3. 插入录制的提示。
4. 录制提示内容。
5. 完成 VoiceXML 模板。
6. 设置 XML/XSLT 环境。
7. 创建数据文件 (XML)。
8. 构建样式表 (XSL)。
9. 测试基础应用。
10. 将 XSL 模板插入样式表。
11. 测试完成的 XSLT 样式表。

## 你将需要

- 一个 Beocal (cafe.beocal.com) 开发者账户
- VoiceXML 1.0 规范 (www.w3.org/voice)
- TextPad 或任何简单的文本编辑器 (www.textpad.com)
- Java 开发工具包 (Java Development Kit)
- Xerces XML 解析器 (xml.apache.org)
- Alan XSL 处理器 (xml.apache.org)
- GoldWave 音频录音机 (www.goldwave.com)
- 《星际迷战》录音文件 (www.stinv.com)
- 本项目的源码 (cafe.beocal.com/wiley/10projects)

# 测验生成器 237

项目中使用的 VoiceXML 元素

| 元素名称 | 描述 |
|---|---|
| `<assign>` | 为变量分配值 |
| `<audio>` | 在提示中播放音频片段 |
| `<block>` | 可执行代码的容器 |
| `<catch>` | 捕获事件 |
| `<exit>` | 退出会话 |
| `<field>` | 在表单中声明输入字段 |
| `<filled>` | 字段填充后执行的操作 |
| `<form>` | 用于展示信息和收集数据的对话 |
| `<goto>` | 跳转到同一文档或不同文档中的对话 |
| `<grammar>` | 指定语音识别或 DTMF 语法 |
| `<help>` | 捕获帮助事件 |
| `<link>` | 为链接范围内的所有对话指定通用转换 |
| `<noinput>` | 捕获无输入事件 |
| `<nomatch>` | 捕获不匹配事件 |
| `<reprompt>` | 当字段在事件后被再次访问时播放字段提示 |
| `<xml>` | 每个 VoiceXML 文档的顶级元素 |

来源：VoiceXML 2.0 草稿，第 1.4

### 应用调用流程

图 8.1 显示了此应用的调用流程。欢迎消息问候调用者，然后输出一组使用测验的说明。将提出一系列问题，每个问题在给出正确答案并移动到下一个问题之前都有两次回答的机会。测验结束时，应用程序以告别消息结束。

# 项目 8

图 8.1 应用流程。

# 创建简单的测验

测验生成器项目分为三个阶段。首先，我们将创建一个简单的测验，作为添加问题的模板。一旦生成了问题，将录制语音提示以替换 TTS 提示。最后一个阶段是创建一个 XML/XSLT 应用，该应用能够动态访问数据以创建任何数量的测验。

## 测验生成器 239

```xml
1. <?xml version="1.0"?>
2. <!DOCTYPE vxml
3. PUBLIC
4. "-//BeVocal Inc/VoiceXML 2.0//EN"
5. "http://cafe.bevocal.com/libraries/dtd/vxml2-0-bevocal.dtd">
6. 
7. <xml version="2.0">
8. 
9. <!-- 问候 -->
10. <form id="greeting">
11. <block>
12. <prompt>
13. 欢迎来到星际迷航引用游戏。
14. </prompt>
15. <goto next="#questions"/>
16. </block>
17. </form>
18. 
19. <!-- 问题 -->
20. <form id="questions">
21. 
22. <ininput count="1">
23. 我没有听听到任何声音。请重试。
24. </ininput>
25. <ininput count="2">
26. 你必须说 Spock（史波克）、Kirk（柯克）或 McCoy（麦科伊）才能参与。
27. </ininput>
28. 
29. <ininput count="3">
30. 这是你的最后机会了，伙计。
31. 你最好说点什么。
32. </ininput>
33. <ininput count="4">
34. 噢，好吧，那是你的损失。
35. <goto next="#goodbye"/>
36. </ininput>
37. 
38. <block>
39. 你将听到一段来自星际迷航
40. 角色的引用。你必须回答 Spock、Kirk、
41. 或 McCoy。这里是第一个引用。
42. </block>
43. 
44. <field>
45. <prompt>
46. 我是一个医生，不是一个瓦工。
47. </prompt>
48. <grammar>
```

**列表 8.1** 一个简单的测验。（续）

```xml
48. | <![CDATA[ |
49. | mccoy bones doc doctor |
50. | ] |
51. | </grammar count="1"> |
52. | 错误。这里有一个提示。 |
53. | 据说他和 Spock 相处得不好。 |
54. | </not> |
55. | <not count="2">重试</not> |
56. | <not count="3"> |
57. | 错误。答案是 'McCoy'。 |
58. | <goto next="#goodbye" /> |
59. | </not> |
60. | <filled> |
61. | 正确！ |
62. | <goto next="#goodbye" /> |
63. | </filled> |
64. | </form> |
65. | <form id="goodbye" |
66. | <block> |
67. | <prompt> |
68. | 感谢参与星际迷航引用游戏。 |
69. | 生生不昌（Live Long and Prosper）。 |
70. | </prompt> |
71. | <disconnect /> |
72. | </block> |
73. | </form> |
74. | </xml> |
```

## 列表 8.1 一个简单的测验。（续）

从第 20 行开始的问题组可以包含任意数量的字段（field），每个 `<field>` 包含一个单独的问题及其答案。`<prompt>` 元素输出问题，而 `<grammar>` 包含正确答案。语法部分应包含用户可能说的、且被认为该问题是正确的的所有可能答案。
