
136.     </exit>

137.   </nomatch>

138. 

139.   <filled>

140.     You said <value expr="beachName$.utterance"/>

141.   </filled>

142.   </field>

143.   </form>

144. </xml>

```

**列表 7.7** 完成的身份验证和海滩选择脚本。（续）

## 生成 URI

列表 7.7 顶部的 `confirmedReporterId` 变量被赋值为等待，文本提到：列表 7.7 顶部声明的 `confirmedReporterId` 变量在第 91 行和 92 行被赋值。90 行的 `<if>` 条件比较了 `reporterName` 槽和 `reporterId` 槽，如果比较为真则赋值。有了 `confirmedReporterId` 变量，现在可以使用它来生成一个访问语法文件中特定海滩集合的 URI。

第 124 行到 148 行的 `<form>` 是读取和处理报告的占位符。它从请求海滩名称开始，并用于比较 `beachnames.grammar` 文件中可用的海滩列表。第 130 行和 131 行使用了 ECMAScript 连接操作符来调用带有片段标识符的外部语法文件。对语法的调用使用了单引号，表示它是与 `confirmedReporterId` 变量连接的字字符串。当变量名没有加引号时，它指示处理器这不是字面文本，而是需要扩展其值的变量。当访问语法文件时，它将寻找以 `confirmedReporterId` 命名的规则，我们将在下一节中设置。

第 144 行是一个占位符，向开发者确认识别到的输入。这将在下一节中替换为记录程序。

> 动手实践 调用外部语法文件中的特定语法规则。片段标识符指向一个与报告员 ID 名称相同的规则。下一节将实际为语法文件中创建这些规则名称。

## 将报告员映射到海滩名称

列表 7.8 显示的外部语法将 `AllBeaches` 语法规则更改为映射到 `reporterId` 的多个语法集。每个 `reporterId` 都映射到一个指定哪些海滩可供报告的语法。

语法内部的注释是用分号做的；而不是常用的注释标签。第 1 行和第 2 行以注释结束，提醒脚本维护者报告员姓名与每个区域相关联。

> 提示 语法不能包含常用的注释标签（`<!-- comment -->`）。要在语法中包含注释，请使用分号。分号后的行上的任何内容都将被视为注释。

报告员可以通过在对应的方括号内插入另一个规则来覆盖多个区域。例如，如果 Tim Chandler 可以覆盖墨西哥下哈边界（Baja）的海滩，同时覆盖加州南部的海滩，则语法规则应作为 B4321 规则的语法进行插入：

```
B4321 [SouthernCalifornia BajaMexico]
```

## 报告记录 221

- 1. AL234 [ Hawaii ] ; Mark Miller
- 2. B4321 [SouthernCalifornia] ; Tim Chandler
- 3.
- 4. 南加州 [
- 5. (ventura beach) (<beachName venturaPoint>)
- 6. (county line) (<beachName countyLine>)
- 7. (huntington beach) (<beachName huntingbeach>)
- 8. (manhattan beach) (<beachName manhattanBeach>)
- 9.
- 10.
- 11. 夏夷 [
- (pipeline) (<beachName pipeline>)
- (south shore) (<beachName southShore>)
- (checkpoint) (cromwells) (<beachName blackPoint>)
- (richardsons) (<beachName richardsons>)
- ]

**Listing 8** 在外部文件中为 `beachName` 语法规则创建一个 `reporterid`。

> 语法标签中的 `expr` 属性是 BeVocal 的专有扩展。如果您没有使用 BeVocal 环境，请查阅您平台的文档以查看该功能是否可用。

> 从 `beachnames.grammar` 文件中删除 `AllBeaches` 语法规则，并将其替换为映射到特定区域的 `reporter id`。在继续之前，请测试您的应用程序。

## 记录报告

在项目 3 中，当调用者想要留下语音消息时会进行录音。我们将以此为起点，创建冲浪报告的录音，如列表 7.9 所示。

```xml
<form id="recordReport">
<field name="beachName">
<audio src="which-beach.wav">
您正在为哪个海滩制作报告？
```
**Listing 7.9** 进行录音。（续上）

```xml
</audio>
<grammar expr="beachnames.grammar#" +
confirmedReporterId"/>
<nomatch count="1">
请重复海滩名称。
</nomatch>
<nomatch count="2">
请拨打 surfline.com 以确认
您的报告员身份
<exit/>
</nomatch>
</field>
<!-- 开始制作录音 --
<record name="theReport"
beep="true"
tmaxime="30s"
finsilence="1.5s"
type="audio/wav">
<audio src="thirty-seconds.wav">
您有 30 秒时间来录制针对 <value expr="beachName$.utterance"/> 的报告
请在提示音后开始说话。
</audio>
</record>
<!-- 回放 --
<field name="confirm" type="boolean">
<audio src="playback.wav">
让我播放一下您录制的内容：
</audio>
<prompt>
<value expr="theReport"/>
</prompt>
<!-- 用户确认 --
<audio src="keep-it.wav">
您想保留它吗？
</audio>
</filled>
<if cond="confirm">
<assign name="nameOfRecording"
expr="beachName + '.wav'"/>
<audio src="saved.wav">
请等待，正在保存报告。
录音名称将为
```
**Listing 7.9** 进行录音。

```xml
54.   <value expr="nameOfRecording"/>
55.   </audio>
56.   <else>
57.     <audio src="re-record.wav">
58.       让我们重新开始。
59.     </audio>
60.     <clear/>
61.   </if>
62.   </filled>
63.   </field>
64. 
65.   <subdialog name="saveMessage"
66.     src="http://localhost/cgi-bin/recording.cgi"
67.     method="post"
68.     enctype="multipart/form-data"
69.     name="thereport nameOfRecording">
70.     </filled>
71.     <audio>
72.       您的报告已保存为文件
73.       <value expr="nameOfRecording"/>
74.     </audio>
75.   </filled>
76.   </subdialog>
77. 
78. <-- 另一个报告吗？ -->
79. <field name="anotherReport" type="boolean">
80.   <audio src="another-report.wav">
81.     您想为不同的
海滩提交报告吗？
83.   </audio>
84.   </filled>
85.   <if cond="anotherReport">
86.     <clear/>
87.     <goto next="#recordReport/>
88.   </if>
89.   </filled>
90.   </field>
91. 
92. <-- 退出/断开 -->
93. <field name="goodbye">
94.   <audio src="thank-you.wav">
95.     感谢帮助。
96.     下次见。
97.   </audio>
98.   <catch event="ninput nomatch">
99.     <exit/>
100.  <catch>
101.  </field>
102. </form>
```
**Listing 7.9** 进行录音。（续上）

## 项目 7

录音 `<form>` 开始通过 `beachName` 字段请求海滩名称，并根据 `beachnames.grammar` 文件中的内容进行比对。`reporterid` 是[此处省略]。

## 报告记录 225

使用列表 7.9 作为设置录音的模板。通过 Vocite 验证脚本有效。

## 保存录音

剩下的工作是保存录音，以便在有人请求海滩时可以访问。

## 将字段名和变量传递子对话

在 7.9 的第 65 行 `<subdialog>` 中，`src` 属性指向处理报告并将其存储在 Web 服务器上的脚本。正如我们看到的，`namelist` 是子对话接收并处理的变量名列表，`theReport` 存储用户的实际输入，`nameOfRecording` 是来自 `<assign>` 元素 49 的生成的文件名。

## 处理录音

VoiceXML 不提供保存录音的方法。它必须动态处理，就像调用 Web 服务器上的任何其他 CGI 脚本一样。列表 7.10 提供了一个简单的 Perl 脚本在 Web 服务器上保存录音，但您可以使用任何选择的编程语言来实现相同的结果。

```perl
1. #! /usr/bin/perl -w
2.
3. use CGI qw(:standard);
4.
5. $pathToRecordings = "./recordings";
6. $nameOfRecording = param("nameOfRecording");
7. $theReport = param("theReport");
8.
9. $++;
10.
11.
12. open (SAVE, ">\$pathToRecordings/\$nameOfRecording)
13. or die("Could not open file for saving: \$!");
14.
15. binmode(SAVE);
16. while (read(param('theReport'),\$data,1024))
17.
    print SAVE \$data; 
18.
19. close(SAVE);
```
**Listing 7.10** 处理录音。（续上

## 226 项目 7

```
20.
21. print "Content-Type: text/xml\n\n"
22.
23.
24. # 确认录音已保存
25.
26. print <<XML;
27. <?xml version="1.0"?>
28.
29. <xml version="2.0">
30. <form id="acceptInput">
31.
32. <body>
33. 输入内容长度为 $ENV{'CONTENT_LENGTH'} 字节。
34. Name $NameOfRecording 已处理
35. 并保存。
36. <return/>
37. </body>
38. </form>
39. </xml>
40.
41. 列表 7.10 正在录音（继续）
```
Perl 脚本开始于对 Perl 解释器的调用。Perl 可能安装在 Web 服务器上的不同位置，因此请咨询您的管理员。第 1 行末尾的 `-w` 选项会开启警告消息，如果脚本运行异常，这些消息可能帮助调试。

`CGI` 模块将通过几个简单的方法处理所有繁重的工作，并刷新缓冲区，将输出立即发送到标准输出。变量将进行拼接以形成录音的路径和文件名，位于第 5 到第 7 行。`PathToRecords` 存储脚本运行当前目录下的目录。`$NameOfRecording` 接收来自调用对话框列表的输入。脚本的其余部分是项目 3 中录音部分的哈希表，使用 `$report` 参数作为文件句柄的输入。

脚本输出的最终 VoiceXML 输出包含在第 26 到第 41 行的 `print` 语句中。第 33 行用于开发者信息，并提供了传递给脚本的录音内容大小的信息。一旦脚本经过测试并运行正常，就可以将其删除。

## 测试脚本

我们需要通过进行录音并保存它来验证脚本是否运行正常。你必须拥有一个允许运行 CGI 处理的 Web 服务器。如果你目前有一个允许 CGI 处理的账户，请将脚本加载到服务器并测试您的应用程序。

对于没有托管账户的用户，运行测试的简单方法是在本地机器上安装 Apache 服务器，并让对话框调用指向 `cgi-bin` 内的脚本。运行 VoiceXML 将允许你在不使用电话的情况下测试您的应用程序。如果你指向的是本地服务器，这对于 CGI 处理是有效的。

首先，将 `<record>` 元素上的 `beep` 属性更改为 `false`，否则 VoiceXML 将报错错误。其次，对话框调用必须指向 IP 地址，目前在列表 7.9 的第 6 行设置为 `localhost`。要查找您的 IP 地址，请使用 DOS 窗口并在提示符处输入 `ipconfig`。输出将包含分配给当前会话的 IP 地址。

你可以通过在本地机器上安装 Apache Web 服务器并将服务器上的脚本作为对话框，来测试你的 Perl 脚本结果。这使得在运行 VoiceXML 脚本运行时方便地更改 CGI 脚本。

在您的 Web 服务器上安装录音脚本。更改 VoiceXML 应用程序对话框调用中的路径以指向脚本。测试应用程序以确认它正将录音保存到您的 Web 服务器上。

## 访问录音

现在录音已存储在 Web 服务器上，需要一种方法来生成冲浪报告列表，并通过网页或电话提供这些服务。列表 7.11 是一个简短的 Perl 脚本，它将动态创建 `recordings` 目录下所有录制文件的列表。

第 1 行指定了 Web 服务器上 Perl 的路径。第 3 行的 `strict` 原始指令强制声明所有变量；这在 Perl 中不是强制性的。第 4 行导入了 `File::Basename` 用于从长字符串中提取文件名。第 8 行使用 Perl 中的 `glob` 函数获取指定目录中所有以 `.wav` 结尾的文件，并将名称作为数组返回。

列出报告文件。从第 10 行开始的循环访问数组中的每个名称，并将其输出为指向 HTML 网页的链接。第 11 行使用 `File::Basename` 模块中的 `basename` 方法提取文件名并将其存储在标量变量 `$filename` 中。使用正则表达式替换移除文件的 `.wav` 扩展名，这样网页上只会显示海滩名称。第 13 行构建了链接，点击该链接将将激活并在浏览器内播放声音文件。

在您的 Web 服务器上安装列表 7.11，并验证您是否有权访问为每个冲浪报告创建的录音。

## reportRecorder.vxml

列表 7.12 是报告记录器项目的最终脚本。为了优化性能，已删除了 `DOCTYPE` ，脚本顶部有一个全局重新开始链接，并删除了所有开发者的测试 `print` 语句。第 93 行在身份验证后按名称问候报告者。通过这些更改，该脚本可以从任何可以访问电话的地方创建冲浪报告。

```
1. <?xml version="1.0"?>
2.
3. <vxml version="1.0">
4.
5. <link next="listing9-11.vxml">
6.   <grammar>(start over)</grammar>
7. </link>
```
列表 7.12 完成的录音器脚本。
