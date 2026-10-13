
这是一种简单且实用的 OpenSSH 方法，但你可以做得更多。Red Hat SSH 客户端会自动配置为通过你的安全连接转发 X。在登录你的 ISP 期间，你可以运行 X Window 客户端软件并在本地机器上查看它：

1. 按照前面的说明登录你的 ISP（或任何运行 Secure Shell 服务器的机器）。
2. 运行一个 X Window 应用程序，例如 `xclock`。

简单的 `xclock` 窗口将显示在你的桌面上。OpenSSH 还允许在机器之间传输文件。提供了两个程序：`scp`（安全复制）和 `sftp`（安全文件传输）。这两个程序都使用 SSH 协议，因此所有数据在传输过程中都是加密的。`scp` 和 `sftp` 的主要区别在于 `scp` 是非交互式的，而 `sftp` 是交互式的。

使用 `scp` 的语法为：

```scp [options] user@host:source destination
```

例如，从远程机器拷贝文件到本地机器：

```
scp user@host:/path/to/file /local/path/
```

要从本地机器拷贝文件到远程机器，顺序反过来。使用冒号分隔主机和路径：

```
scp /local/to/file user@host:/path/to
```

要拷贝目录，使用 `-r` 选项：

```
scp -r /local/to/directory user@host:/path/to
```

使用 `sftp` 的语法为：

```
sftp user@host
```

连接后，你会看到 `sftp` 提示符。你可以使用以下命令：

- `cd`：切换远程目录。
- `lcd`：切换本地目录。
- `ls`：列出远程文件。
- `lls`：列出本地文件。
- `get`：从远程下载文件到本地。
- `put`：从本地上传文件到远程。
- `quit`：退出 `sftp` 会话。

要使用 `sftp` 传输目录，使用 `-r` 选项：

```
sftp -r user@host
```

SSH 的另一个酷功能是它能够隧道任何协议。这允许你在远程机器上运行图形化应用程序，就像它们运行在本地机器上一样。这种方法被称为 X11 转发。

连接 SSH 时使用 `-X` 选项：

```
ssh -X user@host
```

连接后，你可以运行任何 X 客户端程序，例如：

```
xclock
```

## 配置 OpenSSH 服务器

配置 OpenSSH 服务器非常直观。你只需要修改 `/etc/ssh/sshd_config` 文件并运行 `/etc/init.d/sshd` 脚本。让我们来看配置文件，其重要部分列如下：

- 移除旧且有错误的协议版本 1：版本 1 是损坏的，不应使用（如示例所示，将参数 `Protocol 2,1` 改为 `Protocol 2`）：

`Port 22`

`Protocol 2`

## HostKeys for protocol version 2

`HostKey /etc/ssh/ssh_host_rsa_key`

`HostKey /etc/ssh/ssh_host_dsa_key`

- 移除登录宽时间参数前的注释：此操作设置了从你开始登录到完成登录之间的时间限制：

`LoginGraceTime 600`

- 禁止 root 登录：你不应该允许用户（包括你自己）直接以 root 登录。强制用户先作为普通用户登录然后“切换”到 root，这提供了一个审计追踪，用于查看作为 root 用户执行了什么；它还强迫每个人在成为全能的 root 用户之前跳过两个关卡：

`PermitRootLogin no`

`StrictModes yes`

## 第 17 章：保障您的未来

- 取消这些注释以允许各种身份验证模式：

  - # 不应使用 rhosts 验证

    `RhostsAuthentication no`

  # 不要读取用户的 ~/.rhosts 和 ~/.shosts 文件

    `IgnoreRosts yes`

  # 对于此，你还需要在

    `/etc/ssh/ssh_known_hosts` 中包含主机密钥

    `RSAAuthentication no`

  # 协议版本 2 类似类似

    `HostBasedAuthentication no`

  # 如果你不信任 RSAAuthentication 和 HostBasedAuthentication 的 ~/.ssh/known_hosts

    将其改为 yes

    `IgnoreUserKnownHosts no`

