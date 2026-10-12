
479 (Exiftool, 2022), https://exiftool.org/##supported
480 (Exiftool, 2022), https://exiftool.org/

```
kalikali:~/Downloads$ exiftool -a -u brochure.pdf
iftool Version Number : 12.41
File Name : brochure.pdf
Directory : 
File Size : 303 KiB
File Modification Date/Time : 2022:04:27 03:27:39:00
File Access Date/Time : 2022:04:28 07:56:58:00
File Inode Change Date/Time : 2022:04:28 07:56:58:00
File Permissions : -rw-
File Type : PDF
File Type Extension : pdf
MIME Type : application/pdf
PDF Version : 1.7
Linearized : No
Page Count : 4
Language : en-US
Tagged PDF : Yes
XMP Tool : Image::Exiftool 12.41
Creator : Stanley Yelnets
Title : Mountain Vegetables
Author : Stanley Yelnets
Create : Microsoft PowerPoint® for Microsoft 365
Create Date : 2022:04:27 07:34:01+02
Creator Tool : Microsoft PowerPoint® for Microsoft 365
Modify Date : 2022:04:27 07:34:01+02
Document ID : uuid:B86ED371-D165-4BD4-99C9-A15FA9C3A3C
Instance ID : uuid:B86ED371-D165-4BD4-99C9-A15FA9C3A3C
Title : Mountain Vegetables
Author : Stanley Yelnets
Create Date : 2022:04:27 07:34:01+02
Modify Date : 2022:04:27 07:34:01+02
Producer : Microsoft PowerPoint® for Microsoft 365
Creator : Stanley Yelnets
```

The output shows the document was created with Microsoft PowerPoint® for Microsoft 365.

---

### 11.1.2 客户端指纹识别

在本节中，我们将讨论客户端指纹识别，也称为设备指纹识别⁴⁸¹，用于从目标网络获取操作系统信息。在渗透测试中，建立建立立脚点。例如，我们假设我们通过 Harvester⁴⁸² 在网络中建立了立脚点。

在此之前，我们需要确认目标是 Windows 是否启了 Explorer 或 Edge。我们将使用 Canarytokens⁴⁸⁵，一种生成链接的免费服务。我们可以使用 HTML （HTA）⁴⁸³在 Internet Explorer 的文中执行代码。

> ⁴⁸¹ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Device_fingerprint
> ⁴⁸² (Github, 2022), https://github.com/laramies/theHarvester
> ⁴⁸³ (Microsoft, 2013), https://msdn.microsoft.com/en-us/library/ms536496(VS.85)
> ⁴⁸⁴ (The Hacker News, 2021), https://thehackernews.com/2021/04/lazarus-apt-hackers-are-now-using-html
> ⁴⁸⁵ (Canarytokens, 2022), https://canarytokens.com

在准备好借口后，通过在浏览器中加载令牌页面⁴⁸⁷在 Canarytokens 中创建我们的链接。图 166 显示了该站的落地页。

# 使用 Kali Linux 进行 OffSec 渗透测试

![](img/987dc9f6ebd8893c565a1d124d7724e6_319_0.png)

图 166：Canarytokens 落地页

该表单为我们提供了一个下拉菜单，用于选择我们想要创建的跟踪令牌类型。我们必须输入电子邮件地址以接收有关跟踪令牌的警报，或者提供一个 webhook URL。在本例中，从下拉菜单中选择“Web bug / URL token”，将 `https://example.com` 设置为 webhook URL，然后在注释中输入“Fingerprinting”（指纹识别）。输入这些信息后，我们将点击“Create My Canarytoken”。

![](img/987dc9f6ebd8893c565a1d124d7724e6_319_1.png)

图 167：在表单中输入 example.com

出现了一个带有蓝色窗口的新页面，显示我们的 Web 令牌现在已激活：

# OffSec

使用 Kali Linux 进行渗透测试

![](img/987dc9f6ebd8893c565a1d124d7724e6_320_0.png)

# 您的 Web 令牌已激活！

将此 URL 复制到剪贴板并按需使用：

```
canaryotokens.com/tags/static/7uJ 复制
```

记住，每当有人请求该 URL 时它就会触发。

如果 URL 以图像形式提供（例如 `<img src="`），则会提供一个 1x1 的图像。

如果 URL 在浏览器中访问，则会提供一个带有指纹识别 JavaScript 的空白页面。

使用建议：

- 嵌入在具有诱人主题行行的电子邮件中。
- 嵌入在文档中。
- 插入到只能通过暴力破解发现的 canary 网页中。
- 这只是一个示例。除了主机名和实际令牌（随机字符串外），你可以更改 URL 的所有其他部分。

图 16：激活的 Canarytoken

该页面包含了我们可以用于识别目标指纹的跟踪链接。它还提供了如何引导目标点击链接的建议。

接下来，点击页面右上角的“Manage this token”（管理此令牌）。这将我们带令牌设置。

![](img/987dc9f6ebd8893c565a1d124d7724e6_320_1.png)

新令牌历史

# 令牌设置

| Webhook 报告 | 开启 |
| 浏览器扫描 | 开启 |
| 查看令牌时运行 JavaScript 指纹识别 | |

这是您的 Web 令牌：

```
canaryotokens.com/tags/static/7uJ 复制
```

此令牌尚未被触发

我们希望您喜欢 Canarytokens 的免费版！

如需更多（非公开的）令牌、支持、批量部署工具以及更有效地管理您已部署的令牌，请查看我们的商业版 Canarytoken 方案：https://canaryotokens.com/canaryotokens。

由 Thinkst Canary 提供，这是我们极易于使用的蜜罐解决方案，仅需四分钟即可部署。知晓其重要。

PWK - Copyright © 2023 OffSec Services Limited. 版权所有。

321

制作于摩洛哥

# 图 169：Canarytoken 的管理

令牌尚未被触发，这是意料之中的，因为我们刚刚创建了它。在本例中，我们将保持默认设置，因为我们只是对目标进行指纹识别，而不是将令牌嵌入 Web 应用程序或网页。

接下来，点击右上角的“History”（历史）。历史页面向我们显示所有点击过我们 Canarytoken 链接的访问者以及受害者系统的信息。目前列表是空的。

![](img/987dc9f6ebd8893c565a1d124d7724e6_321_0.png)

# 图 170：Canarytoken 历史

假设我们已经根据之前的伪装（pretext）说服了受害者通过电子邮件访问 Canarytoken 链接。受害者一旦点击我们的链接，他们的浏览器中就会出现一个空白页。同时，我们的历史列表中出现了一个新条目：

![](img/987dc9f6ebd8893c565a1d124d7724e6_321_1.png)

# 图 171：带有条目的 Canarytoken

左侧的地图显示了受害者的地理位置。我们可以点击该条目获取更多信息。

# OffSec

使用 Kali Linux 进行渗透测试

![](img/987dc9f6ebd8893c565a1d124d7724e6_322_0.png)

图 172：Canarytoken 的详细信息
