
```perl
1. my $newRecording = createFileName();
2.
3. sub createFileName {
4. my $filename = localtime();
5. $filename =~ s/\s/_g;
6. $filename =~ s/:/-/g;
7. $filename . '.wav';
8. }
```

**Listing 3.5** 生成新文件名。

### 转接电话

XML 使用 HTTP 协议在浏览器和服务器之间交换信息。第 9 行使用 CGI.pm 模块中的 `header` 方法输出 HTTP 头部。`header` 方法设置了标准的 HTTP `content-type`。

第 11 行打开文件句柄 `SAVE`，设置为写入或覆盖存储在 `$pathToRecording` 目录下 `$newRecording` 变量之后的文件。

第 12 行使用 `binmode()` 作为在 Win32 和 Unix 系统之间传递数据的安全机制。Win32 文件系统区分二进制文件和 ASCII 文本文件。`binmode()` 函数指定保存的文件为二进制。它不影响 Unix 到 Unix 或 Win32 到 Win32 的传输。它在该程序中的主要作用是为了移植性。

调用程序传递的 `voiceMessage` 字段在第 13 行读取到 `$data` 变量中，并在第 14 行写入 `$newRecording` 文件。第 15 行关闭 `SAVE` 文件句柄。

> 虽然不是强制性的，但由于 Perl 具有自动垃圾回收机制，关闭任何已打开的文件柄是一个良好习惯。

第 20 行到第 33 行使用 Perl 的 `print` 方法向用户输出确认通知，告知一切顺利。第 23 行是开发者的快速检查，用于测试消息内容的长度。一旦脚本调试完成并运行正常，该行将被注释。

将 Perl 脚本安装到你的 Web 服务器上。在电话上拨打你的程序并留言。打开 Web 浏览器并听录音，确认消息已处理并存储在你的服务器上。拨打几次以确认消息正在被新录音替换。

### `<transfer>` 元素

设置好识别转接请求的菜单后，必须构建一个表单来处理该请求。`<transfer>` 元素是该例程的基础，能够在不退出 VoiceXML 应用的情况下连接另一个电话。

转接有两种类型：桥接（bridge）和盲转（blind）。盲转会断开用户与 VoiceXML 应用的连接，同时让拨号者连接到新号码。桥接中，应用程序会暂停，等待新连接终止，然后返回 VoiceXML 应用。

Listing 3.7 第 2 行的 `<block>` 向用户确认已理解转接请求。第 6 行开始的 `<transfer>` 元素携带了一系列属性，用于设置通话配置。它在字段级别使用 `<filled>` 元素处理来自被叫电话的各种返回。

```xml
1. <form id="transfer">
2. <block>
3. 请等待，我们正在启动安卓。
4. </block>
5.
6. <transfer>
7. name="reception"
8. connecttimeout="20s"
9. maxptime="60s"
10. bridge="true"
11. dest="800-555-1212"
12.
13. <filled>
14. <if cond="reception == 'busy'>
15.   <prompt>
16.     Hal 正在和 Dave 聊天。
17.     请稍试。
18.   </prompt>
19. <elseif cond="reception == 'far_end_disconnect'/>
20. Hal 挂了电话。
21. <elseif cond="reception == 'noanswer'>
22.   <prompt>
23.     Hal 没有接听。
24.     Dave 可能拔了电话。
25.   </prompt>
26. </if>
27. </filled>
28. </transfer>
29.
30. <field name="returnToMenu" type="boolean">
```

**Listing 3.7** 转接电话。

## 联系我们 117

| 行号 | 内容 |

| :--- | :--- |

| 31. | <prompt> |

| 32. | 你想返回主菜单吗？ |

| 33. | </prompt> |

| 34. | |

| 35. | <filled> |

| 36. | <if cond="returnToMenu"> |

| 37. | <goto name="#mainmenu"/> |

| 38. | <else> |

| 39. | 感谢致电。再见。 |

| 40. | <disconnect> |

| 41. | |

| 42. | </filled> |

| 43. | <field> |

| 44. | </form> |

**列表 3.7** 转移通话。（继续）

### `<transfer>` 元素的属性

`<transfer>` 元素的属性控制通话转移通话过程中的处理。`<transfer>` 元素的 *name* 属性是一个唯一标识符，用于存储转移的返回结果。*name* 可用于检查来自桥接转移的返回值并据此处理结果。列表 3.7 第 14 至 26 行的条件检查根据转移返回值是忙音、*far_end_disconnect* 还是 *noanswer* 有相应的响应。

> 有用返回值的完整列表，请参见 VoiceXML 2.0 工作草案的 2.3.7 节。

