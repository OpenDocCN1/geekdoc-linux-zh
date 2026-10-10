
## SSH 流程

如图 1.6 所示，SSH 流程如下：

-   左侧的 SSH 客户端向右侧的 SSH 服务器提供身份验证。在初始连接中，客户端会接收服务器的**主机密钥**；因此，在随后的所有连接中，客户端都知道它正在连接到同一个 SSH 服务器。这使得 SSH 服务器的 IP 地址（容易被欺骗）受到的重视降低，而服务器的主机密钥（不容易被欺骗）受到的重视增加。
-   SSH 服务器通过验证客户端用于身份验证的**用户名/密码**或**公钥**，来确定客户端是否有权连接 SSH 服务。此过程完全加密。
-   如果 SSH 服务器验证了客户端且客户端拥有权限，则两个实体之间开始 SSH 会话。所有通信均完全加密。

SSH 的客户端/服务器架构允许客户端拥有用于身份验证和/或授权的单一来源。身份验证/授权的单一来源仅允许访问 SSH 服务，而访问电子邮件、内网、外网和 IRC 等其他各种服务则需要进一步的认证。此外，如前文所述的 SSH 代理的使用，单一身份验证来源可以提供对应用程序的访问，而无需更多的用户名和密码。

## SSH 的加密架构

SSH 的众多优点之一是它提供了用于传输信息的完全加密协议，但 SSH 使用的是什么加密架构，它是如何部署的？本书不会详细探讨所使用的加密算法或在 SSH 中的实现方式（因为优化和实现是本书的重点），但我确实简要考察了该架构，以提供有关其部署的一些背景知识。SSH 的实现架构与协议本身一样灵活。SSH1 与当今使用的主要加密算法兼容，包括以下算法：

-   3DES
-   Blowfish
-   Twofish (128 和 192)
-   AES (128、192 和 256)
-   Arc Four
-   CAST
-   DES
-   RC4

上述任何加密算法都可以用于 SSH 连接的**密码**。大多数密码都有很好的支持，但强烈建议使用更安全的 3DES 选项，而不是使用 DES。

除了上述密码算法外，SSH 还提供**消息认证码 (MAC)** 算法哈希。大多数 SSH 实现支持的两个选项是 MD5 和 SHA1。MAC 算法哈希用于**数据完整性**。从一个实体传输到另一个实体的数据会使用唯一的加密签名进行哈希处理，从而将其与其他数据区分开来。由 MD5 或 SHA1 哈希生成的加密签名在任何情况下从一个实体到下一个实体都不会改变。这确保了接收数据的实体在没有修改、篡改或未授权实体滥用通用情况的情况下获得了该数据。

## SSH 的基本问题

企业网络中使用的许多协议都存在一些安全问题。SSH 也不例外。SSH 提供了多种解决方案，但重要的是要提到 SSH 曾经存在安全问题，其中包括可能导致未经授权用户远程访问的几个问题。我不讨论与 OpenSSH 或其他 SSH 变种相关的所有安全问题。然而，我确实鼓励大家认识到，SSH 与任何程序或服务一样，需要定期打补丁。请告知您的内部补丁管理流程和网络运营人员定期修补和监控 SSH 服务。

与 SSH 相关的已识别的安全问题包括缓冲区溢出、X11 转发错误、弱的 Challenge/Responses 处理、远程信息泄露和权限提升。欲了解更多信息，请访问以下 URL 获取 OpenSSH 安全问题：www.openssh.com/security.html。

## SSH 客户端/服务器类型

SSH 客户端/服务器有多种软件包形式。以下是本书中提到的组织和产品的简短摘要。

### SSH 服务器

-   OpenSSH (www.openssh.com)
    -   OpenSSH 是 SSH 协议套件的免费版本。OpenSSH 服务器和客户端均可用于 Unix 和 Windows。
    -   OpenSSH 已通过流行的 CYGWIN 工具移植到 Windows。该项目由 Network Simplicity (www.networksimplicity.com) 创建，并被以下网站采用：http://lexa.mckenna.edu/sshwindows/。
-   SSH2 (www.ssh.com)
    -   SSH2 是 SSH 的商业版本，商用需要支付许可费（非商用免费）。商业 SSH 客户端/服务器均可用于 Windows 和 Unix 系统。

