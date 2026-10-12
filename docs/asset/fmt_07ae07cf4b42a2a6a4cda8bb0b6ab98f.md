
| Microsoft Windows Vista/7 - SMB2.0 Negotiate Protocol Request Blue Screen of Death (MS07-063) | windows/dos/0594.txt |

- Shellcodes: 无结果
- Papers: 无结果

包含搜索参数的漏洞将列在输出中。为了演示，让我们假设我们想要使用在渗透测试期间强调的两个漏洞。为了这次演示，我们枚举了受 SMBGhost 和 EternalBlue 影响的 SMB 服务器。

如果我们需要修改漏洞，可以使用 `-m` 选项将其复制到当前工作目录。将漏洞复制到当前工作目录的优点是更容易组织渗透测试中使用的漏洞，并将它们与测试的系统关联起来。

> 当发布新的 exploitdb 漏洞包时，所有漏洞都会被覆盖，在原始位置修改漏洞将导致我们丢失这些更改

让我们使用 `-m` 选项复制漏洞。我们可以使用这些漏洞的路径或 EDB-ID 来操作，这些信息可以在路径名称中找到。

```
kali@kali:$ searchsploit -m windows/remote/48537.py
```

# OffSec Microsoft Windows - 'SMBGhost' Remote Code Execution

Exploit: Microsoft Windows - 'SMBGhost' Remote Code Execution

URL: https://www.exploit-db.com/exploits/48537

Path: `windows/remote/48537.py`

File Type: Python script

```
kali@kali:$ searchsploit -m windows/remote/48537.py
```

# OffSec

使用 Kali Linux 进行渗透测试

该网站似乎是一家人工智能开发公司的网站。通过查看内容，我们在公司的“关于我们”页面上发现了一些员工信息以及他们的电子邮箱。

# 认识我们的团队成员！

首页 关于我们

![](img/336d6ea891e7464f18ad64426619ced4_466_0.png)

### Jeremy

Jeremy 是我们的团队负责人，负责确保开发工作符合我们的需求和预期。

他专注于一系列营销数据分析，并根据用户平台和行为进行针对性广告整合。

他于2020年加入公司。

jemy@OffSecCorp.org

![](img/336d6ea891e7464f18ad64426619ced4_466_1.png)

### Alex

Alex 是我们的首席开发人员，负责创建我们使用的人工智能算法。

他拥有机器人编程背景，并创造性地发现从火星采集的样本。

他于2019年10月加入公司。

alex@OffSecCorp.org

图 232：“关于我们”页面展示了员工、其邮箱以及入职年份

这些员工信息对我们目前没有用，而且我们没有在网站上发现任何安全漏洞或其他问题。让我们使用目录枚举工具扫描 Web 服务器上的任何隐藏目录。

运行目录枚举工具后，我们在网站上发现了一个项目目录。

![](img/336d6ea891e7464f18ad64426619ced4_466_2.png)

图 233：网站有一个登录门户

该网站有一个名为“AI 项目管理门户”的登录门户。在登录窗口下方，我们可以找到 Web 应用程序及其版本“qdPM 9.1”。如果我们无法在此处获取版本号，也可以检查网页的源代码以获取 Web 应用程序及其版本号。

```
<div class="copyright">
<a href="http://qdpm.net" target="_blank">qdPM 9.1</a></a><br /> Copyright &copy;
2022 <a href="http://qdpm.net" target="_blank">qdpm.net</a></a>
</div>
```

列表 364 - 版本在源代码中可见

Web 应用程序及其版本位于源代码页面的底部。通过进一步调查，我们可以确定这是一款免费基础的项目管理软件。

有了这一新发现，我们在 Exploit DB 中搜索了“qdPM 9.1”的远程漏洞，并发现了几个相关的结果。

![](img/336d6ea891e7464f18ad64426619ced4_467_0.png)

| DB-ID | CVE | Author | Type | Platform | Date |
|---|---|---|---|---|---|
| Verified | | | UPDATED | PHP | 2022 |
| Exploit: 1 | | | | Vulnerable App (?) | |

图 234：显示了漏洞利用详情

