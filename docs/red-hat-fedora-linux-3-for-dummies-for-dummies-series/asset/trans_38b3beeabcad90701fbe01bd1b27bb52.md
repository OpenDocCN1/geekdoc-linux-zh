
**sftp** 程序的工作方式类似于老牌 FTP，但当然会使用加密。请按照以下步骤使用 **sftp** 执行简单的文件传输：

- 1. 打开一个 GNOME 终端会话。
- 2. 输入以下命令：
  ```text
  sftp ssh.myisp.com
  ```
- 3. 输入你的用户名和密码。
- 4. 在 **sftp** 提示符下输入 help 命令。

你会看到一系列 **sftp** 命令。你使用最多的命令是 **cd**、**lcd**、**dir**、**ls**、**get** 和 **put**。这些命令的工作方式与它们的 Linux 对应命令类似。

使用 **sftp** 很直观。**get** 用于将文件、多个文件或目录从远程机器传输到本地机器；**put** 用于将内容从本地传输到远程。

![](img/41feae212f5c6612ff709354891f7b39_261_0.png)

OpenSSH 的另一个酷功能是它能够隧道传输任何协议。例如，你可以通过 X 协议将远程机器上的整个 X Window 显示出来。有关更多信息，请参阅 OpenSSH 文档。

## 配置 OpenSSH 服务器

配置 OpenSSH 服务器很简单。你只需要修改 /etc/ssh/sshd_config 文件并运行 **service sshd restart** 命令来重启 OpenSSH 服务器守护进程。查看该配置文件，其中重要的部分列在这里：

- **移除较旧且存在故障的协议版本 1**：版本 1 已损坏且不应使用（将参数 Protocol 2,1 更改为 Protocol 2，如下例所示）：
  ```text
  Port 22
  Protocol 2
  # Hostkeys for protocol version 2
  HostKey /etc/ssh/ssh_host_rsa_key
  HostKey /etc/ssh/ssh_host_dsa_key
  ```

- **移除登录宽限时间参数前面的注释**：此操作设置了一个限制，规定了从你开始登录到完成登录之间的时长：
  ```text
  LoginGraceTime 600
  ```

- 禁止 root 登录：你应该防止用户（包括你自己）直接以 root 身份登录。强制用户先以普通用户身份登录，然后再“su”到 root，可以提供审计轨迹，用于查看谁以 root 用户身份执行了什么操作；这也强制每个人在成为全能的 root 用户之前必须经历两个步骤：
  ```text
  PermitRootLogin no
  StrictModes yes
  ```

- 取消以下参数的注释以允许各种认证模式：
  ```text
  # rhosts authentication should not be used
  RhostsAuthentication no
  # Don't read the user's ~/.rhosts and ~/.shosts files
  IgnoreRhosts yes
  # For this to work you will also need host keys in /etc/ssh/ssh_known_hosts
  RhostsRSAAuthentication no
  # similar for protocol version 2
  HostbasedAuthentication no
  # Change to yes if you don't trust ~/.ssh/known_hosts for RhostsRSAAuthentication and HostbasedAuthentication
  IgnoreUserKnownHosts no
  ```

- 允许人们使用密码认证，但不允许未认证访问：
  ```text
  # To disable tunneled clear text passwords,
  # change to no here!
  PasswordAuthentication yes
  PermitEmptyPasswords no
  ```

要启动 OpenSSH 守护进程，请遵循这些步骤：

- 1. 进行更改并重启 Secure Shell 守护进程：
  ```text
  service sshd restart
  ```
- 2. 如果你正在运行防火墙，请将此规则添加到基于 iptables 的防火墙中：
  ```text
  iptables -A INPUT -p tcp -dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
  ```
- 3. 保存你的新防火墙配置：
  ```text
  iptables-save > /etc/sysconfig/iptables
  ```
- 4. 重启防火墙服务：
  ```text
  service iptables restart
  ```

现在你可以使用 OpenSSH 客户端和服务器在你的 Linux 计算机之间进行通信。使用 OpenSSH 客户端，你可以交互地登录到其他计算机，在计算机之间复制数据，并以此 piggyback（搭载）任意的通信流（例如 X Window）。你可以反过来与你的主机 Fedora Core 计算机通信。OpenSSH 加密你所有的通信，并防止你的密码和数据被窥视者获取。

## 交换密钥让你的生活更轻松

默认情况下，你使用 OpenSSH 通过传统密码登录到远程用户帐户。然而，OpenSSH 可以使用第二种认证方法，开始时需要一些工作，但长远来看可以节省大量时间。

OpenSSH 提供了一种名为公钥密码学的认证方法。该系统使用一个公钥和一个私钥。你在远程系统上安装公钥，并在你的计算机上保留私钥。公钥可以与任何人共享——嘿，它是公开的。私钥必须不惜一切代价保密。事实上，OpenSSH 默认会对私钥进行加密。在使用私钥之前，你必须使用一句密码短语（本质上是一个带空格的文件名）来解密它。

