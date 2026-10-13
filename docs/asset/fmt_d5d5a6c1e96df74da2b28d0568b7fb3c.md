
```
find / ! -fstype proc -perm -4000 -ls \
  & Mail -s 'set-UID' your_address
find / ! -fstype proc -perm -2000 -ls \
  & Mail -s 'set-GID' your_address
```

通过 `find` 命令可以找到许多其他类型的可疑文件。其中一种是寻找 UID 或 GID 不在 `/etc/passwd` 或 `/etc/group` 中的数值型 UID/GID 文件。这些可能是破解者文件，或者是早已删除并遗忘的用户的文件。以下命令将列出这些文件：

```
find / ! -fstype proc '(' -nouser -nogroup ')' -ls
```

接下来的 `find` 命令将找到以 `.` 开头的、对普通视图隐藏的文件。预计你会看到 `.profile` 类似的文件，但破解者有时会在你的登录目录之外创建此类名称的文件。

```
find / ! -fstype proc '(' -name '.*??*' -o -name '[^.]*)' -ls
```

下一个 `find` 命令将找到所有由指定用户拥有的文件。它应该在删除账户后使用。当我执行此操作时，会让我想起那些拥有邮箱、在挂起的打印队列中有留文件的用户：

```
find / ! -fstype proc -user dbcooper -ls
```

以下命令将找到每个用户目录中他们并不拥有的文件，这可能是某人不怀好意的的结果 `-ftp` 期望由 root 拥有文件。用户协作可能导致一个用户的目录中包含另一个用户拥有的文件，但这种情况在许多系统上很罕见。也可以对组所有权进行类似的测试。

```csh
cd /home
foreach i ( * )
echo Testing $i
find $i ! -user $i -ls
end
exit
```

`find` 命令是 UNIX 和 Linux 最强大且最具创新的功能之一。通常，它的使用可以解决没有其他简单解决方案的困难问题。

#### 2.6.3 在启动脚本中使用 umask

| 危险等级 | ☠ ☠ ☠ ☠ ☠ |

与其催促用户和自己频繁使用 `ls` 和 `chmod` 命令，不如直接在 `/etc/profile`、`/etc/csh.login`、`/etc/bashrc`、`/etc/zshrc`（对于 sh 等，可能还有 `/etc/csh.csh`）中放置适当的 `umask` 调用。人们可以在用户账户上使用 `grep` 来检查是否有用户覆盖了你的默认 `umask`（通常为 0），这是因为他们不理解 Linux 安全性，或者他们不想被打扰。

以下命令使用了用户以及默认（且非常流行的）bash shell 用户可用的大括号扩展功能。

```
grep umask /home/*{profile,.bash_profile,.bashrc}
grep umask /home/*{cshrc,.login,.tcshrc}
```

### 2.7 系统初始设置期间的危险与对策

| 危险等级 | ☠ |

许多 Linux 发行版存在临时安全漏洞。此外，在完成发行版的安装和初始配置后，你将对系统进行一些额外的“加固”。为了防止在初始配置期间被入侵，在系统配置完成之前，你不应该连接到不受保护的网络。这意味着在最初启动系统之前，你不应该安装以太线、调制解调器线、ISDN 连接、DSL 或电视调制解调器。对于 DSL 和电缆模式是绝对关重要的，因为你的设备可能会与你的 100 个邻居联网。如果他们中任何一个是破解者（或受攻击系统），他们可能会监听来自你新设备的网络包，以触发自动入侵软件。

> 17. 所有安全专家都建议不要在非安全网络的系统上使用 `rash`，因为 `rash`（以及相关命令）被认为是不安全的。

> 18. `grep` 是全局表达式解析器（Global Expression Parser）的缩写。正则表达式是一个计算机语言术语，用于将此类表达式与其他类型（如上下文相关表达式）区分开。例如，在 tcsh 中，文件名包含需要输入的字符数取决于该目录中有多少个文件匹配此表达式。

### 2.7 系统初始设置期间的危险与对策

通过初始阶段不连接到不可信的网络，你将能够通过常规检查对系统进行“加固”以防范入侵，这些检查包括：所有账户都有难以猜解的密码、没有缺少密码的账户、文件具有正确的权限、所有安全补丁均已安装、未启用不必要的服务等。

