
## Burp

Burp 可用于向其他工具发送任何安全评估信息，并将被正确处理。

![](img/e4f93a89908ca3f498ee2517ddfbfd77_128_0.png)

图 4.9: 配置 Burp suite

### 3. 开始扫描

点击 Burp 界面内的新的 `Scan` 按钮以启动扫描。您还可以更改爬虫、审计和资源池的配置。爬虫将启动全面的爬取以收集信息，随后是自动化活动扫描过程。要开始扫描，输入目标网站的 `URL` 并点击确定，如图 4.10 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_128_1.png)

图 4.10: 开始扫描

### 4. 身份验证扫描

这允许对应用程序进行深度检查，并检测非身份验证扫描期间可能不存在的安全漏洞和其他问题。您可以在 Burp 中输入登录凭据，如图 4.11 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_129_0.png)

图 4.11: 身份验证扫描

### 5. 分析结果

扫描完成后，Burp 将呈现一份在目标网站上发现的漏洞报告。报告将包含每个漏洞的严重程度、描述以及修复建议，如图 4.12 所示。在 `Issue Activity` 部分有多种选项用于分析发现、探索问题详情以及影响端点。

## 网络

网络漏洞评估是一项全面的评估，旨在识别潜在的安全缺陷并评估公司网络安全的稳健性。该过程可以使用手动和自动化方法进行，以发现开放端口、识别服务及其版本，并根据相关的常见漏洞和披露（`CVE`）识别码编制漏洞列表。在本次演示中，我们将使用三个实用工具：`Nessus`、`Legion` 和 `Nmap`，以对网络漏洞过程的实际理解。

### 许可说明

在许可方面，`Nessus` 提供了多个版本以满足多样化的用户需求。作为本次演示的示例，我们有 `Nessus Essentials`，这是一个专门为个人和家庭使用设计的免费版本。然而，它具有某些局限性，最多允许扫描 16 个 `IP` 地址。另一方面，付费版本 `Nessus Professional` 提供了适用于中小型企业或个人安全专业人员的高级功能和能力。

### Nessus Essentials 使用步骤

要使用 `Nessus Essentials`，你可以遵循以下简单的方法：

#### 1. 下载并安装

首先访问 `Tenable` 网站（`https://www.tenable.com/downloads/nessus?loginAttempted=true`）并获取最新版本的 `Nessus Essentials`。按照图 4.13 提供的说明下载并安装软件：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_131_0.png)

#### 2. 创建用户账户

运行 `Nessus Essentials` 并仔细按照屏幕上的说明创建用户账户。此步骤对于获取基本许可密钥至关重要，如图 4.14 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_132_0.png)

![](img/e4f93a89908ca3f498ee2517ddfbfd77_132_1.png)

*图 4.14：创建用户账户*

![](img/e4f93a89908ca3f498ee2517ddfbfd77_132_2.png)

*图 4.15：创建新扫描*

#### 3. 创建新扫描

一旦软件安装完成，访问 `Nessus` 界面并导航到 `scans` 标签页。选择创建新扫描配置的选项，如图 4.15 所示：

#### 4. 自扫描设置

调整扫描设置以符合你的特定需求。在扫描配置中，你可以灵活选择各种扫描类型，例如基础网络扫描或 `Web` 应用程序扫描。此外，你还可以配置扫描策略、启用或禁用特定插件、设置扫描时间并进行其他必要的调整，如图 4.16 所示：

#### 5. 指定目标 IP 地址

在扫描配置中，指定你打算扫描漏洞所需的目标 `IP` 地址或范围。图 4.17 提供了此步骤的视觉指导。或者，你也可以从文件中导入 `IP` 地址列表。

![](img/e4f93a89908ca3f498ee2517ddfbfd77_133_0.png)

#### 6. 启动扫描

一旦你定制了扫描设置，点击 `Launch`（启动）按钮启动漏洞扫描。此操作如图 4.18 所示，将开始扫描过程：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_133_1.png)

![](img/e4f93a89908ca3f498ee2517ddfbfd77_134_0.png)

#### 分析扫描结果

完成后，在 `Nessus` 界面内审查看扫描结果。这些结果提供了有关已识别漏洞的全面信息，包括它们的严重程度、描述和修复建议。此外，你还可以生成各种格式的报告，如 `PDF`、`CSV` 和 `HTML`，如图 4.19 所示。

### 生成 CSV 报告

**报告格式：** `HTML` `PDF` `CSV`

| 列 | 另见 |
| --- | --- |
| 插件 ID | 插件输出 |
| `CVE` | `STIG` 严重性 |
| `CVSS v2.0` 基础分 | `CVSS v3.0` 基础分 |
| 风险 | `CVSS v2.0` 时间分 |
| 主机 | |
| 协议 | `CVSS v3.0` 时间分 |
| 端口 | `VPR` 评分 |
| 名称 | 风险因素 |
| 摘要 | 参考文献 |
| 描述 | 插件信息 |
| 解决方案 | 可利用工具 |

