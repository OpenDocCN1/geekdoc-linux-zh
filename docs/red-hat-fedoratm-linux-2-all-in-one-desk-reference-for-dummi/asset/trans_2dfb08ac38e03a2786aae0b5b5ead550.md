
# 第 2 章：主机安全加固

### 本章内容

-   加固密码
-   保护文件和目录
-   使用 GnuPG 加密和签名文件
-   监控系统安全性

*主机*（Host）是指你的 Fedora Core 系统的技术术语——尤其是在你将其用于提供网络服务时。但即使你只是单独思考这台计算机，这个术语也说得通；它是运行在其上的所有内容的宿主——操作系统以及所有应用程序。计算机安全的一个关键方面是保护主机。

在本章中，我将引导你了解保护 Fedora Core 主机的几个关键步骤。这些步骤包括安装操作系统更新、保护密码、保护文件和目录、在必要时使用加密，以及监控系统的安全性。你可以通过检查日志文件中是否存在可疑活动，以及使用 Tripwire 工具查看是否有人对系统中的重要文件进行了篡改，来监控主机安全性。

### 安装操作系统更新

Fedora Core 及相关应用程序的更新以 RPM 文件形式提供。要手动下载并安装更新，请遵循以下步骤：

1.  **以 root 身份登录并创建一个用于存放更新的目录：**
    ```bash
    mkdir /usr/local/updates
    cd /usr/local/updates
    ```
2.  **使用 `wget` 命令从红帽 FTP 站点下载更新。**
    例如，要下载 Fedora Core 2 i386 版本的更新，请输入：
    ```bash
    wget ftp://download.fedora.redhat.com/pub/fedora/linux/core/updates/2/i386/*.rpm
    ```
3.  **使用以下命令安装所有更新：**
    ```bash
    rpm -F *
    ```
4.  **使用以下命令删除更新文件：**
    ```bash
    rm -fr /usr/local/updates
    ```

### 加固密码

从历史上看，UNIX 密码存储在 `/etc/passwd` 文件中，任何用户都可以读取该文件。例如，典型的旧式 `/etc/passwd` 文件中 root 用户的条目看起来像这样：

`root:t6Z7NWDKlK8sU:0:0:root:/root:/bin/bash`

字段由冒号（`:`）分隔，第二个字段包含加密形式的密码。为了检查密码是否有效，登录程序会对用户输入的明文密码进行加密，并将其与 `/etc/passwd` 文件中的内容进行比较。如果匹配，则允许用户登录。

密码破解程序的工作原理与登录程序类似，不同之处在于这些程序每次从字典中挑选一个单词，加密该单词，并将其与 `/etc/passwd` 文件中的加密密码进行比较以寻找匹配项。为了破解密码，入侵者需要获取 `/etc/passwd` 文件。通常，破解者利用各种 Internet 服务器（如邮件和 FTP）的漏洞来获取 `/etc/passwd` 文件的副本。

最近，多项改进措施使 Fedora Core 中的密码更加安全。这些改进包括影子密码和可插入身份验证模块，你在安装 Fedora Core 时就可以轻松安装这些功能。在安装 Fedora Core 期间，有一个步骤涉及在身份验证配置屏幕中进行选择。如果你接受默认选择——启用 MD5 密码和启用影子密码——你将自动在 Fedora Core 中启用更安全的密码。

#### 影子密码

显然，让密码随处可见且任何人都能获取——即使它们是加密的——都是不良的安全做法。因此， Fedora Core 现在不再将密码存储在 `/etc/passwd` 文件（任何用户均可读取）中，而是将其存储在影子密码文件 `/etc/shadow` 中。只有超级用户（root）可以读取此文件。例如，这是新式 `/etc/passwd` 文件中 root 的条目：

`root:x:0:0:root:/root:/bin/bash`

在这种情况下，请注意第二个字段包含的是 `x` 而不是加密的密码。`x` 是*影子密码*；实际的加密密码现在存储在 `/etc/shadow` 文件中，其中 `root` 的条目看起来像这样：

```
root:$1$AAnI/yN$uEShbzUppY9c$foo1Bf0t$S0:11077:0:99999:7:-1:1:134540536
```

`/etc/shadow` 条目的格式类似于 `/etc/passwd` 文件中的条目，使用冒号分隔字段，但大多数字段的含义不同。第一个字段仍然是用户名，第二个字段是加密的密码。

`/etc/shadow` 每个条目中的其余字段控制密码过期的时间。你不需要解析或修改 `/etc/shadow` 文件中的这些条目。相反，请使用 `chage` 命令来更改密码过期信息。首先，你可以通过使用带 `-l` 选项的 `chage` 命令来检查用户的密码过期信息，如下所示（在这种情况下，你必须**以 root 身份登录**）：