此时，某些系统管理员想要运行 Bastille 加固脚本，目前支持 Red Hat 和 Mandrake。它不再需要新安装的系统。……（注：后续文本内容在原文中存在大量重复和逻辑断句，此处已按原文结构进行对应翻译）

## 2.7 系统初始化期间的危险与对策

```bash
chkconfig --add sshd
service sshd start
```

覆盖你的 shell 和编辑器配置文件，然后开始进行初始加固。这种加固仅仅是为了保护系统免受网络攻击。我假设在最初我们可以信任任何拥有密码的用户不会心有恶意。对 `xinetd` 和 `xinetd.conf` 执行 `man` 命令将提供所有细节。

Red Hat 有一个名为 `inetdconvert` 的程序，可以将 `inetd.conf` 文件转换为 `xinetd` 配置文件，并根据 GNU 非 UNIX (GNU) 通用公共许可证将其发布。它位于附带的 CD-ROM 光中。使用 `-h` 标志调用它会显示一条令人困惑的信息。要从当前目录下的 `inetd.conf` 文件进行转换，可以使用以下命令：

```bash
mkdir foo
inetdconvert -d foo --inetdfile inetd.conf --convertremaining
more foo/*
cp foo/* /etc/xinetd/
killall -1 xinetd
```

我们现在使用将在第 86 页“关闭不需要的服务”中讨论的技巧。使用以下命令启动 X（除非你不打算使用 X）：

```bash
startx
```

执行命令

```bash
netstat -anptu | more
```

哎，你会发现 X 正在监听 TCP 端口 6000，这极易被破解。由于 X 以 root 身份运行，其默认身份验证的安全性存疑，并且存在许多漏洞，因此它不应该允许从网络访问。根据第 117 页的“标记漏洞”部分，编辑 `$HOME/.xserver`。如果该文件已有一行标记“X”的行，请将其删除。添加以下行：

```bash
X -nolisten tcp :0
```

关闭并重启 X，再次调用 `netstat` 以验证 TCP 端口 6000 是否已不再开放。为每个可能调用 X 的账户编辑 `.xserver`。

Sendmail 正在监听 IP 为 127.0.0.1 的环回设备端口 25。目前尚不清楚这是否代表了除了微小的本地可利用风险之外，但除非系统作为邮件服务器，否则没有理由让 Sendmail 监听任何端口。编辑 `/etc/sysconfig/sendmail` 文件并将该行：

```bash
DAEMON=yes
```

改为

```bash
DAEMON=no
```

## 第 2 章 • 常见问题的快速修复

然后执行命令

```bash
service sendmail restart
netstat -anptu | more
```

观察到 Sendmail 不再监听 TCP 端口 25。

检查安全补丁，并按照第 103 页“旧瓶不装新酒”中讨论的，安装任何影响程序、库或内核的补丁。Red Hat 创新的 `up2date` 程序可以检查新的安全补丁并在可用时提供建议，这对于许多人来说是一个很好的解决方案。对于生产系统，任何新版本的软件都需要进行测试，以确保安装过程中没有出现任何错误，并确保新程序不会导致安全性回退（例如权限或访问权限的更改）。

默认情况下，RH7 启动的是 IP Chains 而不是 IP Tables。IP Chains 的启动脚本存在一个漏洞。如果你在网络启用时执行以下命令，该漏洞会导致系统短暂关闭所有防火墙规则：

```bash
/etc/rc.d/init.d/ipchains start
```

或者在停止或重启时。

幸运的是，这是在系统重启或关机期间完成的，网络未启用，因此不会产生漏洞窗口。

此脚本处理来自配置文件的规则

```
/etc/sysconfig/ipchains
```

该文件的格式与包含 `ipchains` 命令的 shell 脚本相同，不同之处在于缺少命令名称 (`ipchains`)，并且使用 `-P` 而不是 `-P` 来指定策略。如果调用了 `/etc/rc.d/init.d/ipchains` 脚本，它会将系统规则保存到此配置文件中。更好的解决方案是安装我修改过的该脚本版本，它只需调用 `/etc/rc.d/rc.fw`，这应该是你根据第 514 页的“带有 IP Chains 和 DMZ 的防火墙”从零开始编写的脚本。
