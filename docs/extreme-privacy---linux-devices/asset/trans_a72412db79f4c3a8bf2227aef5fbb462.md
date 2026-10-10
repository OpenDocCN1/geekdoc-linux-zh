
在左侧菜单中点击“Voice”、“Settings”和“General”。
-   禁用“Request Inspector”并点击“Save”。

所有这些日志记录看起来可能过于侵入。确实如此，但这并非 Twilio 独有。Twilio 所做的与其他电信提供商（包括蜂窝和固定电话公司）并无二致。我们可以在一定程度上控制数据的存储方式，但我不想在此制造不切实际的期望。虽然 Twilio 看起来可能已经删除了您的通话日志、语音邮件、短信和转录记录，但这些数据很可能仍以其系统内的某种形式存在。我们唯一的目标是从仪表板中移除数据。对于传统的电话通话和短信，不要指望有任何隐私保障。VoIP 服务绝不应用于敏感通信。请假设所有记录都会被永久存储。

## Telnx VoIP 服务

在过去的文章中，我强烈推荐过一款名为 Telnx 的 Twilio 替代方案。当时，他们对新账号的限制较少，并鼓励人们尝试其服务。如今，我建议在继续之前务必谨慎。这是由于以下几个问题。

-   Telnx 仅向已确认的企业提供账号。不过，您的新自定义域名邮箱地址可能就足够了。
-   Telnx 不再提供实质性的客户支持。支持工单只能收到模板回复，最终在未解决问题的情况下被关闭。拨打其支持热线只会被告知发送邮件，而这些邮件从未得到回复。如有需要，您必须自行进行故障排查。
-   Telnx 不提供语音邮件服务。
-   Telnx 不允许像 Twilio 那样从系统中删除用户日志或短信。
-   如果其自动欺诈系统检测到异常活动，Telnx 会暂停付费账号。我曾亲身经历过这种情况，当一个闲置账号在他们看来显得可疑时，账号就被暂停了。当我询问此做法时，我并未得到回应。

