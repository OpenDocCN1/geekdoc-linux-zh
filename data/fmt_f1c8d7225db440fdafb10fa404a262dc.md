
```bash
root@kali:~# nmap -sS -Pn 192.168.198.145
Starting Nmap 6.40 ( http://nmap.org ) at 2013-10-23 15:02 EDT
Nmap scan report for 192.168.198.145
Host is up (0.00030s latency).
Not shown: 977 closed ports
PORT STATE SERVICE
21/tcp   open ftp
22/tcp   open ssh
23/tcp   open telnet
25/tcp   open smtp
53/tcp   open domain
80/tcp   open http
111/tcp  open rpcbind
139/tcp  open netblos-ssn
445/tcp  open microsoft-ds
512/tcp  open rexec
513/tcp  open login
514/tcp  open shell
1099/tcp open rmiregistry
1524/tcp open ingresslock
2049/tcp open nfs
2121/tcp open ccproxy-ftp
3306/tcp open mysql
5432/tcp open postgresql
5900/tcp open vnc
6001/tcp open x11
6667/tcp open irc
8000/tcp open ajp13
8180/tcp open unknown
MAC Address: 00:0c:29:07:64:4E (VMware)

Nmap done: 1 IP address [1 host up] scanned in 0.14 seconds
```

那里有很多开放的端口！

好了，我们确实有很多可能的突破口；让我们看看能否找到在这些端口上运行的服务。让我们再次尝试运行 `nmap` 命令，但这次添加 `-A` 参数，它将执行操作系统检测并尝试确定服务版本：

```bash
nmap -sS -Pn -A 192.168.198.145
```

Nmap 将运行一段时间，因为它正在尝试检测在这些端口上运行的实际服务。几分钟后，你会看到一个类似这样的屏幕：

![](img/12315f8a5d9e9bad6bf982c86c5537ea_81_0.png)

对于每个端口，我们都能看到端口号、服务类型，甚至尝试获取服务的软件版本。

在上面的图片中，我们看到几个普通端口是开放的。在高端口也运行着许多服务；其中一个特别的是 Unreal 网络中聊天 `IRC` 程序：

![](img/12315f8a5d9e9bad6bf982c86c5537ea_81_1.png)

通常在教程中，他们会先涵盖主要端口的服务。但我建议查看位于高端口的服务。相比之下，常见的服务更有可能被打了补丁或更新，还是某个安装过一次且可能被遗忘的次要服务？

所以，让我们看看能关于这个 Unreal IRC 服务发现些什么。

在图片中，我们可以看到软件版本，在这里是 *Unreal IRC 3.2.8.1*。我们的下一步是针对该软件版本进行漏洞搜索。只需在 Google 中搜索“unreal3.2.8.1 exploits”就能搞定。

但既然我们可以用 Metasploit 进行搜索，为什么还要用 Google 呢？

### 利用 Unreal IRC 服务

让我们运行 Metasploit：

```bash
root@kali:~# msfconsole
```

现在使用搜索命令并粘贴服务名称和程序版本：

```bash
msf > search Unreal 3.2.8.1
```

运行此搜索返回了：

```bash
exploit/unix/irc/unreal_irc_3281_backdoor   2010-06-12      excellent Unreal IRCD 3.2.8.1 Backdoor Command Execution
```

一个可靠性评级为“优秀（excellent）”的 Unreal 3.2.8.1 后门！

这是一个极好的消息，因为漏洞利用程序是根据成功概率和稳定性进行排序的。

如果你还记得我们对 Metasploit 的介绍，利用漏洞有几个步骤：

- 选择利用程序 `Picking an Exploit`
- 设置利用选项 `Setting Exploit Options`
- 选择有效负载 `Picking a Payload`
- 设置有效负载选项 `Setting Payload Options`
- 执行利用程序 `Running the Exploit`
- 连接到远程系统 `Connecting to the Remote System`

让我们逐步完成这个过程。

### 选择利用程序

如果我们使用 `info` 命令，我们可以获取更多关于我们可能的利用程序的信息。

```bash
msf > exploit/unix/irc/unreal_irc_3281_backdoor
```

执行 `exploit/unix/irc/unreal_irc_3281_backdoor` 后会得到以下信息：

| Name | Date | Description |
| :--- | :--- | :--- |
| exploit/unix/irc/unreal_irc_3281_backdoor | 2010-06-12 | excellent Unreal IRCD 3.2.8.1 Backdoor Command Execution |

在本教程中，我们将使用 Kali 系统作为测试平台，并将故意留的 Metasploitable 2 虚拟机作为目标系统。

### 使用扫描器

要找到可用的扫描器，只需在 Kali 命令行提示符中运行 `msfconsole`。在 Metasploit 启动后，在提示提示符处输入 `search scanner`：

