

- gnupg
- gzip
- hylafax
- inetd
- iproute
- KDE
- Kerberos
- kernel
- lprng
- lsh
- lynx
- mailman
- man
- Mozilla
- mpg123
- MPlayer
- mutt
- MySQL
- OpenSSH
- openssl
- Perl
- pine
- PHP
- Postfix
- PostgreSQL
- Proftpd
- Python
- Rsync
- Samba
- Screen
- Sendmail
- Snort
- Stunnel
- Sudo
- Tcpdump
- Vim
- Webmin
- Wget
- wu-ftpd
- xchat
- XFree86
- Xinetd
- Xpdf
- zlib

一些常见的漏洞如下：

- **BIND (*Berkeley Internet Name Domain*) 漏洞**：BIND 是一款流行的 DNS 软件，攻击者针对它来触发拒绝服务（DoS）事件。如果系统管理员未能及时更新其 BIND 版本，则容易受到进一步的攻击。

- **Linux 交叉引用器（LXR）漏洞**：Linux 交叉引用器（LXR）是一个用于索引和展示源代码库的软件工具集。LXR 主要与 Linux 工具集源代码一起使用，但它对其他源代码项目也很有用。它使用 Web 导航器来读取 Linux 内核源代码。它有助于通过传递变量 'v' 给脚本来导航不同的内核版本并获取版本号。要在没有过滤器的情况下打开文件，某些内容会被放置在 `.:` 特殊目录中。以下是一个利用调用的示例：
  `http://vulnerabile/source?v=.../..../..../..../..../...././etc/passwd%00.`

- **Util-Linux 漏洞**：本地用户可以利用 Util-Linux 漏洞执行未授权的权限操作，允许用户在未使用 nousid 选项的情况下重新挂载文件系统。Util-Linux 集合随 Linux 系统提供，并包含基本实用工具。此漏洞发生在 mount 和 umount 程序错误地检查 *setuid()* 和 *setgid()* 函数的返回值时。此漏洞可被利用来执行具有高权限的操作。

- **Linux 内核能力漏洞**：Linux 内核能力漏洞出现在试图将 root 权限分解为一系列能力的 *setcap()* 调用中。setuid 程序的能力可以被设置和修改，从而不向任何普通用户授予 root 权限。利用此漏洞，本地用户可以获取 root 权限。

## Chroot 技术

如果攻击者能够成功获取 root 用户权限，那么他或她将能够对该系统造成大量破坏。限制攻击破坏程度的一种方法是使用 chroot 技术。*Chroot* 是一个 Linux 安全特性，它允许用户选择应用程序可以访问的目录。此功能限制了非认证服务和入侵者对进程的滥用对整个目录树的访问。如果攻击者能够发现网络服务中的漏洞，他或她将能够访问远程系统和文件系统。然而，如果攻击者能够发现本地漏洞，他或她将会尝试获取 root 访问权限。Root 拥有大量的权限和许多能力。以 root 身份运行的服务可以被利用以获取额外的能力。大多数黑客的目标是获取受攻击机器的 root 访问权限。Chroot 技术通过限制 root 进程的权限来防止这种情况。进程被限制的目录被称为 chroot “监狱（jail）”。例如，假设一个程序 testscript.exe 被限制在 /usr/local/tester 下的目录树的一部分。通过对 testscript.exe 进行 chroot 监狱设置，该进程将能够访问 /usr/local/tester 内的文件或目录。如果 testscript.exe 尝试访问文件 /input.txt，它实际上会访问位于 /usr/local/tester/testscript/input.txt 的文件。如果管理员想要运行程序 testscript.exe，他或她可以在访问之前通过发出命令 `chroot /usr/local/tester /bin/testscript` 对其进行 chroot 操作。这将首先将根目录更改为 /usr/local/tester，然后运行程序 /bin/testscript。

### 工具：Addjailsw

Addjailsw 是一个帮助自动创建 chroot 监狱的工具。它将常用的调试程序复制到监狱中。它还可以帮助在 chroot 监狱中创建新用户。类似的程序包括 Cell 和 Zorp’s Jailer。