检查最新的漏洞，我们确定它符合我们的搜索结果：它是经过验证的、远程的，并且允许远程代码执行。在执行之前，我们将审查该漏洞并对其基本了解。

该漏洞需要项目管理 Web 应用程序的用户名和密码。审查代码后，我们可以得出登录页面的用户名字段是一个电子邮件地址。我们找到了几个邮箱，但没有发现暴露的密码。有了 Web 应用程序的有效凭据，该漏洞将上传一个命令 shell，可以使用它在目标上执行命令。

另一种获取账户密码的方法是使用网站上的列表生成器。生成列表后，我们可以直接尝试列表，或进行修改以创建更复杂的密码。

> 729 (qdPM, 2022), https://qdpm.net/
> 729 (Exploit DB, 2022), https://www.exploit-db.com/exploits/50944

对登录门户使用四个四个邮箱进行字典攻击，我们可以验证 george@AIDevCorp.org 是 George 账户的有效凭据。

![](img/336d6ea891e7464f18ad64426619ced4_468_0.png)

图 235：使用 George 的账户登录项目管理应用程序

成功登录系统后，我们可以枚举任务以及项目管理系统的某些配置。由于我们发现了一个需要凭据的漏洞，现在可以针对目标执行该漏洞。

我们将使用 searchplot 将漏洞复制到当前目录。

```
kali@kali:~ searchplot -m 50944
Exploit: qdp 9.1 - Remote Code Execution (RCE) (Authenticated) (v)
```

测试。收集漏洞利用使用详情所需的任何信息至关重要，正如我们在使用漏洞利用程序时所使用的登录凭据。

让我们通过以下练习来练习所学的内容。

## 15.5 总结

在本模块中，我们检查了运行由不可信作者编写的代码相关的风险。我们还讨论了托管已知漏洞漏洞利用代码的各种在线资源，以及不需要互联网连接的离线资源。最后，我们涵盖了一个场景，展示了如何利用此类在线资源为针对目标枚举阶段发现的软件版本寻找公开漏洞。

## 16 Windows 权限提升

在本学习模块中，我们将涵盖以下学习单元：

- 举举 Windows
- 利用 Windows
- 滥用其他 Windows 组件

在渗透测试期间，我们通常以非特权用户的身份在 Windows 系统上获得初始立足点。然而，我们通常需要管理员权限来在其他用户的目录中搜索敏感信息、检查系统上的配置文件，或使用 Mimikatz 提取密码哈希.³⁷³⁰ 从非特权到特权提升权限和访问的过程被称为权限提升（Privilege Escalation）³⁷³¹

虽然本模块侧重于此，下一个模块将探索 Linux 系统上的权限提升技术。一旦完成两者，我们不仅将理解这两个操作系统的安全模型和攻击面的差异，还将了解如何在每个系统上利用权限提升向量。

在本模块中，我们将介绍 Windows 权限和访问控制机制。然后，我们将介绍如何通过收集信息来在目标系统上建立态势感知。基于这些信息，我们将执行各种权限提升攻击。首先，我们将在系统中搜索用户和操作系统留下的敏感信息。接下，我们将学习如何滥用 Windows 服务来尝试权限提升攻击。最后，我们将审查 Windows 的其他组件，这些组件允许我们通过计划任务（Scheduled Tasks）提升权限.³⁷⁷² 最后，我们将调查漏洞利用的使用。

### 16.1 理解 Windows Windows

此学习单元涵盖了以下学习目标：

- 理解 Windows 权限和访问控制机制
- 获取态势感知
- 在 Windows 系统上搜索敏感信息
- 查找由 PowerShell 生成的敏感信息
- 熟悉自动化枚举工具

每个目标都可能由于操作系统版本、补丁级别、系统配置等差异而是唯一的。因此，我们理解如何获取和利用有关目标系统的信息以实现权限提升非常重要。为了完全掌握 Windows 的攻击向量，我们首先需要熟悉 Windows 权限结构和访问控制机制。

> ³⁷⁰ (Github, 2022), https://github.com/gentilki/wiki/mimikatz
