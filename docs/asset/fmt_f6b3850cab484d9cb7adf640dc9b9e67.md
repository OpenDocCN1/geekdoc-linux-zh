
列表 5.10 是完成后的地址模板，填充了取自项目 3 的代码。原始代码的唯一更改在第 20 到 26 行。原始表单在 `<filled>` 元素中有一个 `if/else` 语句，用于控制流程，将处理转移到告别表单。这现在已更改为处理 `<return/>` 元素。

```xml
1. <?xml version="1.0"?>
2.
3. <vxml version="2.0" application="templates.vxml">
4.
5. <!-- ADDRESS -->
6. <form id="address">
7. <field name="SnailMail" type="boolean">
8.
9. <prompt>
10. <value expr="companyName" of
11. is located on the fourth planet of
12. the local solar system <break size="small"/>
13. third quadrant <break size="small"/>
14. northern section <break size="small"/>
15.
16. parsec 7891<break size="small"/>
17. The main intersection is 12th Street and Vine.
18. Would you like me to repeat the address.
19.
20. </prompt>
21.
22. <filled>
23. <if cond="SnailMail">
24. <clear/>
25. <else>
26. <return/>
27. </if>
28.
29. </field>
30. </form>
```

列表 5.10 地址模板。

# 项目 5

将项目 3 的内容添加到 `templates.vxml` 文档中。在进入下一节之前，验证其处理正常。

### 语音模板

列表 5.11 中的代码直接取自项目 3。

```xml
1. <?xml version="1.0"?>
2.
3. <xml version="2.0" application="templates.vxml">
4.
5. <!-- LEAVE -->
6. <form id="voice">
7.
8. <record name="voice"
9. beep="false"
10. maxtime="10s"
11. finalence="1.5s"
12. type="audio/wav"
13. <prompt>
14. You will have 10 seconds to record a message.
15. Please speak after the tone.
16. </prompt>
17.
18. <record/>
19.
20. <!-- OFFER TO RECORD -->
21. <field name="voiceMessage" type="boolean">
22. <prompt>
23. Here is your message.
24. </prompt>
25.
26. <filled>
27. <if cond="voiceMessage">
28. <clear/>
29. <else>
30. <return/>
31. </if>
32. </filled>
33. </field>
34. </form>
```

列表 5.11 消息。

## 模板与多文档 165

| 行 | 内容 |
| :--- | :--- |
| 39 | name="voiceMessage" |
| 40 | fetchtimeout="10s" |
| 41 | <filled> |
| 42 | <audio>Your message has been sent.</audio> |
| 43 | <return/> |
| 44 | </filled> |
| 45 | <subdialog> |
| 46 | </xml> |
| 47 | </form> |
| 48 |  |
| 49 | </xml> |

列表 5.11 消息。（续）

使用项目 3 中的语音模板来填充占位符模板。

### 传输模板

列表 5.12 在第 35 行使用 `<block>` 元素，因为 `<return>` 不能是 `<form>` 的子元素。

```xml
1. <?xml version="1.0"?>
2.
3. <xml version="2.0" application="templates.vxml">
4.
5. <!-- TRANSFER CALL -->
6. <form id="transfer">
7. <block>
8. Please wait while we wake up the android.
9. </block>
10.
11. <transfer>
12. name="reception"
13. connecttimeout="20s"
14. maxtime="60s"
15. bridge="true"
16. dest="800-555-1212">
17.
18. <filled>
19. <if cond="busy'">
20. <prompt>
21. Hal is busy chatting with Dave.
22. Please try later.
23. </prompt>
24. <else cond="far_end_disconnect'">
25. Hal has terminated the call.
26. <else cond="noanswer'">
27. <prompt>
28. Hal is not responding.
29. Dave might have unplugged him.
30. </prompt>
31. </if>
32. </filled>
33. </transfer>
34. <block><return/></block>
35. </form>
36. </xml>
```

传输模板。

### 安全登录

在项目 4 中，使用用户名/密码组合或语音程序创建了安全登录脚本。我们将把安全登录程序添加到当前项目中，并提供一个隐藏链接，该链接只有专业用户可以通过主菜单访问。

在列表 5.13 的第 5 到 9 行添加了一个链接。当用户说“security”时，处理将转移到 `templatesauthenticate.xml` 脚本。注意，该链接仅在菜单处于激活状态时有效。通过隐藏实现安全并不被认为是访问安全材料的安全方法，因为在激活链接时会有身份验证程序，这对于我们的目的来说足够了。

## 模板与多文档 167

