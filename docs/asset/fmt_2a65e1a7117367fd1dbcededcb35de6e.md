
- 当向 CA 请求密钥对时，它会使用指定的加密方案（如 `RSA` 或 `DSA`）同时生成公钥和私钥。
- 私钥仅交给密钥所有者。
- 公钥可以提供给任何需要它的人。
- CA 的主要角色是验证参与加密交换的各方确实是其所声称的身份。
- 早期的 Linux 网络服务，如 `Telnet`、`rlogin`、`rcp`、`rshell` 和 `FTP`，以明文传输数据，这使得用户名、密码和其他敏感数据容易受到嗅探器的攻击。
- `OpenSSH` 提供了一套你可以用来加密这些数据传输的实用程序：
  - `sshd`
  - `ssh`
  - `scp`
  - `sftp`
  - `slogin`
- `OpenSSH` 同时使用私钥/公钥加密和秘密密钥加密。
- `SSH` 客户端首先与运行 `SSH` 服务器的系统建立连接，端口为 `IP` 端口 `22`。
  - 然后 `SSH` 服务器将其公钥发送给 `SSH` 客户端。
  - 客户端系统从 `SSH` 服务器接收公钥，并检查其是否已拥有该密钥的副本。
  - 如果这些文件中没有服务器的公钥，它会提示用户添加它。
  - 客户端生成一个 `256` 位秘密密钥，使用服务器的公钥对其进行加密，并将其发送给服务器。
  - 服务器使用私钥对其进行解密。
  - 现在两个系统都可以使用对称加密进行会话。
- 你可以在本地计算机上加载 `ssh` 客户端，通过在 shell 提示符下输入 `ssh -l user_name ip_address` 连接到远程 Linux 系统上的 `sshd` 守护进程。
- 你可以通过 `SSH` 隧道安全地隧道传输未加密的网络流量。
  - 当被隧道协议的客户端软件与本地 `SSH` 客户端建立连接时，流量使用 `SSH` 加密并通过隧道传输到 `SSH` 服务器。
  - 在 `SSH` 服务器端，流量被解密，然后转发到适当的目标服务。
- 要配置 `SSH` 隧道，你必须：
  - 编辑运行 `sshd` 的系统上的 `/etc/ssh/sshd_config` 文件，并将 `AllowTcpForwarding` 参数设置为 `yes`。
  - 从本地高 `IP` 端口创建本地 `ssh` 隧道，到远程服务器上目标服务正在监听的端口。
- 你可以在隧道客户端使用 `telnet` 命令来测试隧道。
- 你还可以通过建立 `SSH` 连接将你的 X 服务器流量隧道传输到远程 X 客户端，操作如下：
  - 配置客户端系统以接受来自 X 服务器的连接。
  - 使用 `DISPLAY` 环境变量配置 X 服务器，将其图形显示重定向到客户端系统。
  - 导出该变量的新值。
  - 在 X 服务器系统上的 `/etc/ssh/sshd_config` 文件中将 `X11Forwarding` 选项设置为 `yes`。
  - 在客户端系统的 shell 提示符处，使用 `ssh` 命令的 `-X` 选项登录到远程系统。
  - 输入适当的命令以启动图形应用程序。
- 你可以配置 `SSH` 使用公钥认证，而不是用户名和密码。
  - 为此，客户端系统上用户的公钥必须存储在服务器系统中你要认证的用户主目录下的 `~/.ssh/authorized_keys` 文件中。
  - 要配置公钥认证，你必须执行以下操作：
    - 使用 `ssh-keygen` 命令在客户端系统上创建公钥/私钥对。
    - 使用 `scp` 命令将刚才创建的公钥复制到 `SSH` 服务器。
    - 将刚才复制的密钥文件的内容追加到你要连接到的 `SSH` 服务器上用户主目录下的 `~/.ssh/authorized_keys` 文件末尾。
- 如有需要，你可以使用 `ssh-agent` 命令来消除每次建立 `SSH` 连接时输入密码短语的必要性。
- 为了通过你的 `Linux+`/`LPIC-1` 考试，你需要知道如何使用开源 `GPG` Privacy Guard (`GPG`) 实用工具来加密文件。
  - `GPG` 同时使用非对称加密和对称加密。
    - `GPG` 首先生成一个随机对称密钥，并使用它来加密要传输的消息。
    - 然后，该对称密钥本身使用接收方的公钥进行加密，并与使用对称密钥加密的消息一起发送。
    - 当接收方收到消息时，`GPG` 首先使用用户的私钥解密对称密钥。
    - 然后，`GPG` 使用解密后的对称密钥解密消息的其余部分。
