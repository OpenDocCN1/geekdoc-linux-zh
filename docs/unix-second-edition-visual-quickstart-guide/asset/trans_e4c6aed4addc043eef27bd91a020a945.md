

## 使用 write 与其他用户通信

大多数时候，当你连接到 Unix 系统时，你是在与计算机通信。不过，你也可以与登录到同一系统的其他人通信。write 非常适合向其他用户发送快速消息——有点像在他们的电脑上贴一张黄色便签，如图 12.3 所示。

### 使用 write 与其他用户通信的方法：

- 1. write userid
在 shell 提示符下，输入 write 后跟你想要发送消息的人的 userid。你会得到一个空白行和一个闪烁的光标，就等着你输入内容。
- 2. Wanna meet for lunch?
继续输入你的消息（图 12.3）。
- 3. Ctrl D
输入完毕后，按 Ctrl D 发送消息。你输入的内容会出现在对方用户的屏幕上（图 12.4）。

### 提示

- 请记住，write 消息会突然出现在收件人的屏幕上，可能会让人感到突兀！
- 如果你不想接收 write 消息，在 shell 提示符下输入 mesg n。该命令会阻止其他人在当前会话中向你发送 write 消息。输入 mesg y 即可再次启用 write。

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_269_0.png)

图 12.3 你可以使用 write 向系统上的另一用户发送快速消息。

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_269_1.png)

图 12.4 消息会突然出现在用户的屏幕上。

- 你可以使用 wall 命令向登录到系统的所有人发送类似 write 的消息。系统管理员在需要警告人们系统即将关闭时常常用 wall。
- 使用 w 或 who 来查找还有谁登录到系统。有关更多信息，请参阅第 7 章中名为 Learning Who Else Is Logged In with who 和 Learning Who Else Is Logged In with w 的部分。

## 使用 talk 与其他用户通信

你也可以使用 talk 与登录到系统的另一用户进行实时双向对话（非常类似于即时消息聊天）。如图 12.5 所示，你输入消息，对方输入他的消息，你们双方都会在屏幕上看到交流内容。

### 使用 talk 与其他用户通信的方法：

- 1. talk deb
在 shell 提示符下，输入 talk 和你想要交谈的人的 userid。对方用户将被提示输入 talk 和你的 userid。然后，你会看到如图 12.5 所示的 talk 屏幕。
- 2. You just wouldn’t have believed it!
I had just chased the dog for six blocks...Yeah, the stinkin’ pooch always thinks the garbage truck is stealing our stuff... Right. Hilarious.
Anyway, there I was huffing and puffing on the front porch, when a neighbor informed me that some kids were rooting through my trash. Like, what did they expect to find? Old panty hose and coffee filters? Nawww.
I stopped using panty hose for coffee filters a long time ago. It made me look too tan.
输入你想要的任何内容。每个按键都会显示在对方的屏幕上，因此他们会清楚地看到你打字的速度（以及打字的好坏）。
- 3. Ctrl C
完成后，断开连接。

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_270_0.png)

图 12.5 talk 让你可以进行实时双向在线对话。

### 提示

- 你也可以与登录到其他 Unix 系统的人交谈。只需使用 talk userid@wherever.com。当然，填写对方实际的 userid 和地址，这通常与该人的电子邮件地址相同。防火墙经常——但并非总是——会阻止这些聊天。
- 如果有人请求与你进行 talk，只需输入 talk 和该人的 userid（如果该人的主机名与你的不同，则为 userid@wherever.com）。
- 与 write 一样，你可以在 shell 提示符下输入 mesg n 和 mesg y 来在当前会话中关闭和打开 talk。
- 虽然 talk 没有图形界面的即时消息程序那么酷，但它仍然相当不错，对吧？它也是向系统上更有经验的用户寻求帮助的好方法。

