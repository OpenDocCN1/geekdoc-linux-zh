
选择什么是“可疑活动”无疑取决于程序及其输入，执行失败的输入显然是候选对象（例如包含 `NIL`）。不可能是通过正常使用产生的输入应该被记录，例如，在一个 `CGI` 程序中，某些必填字段以可疑的方式缺失。在许多情况下，任何包含类似 `/etc/passwd` 或 `/etc/shadow` 等短语的输入都是非常可疑的。同样，尝试访问 Windows `registry` 文件或 `.pwl` 文件也是非常可疑的。

不要在审计记录中记录密码。人们经常会不小心输入另一个系统的密码，记录密码允许系统管理员入侵其域之外的另一台计算机。

## 11.10. 物理发射

尽管这真的超出了本书的范围，但重要的是记住计算和通信设备会泄露大量信息，这使得它们变得不再安全。许多人知道 `TEMPEST` 要求，这些要求涉及计算机、显示器、键盘和其他组件的无线频率，这些频率可以被窃听。如果显示器的光线反射在远处的办公室墙壁上，也可以被窃听 [Kuhn 2002]。现代调制解调器足以判断底层通信内容。

## 11.11. 杂

以下是我似乎无法放入其他任何地方的杂项安全指南：

- 在程序使用其假设之前，至少检查一下这些假设（例如在程序开头）。如果你依赖于目录上设置的 `sticky` 位，请对其进行测试；此类测试花费的时间很短，并且可以防止严重问题。如果你担心每次调用执行某些测试的执行时间，请在安装时执行测试，或者更好在应用程序启动时执行测试。

- 如果你有一种构建脚本语言，该语言可能会设置一个对调用脚本的程序产生不利影响的环境变量。对此进行防御。

- 如果你需要一种配置语言，确保该语言具有字符集，并包含一些被注释掉的安全示例。通常使用 `#` 用于注释，意味着“该行的剩余部分是注释”。

- 如果可能，不要创建 `setuid` 或 `set root` 程序；让用户以 root 身份登录。

- 为你的代码进行签名。这样，其他人就可以检查发送的内容是否完整无误。

- 在某些应用程序中，你可能需要担心计时攻击，其中 CPU 利用率的变化是关键的。这种攻击已被用于从智能卡中获取密钥信息，例如：Mauro Lacy 发表了一篇名为《Remote Timing Techniques》的论文，显示你（在某些情况下）可以根据 CPU 消耗的工作量判断给定的用户 ID 是否（这可以使用论文中描述的技术进行检测）。处理此类问题的唯一方法是确保在不需要时也执行相同的工作量。问题是，在某些情况下可能会使系统更容易受到拒绝服务攻击，因为你无法进行优化。

- 考虑静态链接安全程序。通过确保安全程序不使用动态库，可以防止针对动态库机制的攻击。然而，这有几个缺点。这可能会增加磁盘和内存的使用（由于相同例程的多个副本）。更糟糕的是，这使得库更新（例如安全漏洞）变得更加困难——在大多数系统中，它们不会自动更新，必须独立跟踪。

- 在阅读代码时，考虑所有未匹配的情况。如果有 `switch` 语句，会发生什么？如果有 `if` 语句，会发生什么？

# 第 12 章 结论

> 事结终胜于事初，耐心胜于骄傲。
>
> 《传道书》7:8 (和合本)

在如 `Linux` 和 `Unix` 等类 Unix 系统上，设计并实现一个真正安全的程序实际上是一项艰巨的任务。困难之处在于，一个真正安全的程序必须对潜在敌对用户控制的所有输入和环境做出恰当响应。安全程序的开发者必须深入理解其平台，遵循安全和使用准则（如这些准则），并使用保证过程（如检查和其他同行评审技术）来减少程序的漏洞。

总结来说，以下是书中的一些关键准则：

- 验证你所有的输入，包括命令行输入、环境变量、`CGI` 输入等。不要仅仅拒绝 `bad`（错误的）输入；要定义什么是 `acceptable`（接受）输入并拒绝任何不匹配。

- 避免缓冲区溢出。确保长输入（以及较长的中间数据值）不会被用于接管你的程序。这是目前最主要的编程错误。

