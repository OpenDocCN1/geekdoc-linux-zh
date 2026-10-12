
| rdp-ntlm-info: |
|---|---|
| Target_Name | sandbox |
| NetBIOS_Domain_Name | SANDBOX |
| NetBIOS_Computer_Name | sandbox.local |
| DNS_Domain_Name | sandbox.local |
| DNS_Computer_Name | SANDBOX.sandbox.local |
| DNS_Tree_Name | sandbox.local |
| Product_Version | 10.0.14393 |
| System_Time | 2019-12-17T01:36:29+00:00 |
| Subject | CommonName=SANDBOX.sandbox.local |
| Not valid before | 2019-11-25T06:48:49 |
| Not valid after | 2020-05-26T06:48:49 |
| ssl_date | 2019-12-17T10:36:28+00:00(+8h001s from scanner time. |

| Host script results: |
|---|---|
| clock_skew | mean: 9h3m0s, deviation: 3h34m2s, median: 8h0m0s |
| smb-os-discovery | OS: Windows 10 15063 (Windows 10 6.3) OS CPE: cpe:/o:microsoft:windows_10::| Computer name: CEVAPI NetBIOS computer: SANDBOX Domain name: sandbox.local Forest name: sandbox.local FQDN: CEVAPI.sandbox.local System time: 2019-12-17T15:03:48+00:00 smb-security-mode: account_used: guest authentication-level: user challenge_response: supported message_signed: disabled (dangerous, but default) smb2-security-mode: 2.0.2. Message signing enabled but not required smb-time: date: 2019-12-17T23:23:37 start_date: 2020-01-01T22:07:03 |

# 攻击性安全

可以通过打开 Firefox 选项并搜索“proxy”（代理）来实现。

![](img/f99f528ca9845f4c256ce54e882b1345_821_0.png)

图 352：正在查找代理设置

应取消勾选“所有协议都使用此代理服务器”选项，并将 SOCKS 主机设置为 127.0.0.1，端口设置为 1080。最后，我们将点击 SOCKS v4 单选按钮并点击确定。

# 网络设置

配置 Firefox 代理连接互联网。了解更多

# 配置代理访问互联网

- 不使用代理
- 自动检测此网络的代理设置
- 使用系统代理设置
- 手动代理配置

| HTTP 代理 | 端口 | 0 |
| :--- | :--- | :--- |
| SSL 代理 | 端口 | 0 |
| ETP 代理 | 端口 | 0 |
| SOCKS 主机 | 127.0.0.1 | 端口 | 1080 |

- 所有协议都使用此代理服务器
- SOCKS v4
- SOCKS v5
- 自动代理配置 URL

示例：.mozilla.org, .net.nz, 192.168.1.0/24
- 如果保存了密码，则不提示验证
- 使用 SOCKS v5 时代理 DNS
- 启用通过 HTTPS 的 DNS

![](img/f99f528ca9845f4c256ce54e882b1345_822_0.png)

# 使用 Kali Linux 2.0 进行渗透测试

接下来，我们将打开 Offensive Sec 新标签页并访问 `http://10.5.5.25:8080`

![](img/f99f528ca9845f4c256ce54e882b1345_823_0.png)

# 欢迎使用 Jenkins!

用户名
密码
登录

保持登录状态

![](img/f99f528ca9845f4c256ce54e882b1345_823_1.png)

图 354：访问端口 8080  10.5.5.25

打开的页面是 Jenkins 登录页面。这是一个非常有的目标，因为 Jenkins 是一个极其强大的软件，可能会暴露一些攻击面。因此，接下来我们将把精力集中在这个主机上。

## 24.8 目标：Jenkins

Jenkins 是一个自动化服务器，可用于自动化许多与软件开发相关的任务。由于其本质性，像 Jenkins 这样的持续集成和交付工具通常能够执行代码。为了使用由特定事件或操作触发的自定义可重复任务，这种能力是必要的。

Jenkins 这类工具的常见用途是在推送提交（commit）后拉取 git 仓库，运行一系列测试以确保更改期间没有损坏应用程序，如果一切顺利，则将代码合并到 master 分支。为了实现这一点，Jenkins 需要具备以下能力

> 745（维基百科，2019），https://en.wikipedia.org/wiki/Jenkins_(software)
> 746（持续交付基金会，2020），https://jenkins.io/doc/

来执行系统命令。作为渗透测试员，访问 Jenkins 将为我们提供代码执行的路径。

一如既常，在开始尝试利用任何东西之前，我们想要进行某种程度的枚举。我们已经通过端口扫描进行了网络枚举，但现在我们只想专门关注 Jenkins 应用程序本身。

### 24.8.1 应用程序枚举

首先，我们可以通过查看 Jenkins 登录页的文档对象模型（DOM）开始枚举。稍后我们还会查看 HTML 源代码，因为它可能与 DOM 不同。要查看 DOM，请右键点击页面并选择“检查元素”。

![](img/f99f528ca9845f4c256ce54e882b1345_824_0.png)

图 355：检查元素

# 攻击性安全
www.offensive-security.com

使用 Kali Linux 2.0 进行渗透测试

在 Firefox 开发工具窗口中，右键点击顶部的 HTML 标签并选择“全部展开”。

![](img/f99f528ca9845f4c256ce54e882b1345_825_0.png)

图 356：展开 DOM

PWK 2.0 版权 © Offensive Security Ltd. 保留所有权利。826

# 攻击性安全
www.offensive-security.com

使用 Kali Linux 2.0 进行渗透测试

查看 DOM 没有显示任何信息。我们可以看到页面是一个基础 HTML 表单。

![](img/f99f528ca9845f4c256ce54e882b1345_826_0.png)

接下来，我们将查看源代码，看看是否隐藏了什么。

# 攻击性安全
www.offensive-security.com

使用 Kali Linux 2.0 

要这样做，右键点击页面任意位置并选择“查看源代码”。

![](img/f99f528ca9845f4c256ce54e882b1345_827_0.png)

图 358：Jenkins 

DOM 视图没有显示任何信息。我们可以看到页面是一个基础 HTML 表单。

![](img/f99f528ca9845f4c256ce54e882b1345_828_0.png)

接下来，我们将查看源代码，看看是否隐藏了什么。

# 攻击性安全
www.offensive-security.com

使用 Kali Linux 2.0 

虽然通过查看源代码可以发现某些信息，但在这里似乎并不是这样。源代码看起来非常相似。

![](img/f99f528ca9845f4c256ce54e882b1345_829_0.png)

接下来，我们将运行 `dirb` 扫描来发现任何隐藏文件。Jenkins 在我们未登录时会响应为 403，这对于任何目录都是如此。

因此，我们将使用 `-w` 标志来进行扫描。

```
kali@kali~$ proxychains dirb http://10.5.5.25:8080/ -w

----------------------

TARGET          http://10.5.5.25:8080/

WORDLIST         :/usr/share/dirb/wordlists/common.txt

[OK] 200          http://10.5.5.25:8080/

[NOT FOUND] 404 http://10.5.5.25:8080/admin
```
