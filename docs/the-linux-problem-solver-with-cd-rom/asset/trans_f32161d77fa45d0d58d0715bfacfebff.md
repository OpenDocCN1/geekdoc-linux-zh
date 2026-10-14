

broadway,broadway.example.com 1024 3314991439557381242252657691002370430 73530453279320245581463444618610244719198805716250346934799195377060242 7...

如果你是第一次安装 ssh，make install 会为你生成并安装主机密钥。你需要做的只是让 sshd 在启动时启动。第一章介绍了 init.d 和 rc*.d 目录，它们控制启动时启动的进程。

如果你通过 ssh 连接到另一台机器，并且其公钥主机密钥不在 /etc/ssh_known_hosts 中，ssh（取决于其配置方式）要么询问你是否要继续连接并将主机密钥添加到你个人的 ~/.ssh/known_hosts 文件中，要么直接在不询问的情况下添加密钥。如果在连接时 ssh 的主机密钥验证失败（由于密钥不同），你会收到一条难看且令人不安的消息：

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: HOST IDENTIFICATION HAS CHANGED!    @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that the host key has just been changed.
Please contact your system administrator.
```

（此消息通常是由于管理员更改主机密钥或机器升级造成的，但询问一下总是有好处的。）ssh 和 sshd 的系统范围配置文件分别是 /etc/ssh_config 和 /etc/sshd_config。正常系统上 ssh_config 的默认值包括以下内容（以及它们相关的命令行对应项）。

| 配置文件选项 | 命令行选项 |
|---|---|
| ForwardAgent yes | (-a 禁用此项) |
| ForwardX11 yes | (-x 禁用此项) |
| RhostsAuthentication yes | (无) |
| RhostsRSAAuthentication yes | (无) |
| RSAAuthentication yes | (无) |
| TISAuthentication no | (无) |
| PasswordAuthentication yes | (无) |
| FallBackToRsh yes | (无) |
| UserRsh no | (无) |
| BatchMode no | (无) |
| StrictHostKeyChecking no | (无) |
| IdentityFile ~/.ssh/identity | (-i $HOME/.ssh/identity) |
| Port 22 | (-p 22) |
| Cipher idea | (-c idea) |
| EscapeChar ~ | (-e ~) |

安装后，ssh 的行为或多或少就像 rlogin。如果要使用不同的登录名通过 ssh 连接到另一台主机，命令行是 ssh -l name hostname，就像 rlogin 一样。

## scp

ssh 提供的另一个重要服务是 scp，这是一种安全地将文件复制到远程主机或从远程主机复制文件的方式。它接受与 rcp 相同的选项：

```
$ scp user@remotehost local-pathname
$ scp local-file user@remotehost
```

如果你的用户名在远程主机上相同，则 user@ 部分是可选的。local-pathname 可以是本地机器上的文件名或目录；local-file 必须是本地机器上的文件。

## ssh Clients for Other Operating Systems

TeraTerm 是一个非常流行且免费的 Windows ssh 客户端。

http://www.zip.com.au/~roca/ttssh.html

NiftyTelnet-ssh for the Macintosh 也是免费的，包含 ssh 支持；不幸的是，软件专利问题使其在美国在专利到期前使用是非法的。

http://www.lysator.liu.se/~jonasw/freeware/niftyssh/

SecureCRT 是一款商业 ssh 客户端，是 Windows 上流行的 CRT 终端仿真器的 ssh 兼容版本。

http://www.vandyke.com/products/securecrt

Data Fellows 为 Macintosh 和 Windows 提供商业 ssh 客户端。

http://www.datafellows.com

## PROBLEM 13 (CONTINUED)

问题：缓冲区溢出漏洞利用。

修复：请参阅下一节。

说明：有人尝试入侵并且可能已成功。上述示例表明这是一次缓冲区溢出攻击，它向服务器提供连续输入，试图将其超载到崩溃点。虽然许多缓冲区溢出问题已得到纠正，但不可避免地还有更多潜伏在外。

## Detecting Break-Ins

如果你经历过入侵（而且并不总是显而易见），一个名为 tripwire 的程序可以找到所谓的特洛伊木马和被篡改的文件。在创建所有系统文件的目录后，它会定期检查系统的完整性（除非你最初在干净的系统上运行它以获取“健康配置的快照”，否则它毫无用处，所以不要等待去做）。

注意是否有额外的 inetd 进程在运行。一种常见攻击方法是利用缓冲区溢出漏洞，然后在 /tmp 等位置创建一个文件，其中包含一条 inetd.conf 行：

```
8080 stream tcp nowait root /bin/sh -s -i
```

攻击随后在该文件上运行另一个 inetd。对受损机器的 8080 端口进行 telnet 将产生一个 root shell，使攻击者能够对机器为所欲为。

## What to Do if Someone Breaks In

如果有人入侵你的机器，真的无法确定你的攻击者做了什么。为了防止该个人再次回来，你需要重新安装至少操作系统的核心部分（以及机器上的任何自定义服务）。首先，试着找出入侵者是如何进入的，因为如果你把系统恢复成之前的状态，很可能入侵者会再次回来。

当然，你也应该先备份你的数据。

## 2.6 Diagnostics

我们都知道网络并不总是按预期运行。幸运的是，Linux 可用的许多工具可以帮助你找到问题。大多数发行版都附带大量安装在 /usr/sbin 中的工具。以下是好东西的列表及其基本功能。

