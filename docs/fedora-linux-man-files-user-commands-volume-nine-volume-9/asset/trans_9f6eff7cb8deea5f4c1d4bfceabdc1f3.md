
## 环境变量

**ssh** 通常会设置以下环境变量：

- **DISPLAY**
  **DISPLAY** 变量指示 X11 服务器的位置。它会被 **ssh** 自动设置为 "hostna:n" 形式的值，其中 "hostna" 指示运行 shell 的主机，'n' 是大于或等于 1 的整数。**ssh** 使用这个特殊值通过安全通道转发 X11 连接。用户通常不应显式设置 **DISPLAY**，因为这会使 X11 连接变得不安全（并且要求用户手动复制所需的授权 cookie）。
- **HOME**
  设置为用户主目录的路径。
- **LOGNAME**
  这是 **USER** 的同义词，为那些使用此变量的系统而设置的兼容项。
- **MAIL**
  设置为用户邮箱的路径。
- **PATH**
  设置为编译时指定的默认 **PATH**。
- **SSH_ASKPASS**
  如果 **ssh** 需要密码短语，如果它是从终端运行的，它将从当前终端读取密码短语。如果 **ssh** 没有关联的终端但设置了 **DISPLAY** 和 **SSH_ASKPASS**，它将执行由 **SSH_ASKPASS** 指定的程序并打开一个 X11 窗口来读取密码短语。这在从 .xsession 或相关脚本调用 **ssh** 时特别有用。（注意，在某些机器上，可能需要将输入重定向到 /dev/null 才能使此功能正常工作。）
- **SSH_AUTH_SOCK**
  标识用于与 agent 通信的 UNIX 套接字的路径。
- **SSH_CONNECTION**
  标识连接的客户端端和服务器端。该变量包含四个以空格分隔的值：客户端 IP 地址、客户端端口号、服务器 IP 地址和服务器端口号。
- **SSH_ORIGINAL_COMMAND**
  如果执行了强制命令，此变量包含原始命令行。它可以用于提取原始参数。
- **SSH_TTY**
  此变量被设置为与当前 shell 或命令关联的 tty 的名称（设备的路径）。如果当前会话没有 tty，则不设置此变量。
- **TZ**
  如果在守护进程启动时设置了时区，则会设置此变量以指示当前时区（即守护进程将该值传递给新连接）。
- **USER**
  设置为登录用户的名称。

此外，**ssh** 会读取 `~/.ssh/environment`，如果该文件存在并且用户被允许更改其环境，则会将格式为 “`VARNAME=value`” 的行添加到环境中。更多信息，请参阅 `sshd_config` 5 中的 **PermitUserEnvironment** 选项。

### SSH_USE_STRONG_RNG

OpenSSL 随机数生成器的重新播种通常来自 **/dev/urandom**。如果设置了 **SSH_USE_STRONG_RNG** 环境变量且其值不为 **0**，则 OpenSSL 随机数生成器将从 **/dev/random** 重新播种。读取的字节数由 SSH_USE_STRONG_RNG 的值定义。最小值为 14 字节。不建议在没有硬件随机数生成器的计算机上使用此设置，因为熵不足会导致连接被阻塞，直到有足够的熵可用。

## 文件

**~/\.rhosts**

此文件用于基于主机的身份验证（见上文）。在某些机器上，如果用户主目录位于 NFS 分区上，此文件可能需要对所有人可读，因为 (8) 以 root 身份读取它。此外，此文件必须由用户拥有，且不得具有其他任何人的写入权限。大多数机器推荐的权限是用户可读写，其他人不可访问。

**~/\.shosts**

此文件的使用方式与 .rhosts 完全相同，但允许基于主机的身份验证，而不允许通过 rlogin/rsh 登录。

**~/\.ssh/**

此目录是所有用户特定配置和身份验证信息的默认位置。没有普遍要求将此目录的全部内容保密，但推荐的权限是用户可读写执行，其他人不可访问。

**~/\.ssh/authorized_keys**

列出可用于以该用户身份登录的公钥（DSA、ECDSA、Ed25519、RSA）。此文件的格式在 (8) 手册页中有描述。此文件不是高度敏感的，但推荐的权限是用户可读写，其他人不可访问。

**~/\.ssh/config**

这是每个用户的配置文件。文件格式和配置选项在 ssh_config5 中有描述。由于滥用的可能性，此文件必须具有严格的权限：用户可读写，其他人不可写。

**~/\.ssh/environment**

包含环境变量的额外定义；参见上文中的 **ENVIRONMENT**。

**~/\.ssh/identity**
**~/\.ssh/id_dsa**
**~/\.ssh/id_ecdsa**
**~/\.ssh/id_ed25519**
**~/\.ssh/id_rsa**

包含用于身份验证的私钥。这些文件包含敏感数据，应允许用户读取但其他人不可访问（读/写/执行）。如果私钥文件可被其他人访问，**ssh** 将简单地忽略它。生成密钥时指定密码短语是可能的，该密码短语将用于使用 3DES 加密此文件的敏感部分。

**~/\.ssh/identity.pub**
**~/\.ssh/id_dsa.pub**
**~/\.ssh/id_ecdsa.pub**
**~/\.ssh/id_ed25519.pub**
**~/\.ssh/id_rsa.pub**

包含用于身份验证的公钥。这些文件不是敏感的，可以（但不一定需要）被任何人读取。

**~/\.ssh/known_hosts**

包含用户已登录的所有主机的主机密钥列表，这些主机尚不在系统范围的已知主机密钥列表中。有关此文件格式的进一步详细信息，请参阅 (8)。

**~/\.ssh/rc**

此文件中的命令在用户登录时由 **ssh** 执行，就在用户的 shell（或命令）启动之前。更多信息请参阅 (8) 手册页。

**/etc/hosts.equiv**

