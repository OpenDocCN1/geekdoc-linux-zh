

# 身份验证漏洞扫描

*   返回扫描

| 严重程度 | 分数 | 名称 | 插件族 | 数量 | 扫描详情 |
|---|---|---|---|---|---|
| 严重 | 10.0 | Ubuntu 16.04 (TS) / 18.04 (TS) / 20.04 (TS) - Sandbox-update (CVE-2019-5736) | Ubuntu 本地安全检查 | 1 | 策略：凭据补丁审计已完成；基础：本地扫描器；扫描器：今天凌晨 12:48；结束： 3 分钟后过期 |
| 严重 | 10.0 | Ubuntu 16.04 (TS) / 18.04 (TS) / 20.04 (TS) - DirtyCOW 漏洞 (CVE-2016-5195) | Ubuntu 本地安全检查 | 1 | 漏洞 |
| 严重 | 9.8 | Ubuntu 16.04 (TS) / 18.04 (TS) / 20.04 (TS) - Ghostbleed 漏洞 (CVE-2017-5754) | Ubuntu 本地安全检查 | 1 | 严重；高；中；低；信息 |
| 严重 | 9.8 | Ubuntu 16.04 (TS) / 18.04 (TS) / 20.04 (TS) / 20.10 / 21.04 - Intel处理器微代码漏洞 (CVE-2022-20924) | Ubuntu 本地安全检查 | 1 | |
| 严重 | 9.8 | Ubuntu 16.04 (TS) / 18.04 (TS) / 20.04 (TS) / 20.10 - 完美向前安全性 (CVE-2021-31560) | Ubuntu 本地安全检查 | 1 | |
| 严重 | 9.8 | Ubuntu 16.04 (TS) / 18.04 (TS) / 20.04 (TS) / 20.10 - Bleeding Pipe 漏洞 (CVE-2021-3156) | Ubuntu 本地安全检查 | 1 | |

图 67：身份验证扫描结果

我们从 Ubuntu 本地安全检查插件族中获取了漏洞列表。320 个插件被分到不同的插件检查中，用于在相同的上下文中查找漏洞。例如，检查数据库、框架或 Web 服务器漏洞的插件有各自的插件族。Ubuntu 本地安全检查插件族包含许多插件，用于检查 Ubuntu 的本地漏洞和缺失的补丁。

> 320 (Tenable, 2022), https://www.tenable.com/plugins/families/Ubuntu%20Local%20Security%20Checks
> 321 (Tenable, 2022), https://www.tenable.com/plugins/ness/families

PWK - © 2023 OffSec Services Limited. 保留所有权利。

# OffSec

使用 Kali Linux 进行渗透测试

| | | | | | | |
|---|---|---|---|---|---|---|
| 严重 | 9.8 | Ubuntu 20.04 LTS / 20.04: Firefox 漏洞 (USN-5284-1) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.8 | Ubuntu 20.04 - Ghostscript 漏洞 (USN-4445-1) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.8 | Ubuntu 20.04 LTS / 20.04: Python 漏洞 (USN-4973-1) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.8 | Ubuntu 20.04 LTS / 20.10: Python 漏洞 (USN-4940-1) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.8 | Ubuntu 20.04 LTS / 21.10: Linux 内内核漏洞 (USN-5208-1) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.8 | Ubuntu 20.04 LTS - GnuTLS 漏洞 (USN-5029-1) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.8 | Ubuntu 20.04 LTS - Python 漏洞 (USN-4973-2) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.1 | Ubuntu 16.04 LTS / 18.04: App 漏洞 (USN-4449-1) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.1 | Ubuntu 16.04 LTS / 20.04: NGS 漏洞 (USN-4476-1) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.1 | Ubuntu 16.04 LTS / 18.04 / 20.10: snapbleed 漏洞 (USN...) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.1 | Ubuntu 18.04 LTS / 20.04 / 21.01: Pillow 漏洞 (USN-49...) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.1 | Ubuntu 18.04 LTS / 20.04 / 21.01: Bluebleed (USN-51...) | Ubuntu 本地安全检查 | 1 | ✓ |
| 严重 | 9.1 | Ubuntu 20.04 LTS / 20.04 / 21.10: cryptography 漏洞 (USN-5286-1) | Ubuntu 本地安全检查 | 1 | ✓ |

图 68：Firefox 和 cURL 的漏洞数据

## 7.2 使用 Nessus 插件

默认情况下，Nessus 在运行默认模板时会在后台启用许多插件。这在许多场景中非常有用；但我们也可以微调选项以快速运行单个插件。我们可以利用此功能来验证之前的发现，或者发现环境中所有面临风险的威胁。

在本例中，我们将设置一个插件过滤器来识别主机是否容易受到 CVE-2021-3156 漏洞的影响，这是一个可以在本地利用的漏洞，允许非特权用户提升权限到 root。为了利用插件过滤器，我们将再次开始一次“新扫描”。