`timeout` 属性指定了转移尝试连接拨号号码的秒数。默认值由平台决定。如果在分配时间内未建立连接，则在属性中设置 `noanswer` 值。我们的应用程序在第 21 行处理 *noanswer* 值，通知用户已拨通该号码但未接通。*maxtime* 限制了转移后的通话长度。该属性有助于对每路通话执行最大时间限制。由于可能被滥用的风险，大多数语音门户都会对通话转移执行时间限制。BeVocal 对每次转移都有 60 秒的限制。

由于开发者可能滥用 `<transfer>` 函数，大多数语音门户将免费开发者账户的转移通话限制在最多 60 秒。该时间限制不属于 VoiceXML 规范的一部分。

# 项目 3

`bridge` 属性指定在通话终止后是否应将处理传回调用应用程序。BeVocal 平台上的 `bridge` 默认设置为 true。

默认情况下，所有 BeVocal 转移都是将控制权返回给调用脚本的桥接转移（bridge transfers）。

`dest` 属性的值是要拨打的电话号码。长途号码前可以有一个可选的 1。BeVocal 平台允许 5 种格式：

```
phone://8005551212
800-555-1212
phone://800-555-1212
tel:800-555-1212:postd=123
```

最后一个示例在接主号码后拨打分机号。请查看您的平台文档以获取特定的格式要求。

### 检查返回结果

一旦完成转移，错误检查将在 `<filled>` 元素中处理，从第 13 行开始。`goto` 属性使用 `<transfer>` 元素的名称作为检查的条件。忙音、被叫方断开以及接收端的接听都通过描述性消息向用户处理，然后按顺序返回主菜单。

`<transfer>` 元素是字段级元素，允许处理流到 `<form>` 内的下一个项目。一旦 `<filled>` 元素在第 27 行完成处理，将自动访问 `returnToMenu<field>`。它被设置为 `boolean` 类型，使用平台提供的 true/false 语法。在第 32 行，输出一个 `<prompt>`，提议用户返回主菜单。肯定的响应将处理过程转移到菜单顶部。否则，输出一条礼貌消息并终止连接。

在您的应用程序中设置通话转移。通过更改电话号码以访问您的私有语音信箱系统或长途电话来测试该应用程序。

### 完成脚本

“联系我们”脚本的主要部分现在已完成。为了完成脚本，我们需要添加问候和告别表单、全局帮助以及一个重启应用程序的链接，并且我们需要对现有表单进行更改以访问新章节。列表 3.8 显示了完成的脚本。

# 联系我们 119

```
1. <?xml version="1.0"?>
2.
3. <vxml version="2.0">
4. <var name="companyName" expr='Mars Colony 7'/>
5.
6. <!-- 重置链接 --
7. <link next="contact-us.vxml">
8. <grammar>
9. <!--[CDATA[
10. [start over)]
11. ]]]
12. </grammar>
13. </link>
14.
15. <!-- 全局帮助 --
16. <link root="help">
17. <grammar>
18. <rule id="help">
19. <one-of>
20. <item>help me</item>
21. <item>help</item>
22. <item>i'm lost</item>
23. <item>where am lost</item>
24. </one-of>
25. </rule>
26. </grammar>
27. </link>
28.
29. <!-- 全局帮助输出 --
30. <help>
31. <prompt>
32. 你正在与
33. <value expr="companyName"/> 的语音系统。
34. 请选择。
35. </prompt>
36. <reprompt/>
37. </help>
38.
39. <!-- 问候 --
40. <form id="greeting">
41. <block>
42. 你已到达
43. <value expr="companyName"/> 的信息中心。
44. <goto next="#mainmenu"/>
45. </block>
46. </form>
47.
48. <!-- 主菜单 --
```

**列表 3.8** 完成的联系我们脚本。（继续）