```
chage -l root
```

此命令显示过期信息，包括密码的有效持续时间和你更改密码的频率。

如果你希望确保用户每 90 天强制更改一次密码，你可以使用 `-M` 选项设置密码保持有效的最大天数。例如，为了确保用户 `naba` 在 90 天内被提示更改密码，我以 **root** 身份登录并输入以下命令：

```
chage -M 90 naba
```

你可以为每个用户账户使用此命令，以确保所有密码在适当时候过期，并且所有用户都必须选择新密码。

#### 可插入身份验证模块 (PAMs)

除了通过使用影子密码提高密码文件的安全性外，Fedora Core 还使用 RFC 1321 中描述的 MD5 信息摘要算法（`www.ietf.org/rfc/rfc1321.txt` 或 `www.cis.ohio-state.edu/cgi-bin/rfc/rfc1321.html`）提高了存储在 `/etc/shadow` 文件中密码的实际加密强度。MD5 将任意长度的消息缩减为 128 位消息摘要（或*指纹*），从而你可以使用你的私钥对其进行加密以实现数字签名。MD5 在密码加密方面也表现相当好。

![](img/9f89727199836b0f871f1745838aa8b2_563_0.png)

MD5 相对于旧式密码加密的另一个优势在于，旧式密码长度限制在最多八个字符；而新密码（使用 MD5 加密）可以长得多。即使 `/etc/shadow` 文件落入坏人手中，更长的密码也更难被猜到。

你可以通过观察 `/etc/shadow` 文件来判断是否启用了 MD5 加密。加密后的密码更长，并且它们都以 `$1$` 前缀开头，如下面示例条目的第二个字段所示：

```
root:$1$AAAAni/YN$uESHbzUpy9Cgfo0I8fOt5$:11077:0:99999:7:-1:-1:134540356
```

一个称为可插入身份验证模块（PAM）的附加程序模块执行实际的 MD5 加密。Fedora Core PAM 提供了一种灵活的用户身份验证方法。通过设置 PAM 的配置文件，你可以随时更改身份验证方法，而无需实际修改验证用户身份的关键程序（如 login 和 passwd）。

Fedora Core 广泛使用 PAM 功能。PAM 位于许多不同的模块中（稍后会详细介绍）；它们的配置文件位于系统 `/etc/pam.d` 目录中。通过输入以下命令查看此目录的内容：

```
ls /etc/pam.d
```

此目录中的每个配置文件都指定了特定工具如何验证用户。例如，你可以找到针对 login、passwd 和 su 的文件。以下是我在我的系统上输入 `cat /etc/pam.d/passwd` 文件时看到的内容：

```
#%PAM-1.0
auth    required    pam_stack.so service=system-auth
account   required    pam_stack.so service=system-auth
password  required    pam_stack.so service=system-auth
```

这些行表明，身份验证、账户管理和密码检查都是通过 pam_stack 模块（`/lib/security/pam_stack.so`）并使用参数 `service=system-auth` 来完成的。本质上，pam_stack 模块引用了 `/etc/pam.d` 目录中的另一个配置文件。在这种情况下，配置文件是 `/etc/pam.d/system-auth`。以下是我在我的 Fedora Core 计算机上 `/etc/pam.d/system-auth` 文件的内容：

```
#%PAM-1.0
# This file is auto-generated.
# User changes will be destroyed the next time authconfig is run.
auth    required    /lib/security/$ISA/pam_env.so
```

如果你更喜欢通过电子邮件接收定期安全更新，你还可以订阅（sign up for）各种邮件列表：

-   **FOCUS:LINUX:** 填写 www.securityfocus.com/cgi-bin/subscribe.pl 上的表单以订阅这个专注于 Linux 安全问题的邮件列表。
-   **US-CERT 国家网络安全警报系统：** 按照 www.us-cert.gov 上的说明订阅此邮件列表。网络安全警报系统通过其邮件列表提供四个类别的安全信息：
  - 技术网络安全警报提供有关常见软件产品中漏洞的技术信息。
  - 当漏洞影响公众时，会发送网络安全警报。它们概述了非技术家庭和企业计算机用户可以采取的步骤和措施，以保护自己免受攻击。
  - 网络安全公告是每两周发布一次的摘要，涵盖安全问题和新的漏洞，以及用户可以采取的帮助降低风险的补丁、变通方法和其他措施。
  - 网络安全提示为非技术计算机用户提供常见安全问题的建议。

最后，请查看 Fedora Core 网站 `fedora.redhat.com/download/updates.html` 上的更新，这些更新可能会修复 Fedora Core 中已知的任何安全问题。

