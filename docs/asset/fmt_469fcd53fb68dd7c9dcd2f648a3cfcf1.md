
每个页面在其行的开头还有两个灰色的图标。点击第一个会暂停对此页面的检查，

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_26_0.png)

点击第二个则停止通知你更改，但继续检查它们。点击 `Edit` 按钮会打开该页面变化检测监视项的设置。

### 基本设置

在添加页面之前，我将首先介绍 `changedetection.io` 的一些基本设置。点击右上角的 `Settings` 后，`General`（通用）选项卡允许你设置检查之间的时间间隔（默认为三小时）以及其他通用设置。这是你为 `changedetection.io` 设置密码的地方。如果你更改了任何设置，请点击底部的 `Save`。

在 `Notifications`（通知）选项卡（图 3）中，你定义 `changedetection.io` 检测到页面更改时如何向你发送通知。如果你习惯于手动定期检查监视列表，或者在 RSS 阅读器中监控更改，可以留空此字段。但如果你希望获得更快的通知，请在此处进行设置。

`Changedetection.io` 使用 `Apprise` [4] 进行通知。`Apprise` 是一个库，支持向 100 多个流行服务发送通知，包括 `Telegram`、`Discord`、`Slack`、`Home Assistant`、`Kodi`、`Pushbullet` 和电子邮件。对于每个这些服务，`Apprise` 都定义了一个 URL。我将使用 `Mailjet` [5] 发送电子邮件作为示例（更多示例请参见 `Apprise` wiki [6]）。

在 `changedetection.io` 的 `Notification URL List`（通知 URL 列表）中输入一个或多个 `Apprise` URL。对于 `Mailjet`，看起来像这样：

```
mailto://username:password@in-v3.mailjet.com/?from=Change&detection2@changedetection@example.com&to=koen@vervioesem.eu&mode=ssl
```

这将通知定义为安全的 SMTP，包含登录的用户名和密码，以及 SSL 模式下的发件人和收件人电子邮件地址。

然后，如果你点击 `Send test notification`（发送测试通知），你应该会在所有设置好的服务上收到通知。如果没有，请点击 `Notification debug logs`（通知调试日志）并找出哪里出了问题。你也可以更改通知的标题和正文，但默认值通常就很好。

别忘了点击底部的 `Save` 来保存你的通知设置。目前，你可以忽略 `changedetection.io` 设置中的其他选项卡。

### 添加新的变化检测监视项

如果你想监控特定网页的变化，你可以简单地在上方的文本框（`Add a new change detection watch` 下方）中输入 URL。可选地，添加一个或多个标签（用逗号分隔），然后点击 `Watch` 以默认设置添加监视项，或点击 `Edit | Watch` 在添加前编辑监视项的设置。

默认情况下，`changedetection.io` 监视网页文本/HTML、JSON 和 PDF 的变化。然而，如果你为单个产品页面选择 `Re-stock & Price detection`（补货与价格检测），程序会寻找价格或诸如 "in stock"（有货）或 "out of stock"（缺货）等术语的迹象，这让你可以监视价格或库存状态的变化。请注意，这仅在该页面只涵盖一个产品时有效。

还有一个 `Chrome` 扩展程序 [7]，可与你的 `changedetection.io` 实例配合使用。只需将其添加到 `Chrome`，打开你的 `Changedetection.io` 设置并转到 `API` 选项卡。然后从工具栏打开扩展程序并点击 `Sync API Access`（同步 API 访问）。该扩展程序随后会自动配置自身以与你的 `changedetection.io` 实例通信。

在任何页面上，你现在都可以点击工具栏中的扩展程序图标，选择是否要检测普通更改还是库存和价格更改，可选地添加一个或多个标签，然后点击 `Watch this website`（监视此网站）以添加变化检测监视项（图 4）。

### 变化检测监视项设置

如果你在添加新监视项时点击 `Edit | Watch`，或对现有监视项点击 `Edit`，你可以修改与该变化检测监视项相关的各种设置。在 `General`（通用）选项卡中，你可以更改监视表格中显示的标题（默认为完整 URL）、标签，以及如果你希望不同于全局设置时的检查时间间隔。`Request`（请求）选项卡允许你调整 `changedetection.io` 获取网页的方式，我稍后解释。对于一般网页变化，有设置用于过滤页

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_27_0.png)

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_28_0.png)

`changedetection.io` 用于监控变化。`视觉过滤器选择器` 是一种高级功能，我稍后会解释，而 `过滤器` 和 `触发器` 允许你从页面中移除 HTML 元素或仅选择特定的 HTML 元素。例如，我正在监控的一个网页底部有一个页脚，显示它拦截了多少次“恶意”访问尝试。显然，这触发了我不关心的变化检测。在检查该网页的 HTML 代码时，我注意到 `main` 元素包含了我所需的所有信息，而不包括页脚。因此，我在该选项卡的 CSS/JSONPath/JQ/XPath 过滤器文本框中添加了 XPath 过滤器 `/main`。别忘了保存你的更改。

对于库存和价格检测，`重新补货 & 价格检测` 选项卡允许你调整监控行为。例如，你可以指定是想了解任何可用性变化，还是仅当缺货产品重新有货时才通知。你还可以启用或禁用价格监控，甚至可以在价格低于或高于设定值时触发通知（图 5）。

![](img/d6d2a4cd4a2f445e8c9e8079857e2469_28_1.png)

对于这两种类型的变化检测监控，`通知` 选项卡允许你将行为从使用通用通知设置修改为针对此监控的自定义设置。例如，你可以禁用此监控的通知，或添加另一个 `Apprise` URL 用于自定义通知。`统计信息` 选项卡仅显示监控的一些统计数据，并允许你下载 `changedetection.io` 从页面下载的最新 HTML 版本以调试任何问题。

## 使用 Chromium/JavaScript 服务器

默认情况下，`changedetection.io` 使用 HTTP 客户端将监控的页面下载为纯 HTML 文件。这对于许多网页有效且速度快。但是，一旦页面使用 JavaScript 渲染其内容的重要部分，这个简单的 HTTP 客户端就无法看到内容。幸运的是，你可以在 Docker 容器中运行一个 Web 浏览器，并让 `changedetection.io` 使用它来获取监控的页面。

### 列表 2：包含 Chromium/JavaScript 服务器的 changedetection.io Docker Compose 文件

```yaml
version: '3.2'
services:
  changedetection:
    image: ghcr.io/dgtlmoon/changedetection.io
    container_name: changedetection
    hostname: changedetection
    volumes:
      - /home/ksan/changedetection:/datastore
    ports:
      - 5000:5000
    environment:
      - PLAYWRIGHT_DRIVER_URL=ws://playwright-chrome:3000
    restart: unless-stopped
    depends_on:
      playwright-chrome:
        condition: service_started
  playwright-chrome:
    image: dgtlmoon/sockpuppetbrowser:latest
    container_name: playwright-chrome
    hostname: playwright-chrome
    environment:
      - SCREEN_WIDTH=1920
      - SCREEN_HEIGHT=1024
      - SCREEN_DEPTH=16
      - MAX_CONCURRENT_CHROME_PROCESSES=10
    restart: unless-stopped
```

要配置此功能，请使用列表 2 中显示的 Docker Compose 文件更新你的 `docker-compose.yml` 文件。这会添加一个运行 `Chromium` Web 浏览器的第二个容器，并让 `changedetection.io` 的容器等待此容器启动。在这些更改后，使用以下命令重启 Docker Compose：

```bash
$ docker compose up -d
```
