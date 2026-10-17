
测验中的所有问题都有两级错误检查。从第 20 行开始的 `<form>` 以 `<input>` 错误检查开始，该检查的作用范围在表单级（form level），允许问题表单内的所有字段访问该检查。`<input>` 的 `count` 属性在每次被访问时都会递增。系统会输出有用的提示，试图告知调用者需要某种类型的输入。

从第 22 行开始的第一个 `<input>` 包含一条基础礼貌消息，第二个是指令的简要总结，以防用户不确定该做什么。第三条消息是警告，如果在第四次尝试后仍无响应，将退出程序。在第四次尝试从用户获取输入时，第 34 行的 `<goto>` 元素将处理转移到 `goodbye` 表单以结束通话。

第二级错误检查位于包含问题的每个 `<field>` 内部。一组 `<nomatch>` 元素会将用户输入与定义的语法进行比较。语法是由问题的正确答案构建的。第一个 `<nomatch>` 会输出一个指向正确答案的提示，以及一个简单的“重试”鼓励。在每个问题的第三次 `<nomatch>` 尝试中，将给出正确答案并将处理过程传递给 `goodbye` 表单。

当用户正确回答问题时，从第 61 行开始的 `<filled>` 块将确认答案并将处理过程转转移到 `goodbye` 表单。随着项目的开发，将添加更多问题，每当没有答案时，处理过程将落到一个新问题。

## 向测验中添加问题

现在测验中的第一个问题可以用作模板。问题表单可以包含任意数量的作为 `<field>` 单元的问题。在我们的应用程序中，将会有三个。

## 处理第一个字段

在列表 8.2 中，单个表单内字段的处理按照 `<form>` 中的第一个 `<field>` 线性进行。当 `<field>` 被 `<filled>` 一个可识别的言语时，处理将自动进入下一个 `<field>`。

```xml
<form id="questions">
1. <input count="1">
2. 我没有听听到任何声音。请重试。
3. </input>
4. <input count="2">
5. 你必须说 Spock、Kirk 或 McCoy 才能参与。
6. </input>
7. <input count="3">
8. 这是你的最后机会了，伙计。
9. 你最好说点什么。
10. </input>
11. <input count="4">
12. 噢，好吧，那是你的损失。
13. <goto next="#goodbye"/>
14. </input>
15. <block>
16. 你将听到一段来自星际迷航
17. 角色的引用。你必须回答 Spock、Kirk、
18 或 McCoy。这里是第一个引用。
19. </block>
20. <field name="question1">
21. <prompt>
22. 我是一个医生，不是一个瓦工。
23. </prompt>
24. <grammar>
25. <![CDATA[
26. mccoy bones doc doctor
27. ]]>28. </grammar>
29. <nomatch count="1">
30. 错误。这里有一个提示。
31. 据说他和 Spock 相处得不好。
32. </nomatch>
33. <nomatch count="2">重试</nomatch>
34. <nomatch count="3">
35. 错误。答案是 'McCoy'。
36. <goto next="#goodbye" />
37. </nomatch>
38. <filled>
39. 正确！
40. <goto next="#goodbye" />
41. </filled>
42. </field>
43. <field name="question2">
44. <prompt>
45. 谁是那个著名的医生麦科伊？
46. </prompt>
47. <grammar>
48. <![CDATA[
49. mccoy bones doc doctor
50. ]]>51. </grammar>
52. <nomatch count="1">
53. 错误。这里有一个提示。
54. 他的绰号是“骨”。
55. </nomatch>
56. <nomatch count="2">重试</nomatch>
57. <nomatch count="3">
58. 错误。答案是 'McCoy'。
59. <goto next="#goodbye" />
60. </nomatch>
61. <filled>
62. 正确！
63. <goto next="#goodbye" />
64. </filled>
65. </field>
66. <field name="question3">
67. <prompt>
68. 星际迷航中哪位是指挥官？
69. </prompt>
70. <grammar>
71. <![CDATA[
72. kirk captain kirk captain
73. ]]>74. </grammar>
75. <nomatch count="1">
76. 错误。这里有一个提示。
77. 他的姓氏是柯克。
78. </nomatch>
79. <nomatch count="2">重试</nomatch>
80. <nomatch count="3">
81. 错误。答案是 'Kirk'。
82. <goto next="#goodbye" />
83. </nomatch>
84. <filled>
85. 正确！
86. <goto next="#goodbye" />
87. </filled>
88. </field>
89. </form>
90. <form id="goodbye">
91. <block>
92. <prompt>
93. 感谢参与星际迷航引用游戏。
94. 生生不昌。
95. </prompt>
96. <disconnect />
97. </block>
98. </form>
99. </xml>
```

