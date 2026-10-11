
# Linux 词典

GNU 项目使用 `texinfo` 格式作为其大部分文档。`info` 包提供了一个独立的 TTY 浏览器，用于查看 `texinfo` 文件。你应该安装 `info`，因为 GNU 的 `texinfo` 文档是系统软件信息的重要来源。来自 Mandrake 9.0 RPM `http://www.tldp.org/LDP/Linux-Dictionary/html/index`

## info page

`info` 页面提供了命令或文件的详细信息（`man` 页面则要求简短且解释较少）。`info` 页面具有交互性，带有导航菜单系统。访问一个

带有 `info` 命令的帮助页，来自 RedHat 词汇表

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## info2www

使用 WWW 浏览器读取文件。`info2www` 让你通过 WWW 浏览器读取 `info` 文件。它需要一个支持 CGI 的 HTTP 服务器。来自 Debian 3.0r0 APT

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## Infobot (或 mailbot)

一个可以自动返回用户请求信息的电子邮件地址。来自远程教育与互联网术语词表

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## infobserver

读取 `info` 文档。来自 `what`

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## infocmp

比较或打印 `info` 描述。来自 `Whatis`

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## inform-mode

用于编辑 Info 的 Emacs 模式。这是一个用于编辑 `info` 源代码的 XEm 模式。`Inform` 用于为 Z-Code 虚拟机（一种 Incom）编写游戏。此包将为你的 Emacs 添加一个用于编辑文件的模式。来自 Debian 3.0r0 APT

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## INFOSEC

安全

对比：“信息安全”一术语与“物理安全”区分开来。关键点：用于描述安全的常用标准是 OSI/ISO/IEC 10181 标准。它将信息安全细分为以下领域：

- 身份验证 (`Authentication`)：人们证明自己身份的地方。
- 访问控制 (`access control`)：人们允许访问计算机或文件的地方。
- 不否认性 (`non-repudiation`)：确保交易双方都无法否认交易的发生。（反义词：声誉 `reputation`/随机数 `nonce`）
- 机密性 (`confidentiality`)：防止未经授权的信息泄露。（反义词：泄露 `disclosure`）
- 完整性 (`integrity`)：确保事物不被损坏。（反义词：损坏 `corruption`、篡改 `tampering`）
- 审计与告警 (`audits and alerts`)：跟踪正在发生的事情。
- 可用性 (`availability`)反义词：拒绝服务 `Denial-of-Service)`
- 可追责性 (`accountability`)：确保人们对自己的行为负责。（反义词：匿名 `anonymity`）。这包括发现违反安全策略的行为，以及因使用网络资源而变更部门。

关键点：最常见的威胁是：

- 披露被泄露给未经授权的人员。
- 完整性违规：数据被篡改，例如账户余额被更改、伪装/伪造。
- 安全：假装安全或生成一条伪装成来自自己的消息。
- 来自人们惩罚你的拒绝服务攻击。
- 后门/特木马。

关键点：信息安全和黑客领域并不一定相关。后者拥有一个打破规则的领域。例如，通过遵循信息安全的最佳实践，你可以验证服务器是安全的、数据是加密的，并且只有经过授权的用户才能访问。然而，一个黑客可以执行缓冲区溢出漏洞来绕过所有安全措施。

军事连接必须包含 `COMSEC` – 通信安全，描述来自敌人的通信。反义词是 `COMINT`（通信情报）。来自黑客词汇表

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## infotoc

将术语定义转换为 `termcap` 描述。来自 `Whatis`

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## ingerman

用于 `is` 的新德语词典。这是一个用于 `isspell` 的新德语拼写法的词典。它基于由 Heinz Knutzen 的著名的 `hkgerman` 词典（使用旧德语拼写法），并作为 Debian 包 `icager` 提供。来自 Debian 3.0r0 APT

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## INGRES

交互式图形检索系统 (`Interactive Graphic Retrieval System`)。来自 `VERA`

`http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

## INHOPE

欧洲互联网热线供应商（组织，ISP）。来自 `VERA`

`http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

## inimf

`Metafont`，一种用于字体和 Logo 设计的语言。来自 `Whatisn`

`http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

## inimpost

`MetaPost`，一个用于设计图片的系统。来自 `Whatisn`

`http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

## iniomega

扩展 `unicode` 的 TeX。来自 `Whatis`

`http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

## init

`init` 是内核启动的第一个用户进程。`init` 有许多职责，例如启动 `getty`（使用户可以登录）、实施规则以及处理孤儿进程。`init` 是 Linux 系统运行至关重要的进程之一，但你仍然可以管理它。通常在你连接终端或想要更改默认级别时，可能需要担心 `init`。当内核启动（启动）后，`init` 已经启动（加载了），并启动了 `getty`（使用户可以登录），实施了规则并处理了孤儿进程。`init` 位于 `/sbin/init`。当内核启动后，`init` 运行了 `/sbin/init`，完成了初始化并关闭了终端。`init` 运行了初始化。当内核启动后，`init` 已经运行，完成初始化。当内核启动后，`init` 已经运行，完成了初始化。当内核启动后，`init` 已经运行，完成了初始化。当内核启动后，`init` 已经运行，完成了初始化。当内核启动后，`init` 已经运行，完成了初始化。当内核启动后，`init` 已经运行，完成了初始化。当内核启动后，`init` 已经运行，完成了初始化。当内核启动后，`init` 已经运行，完成了初始化。当内核启动后，`init` 已经运行，完成了初始化。`init` 位于 `/sbin/init`。

## infobserver

读取 `info` 文档。来自 `what`

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## infocmp

比较或打印 `info` 描述。来自 `Whatis`

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## inform-mode

用于编辑 Info 的 Emacs 模式。这是一个用于编辑 `info` 源代码的 XEm 模式。`Inform` 用于为 Z-Code 虚拟机（一种 Incom）编写游戏。此包将为你的 Emacs 添加一个用于编辑文件的模式。来自 Debian 3.0r0 APT

`http://www.ldp.org/LDP/Linux-Dictionary/html/index.html`

## INFOSEC

安全

对比：“信息安全”一术语与“物理安全”区分开来。关键点：用于描述安全的常用标准是 OSI/ISO/IEC 10181 标准。它将信息安全细分为以下领域：

- 身份验证 (`Authentication`)：人们证明自己身份的地方。
- 访问控制 (`access control`)：人们允许访问计算机或文件的地方。
- 不否认性 (`non-repudiation`)：确保交易双方都无法否认交易的发生。（反义词：声誉 `reputation`/随机数 `nonce`）
- 机密性 (`confidentiality`)：防止未经授权的信息泄露。（反义词：泄露 `disclosure`）