## 为什么 Linux 会被入侵？

Linux 成为许多攻击目标的原因有很多。首先，Linux 是一个吸引人的目标，因为它在大量服务器上被广泛使用，使其成为事实上的骨干网络。其次，由于代码是免费提供的，更容易发现漏洞。第三，Linux 默认安装了大量的应用程序，使系统容易受到攻击。除非系统管理员小心地设置策略并更新程序，否则安全漏洞可能会蔓延。

一些预测问题的良好对策包括：

- 在程序中没有必要时，关闭 *suid* 和 *sgid* 权限。这可以防止攻击者利用缓冲区溢出升级他或她的权限。
- 诸如 StackGuard、Libsafe 和 Openwall Project 的非可执行堆栈内核补丁之类的软件。

- StackGuard 是一种编译器，通过增强程序来抵御堆栈破坏攻击。使用 StackGuard 编译的程序不需要任何源代码更改。它通过在返回指针旁边放置一个“金丝雀（canary）”字来工作。金丝雀字的改变表示攻击并终止程序。
- Libsafe 是一个动态加载库，它检查对易受攻击的库函数的所有调用。它通过将易受攻击的函数替换为功能等效的函数来工作。它没有高性能开销，并且已知能够避免即使是未知的缓冲区溢出攻击。
- Openwall Project 的非可执行堆栈内核补丁是 Linux 内核的一组安全特性，使堆栈不可执行。虽然它不能阻止所有缓冲区溢出攻击，但它可以向用户警告简单的尝试。

缓冲区溢出是漏洞的常见原因。必须采取一些安全措施来保护 Linux 操作系统免受已知或未知缓冲区溢出的利用。

## 如何对存在漏洞的程序应用补丁

用户可以审计开源程序中的漏洞和安全缺陷。用户可以检查其 Linux 发行版的首页以获取更新。他们还可以检查软件供应商的网站并查找补丁。这些包括：

- LCLint 检查 C 程序中的缺陷，如内存管理错误、不一致的数据共享、不正确的链接、解引用空指针等。
- Cqual 允许编码者定义类型限定符。它是一个类型检查器，执行限定符推断以检查注释。
- 安全粗糙审计工具（RATS）验证和审计 C、C++、Perl、Python 和 PHP 代码。它充其量只是一个初步检查，不能用作代码检查的替代。
- Flawfinder 审计代码中函数的安全缺陷，这些函数被发现特别容易受到缓冲区溢出（*strcpy*()）、格式错误（*printf*()）、竞态条件（*chmod*()）、shell 元字符问题（*system*()）、随机数生成（*random*()）以及其他问题的影响。
- Spike 用于协议分析并作为复现工具，而 sharefuzz 是一个使用 LD_PRELOAD 分析 suid 程序中缓冲区溢出的程序。

用户还可以使用运行在本地系统安全性上的系统扫描器，并识别潜在的安全漏洞。这些包括 sXid、COPS、TAMU's Tiger、GNU Tiger、Nabou 和 LSAT。

## 网络扫描

一旦知道目标系统的 IP 地址，攻击者就可以开始端口扫描过程，或者寻找系统中的漏洞。一个典型的系统有 2^16 − 1 个端口号，每个号码有一个 TCP 端口和一个 UDP 端口。这些端口中的每一个都是进入系统的潜在途径。Linux 上最流行的扫描工具是 Nmap。其他工具包括 nescat 和 strobe。

Nescat 可用于扫描高达 2024 的端口。Nescat 扫描每个端口并等待 10 秒超时。然后它显示结果。Nescat 可以使用以下命令启动：

```
nc -v -w 10 -z www.example.com 1-2024
```

Strobe 并行扫描端口，使用最大带宽同时消耗最少资源。Strobe 能够单独扫描 TCP 端口。然而，其开发者不再维护 strobe。

## Linux 中的 Nmap

Nmap 无疑是目前可用的最佳端口扫描器，此外还具有操作系统检测、RPC 识别和 ping 扫描的附加功能。Nmap 还附带一个前端，Nmapfe，赋予其图形用户界面。Nmap 还可以作为网络管理员有价值的诊断工具。