```
49. <menu id="mainmenu">
50. <prompt>
51. 要听 <value expr="companyName"/> 的地址，
52. 请说“地址”。
53. 要留言，请说“语音”。
54. 如果你想找接待员，
55. 请说“转移”。
56. </prompt>
57.
58. <choice next="#address">
59. <grammar>address please</grammar>
60. 地址
61. </choice>
62. <choice next="#voice">
63. <grammar>voice message</grammar>
64. 语音
65. </choice>
66. <choice next="#transfer">
67. <grammar>receptionist</grammar>
68. 转移
69. </choice>
70. <nomatch>
71. 您的选项是
72. 请重试。
73. </nomatch>
74. </menu>
75.
76. <!-- 邮件 --
77. <form id="address">
78. <field name="snailMail" type="boolean">
79.
80. <prompt>
81. <value expr="companyName"/>
82. 位于第四行星
83. 本地系统 <break="small"/>第三象限 <break="small"/>
84. 北区 <break="small"/>
85. 第7 秒区 <break="small"/>
86.
87. 主交汇口是 12 街和 Vine 路。
88. 你想重听地址吗？
89. </prompt>
90.
91. <filled>
92. <if cond="snailMail">
93. <clear/>
94. <else>
95. <goto next="#goodbye"/>
96. </if>
97. </filled>
98. </field>
99. </form>
100.
101. <!-- 语音消息 --
102. <form id="voice">
103. <record name="voiceMessage">
104. beep="false"
105. maxtime="10s"
106. finalsilence="1.5s"
107. type="audio/wav">
108. <prompt>
109. 你有 10 秒时间录音。
110. 请在提示音后说话。
111. </prompt>
112. </record>
113.
114. <!-- 提再次录音 --
115. <field name="processMessage" type="boolean">
116. <prompt>
117. 这是你的消息 <value expr="voiceMessage"/>
118. 你想把这条消息发送给
119. <value expr="companyName"/>
120. </prompt>
121.
122. <filled>
123. <if cond="processMessage">
124. 请稍候，正在保存您的消息。
125. <else>
126. 让我们重试。
127. <clear>
128. </if>
129. </filled>
130. </field>
131.
132. <!-- 保存消息 --
133. <subdialog name="saveMessage">
134. src="recording.cgi"
135. method="post"
136. enctype="multipart/form-data"
137. namelist="voiceMessage">
138. <filled>
139. <audio>你的消息已发送。</audio>
140. <goto next="#goodbye"/>
141. </filled>
142. </subdialog>
```

列表 3.8 完成的联系我们脚本。（继续）

```
145. </form>

<!-- 转移通话 -->
<form id="transfer">
<block>
请稍候，我们正在唤醒机器人。
</block>

<transfer>
name="reception"
connecttimeout="20s"
maxtime="60s"
bridge="true"
dest="800-555-1212">

<filled>
<if cond="reception == 'busy'">
<prompt>
Hal 正在和 Dave 聊天。
请稍后重试。
</prompt>
<elseif cond="reception == 'far_end_disconnect'">
Hal 已挂断通话。
<elseif cond="reception == 'noanswer'">
<prompt>
Hal 没有响应。
Dave 可能拔掉了插头。
</prompt>
</if>
<goto next="#goodbye"/>
</filled>
</transfer>
```

# 联系我们 123

```
192.
193. <!-- GOODBYE -->
194. <form id="goodbye">
195.   <field>
196.     <prompt>
197.     祝您愉快。再见。
198.     </prompt>
199.     <grammar>quit</grammar>
200.   </field>
201. </form>
202.
203. </vxml>
```

列表 3.8 完成的“联系我们”脚本（续）

在列表 3.8 中，第 7 行创建了一个全局重新开始链接。正如在项目 2 中讨论的那样，该链接允许开发人员轻松地使用一组新变量重启应用程序，而无需断开并重新拨打。从第 16 行开始的全局帮助模板可以在用户说出帮助语法中被识别的术语时，从应用程序内的任何位置激活。

第 40 行至 46 行的问候语包含在它自己的表单中，以将其与主菜单隔离。这对于允许用户返回主菜单而无需每次都听问候非常有用。第 44 行的 `<goto>` 元素将处理过程转移到 `mainmenu`。

应用程序中的最后一个表单（第 194 行至 201 行的再见表单）有两个用途。它被用作离开应用程序时的优雅退出，并为开发人员提供了通过激活全局重新开始链接来重启应用程序的机会。请注意，这对于用户提示是不可见的，只有开发人员知道。

需要进行一些更改使基础脚本接受再见表单。第 96 行和 97 行向 `<if>` 语句中添加了 `<else>` 条件，如果用户不想重复公司地址，则将用户转移到再见表单。子对话中从第 140 行开始的 `<filled>` 条件现在以 `<goto>` 元素结束再次再次用户发送到再见表单。

通过这些添加和更改，基础的“联系我们”脚本就完成了。

## 结语

就是这样，一个简单的自动问答服务。当你开发更复杂的项目时，请参考我们的自动接线员 Hal，并赋予它更多责任。我们仅用它来处理最基础的服务，但通过菜单层次结构，扩展主菜单以涵盖常见问题（FAQs）、活动日历和一般公司信息将相对简单。项目 6 展示了如何构建一个可以轻松集成到“联系我们”项目的电话目录系统。

项目的另一个添加项是扩展 `<record>` 例行程序，将语音消息保存到每个收件者的私有网页中。收件者可以在在途中登录公司网站并通过 VoiceXML 接口检索消息。`<record>` 元素将在项目 5 中再次使用，届时我们将研究如何将代码片段模块化，使其足够通用，以便在多个应用程序中使用。

该项目的列表可以从 BeVocal 网站 cafe.bevocal.com/wiley/10projects 下载。它们以文本文件的格式保存，可以作为创建你自己的 VoiceXML 脚本的模板。

下一章项目 4 将通过开发一个登录系统来验证用户，完成我们对网页 基础组件的观察。

# 项目 4

用户身份验证