然而，我知道有些人更喜欢 Telnx 而非 Twilio。他们的月度号码费用稍低，而且冗余总是好事。如果 Twilio 教程未能产生您期望的使用效果（可能是由于账号被暂停），您可以考虑 Telnx（[https://refer.telnx.com/refer/zrfmo](https://refer.telnx.com/refer/zrfmo)）。这家 VoIP 提供商复制了 Twilio 提供的服务，但其设置过程更简单。既然您现在已经了解了 Twilio，我将在此简要介绍 Telnx 的步骤。

-   在 [https://refer.telnx.com/refer/zrfmo](https://refer.telnx.com/refer/zrfmo) 创建一个免费账号。此特定网址提供 20 美元的免费额度，可立即使用。
-   提供之前解释过的自定义域名邮箱地址。
-   如果被询问用途，请选择“SIP Trunking”。

现在您应该已经登录到 Telnx 门户。您可以创建第一个连接并购买电话号码。

-   从侧边菜单点击“Voice”然后“SIP Trunking”。
-   点击“+ Add SIP Connection”按钮。
-   输入您希望为连接起的名称（我选择了“VoIP”）。
-   点击“Create Sip Connection”。
-   启用“Credentials”作为“Connection Type”。
-   复制自动生成的用户名和密码。
-   点击“Save and finish editing”。
-   点击“Numbers”、“My Numbers”和“Search & Buy Numbers”。
-   输入位置并点击“Search Numbers”。
-   选择一个号码并点击“Add to Cart”。
-   点击右上角的“Cart”。
-   在“Connection or Application”下，选择您的连接（我之前的连接名为“VoIP”）。
-   使用您的免费额度点击“Place Order”购买号码。
-   点击“Voice”、“Outbound Voice Profiles”然后“Add new profile”。
-   提供名称“outgoingvoice”并点击“Create”。
-   点击“Outbound Voice Profiles”然后“outgoingvoice”旁边的“Edit”图标。
-   选择您的连接（VoIP）并点击“Add Connection/Apps to Profile”。
-   点击“Voice”、“Sip Trunking”、“SIP Connections”然后连接右侧的“Outbound Options”。
-   在“Caller ID Override”中输入您的新电话号码，然后点击“Save”。

## Telnx Linphone 配置

-   启动 Linphone 并点击“Home”按钮。
-   选择 Account Assistant。
-   选择“Use A SIP Account”。
-   输入 Telnx 提供的登录名作为“Username”。
-   输入您的电话号码作为“Display Name”，例如“2025551212”。
-   将“SIP Domain”输入为“sip.telnx.com”。
-   输入 Telnx 提供的登录凭证的“Password”。
-   将“Transport”更改为“TLS”。如果失败，请尝试“UDP”或“TCP”。

现在，您的 Linphone 应用可以在不添加资金的情况下进行和接收电话。这是 Telnx 独有的。如果您希望承诺将 Telnx 作为您的 VoIP 提供商，请务必向您的账号添加 20 美元的新资金，以防止试用期终止。这提供了足够的额度（40 美元），可以为单个号码和用量提供超过三年的 VoIP 服务。

Telnx 不向其 Web 门户或另一个号码提供原生短信转发。唯一的选项是像我们对 Twilio 做的那样，自行托管一个转发器到电子邮件地址。如果您有自己的域名和共享网络托管，请创建一个标题为 telnx.php 的文本文件，内容如下。将“your@email.com”更改为您希望接收通知的地址。将“@yourdomain.com”更改为您的实际域名。

```php
<?php
$to = "your@email.com";
$subject = "Text Message from {$_REQUEST['From']} to {$_REQUEST['To']}";
$message = "{$_REQUEST['Body']}";
$headers = "From: telnx@yourdomain.com ";
mail($to, $subject, $message, $headers);
```

将文件上传到您的网络托管。之后，您的特定 URL 可能类似于 [https://yourdomain.com/telnx.php](https://yourdomain.com/telnx.php)。在 Telnx 内部，请执行以下操作。

-   点击“Messaging”、“Programmable Messaging”然后“Add New Profile”。
-   提供名称“sms”并选择“Twilio API”。
-   在两个“webhook”字段中，输入之前创建的 PHP 文件的 URL。
-   点击“Save”。
-   在左侧菜单中点击“Numbers”然后“My Numbers”。
-   在您的号码条目中，在“Messaging profile”字段中选择“sms”。
-   如果被提示，请确认费率通知。

传入的短信现在应该会被转发到您的电子邮件地址。主题将标识发送者和接收者，而消息正文将显示短信内容。这种方法防止了 Telnx 像 Twilio 那样在其自己的服务器上存储您所有传入消息（内容），但他们仍然维护永久日志。他们仍然有能力拦截并查看内容，但这种情况不太可能。一旦消息路由到您的电子邮件，您应该是内容的唯一宿主（但不是日志的宿主）。

如果您想从新的 Telnx 号码发送短信，请依次点击“Messaging” > “Programmable Messaging” > “Learn & Build” > “Send & Receive a Message”。您可以使用在线表单向任何号码发送 SMS 短信。您也可以使用该页面提供的命令在终端中发送消息。与 Twilio 类似，我不使用此功能。我从不使用 VoIP 号码进行来回对话。我只需要接收偶尔的确认短信，这些短信由两家提供商转发到我的电子邮件。

您可以在 Telnx 门户中自定义传出电话期间显示的来电显示名称。从菜单中点击“Numbers” | “My Numbers”，然后在下拉菜单中选择“Caller ID/CNAM Listing”服务区域。启用“CNAM Listing”和“Caller ID Name”选项，然后输入任何期望的名称。可能需要一周时间才能生效。请务必通过“Security”部分的“My Account”启用双因素身份验证（2FA）。

虽然这种配置比 Twilio 简单，但功能较少。然而，也有 Twilio 不具备的优势。请考虑以下方面。

-   在使用 Twilio 时，未接通的电话直接转入语音邮件，消息被转录并发送给我。而在 Telnx，未接通的电话会在大约 30 秒后断开连接。有一个语音邮件选项，但需要付费的第三方服务。如果您需要语音邮件和转录功能，Twilio 是最佳选择。
-   Twilio 允许传入的短信原生直接投递到您的仪表板或转发到任何其他号码。Telnx 要求您自行托管消息转发服务器才能实现此功能。如果您需要号码支持传入 SMS 文本而不依赖第三方服务，那么 Twilio 是合适的选择。如果您有自己的网站，复制此过程相当简单。
-   Twilio 拥有许多欺诈触发机制，可能会影响我们的使用。许多读者报告仅仅创建账号并允许访问都遇到了困难。Telnx 在注册“企业”邮箱地址时提供即时访问。然而，我目睹过 Telnx 暂停使用 VPN 后通过免费电子邮件域名创建的账号。始终提供一个与自定义域名关联的电子邮件地址，并在连接到公共 Wi-Fi 时操作，以获得获得新账号的最高几率。由于您将使用此服务进行与真实姓名相关的电话通话和接收，我很少看到使用别名注册的充分理由。
-   Telnx 和 Twilio 的定价和整体通话质量几乎相同。

我目前通过这两种服务维护号码，并将每个都配置到 Linphone 中。如果我被迫只依赖一种服务，我会选择 Twilio，因为其语音邮件记录、清理选项和整体稳定性。如果您有一个 Telnx 账号并且它适合您，那很好。然而，我鼓励其他人将精力集中在 Twilio 上。我目前通过 Twilio 维护多个号码，并将每个都配置到 Linphone 中。传入的 SMS 文本消息通过我的网站转发到我的电子邮件账号。
