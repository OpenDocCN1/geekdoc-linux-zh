
`ssh` `server.com`

# SSH，安全外壳

`ssh` 尝试在 22 端口（IANA 分配的 SSH 标准端口）建立 TCP 连接。当连接建立时，服务器发送其公钥进行验证。如果主机未知且未信任，`ssh` 会提示：

`server.com` 的真实性无法确认。ECDSA 指纹为 SHA256:... 你确定要连接吗？(yes/no)

其目的是服务器管理员可以提前告知用户主机密钥。用户在首次连接时可以将收到的信息与指纹进行对比。如果两者匹配，主机身份得到证明。一旦用户接受密钥，指纹将被添加到 `~/.ssh/known_hosts` 以供以后使用，除非密钥更改，否则 `ssh` 不会提及主机身份已更改。

在实践中，这种服务器验证通常会被忽略。管理员很少向用户发送主机密钥，而用户盲目接受主机密钥。这种对新主机的盲目认可使其易受到中间人攻击。坦率地说，这个过程是可以自动化和精简的。

一旦主机被接受，服务器将列出它支持的认证方法。OpenSSH 实现了 SSH RFC 中描述的所有方法，包括 UNIX 密码认证、信任主机、公钥、用于集成 Kerberos 的 GSSAPI 以及支持 PAM 和一次性密码的灵活挑战/响应方案。这些方法中，公钥认证是最常用的，也是我们为大多数站点推荐的方法。它在强力和便利性之间取得了最佳平衡。我们从第 1019 页的“公钥认证”开始详细讨论 SSH 公钥的使用。

`ssh` 和 `sshd` 可以根据不同的需求和安全类型进行调整。配置位于 `/etc/ssh` 目录，这是在所有 UNIX 和 Linux 发行版中一个罕见的标准位置。表 27.1 列出了该目录下的文件。

## 表 27.1 `/etc/ssh` 目录下的文件

| 文件 | 权限 | 内容 |
|---|---|---|
| `ssh_config` | 0644 | 站点客户端配置 |
| `sshd_config` | 0644 | 服务器配置 |
| `moduli` | 0644 | DH 密钥交换的质数和生成器 |
| `*_key` | 0600 | 服务器支持的所有算法的私钥 |
| `*_key.pub` | 0644 | 与每个私钥对应的公钥 |

## 第 27 章 安全

除了 `/etc/ssh` 外，OpenSSH 还使用 `~/.ssh` 来存储公钥和私钥、用户客户端配置覆盖，以及其他一些用途。除非 `~/.ssh` 目录的权限设置为 0700，否则该目录会被忽略。

OpenSSH 在安全漏洞方面拥有一段值得信赖但并非完美的记录。根据 CVE 数据库 (`cve.mitre.org`)，早期版本中发现了几个关键漏洞。其中最后一个记录于 2006 年。偶尔会有拒绝服务攻击和绕过漏洞继续发布，但它们大多数被认为风险相对较低。尽管如此，作为定期补丁计划的一部分，更新 OpenSSH 软件包仍然是智智。

## `ssh` 客户端

开始使用 `ssh` 非常简单，但它的强大和多功能性在于它的许多选项。通过配置，你可以选择加密算法和密文、方便的主机别名、设置端口转发等。

基本语法为：

```bash
ssh [options] [username@host [command]]
```

例如，检查 `/var/log` 的磁盘空间：

```bash
$$ server.admin.com df -h /var/log
```

如果你指定了命令，`ssh` 会向主机进行身份验证，运行该命令并在不打开交互式 shell 的情况下退出。如果不指定用户名，`ssh` 将在远程主机上使用本地用户名。

`ssh` 从全范围文件 `/etc/ssh/ssh_config` 读取配置设置，并根据每个用户从 `~/.ssh/config` 处理额外的选项和覆盖。表 27.2 列出了你可以在这些文件中调优的一些较有趣的选项。我们将在本章中更详细地讨论其中一些选项。

当 `ssh` 组装最终配置时，命令行参数的优先级高于 `~/.ssh/config` 中的条目。在 `/etc/ssh/ssh_config` 中设置的全局配置是配置选项优先级最低的源。

如果没有指定其他值，`ssh` 将当前用户名作为登录名。你可以使用 `-l` 标志或以下语法提供不同的用户名：

