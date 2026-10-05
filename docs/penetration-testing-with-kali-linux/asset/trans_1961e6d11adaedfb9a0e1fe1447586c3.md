
# OffSec

```
kali@kali:-$ mkdir beyond
kali@kali:-$ cd beyond
kali@kali:~/beyond$ mkdir mailsrv
kali@kali:~/beyond$ mkdir webserv1
kali@kali:~/beyond$ touch creds.txt
```

856 - 次渗透测试的基础工作环境

现在我们已经建立了工作环境，准备好对第一个目标机器 MAILSRV 进行枚举了。

> 记录你的发现是每次渗透测试中至关重要的过程。对于本模块，我们将结果存储在刚刚建立的基础工作环境中。然而，Markdown 编辑器（如 Obsidian¹¹⁷³）在实际评估中记录发现和数据已变得非常流行，因为它们独立于应用程序，并且包含简化编写和协作的功能¹¹⁷⁴。

等等，我看到原文中 "Let begin" 有拼写错误，我将其更正为 "Let's begin"。

让我们使用 Nmap 对 MAILSRV 进行端口扫描开始。端口扫描通常是我们要执行的第一种信息收集方法，用于获取开放端口和可用服务的概览。

> 在渗透测试中，我们还会使用被动信息收集技术，例如 Google Dorks 和泄露的密码数据库，来获取额外信息。这将为我们提供用户名、密码和敏感信息。

我们将使用 -sV 来枚举服务和版本检测，使用 -sC 运行 Nmap 的默认脚本。此外，我们将输入 -O 来创建一个包含扫描结果的输出文件。

```
kali@kali:~/beyond$ sudo nmap -sC -sV -on mailsrv1/nmap 192.168.50.242
Starting Nmap 7.92 (https://nmap.org) at 2022-09-29 08:53 EDT
nmap scan report for 192.168.50.242
host is up (0.1ms latency).
Not shown: 992 closed tcp ports (reset)
PORT STATE VERSION
25/tcp open smtp smtp-commands: MAILSRV1, SIZE 28488000, AUTH LOGIN, HELP
| 211 DATA HELLO EHLAO NOOP QUIPT RSET SAML TURN VRFY
80/tcp open http Microsoft IIS HTTP 10.0.0
/_http-title: IIS Windows Server
```

¹¹⁷³ (Obsidian, 2022), https.obsidian.md/
¹¹⁷⁴ (TrustedSec, 2021), https://www.trustedsec.com/blog/obsidian-taming-a-collective-consciousness/

# OffSec

| http-methods: |
| :--- |
| Potentially risky methods: TRACE |
|/_http-server-header: Microsoft-IIS/10.0 |
110/tcp pop3 hMailServer pop3d
|/_pop3-capabilities: UIDL USER TOP
135/tcp msrpc Microsoft Windows RPC
139/tcp netbios-sns Microsoft Windows netbios-sns
143/tcp imap hMailServer imap
|/_imap-capabilities: CHILDREN OK ACL IMAP4 completed CAPABILITY NAMESPACE
443/tcp microsoft-ds:
587/tcp smtp hMailServer smtp
|/_smtp-commands: MAILSRV1, SIZE 20480000, AUTH LOGIN, HELP
|/_ 211 DATA HELLO MAIL NOOP QUIT RCF SAML TURN VRFY
Service Info: Host: MAILSRV1; OS: Windows; CPE:o:microsoft:windows

Host script results:
|_ smb-time:
|_ date: 2022-09-29T12:54:00
|_ start_date: N/A
|_ smb2-security-mode:
|_ 3.1.
|_ Message signing enabled but not required
|_ clock-skew: 21

Service detection performed. Please report any incorrect results at https://nmap.org/submit/
Nmap done: 1 IP address (1 host) scanned in 37.95 seconds

列表867 显示 Nmap 发现了开放端口。根据这些信息，我们可以确定目标机器是一个运行 IIS Web 服务器和 hMailServer 的 Windows 系统¹¹⁷⁵。从客户提供的拓扑结构来看，这并不意外。

> 在真实的渗透测试中，主机名可能不像本模块中这样具有描述性。

由于我们可能不熟悉 hMailServer¹¹⁶，可以通过浏览应用程序的网页来研究它。我们了解到 hMailServer 是适用于 Microsoft Windows 的免费开源电子邮件服务器。

为了识别 hMailServer 中的潜在漏洞，我们可以使用搜索引擎来查找 CVE 和公开漏洞¹¹⁷⁷。然而，Nmap 没有发现版本号，我们必须进行更广泛的搜索。遗憾的是，除了某些 CVE 之外，搜索没有提供任何有意义的结果。

# OffSec. 使用 Kali Linux 进行渗透测试

## Hmailserver: 安全漏洞

| # | CVE | WID | # Exploits | Vulnerability Type(s) | Publish Date | Update Date | Score | Gained Access | Access | Complexity | Authentication | Conf. | Intrig. |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | CVE-2020-15719 | | | 2020-01-07 | | | None | Remote | High | Not required | None | Partial |
| 2 | CVE-2008-2562 | | | 2008-06-11 | 2018-08-31 | 4.1 | | Remote | Medium | Not required | None | Partial | |

图287. HmailServer 中的漏洞

如果我们有一个可以提供代码执行的匹配漏洞，就不应该跳过剩余的枚举步骤。虽然我们可能获得目标系统的访问，但可能会丢失其他服务系统的关键数据或信息。

接下来，让我们枚举 IIS 服务器。首先，我们将浏览网页。

![](img/336d6ea891e7464f18ad64426619ced4_808_0.png)

图288 显示 MAILSRV1 上显示了默认页面

图288 显示 IIS 显示了默认网页。让我们尝试使用 gobuster 来识别目录和文件。我们将输入 dir 进入目录模式，-u 指定 URL，-w 指定字典，-x 指定我们要识别的文件。在示例中，我们将使用 txt、pdf 和 config 来识别潜在的文档或配置文件。此外，我们将使用 -o 创建输出。

```
kali@kali:~beyond$ gobuster dir -u http://192.168.50.242 -w /usr/share/wordlists/dirb/common.txt -o mailsrv1 -x txt,pdf,config
```

¹¹⁷⁵ (hMailServer Homepage, 2022), https://www.hmailserver.com/
¹¹⁷⁶ (hMailServer Homepage, 2022), https://www.hmailserver.com/
¹¹⁷⁷ (CVE Details, 2022), https://www.cvedetails.com/vulnerability-list/vendor_id-8442/Hmailserver.html

