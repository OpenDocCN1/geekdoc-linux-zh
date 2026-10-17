
有时，你可能需要撤销公钥。例如，假设你在笔记本电脑上存储了公钥的副本，而该笔记本电脑被盗了，或者可能员工离开了你的组织，你不再希望这些个人能够使用与其员工账户关联的密钥。要撤销密钥，你对`gpg`使用`--gen-revoke keyname`：

```
$ gpg --gen-revoke jennie@luna.com
```

程序会要求你回答几个问题，例如撤销密钥的原因。然后它会生成一个密钥块，如下：

```
-----BEGIN PGP PUBLIC KEY BLOCK-----Version: GPG v2.0.19
(GNU/Linux)Comment: A revocation certificate should follow
E1WE1EBCAWAALIBPVkFHQG628bACgQBbimvMO2y4uzwCCeQiLKX8j12jk+hNO0KU13ezMBA8Q2twdU+AP6wv0NU/YQi8a78=s0s
-----END PGP PUBLIC KEY BLOCK-----
```

`uid`行包含你在加密或解密数据时使用的标识符，因此你应该特别注意这些信息。

加密派对是交换公钥的一种流行方式。一群朋友聚在一起度过晚上，每个人都带一个包含自己公钥的`U盘`。一个朋友还带了一台电脑。朋友们使用电脑交换公钥。晚上结束时，朋友们度过了愉快的社交时光，并带着有所有人公钥的`U盘`回家。

# 撤销密钥

有时，你可能需要撤销公钥。例如，假设你在笔记本电脑上存储了公钥的副本，而该笔记本电脑被盗了，或者可能员工离开了你的组织，你不再希望这些个人能够使用与其员工账户关联的密钥。要撤销密钥，你对`gpg`使用`--gen-revoke keyname`：

```
$ gpg --gen-revoke jennie@luna.com
```

程序会要求你回答几个问题，例如撤销密钥的原因。然后它会生成一个密钥块，如下：

```
-----BEGIN PGP PUBLIC KEY BLOCK-----Version: GPG v2.0.19
(GNU/Linux)Comment: A revocation certificate should follow
E1WE1EBCAWAALIBPVkFHQG628bACgQBbimvMO2y4uzwCCeQiLKX8j12jk+hNO0KU13ezMBA8Q2twdU+AP6wv0NU/YQi8a78=s0s
-----END PGP PUBLIC KEY BLOCK-----
```

`uid`行包含你在加密或解密数据时使用的标识符，因此你应该特别注意这些信息。

加密派对是交换公钥的一种流行方式。一群朋友聚在一起度过晚上，每个人都带一个包含自己公钥的`U盘`。一个朋友还带了一台电脑。朋友们使用电脑交换公钥。晚上结束时，朋友们度过了愉快的社交时光，并带着有所有人公钥的`U盘`回家。

# 撤销密钥

有时，你可能需要撤销公钥。例如，假设你在笔记本电脑上存储了公钥的副本，而该笔记本电脑被盗了，或者可能员工离开了你的组织，你不再希望这些个人能够使用与其员工账户关联的密钥。要撤销密钥，你对`gpg`使用`--gen-revoke keyname`：

```
$ gpg --gen-revoke jennie@luna.com
```

程序会要求你回答几个问题，例如撤销密钥的原因。然后它会生成一个密钥块，如下：

```
-----BEGIN PGP PUBLIC KEY BLOCK-----Version: GPG v2.0.19
(GNU/Linux)Comment: A revocation certificate should follow
E1WE1EBCAWAALIBPVkFHQG628bACgQBbimvMO2y4uzwCCeQiLKX8j12jk+hNO0KU13ezMBA8Q2twdU+AP6wv0NU/YQi8a78=s0s
-----END PGP PUBLIC KEY BLOCK-----
```

# 加密和解密数据

要加密数据，你使用`--recipient`和`--encrypt`选项：

```
$ gpg --recipient jennie@luna.edu --armor --encrypt original-file
```

要解密文件，你使用`--decrypt`选项：

```
$ gpg --out decrypted-file --decrypt encrypted-file
```

# 签名消息和验证签名