| 全选 | 清除 | 系统 |

生成报告

保存为默认

图 4.19：分析扫描结果

> 以前被称为 `OpenVAS` 的 `Greenbone` 漏洞管理 (`GVM`) 是一项著名的开源解决方案。它提供免费使用的 `GVM` 社区版和用于商业的 `GVM` 企业版，提供了全面的漏洞管理能力。

### Legion

它是一个开源、半自动的网络漏洞评估和渗透测试框架。其基于 `GUI` 的界面提供了广泛的自定义选项，并能够自动检测 `漏洞与披露 (CVEs)` 和 `通用平台枚举 (CPEs)`。`Legion` 包含了数百种工具和脚本以实现自动化扫描，包括 `Nmap`, `Hydra`, `WhatWeb`, `Nikto`, `SSLLyzer`, `SMBenum`, `Durbuster`, `Vulners` 和 `Webslayer`。让我们按照步骤了解如何配置扫描，并理解其功能：

#### 1. 在 Kali Linux 上安装 Legion

如果你的系统中尚未安装，可以轻松地下载并安装。

#### 2. 启动 Legion

一旦安装完成，启动应用程序并导航到主界面，如图 4.20 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_136_0.png)

#### 3. 配置扫描

从主界面，你可以配置设置，例如目标 `IP` 范围、端口范围和扫描类型。通过点击扫描部分的添加主机按钮并填写目标详情，选择在扫描期间运行的工具和脚本，如图 4.21 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_136_1.png)

#### 4. 启动扫描

配置完扫描设置后，按下提交按钮开始扫描。`Legion` 将执行工具和脚本，生成如图 4.22 所示的结果。

![](img/e4f93a89908ca3f498ee2517ddfbfd77_137_0.png)

图 4.22：启动扫描

#### 5. 分析结果

扫描完成后，你可以分析结果并进行处理，如图 4.23 所示：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_137_1.png)

图 4.23：分析结果

### Nmap

`Nmap` 是一个用于网络发现和安全审计的开源强大工具。它被用于发现网络上的主机、确定主机上运行的服务并识别操作系统。

```
nmap -sV -sC 192.168.1.129 -oN scanout.txt

Starting Nmap for 192.168.1.129

Nmap 7.91 (Nmap) at 2023-02-21 23:56 EST

Host is up (0.000s).

PORT STATE SERVICE VERSION

21/tcp open vsftpd 2.3.4

21/tcp open ftp-vsftd-backdoor vsftpd 2.3.4

State ENABLED (polite)

vsftpd version 2.3.4, this was reported on 2011-07-04.

Guidance date: 2018-10-28

Exploit results:

Results: user:root

References:

https://exploit-db.com/vulns/46899

https://www.cve.org/vuln/details/CVE-2011-2127/vsftpd-23_backdoored.html

https://www.cve.org/vuln/details/CVE-2011-2127

21/tcp open vulns:

cssl: openssl 7.8.1f https://www.vulners.com/securityvulns/SECURITYVULNS:8116

CVE-2018-5648 7.5 https://www.vulners.com/securityvulns/SECURITYVULNS:8116

CVE-2020-2640 5.0 https://www.vulners.com/cve/CVE-2020-2640

CVE-2005-2735 5.0 https://www.vulners.com/cve/CVE-2005-2735 **EXPLOIT*

CVE-2012-0814 3.5 https://www.vulners.com/cve/CVE-2012-0814

CVE-2019-1580 3.5 https://www.vulners.com/cve/CVE-2019-1580

CVE-2021-4327 2.1 https://www.vulners.com/cve/CVE-2021-4327

CVE-2002-2522 1.2 https://www.vulners.com/cve/CVE-2002-2522

SECURITYVULNS:VULN:9455 https://www.vulners.com/securityvulns/SECURITYVULNS:VULN:9455
```

图 4.26：写入输出

* **调整扫描计时**：`Nmap` 提供了一种简单的方法，其包含六种计时模板，可以通过 `-T` 选项通过其数字（0–5）或名称使用。前两个模板专为规避 `IDS`（入侵检测系统）设计。要使用模板 2（礼貌模式），请运行命令 `nmap -sV -T4 --script vuln <target>`，如图 4.27 所示。

模板的名称为：
* 妄狂 (`T0`)
* 狡猾 (`T1`)
* 礼貌 (`T2`)
* 正常 (`T3`)
* 激进 (`T4`)
* 剧烈 (`T5`)