```
msf > search scanner
Matching Modules
=================
Name                               Rank    Description
auxiliary/admin/smb_check_dir_file    normal  SMB Scanner Check File/Directory Utility
auxiliary/bnat/nat_scan               normal  BNAT Scanner
auxiliary/gather/citrix_published_applications  normal  Citrix Metaframe ICA Published Applications
auxiliary/gather/enum_nz_                normal  DNS Record Scanner and Enumerator
auxiliary/gather/natpmp_external_address  normal  NAT-PMP External Address Scanner
auxiliary/pro/nexpose                    normal  NAT-PMP External Address Scanner
auxiliary/pro/webscan                   normal  PRO: Nexpose Scanner Integration
```

向下阅读庞大的列表以查看可用内容。

在本教程中，我们将注意力缩小在发现的常用端口上。作为回顾，这里是上一章节执行的 `nmap` 扫描结果：

```
PORT        STATE
21/tcp      open ftp
22/tcp      open ssh
23/tcp      open telnet
25/tcp      open smtp
53/tcp      open domain
80/tcp      open http
```

让我们关注端口 `22`，它就是安全外壳 `ssh`。

继续在 Metasploit 中搜索 `ssh` 扫描器：

![](img/12315f8a5d9e9bad6bf982c86c5537ea_88_0.png)

注意这里有几个可用的。我们现在只是寻找版本信息，因此我们将使用 `auxiliary/scanner/ssh/ssh_version` 模块。

- 输入 `use auxiliary/scanner/ssh/ssh_version`
- 然后输入 `show options` 查看你可以可以使用哪些选项。
- 在这种情况下，我们只需要做的的是 `set RHOSTS <IP>`，即远程主机，这是我们的目标。
- 然后只需输入 `exploit` 运行。

![](img/12315f8a5d9e9bad6bf982c86c5537ea_88_1.png)

我们看到目标确实在运行 SSH 服务，并且我们看到了软件版本：

> `SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu`

我们现在可以使用此信息来搜索漏洞利用程序。

注意设置远程主机的命令是复数 `RHOSTS`，我们可以在这里输入整个系统范围，使我们能够快速轻松地扫描整个网络以寻找 `ssh` 服务器。

现在我们已经有了 SSH 的版本号，可以尝试为它寻找漏洞利用程序，或者我们可以使用另一个辅助模块 `auxiliary/scanner/ssh/ssh_login`，使用字典文件尝试暴力破解密码。我们将这个练习留给你们。

### 使用额外的扫描器

某些扫描器返回的信息与其他扫描器不同。

#### MySQL

例如，如果我们使用 MySQL 扫描，我们会得到这个：

```
msf> use auxiliary/scanner/mysql/mysql_version
msf auxiliary(mysql_version) > show options
Module options (auxiliary/scanner/mysql/mysql_version):
Name            Current Setting Required Description
RHOSTS                  yes             The target address range or
CIDR                                
PORT            3306                The target port
THREADS         1               yes             The number of concurrent threads

msf auxiliary(mysql_version) > set RHOSTS 192.168.198.145
nRHOSTS => 192.168.198.145
msf auxiliary(mysql_version) > exploit
[*] 192.168.198.145:3306 is running MySQL 5.0.51a-ubuntu5 (protocol 10)
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module completed
msf auxiliary(mysql_version) >
```

扫描显示正在运行 MySQL 5.0.51a。

但其他的可以发现更多的信息。例如，让我们看看 Telnet。

#### TELNET

Telnet 版本扫描器可以以不同的方式工作。如果我们使用用户名和密码，它将尝试登录服务。如果不使用，它将只获取横幅。

注意这与我们之前涵盖的不同；在 Metasploitable 机器上不返回版本号，而是执行横幅获取。

有时你可以通过它发现一些有趣的信息。

让我们设置扫描器：

```
msf auxiliary/scanner/telnet/telnet_version) > show options
Module (auxiliary/scanner/telnet/telnet_version):
Name                Current Setting  Required Description
PASSWORD            yes              The password for the specified username
HOSTS               yes              The target address range or CIDR
PORT                23               yes       The target port
THREADS             yes              The number of concurrent threads
TIMEOUT             30               yes       Timeout for the Telnet probe
USERNAME            yes              The username to authenticate as
msf auxiliary(telnet version) > set RHOST 192.168.198.145
```

现在，当我们输入 `exploit` 时看到这个：

![](img/12315f8a5d9e9bad6bf982c86c5537ea_90.png)

看起来只是一堆关于软件正在运行的文本，没有提示。但如果我们观察仔细一点，我们可以看到其他的：`Login to get started`，看起来他们在 Telnet 页面上暴露了登录凭据。试试是否有效：

```
root@metasploitable~$ telnet 192.168.198.145
Connected to 192.168.198.145.
Password:
Last login: Wed Oct 23 24:48 EDT on tty1
Linux metasploitable 2.6.24-generic #1 SMP Apr 10 58:00 UTCThe programs included with the Ubuntu system are free; the exact distribution for each program are described in the individual files in /usr/share/doc/.
Ubuntu comes with ABSUTELY NO WARRANTY, the extent permitted by applicable law.
To access official documentation, please visit: http://help.ubuntu.com/
metasploitable~$
```

进去了！
