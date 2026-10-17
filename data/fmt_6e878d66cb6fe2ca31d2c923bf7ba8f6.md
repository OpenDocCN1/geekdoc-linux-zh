
`Nmap done: 1 IP address (1 host) scanned in 6.8 seconds`

### 列表 97 - CVE-2021-41773 NSE 脚本

输出表明目标存在 `CVE-2021-41773` 漏洞，并我们提供了额外的背景信息。

虽然 `Nmap` 不是传统意义上的漏洞扫描器，但我们发现 `NSE` 是一个强大的工具，允许我们进行轻量级的漏洞扫描。在渗透测试中，当没有全功能的漏洞扫描器可用或当我们想要验证其他工具的发现时，我们可以使用 `Nmap`。

然而，在考虑任何其他漏洞扫描器时，我们有相同的考虑因素。`NSE` 脚本分类可以提供有用信息，例如脚本是侵入性的还是安全的，但我们也必须记住，`NSE` 脚本可能包含恶意代码，让攻击者获得我们系统的完全访问权限。出于因此，我们总是需要确保 `NSE` 脚本不仅提供功能，而且是安全的。

# 7.4 总结

本节提供了使用 `Nessus` 和 `Nmap` 进行漏洞扫描的概述，并介绍了漏洞扫描的不同类型和注意事项。

漏洞扫描在任何类型的评估中都非常有帮助。如果配置正确，漏洞扫描工具可以提供大量的意义数据。重要的是我们仍然需要手动审核结果，并且扫描器只能发现它们配置过的漏洞。最后，我们应该始终记住漏洞扫描工具可能会执行对网络或目标产生危害的操作，因此在使用它们时必须小心。

# Web 应用攻击简介

在本模块中，我们将涵盖以下学习单元：

- Web 应用评估方法论
- Web 应用枚举
- 跨站脚本 (`XSS`)

在本模块中，我们将开始介绍简化的 Web 应用攻击。现代开发框架和托管解决方案简化了构建和部署 应用程序的过程。然而，由于多个依赖项、不安全的服务器配置、代码不成熟以及业务漏洞，这些应用程序通常暴露了巨大的攻击面。

Web 应用使用多种编程语言和框架编写，每种语言都会引入特定类型的漏洞。由于常见漏洞在概念上是类似的，且各种框架无论底层技术栈如何都很相似，我们将遵循类似的利用路径。

# 8.1 Web 应用评估方法论

本单元涵盖以下学习目标：

- 理解 Web 应用安全测试
- 学习 Web 应用测试的不同类型和方法
- 了解 `OWASP Top10` 和常见的 漏洞

在讨论枚举和利用之前，让我们不同的应用程序渗透测试方法论。

作为渗透测试人员，我们可以根据提供的信息、来源和特定的参与规则，使用三种不同的方法评估 Web 应用。

白盒测试描述了对应用程序源代码、其所在的基础设施及其设计文档具有不受限制访问的情况。

黑盒测试（也称为零知识测试）不提供关于目标的任何信息。

灰盒测试发生在我们被提供有限信息时，包括身份验证方法、凭据或关于框架的细节。

# OffSec (离安全)

使用 `Kali Linux` 进行渗透测试

| 端口 状态 服务 版本 |
| :--- | :--- |
| 80/tcp 开启 | Apache 2.4.41 ((Ubuntu)) |

列表 列表 98 - 运行 `Nmap` 扫描以发现 Web 服务器主机。

我们的扫描显示 `Apache 2.4.41` 版本正在运行在 `Ubuntu` 主机上。

为了进一步进行枚举，我们使用了特定于服务的 `Nmap` `NSE` 脚本，例如 `http-enum`，它会对 Web 服务器进行初步的指纹识别。

```
kali@kali:$ sudo nmap -p80 --script=http-enum 192.168.50.20

Starting Nmap 7.92 (https://nmap.org) at 2022-03-29 06:30:26 EDT

Nmap scan report for 192.168.50.20

Host is up (0.10s latency).

PORT STATE SERVICE

80/tcp open http

| http-enum:

| /login/: Possible admin folder

| /db/: BlogWork Database

| /css/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)

| /db/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)

| /images/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)

| /js/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)

| /uploads/: Potentially interesting directory w/ listing on 'apache/2.4.41 (ubuntu)'

```

`Nmap done: 1 IP address (1 host up) scanned in 16.82 seconds`
列表 列表 99 - 对目标运行 `Nmap` `NSE` `http` 枚举脚本

如上所示，我们发现了几个有趣的文件夹，这些文件夹可以引导我们目标 Web 应用程序的更多细节。

通过使用 `Nmap`，我们成功发现了更多特定于应用程序信息，可以将这些信息添加到我们之前执行的 Web 服务器枚举中。

## 8.2.2 使用 Wappalyzer 识别技术栈

除了我们通过 `Nmap` 进行的主动收集，我们还可以通过 `Wappalyzer` 被动获取丰富的技术栈信息。

一旦注册免费账户，我们就可以对 `megacorpone` 域名进行技术查询。

> 342 (Wappalyzer, 2022), https://www.wappalyzer.com/

`PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.`

![](img/336d6ea891e7464f18ad64426619ced4_201_0.png)

### 技术栈

| 类别 | 技术 |
| :--- | :--- |
| 操作系统 | Debian |
| UI 框架 | Bootstrap |
| Web 服务器 | Apache |
| CDN | Google Hosted Libraries |
| 字体脚本 | Font Awesome |
| JavaScript 库 | jQuery, Modernizr, prettyPhoto |

> 图 81: Wappalyzer 发现结果

通过这种快速的第三方分析，我们了解了操作系统、UI 框架、服务器以及更多信息。发现还提供了关于 Web 应用程序使用的 JavaScript 库的信息——这些可能是非常有价值的数据，因为某些版本的 JavaScript 库已知会受到多个漏洞的影响。

## 8.2.3 使用 Gobuster 进行目录爆破

一旦在 Web 服务器上发现了运行的应用程序，我们的下一步是映射所有公共可访问的文件和目录。为了做到这一点，我们需要对目标进行多次查询以发现任何隐藏路径。`Gobuster` 是一个（用 `Go` 语言编写）工具，可以帮助我们进行此类枚举。它使用字典文件通过暴力破解来发现服务器上的目录和文件。

> 343 (OJ, 2022), https://www.kali.org/tools/gobuster/

`PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.`

由于其暴力破解的本质，`Gobuster` 会产生大量流量，这意味着在需要规避侦测时它将无用用处。

`Gobuster` 支持不同的枚举模式（模糊测试和 `dns`），但目前我们只依赖 `dir` 模式，它会枚举文件和目录。我们需要使用 `-u` 参数指定目标 `IP`，并使用 `-w` 指定字典文件。默认运行线程为 10；我们可以通过 `-t` 参数设置较低的值来减少流量。

```
kali@kali$ gobuster dir -u 192.168.50.20 -w /usr/share/wordlists/dir/common.txt -t 5
```

```
Gobuster v3.1.0

by O3 Reeves (@TheColonial) & Christian Mehlauer (@fireheart)
```

```
http://192.168.50.20/

GET

5

/usr/share/wordlists/dir/common.txt

404

gobuster/3.1.0

10

2022/03 05:16:21 Starting Gobuster in directory mode

.html (Status: 403)

.htaccess (Status: 403)

.htpasswd (Status: 403)

/css (Status: 301)

/db (Status: 301)

/images (Status: 301)

/index.php (Status: 301)

/js (Status: 301)
```
