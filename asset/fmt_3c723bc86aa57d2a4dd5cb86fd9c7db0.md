
`utterance` 影子变量返回平台理解为属于该字段定义语法一部分的原始输入。在当前应用程序中，用户说出一个名字，平台根据语法中可用的姓名列表检查输入，如果识别出名字，则将输入存储在 `getContactName$.utter` 影子变量中。平台识别语音语法的置信度可以通过 `getContactName$.confidence` 变量访问，输入模式（无论是 DTMF 还是语音）可以通过 `getContactName$.input` 变量访问。

### 检查用户输入

列表 6.3 第 35 行的 `<prompt>` 中设置了一个 1.5 秒的机遇窗口，为呼叫者提供了响应提示的机会，尽管他们并不知道该窗口的存在。存在一个隐藏的提示，其任何响应都被视为错误，并由第 42 行的 `<nomatch>` 元素处理。如果用户有任何响应，表单中的所有字段将通过第 42 行 `<nomatch>` 块内的 `<clear>` 元素清除。应用程序将通过输出 "I'm sorry" 对错误承担口责任，FIA 回到第一个字段。

在 1.5 秒窗口关闭后，假设呼叫者没有反应，意味着电话是要取消的。`<noinput>` 元素为 `confirmName` 字段赋值，允许 FIA 继续进入对话的下一部分。从第 48 行开始的 `getBlock` 是占位符，将在后续章节中开发。

> 使用隐含和隐藏对话是确认用户输入且不拖累用户的好方法，无需重复。

将列表 6.1 中的现有语法替换为列表 6.2 中新定义的槽位填充语法。测试您的应用程序以验证输出的是要拨打人员的电话号码，而不是其姓名。

### 确认用户输入

如果用户每次说话时都隐含对其输入的确认，而不是每次都显式陈述，语音应用程序听起来会更自然。例如，如果用户说“Mary”来请求一个名字，应用程序不是用提问确认（“你说的是 Mary。正确吗？”），而是用陈述回答：“正在拨打 Mary 201456464。”这确认了系统正确理解了用户并获取了电话号码。

作为一个一般规则，系统会向用户重复你刚刚说的陈述，用户的任何响应都应被视为否定响应并作为错误捕获。列表 6.3 开启了一个 1.5 秒的小窗口，用于接收用户的响应。

```
1. <?xml version="1.0"?>
2.
3. <!DOCTYPE vxml
4. PUBLIC
5. "//BeVocal In//VoiceXML 2.0//EN//dtd/vxml2-0-bevocal.dtd"
6. "http://cafe.bevocal.com/libraries/dtd/vxml2-0-bevocal.dtd"
7.
8. <xml version="2.0">
9.   <form id="gettxtName">
10.
11.    <prompt>
12.      Whom would you like to contact?
13.    </prompt>
14.
15.
16.    <grammar>
17.     <![CDATA[
18.     [
19.      [rosmary] (<contactList 7183991234 >)
20.      [john] (<contactList 2012342432 >)
21.      [anthony] (<contactList 2013453453 >)
22.      [kristi] (<contactList 2013453453 >)
23.      [cubby] (<contactList 3343615678 >)
24.      [kim] (<contactList 3343615678 >)
```

**列表 6.3** 确认用户输入。

```
25. [mary] { <contactList 2079674564> }
26. [richard] { <contactList 2079674564> }
27. [aaron] { <contactList 2079674564> }
28. [justin] { <contactList 2079674564> }
29. ]
30. ]>
31. </grammar>
32. </field>
33.
34. <field name="confirmContactName">
35. <prompt timeout="1.5s">
36. Calling <value expr="contactList$.utterance"/>
37. at <value expr="contactList"/>
38. </prompt>
39. <noinput>
40. <assign name="confirmContactName" expr='true*' >
41. </noinput>
42. <nomatch>I'm sorry, clear./</nomatch>
43. </field>
44.
45. <block>
46. Glad to be of service. Good bye.
47. </block>
48.
49. </form>
50.
51. </vxml>
```

**列表 6.3** 确认用户输入。（续）

从第 34 行开始的 `<field>` 元素 `confirmContactName` 会向呼叫者重复识别出的姓名和映射到该姓名的电话号码。要访问用户识别的输入，请引用 `getContactName$.utterance` 影子变量。字段级影子变量返回的是用户说的内容，而不是设置为槽位值的内容。

### 字段级影子变量

在项目 4 验证呼叫者的语音点时，我们简要提到了影子变量。字段级影子变量是作为 VoiceXML 平台语法识别系统的一部分设置的。它们是只读变量，提供了访问平台对语音输入分析的权限，可以根据其值用于条件处理。

`utterance` 影子变量返回平台理解为属于该字段定义语法一部分的原始输入。在当前应用程序中，用户说出一个名字，平台根据语法中可用的姓名列表检查输入，如果识别出名字，则将输入存储在 `getContactName$.utter` 影子变量中。平台识别语音语法的置信度可以通过 `getContactName$.confidence` 变量访问，输入模式（无论是 DTMF 还是语音）可以通过 `getContactName$.input` 变量访问。

### 检查用户输入