## 列表 8.2 一个表单中的多个问题。（续）

第一个关于 McCoy 的问题包含了有助于控制流程的更改。`<goto>` 元素已从 match 和 filled 事件中移除。在 8.2 中，使用 `<assign>` 元素为字段赋值值，以便测验继续。

这引出了关于用户响应的有趣话题。测验的原始指令给出了三个可能的答案：“Kirk”、“Spock”或“McCoy”。每个问题的语法并没有假设用户会局限于所提供的特定选择。在可能的情况下，扩展语法以包含用户可能说的每种被视为正确响应的可能选择。这将使您的应用程序更加用户友好，并使其理解语音输入时给人一种相当智能的印象。

## 插入提示词

使用 TTS（语音合成）生成的提示词是测试应用程序的一种良好方法，但录制的提示词会让语音界面更加用户友好。`<audio>` 标签用于指向可以作为提示词的音频文件。`src` 属性是音频文件的名称。对于 `<audio>` 标签的内容，应该是当音频文件不可用时将使用的文本。

VoiceXML 规范推荐了两种类型的音频文件：原始（无头）和 WAV（RIFF 头）。接受的文件类型取决于平台。最广泛接受的格式是 `*.wav`。请检查您的平台文档查看可以处理何种类型的音频文件。

## 下载《星际迷航》音频文件

此项目的《星际迷航》资源文件可以在 stinsv.com（Star Trek in Sound and Vision）找到；图 8.2 显示了其首页。网站所有 Dave Wythe 要求您下载项目所需的文件，而不是在他的网站上引用它们。由于有超过 18,000 个文件，您可以理解他为什么这么要求。在使用其中任何文件之前，请阅读“使用条款”。

- 访问 www.stinsv.com 并下载您喜欢的音频文件作为您项目中的引用。您可以重命名文件以便更容易记忆，但必须保持相同的文件扩展名 `.wav`。在将文件上传到 BeV 环境时，所有名称都会被强制转换为小写字母，您也可以从开始就用小写命名。

## 项目 8

### 插入 `<audio>` 元素

`<audio>` 元素用于用录制的输入替换 `<prompt>` 标签。`<audio>` 元素比 `<prompt>` 更具通用性，允许 `src` 属性指向由提示词生成的音频，同时在源文件不可用时允许 TTS 解释器朗读元素的内容。

`<audio>` 元素可以在 `src` 属性中携带一个可选的 `exp` 属性。`exp` 值由 JavaScript 表达式生成，该表达式评估为将播放的 URI 或 URI 数组。还可以使用 `fetchtimeout` 属性来强制获取音频资源超时。默认情况下，超时为 60 秒，对于我们的应用程序来说是足够的。列表 8.3 第 3、11 和 19 行的 `fetchtimeout` 属性被设置为 1500 毫秒，如果无法快速检索音频文件，将强制 TTS 进行朗读。如果在规定时间内无法访问音频提示，TTS 引擎将输出 `<audio>` 元素的内容。

- 将您应用程序中的引用提示改为指向从 Star Trek in Sound and Vision 网站下载的文件 `<audio>` 元素。测试您的应用程序以验证输出。

最后更新于 2001 年 7 月 11 日。最新更新如既往是一大批新文件集合，但只有一个页面专门用于《星际迷航》系列——《企业号》（Enterprise）。新增详情请参阅新闻页。

如果您的浏览器可以正常显示图形，如果您的连接较慢或者您正在下载大量相似的文件，我们建议您充分利用我们的材料。获取网站的最新版本。

本网站使用了大量的图形和表格（但没有框架），在 800x600 及以上的分辨率下查看效果最佳。我们还使用了级样式表（CSS）以获得更好的效果。

