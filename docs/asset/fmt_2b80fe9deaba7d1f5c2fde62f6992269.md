
Nmap 端口扫描完成 -- 在 12 秒内扫描了 1 个 IP 地址 (1 个主机)

通过 FTP 服务器进行 Nmap 端口扫描比普通端口扫描慢，因为 Nmap 完全没有控制包范围的能力，而是必须依赖 FTP 服务器的完整 TCP 三次握手。这意味着 Nmap 无法并行扫描端口，除非你编写脚本让 Nmap 为不同的端口范围向 FTP 服务器建立多个连接。

# FTP 弹跳扫描攻击 (FTP Bounce Scan) 应对措施

许多 FTP 服务器的出站连接源端口为 20，即 `ftp-data` 端口。如果你阻止从源端口 20 到你服务器的连接，那么就可以防止你的机器被 FTP 弹跳扫描。当然，你也可能阻止合法的 FTP 流量。

```
# 针对 2.2 内核：
ipchains -A input -i eth0 -p tcp -d $ME -s 0/0 20 www -j DENY

# 针对 2.4 内核：
iptables -A INPUT -i eth0 -p tcp -d $ME -s 0/0 --dport 20 -j DENY
```

注意 (`CAUTION`) 然而，实际上并不是所有的 FTP 服务器都使用端口 20 作为源端口，因此这不是万无一击的解决方案。

# 暴露的 Linux：Linux 安全与解决方案

以下是 FTP 服务器在 Nmap 扫描期间记录的条目：

```
command: USER username
<--- 331 username 需要密码
command: PASS password
<--- 230 用户 username 已登录。
FTP LOGIN FROM hacker_box.com [192.168.2.2], username
command: PORT 172,16,217,202,23,112 #端口 6000
<--- 200 PORT 命令成功。
command: LIST
<--- 425 无法建立数据连接：连接被拒绝。
command: PORT 172,16,217,202,21,124 #端口 5500
<--- 200 PORT 命令成功。
command: LIST
<--- 425 无法建立数据连接：无法分配请求地址。
command: PORT 172,16,217,202,23,12 #端口 5900
<--- 200 PORT 命令成功。
command: LIST
<--- 150 正在为 /bin/ls 开启 ASCII 模式数据连接。
<--- 226 传输完成。
command: PORT 172,16,217,202,22,168 #端口 5400
<--- 200 PORT 命令成功。
command: LIST
<--- 150 正在为 /bin/ls 开启 ASCII 模式数据连接。
<--- 226 传输完成。
<--- 200 PORT 命令成功。
command: LIST
<--- 150 正在为 /bin/ls 开启 ASCII 模式数据连接。
<--- 226 传输完成。
<--- 221 你至少可以说再见。
FTP 会话关闭
```

我们在 PORT 行的末尾添加了端口号以便阅读。使用 `ftpd -1lvLaio` 中的参数为 FTP 服务器 (`wu-ftpd`) 开启了完整调试。

客户端的 IP 地址为 `192.168.2.2`。然而，PORT 命令将 FTP 服务器指向了 `172.16.217.202`，即实际扫描目标。大量的 `425` 错误信息（连接失败）表明某些异常。请使用你的日志分析工具关注这些错误。

大多数 FTP 服务器现在已配置为拒绝除 FTP 客户端机器以外的 IP 地址的 PORT 命令，尽管它们实现这个简单的更改花费了一段时间。例如，“Hobit”在 1995 年 7 月在 Bugtraq 的一个帖子中写过这个问题，但 `wu-ftpd` 直到 1999 年 10 月才实现解决方案。

因此，你应该手动检查以确保你的 FTP 服务器已配置为拒绝不当的 PORT 选择。这里有一种检查你系统的快速方法：

```
machine$ cat ftp.bounce.detect
USER username
PASS password
PORT 127,0,0,1,10,10
LIST
QUIT
```