列表 6.3 第 35 行的 `<prompt>` 中设置了一个 1.5 秒的机遇窗口，为呼叫者提供了响应提示的机会，尽管他们并不知道该窗口的存在。存在一个隐藏的提示，其任何响应都被视为错误，并由第 42 行的 `<nomatch>` 元素处理。如果用户一个任何响应，表单中的所有字段将通过第 42 行 `<nomatch>` 块内的 `<clear>` 元素清除。应用程序将通过输出 "I'm sorry" 对错误承担口责任，FIA 回到第一个字段。

在 1.5 秒窗口关闭后，假设呼叫者没有反应，意味着电话是要取消的。`<noinput>` 元素为 `confirmName` 字段赋值，允许 FIA 继续进入对话的下一部分。从第 48 行开始的 `getBlock` 是占位符，将在后续章节中开发。

> 使用隐含和隐藏对话是确认用户输入且不拖累用户的好方法，无需重复。

### 可选标记

问号在 VoiceXML 语法中表示可选。要使某些内容变为可选，请在标记之前直接放置一个问号，如列表 6.6 所示。现在，当用户只说出名字或同时说出名和姓时，处理器都能理解用户的请求。为了处理重复项，请省略问号并强制要求姓。

```xml
<grammar>
<![CDATA[
  ( rosemary miller ) { < contactList 718391234 > )
  ( john ?caviglia ) { < contactList 2072342342 > )
  ( anthony kristi ?caviglia ) { < contactList 2074354435 > )
  (( cubby miller ) { < contactList 3343615678 > )
  (( mary jo) richard anton justin) ?weiss)<contactList 2014564564>)>
]]>
</grammar>
```

**列表 6.6** 可选的姓。

## 创建昵称

处理重复项的另一种方法就像我们在现实生活中一样：给其中一个重复项起一个昵称。Anthony 的父亲的名字是 Anthony。在成长过程中，他获得了 Ants 这个昵称。当他母亲大叫他在吃饭前洗手时，不会混淆到底是哪个 Anthony 真的遇到了麻烦。使用相同的技术（当然，不需要大叫）来开发一个没有歧义的列表。

```xml
<grammar>
<![CDATA[
  ( rosemary miller ) { < contactList 718391234 > )
  ( john ?caviglia ) { < contactList 2072342342 > )
  ( anthony louise ) ?caviglia { < contactList 5105812384 > }
  ({ants kristi} ?caviglia { < contactList 2074354533 > }
  (( cubby miller ) { < contactList 3343615678 > )
  (( mary jo) richard anton justin) ?weiss)<contactList 2014564564>
]]>
</grammar>
```

**列表 6.7** 插入昵称。

列表 6.7 为 Anthony 和 Louise Cavaglia 增加了一条联系行。由于此冲突涉及 Anthony 和 Kristi Cavaglia，Anthony Junior 的昵称被插入在第 7 行。

## 主要选择

我们的大多数人都有一个经常联系的简短名单。我们可以通过不将姓指定为标记的一部分，让他们在其他具有相同名字的人中中获得名字的优先级：在主要联系人中省略其姓，并对重复项强制要求姓。用户可以通过一次话语访问集合中最重要的成员，而无需说出全名。

列表 6.8 的第 4 到第 6 行作为主要联系人，并为每个 Rosemary 省略了姓并强制要求了姓。

```xml
<grammar>
<![CDATA[
  {
    romary < contactList 7183991234 >
    (romary oconnor) < contactList 3012932394 >
    (romary clooney) < contactList 2124354455 >
    (john Cavaglia) < contactList 2072342342 >
    (anthony louise) ?cavaglia (< contactList 510581234 >
    ((ants kisti) ?cavaglia) < contactList 2073453435 >
    ((cubby kim) ?miller) < contactList 334615678 >
    ((mary jo) richard aaron justin) ?weiss)<contactList 2014564564>
  }
]]>
```

**列表 6.8** 主要选择。

## 一个联系人的多个号码

许多人有多个联系电话号码。我们可以通过将电话号码标记为可选，来处理一个联系人的多个号码。用户可以通过一次话语访问这些号码，而不需要说出完整的名字。

```xml
1. <grammar>
2. <![CDATA[
3. { ( rosemary ) < contactList 7183991234 >
4. (romary oconnor) < contactList 3012932394 >
5. (romary clooney) < contactList 2124354455 >
6. (john Cavaglia) < contactList 2072342342 >
7. (anthony louise) ?caviglia (< contactList 510581234 >
8. ((ants kisti) ?caviglia) < contactList 2073453435 >
9. ((cubby kim) ?miller) < contactList 334615678 >
10. ((mary jo) richard aaron justin) ?weiss)<contactList 2014564564>
11. }
12. ]
13. </grammar>
```

## 在短句中添加可选词

你可以插入可选的关键词来使短句完整。“rosemary work” 听起来没有“rosemary at work”那么直观。我们将通过这些技术来处理这些号码。

```xml
1. <grammar>
2. <![CDATA[
3. { ( rosemary ) < contactList 7183991234 >
4. (romary oconnor) < contactList 3012932394 >
5. (romary clooney) < contactList 2124354455 >
6. (john Cavaglia) < contactList 2072342342 >
7. (anthony louise) ?caviglia < contactList 510581234 >
8. ((ants kisti) ?caviglia) < contactList 2073453435 >
9. ((cubby kim) ?miller) < contactList 334615678 >
10. ((mary jo) richard aaron justin) ?weiss)<contactList 2014564564>
11. }
12. ]
13. </grammar>
```

**列表 6.9** 短句中的可选词。

## 控制类型语音