如前所述，`GPG`可以对消息进行签名，以便人们知道它们来自你。这样做请使用`--sign`或`--clearsign`选项：

```
$ gpg --clearsign original-file
```

要验证签名消息，你可以使用`--verify`选项来验证签名：

```
$ gpg --verify received-file
```

## 考试要点

### 超级服务器（Super server）的作用

超级服务器（也称为超级守护进程），如`inetd`和`xinetd`，管理多个服务器的入站网络连接。它们可以添加安全性和便利功能，并帮助最大限度地减少很少访问的服务器带来的内存负载。

### 解释超级服务器端口访问控制的功能

超级服务器或其调用的程序（如`TCP封装`）可以限制对其管理的服务器的端口的访问。这些限制发生在比防火墙限制更高的层级，并且仅适用于由超级服务器管理的服务器。

### 总结你可以用于识别运行在计算机上运行的服务器的工具

`netstat`和`lsof`程序都提供了选项来列出所有（或部分）打开的网络连接，以及正在监听连接的程序。远程网络扫描器（如`Nmap`）可以探测另一台机器的开放网络端口。`fuser`程序可以确定当前使用特定网络端口的进程。查阅本地配置文件也可以为计算机上运行的程序提供线索。

### 描述为什么 SUID 和 SGID 程序具有潜在风险

设置用户ID (SUID) 和设置组ID (SGID) 位告诉`Linux`以文件所有者用户或组的身份运行程序。当`root`拥有程序文件时，这特别危险，因为在运行该文件时它本质上将所有用户提升到了`root`，使得程序中的错误变得更加危险，并增加了精明用户滥用程序以获取完全`root`权限或制造破坏的可能。

### 解释为什么影子密码（shadow passwords）很重要

影子密码将哈希值存储在普通用户无法读取的文件中，使得本地系统上的攻击者更难读取哈希后的密码，并无法通过破解攻击发现其他用户的密码。现代`Linux`发行版默认使用影子密码。

### 解释如何生成良好的密码

理想情况下，密码应该是随机的。如果无法做到这一点，一种很好的方法是生成一个难以猜测的基础字符串，然后通过添加数字和标点符号、更改某些字符的大小写、更改字母顺序并显著增加密码长度（甚至是重复字符）。

### 解释为什么 SSH 是首选的远程文本模式登录工具

安全外壳 (SSH) 协议为所有流量提供加密，包括密码交换和所有后续数据交换，而较旧的工具（如`Telnet`）则没有。这使得`SSH`在交换敏感数据时更加安全，特别是在通过互联网等不可信的网络时。

### 识别最重要的 SSH 配置文件

`SSH`服务器通过`/etc/ssh/sshd_config`文件控制。`SSH`客户端配置文件是`/etc/ssh/ssh_config`；不要将两者混淆。

### 描述 SSH 公钥和私钥文件

这些密钥通常存储在`/etc/ssh/`目录下。私钥文件称为`ssh_host_rsa_key`、`ssh_host_rsa1_key`和`ssh_host_dsa_key`，取决于使用的加密算法。公钥文件与私钥文件名相同，但多了一个`.pub`扩展名。

### 描述 GPG 的功能

`GPG`支持单个文件或电子邮件消息的公钥加密。你可以使用`GPG`对通过电子邮件或其他不安全手段传输敏感数据进行加密。

## 复习题

1. 输入`lsof -i | grep LISTEN`产生三行输出，分别对应`sendmail`、`sshd`和`proftpd`服务器。关于该系统的安全性，你可以得出什么结论？

   - A. 一切正常；`sshd`的存在确保数据正通过`SSH`进行加密。
   - B. `sendmail`和`sshd`服务器是正常的，但`proftpd`使用的`FTP`协议是不安全的，不应被使用。
   - C. `sendmail`服务器应该替换为`Postfix`或`qmail`以提高安全性，但`sshd`和`proftpd`是没问题的。
   - D. 因为`sendmail`和`proftpd`使用未加密的文本模式传输，因此它们都不适用于连接到网络的计算机上。
   - E. 在没有进一步信息的情况下无法得出结论；列出的服务器可能合适也可能不合适，或者不真实。