- 允许用户使用密码验证，但不允许未经授权的访问：

  - 若要禁用隧道传输明文密码，请在此处将其改为 no！

    `PasswordAuthentication yes`

    `PermitEmptyPasswords no`

启动 OpenSSH 守护进程，请遵循以下步骤：

1. 更改并重启 Secure Shell 守护进程：

   `/etc/init.d/sshd restart`

2. 如果你正在运行防火墙，请向基于 iptables 的防火墙添加此规则：

   `iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT`

3. 保存新的防火墙配置：

   `iptables-save > /etc/sys/iptables`

4. 重启防火墙：

   `/etc/init.d/iptables restart`

你可以使用 OpenSSH 客户端和服务器与你的 Linux 计算机进行通信。使用 OpenSSH 客户端，你可以交互式地登录其他计算机，在计算机之间复制数据，并利用这个小工具挂载任意通信流——例如 X Window。你可以反转该过程与你的主机 Red Hat Linux 计算机通信。OpenSSH 会加密你所有的通信，防止你的密码和数据暴露给窥探的目光。

## 密钥交换让你的生活更轻松

你默认使用 OpenSSH 通过传统密码登录远程用户账户。然而，OpenSSH 可以使用第二种身份验证方法，虽然启动需要一些精力，但长远来看可以节省工作。

OpenSSH 提供了一种名为公钥加密的身份验证方法。该系统使用一个公和一个私钥。你将公钥安装在远程系统中，并将私钥保存在你的计算机上。公钥可以与任何人共享——嘿，它是公开的。私钥必须不惜保密。事实上，OpenSSH 默认会对私钥进行加密。你必须使用一个短语（本质上是带有空格的密码）在使用之前解密私钥。

当你想要登录或与远程计算机通信时，密钥将用于协商该过程。公私钥系统保证了你的用户账户经过了验证，并且是发起主机；密码仅验证你的登录账户，而不验证你所连接的计算机。

## 设置公钥加密密钥交换

要设置密钥交换，请遵循以下步骤：

1. 登录本地计算机上的用户账户。

   例如，在 `cancun` 上以用户 `rod` 的身份登录。
2. 打开一个 GNOME Terminal 会话。
3. 运行此命令：

```
ssh-keygen -t dsa
```

> 此步骤启动了生成你的公钥和私钥的程序。存在多种加密方法：DSA（数字签名标准）和 RSA（以 Ron Rivest、Adi Shamir 和 Len Adleman 命名）最流行。DSA 是一种非专利算法，而 RSA 直到最近才获得专利。尽管 RSA 可以公开使用，但我们建议使用 DSA。

程序思考了一会儿并返回此输出：

Enter file in which to save the key

(/home/rod/.ssh/id_dsa):

![](img/453364505e32ffec24f7d88ac7824962_271_0.png)

## 第 17 章：保障您的未来

密钥被保存到家目录下的 `.ssh` 目录中。默认设置应该是可以，所以按回车键。

4. `ssh-keygen` 程序要求你输入一个短语，它用于加密你的私钥：

Enter passphrase (empty for no passphrase):

5. 输入包含数字和其他字符的短语。例如，你可以尝试这样的短语：

Givv3 m3 @bre@k!

6. 再次输入以验证你的短语。

`ssh-keygen` 程序生成你的公钥和私钥。它们存储在 `.ssh` 目录中。

## 将你的公钥复制到远程

要将公钥复制到远程计算机，请遵循以下步骤：

1. 登录本地计算机上的用户账户。

   例如，在 `cancun` 上以用户 `rod` 的身份登录。
2. 打开一个 GNOME Terminal 会话。
3. 使用命令将你的公钥复制到远程服务器：

```
ssh-copy-id rod@cancun
```

`ssh-copy-id` 命令简化了通过网络在远程主机上安装你公钥的过程。如果你没有安装 `ssh-copy-id`，可以使用以下方法：

1. 在本地机器上显示你的公钥：

```bash
cat ~/.ssh/id_dsa.pub
```

2. 输出并粘贴到远程机器上的 `authorized_keys` 文件中：