```bash
$ ssh -l hsolo server.admin.com
$ ssh hsolo@server.admin.com
```

不能作为 `ssh` 直接参数可用的客户端选项仍然可以通过 `-o` 标志在命令行上设置。例如，你可以禁用对某个服务器的主机检查：

```bash
$ ssh -o StrictHostChecking=no server.admin.com
```

`-v` 选项打印调试信息。指定多次（最多三次）可以增加详细程度。你会发现在调试身份验证问题时，此标志是无价的。

## SSH，安全的 Shell

### 表 27.2 有用的 `ssh` 客户端配置选项

| 选项 | 含义 | 默认 |
| --- | --- | --- |
| AddKeysToAgent | 自动将密钥添加到 `ssh-agent` | no |
| ConnectTimeout | 连接超时时间（秒） | varies a |
| ControlMaster | 允许连接复用 | no |
| DynamicForward | 设置 SOCKS4 或 SOCKS5 代理 | |
| ForwardAgent | 启用 `ssh-agent` 转发 | no |
| Host | 新主机别名的标记 | |
| IdentityFile | 身份验证私钥的路径 | `~/.ssh/id_rsa` |
| Port | 要连接的端口 | |
| RequestTTY | 指定是否需要 TTY | auto |
| ServerAliveInterval | 向服务器连接发送心跳 | 0 (禁用) |
| StrictHostKeyChecking | 要求 (yes) 或忽略 (no) 密钥 | ask |

a. 默认值由内核的 TCP 默认决定，差异很大。
b. 前缀名取决于身份验证算法。默认情况下，所有密钥都以 id.. 开始。

为了方便起见，`ssh` 返回远程命令的退出状态。使用此行为在从脚本中调用 `ssh` 时检查错误状况。

查阅 `man ssh` 和 `man ssh_config` 以熟悉可用选项和功能。运行 `ssh -h` 可获取简要摘要。

## 公钥认证

OpenSSH（以及 SSH 协议）通常可以使用公钥加密来对远程系统进行身份验证。作为用户，从创建公钥/私钥对开始。将公钥交给服务器管理员，将其添加到服务器的 `~/.ssh/authorized_keys` 文件中。你可以通过使用远程用户名和私钥运行 `ssh` 来登录。

```bash
$ ssh -i ~/.ssh/id_ecdsa hsolo@server.admin.com
```

使用 `ssh-keygen` 生成密钥对。你可以指定使用的加密算法以及位长和其他特征。例如，生成 256 位的椭圆 ECDSA 密钥：

```bash
$ ssh-keygen -t ecdsa -b 256
```

正在生成 ecdsa 公钥/私钥对。

保存密钥的文件 (`/home/ben/.ssh/id_ecdsa`):

输入密码（留空无密码）：

再次输入密码：

标识已保存到 `/home/ben/.ssh/id_ecdsa`。

公钥已保存到 `/home/ben/.ssh/id_ecdsa.pub`。

指纹为：

SHA256:BIOyfcp/256

公钥 (`~/.ssh/id_ecdsa.pub`) 和私钥 (`~/.ssh/id_ecdsa`) 文件是 base64 编码的文件。`ssh-keygen` 正确设置了公钥和私钥的权限分别为 644 和 600。使用 2048 或 4096 位的 r 也可以。`ssh-keygen` 会提示加密私钥。如果你使用密码，在 `ssh` 读取之前必须输入。建议对特权账户（即具有 sudo 权限的账户）使用密码。如果你是服务器管理员并需要为新用户添加公钥，请以下步骤操作：

1. 确保用户具有活动的有效 shell。
2. 获取用户 `.ssh` 目录的副本。
3. 创建权限为 0700 的 `user/.ssh` 目录。
4. 将公钥添加到 `user/.ssh/authorized_keys` 并将其权限设置为 600。

例如，如果 `hsolo` 的公钥保存在 `/tmp/hsolo.pub`，过程将如下：

```bash
$ grep hsolo /etc/passwd
hsolo:x:1003:/home/hsolo:/bin/bash
$ mkdir -p hsolo/.ssh && chmod 700 hsolo/.ssh
$ cat /tmp/hsolo.pub >> hsolo/.ssh/authorized_keys
```
