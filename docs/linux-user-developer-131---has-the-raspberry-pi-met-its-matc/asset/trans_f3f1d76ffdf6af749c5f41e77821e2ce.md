

## 教程：制作一个 Python Twitter 客户端

使用 Twitter 开发者账户工具创建你自己的应用详情，无论是用于个人使用还是计划发布的应用。通过 Python 封装库访问整个 Twitter 数据集，从而获取时间线、列表和用户资料等。创建用户和 OAuth 的认证密钥，让你能够接入 Twitter API。使用 Twython 模块编写自己的推文，以访问 Twitter API 的各个组件。

使用 Python 库学习 Twitter API 的基础知识，并创建一个简单的 Twitter 客户端来发布和监控推文。

**导师**
Rob Zwetsloot 擅长建模复杂系统，是一位精通 Python、Django 和 PHP 的 Web 开发者。他喜欢进行计算实验。

![](img/dd9251551a61a36067892b1cc68615b0_65_0.png)

Python 有很多优点，其中之一就是你可以用它来创建轻量级的桌面软件和物联网软件包。用于此目的的服务之一是 Twitter，它有几个你可以利用的 Python API，可以在 Python 脚本中检查和发布指定用户的推文。

由此，你可以在命令行中创建一个标准的 Twitter 客户端，或者使用 Tkinter（来自 LUD 之前的问题）为其制作一个 UI。你还可以指定通常从客户端请求的登录详情，然后使用它来检查 Twitter 上的特定单词、转发、接收的消息，或者查看特定的人是否在发送推文。

在这个教程中，我们将使用 Twython，它提供了 Python 的纯 Twitter 接口，并展示如何获取你自己独特的 API 密钥，以便与 Twitter 本身一起使用。

### 资源
- 一个 Twitter 账户
- Python 2: www.python.org/

![](img/dd9251551a61a36067892b1cc68615b0_65_1.png)

### 01 账户权限
要创建一个 Twitter 应用，你需要一个 Twitter 账户。登录你的账户，或者如果你想在该服务中拆分个人和开发账户，请创建一个单独的账户。完成后，前往 dev.twitter.com 并使用你想要的账户登录。

![](img/dd9251551a61a36067892b1cc68615b0_66_0.png)

![](img/dd9251551a61a36067892b1cc68615b0_66_1.png)

![](img/dd9251551a61a36067892b1cc68615b0_66_2.png)

![](img/dd9251551a61a36067892b1cc68615b0_66_3.png)

### 02 新的开始
前往“我的应用程序”并点击“创建新应用程序”。在这里，你需要输入应用程序的名称、简短描述以及一个可以了解你和/或该应用程序更多详情的网站。应用程序名称不允许使用“Twitter”一词。

![](img/dd9251551a61a36067892b1cc68615b0_66_4.png)

### 03 权限
创建完成后，你会被带到该应用程序的详情页。在我们继续之前，点击“设置”并在“应用程序类型”下选择“读取、写入和访问直接消息”，以便我们可以将其作为 Twitter 客户端正确使用。

### 04 访问令牌
我们现在可以为该应用程序创建一个访问令牌，使其能够与你的 Twitter 账户配合使用。一旦读取和写入权限更改完成后，返回详情页，滚动到底部。点击“创建我的访问令牌”以获取它。

### 05 安装 Pip
我们将从我们的网站安装最新版本的 python-twitter。为此，首先安装 pip，因为我们使用 Python，在软件源中可用为 python-pip。由于我们使用的是 Debian，命令如下：

```bash
sudo apt-get install python-pip
```

……这将允许我们设置 Python 模块。

![](img/dd9251551a61a36067892b1cc68615b0_66_5.png)

### 06 安装 Twython
既然我们已经安装了 Pip，我们可以继续安装 Twython。为此，在终端中继续并输入：

```bash
sudo pip install twython
```

这将获取 Twython 模块以及你登录账户所需的所有 OAuth 包，使用我们之前创建的令牌。

![](img/dd9251551a61a36067892b1cc68615b0_66_6.png)

### 07 认证文件
我们需要创建一个 Python 文件来保存所有的认证详情。启动 IDLE 或你选择的文本编辑器，首先通过以下方式导入 Twython：

```python
from twython import Twython
```

确保手头有我们之前创建的密钥，以便在下一部分中添加。如果输出较长，请按回车键转到下一个屏幕。

![](img/dd9251551a61a36067892b1cc68615b0_66_7.png)

### 08 应用密钥
将以下内容添加到你的代码中：

```python
APP_KEY = 'YOUR_CONSUMER_KEY'
APP_SECRET = 'YOUR_CONSUMER_SECRET'
```

……分别用你自己的消费者密钥（consumer key）和消费者机密（consumer secret）替换 YOUR_APP_KEY 和 YOUR_APP_SECRET。

### 09 访问密钥
现在我们可以将之前创建的访问令牌添加到脚本中：

```python
OAUTH_TOKEN = 'YOUR_ACCESS_TOKEN'
OAUTH_TOKEN_SECRET = 'YOUR_ACCESS_TOKEN_SECRET'
```

……同样，你需要用相应的数字替换 YOUR_ACCESS_TOKEN 和 YOUR_ACCESS_SECRET。

### 10 验证
现在是时候验证你到目前为止所做的工作是否真的有效了。在脚本的底部输入以下内容：

```python
twitter = Twython(APP_KEY, APP_SECRET, OAUTH_TOKEN, OAUTH_TOKEN_SECRET)
twitter.verify_credentials()
```

然后运行。如果没有出现任何错误，说明一切工作正常。

### 11 测试发布
既然一切似乎都在正常工作，你可以尝试直接向 Twitter 发送一条测试推文。在我们的代码底部，输入：

```python
twitter.update_status(status="Test")
```