2. 作为安全审计的一部分，你计划使用`Nmap`检查网络上所有计算机是否有不必要的服务器。在运行`Nmap`检查之前，你应该执行以下哪些任务？

   - A. 备份目标系统上的`passwd`以消除被损坏的可能性。
   - B. 获取目标系统的`root`密码，以便能够正确配置它们以接受`Nmap`探测。
   - C. 获得你老板的书面许可以执行`Nmap`扫描。
   - D. 在你打算用于扫描的计算机上配置`sudoers`，以便赋予自己运行`Nmap`的权限。
   - E. 禁用运行`Nmap`的计算机与你打算扫描的服务器之间的任何防火墙。

3. 你的登录服务器使用`PAM`，你想限制用户对系统资源的访问。你需要编辑哪个配置文件？

   - A. `/etc/limits.conf`
   - B. `/etc/pam/limits.conf`
   - C. `/etc/security/limits.conf`
   - D. `/etc/security/pam/limits.conf`
   - E. `/usr/local/limits.conf`

4. 哪些工具可能用于检查本地计算机上的开放端口？（选择三项）

   - A. `Nmap`
   - B. `netstat`
   - C. `lsof`
   - D. `portmap`
   - E. `services`

5. 下列哪个命令可以找到计算机上带有`SUID`位的程序文件？

   - A. `find /perm -4000`
   - B. `find /type`
   - C. `find /perm +4000`
   - D. `find /type`
   - E. `find -id`

6. 下列行出现在`sudoers`文件中。影响是什么？

   - A. 管理员组可以运行。
   - B. 管理员组的用户可以运行。
   - C. 定义了管理员组。
   - D. 定义了用户。
   - E. 以`root`运行。

7. 你以`root`身份输入哪个命令来发现计算机上所有的开放连接？

   - A. `lsof -c`
   - B. `netstat -ap`
   - C. `ifconfig -s`
   - D. `nmap -s`
   - E. `top`

8. 服务器同时出现在`hosts.allow`和`hosts.deny`中。使用`wrappers`时结果如何？

   - A. 拒绝并记录在`/log/messages`中。
   - B. 系统决定。
   - C. `hosts.deny`优先，被拒绝。
   - D. `hosts.allow`优先，被允许。

9. `xinetd`的`bind`选项什么时候有用？

   - A. 当你想运行两个时。
   - B. 当你想通过名称而非`IP`指定。
   - C. 当`xinetd`运行在两个接口上。
   - D. 当解析冲突。
   - E. 当`xinetd`管理`DNS`。

10. 你发现`Waiter`程序（一个网络服务器）运行在你的计算机上，因此你将其关闭。如何进一步减少外部人员滥用`Waiter`的风险？（选题）

    - A. 通过防火墙拦截`Waiter`端口
    - B. 通过`Waiter`文档了解如何以隐藏模式运行
    - C. 通过`SSH`隧道`Waiter`端口
    - D. 卸载`Waiter`包
    - E. 卸载客户端

11. 你想使用`xinetd`访问控制来限制谁访问服务器。具体来说，只有`192.168.0.0/24`网络的用户应该可以使用该服务器。你应该如何做？

    - A. 在`/etc/xinetd.conf`中输入`hosts_allowed = 192.168.0.0/24`。
    - B. 在`/etc/xinetd.conf`中输入`only_from = 192.168.0.0/24`。
    - C. 在`/etc/hosts.allow`中输入`server : 192.168.0.0/24`，其中`server`是服务器名。
    - D. 在`/etc/hosts.deny`中输入`server : 192.168.0.0/24`，其中`server`是服务器名。
    - E. 输入`iptables -L 192.168.0.0/24`以仅允许`192.168.0.0/24`用户访问。

12. 在以下密码中，哪个是最好的？

    - A. `Odysseus`
    - B. `iA71ocIaMy~~~~`
    - C. `pickettomato`
    - D. `Denver2Colorado`
    - E. `123456`

13. 下列哪种攻击涉及发送虚假电子邮件以诱导毫无防备的人泄露敏感财务或其他信息？

    - A. 钓鱼 (Phishing)
    - B. 脚本小子 (Script kiddies)
    - C. 欺骗 (Spoofing)
    - D. 诱捕 (Ensnaring)
    - E. 黑客攻击 (Hacking)