- 结构化程序内部。加固接口，最小化权限，使初始配置和默认值安全，并确保失败时安全（`fail safe`）。避免竞态条件（例如，通过在 `/tmp` 等共享目录中安全地打开任何文件）。只信任可信的通道（例如，大多数服务器不应信任客户端进行安全检查或其他敏感数据校验，如购买时的物品价格）。

- 谨慎调用其他资源。将它们的值限制在有效范围内（特别要关注元字符），并检查所有系统调用的返回值。

- 审慎地回复信息。特别是要最小化反馈，并对来自不可信用户的完整输出或无响应输出进行处理。

# 第 13 章 参考文献

智慧人的话语如羊群，聚集起来的言论如稳固嵌入的钉子——乃由一位牧者所赐。我的儿子，凡是这些以外的，都要你警备。书写得多，无穷无尽，过度的研读使人疲乏。

《传道书》12:11–12 (和合本)

请注意，书中重点强调了网络上的技术文章，因为大部分这类技术信息都可以在那里找到。

[Advosys 2000] Advosys Consulting (原名 Webber Technical Services)。编写安全的 Web 应用程序。http://advosys.com/tips/web-security.html

[Al-Herish 1999] Al-Herish. Thamer. 1999。安全 Unix 编程 FAQ。http://www.whitefang.com/sup.

[Aleph1 1996] Aleph1. 1996年11月8日。“为了乐趣和利润而粉碎栈”。Phrack 杂志，第 49 期，第 14 文章。http://www.phrack.com/search.php?view=p49-14 或 http://www.2600.net/phrack/ph4-49.html。

[Anonymous 1999] Anonymous. 1999年10月。最大安全性：黑客保护你的 Linux 服务器和工作站指南。 Sams。ISBN: 062316706。

[Anonymous 1998] Anonymous. 1998年9月。最大安全性：黑客保护你的网站和网络指南。第2版。ISBN: 0672313413。

[Anonymous Phrack 2001] Anonymous. 2001年8月11日。从（免费）。Phrack，第 09x ，第 03x 期，Phile #09 of 02。http://ptr.phrack.org/show.php?p=57&a=9

[AUSCERT 1996] 澳大利亚计算机应急响应小组 (AUSCERT) 和 O'Reilly。1996年5月23日（录 3C）。编写安全单元代码的工程师清单。http://ftp.auscert.org/pub/secure_checklist

[Bach 1986] Bach, Maurice J. 1986。操作系统设计。Englewood Cliffs, NJ: Prentice-Hall, ISBN-0-23-10799。

[Beattie 2002] Beattie, Steve, Stein Arnold, Crispin Cowan, Perry Wagle, Chris Wright, Adam Stockhardt, 2002。安全补丁的实现。LISA, Wiley，3–8。

[Bellovin 1999] Bellovin, Steven M. 1999年4月。“TCP/IP 协议的安全问题”。Communications Review 2:19, pp. 32–48。http://www.research.att.com/~smb/jpext.pdf

[Bellovin 1994] Bellovin, Steven M. 1994。编写（更多）安全软件。Murry Hill, NJ: AT&T。Linux 和 Unix 安全编程 HOWTO

[Bishop 1997] Bishop, Matt. 1997年10月。“编写特权程序”。Network Security 1997 New Orleans, LA。http://olympus.uc.edu/~bishop/secprog

[Blaze 1996] Blaze, Matt. Diffie, Ronald L., Bruce Schnee, Tsutomu Shimakura, Michael Weiner, 1996。“提供足够安全的最小密钥：密码学家和计算机科学家报告。http://ftp.research.att.com/dist/keylength.txt

[CC 1999] 通用标准 (CC)。1999。第 2.1 版。同于国际标准/IEC 15408。http://www.nist.gov/ccv2/clist

[CERT 1998] 计算机应急响应小组 (CERT) 协调中心 (CERT/CC)。1998年2月13日。CGI 中的用户数据清洗。CERT–97.25.CGI。http://www.cert.org/advisories/CA–97

[Cheswick 1994] Cheswick, William R. and Steven M. Bellovin.1994。防火墙和互联网安全：防御全面攻击。http://www.hacker.com