然后再次运行。如果成功，将不会有错误，并且它会显示在你的时间线上。

### 12 撰写帖子
让我们创建一种通过脚本向你的时间线发布推文的方法。我们将使用人工输入，如下所示：

```python
post = raw_input("Write your tweet: ")
```

……这将把我们的推文以字符串形式存储在 `post` 中。

要发布此内容，我们使用之前的 `update_status` 部分，只是现在它使用 `post` 中的字符串来更新我们的时间线。添加：

```python
twitter.update_status(status=post)
```

然后保存文件。运行它，并再次测试代码。

### 13 更新
编写帖子的完整脚本结构如下所示：

```python
APP_KEY = 'YOUR_CONSUMER_KEY'
APP_SECRET = 'YOUR_CONSUMER_SECRET'
OAUTH_TOKEN = 'YOUR_ACCESS_TOKEN'
OAUTH_TOKEN_SECRET = 'YOUR_ACCESS_TOKEN_SECRET'

from twython import Twython
twitter = Twython(APP_KEY, APP_SECRET, OAUTH_TOKEN, OAUTH_TOKEN_SECRET)

post = raw_input("Write your tweet: ")
if twitter.update_status(status=post):
    print("Tweet sent!")
```

### 14 时间线
要访问我们账户推文的时间线，我们使用以下内容：

```python
twitter.get_user_timeline()
```

这会访问我们账户发布的过去 20 条帖子。你还可以通过添加 `screen_name` 选项来指定要检查的时间线：

```python
twitter.get_user_timeline(screen_name='username')
```

### 15 完整时间线
我们可以通过使用 `get_home_timeline` 函数来访问账户的完整时间线，如下所示：

```python
twitter.get_home_timeline()
```

如果你打印出来，它将显示时间线上最近 20 条推文的所有未经过滤的数据。你可以通过向 `get_home_timeline` 添加 `count` 参数来修改推文数量。

```python
twitter.get_home_timeline(count = 5)
```

我们需要解析数据，以确保我们获得连贯且可识别的时间线。

> “创建一种简单的方法，将推文发布到你的时间线上”

### 16 搜索推文
我们可以使用以下内容在 Twitter 上搜索特定关键字：

```python
twitter.search(q="linux")
```

这将返回与单词 Linux 相关的推文混合结果。你可以使用 `result_type` 参数进行过滤，将其设置为混合（mixed）、最新（recent）或热门（popular）。

### 17 关注
要在 Twitter 上关注某人，我们使用 `create_friendship` 函数。我们需要你想关注的 Twitter 用户的屏幕名称或数字 ID – 你很可能使用屏幕名称，所以我们要这样写：

```python
twitter.create_friendship(screen_name = "LinuxUserMag")
```

### 18 转发
由于转发是 Twitter 的重要组成部分，其功能仅仅是 `retweet`。我们需要推文 ID 用于此，这是用于每个推文的数字字符串，并显示在推文的 URL 中。我们使用以下方式：

```python
twitter.retweet(id = '12345')
```

### 19 收藏
这的工作方式与转发非常相似，使用 URL 中使用的推文唯一 ID 来确定要收藏哪条推文。此功能的函数是 `create_favorite`，写法如下：

```python
twitter.create_favorite(id = '12345')
```

在进行此操作时，请确保使用美式拼写（favourite，尽管这里代码中可能是 favorite，需注意原文语境，原文用了 favourite，但代码标准通常是 favorite，此处保留原文翻译意图，即美式拼写注记，实际上 Twitter API 参数是 favorite，原文提示“American spelling”可能指代码层面，但中文翻译保留原意即可）。

*更正/精炼第 19 点最后句翻译：*
在这里，请确保使用美式拼写（favorite）。（注：原文说 "Make sure to use the American spelling (favourite)" 其实有点矛盾，因为 American spelling 通常是 favorite，而 British 是 favourite。原文括号里写的是 favourite，但文字说是 American spelling。考虑到 API 参数实际上是 `create_favorite`，这里翻译时保留原文的逻辑：请确保使用美式拼写。）

### 20 获取收藏
Twitter 会存储用户的所有收藏，以便你随时可以恢复它们。你可以获取自己的，或者指定用户以获取其收藏。基本代码是：

```python
twitter.get_favorites()
```

……这将获取你自己的收藏。像以前一样，你可以分别使用 `user_id` 和 `screen_name` 指定用户 ID 号码或屏幕名称，以获取特定列表。

### 21 提及
你还可以访问已认证账户的提及列表。为此，使用 `get_mentions_timeline` 函数。它像其他时间线一样工作，允许你限制从选择中获取的帖子数量。像之前一样将其限制为五个：

```python
twitter.get_mentions_timeline(count='5')
```

### 22 热门话题
得益于 Twitter 的热门话题，每个人都知道其他人在谈论什么，无论是年轻的加拿大音乐家还是重要的世界事件。你通过以下方式访问趋势：

```python
twitter.get_place_trends(id = '1')
```

ID 为 1 返回全球趋势。你可以为不同的地区指定不同的 ID。

### 23 获取列表
如果你更喜欢通过策划人员列表来使用 Twitter，你可以使用 `get_list_statuses` 函数获取任何列表的内容：

```python
twitter.get_list_statuses(id = '12345')
```

每个列表都有一个你可以使用的唯一 ID 或标识符（slug）。你还可以调用任何列表的成员，或任何订阅该列表的人。

![](img/dd9251551a61a36067892b1cc68615b0_68_0.png)

### 24 结尾
使用所有这些函数，你可以开始选择数据并让我们的代码做很多事情，而不仅仅是发布推文。从时间线函数中获取特定属性将允许你显示一个连贯的时间线，并且还包括关注用户及其链接所需的详细信息。

