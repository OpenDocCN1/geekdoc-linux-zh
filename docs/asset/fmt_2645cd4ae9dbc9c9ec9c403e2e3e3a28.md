
8. 进行一些优化：

- **Web、telnet 和 ssh 流量最小延迟：**

```bash
iptables -t mangle -A PREROUTING -m multiport -p tcp --dport 80,23,22 -j TOS --set-tos 16
iptables -t mangle -A PREROUTING -m multiport -p tcp --sport 80,23,22 -j TOS --set-tos 16
```

- **FTP 数据最大吞吐量：**

```bash
iptables -t mangle -A PREROUTING -p tcp --dport ftp-data -j TOS --set-tos 8
iptables -t mangle -A PREROUTING -p tcp --sport ftp-data -j TOS --set-tos 8
```

- **smtp 最大可靠性：**

```bash
iptables -t mangle -A PREROUTING -p tcp --dport smtp -j TOS --set-tos 4
```

- **pop-3 最小成本：**

```bash
iptables -t mangle -A PREROUTING -p tcp --dport 110 -j TOS --set-tos 2
```

还有最后一组规则，你可能想用它来阻止 IP 欺骗（即外部有人冒充你）。任何人都不应该声称来自内部而连接到外部接口。下面的规则可以让你丢弃这些数据包（但请记住，如果你已开启 `/proc/sys/net/ipv4/conf/all/rp_filter`，内核会丢弃伪造的数据包）：

```bash
iptables -I FORWARD -i eth1 -s 192.168.0.0/24 -j DROP
iptables -I FORWARD -i eth1 -s 127.0.0.0/8 -j DROP
iptables -I INPUT -i lo -s 127.0.0.1 -j DROP
```

别忘了：

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

还可以（也许）加上：

```bash
echo 1 > /proc/sys/net/ipv4/conf/rp_filter/all
```

这应该能让你对 `iptables` 的灵活性有所了解。一些来自不同来源的程序可以帮助你创建防火墙规则。但请记住，要通过向其发送流量并记录结果来测试你的规则。

## 第37章：远程管理

本章内容包括

- 加密 722
- OpenSSL 722
- OpenSSH 723
- Net_SSLeay 725
- Webmin 726
- 故障排除 728

### 加密

你需要了解如何安装和配置 `OpenSSH` 和 `Webmin`，以便安全地进行远程系统管理。你会希望能够远程管理那些你并非时刻坐在面前的所有系统，而不是以明文形式发送信息。虽然用户本身不是问题所在，但通过任何网络以未加密方式发送密码，都会让连接到该网络的任何人看到你的密码。那个人只需使用一个能捕获流经网络流量的程序即可。

近期（2000 年初）的裁决已取消了美国对加密材料出口的多项限制，这意味着加密技术现在更容易获取。这种可获取性对于电子商务和远程系统管理至关重要。虽然并非所有限制都已取消，但解除的程度已足以让用户使用 128 位（1024 位）加密——这是当今进行安全交易的最低要求。

美国制作的 Linux 发行版仍然不能包含某些加密程序，因此你必须自行下载并安装这些程序。不过别担心；这很容易，本章将一步步带你完成。你将首先学习 `OpenSSL`，它是所有其他安全程序和模块的基础；然后学习 `OpenSSH`，它支持安全的 telnet 和文件传输。最后，你将了解 Perl 的 `Net_SSLeay` 模块，它允许你使用 Netscape 通过加密的 `Webmin` 会话安全地管理系统。

> **注意：** 在世界许多地方，加密技术的使用受到限制或被禁止。你有责任遵守所在国家关于加密技术的法律。如果这使你的系统面临风险，你需要与你的政府进行协商。

### OpenSSL

在你开始安装 `OpenSSH` 或 Perl 的 `Net_SSLeay.pm` 模块之前，你需要先安装 `OpenSSL`。`OpenSSL` 为加密过程提供安全套接层（SSL）库。务必确保获取最新版本，并保持其更新。

