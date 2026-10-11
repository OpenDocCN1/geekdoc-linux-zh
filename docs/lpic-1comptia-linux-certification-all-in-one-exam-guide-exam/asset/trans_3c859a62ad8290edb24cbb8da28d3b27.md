
让我们在以下练习中练习如何控制用户对 Linux 系统的访问。

### 练习 17-1：管理用户访问

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_710_0.png)

在这个练习中，你将练习设置用户密码的有效期限制。你还将配置 sudo，以便允许标准用户以 root 用户的身份终止系统中的进程。请完成以下操作：

- 1. 启动你的 Linux 系统并以标准用户身份登录。
- 2. 打开一个终端会话。
- 3. 通过在 shell 提示符下输入 `su –` 并接着输入你的 root 用户密码，切换到你的 root 用户账户。
- 4. 通过完成以下操作来练习配置有效期限制：
  - a. 使用 `cat` 或 `less` 实用程序查看 `/etc/passwd` 文件。识别出你想要为其配置密码有效期限制的系统用户。
  - b. 通过在 shell 提示符下输入 `chage –m 3 –M 60 –W 7 username`，将最小密码有效期设置为 3 天，最大密码有效期设置为 60 天，到期前警告天数设置为 7 天。
- 5. 通过执行以下操作来配置 sudo，允许系统中的用户以 root 用户身份终止进程：
  - a. 识别出你想授权其以 root 身份终止进程的系统用户。
  - b. 作为你的 root 用户，在 shell 提示符下输入 `visudo`。你应看到 `/etc/sudoers` 文件在 vi 文本编辑器中加载。
  - c. 按下 `ins` 键。
  - d. 向下滚动到示例中所示的行，通过在每行开头插入 `#` 字符来注释掉这些行。

```
Defaults targetpw # ask for the password of the target user i.e., root
ALL ALL=(ALL) ALL # WARNING! Only use this together with 'Defaults targetpw'!
```

  - e. 将以下行添加到 sudoers 文件的末尾：

```
User_Alias PWRSRS = tux, ksanders, itrcay
Cmnd_Alias KILLPROCS = /bin/kill, /usr/bin/killall
Host_Alias MYHOSTS = WS1
PWRSRS MYHOSTS = (root) KILLPROCS
```

  - f. 按下 `ESC` 键，然后输入 `:exit` 以保存对 sudoers 文件的更改。
  - g. 作为你的 root 用户在 shell 提示符下运行 `top`。
  - h. 打开一个新的终端会话，并（作为你的标准用户）输入 `ps -elf | grep top`。你应该看到一个由 root 用户拥有的正在运行的 `top` 进程。
  - i. 通过在 shell 提示符下输入 `sudo killall top` 来以你的标准用户身份终止该进程。
  - j. 在提示时，输入你的用户密码。
  - k. 再次在 shell 提示符下输入 `ps -elf | grep top`。你应该看到由 root 用户拥有的那个 `top` 进程已被终止。

现在你已经确保了用户的安全，接下来让我们讨论如何防御网络攻击。

## 防御网络攻击

如果生活在一个我们可以将网络连接在一起，并且能够信任他人尊重我们系统的世界中，那将是很美好的。不幸的是，这样的世界并不存在。如果你的 Linux 系统连接到网络，你需要非常关注网络攻击。如果你的网络连接到公共网络，例如互联网，那么你需要极度关注网络攻击。

正如本书讨论的大多数主题一样，网络安全是一个庞大的主题，可以写满许多卷书。我们在这里真的没有时间和空间来充分阐述这个主题。相反，我将讨论一些你可以做的防御网络攻击的基本事项。我将讨论以下内容：

- 减轻网络漏洞
- 实施防火墙

让我们从讨论一些你可以做的减轻网络漏洞的事项开始。

### 减轻网络漏洞

好消息是，有一些简单的事情你可以做，以减轻网络攻击对你 Linux 系统的威胁。这些包括以下内容：

- 了解当前的威胁
- 卸载不必要的服务
- 安装更新

让我们首先讨论如何了解当前的网络威胁。

### 了解当前的威胁