- 要使用 `GPG` 加密文件，请执行以下操作：
  - 使用 `gpg --gen-key` 命令生成你的密钥。
  - 使用 `gpg -e -r key_user_name filename` 命令加密文件。
- 一旦文件被加密，就可以使用 `gpg --output output_filename --decrypt encrypted_filename` 命令对其进行解密。
- 如果你想将加密的文件发送给他人，你可以导出你的公钥并将其发送给他们：
  - 输入 `gpg --export key_user_name > public_key_filename`。
  - 将此密钥文件发送给你希望能够打开你的加密文件的用户。
  - 他们可以使用 `gpg --import public_key_filename` 命令将你的公钥导入他们的 `GPG` 密钥环。
- 你可以使用 `gpg --list-keys` 命令查看你 `GPG` 密钥环中的文件。
- 导入公钥后，你可以使用 `gpg --output output_filename --symmetric encrypted_filename` 命令解密发送给你的文件。

#### 问题

1. 关于对称加密，下列哪项陈述是正确的？（选择两项。）

   A. 它使用私钥/公钥对。

   B. 发送方和接收方都必须拥有相同密钥的副本。

   C. `RSA` 是对称加密的一种形式。

   D. `Blowfish` 是对称加密的一种形式。

   E. 私钥被发送给接收方，用于解密使用公钥加密的信息。

2. 关于非对称加密，下列哪项陈述是正确的？（选择两项。）

   A. 私钥被发送给接收方。

   B. 公钥被发送给接收方。

   C. 使用公钥加密的信息只能用私钥解密。

   D. 使用公钥加密的信息可以用公钥解密。

   E. 使用私钥加密的信息可以用私钥解密。

3. 哪些主机密钥文件存储了 `SSH` 版本 `2` 服务器使用的私钥？（选择两项。）

   A. `/etc/ssh/ssh_host_key`

   B. `/etc/ssh/ssh_host_key.pub`

   C. `/etc/ssh/ssh_known_hosts`

   D. `/etc/ssh/ssh_host_rsa_key`

   E. `/etc/ssh/ssh_host_dsa_key`

4. `/etc/ssh/sshd_config` 文件中的哪个参数指定 `sshd` 守护进程应使用的 `SSH` 版本？

   A. `HostKey`

   B. `Protocol`

   C. `SSHVersion`

   D. `ListenAddress`

5. `/etc/ssh/ssh_config` 文件中的哪个参数配置 `ssh` 客户端仅与那些公钥已添加到 `~/.ssh/known_hosts` 或 `/etc/ssh/ssh_known_hosts` 文件中的 `SSH` 服务器建立连接？

   A. `StrictHostKeyChecking`

   B. `HostKey`

   C. `Protocol`

   D. `User`

6. `sshd` 守护进程默认监听哪个端口以接收传入的 `SSH` 连接？

   A. `20`

   B. `22`

   C. `389`

   D. `631`

   E. `80`

   F. `443`

7. 下列哪个 shell 命令将加载 `ssh` 客户端并以 `ksanders` 用户身份连接到 `IP` 地址为 `10.0.0.254` 的 `SSH` 服务器？

   A. `sshd -l ksanders 10.0.0.254`

   B. `ssh -- ksanders 10.0.0.254`

   C. `ssh -l ksanders 10.0.0.254`

   D. `ssh user=ksanders 10.0.0.254`

8. 你想在运行 `sshd` 守护进程的 `POP3` 邮件服务器和运行 `Mozilla Thunderbird` 邮件客户端的本地 `ssh` 客户端系统之间配置 `SSH` 隧道。`/etc/ssh/sshd_config` 文件中的哪个参数必须设置为 `yes` 才能启用该隧道？

   A. `AllowTcpForwarding`

   B. `AllowTcpTunneling`

   C. `AllowSSHTunnel`

   D. `AllowPop3Tunnel`

   E. `AllowPop3ImapForwarding`

9. 你想为 X 服务器流量建立安全的 `SSH` 隧道。X 客户端系统上的 `/etc/ssh/ssh_config` 文件和 X 服务器系统上的 `/etc/ssh/sshd_config` 文件中的哪个参数可用于启用此功能？

   A. `AllowTcpForwarding`