> 332 (Mozilla, 2022), https://www.mozilla.org/en-US/firefox/news
> 333 (Wikipedia, 2022), https://en.wikipedia.org/wiki/
> 334 (Tenable, 2021), https://www.tenable.com/cve/CVE-2021-3156

PWK - © 2023 OffSec Services Limited. 保留所有权利。

图 69：创建扫描

默认情况下，Nessus 在运行默认模板时会在后台启用许多插件。这在许多场景中非常有用；但我们也可以微调选项以快速运行单个插件。我们可以利用此功能来验证之前的发现，或者发现环境中所有面临风险的威胁。

在本例中，我们将设置一个插件过滤器来识别主机是否容易受到 CVE-2021-3156 漏洞的影响，这是一个可以在本地利用的漏洞，允许非特权用户提升权限到 root。为了利用插件过滤器，我们将再次开始一次“新扫描”。

> 332 (Mozilla, 2022), https://www.mozilla.org/en-US/firefox/news
> 333 (Wikipedia, 2022), https://en.wikipedia.org/wiki/
> 334 (Tenable, 2021), https://www.tenable.com/cve/CVE-2021-3156

PWK - © 2023 OffSec Services Limited. 保留所有权利。

图 70：选择高级扫描

为了做到这一点，我们将选择高级扫描。该模板允许我们使用过滤器，而不是手动启用或禁用插件。这一次，我们将配置名称和目标。

> 332 (Mozilla, 2022), https://www.mozilla.org/en-US/firefox/news
> 333 (Wikipedia, 2022), https://en.wikipedia.org/wiki/
> 334 (Tenable, 2021), https://www.tenable.com/cve/CVE-2021-3156

PWK - © 2023 OffSec Services Limited. 保留所有权利。

图 71：输入名称和目标

接下来，我们将提供相同的 SSH 和 sudo 凭据，这意味着我们也在进行身份验证扫描。现在，我们可以选择想要使用的插件。如前所述，高级扫描允许我们使用过滤器，而不是启用或禁用插件。

> 332 (Mozilla, 2022), https://www.mozilla.org/en-US/firefox/news
> 333 (Wikipedia, 2022), https://en.wikipedia.org/wiki/
> 334 (Tenable, 2021), https://www.tenable.com/cve/CVE-2021-3156

PWK - © 2023 OffSec Services Limited. 保留所有权利。

图 72：筛选特定插件

为了这样做，我们将点击“动态插件”选项卡。在下拉菜单中，我们选择 CVE 来过滤特定的 CVE。在右侧下拉菜单中，我们可以指定 CVE 编号。在输入“CVE-2021-3156”后，我们可以点击“预览插件”。这可能需要几分钟才能完成。

> 332 (Mozilla, 2022), https://www.mozilla.org/en-US/firefox/news
> 333 (Wikipedia, 2022), https://en.wikipedia.org/wiki/
> 334 (Tenable, 2021), https://www.tenable.com/cve/CVE-2021-3156

图 73：选择 CVE-2021-3156 的插件族

一旦预览插件运行完成，我们将获得覆盖特定 CVE 的插件族列表。

动态插件过滤器的一个非常实用的功能是可以组合多个过滤器。在本例中，我们知道目标是一个 Ubuntu Linux 系统，然后可以使用第二个过滤器来指定相关的插件族。让我们通过点击第一个过滤器旁边的“+”按钮来添加新过滤器。

> 332 (Mozilla, 2022), https://www.mozilla.org/en-US/firefox/news
> 333 (Wikipedia, 2022), https://en.wikipedia.org/wiki/
> 334 (Tenable, 2021), https://www.tenable.com/cve/CVE-2021-3156

图 74：添加过滤器

出现一个新的插件过滤器。为了将插件族限制为针对 Ubuntu 的特定检查，我们在左侧下拉菜单中选择“插件族”，并在右侧下拉菜单中选择“Ubuntu 本地安全检查”。

> 332 (Mozilla, 2022), https://www.mozilla.org/en-US/firefox/news
> 333 (Wikipedia, 2022), https://en.wikipedia.org/wiki/
> 334 (Tenable, 2021), https://www.tenable.com/cve/CVE-2021-3156

图 75：组合插件过滤器

然后我们可以点击“预览插件”，列出由我们的过滤器确定的插件。完成后，点击下拉菜单并选择“Ubuntu 本地安全检查”。Nessus 显示有关该插件的信息，包括影响的 Ubuntu 版本、简短描述和补丁编号，以及插件 ID。

图 76：针对 CVE-2021-3156 的 Ubuntu 本地安全检查插件

我们可以通过点击插件获取更多信息。图 77 显示了指定插件的详细信息。

