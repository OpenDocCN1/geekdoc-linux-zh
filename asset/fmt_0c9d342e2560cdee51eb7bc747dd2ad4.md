
全选我们所有人!

`AM`

`PM`

`FM`

<HR>

### 表单3 隐藏

`f3-1`

`f3-2`

项目 1
项目 2
项目 3
项目 4
项目 5

![](img/6e99147f217994f89499215b2cff677f_175_0.png)

图 5.1: 一个多表单文档（列表 5.1-

# 处理表单

#### 注意

你可以通过此书在 Sytex 网站上的链接 `http://www.sytex.com` 访问列表 5.1 的文件 `formacc.htm` 以及这本 Complete 书中的所有代码列表。

`displayFormData()` 函数创建并打开一个单独窗口，并将窗口对象赋值给变量 `win2`。然后，它使用 `text/plain` MIME 类型打开窗口文档。它利用第一个窗口文档对象的数组来确定文档中包含多少个表单。然后它将这些信息写入 `win2` 包含的文档中。接下来，它使用表单元素数组的 `length` 属性识别每个表单中的元素数量。最后，通过 `win2` 显示表单元素的 `type` 属性，如图 5.2 所示。

![](img/6e99147f217994f89499215b2cff677f_176_0.png)

图 5.2: 多表单文档的内容摘要（列表 5.1）

# 使用表单事件处理器

JavaScript 处理表单相关事件的能力是自定义表单行为的强大工具。它允许你控制用户与表单的交互，并在用户输入数据时处理表单数据。它还允许在用户的浏览器本地处理表单数据，减少对通信带宽和 Web 服务器的负载。

# 第五章

表单事件处理器响应指示用户执行了输入操作的事件，例如填写文本字段、点击按钮或提交表单。这些事件处理器检查用户输入的数据，然后提示用户纠正错误，或提供有关输入数据的其他反馈。你还可以使用表单事件处理器根据用户对之前表单的响应，自适应地向用户展示新表单。

### 响应用户操作

一般的事件处理以及表单事件处理在第 3 章“JavaScript”中介绍。如果你还没有读过第 3 章，最好在继续阅读本章之前复习相关内容。

大多数表单属于以下几类：

- **点击与勾选**：这是常见的表单事件类型。用户点击按钮或勾选复选框以提供信息或执行操作。这些事件由事件处理函数处理，这些函数向用户反馈响应点击或勾选操作的结果。
- **文本更改**：文本更改是另一种常见的表单事件。用户在文本字段或文本区域中输入数据时会生成一个事件，事件处理器会验证用户的输入并根据用户的输入进行进一步处理。
- **列表选择**：当用户从选择列表中选择一个项目时，事件处理代码会验证该选择与其他输入保持一致，并执行由选择指示的任何处理。
- **焦点改变**：当表单元素（如文本字段或选择列表）接收或丢失当前输入焦点时会发生焦点改变事件。这些事件通常不需要特殊的事件处理。然而，在需要时 JavaScript 提供了此类操作的能力。
- **表单提交与重置**：当用户点击提交或重置按钮时会生成这些事件。表单提交事件通常通过验证用户输入的所有数据、对数据进行任何本地处理，然后将数据转发给 CGI 程序或其他服务器端脚本来处理。

由于我们在第 3 章中已经涵盖了表单事件处理，我不会再用更多琐碎的例子来扰你。相反，让我们利用 JavaScript 的事件处理能力创建一个基于表单的吊挂游戏——这在仅用 HTML 是无法实现的。

如果你还不熟悉吊挂游戏（Hangman），这里有一个简短描述：你尝试通过一个一个猜字母来猜一个未知单词。起初你会看到一个单词模式，其中要猜单词的每个字母都由下划线 `_` 字符表示。该模式指示单词中有多少个字母，仅此而已。当你猜出一个单词中有的字母时，单词中的下划线将被字母替换，从而显示该字母出现的位置。你继续猜，直到用完猜测次数或猜中单词。每当你猜错一次，吊架上就会增加一个部分。你只有七次猜错的机会，否则就会结束。如果你猜中了所有字母，你就赢了。这就是为什么它叫吊挂游戏。

# 152 第五章

![](img/6e99147f217994f89499215b2cff677f_179_0.png)

图 5.3: 吊挂游戏开始（列表 5.2）。

![](img/6e99147f217994f89499215b2cff677f_179_1.png)

图 5.4: 猜对了（列表 5.2）。

![](img/6e99147f217994f89499215b2cff677f_180_0.png)

图 5.5: 猜错了（列表 5.2）。

![](img/6e99147f217994f89499215b2cff677f_180_1.png)

图 5.6: 你被挂了（列表 5.2）。

#### 注意

如果你尝试修改任何表单字段，弹出的提示消息会告诉你不要动它。试试看会发生什么。

列表 5.2 显示了 `hangman.htm` 文件的内容。这个文件相当长，但不用担心；我会逐部分讲解。该文件包含两个脚本：一个在文档头部（head），一个在文档主体（body）。我将从文档头部的脚本开始，因为浏览器首先处理它。

# 处理表单

# 列表 5.2: JavaScript 吊挂游戏 (hangman.htm)

```html
<HTML>
<HEAD>
<TITLE>Hangman</TITLE>
<SCRIPT LANGUAGE="JavaScript">
gallows = new Array(
"------"
0
|/\n|/\n|/\n======,
"------"
0
|/\n|/\n|/\n======,
"------"
0
|/\n|/\n|/\n======,
"------"
0
|/\n|/\n|/\/\n======,
"------"
0
|/\n|/\n|/\/\n======,
"------"
0
|/\n|/\n|/\n/\n======,
"------"
0
|/\n|/\n|/\/\n\n=====") = new
guessChoices = Array("JavaScript","Navigator","LiveConnect","LiveWire")
function startGame() {
guesses = 0
max = gallows.length-1
guessed = ""
len = guessChoices.length -1
toGuess = guessChoices[Math.round(len*Math.random())].toUpperCase()
displayHangman()
displayToGuess()
displayGuessed()
}
function stayAway() {
document.game.elements[3].focus()
alert("Don't mess with this form element!")
}
function displayHangman() {
document.game.status.value=gallows[guesses]
}
function displayToGuess() {
pattern=""
for(i=0;i<toGuess.length;++i) {
if(guessed.indexOf(toGuess.charAt(i)) != -1)
pattern +=(toGuess.charAt(i)+"")
else pattern +==" "
}
}
```
</SCRIPT>
</HEAD>
<BODY>
<form name="game">
<input type="hidden" name="status">
<div id="display"></div>
<input type="text" name="guess" onclick="stayAway()">
<input type="button" value="Start" onclick="startGame()">
</form>
</BODY>
</HTML>
```
