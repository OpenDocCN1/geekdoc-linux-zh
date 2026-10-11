

## 使用 Python 访问 Twitter

Twitter 可以成为极佳的沟通渠道，让你的树莓派项目与世界对话。

![](img/e7f197876caa0b235fb5da2d16a578ea_77_0.png)

**乔伊·伯纳德** 是一位真正的通才，他将时间分配在家具制作、协助研究人员解决科学计算问题以及编写 Android 应用上。

### 为什么选择 Python？

它是树莓派的官方编程语言。请阅读位于 python.org/doc 的文档。

> 在上一期中，我们探讨了如何将树莓派变成一个 RSS 阅读器，以及如何让你的树莓派发布 RSS 源供他人阅读。

在本期中，我们将沿着同样的思路，看看如何添加功能，使你的树莓派能够发布推文，让全世界都能关注正在发生的事情。

第一步是找到一种与 Twitter 通信的方式。Twitter 提供了完整的 API，定义了你如何发送和阅读推文。我们可以使用原始套接字；手动构建和发送消息，然后处理返回的结果。

然而，这完全违背了 Python 的核心要点和代码复用的前提。相反，我们将使用模块 python-twitter。还有其他几种选择可用，如果你希望寻找一个使用不同代码风格且更契合你个人风格的模块。它们应该都具有相同的功能，因此请随意探索和实验。对于这些示例，你可以使用 `pip install python-twitter` 安装该模块。这对 Python 2.x 运行良好，但 Python 3 的支持正在开发中，因此如果你想使用 Python 3，可能需要选择一个不同的模块。

如果你需要最新的功能，你可以随时从 GitHub 获取源代码并构建它。

安装好模块后，你可以在代码中使用 `import twitter` 导入它。类 `twitter.API` 提供了主要接口，使你能够与 Twitter API 进行交互。当你创建该类的新实例时，需要提供你的凭据以进行身份验证，从而被允许操作你的账户。Twitter 现在主要使用 OAuth 来处理身份验证，这意味着你需要生成一个访问令牌，以便你的代码可以借此在 Twitter 上识别自己。其开发者文档中有一个专门章节涵盖了获取令牌所需的步骤，位于 goo.gl/99oAfA。第一步是，你需要将你的代码注册为被授权与 Twitter 通信的应用程序。

你通过前往 apps.twitter.com 并创建一个新的应用来处理此事。这将为你提供消费者密钥（consumer key）和消费者秘密（consumer secret），以标识你的代码被允许连接到 Twitter。第二步是，为你的账户创建一个身份验证令牌，这将告知 Twitter 该应用被授权连接到你的账户、读取并发布内容。最终你会得到两组独立的密钥和秘密，现在你可以用它们来创建 API 类的实例。代码看起来像这样：

```python
import twitter
api = twitter.API(consumer_key="consumer_key",
                  consumer_secret="consumer_secret",
                  access_token="access_token",
                  access_token_secret="access_token_secret")
```

...其中相关的密钥和秘密就是你上面生成的那些。你可以通过调用函数 `api.VerifyCredentials()` 来检查你的凭据是否有效。这将给你一个错误或提供一个账户信息的详细分解。

一旦你拥有了已认证的 Twitter 连接，你的树莓派项目就可以开始与广阔的世界对话了。最基本的方法是 `PostUpdate()`。使用这个函数，你可以发送状态更新消息，最多 140 个字符。如果你的消息长于此，你可以使用函数 `PostUpdates()`，它将发布多个状态更新，直到整个消息被发布完毕。

如果需要，你可以在消息中包含其他详细信息。这包括选项，如你当前的经度和纬度，或地点 ID，以识别特定更新的来源。这在某种移动监测项目中可能很有用，当你想知道某个特定更新的来源时。你还可以通过在函数调用中包含 `in_reply_to_status_id=` 选项，将更新作为对其他消息的回复来发布。

如果你不想使用公开状态更新来发送你的消息，你可以使用函数 `PostDirectMessage()` 向特定账户发送文本消息。你可以使用 `user_id` 或 `screen_name` 来识别你的直接消息的接收者。虽然这比公开更新稍微私密一些，但绝非安全，因此不要使用此方法发送任何敏感信息。

