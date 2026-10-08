
关键漏洞。尽管所有漏洞都至关重要，但我们应该优先关注关键漏洞，因为它们可能使我们的系统易受勒索软件和远程代码执行（RCE）等危险的攻击。

让我们点击图表中的关键部分。这将打开并显示关键漏洞。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_248_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_249_0.png)

这现在会打开一个包含关键漏洞列表的屏幕。请注意，中间的漏洞被标记为 MS17-010。这是微软对“永恒之蓝”（EternalBlue）漏洞的命名，该漏洞由美国国家安全局（NSA）开发，于 2017 年 4 月由影子经纪人（ShadowBrokers）黑客组织泄露，并被 WannaCry 和 Petya 勒索软件等恶意软件利用，在全球范围内攻击系统。正如上面 nmap 扫描所警告的那样，我们的系统极易受到此攻击。

我们可以更深入地挖掘，点击 MS17-010 漏洞，获取更详细的详细信息。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_250_0.png)

# 新扫描 / 插件 #97833

< 返回漏洞组

- 漏洞：21 个

CRITICAL | MS17-010: Microsoft Windows SMB 服务器安全更新 (401389) (ET...

**描述**

远程 Windows 主机受到以下漏洞的影响：

- 由于对某些请求处理不当，Microsoft Server Message Block 1.0 (SMBv1) 中存在多个远程代码执行漏洞。未经身份验证的远程攻击者可以通过特别构造的包利用这些漏洞执行任意代码。(CVE-2017-0143, CVE-2017-0144, CVE-2017-0145, CVE-2017-0146, CVE-2017-0148)
- 由于对某些请求处理不当，Microsoft Server Message Block 1.0 (SMBv1) 中存在信息泄露漏洞。未经身份验证的远程攻击者可以通过特别构造的包利用此漏洞泄露敏感信息。(CVE-2017-0147)

ETERNALBLUE、ETERNALCHAMPION、ETERNALROMANCE 和 ETERNALSYNERGY 是 Equation Group 在 2017/04/14 由影子经纪人（Shadow Brokers）组织公开的多个漏洞和利用工具中的一部分。WannaCry / WannaCrypt 是利用 ETERNALBLUE 漏洞的勒索软件程序，而 EternalSyS 是利用 Equation Group 七个漏洞的蠕虫。Petya 是一种勒索软件程序，首先利用 CVE-2017-0199（Microsoft Office 中的一个漏洞），然后通过 ETERNALBLUE 进行传播。

**解决方案**

微软已发布了一系列适用于 Windows Vista、2008、9、2008 R2、2012、8.1、RT 8.1、2012 R2、10 和 2016 的补丁。微软还为不再支持的 Windows 操作系统发布了紧急补丁，包括 Windows XP、2003 和 8。

对于不受支持的 Windows 操作系统，例如 Windows XP，微软建议用户停止使用 SMBv1。SMBv1 缺乏后续 SMB 版本中包含的安全功能。可以按照供应商提供的说明禁用 SMBv1

| 插件详情 |
| :--- |
| 严重性：关键 |
| ID：97833 |
| 版本：1.22 |
| 类型：远程 |
| 类别：Windows |
| 发布时间：2017年3月20日 |
| 修改时间：2019年2月26日 |

| 风险信息 |
| :--- |
| 风险因素：关键 |
| CVSS v3.0 基础评分：8.1 |
| CVSS v3.0 向量：CVSS:3.0/AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H |
| CVSS v3.0 时间向量：CVSS:3.0/E:H/RL:O/RC:C |
| CVSS v3.0 时间评分：7.7 |
| CVSS 基础评分：10.0 |
| CVSS 时间评分：8.7 |
| CVSS 向量：CVSS2#AV:N/AC:L/Au:N/C:C/I:C/A:H |

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_251_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_252_0.png)

Nessus 现在会询问您是否想要创建执行摘要或自定义报告。我选择了执行摘要，然后在右上角选择了 PDF 格式。现在 Nessus 将开始生成一份外观专业的 PDF 格式“执行摘要”，总结您的漏洞扫描结果，可直接提交给您的 CTO 或 CISO。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_254_0.png)

# 使用 OWASP ZAP 进行网站漏洞扫描

Nessus 是一个查找系统和应用程序漏洞的绝佳工具，但如果我们想要测试网站和 Web 应用程序的漏洞，我们可能希望使用专门为该目的设计的工具。在第 6 章中，我们使用 whatswweb 工具对网站进行指纹识别，它提供了关于该网站的重要信息，例如：
1. 提供该网站的所属国家；
2. CMS（内容管理系统）；
3. Web 服务器；以及
4. 构建网站所使用的技术。