每当你想登录或与远程计算机通信时，密钥将用于协商该过程。公钥-私钥系统保证你的用户帐户已通过认证，并且是发起的主机；密码仅认证你的登录帐户，而不是你从中连接的计算机。

## 设置公钥密码学密钥交换

要设置密钥交换，请遵循这些步骤：

- 1. 登录到本地计算机上的用户帐户。
  - 例如，以 cancrun 上的用户 rod 身份登录。
- 2. 打开一个 GNOME 终端会话。
- 3. 运行此命令：
  ```text
  ssh-keygen -t dsa
  ```
  此步骤启动了生成公钥和私钥的程序。存在几种加密方法：DSA（数字签名标准）和 RSA（以 Ron Rivest、Adi Shamir 和 Len Adleman 的名字命名）是最流行的。DSA 是非专有的算法，而 RSA 直到最近才拥有专利。尽管 RSA 可用于公共用途，但我们建议使用 DSA。

程序思考片刻后返回以下输出：

```text
Enter file in which to save the key (/home/rod/.ssh/id_dsa)
```

密钥保存到你的主目录中的 `.ssh` 目录。默认值应该没问题，所以按 Enter 键。

- 4. `ssh-keygen` 程序要求你输入一个**密码短语**，它用于加密你的私钥：
  ```text
  Enter passphrase (empty for no passphrase):
  ```
- 5. 输入你的密码短语，`ssh-keygen` 将生成密钥。
  - 使用包含数字和其他字符的短语。例如，你可以尝试像这样的密码短语（不，不是这个确切的，但你知道的）：
    ```text
    Giv3_m3@brek!
    ```
- 6. **通过第二次输入该短语进行验证。**

`ssh-keygen` 程序生成你的公钥和私钥。这些密钥默认存储在 `.ssh` 目录中。`.ssh` 目录默认存储在你的主目录中；如有必要，`ssh-keygen` 会创建 `.ssh` 目录。

## 将公钥复制到远程计算机

你必须将公钥复制到你安全通信的计算机上。这些步骤描述了如何复制和配置它们：

- 1. **登录到本地计算机上的用户帐户。**
  - 例如，以 cancun 上的用户 `rod` 身份登录。
- 2. **点击 GNOME 菜单按钮并选择 System Tools > Terminal 来打开 GNOME 终端窗口。**
- 3. **将公钥复制到远程计算机上的你的帐户。** 例如，如果远程计算机 `cancun` 上的你的帐户是 `rod`，你可以使用 Secure Copy（`scp`）：
  ```text
  scp .ssh/id_dsa.pub rod@cancun:
  ```
  - 在此示例中，你连接的是你已经登录的同一台计算机。这是测试你正在实验的 OpenSSH 服务器最简单的方法。不需要其他机器，甚至不需要网络。
- 4. **在提示时输入你的帐户密码，DSA 公钥将被复制到 Cancun 上的你的主目录。**
- 5. **登录到远程机器。** 例如，使用 `ssh`：
  ```text
  ssh cancun
  ```
- 6. **在提示时输入你的密码。**

OpenSSH 默认在 `.ssh` 目录（在你的主目录中）的 `authorized_keys` 文件中查找公钥。

- 7. 使用这些命令将公钥复制到 `authorized_keys` 文件（记住你应该仍在你的主目录中）：
  ```text
  cat id_dsa.pub > .ssh/authorized_keys
  ```
  - `cat` 命令将 `id_dsa.pub` 的内容“连接”到 Linux 标准输出（通常是你的控制台，在这种情况下是 GNOME 终端）。双大于号 (>) 将标准输出附加到 `.ssh` 目录中的 `authorized_keys` 文件。预先存在的密钥不会受到干扰。
  - `authorized_keys` 文件必须具有正确的权限。（有关文件权限的更多信息，请参阅附录 C。）在这种情况下，宽松的权限会导致船只沉没，OpenSSH 无法与例如 `读/写/执行` 组权限配合工作。
- 8. 确保正确的权限：
  ```text
  chmod 644 .ssh/authorized_keys
  ```
- 9. 确保 OpenSSH 服务器配置允许密钥交换。这些选项应在 `/etc/ssh/sshd_config` 文件中设置：
  ```text
  RSAAuthentication yes
  PubkeyAuthentication yes
  AuthorizedKeysFile .ssh/authorized_keys
  ```
- 10. 如果你对 `sshd_config` 文件进行了任何更改，请重启 `sshd` 守护进程：
  ```text
  service sshd restart
  ```

## 通过使用密钥交换连接远程计算机

准备好使用密钥交换认证系统了吗？从主机（本地）计算机，尝试这些步骤：

- 1. 登录到本地计算机上的用户帐户。
  - 例如，以 cancun 上的用户 `rod` 身份登录。
- 2. 打开一个 GNOME 终端会话。
- 3. 登录到远程机器：
  - `ssh cancun`
- 4. 输入你用于加密私钥的密码短语。

```text
ssh cancun
```

远程计算机认证了你和你的主机计算机。瞧！你进去了。