```xml
1. <?xml version="1.0"?>
2.
3. <xml version="2.0" application="templates.vxml">
4.
5. <link next="templatesauthenticate.vxml">
6. <grammar>
7. <![CDATA[(security access)]]>
8. </grammar>
9. </link>
10.
11. <!-- 主菜单 -->
12. <menu id="mainmenu" dtmf="true">
13. <prompt>
14. 如需听取公司地址，请说“Address”。
15. <break size="medium"/>
16. 如需语音留言，请说“Voice”。
17. <break size="medium"/>
18. 如需与 AI 接线员通话，请说“Hal”。
19. </prompt>
20.
21. <choice next="templatesaddress.vxml">
22. <grammar>[ address ]</grammar>
23. </choice>
24. <choice next="templatesvoice.vxml">
25. <grammar>[ voice ]</grammar>
26. </choice>
27. <choice next="templatesoperator.vxml">
28. <grammar>[ hal ]</grammar>
29. </choice>
30. <nomatch>
31. 我没听清。请重试。
32. <reprompt/>
33. </nomatch>
34. </menu>
35.
36. </vxml>
```

**列表 5.13** 在菜单中添加一个隐藏链接。

在为经验用户创建应用程序时，隐藏链接非常有用。如果呼叫者知道这些链接可用并知道激活它们需要什么语法，它们可以为用户开启一个短暂的机会窗口。因为没有提示指示该链接的存在，用户必须预先知道提示的位置。当将其明智地插入 VoiceXML 应用程序中时，它可以允许经验用户通过直接跳转到相关部分来跳过说明性消息和分级菜单。

### 语法的范围

语法有范围，就像变量范围一样。语法的范围可以通过上下文设置（如列表 5.13 所示），或者在某些情况下显式使用 `scope` 属性设置为 `document` 或 `dialog`。列表 5.13 第 5 到第 9 行的隐藏链接仅在 `templatesmain.xml` 文档激活时可用。

在链接内设置的语法范围与包含链接的元素处于同一级别。我们之前在构建应用程序根节点顶部的“重新开始”链接时已经见过，创建了一个可以在整个应用程序中访问的语法。链接语法也可以被限制在文档中任何叶子节点的文档级别，使用将 `grammar` 作用于当前文档的设置，正如列表 5.12 所示。链接内的语法无法使用 `scope` 属性。

表单级（Form-level）语法在处理处于 `<form>` 内部时激活。这被认为是对话范围（dialog scope），`<menu>` 元素的默认范围与 `<form>` 元素处于同一级别，遵循语法范围的规则。

`<form>` 可以携带一个 `scope` 属性到 `document`，从而覆盖语法的默认范围，强制将其设置为文档级别。如果包含 `<form>` 的文档是应用程序根文档，则该语法在整个多文档应用程序中可用。当识别并激活当前 `<form>` 或 `<menu>` 的语法时，当前 `<form>` 或 `<menu>` 的处理将终止，控制转移到识别该语法的 `<form>` 或 `<menu>`。

表单不仅限于包含单个 `<grammar>`。在 `<form>` 内部，每个 `<grammar>` 元素都可以携带 `scope` 属性，指定对话级别或文档级别内的元素。如果 `<form>` 和 `<grammar>` 元素都带有 `scope` 属性，则以 `<grammar>` 元素为优先。

在字段级（field level）设置的语法仅在该字段内激活，且不能携带 `scope` 属性。

> 安全访问链接被视为文档级范围。它被限制为从菜单文档内部访问。请参阅 W3C VoiceXML2.0 工作草案第 3.1.3 节，获取语法范围的详细概述。

![](img/d9ce4ec0787e3fb0ec0d55aacfae3973_190_0.png)

通过插入一个访问验证程序的隐藏链接来修改 `templatesmain.xml` 文件。

![](img/d9ce4ec0787e3fb0ec0d55aacfae3973_190_1.png)

### 登录模板

菜单模板中的隐藏安全链接指向 `templatesauthenticate.xml` 文件。该文件是一个占位符（如列表 5.14 所示），用于验证程序。第 8 行指向包含安全数据的文件或过程（在本例中，这是一个占位符模板），如列表 5.15 所示。

```xml
1. <?xml version="1.0"?>
2.
3. <xml version="2.0" application="templates.vxml">
4.
5. <form id="authenticate">
6. <block>
7. 在验证模板内部。
8. <goto next="templatessecureddata.vxml"/>
9. </block>
10. </form>
11.
12. </xml>
```

**列表 5.14** 登录模板。

由于这些模板不是作为子对话调用的，因此 `<return>` 元素不将处理传回对话。每个模板都使用 `<goto>` 元素显式访问下一个文档。