如果需要，你还可以将多媒体文件作为 Twitter 更新发送。函数 `PostMedia()` 可以接受本地文件名或 HTTP URL 来执行多媒体推文。你可以发送 JPEG、GIF 或 PNG 等图像文件。你还可以为推文包含相关的文本消息，以及位置信息，如果你想要对推文和图片进行地理定位的话。

一旦你完成这些发布功能中的任何一个，你将获得一个返回的状态对象，其中包含你状态的信息。有两打元素提供项目，例如是否已收藏、创建时间以及相关的标签。

Twitter API 还允许你阅读来自其他用户的更新和直接消息。这意味着你可以使用相同的通信渠道向你的树莓派项目发送命令。

函数 `GetDirectMessages()` 可以获取发送到你树莓派 Twitter 账户的最后 20 条直接消息。幸运的是，你不必每次都这样做。你可以使用选项 `since_id=x` 告诉 Twitter 仅发送比消息 ID x 更新的那些直接消息。

如果你只感兴趣于获取最后 Y 条消息，你可以转而使用选项 `count=Y`。此函数返回 DirectMessage 对象实例的序列。此结构包含消息 ID、创建日期、接收者和发送者信息，以及实际消息的文本。这样，你可以将命令放在文本消息中，使你的项目在被部署后能够执行不同的任务。

根据我们在这里的示例，你应该能够使你的项目发布世界上正在发生的事情的推文。

### 管理交互

![](img/e7f197876caa0b235fb5da2d16a578ea_78_0.png)

你可能希望对你的树莓派项目的 Twitter 账户进行更复杂的控制。Twitter Python 模块提供了对 Twitter API 的完整访问，因此你可以更改此账户与其他 Twitter 用户之间的关系。

- 你可以使用函数 `CreateFriendship()` 关注另一个用户。
- 如果你改变主意，你可以随时使用函数 `DestroyFriendship()` 取消关注某个用户。

然而，更有趣的是检查有多少人正在关注你。或者更具体地说，有多少人正在关注你的树莓派项目。你可以使用函数 `GetFollowers()` 获取关注你项目的 Twitter 用户序列。默认返回的关注者最大数量为 200。因此，如果你的项目变得非常流行，你需要使用函数 `GetFollowersPaged()` 以每 200 个为一组获取所有关注者。你可以使用选项 `cursor=X` 来控制返回的页面。默认情况下还返回所有这些用户的状态，这可能不是你必须处理的。如果是这样，你可以使用选项 `skip_status=true`。

你还可以使用函数 `GetFriends()` 获取你结交朋友的次数（即好友数量）。在这种情况下，默认返回的结果数量为 20。你可以使用选项 `count=X` 将其增加到最多 200。如果你有超过 200 个朋友，你也可以在这里获取分页结果。你可以使用 `cursor` 选项来控制返回结果的页面，如上所述。

如果你想更广泛地了解谁在关注你的项目，你可以使用函数 `GetMentions()` 查看谁提到了你项目的用户账户。默认情况下你会获得最后 20 次提及，但你可以请求最多 200 次。

衡量你公共领域影响力的另一个指标是你获得的转推数量。你可以通过使用函数 `GetRetweetsOfMe()` 来找出。默认返回的数量是 20，但你可以请求最新的 100 条转推。

借助这些额外功能，你可以实际上让你的树莓派项目与一般世界互动，并监控其自身的公众沟通能力。这对于公民科学项目可能很有用。

### 完整代码列表

```python
import twitter

# The first step is to connect to Twitter
api = twitter.Api(consumer_key='consumer_key',
                  consumer_secret='consumer_secret',
                  access_token='access_token',
                  access_token_secret='access_token_secret')

# You can post status updates
update_status = api.PostUpdate('I am now connected!')

# You can geotag updates with lat/long
update_status = api.PostUpdate('I am here: ', latitude=45.949874,
                               longitude=-66.642347)

# Posting images taken from your RP1
update_status = api.PostMedia('This is my picture', 'image1.png')

# Get the last 10 mentions and retweets
mentions = api.GetMentions(count=10)
retweets = api.GetRetweetsOfMe(count=10)

# Finding out how many followers you have
followers = api.GetFollowers()
follower_cnt = len(followers)
```

![](img/e7f197876caa0b235fb5da2d16a578ea_78_1.png)

*上方* 建议为你的项目专门设置一个新的 Twitter 账户

