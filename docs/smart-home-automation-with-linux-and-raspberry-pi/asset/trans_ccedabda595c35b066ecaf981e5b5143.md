
你可以据此判断，因为使用 POP3 意味着你不再会看到它们网页上的广告。但当它可用时，通常可以在服务的设置部分找到。所有主要公司都提供这项服务，尽管并非全部免费。

- Hotmail 默认提供 POP3 访问，无需手动开启；在多年仅通过订阅服务提供此功能后，现在 Hotmail 已免费提供。服务器目前位于 `pop3.live.com`。
- Google Mail 是第一个提供免费 POP3 电子邮件访问的服务，服务器为 `pop.gmail.com`。虽然现在大多数账户默认已启用，但一些较老的账户还没有。因此，你需要进入“设置”中的“转发和 POP/IMAP”。在这里，你可以为所有邮件或任何新收到的邮件启用它。
- Yahoo! 仅通过其 Yahoo! Plus 付费服务提供对其电子邮件的 POP3 访问和转发。在某些服务上（虽然不是 Yahoo!）有一种变通方法，你可以将所有邮件转发到另一个提供免费 POP 服务的服务（如 Hotmail 或 Gmail）！

以前，有一个项目可以直接处理 HTML 邮件，从而无需为 POP3 服务付费。其中包括现已关闭的 `http://httpmail.sourceforge.net`。幸运的是，这些措施已不再必要。一旦你知道了你的电子邮件所在的服务器，就可以下载它。这既可以在本地阅读，也可以用于备份，还可以用于处理邮件中发送的命令。虽然大多数电子邮件软件都可以处理 POP3 服务器，但我使用 getmail。

```sh
apt-get install getmail4
```

我将其配置为将每个电子邮件账户下载到单独的文件中。我将通过一个示例来演示，先从目录结构开始：

```sh
mkdir ~/.getmail
mkdir ~/externalmail
touch ~/externalmail/gmail.mbox
touch ~/externalmail/hotmail.mbox
touch ~/externalmail/yahoo.mbox
```

然后，为每个服务器创建一个单独的配置文件，名为 `~/.getmail/getmail.gmail`，内容如下：

```ini
[retriever]
type = SimplePOP3SSLRetriever
server = pop.gmail.com
username = my_email_address@gmail.com
password = my_password

[destination]
type = Mboxrd
path = ~/externalmail/gmail.mbox

[options]
verbose = 2
message_log = ~/.getmail/error.log
```

如果你希望将它们放入传统的 Linux 邮箱中，那么你可以将路径改为以下内容：

```sh
path = /var/mail/steev
```

然后，你可以像这样提取它们，并观察系统下载这些电子邮件：

```text
getmail -r getmail.gmail
```

有些服务，尤其是 Google Mail，不允许你在邮件很多时一次性下载所有邮件。因此，你需要重新调用该命令。这有助于减轻双方机器的带宽压力。

> **提示** 如果你只有一个外部电子邮件账户，那么将配置文件命名为 `getmailrc` 可以让你省略文件名参数。

然后，你可以在你选择的客户端中查看这些邮件。下面是一个示例：

```text
mutt -f ~/externalmail/gmail.mbox
```

请务必让 getmail 完成邮件的提取；否则，你的收件箱中会收到每封邮件的两份副本。

如果你打算像第 5 章中看到的那样使用 procmail 处理这些电子邮件，那么你需要将传入的电子邮件写入到 procmail 本身，而不是收件箱。这可以通过如下配置 destination 来完成：

```ini
[destination]
type = MDA_external
path = /usr/bin/procmail
unixfrom = True
```

## Twitter

Twitter 这一现象让普通大众变成了自封的微名人，因为他们采用了一种简单的广播通信机制，即一个人向众多“关注者”发送消息。虽然通信通常是公开的，但也可以创建用户列表，让同一家庭的成员私下相互关注。这可以通过在账户设置页面中选择“保护我的推文”来完成。

Twitter 比大多数社交网站做得更好的一点是，它没有偏离其最初的微博理念，也就是说，用于查询和控制信息流的 API 始终保持一致。这让你（或你的房子）可以轻松地将信息发到你的信息流中，或者让房子处理它们并据此采取某种行动。但无论如何，你都必须代表你的房子手动注册一个账户。过去几年中唯一的变化是要求使用 OAuth 来加强安全性。

### 使用 OAuth 发布推文

Twitter API 使用 HTTP 请求上传新推文，主要实现是通过 TwitterOAuth，该库来自 [https://github.com/abraham/twitteroauth](https://github.com/abraham/twitteroauth)。

```php
$auth = getTwitterDetails($user);
$connection = new TwitterOAuth($auth->ckey, $auth->csecret, $auth->oatoken, $auth->oasecret);
$content = $connection->get('account/verify_credentials');

$connection->post('statuses/update', array('status' => $all));
```

这个示例使用 PHP，但任何绑定 OAuth 的语言都以相同的方式工作。你只需要填写登录凭据，就可以从命令行发布推文。

$auth 结构正如它看起来的那样简单，通过如下代码从配置文件的内容中填充：

```
function getTwitterDetails($user) {
    $contents = @file("twitter.conf");

    $oauth = new OAuthDetails();
    $oauth->ckey = trim($contents[0]);
    $oauth->csecret = trim($contents[1]);
    $oauth->oatoken = trim($contents[2]);
    $oauth->oasecret = trim($contents[3]);

    return $oauth;
}
```

唯一的复杂之处在于获取这些 secret 和 token 的值。幸运的是，这是标准做法，如果你以前用过 OAuth，就不会有什么警报，也不会有什么意外。如果你没用过，请继续阅读……

有几种不同的方式可以访问 Twitter API，但就我们的目的而言，我们想要的解决方案被称为“只想从你自己的……访问 API”。这在 https://dev.twitter.com/docs/auth/application-only-authentication 中有说明。

在这里你可以创建一个 Twitter 应用程序，这是必要的，因为与 Twitter API 通信的是你的脚本（即应用程序），而不是用户。这将为你提供 consumer key 和 consumer secret，即 ckey 和 csecret。有了这些，你就可以通过其 API 与 Twitter 对话了。

为了能够代表用户发布或读取消息，用户需要通过你的应用程序向 Twitter 进行身份验证。这需要用户获取 oatoken 和 oasecret。创建应用程序密钥后，Twitter 网页上有一个名为“Your Access Token”的模块，它提供了一键获取这些数据的方法。将其添加到配置文件中，以便 getTwitterDetails 可以解析它，现在你就可以以编程方式发送推文了。

### 使用 OAuth 阅读推文

与通过简单的 HTTP 请求发布推文一样，推文也可以被读取。文档中包含用于获取你的时间线、好友时间线以及转发等详细信息的 URL。这些调用会返回有关所选推文的所有可用信息，包括发布者的完整信息（如姓名、头像和关注者数量）、消息内容以及回复数据（包括状态、用户和屏幕名称）。这通常比你需要的要多，但在 API 设计中，尽可能不丢失信息是一个好主意——过滤掉比重新加回来更容易。你可以使用这段代码在离线时跟踪推文：让计算机拦截格式合适的推文，并通过 SMS 传输代码将其转发出去。我们在第 2 章中看到了一个这样的应用：自动喂狗器。

### 使用 RSS 阅读推文

Twitter 的本质非常契合现有的 RSS 技术，因此无需自定义解析器。用户 @apress 的 URL 如下所示：

https://api.twitter.com/1/statuses/user_timeline.rss?screen_name=apress