14. 普通用户报告无法登录计算机，但`root`登录没有问题。你可以检查什么来解释这种情况？

    - A. 一个运行异常的`syslog`守护进程
    - B. 一个以`root`身份运行的登录进程
    - C. 存在`etcnnlogin`文件
    - D. `binlogin`上存在`SUID`位

15. 在激活`SSH`服务器后，你可能会考虑退役哪些服务器？

    （选择两个。）

    - A. `SMTP`
    - B. `Telnet`
    - C. `FTP`
    - D. `NTP`
    - E. `Samba`

16. 你发现`/etc/ssh`中的`ssh_host_dsa_key`文件的权限为`0666` (-rw-rw-rw-)。你的`SSH`服务器已经运行了几个月。你应该担心吗？

    - A. 是
    - B. 否
    - C. 仅当`ssh_host_dsa_key.pub`文件也是所有人可读时才需要
    - D. 仅当你从超级服务器启动`SSH`时才需要
    - E. 仅在你使用笔记本电脑时需要

17. 为了获得最佳`SSH`服务器安全性，你应该如何设置`/etc/ssh/sshd_config`中的`Protocol`选项？

    - A. `Protocol 1`
    - B. `Protocol 2`
    - C. `Protocol 1,2`
    - D. `Protocol 2,1`
    - E. `Protocol *`

18. 为什么允许`root`直接通过`SSH`登录是不明智的？

    - A. 禁止直接访问`root`意味着`SSH`服务器可能由非`root`用户运行，从而提高了安全性。
    - B. `root`密码绝不应通过网络连接发送；以以这种方式允许`root`登录等同于自寻死路。
    - C. `SSH`将所有登录信息（包括密码）存储在公开可读的文件。
    - D. 使用`SSH`登录时，`root`的命令可以被不受欢迎的元素轻易拦截和复制。
    - E. 拥有`root`密码但没有其他密码的人随后可以入侵计算机。

19. 你从一个网站下载了一个`GPG`公钥并保存为文件`fredkey.pub`。你需要对此密钥进行什么操作才能使用它？

    - A. 输入`inspect-gpg fredkey.pub`。
    - B. 输入`gpg --readkey fredkey.pub`。
    - C. 输入`import-gpg fredkey.pub`。
    - D. 输入`gpg --import fredkey.pub`。
    - E. 输入`gpg-import fredkey.pub`。

20. 你想向一个邮件联系人发送一条加密消息。你们都有`GPG`。在发送加密消息之前，你们需要交换什么？

    - A. 你的联系人必须获取你的`GPG`公钥。
    - B. 你的联系人必须获取你的`GPG`私钥。
    - C. 你必须与联系人交换私钥。
    - D. 你必须获取联系人的`GPG`私钥。
    - E. 你必须获取联系人的`GPG`公钥。

# 附录答案

# 第 1 章：探索 Linux 命令行工具

1. D. 这些方法中的任何一种都有效，或者至少可能。（在执行其中任何一种时你可能会出错。）选项B或C可能是效率效率的；由于需要输入长文件名，选项A可能会很繁琐。

2. E. `echo`命令是在`bash`内部实现的，尽管大多数系统中也提供外部版本。`cat`、`less`和`sed`命令不是在`bash`内部实现的，尽管它们可以作为外部命令被调用。

3. E. `echo`命令将后面的内容输出到标准输出，`$`是一个环境变量。因此`echo`显示了`$PROC`的值，这意味着它一定是由你的某个配置文件指定的。许多变量被设为特定值以传达信息，而`$`不是一个标准环境变量。

4. A. `pwd`命令打印（到标准输出）当前目录的名称。其余选项都是错误的，尽管选项B描述了`cd`命令，并且可以使用各种工具重新格式化文本以减少列数。

5. A. 字符`.`指代当前目录，斜杠`/`是目录分隔符。因此`/`表示运行存储在根目录下的程序的意图。由于安全原因，路径通常会省略当前目录，因此此选项可能会失败。该命令不是标准的，所以选项C不可能。此文件可能不存在，即使存在，E也会运行路径上找到的`myprog`的第一个实例，并且额外会在后台执行中详细地运行该程序。
