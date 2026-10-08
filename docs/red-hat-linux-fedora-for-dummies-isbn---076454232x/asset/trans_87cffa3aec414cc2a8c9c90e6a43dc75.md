
3. 输入你的用户名和密码。

4. 在 `sftp` 提示符下输入 `help` 命令。

你将看到一系列 `sftp` 命令。你使用最频繁的命令是 `cd`、`lcd`、`dir`、`ls`、`get` 和 `put`。这些命令的工作方式与其 Linux 等价命令类似。

使用 `sftp` 非常直观。使用 `get` 将文件、多个文件或目录从远程机器传输到本地机器；使用 `put` 则从本地传输到远程。

![](img/8c094d1b36276212c03d10d898508a6e_267_0.png)

**提示**

OpenSSH 的另一个酷炫功能是它可以隧穿任何协议。例如，你实际上可以通过 X 窗口系统从远程机器显示整个 X 窗口。有关更多信息，请查阅 OpenSSH 文档。

## 配置 OpenSSH 服务器

配置 OpenSSH 服务器很简单。你只需修改 `/etc/ssh/sshd_config` 文件并运行 `/etc/init.d/sshd` 脚本。让我们来看看配置文件，其重要部分如下所示：

-   **移除较旧的、有缺陷的协议版本 1：** 版本 1 存在漏洞且不应使用（将参数 `Protocol 2,1` 更改为 `Protocol 2`，如本例所示）：

```
Port 22
Protocol 2
# HostKeys for protocol version 2
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_dsa_key
```

-   **移除登录宽限时间参数前的注释：** 此操作设定了从开始登录到完成登录的时限：

```
LoginGraceTime 600
```

-   **禁止 root 登录：** 你应该防止用户（包括你自己）直接以 root 身份登录。强制用户先以普通用户身份登录，然后“su”切换到 root，可以提供审计跟踪，用于查看谁以 root 身份执行了什么操作；这也迫使每个人在成为全能的 root 用户之前必须经过两道关卡：

```
PermitRootLogin no
StrictModes yes
```

**取消注释这些参数以允许各种身份验证模式：**

```
# rhosts authentication should not be used
RhostsAuthentication no
# Don't read the user's ~/.rhosts and ~/.shosts files
IgnoreRhosts yes
# For this to work you will also need host keys in
/etc/ssh/ssh_known_hosts
RhostsRSAAuthentication no
# similar for protocol version 2
HostbasedAuthentication no
# Change to yes if you don't trust ~/.ssh/known_hosts for
RhostsRSAAuthentication and HostbasedAuthentication
IgnoreUserKnownHosts no
```

**允许人们使用密码身份验证，但不允许未通过身份验证的访问：**

```
# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication yes
PermitEmptyPasswords no
```

要启动 OpenSSH 守护程序，请遵循以下步骤：

1.  **进行修改并重启 Secure Shell 守护程序：**
    ```bash
    /etc/init.d/sshd restart
    ```
2.  **如果你正在运行防火墙，请将此规则添加到基于 iptables 的防火墙中：**
    ```bash
    iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
    ```
3.  **保存你的新防火墙配置：**
    ```bash
    iptables-save > /etc/sysconfig/iptables
    ```
4.  **重启防火墙：**
    ```bash
    /etc/init.d/iptables restart
    ```

现在，你可以使用 OpenSSH 客户端和服务器与你的 Linux 计算机进行通信。使用 OpenSSH 客户端，你可以交互式登录到其他计算机，在计算机之间复制数据，并搭载任意通信流——例如 X 窗口——这个小家伙能做到这些。你可以反过来这个过程，与你的主机 Red Hat Linux 计算机通信。OpenSSH 加密你的所有通信，并防止你的密码和数据被窥探者获取。

## 交换密钥让你的生活更轻松

默认情况下，你使用传统的密码通过 OpenSSH 登录到远程用户账户。然而，OpenSSH 可以使用第二种身份验证方法，这种方法开始时稍费些功夫，但长期来看能省去很多麻烦。

OpenSSH 提供一种称为公钥密码学的身份验证方法。该系统使用一对公钥和私钥。你将公钥安装在远程系统上，并将私钥保留在你的计算机上。公钥可以与任何人共享——嘿，它是公有的。私钥必须不惜一切代价保密。事实上，OpenSSH 默认对私钥进行加密。在使用私钥之前，你必须使用一个口令短语——本质上是一个带空格的密码——来解密私钥。

当你想要登录或远程通信时，这些密钥将用于协商过程。公私钥系统保证你的用户账户已通过身份验证，并且是发起主机；密码仅验证你的登录账户，而不是你正在连接到的计算机。

## 设置公钥密码交换