`OpenSSL` 软件包可以从 `http://www.openssl.org/source/` 获取。确保你拿到的是最新版本，其名称旁边会标有 `[LATEST]`。

在美国，你需要获取并编译 RSA 公司的 RSAref 库。幸运的是，RSA 的专利将于 2000 年 11 月到期，因此在那之后你就不再需要它了（除非 RSA 设法延长了专利期）。如果你处于不需要使用它的位置，就不要安装它。这个库比较陈旧，并且至少包含一个已知的安全漏洞。如果你确定确实需要它，RSA 已不再提供该库，所以你需要自行在互联网上搜索。要小心，因为一些欧洲网站提供了该库的欧洲改写版本，如果你在美国，你不会需要那个版本。只要仔细按照说明操作，你应该可以顺利链接它。

> **提示：** 要安装 `OpenSSL`，你需要先安装 `Perl 5`。

下载库后，运行以下命令（假设最新版本是 `openssl-0.9.5`）：

```
tar xzvf openssl-0.9.5.tar.gz
```

你运行的命令应与下载的软件包版本相匹配。

当软件包解压完成后，你会得到一个名为 `openssl-0.9.5` 的目录，你需要 `cd` 进入该目录。

当你进入 `openssl` 构建目录后，运行以下命令：

```
./config && make
```

此命令会检测你系统的几项配置，如果成功，你应该运行 `make`。`make` 完成后，成为 `root` 用户（如果你还不是），然后运行此命令：

```
make install
```

### OpenSSH

`OpenSSH` 软件包允许你运行一个安全外壳服务器，并使用安全外壳客户端连接到它。两者之间的所有通信都是加密的。从 `http://violet.ibs.com.au/openssh/files/` 下载 SSH 软件包。

不要获取源码 RPM 软件包。源码 RPM 只有在安装了 GNOME 的情况下才能构建，这是 Red Hat 专用的 RPM。二进制 RPM 也是如此；它们无法正常工作。请获取源文件。

获取源文件后，按照与 `OpenSSL` 软件包相同的方式解压（假设你的 `OpenSSH` 版本是 `1.2.3`）：

```
tar xzvf openssh-1.2.3.tar.gz
```

`cd` 进入构建目录并运行 `configure`：

```
cd openssh-1.2.3 ; ./configure --with-ssl-dir=/usr/local/ssl && make
```

`make` 成功后，运行以下命令：

```
make install
```

安装过程会安装二进制文件，但不会生成二进制文件所需的服务器密钥。要安装服务器密钥，请运行以下命令：

```
ssh-keygen
```

在密钥生成过程中，系统会要求你提供一个密码——请勿提供，否则你将无法启动服务器。只有在你想为自己生成个人密钥并加以保护时才应使用密码。当密钥生成后，它会询问你希望将密钥写入何处。告诉它写入 `/usr/local/etc/ssh_host_key`。

要开始使用服务器，你需要确保它已启动。以 `root` 身份运行 `sshd`。这会启动服务器程序，它将绑定端口 22。

你可以通过连接到服务器来测试其是否正常工作：

```
ssh localhost
```

这应该会提示你输入密码。与 `telnet` 不同，允许 `root` 登录是安全的，因为整个会话（包括用户名和密码的提示）都是加密传输的。然而，`OpenSSH` 的 PAM 文件默认仍禁止 `root` 登录。要更改此设置，请 `cd` 到 `/etc/pam.d` 并在以下行前面加上 `#`：

```
auth                 required             pam_securetty.so
```

> 根据 `OpenSSH` 的版本以及随附的 PAM 文件（你需要将该文件复制到 `/etc/pam.d/`），你可能只需要构建一个正确的、可用的 `sshd` PAM 文件即可。你的 `sshd` PAM 文件应该看起来像这样：

```
#%PAM-1.0
# [对于 1.0 版本的语法，上述头部是可选的]
#
# sshd 服务的 PAM 配置文件
#
auth                 required             pam_pwdb.so
auth                 required             pam_nologin.so
```