此文件用于基于主机的身份验证（见上文）。它应该只能由 root 写入。

**/etc/ssh/shosts.equiv**

此文件的使用方式与 hosts.equiv 完全相同，但允许基于主机的身份验证，而不允许通过 rlogin/rsh 登录。

**/etc/ssh/ssh_config**

系统范围的配置文件。文件格式和配置选项在 ssh_config5 中有描述。

- /etc/ssh/ssh_host_key
- /etc/ssh/ssh_host_dsa_key
- /etc/ssh/ssh_host_ecdsa_key
- /etc/ssh/ssh_host_ed25519_key
- /etc/ssh/ssh_host_rsa_key

这些文件包含主机密钥的私有部分，用于基于主机的身份验证。如果使用协议版本 1，**ssh** 必须设置为 root，因为主机密钥只能由 root 读取。对于协议版本 2，**ssh** 使用 ssh-keysign8 来访问主机密钥，从而消除了在使用基于主机的身份验证时需要将 **ssh** 设置为 root 的要求。默认情况下，**ssh** 不是以 root 身份设置的。

**/etc/ssh/ssh_known_hosts**

系统范围的已知主机密钥列表。此文件应由系统管理员准备，包含组织中所有机器的公有主机密钥。它应该对所有人可读。有关此文件格式的进一步详细信息，请参阅 (8)。

**/etc/ssh/sshrd**

此文件中的命令在用户登录时由 **ssh** 执行，就在用户的 shell（或命令）启动之前。更多信息请参阅 (8) 手册页。

## 退出状态

**ssh** 以远程命令的退出状态退出，或者在发生错误时以 255 退出。

## IPv6

IPv6 地址可以在使用 IPv4 地址的任何地方使用。在所有条目中，IPv6 地址必须用方括号括起来。注意：方括号是 shell 的特殊字符，必须在 shell 中进行转义。

## 另请参阅

(1), (1), ssh-add1, ssh-agent1, ssh-keygen1, ssh-keyscan1, (4), ssh_config5, ssh-keysign8, (8)

## 标准

- S. Lehtinen C. Lonvick 2006 年 1 月 *RFC 4250 安全 Shell (SSH) 协议分配编号*
- T. Ylonen C. Lonvick 2006 年 1 月 *RFC 4251 安全 Shell (SSH) 协议体系结构*
- T. Ylonen C. Lonvick 2006 年 1 月 *RFC 4252 安全 Shell (SSH) 认证协议*
- T. Ylonen C. Lonvick 2006 年 1 月 *RFC 4253 安全 Shell (SSH) 传输层协议*
- T. Ylonen C. Lonvick 2006 年 1 月 *RFC 4254 安全 Shell (SSH) 连接协议*
- J. Schlyter W. Griffin 2006 年 1 月 *RFC 4255 使用 DNS 安全发布安全 Shell (SSH) 密钥指纹*
- F. Cusack M. Forssen 2006 年 1 月 *RFC 4256 安全 Shell 协议 (SSH) 的通用消息交换认证*
- J. Galbraith P. Remaker 2006 年 1 月 *RFC 4335 安全 Shell (SSH) 会话通道中断扩展*
- M. Bellare T. Kohno C. Namprempre 2006 年 1 月 *RFC 4344 安全 Shell (SSH) 传输层加密模式*
- B. Harris 2006 年 1 月 *RFC 4345 改进的安全 Shell (SSH) 传输层协议中的 Arcfour 模式*
- M. Friedl N. Provos W. Simpson 2006 年 3 月 *RFC 4419 安全 Shell (SSH) 传输层协议的 Diffie-Hellman 组交换*
- J. Galbraith R. Thayer Noever 2006 年 *RFC 4716 安全 Shell (SSH) 公钥文件格式*
- D. Stebila J. Green 2009 年 12 月 *RFC 5656 安全 Shell 传输层中的椭圆曲线算法集成*
- A. Perrig D. Song 1999 年 *国际密码技术与电子商务研讨会 (CrypTEC ’99) 哈希可视化：一种提高现实世界安全性的新技术*