在此阶段，我们想了解更多信息。我们想知道网站可能存在哪些我们可以利用的潜在漏洞。有许多优秀的商业工具可用于此目的，但幸运的是，OWASP（开放式 Web 应用程序安全项目）拥有其中最好的工具之一，而且它是免费的！

从 Kali GUI，你可以转到应用程序，Web 应用程序分析，然后点击 OWASP ZAP，或者，如果你更喜欢命令行，只需在命令行中输入 **OWASP ZAP**。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_257_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_257_1.png)

- 收藏夹
    - 01 - 信息收集
    - 02 - 漏洞分析
    - 03 - Web 应用程序分析
    - 04 - 数据库评估
    - 05 - 密码攻击
    - 06 - 无线攻击
    - 07 - 逆向工程
    - 08 - 利用工具
    - 09 - 嗅探与欺骗
    - 10 - 后渗透
    - 11 - 取证
    - 12 - 报告工具
    - 13 - 社会工程学工具
    - 14 - 系统服务
    - 常用应用程序
- burpsuite
- commix
- htrack
- **owasp-zap**
- paros
- skipfish
- sqlmap
- webscarab
- wpscan

```
root@kali-2019:~# owasp-zap
Found Java version 11.0.2
Available memory: 5926 MB
Setting jvm heap size: -Xmx1481m
0 [main] INFO org.zaproxy.zap.GuiBootstrap - OWASP ZAP 2.7.0 started 29/07/2019, 09:47:00 with home /root/.ZAP/
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.zaproxy.zap.GuiBootstrap (file:/usr/share/zaproxy/zap-2.7.0.jar) to field sun.awt.X11.XToolkit.awtAppClassName
WARNING: Please consider reporting this to the maintainers of org.zaproxy.zap.GuiBootstrap
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
1350 [AWT-EventQueue-0] INFO org.parosproxy.paros.network.SSLConnector - Reading supported SSL/TLS protocols...
1364 [AWT-EventQueue-0] INFO org.parosproxy.paros.network.SSLConnector - Using a SSL4Engine...
2428 [AWT-EventQueue-0] INFO org.parosproxy.paros.network.SSLConnector - Done reading supported SSL/TLS protocols: [SSLv2Hello, SSLv3, TLSv1, TLSv1.1, TLSv1.2, TLSv1.3]
2469 [AWT-EventQueue-0] INFO org.parosproxy.paros.extension.option.OptionsParamCertificate - Unsafe SSL renegotiation disabled.
```

第一次使用 OWASP ZAP 时，您将必须阅读并同意最终用户许可协议（EULA）。完成后，OWASP ZAP 将向您显示以下屏幕。此屏幕询问

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_260_0.png)

你是否想要“保留 ZAP 会话”。本质上，它在询问你是否想要保存该会话。

最好通过名称和位置“保留”会话，即第二个单选按钮选项。这将把结果保存到您选择位置的文件中。我将把我的命名为“第一次 Web 漏洞扫描”（我很有创意，不是吗），并将其保存到 /root 文件夹。

接下来，您将看到一个标题为“管理插件”的屏幕，如下所示。

# 管理插件

已安装 | 市场

ZAP Core 2.7.0 : ZAP 是最新版本

插件

筛选器：

| 名称 | 描述 | 更新 |
| :--- | :--- | :--- |
| Active scanner rules | 发布质量的主动扫描器规则 | 更新 |
| AdvFuzzer | 用于手动测试的高级模糊测试器 | |
| Ajax Spider | 允许您对大量使用 Java... 的网站进行爬行 | 更新 |
| Context Alert Filters | 允许您自动更改警报风险级别。 | 更新 |
| Core Language Files | 核心语言文件的翻译 | 更新 |
| Diff | 显示两个请求之间差异的对话框... | |
| Directory List v1.0 | 要与“强制浏览...”一起使用的目录名称列表 | |
| Forced Browse | 使用代码fro...对文件和目录进行强制浏览 | |
| Getting Started with ZAP ... | ZAP 入门指南的简短说明。 | 更新 |
| Help - English | ZAP 帮助文件的英文（主）版本。 | |
| Import files containing URLs | 添加导入 URL 文件的选项。文件必须... | |
| Invoke Applications | 通过传递上下文相关信...调用外部应用程序 | 更新 |
| jxBrowser (core) | 基于 Chromium 的嵌入式浏览器，您必须... | 更新 |
| jxBrowser (Linux 64) | 基于 Chromium 的嵌入式浏览器。Linux 64 s... | 更新 |

卸载所选 | 更新所选 | 更新全部 | 关闭

