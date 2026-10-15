

MANN, SCOTT, AND ELLEN L. MITCHELL. 《Linux 系统安全：开源安全工具管理员指南》（第 2 版）。新泽西州上萨德尔河：Prentice Hall PTR，2002 年。

MORRIS, ROBERT, AND KEN THOMPSON. “密码安全：一个案例研究。”《ACM 通讯》，22（11）：594–597，1979 年 11 月。转载于《UNIX 系统管理员手册》，4.3 伯克利软件发行版。加利福尼亚大学伯克利分校，1986 年 4 月。

RITCHIE, DENNIS M. “关于 UNIX 的安全性。”1975 年 5 月。转载于《UNIX 系统管理员手册》，4.3 伯克利软件发行版。加利福尼亚大学伯克利分校，1986 年 4 月。

SCHNEIER, BRUCE. 《应用密码学：C 语言中的协议、算法和源代码》。纽约，NY：Wiley，1995 年。

STEVES, KEVIN. “使用 HP-UX 11 构建堡垒主机。”HP Consulting。2002 年。tinyurl.com/5sfiy2

THOMPSON, Ken. “反思信任的信任”，载于《ACM 图灵奖演讲：前二十年 1966–1985》。马萨诸塞州雷丁：ACM Press（Addison-Wesley），1987 年。

练习从下一页开始。

## 22.19 练习

E22.1 讨论在使用密码时与使用密码短语和密钥对时 SSH 身份验证的强度。如果其中一种明显比另一种更安全，你是否应该自动要求使用更安全的身份验证方法？

★ E22.2 SSH 隧道通常是唯一能够将流量隧道到你没有管理员权限的远程机器的方法。阅读 ssh 手册页并编写一条命令行，将流量从 localhost 端口 113 隧道到 mail.remotenetwork.org 端口 113。你的隧道的转发点也应为主机 mail.remotenetwork.org。

★ E22.3 选择一起最近的安全事件并研究它。找到有关该事件的最佳信息来源，并找到适用于你实验室系统中适当的补丁或变通方法。列出你的来源和你为保护实验室而提出的操作。

★ E22.4 在获得本地系统管理员组的许可后，安装 John the Ripper，该程序用于搜索具有弱密码的登录名。
- a) 修改源代码，使其仅输出与弱密码关联的登录名，而不是密码本身。
- b) 在你本地实验室的密码文件中运行 John the Ripper（你需要访问 /etc/shadow），看看你能找到多少个可破解的密码。
- c) 将你的密码设置为一个字典单词，并只给 john 提供你在 /etc/shadow 中的条目。john 花了多长时间找到它？
- d) 尝试其他模式（大写字母、字典单词后跟数字、单字母密码等），以查看 john 到底有多聪明。

★★ E22.5 在计算机实验室中设置两台机器：一台目标机和一台探测机。
- a) 在探测机上安装 nmap 和 Nessus。用这些工具攻击目标机。你如何在目标机上检测到攻击？
- b) 在目标机上设置防火墙；使用 iptables 来防御探测。你现在还能检测到攻击吗？如果可以，如何检测？如果不能，为什么不能？
- c) 还可以设置哪些其他防御措施来抵御攻击？（需要 root 访问权限。）

★★ E22.6 使用常见的<|message|>安全邮件列表或网站，识别出最近遇到漏洞的应用程序。找到有关该漏洞的良好信息来源并讨论问题以及最好解决它们的方法。

### E22.7

Setuid 程序有时是必要的恶。但应避免使用 setuid shell 脚本。为什么？

### E22.8

使用 tcpdump 捕获主动和被动 FTP 会话的 FTP 流量。支持匿名 FTP 服务器的需求如何影响站点的防火墙策略？防火墙规则需要允许什么？（需要 root 访问权限。）

### E22.9

以下 iptables 输出中的规则允许和禁止什么？有哪些简单的补充可以增强安全性和隐私？（提示：OUTPUT 和 FORWARD 链可能需要更多规则。）

```
Chain INPUT (policy ACCEPT)
target  prot opt  source        destination
block   all  --  anywhere      anywhere

Chain FORWARD (policy ACCEPT)
target  prot opt  source        destination
all     --  anywhere      anywhere

Chain OUTPUT (policy ACCEPT)
target  prot opt  source        destination

Chain block (1 references)
target  prot opt  source        destination
ACCEPT  all  --  anywhere      anywhere      state RELATED,ESTABLISHED
ACCEPT  tcp  --  anywhere      anywhere      state NEW tcp dpt:www
ACCEPT  tcp  --  anywhere      anywhere      state NEW tcp dpt:ssh
ACCEPT  tcp  --  128.138.0.0/16 anywhere      state NEW tcp dpt:kerberos
ACCEPT  icmp --  anywhere      anywhere
DROP    all  --  anywhere      anywhere
```

### E22.10

检查本地防火墙的规则集。讨论你在政策方面发现了什么。有任何明显的漏洞吗？（此练习可能需要你本地站点安全负责管理员的合作。）

### E22.11

编写一个工具来确定站点上的任何网络接口是否处于混杂模式。定期在你的网络上运行它以便快速发现此类入侵。该工具会产生多少负载？你必须在每台机器上运行它，还是可以远程运行？你可以设计一个会告诉你接口是否处于混杂模式的隐蔽数据包吗？如果是，它是什么样的？（需要 root 访问权限。）