```bash
# [root@]# nmap -sV -T4 192.168.149.129

Starting nmap with 1 target at 2023-02-22 08:00 UTC

Nmap scan report for host (0.00s latency)

Not all 100 ports are listed (confused)

PORT STATE VERSION

21/tcp open  vsftpd 2.3.4

- vsftpd 2.3.4

VULNERABLE:

  State: VULNERABLE (exploitable)

  CVE-2011-2523

vsftpd version 2.3.4, this backdoor was reported on 2011-07-04.

Discovery date: 2011

Exploit results:

  Small command execution: id(root)

References:

  https://github.com/vulncheck/framework-blaster/master/exploits/unix/vsftpd_234_backdoor.rb

  https://www.vulners.com/cve/CVE-2011-2523

  https://scarysecurity.blogspot.com/2011/07/backdoor-vsftpd-download-backdoored.html

22/tcp open ssh

- Ubuntu-OpenSSH 7.4p1

CVE-2018-15463 7.5 https://www.vulners.com/securityvulns/SECURITYVULNS:8136

CVE-2020-4488 7.5 https://www.vulners.com/cve/CVE-2020-4488

CVE-2019-5669 5.0 https://www.vulners.com/cve/CVE-2019-5669 **EXPLOIT*

CVE-2018-5107 5.8 https://www.vulners.com/cve/CVE-2018-5107

CVE-2011-0014 3.5 https://www.vulners.com/cve/CVE-2011-0014

CVE-2011-5800 3.5 https://www.vulners.com/cve/CVE-2011-5800

CVE-2011-4327 2.1 https://www.vulners.com/cve/CVE-2011-4327

CVE-2014-3156 2.2 https://www.vulners.com/cve/CVE-2014-3156

SECURITYVULNS:VULN:9455 0.0 https://www.vulners.com/securityvulns/SECURITYVULNS:9455
```

![](img/e4f93a89908ca3f498ee2517ddfbf77_141_0.png)

### 调节速度

`--max-parallelism` 和 `--min-parallel` 选项可控制 `Nmap` 扫描的速度。例如，防止 `Nmap` 同时发送多个进程。

另一种调节速度的方法是使用 `--scan-delay` 选项。要使用 `--min-parallel` 实例，请运行命令 `nmap -sV <target> --min-parallel 300`，如图 4.28 所示。

```bash
# [root@]# nmap -sV -T4 192.168.149.129 --min-parallel 300

Starting nmap with min-parallel option is high! This can help reliability.

Nmap scan report for host (0.00s latency)

Discovery date: 2023-02-22 08:00 UTC

Not all 100 ports are listed (confused)

PORT STATE VERSION

21/tcp open  vsftpd 2.3.4

- vsftpd 2.3.4

VULNERABLE:

  State: VULNERABLE (exploitable)

  CVE-2011-2523

vsftpd version 2.3.4, this backdoor was reported on 2011-07-04.

Discovery date: 2011

Exploit results:

  Small command execution: id(root)

References:

  https://github.com/vulncheck/framework-blaster/master/exploits/unix/vsftpd_234_backdoor.rb

  https://www.vulners.com/cve/CVE-2011-2523

  https://scarysecurity.blogspot.com/2011/07/backdoor-vsftpd-download-backdoored.html

22/tcp open ssh

- Ubuntu-OpenSSH 7.4p1

CVE-2018-15463 7.5 https://www.vulners.com/securityvulns/SECURITYVULNS:8136

CVE-2020-4488 7.5 https://www.vulners.com/cve/CVE-2020-4488

CVE-2019-5669 5.0 https://www.vulners.com/cve/CVE-2019-5669 **EXPLOIT*

CVE-2018-5107 5.8 https://www.vulners.com/cve/CVE-2018-5107

CVE-2011-0014 3.5 https://www.vulners.com/cve/CVE-2011-0014

CVE-2011-5800 3.5 https://www.vulners.com/cve/CVE-2011-5800
```

### Mobile Security Framework (MobSF)

`Mobile Security Framework (MobSF)` 是一个针对 `Android`、`iOS` 和 `Windows` 的综合自动化安全框架。`MobSF` 可以在运行时进行静态和动态分析。该框架由 `CapFuzz`（专门针对 `Web` `API` 的扫描器）驱动，也具有强大的模糊测试能力。分析结果以易访问的方式呈现在 `MobSF` 仪表板上，并可以下载进行进一步分析。让我们深入了解配置应用程序扫描并生成报告的步骤：

#### 1. 打开 MobSF

导航到 `MobSF` 文件夹并运行命令 `./run.sh`，如图 4.29 所示：

```bash
# [root@]# ~/Desktop
$ cd Mobile-Security-Framework/
# [root@]# ~/Mobile-Security-Framework/
$ ./run.sh
```