关于如何导航本网站和技术方面的说明：

图 8.2 《星际迷航：声音与视觉》。

```xml
<field name="question1">
  <audio src="mccoy-bricklayer.wav" timeout="1500">
    我是一个医生，不是一个泥瓦工。
  </audio>
  ...
</field>

<field name="question2">
  <audio src="spock-mindprobe.wav" timeout="1500">
    船长，我建议使用瓦肯精神脑探测。
  </audio>
</field>

<field name="question3">
  <audio src="kirk-beameup.wav" timeout="1500">
    柯提。把我送上去。
  </audio>
  ...
</field>
```

列表 8.3 用于引用的音频提示。

## 录制提示词

使用 Program Files 中提供的附件录音机，您可以在本地 Windows 桌面上录制 `.wav` 文件。这些录制对于构建您的初始原型很有用，但生产级应用程序应该具有专业录制的提示词。

音频文件包含在当前项目的下载包中。它们将帮助您快速上手，但如果您录制自己的，您的项目将具有个性化。

表 8.1 语音提示词和内容

| 姓名 | 内容 |

| :--- | :--- |

| Correct | 正确！ |

| Incorrect | 错误。 |

| Try | 再试。 |

| Thank you | 感谢参与。 |

## 完成 VoiceXML 模板

```xml
<?xml version="1.0"?>
<!DOCTYPE vxml PUBLIC "-//W3C//DTD VoiceXML 2.0//EN" "http://www.w3.org/TR/voicexml1/dtd">
<vxml version="2.0">
  <!-- 问候 -->
  <form id="greeting">
    <block>
      <audio src="startrek-theme.wav" fetch="stream"/>
      <audio src="startrek-welcome.wav" timeout="2000">
        欢迎来到《星际迷航》引用游戏。
      </audio>
      <goto next="#questions"/>
    </block>
  </form>

  <!-- 问题 -->
  <form id="questions">
    <!-- 表单作用域无输入处理 -->
    <input count="1">
      <audio src="startrek-noinput1.wav" timeout="1000">
        我什么都没听见。请重试。
      </audio>
    </input>
    <input count="2">
      <audio src="startrek-noinput2.wav" timeout="1000">
        你必须说 Spock、Kirk 或 McCoy 才能参与。
      </audio>
    </input>
    <input count="3">
      <audio src="startrek-noinput3.wav" timeout="1000">
        这是你的最后机会，伙计。你最好说点什么。
      </audio>
    </input>
  </form>
</vxml>
```

列表 8.4 完成的测验生成器脚本。

# 项目 8

```xml
60.   <input count="4">
61.   <audio src="startrek-noinput4.wav"
62.     fetchtimeout="1000">
63.     噢，好吧，那是你的损失。
64.   </audio>
65.   <goto next="#goodbye" />
66.   </input>
67.
68.   <!-- 指令 -->
69.   <block>
70.     <audio src="startrek-instructions.wav">
71.       fetchtimeout="1000">
72.     你将听到一段《星际迷航》角色的
73.     引言。你必须回答斯波克（Spock）、柯克（Kirk）
74.     或麦伊（McCoy）。
75.   </audio>
76.   </block>
77.
78.   <!-- 开始确认 -->
79.   <block>
80.     <audio src="startrek-confirmbegining.wav">
81.     这是第一段引言。
82.   </audio>
83.   </block>
84.
85.   <!-- 问题 1 -->
86.   <field name="startrek-mccoy-bricklayer.wav">
87.     <audio src="startrek-mccoy-bricklayer.wav">
88.       fetchtimeout="2000">
89.     我是一个医生，不是砖瓦工。
90.   </audio>
91.   <grammar>
92.     <![CDATA[
93.       [ mccoy bones doc doctor ]
94.     ]]>
95.   </grammar>
96.
97.   <!-- 匹配处理处理器 -->
98.   <nomatch count="1">
99.     <audio src="startrek-incorrect.wav">
100.      fetchtimeout="1000">
101.     错误。
102.   </audio>
103.   <audio src="startrek-hint.wav">
104.     fetchtimeout="1000">
105.     这里有一个提示。
106.   </audio>
```

**列表 8.4** 完成的测验生成器脚本。（续）
