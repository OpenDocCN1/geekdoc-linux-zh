
公钥 (`p22`) | 指纹 (`p23`) | SCP (`p23`) | 隧道 (`p24`)

### 5.1 公钥认证

使用公钥认证无需密码连接到主机。其思想是将你的公钥追加到远程主机的 `authorized_keys2` 文件中。对于此示例，让我们将 `host-client` 连接到 `host-server`，密钥在客户端生成。使用 `cygwin` 时，你可能需要创建主目录和 `.ssh` 目录，执行 `# mkdir -p /home/USER/.ssh`

- 使用 `ssh-keygen` 生成密钥对。`~/.ssh/id_dsa` 是私钥，`~/.ssh/id_dsa.pub` 是公钥。
- 将公钥复制到服务器并追加到服务器上你主目录中的文件 `~/.ssh/authorized_keys2`。

```
# ssh-keygen -t dsa -N ''
# cat ~/.ssh/id_dsa.pub | ssh you@host-server "cat - >> ~/.ssh/authorized_keys2"
```

#### 使用来自 ssh.com 的 Windows 客户端

非商业版的 `ssh.com` 客户端可以从主 `ftp` 站点下载：`ftp.ssh.com/pub/ssh/`。`ssh.com` 客户端生成的密钥需要转换为 OpenSSH 服务器可用的格式。这可以使用 `ssh-keygen` 命令完成。

`9.http://www.g-loaded.eu/2006/11/06/netcat-a-couple-of-useful-examples`

`10.http://www.terminally-incoherent.com/blog/2007/08/07/few-useful-netcat-tricks`

- 使用 `ssh.com` 客户端创建密钥对：设置 - 用户身份验证 - 生成新...
- 我使用密钥类型 `DSA`；密钥长度 `2048`。
- 将 `ssh.com` 客户端生成的公钥复制到服务器的 `~/.ssh` 文件夹中。
- 密钥位于 `C:\Documents and Settings\%USERNAME%\Application Data\SSH\UserKeys`。
- 在服务器上使用 `ssh-keygen` 命令转换密钥：

```
# cd ~/.ssh
# ssh-keygen -i -f keyfilename.pub >> authorized_keys2
```

注意：我们使用的是 `DSA` 密钥，`RSA` 也是可能的。密钥未受密码保护。

#### 使用 putty for Windows

`Putty` 是 Windows 的一个简单免费 `ssh` 客户端。

- 使用 `puTTYgen` 程序创建密钥对。
- 保存公钥和私钥（例如保存到 `C:\Documents and Settings\%USERNAME%\.ssh`）。
- 将公钥复制到服务器的 `~/.ssh` 文件夹中：

```
# scp .ssh/puttykey.pub root@192.168.51.254:~/.ssh/
```

- 在服务器上使用 `ssh-keygen` 命令将密钥转换为 OpenSSH 用：
- 在 `putty` 设置中指定私钥位置：连接 - SSH - 身份验证

```
# cd ~/.ssh
# ssh-keygen -i -f puttykey.pub >> authorized_keys2
```

### 5.2 检查指纹

首次登录时，`ssh` 会询问是否将未知主机及其指纹存储在 `known hosts` 中。为了避免中间人攻击，服务器管理员可以向你发送服务器指纹，然后在首次登录时进行比较。使用 `ssh-keygen -l` 获取指纹（在服务器上）：

```
# ssh-keygen -l -f /etc/ssh/ssh_host_rsa_key.pub    # For RSA key
2048 61:33:be:9b:ae:6c:36:31:fd:83:98:b7:99:2d:9f:cd  /etc/ssh/ssh_host_rsa_key.pub
# ssh-keygen -l -f /etc/ssh/ssh_host_dsa_key.pub    # For DSA key (default)
2048 14:4a:aa:d9:73:25:46:6d:0a:48:35:c7:f4:16:d4:ee  /etc/ssh/ssh_host_dsa_key.pub
```

现在连接到此服务器的客户端可以验证自己是否连接到正确的服务器：

```
# ssh linda
The authenticity of host 'linda (192.168.16.54)' can't be established.
DSA key fingerprint is 14:4a:aa:d9:73:25:46:6d:0a:48:35:c7:f4:16:d4:ee.
Are you sure you want to continue connecting (yes/no)? yes
```

### 5.3 安全文件传输

一些简单命令：

```
# scp file.txt host-two:/tmp
# scp joe@host-two:/www/*.html /www/tmp
# scp -r joe@host-two:/www /www/tmp
```

在 `Konqueror` 或 `Midnight Commander` 中，可以使用地址 `fish://user@gate` 访问远程文件系统。但是实现非常慢。

此外，还可以使用基于 `SCP` 的文件系统客户端 `sshfs` 挂载远程文件夹。参见 `fuse sshfs`。

```
ssh_exchange_identification: Connection closed by remote host
```

出现此错误时，请在服务器上尝试以下操作：

```
echo 'SSHD: ALL' >> /etc/hosts.allow
/etc/init.d/sshd restart
```

### 5.4 隧道

`SSH` 隧道允许通过 `SSH` 连接转发或反向转发端口，从而保护流量并访问原本会被阻止的端口。这仅适用于 `TCP`。转发和反向的通用命名法为（另见 `ssh` 和 `NAT` 示例）：

```
# ssh -L localport:desthost:destport user@gate  # desthost as seen from the gate
# ssh -R destport:desthost:localport user@gate  # forwards your localport to destination
#   desthost:localport as seen from the client initiating the tunnel
# ssh -X user@gate   # To force X forwarding
```

这将连接到 `gate` 并将本地端口转发到主机 `desthost:destport`。请注意 `desthost` 是 `gate` 所见的目的主机，因此如果连接至 `gate`，则 `desthost` 为 `localhost`。可以同时转发多个端口。

#### 在 gate 上直接转发

假设我们想要访问在 `gate` 上运行的 `CVS`（端口 `2401`）和 `http`（端口 `80`）。这是最简单的示例，`desthost` 因此为 `localhost`，我们在本地使用端口 `8080` 而不是 `80`，这样就不需要 `root` 权限。一旦 `ssh` 会话打开，两个服务都可以通过本地端口访问。

```
# ssh -L 2401:localhost:2401 -L 8080:localhost:80 user@gate
```

#### Netbios 和远程桌面转发到第二台服务器

假设一台 Windows `smb` 服务器位于 `gate` 后面且未运行 `ssh`。我们需要访问 `smb` 共享以及对服务器的远程桌面。

```
# ssh -L 139:smbserver:139 -L 3388:smbserver:3389 user@gate
```

现在可以通过 `\\127.0.0.1\` 访问 `smb` 共享，但前提是本地共享被禁用，因为本地共享正在监听端口 `139`。

可以保留本地共享启用，为此我们需要创建一个具有新 IP 地址的新虚拟设备，通过该地址连接 `smb` 共享。此外，本地 `RDP` 已在 `3389` 上监听，因此我们选择 `3388`。对于此示例，让我们使用虚拟 IP `10.1.1.1`。

- 使用 `putty` 设置源端口=`10.1.1.1:139`。可以创建多个环回设备并进行隧道。在 Windows 2000 上，只有 `putty` 对我有效。在 Windows Vista 上，还需额外转发端口 `445` 除了端口 `139`。此外在 Vista 上，补丁 `KB942624` 会阻止端口 `445` 的转发，因此我不得不卸载 Vista 上的此补丁。
- 使用 `ssh.com` 客户端，禁用“仅允许本地连接”。由于 `ssh.com` 将绑定到所有地址，因此只能连接单个共享。

现在创建具有 IP `10.1.1.1` 的环回接口：
