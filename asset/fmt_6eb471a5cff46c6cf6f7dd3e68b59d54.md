
# 在 Pi 上使用 Python

## 从你的 Pi 发送短信

你可能需要的...

## 从你的 Pi 发送短信

- 树莓派
- Twilio 账户

创建一个结合 Twilio Python 代码的程序，并从你的 Pi 发送短信

短信，或 SMS（短消息服务），已成为日常通信的主流。对于我们许多人来说，没有哪一天不发短信。这种最初只是一项 40 便士短信费的服务，现在已由大多数资费提供商作为无限服务。

Twilio 是一家云通信公司，它允许你仅需六行代码，就能从树莓派免费向手机发送短信。因此，当你工作时，你就不再需要被束缚在手机旁，而且可以专注于一个屏幕而不是两个屏幕了！

![](img/f16311c48f0c39ab87b1836be5339b9e_109_0.png)

通过这种方法，你可以让你的 Pi 在运行完脚本后发送短信

![](img/f16311c48f0c39ab87b1836be5339b9e_109_1.png)

## 语音、短信与 MMS

### API 凭据

要使用 Twilio API，你需要 `AccountSid` 和 `Auth Token`

#### ACCOUNT SID

#### AUTH TOKEN

准备好移除试用限制并享受完整功能了吗？
了解有关试用账户的更多信息

升级你的账户

### Sandbox 应用

### 开发者工具

### 测试你的应用

生成 Twilio API 的代码

调用 Sandbox 号

拨打电话

输入你的 Sandbox PIN 码

1 次呼叫

不需要 PIN 码

导出

发送消息

应用详情

在上方你可以在 Twilio 仪表板上找到你的 `AccountSid` 和 `Auth Token`

## 设置你的 Twilio 账户

此项目的第一步是注册 Twilio 账户和 Twilio 号。这是免费的，并将使你能够向注册并验证过的手机发送短信。一旦注册，你将通过短信向注册手机接收验证码。在提示时，将此代码输入 Twilio 网站以验证你的账户并访问 `twilio.com/try-twilio` 创建你的账户。

## 注册并验证手机号码

你的 Twilio 账户是一个试用账户（除非你升级付费），这意味着你只能从验证过的手机号码发送和接收通信。输入你想验证的手机号码，确保选择了正确的国家代码。Twilio 会给你一个验证码。将此代码输入网站表单并提交。

## 仪表板

注册并登录后，访问仪表板页面，它将显示你的 `AccountSid` 和 `Auth Token`。使用 Twilio REST 需要这两者。请保持它们的安全和隐私，但务必做好记录，因为你稍后编写 Python 程序时需要它们。

## REST

## 安装软件

REST 代表表象状态转换（有时写为 "`REST`"）。它依赖于无状态、客户端-服务器、可缓存的通信协议——在几乎所有情况下都是设计网络应用的 HTTP 协议架构风格。

04 启动你的树莓派并连接到。在安装 Twilio 软件之前，最好更新并升级你的 Pi。在 LX Terminal 中，输入 `sudo apt-get update`，然后输入 `sudo apt-get upgrade`。完成后，输入 `sudo easy-install twilio` 或 `sudo apt-get install twilio` 来安装软件。（如果你需要安装 pip，输入 `sudo apt-get install3-dev`，按回车，然后输入 `sudo pip install -U pip`。）

## Twilio 验证

05 现在你准备好创建一个发送短信到手机的程序了。打开你的 Python 编辑器并导入 Twilio REST 库（下方的第一行）。接下来替换你的 `AccountSid` 和 `Auth Token`，将 X 替换为在仪表板上找到的内容。

```python
from twilio.rest import TwilioRestClient

account_sid = "XXXXXXXXXXXXXXXXXXXXXX"

## 输入你自己的 X

auth_token = "XXXXXXXXXXXXXXXXXXXXXX"

## 输入你自己的 X

client = TwilioRestClient(account_sid, auth_token)
```

![](img/f16311c48f0c39ab87b1836be5339b9e_111_0.png)

图中所示的 Twilio 网站已被可口可乐、Uber 和 Nordstrom 等大公司使用

Twilio 提供了大量的 API 代码和参考文档来创建其他通信程序

## 发送消息

## 创建你的消息

现在发送你的消息。下面的代码不是必须的，但对于指示消息已发送很有用。添加这些行并保存你的程序。Pi 已连接到互联网且你的手机在线，然后运行你的程序。你刚刚从你的树莓派发送了短信。

你可能想更改同一个内容。在程序中创建一个名为 `message` 的新变量。这会提示你输入想要发送到手机的文本。当程序运行时，这就是将发送的消息：

```python
message = raw_input("Please enter your message")
```

```python
print_message.sid

print "Your message is being sent"

print "Check your phone!"
```

## 添加你的号码

## 其他 API 和代码

要发送消息，你需要添加下面的代码和两个号码。第一个号码是你的手机号码，经过 Twilio 验证的。第二个号码是你的 Twilio 号码，可以从你的仪表板获取。将 Sandbox 号更改为你的位置并记得添加国家代码。

Twilio 提供了广泛的 API 代码和参考文档来创建其他通信程序，如拨打电话、录音以及来者 ID 和时长。

```python
message = client.messages.create(to="+44YOURMOBILE",
from="+44YOURILIO", body=message)
```

![](img/f16311c48f0c39ab87b1836be5339b9e_112_0.png)

## 你可能需要的...

- 便携式扬声器
- python-espeak 模块
- Raspbian

## 语音合成器

将语音功能添加到你的树莓派项目中。我们展示了树莓派如何用于各种项目，但作为一个微型电脑，eSpeak 库对于任何想要使用它的人都是轻而易用的。还有一个模块允许你在 Python 中使用 eSpeak，这样你可以执行自动化任务。使用 eSpeak 可以控制说话的方式，让声音听起来不同。

## Pi 的第一个词

![](img/f16311c48f0c39ab87b1836be5339b9e_13_0.png)

02 eSpeak 库非常简单——在终端中让它说点什么：

```
$ espeak "[message]"
```

这将使用库的默认设置来读取任何输入的内容。虽然这个简单的命令很有趣，但还有更多可以做的……

## 说些更多

03 你可以更改 eSpeak 读取文本的方式，例如性别、读取速度，甚至它的发音音节。例如，命令如下：

```
$ espeak -f3150 "[message]"
```

...会让声音变成女性、大写字母并让阅读变慢。

## 你需要的一切

01 我们将安装此教程中计划使用的所有内容。包括 eSpeak 库和 Python 模块。打开终端并安装：

```
$ sudo apt-get install python-espeak-tk
```

![](img/f16311c48f0c39ab87b1836be5339b9e_113_1.png)

## 在 Python 中调用命令

## 完整代码列表

04 在 Python 中使用 espeak 的基本方法。导入它，然后使用：`subprocess.call("espeak", ["Option 1", "Option 2", "Option 3"], "Your message here")`

导入必要的 eSpeak 和 GUI 模块，以及获取时间的模块

```python
from espeak import espeak
from tkinter import *
from datetime import datetime
```

定义界面将使用的不同函数，包括简单的固定消息、时间和自定义消息

```python
def hello_world():
    espeak.synth("Hello World")
```
