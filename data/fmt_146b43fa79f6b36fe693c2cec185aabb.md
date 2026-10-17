
```
$ dig 8.3 apple.com
;; options: init
;; got answer:
;; -- opcode, status:NOERROR, id: 2
;; flags: qr ra; QUERY: 1, ANSWER: 1, AUTHORITY: 6
;; QUERY SECTION:
    apple.com., type = A, class = IN

;; ANSWER SECTION:
apple.com. 54m26s In A 17.254.3.183

;; AUTHORITY SECTION:
apple.com. 1d23h59m11s NS nserver4.apple.com.
apple.com. 1d23h59m11s NS nserver.asia.apple.com.
apple.com. 1d23h59m11s NS nserver.euro.apple.com.
apple.com. 1d23h59m11s NS nserver.apple.com.
apple.com. 1d23h59m11s NS nserver2.apple.com.
apple.com. 1d23h59m11s NS nserver3.apple.com.

;; ADDITIONAL SECTION:
nserver.asia.apple.com. 23c5h59m11s In A 203.120.14.5
nserver.euro.apple.com. 23h559m11s In A 17.720.133.64
nserver.apple.com. 4d23h59m11s In A 17.254.0.50
nserver2.apple.com. 4d23h59m11s In A 17.254.0.59
nserver3.apple.com. 4d23h59m11s In A 17.112.144.50
nserver4.apple.com. 4d23h59m11s In A 17.112.144.59
```

```
;; Total query time: 221 msec
;; FROM: Walden.local, to SERVER: -- 193.252.192.3
;; WHEN: Thu Jun 19 19:07:39 2003
;; MSG SIZE sent: 27 rcvd: 284
```

此命令返回域名的 IP 地址、名称服务器以及它们的 IP 地址。使用这些命令的主要目的是查找你是否正在尝试连接主机，或者主机是否因为 DNS 原因无法访问——可能是因为它们没有续订（这种情况会发生），或者你的 DNS 服务器找不到它们。

`host` 命令非常简洁，仅提供你所检查域名的 IP 地址以及任何别名：

```
$ host www.apple.com
www.apple.com is an alias for www.apple.com.akadns.net
www.apple.com.akadns.net has address 17.112.152.32
```

与其他网络实用一样，这些命令有很多选项，包括搜索特定类型信息的可能性。更多信息请参阅 `nslookup` 的 man 页面。

## nslookup 命令概述

### 命令语法

```
nslookup [option(s)] host
dig [option(s)] host
host [option(s)] host
```

#### Finder 等效项

网络实用工具（Network Utility）的“查找”（Lookup）选项卡。

## nslookup 选项概述

- - `nslookup` `nslookup` 命令返回指定主机的 DNS 信息。
- `dig` `dig` 命令返回指定主机的 DNS 信息。
- `host` `host` 命令返回指定主机的 DNS 信息。

### 获取更多信息

要显示帮助页面并了解更多关于这些命令的信息，请在终端中输入 `man command_name`。

## 使用 traceroute 追踪数据包

诊断网络问题的另一个有用工具是 `traceroute`。此命令向你的计算机与选定主机之间的每一个跳发送数据包，并返回这些机器响应的 IP 地址和时间。这是一个示例：

![](img/6906cb53af244b9a7484b2b812444bde_377_0.png)

在这个示例中，我为 www.google.com 运行了 `traceroute`。路径上的每一跳都会响应，但最后一个没有——这可能是因为设置了防火墙不响应 `traceroute` 数据包。`traceroute` 命令对于发现网络问题发生在哪里非常有。如果你无法获取某个点之后的数据，显然该位置存在问题。它对于诊断互联网和本地网络的问题很有用。

## 命令行界面

### traceroute 命令概述

### 命令语法

```
traceroute [option(s)] host
```

#### Finder 等效项

网络实用工具（Network Utility）的“追踪”（Traceroute）选项卡。

## traceroute 选项概述

- `traceroute` `traceroute` 命令返回数据在两个主机之间路径的信息。

### 获取更多信息

要显示帮助页面并了解更多关于 `traceroute` 的信息，请在终端中输入 `man traceroute`。

## 使用 whois 获取域名信息

`whois` 命令让你查找有关主机的信息，例如谁拥有该域名、他们的名称服务器等。`whois` 命令非常简单且返回的信息有限。这是一个 `whois` 命令运行的示例：

```
$ whois apple.com
```

Whois Server Version 1.3

```
[...]
Domain Name: APPLE.COM
Registrar: EMARKMONITOR INC. DBA MARKMONITOR
Whois Server: whois.markmonitor.com
Referral URL: http://www.markmonitor.com
Name Server: NSERVER2.APPLE.COM
Name Server: NSERVER.EURO.APPLE.COM
Name Server: NSERVER.ASIA.APPLE.COM
Name Server: NSERVER3.APPLE.COM
Name Server: NSERVER4.APPLE.COM
Status: REGISTRAR-LOCK
Updated Date: 20-may-2004
Creation Date: 19-feb-1987
Expiration Date: 20-feb-2007
[.]
```

