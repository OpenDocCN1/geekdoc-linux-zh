
6. 确保此日历已勾选或切换显示事件。

7. 如果没看到 Mailcow 日历，返回 `DAVx` 应用，找到你的账户并确保日历同步已启用。

你应该能在 Mailcow 日历中看到刚刚创建的事件。如果没有看到，你可能忘记正确配置 `DAVx` 以使其立即同步。或者你没用 VPN。或者你只是配置乱了；不要放弃。

### 7.3 在 Mailkow 中添加事件并在 Android 上验证

1. 在 Mailkow Web 界面中，进入 `Calendar`（日历）部分。

2. 找到添加新事件的选项（通常是“+”或 `New Event` 按钮）。

3. 创建一个具有唯一名称的事件（例如，“Test Mailkow to Sync”）。

4. 设置日期、时间和其他细节。

5. 保存事件。

6. 在你的 Android 手机上，打开 `Fossify Calendar` 应用。

7. 向下滑或点击刷新。

8. 新事件应该出现在你的日历视图中。

9. 假的

### 7.4 刷新日历数据不是假的

直接在 `Fossify Calendar` 应用中刷新并不会立即显示服务器上的新事件。要进行立即更新：

1. 在 Android 手机上打开 `DAVx`。

2. 点击 `Refresh`（刷新），然后点击 `Synchronize Now`（立即同步）按钮。

3. 点击此强制与你的 Mailcow 服务器同步。

4. `DAVx` 同完成后，打开 `Fossify Calendar` 应用。

5. 你的日历现在应该显示最新的信息了。

你可能会奇怪，为什么日历有一个同步选项“Refresh CalDAV”，但它并没有刷新你的日历。欢迎来到开源软件的美妙世界：我希望你远离它。我们在功能性 UI 上的缺陷，通过不将你的数据卖给追踪者和赏金猎人（https://docs.fcc.gov/public/attachments/FCC-24-40A2.pdf）来弥补。这是值得的……某种程度上。

当你点击“Refresh CALDAV Calendars”时，你实际上是在要求日历应用检查 `CALDAV` 中是否有变化。你并没有告诉 `CALDAV` 同步你的服务器以获取新条目。

工作原理如下：

1. Mailkow 服务器 — `CALDAV`（Mailkow 每 15 分钟发送更新）

2. `CALDAV` — 日历应用（日历应用从 `CALDAV` 获取数据）

除非手动请求，否则日历不会立即刷新。

99% 的这类大型邮件服务器接收来自家庭宽带连接的邮件，它们来自那些被黑客攻击、现在正不知情地向互联网的一大部分发送垃圾邮件的人。我们为了摆脱……而交易了自由。

无论你认为这是否免费。如果你想让邮件送达目标收件人，你需要一个 SMTP 继发。

`SMTP` 通过你 Postmark 的服务器发送你的邮件。使用 Postmark，icoud/gmail 将让你的邮件通过发送，而不是让某个运行着 Windows 服务程序包 1、并将你的银行密码写在便利签贴在显示器上的笨蛋成为垃圾邮件机器人的一部分。

