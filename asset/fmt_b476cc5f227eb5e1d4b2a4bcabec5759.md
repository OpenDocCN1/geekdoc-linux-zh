
# 第4章 客户端攻击

将有一份通过客户端的所有活动日志。虽然 MitM Proxy 不在典型的 Web 渗透测试中作为活动组件使用，但在于真实环境中使用该包之前设置和测试 SET 时，它是非常有用的工具。在后面的章节中，我们将检查其他类型的代理；然而，我们喜欢 MitM Proxy 的原因是，作为一个渗透测试人员，通过直接连接到你的 Kali Linux 机器，它是测试攻击的一种简便方法。

## 主机扫描

访问主机系统的常用方法是识别并利用操作系统、已安装应用程序和其他程序中的漏洞。如 Nessus 等工具是评估系统漏洞的自动化方法。本节将介绍如何针对目标系统安装和运行 Nessus。利用将在第 3 章“服务器端攻击”中介绍，可用于利用 Nessus 识别出的漏洞。

### 使用 Nessus 进行主机扫描

Nessus 并没有随 Kali 预装。你需要针对目标系统运行 Nessus。免费版仅供个人使用，商业用途需要购买授权。

### 在 Kali 上安装 Nessus

Nessus 并没有随 Kali 预装。你需要将你的扫描器注册到插件库，我们将下载它。你需要针对目标系统安装和运行 Nessus。

1. 下载 Nessus。
2. 下载 Nessus 后，执行以下命令：
3. 将 `/tmp/opt/nessus` 复制到 `/opt` 目录；如果它不存在，请创建 `/opt`。
4. 你可以删除 `/tmp` 中的 Nessus 下载内容。
5. 为了启动 Nessus，执行命令：
6. 登录 Nessus 管理界面。

### 使用 Nessus

当你第一次登录 Nessus 时，会看到一些欢迎消息，并且会弹出一个 SSL 证书提示你正在连接到自签名证书。在一些说明性的屏幕之后，系统会提示输入激活码并下载最新插件。

你还将设置一个用户名和密码，用于管理 Nessus。以下截图显示了设置账户以及提供 Tenable 在注册后通过电子邮件提供的 Nessus 激活码的过程：

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_164_0.png)

初始下载插件需要一些时间，请耐心等待。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_165_0.png)

一旦所有更新下载并初始化，你将看到登录界面。使用你在初始安装期间设置的用户名和密码。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_165_1.png)

要扫描，点击顶部丝带上的 Scan（扫描）选项卡并选择 New Scan（新扫描）。系统会提示你输入目标的详情。你会被要求选择想要使用的模板。Nessus 内置的模板较少。在示例中，我们选择了外部网络扫描。

如果 Scan 选项卡不可，你也可以选择 Scan Templates（扫描模板）和 New Scan（新扫描）来创建新扫描。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_166_0.png)

选择 Create Scan（创建扫描）后，扫描将在指定的时间启动。默认计划将立即运行，因此在大多数情况下，扫描将立即开始。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_166_1.png)

扫描完成后，可以通过点击 Results（结果）选项卡查看结果。这将为管理员提供一份 Nessus 发现的报告。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_166_2.png)

我们可以像下面的截图所示，检查已完成的扫描以及目前任何活动扫描中收集到的任何结果：

| 结果标题 | 最后更新 | 状态 |
|---|---|---|
| Internal_web | 2013年5月09日 00:13:23 | 已完成 |
| securlyblogger.com | 2013年5月08日 00:12:20 | 运行中 |
| CloudCentrics | 2013年5月08日 00:04:44 | 运行中 |

作为渗透测试员，你必须关注任何漏洞。通过微软补丁或漏洞参考编号识别的漏洞可以在 Metasploit 框架中搜索，以便对目标主机使用利用程序。更多信息请参阅第3章“服务端攻击”中关于如何使用 Metasploit。

| 漏洞摘要 | | |
|---|---|---|
| CVE-0522: Microsoft Windows Task Scheduler Remote Overflow | Windows | 1 |
| CVE-0527: Vulnerability in SMB Allow Remote Code Execu... | Windows | 1 |
| CVE-0501: Microsoft Windows SMB Vulnerability Remote Code | Windows | 1 |
| CVE-0567: Microsoft Windows Server Service Crafted RPC | Windows | 1 |
| CVE-0326: Microsoft RPC-Interface Buffer Overrun (KB921596) (x... | Windows | 1 |
| CVE-0339: Microsoft RPC-Interface Buffer Overrun (KB924148) (x... | Windows | 1 |
| CVE-0457: ASNI 1 Vulnerability Could Allow Code Execution (02... | Windows | 1 |
| CVE-0111: Security Update for Microsoft Windows (KB32732) | Windows | 1 |
| CVE-0412: Cumulative Update for Microsoft RPC Runtime (KB32741) | Windows | 1 |
| CVE-0340: Vulnerability in Server Service Could Allow Reme... | Windows | 1 |
| CVE-0453: Vulnerability in Printer Spooler Service Could All... | Windows | 1 |
| CVE-0535: Vulnerability in Server Service Could Allow Remote... | Windows | 1 |
| CVE-0507: Vulnerability in Windows Could Allow Information D... | Windows | 1 |
| Microsoft Windows SMB NLLM Session Authentication | Windows | 1 |
| SMB Signing Disabled | Mac | 1 |

前面的示例显示了一些极其危险的漏洞（别担心，我们已经对系统进行了加固和修复）。所有这些漏洞都可以使用 Metasploit 或攻击工具来利用系统。要利用 Nessus 发现的漏洞，请参阅第3章“服务端攻击”中的 Metasploit。

Nessus 提供导出已识别漏洞详情的。你可以将结果导出为 HTML、CSV、PDF 以及许多其他常见文件类型。要导出结果，进入 Results（结果）部分并选择已完成的扫描。左侧的第三个选项卡提供了导出扫描选项，如两个截图所示：

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_168_0.png)

## 获取密码

获取密码最简单的方法是社会工程学。然而也有许多技术方法。本节将侧重于技术方法。

- 猜测：手动尝试密码。
- 字典：使用单词列表。
- 暴力破解：尝试所有组合。
- 混合攻击：字典和暴力破解的结合。
- 彩虹表：使用预计算的哈希来加速过程。

Windows 中常用的哈希是 NTLM。它是一个 128 位哈希。虽然它可以被破解，但比旧的 LM 哈希困难。

### Windows 密码

Windows 是常用的操作系统。微软引入了安全功能。目前的产品比旧版本更安全；但仍然受到攻击。

Windows 将密码存储在 `SAM`（系统账户管理）注册文件中。例外情况是使用了 Active Directory。Active Directory 是一个独立的认证系统，将密码存储在 LDAP 中。`SAM` 文件位于 `c\<systemroot>\sys32\config`。

> 注意，如果你在 Windows 中访问文件，你会修改其 MAC（修改、访问和更改），这是 Windows 记录你出现的方式。为了避免留存取证证据，建议在启动攻击之前复制目标主机系统。

### 挂载 Windows

有可用的工具可以获取 Windows 的 `SAM` 和 `SYSKEY` 文件。获取这些文件的一种方法是挂载目标 Windows 系统，以便其他工具可以在 Microsoft Windows 未运行时访问这些文件。

第一步是使用 `fdisk -l` 命令识别你的分区。你必须识别 Windows 分区和分区类型。`fdisk` 输出显示了一个 NTFS 分区，如下：