网络安全威胁最大的问题之一在于，我们总是比那些戴黑帽子的人落后一步。我们还没来得及实施修复措施来保护我们的系统免受最新漏洞利用的攻击，他们就用新的攻击手段袭击我们。因此，保持与最新网络威胁的同步至关重要。你很快就会看到，这些威胁每周甚至在每天都在变化！你确保系统安全的唯一方法是了解当前的威胁是什么。

做到这一点的最佳方法是定期访问与安全相关的网站。这些网站会告知你最新的漏洞利用以及如何防御它们。最值得访问的网站之一是 www.cert.org，该网站由卡内基梅隆软件工程研究所（Carnegie Mellon Software Engineering Institute）的计算机应急响应小组（CERT）维护。CERT 网站包含指向最新安全公告的链接。

另一个优秀的资源是 www.us-cert.gov。由美国政府的计算机应急准备小组（US-CERT）维护，US-CERT 网站提供了关于当前网络攻击的大量信息。

当然，还有数百个其他与安全相关的网站。然而，我在此列出的网站是最权威的网站之一。大多数其他与安全相关的网站的内容都源自这些网站。如果你虔诚地访问这些网站，你就可以了解安全界正在发生的事情，并希望防止你的系统遭受攻击。

除了保持与这些网站的同步之外，你还应该审查你的系统，以确认其提供的所有服务是否真的必要。接下来我们将谈谈如何做到这一点。

### 卸载不必要的服务

减轻网络攻击威胁最简单的事情之一，就是简单地卸载你系统上不需要正在运行的网络服务。根据你使用的发行版及其安装方式，你的系统上可能有许多你甚至不知道存在且并不需要的服务在运行。你可以通过在 shell 提示符下输入 **chkconfig** 来查看已安装服务的列表及其是否正在运行。此命令将列出每个服务及其状态，如图 17-10 所示。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_712_0.png)

> **注意** chkconfig 实用程序并非在所有发行版上都可用。它最初是一个 Red Hat 实用程序，已被移植到许多其他发行版，如 SUSE Linux。但是，如果你使用的是 Debian，你会发现它不可用。

然而，作为一个警告，除非你知道某个服务实际是做什么的，否则不要禁用它。某些守护进程是系统正常运行所必需的。如果你不知道某个特定服务是什么，请使用 man 实用程序、info 实用程序或互联网对其进行研究，以确定它是否必要。

除了 chkconfig，你还可以使用 `nmap` 命令来查看你的 Linux 系统上开放的 IP 端口。这些信息真的很有用。你的 Linux 系统上的每个开放端口都代表一个潜在的漏洞。某些开放端口是必要的。然而，其他端口可能并不必要。你可以通过卸载使用它的服务来关闭该端口。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_713_0.png)

```
ws1:~ # chkconfig
suSEfirewall2_init  off
suSEfirewall2_setup off
sserdnt           on
acpid             on
alsasound         on
ald               off
auditd            on
autofs            off
autovs1           off
avahi-daemon      on
avahi-dnsconfd    off
bluez-coplug      on
chargen           off
chargen-udp       off
ctts              on
cron              on
cups              off
cups-lpd          off
cvs               off
day/time          off
day/time-udp      off
dbus              on
discard           off
```

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_713_1.png)

> 注意 你在使用 nmap 命令之前需要安装 nmap 软件包。

使用 nmap 的语法对于 TCP 端口扫描是 **nmap -sT host_IP_address**，对于 UDP 端口扫描是 **nmap -sU host_IP_address**。在图 17-11 中，nmap 实用程序被用于扫描开放的 TCP 端口。

正如你在图 17-11 中所看到的，被扫描的主机上正在运行许多服务。你可以使用此输出来确定哪些服务应该和哪些不应该保留在系统中运行。要禁用服务，你可以使用 init 目录中的 init 脚本将其关闭。你还应该使用 chkconfig 命令配置该服务，使其不会自动启动。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_713_2.png)

> 提示 你应在本地和从另一个系统针对同一主机运行 nmap。这将告诉你哪些端口在你的系统上是开放的，以及哪些服务被允许通过你的主机防火墙。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_713_3.png)

```
ws1:~ # nmap -sT 192.168.1.84
Starting Nmap 5.00 ( http://nmap.org ) at 2011-05-23 14:40 MDT
Interesting ports on ws1.mydomain.com (192.168.1.84):
Not shown: 996 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 8.28 seconds
```