### VanDyke Software (www.vandyke.com)

-   VanDyke Software 制造商业版本的 SSH，使用需要支付许可费。商业 SSH 服务器 (VShell) 和客户端 (SecureCRT) 可用于 Windows 操作系统。

### SSH 客户端

-   商业 SSH
-   OpenSSH
-   PuTTY
-   Secure-CRT
-   MindTerm——通过 Java 和 Web 浏览器实现的 SSH
-   WinSCP

## SSH 的基本设置

本节重点介绍在 Unix 和 Windows 环境中设置 SSH 服务器。该设置基于您选择的操作系统创建了一个基础 SSH 服务器安装，从而能够讨论本书中出现的各种 SSH 功能。以下列出了演示的实现类型：

-   Unix 上的 OpenSSH (Red Hat Linux 8.0 和 OpenBSD 3.1)
-   Windows 上的 OpenSSH (Windows 2000 Server)
-   Unix 上的商业 SSH (Red Hat Linux 8.0 和 OpenBSD 3.1)
-   Windows 上的商业 SSH (Windows 2000 Server)
-   Windows 上的 VShell SSH 服务器 (Windows 2000 Server)

许多操作系统，如 OpenBSD，默认加载了 OpenSSH。为了本节的宗旨，我假设您的系统没有预装任何类型的 SSH 服务器。如果您有一台机器已经监听着 SSH 服务/守护程序，请随意跳过本节。

### OpenSSH

以下段落描述了使用 OpenSSH 的流行服务器。

### Red Hat Linux 8.0

以下是在 Red Hat 8.0 上安装 SSH 的分步程序。

#### 基于 RPM 的实现

在 Red Hat 8.0 服务器完全安装后，使用您最喜欢的 FTP 客户端，如命令行客户端或内置 Web 浏览器的 FTP 功能，从 ftp://ftp5.ustc.openbsd.org/pub/OpenBSD/OpenSSH/portable/rpm/RH80 下载最新的 RPM (Red Hat Package Manager)。我将使用版本 3.5 (openssh-3.5p1-1.i386.rpm)。将 RPM 下载到您选择的目录；我推荐 /usr/local/src。一旦文件下载完成，请按照以下步骤操作：

1.  在 shell 中，更改目录到 OpenSSH RPM 的下载位置：
    ```bash
    # cd /usr/local/src
    ```
2.  安装 OpenSSH RPM：
    ```bash
    # rpm -i openssh-3.5p1-1.i386.rpm
    ```

要启动守护程序，请更改到安装目录并启动服务：

```bash
# cd /usr/sbin
# ./sshd -p 22
```

请注意，如果您使用默认端口 (22)，则不需要 -p 选项。此时，您的 Red Hat 8.0 机器上应该已经在端口 22 上运行了 SSH 服务器。要确认这一点，请输入 `netstat -an`，您应该看到图 1.7 中所示的屏幕。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_45_0.png)

请注意，所有由 0.0.0.0 表示的接口都在监听端口 22，即 SSH。

#### 基于软件包的实现

在 Red Hat 8.0 服务器完全安装后，使用您最喜欢的 FTP 客户端，如命令行客户端或内置 Web 浏览器的 FTP 功能，从 ftp://ftp3.usa.openbsd.org/pub/OpenBSD/OpenSSH/portable/openssh03.5p1.tar.gz 下载最新的软件包。我将使用版本 3.5 (openssh-3.5p1.tar.gz)。将软件包下载到您选择的目录；我推荐 /usr/local/src。一旦文件下载完成，请执行以下步骤：

1.  在 shell 中，更改目录到 OpenSSH 软件包的下载位置：
    `# cd /usr/local/src`
2.  使用 gunzip 解压 tarball：
    `# gunzip -c openssh-3.5p1.tar.gz | tar xvf -`
3.  更改目录到 SSH：
    `# cd openssh-3.5p1`
4.  配置目标文件和依赖项：
    `# ./configure`
5.  创建二进制文件：
    `# make`
    `# make install`

**完成了！**
要启动守护程序，请更改到安装目录并启动服务：
`# cd /usr/local/src/ssh`
`# ./sshd -p 22`
请注意，如果您使用默认端口 (22)，则不需要 -p 选项。