## 命令行界面

### whois 命令概述

### 命令语法

```
whois [option(s)] host
```

#### Finder 等效项

网络实用工具（Network Utility）的“Whois”选项卡。

## whois 选项概述

- `whois` `whois` 命令返回指定主机的域名注册信息。

### 获取更多信息

要显示帮助页面并了解更多关于 `whois` 的信息，请在终端中输入 `man whois`。

如你所见，它提供的信息比域名注册日期（苹果的域名已经很久了！）、更新日期和过期日期，以及注册商和域名的名称服务器。`whois` 返回的数据还会提供更具体的信息，例如名称服务器的 IP 地址等。

## 使用 finger 获取用户信息

`finger` 命令提供有关你系统中拥有账户用户的基本信息。其语法为：

- `finger user`

以下是关于该用户的显示：

```
$ finger kirk
Login: kirk Name: Kirk McElhorn
Directory: /Users/kirk Shell: /bin/bash
On Wed May 31 13:23 (CEST) on console, idle 1 day 21:17 (messages off)
On Wed 2 Jun 08:58 (CEST) on tty1
Last login Wed 2 Jun 10:32 (CEST) on tty2
No Mail.
No Plan.
```

你可以获取系统上任何其他用户的类似信息，或者如果远程主机上运行了 `finger` 服务器，可以获取关于另一台计算机的用户的信息。要获取远程用户的信息，请运行命令：

```
finger user@host
```

大多数组织都会关闭 `finger` 服务器，因此你无法获取这样的远程用户信息。Mac OS X 就是这种情况。如果你想开启它，请参见本章前面的“启用 Telnet”侧边栏。你可以使用侧边栏描述的相同启用 `finger`。

## 命令行界面

### finger 命令概述

### 命令语法

```
finger user@host
```

#### Finder 等效项

网络实用工具（Network Utility）的“finger”选项卡。

## finger 选项概述

- `finger` `finger` 命令返回指定用户的信息。

### 获取更多信息

要显示帮助页面并了解更多关于 `finger` 的信息，请在终端中输入 `man finger`。

## 扫描端口

扫描端口用于发现主机上运行了哪些服务。这也可以用于安全审计，查看是否有未经授权的服务暴露在网络中。在示例中，我们使用 `nmap` 命令扫描本地机器的端口。

```
$ nmap localhost
```

`nmap` 的输出如下：

```
Starting scan for localhost (127.0.0.1)
Host scan report for 127.0.0.1
1 scan took 0.01 seconds
69 ports open (tcp)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
53/tcp   open  dns
110/tcp  open  pop3
139/tcp  open  netbios
143/tcp  open  imap
443/tcp  open  https
548/tcp  open  microsoft-ds
80/tcp   open  http
8080/tcp  open  http-proxy
```

`nmap` 命令是一个强大的网络发现和安全审计工具。它有很多选项，但我们将使用基础选项。更多信息请参阅 `nmap` man 页面。

## 使用 whois 获取域名信息

`whois` 命令让你查找有关主机的信息，例如谁拥有域名、他们的名称服务器等。`whois` 命令非常简单且返回的信息有限。这是一个 `whois` 命令运行的示例：

```
$ whois apple.com
```

Whois Server Version 1.3

```
[...]
Domain Name: APPLE.COM
Registrar: EMARKMONITOR INC. DBA MARKMONITOR
Whois Server: whois.markmonitor.com
Referral URL: http://www.markmonitor.com
Name Server: NSERVER2.APPLE.COM
Name Server: NSERVER.EURO.APPLE.COM
Name Server: NSERVER.ASIA.APPLE.COM
Name Server: NSERVER3.APPLE.COM
Name Server: NSERVER4.APPLE.COM
Status: REGISTRAR-LOCK
Updated Date: 20-may-2004
Creation Date: 19-feb-1987
Expiration Date: 20-feb-2007
[.]
```

## 命令行界面

### whois 命令概述

### 命令语法

```
whois [option(s)] host
```

#### Finder 等效项

网络实用工具（Network Utility）的“Whois”选项卡。

## WHOIS 选项概述

- `whois` `whois` 命令返回指定主机的域名注册信息。

### 获取更多信息

要显示帮助页面并了解更多关于 `whois` 的信息，请在终端中输入 `man whois`。

如你所见，它提供的信息比域名注册日期（苹果的域名已经很久了！）、更新日期和过期日期，以及注册商和域名的名称服务器。`whois` 返回的数据还会提供更具体的信息，例如名称服务器的 IP 地址等。

## 使用 finger 获取用户信息

`finger` 命令提供有关你系统中拥有账户用户的基本信息。其语法为：

- `finger user`