要设置密钥交换，请遵循以下步骤：

1.  登录到本地计算机上的用户账户。
    例如，以用户 `rod` 身份登录到 `cancun`。
2.  打开一个 GNOME 终端会话。
3.  运行此命令：
    ```bash
    ssh-keygen -t dsa
    ```
    此步骤启动了生成你的公钥和私钥的程序。存在几种加密方法：DSA（数字签名标准）和 RSA（以 Ron Rivest、Adi Shamir 和 Len Adleman 命名）是最流行的。DSA 是一种非专有算法，而 RSA 直到最近才拥有专利。尽管 RSA 已可公共使用，但我们建议使用 DSA。

    程序会思考片刻并返回此输出：
    ```
    Enter file in which to save the key (/home/rod/.ssh/id_dsa):
    ```

![](img/8c094d1b36276212c03d10d898508a6e_269_0.png)

密钥保存在你主目录下的 `.ssh` 目录中。默认值应该没问题，因此按 Enter 键。

4.  `ssh-keygen` 程序会要求你输入一个口令短语，用于加密你的私钥：
    ```
    Enter passphrase (empty for no passphrase):
    ```
5.  输入你的口令短语，`ssh-keygen` 将生成密钥。

    使用包含数字和其他字符的短语。例如，你可以尝试这样的口令短语：
    ```
    Giv3 m3 @ bre@k!
    ```
6.  通过第二次输入短语来验证。

    `ssh-keygen` 程序生成你的公钥和私钥。这些密钥默认存储在 `.ssh` 目录中。`.ssh` 目录默认存储在你的主目录中；如有必要，`ssh-keygen` 会创建 `.ssh` 目录。

## 将公钥复制到远程计算机

你必须将公钥复制到你要与之安全通信的计算机上。以下步骤描述了如何复制和配置它们：

1.  登录到本地计算机上的用户账户。
    例如，以用户 `rod` 身份登录到 `cancun`。
2.  通过点击 GNOME 菜单按钮并选择 系统工具 > 终端 来打开一个 GNOME 终端窗口。
3.  将你的公钥复制到远程计算机上的你的账户中。例如，如果你在远程计算机 `cancun` 上的账户是 `rod`，你可以使用 Open Secure Copy (`scp`)：
    ```bash
    scp .ssh/id_dsa.pub rod@cancun:
    ```
    在本例中，你正在连接回你已登录的同一台计算机。这是测试你正在实验的 OpenSSH 服务器的最简单方法——不需要其他机器，甚至不需要网络。
4.  当被提示时，输入你的账户密码，DSA 公钥将被复制到 Cancun 上的你的主目录中。
5.  登录到远程机器。例如，使用 `ssh`：
    ```bash
    ssh cancun
    ```
6.  **当被提示时，输入你的密码。**
    OpenSSH 默认在 `.ssh` 目录（在你的主目录中）的 `authorized_keys` 文件中查找公钥。
7.  **使用这些命令将公钥复制到 `authorized_keys` 文件中（记住你仍然应该在你的主目录中）：**
    ```bash
    cat id_dsa.pub >> .ssh/authorized_keys
    ```
    `cat` 命令将 `id_dsa.pub` 的内容“连接”到 Linux 标准输出（通常就是你的控制台，在这种情况下是 GNOME 终端）。双大于号 (>>) 将标准输出追加到 `.ssh` 目录中的 `authorized_keys` 文件。现有的密钥不会受到干扰。

    `authorized_keys` 文件必须具有正确的权限。（有关文件权限的更多信息，请参见附录 B。）在这种情况下，宽松的权限会导致船只沉没（意指系统不安全/失败），OpenSSH 无法工作，例如具有组读/写/执行权限的情况。
8.  **确保权限正确：**
    ```bash
    chmod 644 .ssh/authorized_keys
    ```
9.  **确保 OpenSSH 服务器配置允许密钥交换。这些选项应在 `/etc/ssh/sshd_config` 文件中设置：**
    ```bash
    RSAAuthentication yes
    PubkeyAuthentication yes
    AuthorizedKeysFile    .ssh/authorized_keys
    ```
10. **如果你对 `sshd_config` 文件进行了任何更改，请重启 `sshd` 守护程序：**
    ```bash
    /etc/init.d/sshd restart
    ```

### 通过密钥交换连接到远程计算机

准备好使用密钥交换身份验证系统了吗？从主机（本地）计算机，尝试这些步骤：

1.  **登录到本地计算机上的用户账户。**
    例如，以用户 `rod` 身份登录到 `cancun`。
2.  **打开一个 GNOME 终端会话。**
3.  **登录到远程机器：**
    ```bash
    ssh cancun
    ```
4.  **输入你用于加密私钥的口令短语。**