做生意的关键在于**你**。你正在为发送电子邮件的能力支付过路费。但 Postmark 的都是人，所以你会享受其中。我希望你不会因为他们去纽约市竞争（[https://www.youtube.com/watch?v=qFVWcFHKSE&list=PlkbVsAIWN2vRiOz6haEJ26Ho&index=2））而取消我的服务。抱歉，postmark；这是计划之中的：

## 步骤 1：将 Postmark 设置为 SMTP 继发

### 1. 创建 Postmark 账户

- 访问：[postmarkapp.com](https://postmarkapp.com)

- 注册：点击页面右上角的“Free trial”（免费试用）。

- 这是一项服务，你无论如何都得付钱。如果你不想处理忘记注册过试用的问题，请使用 [privacy.com](https://privacy.com) 创建一个授权金额为 $0 的信用卡，然后在将其输入 Postmark 的一刻立即将其删除。但如果你选择自托管邮件路线，你将是需要付钱的；请记住这一点。

- 完成注册：输入所需的详情（电子邮件、密码等），并通过通过邮件验证确认你的账户。

与 Postmark 沟通；他们需要知道你不是垃圾邮件发送者。

- Postmark 不会在不先请你吃一顿饭的情况下就让你发送邮件。你需要了解他们，他们也需要了解你。并不是**任何人**都能直接使用。

- 他们需要一天或几天时间来验证你不是已已的垃圾邮件发送者/诈骗者。如果他们没有快速回复你，可能需要联系客服，但通常是因为 Postmark 被垃圾邮件示例淹没了。

- 他们可能会向你询问你的信息。这是正常的；没有信誉良好的 SMTP 继发器想要负责协助发送垃圾邮件！

这可能会有些不便

如果你勾选了这三个框，你很可能是一个垃圾邮件发送者，并且导致了困扰、恼火和烦躁体验增加：

1. 使用模板

2. 包含图片

3. 有“UNSUBSCRIBE”（退订）按钮

如果是这样，去洗吧。

### 1.2 创建新服务器

- 导航到 **Servers**（服务器）页面：

- 登录后，访问 `https://account.postmarkapp.com/servers` 或在导航栏中找到“Servers”标签页。

- 创建新服务器：

- 点击“Servers”页面上的 **Create Server**（创建服务器）按钮。

- **Name your server（为你的服务器命名）：** 为你的 SMTP 继发服务器输入一个名称。

- 点击 **Save**（保存）创建服务器。

### 1.3 配置流（Streams）

- 点击它的名称导航到你刚刚设置的服务器。

- 从显示的流中选择 **Default stream**（默认流）。

- 注意：**Transactional**（事务型）用于低频率但旨在快速发送给单个用户的消息，**broadcast**（广播型）用于发送给大量用户的消息（即垃圾邮件）。

### 1.4 获取 SMTP 凭据

- 点击你的流后，导航到 **Setup Instructions**（设置说明）页面。

- 如果忘记了如何操作，点击 **Servers** → **Default stream** → **Setup Instructions**。

- 配置好出口流后，进入 **Transactional Stream**（事务流）的 **Setup Instructions** 页面。

- 你会被大量的选项淹没——选择库——无需担心，我们选择了 SMTP。

**SMTP 详情：**

- Server（服务器）：`smtp.postmarkapp.com`

- Ports（端口）：25、252 或 587。我们将使用带有 TLS 的 587 端口。你不需要在这里选择或配置任何内容；这是一个显示你稍后要输入 Mailcow 的凭据页面。请安全地保存它们。

- Authentication（身份验证）：Postmark 支持纯文本（Plain Text）、CRM 或 TLS。

- Username（用户名）：这是你的 Postmark 服务器令牌。它看起来像一长串字符（例如 `17883dd83-9917-46e1-b39a-89c10bd7`）。

- Password（密码）：与用户名相同（Postmark 使用服务器令牌同时作为用户名和密码）。

- 注意：在接下来的过程中，我将使用**我的**凭据作为示例。**这些与你的完全不同**。**请使用你自己的凭据。**

## 步骤 2：配置 Mailcow 使用 Postmark 作为 SMTP 继发

### 2.1 访问 Mailcow 管理界面

- 登录 Mailcow：

- 通过访问管理界面进入你的 Mailcow 实例（例如，`https://192.168.5.3/admin` 或 `https://mailserver.home.arpa/admin`）。

- 使用你的管理员凭据登录。

### 2.2 找到 SMTP 继发部分

- 在 Mailcow 管理主仪表板，点击顶部的 **System**（系统），然后点击 **Configuration**（配置）。

- 点击 **routing**（路由）标签页。

- 注意“sender-dependent transport”（依赖发送者的传输）部分。这就是我们放置 Postmark 凭据的地方。

### 输入 Postmark 详情

- 使用提供的凭据。

- **SMTP Server（SMTP 服务器）：** 设置 SMTP 服务器为 Postmark 的 `smtp.postmarkapp.com:587`。

- **Ports（端口）：** 如果 Postmark 使用 TLS 和加密，使用端口 587。

- **Username & Password（用户名与密码）：** 输入上一步由 Postmark 提供的令牌。此令牌同时作为用户名和密码。

- **Username（用户名）：** 替换为你的令牌。

- **Password（密码）：** 与用户名相同。

- 点击添加

这就是在 Mailcow 中配置 Postmark 作为 SMTP 继发服务器的。