以下是关于该用户的显示：

```
$ finger kirk
Login: kirk Name: Kirk McElhorn
Directory: /Users/kirk Shell: /bin/bash
On Wed May 31 13:23 (CEST) on console, idle 1 day 21:17 (messages off)
On Wed 2 Jun 08:58 (CEST) on tty1
Last login Wed 2 Jun 10:32 (CEST) on tty2
No Mail.
No Plan.
```

你可以获取系统上任何其他用户的类似信息，或者如果远程主机上运行了 `finger` 服务器，可以获取关于另一台计算机的用户的信息。要获取远程用户的信息，请运行命令：

```
finger user@host
```

大多数组织都会关闭 `finger` 服务器，因此你无法获取这样的远程用户信息。Mac OS X 就是这种情况。如果你想开启它，请参见本章前面的“启用 Telnet”侧边栏。你可以使用侧边栏描述的相同启用 `finger`。

## 命令行界面

### finger 命令概述

### 命令语法

```
finger user@host
```

#### Finder 等效项

网络实用工具（Network Utility）的“finger”选项卡。

## FINGER 选项概述

- `finger` `finger` 命令返回指定用户的信息。

## 使用 ipfw 防火墙保护您的 Mac

计算机安全在今天是一个关键问题，许多计算机通过互联网保持着常连接。这些计算机对世界上其他地方都是开放的，不使用防火墙保护你的电脑就像不锁大门。我们大家都希望生活在那种状态下，但现实是，有人出于好奇或恶意，想要闯进这扇门。

Macintosh 计算机天生比其他平台更安全，且 Mac OS X 的基本安全策略相当有效：开箱即用时不激活任何服务；你必须手动开启想要访问的许多服务（如文件共享）。有人说，除非将电脑锁在保险库里、由武装守卫保护并且永不开启，否则没有电脑是完全安全的。但我们不必做到那种地步——那样电脑就完全无法使用了——你可以采取一些预防措施来让它更安全。

计算机的主要风险在于在你不知情的情况下激活了服务或打开了端口。你可以相当容易地检查是哪些服务；Mac OS X 通过“共享”偏好设置面板运行大多数服务，你也可以通过命令行或从恶意应用程序内部开启服务。某些应用程序可能会在你不察觉的情况下打开端口，以便与其他应用程序通信或为了隐私防护。为了完全安全，你需要确保没有流量通过任何你不希望通过的端口。Apple 在 Mac OS X 中包含了一个工业级的防火墙 `ipfw`（Internet 协议防火墙）。该防火墙基于一个相对简单的原理：根据规则允许或拒绝流量。这些规则涵盖了端口、IP 地址、范围等。遗憾的是，`ipfw` 是一个配置非常复杂的工具；这就是为什么 Apple 在“共享”偏好设置中包含了基础配置工具。该偏好设置中的防火墙标签页（见图 13.2）允许你按端口或服务开启或关闭；它不允许设置地址或地址范围，对于大多数用户来说这足够了。如果你点击“启动”，防火墙就会激活并阻止列表之外的所有服务和端口。

### 图 13.2

“共享”偏好设置面板的标签页。

![](img/6906cb53af244b9a7484b2b812444bde_382_0.png)

## 动手实践：监听你的网络流量

你想看看你的 Mac 和网络之间到底发生了什么吗？运行 `tcpdump` 命令：

```bash
$ tcpdump
```

此命令向你显示进入和离开你网络的数据包。诚然，它返回的数据有点难以筛选，但如果你好奇并想查看网络上的所有活动，这是唯一的方法。

请参阅 `tcpdump` 手册中关于使用此命令的页面。

要从 `ipfw` 进行自定义，你必须从命令行配置 `ipfw`。当你启动 Mac 时，`ipfw` 作为内核扩展加载；这意味着它始终处于开启状态，当你在“共享”偏好设置中关闭它时，你只是清空了它的规则，创建了一条允许所有流量进入和离开你的 Mac 的单一规则。你可以通过在防火墙开启时运行以下命令查看此规则：

```bash
$ sudo ipfw list
65535 allow ip from any to any
```

每当你在“共享”偏好设置中切换防火墙时，它都会运行此命令：

```bash
$ sudo ipfw flush
```

这将删除所有规则并将其替换为默认规则（即上述示例中的规则），允许所有流量进入和离开你的 Mac。每当你想重置防火墙规则时，运行该命令。

防火墙规则的语法如下（规则的所有部分应在同一行）：

```bash
[rule number 1-65535] action [log [logamount number]] protocol from source to destination [interface] [options]
```

如你在此示例所示，规则的内容如下：

| 字段 |  |

| :--- | :--- |

| 65535 | 规则编号 |

| allow | 动作 |

| ip | 协议 |

| from to any | 源和目的地 |

现在看看如果你在“共享”偏好设置中关闭所有服务并开启防火墙时，你会看到什么：