```
machine$ nc ftpserver 21 < ftp.bounce.detect
220 欢迎来到我们的 FTP 服务器。祝你有愉快的一天！
331 username 需要密码。
230 用户 username 已登录。
200 PORT 命令成功。
425 无法建立数据连接：连接被拒绝。
221 你在 0 个文件中传输了 0 字节。
221 此会话的流量流量为 92 字节。
221 再见。
```

在示例中，服务器容易受到弹跳攻击，正如“425 无法建立数据连接：连接被拒绝”行所示。这表明机器实际上尝试联系 PORT 命令中列出的主机/端口。大多数配置适当的 FTP 服务器将给你一个不同的错误信息，或者更有可能立即断开连接，如下所示：

```
machine$ nc anotherftpserver 21 < ftp.bounce.detect
220 欢迎来到我们的 FTP 服务器。祝你有愉快的一天！
331 username 需要密码。
230 用户 username 已登录。
```

# 攻破解 Linux 解析：安全秘密与解决方案

```perl
open NC, "nc Hostname 21" or die "Can't fork netcat";
NC->autoflush(1);

print NC "USER $username\nPASS $password\n";
for ( 1..10 ) { sleep 1; print NC "PASV\n"; }
print NC "QUIT\n";
```

只需运行该程序并检查输出：

```
machine$ pasv_ports.pl anonftpserver
已打开被动端口：
8273 8274 8276 8277 8279 8280 8281 8282 8283 8285
```

```
machine$ pasv_ports.my ftpserver username password
已打开被动端口：
41715 5982 35909 51887 42917 1541 24804 47636 6144 29254
```

第一台服务器使用顺序端口号。序列中偶尔出现的断开是因为其他用户建立了 PASV FTP 连接。然而，第二台机器显然是以随机方式生成端口的。如果你的服务器使用顺序端口，请更新到最新版本，或者如果你计划支持 PASV FTP，请切换到不同的 FTP 服务器。

为了能够通过防火墙或路由器的访问控制列表（ACL）支持 FTP，FTP 服务器通常被配置为仅对 PASV FTP 使用一小范围的端口。这缩小了黑客需要尝试的端口范围。讽刺的是，为了防火墙安全限制 PASV 端口反而让数据劫持变得更容易，因为黑客需要连接的端口更少了。

避免 PASV 数据劫持的一种方法显然是不使用被动 FTP。然而，FTP 客户端默认使用主动 FTP，但你可以通过运行 `ftp -p hostname` 或 `pftp hostname` 客户端来强制进入被动模式。

# PORT FTP 数据劫持

| 流行度 | 3 |

| :--- | :--- |

| 简单性 | 3 |

| 影响 | 5 |

| 风险等级 | 4 |

# 第 11 章：邮件与 FTP 安全

主动 FTP 的劫持方式与被动 FTP 非常相似。数据端口不是在 FTP 服务器上打开，而是在 FTP 客户端上，正如 FTP 命令中指定的那样。然而，这种攻击对黑客的吸引力较小。他们很容易选择一个 FTP 服务器，并认定其中有你想访问的数据，然后尝试获取 PASV 端口以期获得某些东西。但是，尝试通过攻击 FTP 客户端来获取那些数据并不简单。

首先，攻击者必须知道哪些 FTP 客户端正在访问该 FTP 服务器。这些信息显然在 FTP 服务器本身上可用，但如果攻击者能够直接访问 FTP 服务器，他已经获得了访问 FTP 数据的权限。因此，这需要大量的猜测。

> 黑客可能能够获取到哪台机器正在访问 FTP 服务器，这并不遥不可及。例如，某位员工想要访问其他部门访问的内部 FTP 服务器上的机密人力资源（HR）或薪资账单文件。

# PORT FTP 劫持防御措施

你可以通过运行以下命令模拟攻击，以测试 FTP 客户端是否存在漏洞。由于尝试在 PORT 和 LIST 命令之间插入我们的数据的暴力破解失败，并不能断判定客户端是安全的，我们将手动伪造一个 FTP 连接，并控制 PORT 和数据传输命令的时机。我们求助于朋友 Netcat：
