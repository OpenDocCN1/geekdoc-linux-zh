
## 第 12 章：保护您的服务器

### 用户身份验证

当你使用 `ssh-keygen2`（在本章稍后部分讨论）创建用户密钥时，系统会提示你输入短语（pass phrase）。该短语长度可达 20 个字符并并包含空格。在验证过程中，系统会提示你输入短语。正确输入后，你将登录到远程系统。如果主机验证失败或你输入了错误的短语，Secure Shell 将回退到普通登录过程，你需要输入常规登录账户密码（你可以关闭普通登录过程以仅允许短语验证。更多信息请参阅“配置常规参数”章节）。

关于此主题的更多信息，请参见“加密方法”章节列出的 URL。

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_406_0.png)

> 第二个 URL 的文章讨论了第一版本 Secure Shell 的操作。请记住，本书使用的 Secure Shell 2 配置的是文章中讨论的版本的密钥，但整体概念是相同的。

### 下载 SECURE SHELL

Linux/UNIX 版本的 Secure Shell 可通过互联网获取（http://www.ssh.fi/sshprotocols2），但仅供非用户用户。如果用于商业目的，必须购买 Secure Shell。请阅读许可协议以确定你是否可以合法使用公开可用版本。SSH Communication Security 的主页 http://www.ssh.fi 包含更多产品。

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_406_1.png)

位于 http://www.datafellows.com 的 Data Fellows Ltd. 是 Secure Shell 授权授权商。除了 Secure Shell 商业版，他们还提供免费的商业试用版。

要下载 `ssh2` 的 RPM 版本，请按照以下步骤操作：

- 1. 以 root 身份登录 `atlas`。
- 2. 进入 `/usr/local/src` 目录。
  ```
  cd /usr/local/src
  ```
- 3. 连接到 http://rufus.w3.org/linux/RPM/replay/crypto/linux/redhat/1386。
- 4. 下载 `ssh2`、`ssh2-client`、`ssh2-server` 和 `ssh2-extras` 的 RPM 包。

### 安装并配置 SECURE SHELL

Secure Shell 要求连接的机器——服务器——运行 `ssh2` 守护进程。一旦你配置了客户端和服务器，就可以从任何其他机器——客户端——使用 `ssh2` 客户端程序连接该机器。以下章节描述了如何配置双方。

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_407_0.png)

你的 Secure Shell 服务器和客户端可以放在同一台机器上。只需将以下安装和配置客户端的指令应用到你的服务器上即可。如果你没有多台 Linux 计算机可以使用，这是一个测试 Secure Shell 的好方法。

#### 在服务器计算机上安装 SECURE SHELL

在本示例中，Linux 互联网网关和防火墙 `atlas` 将充当 Secure Shell 服务器。网络上的任何 Linux 计算机都可以提供此功能。然而，通过将其放置在网关上，你可以从互联网访问私有网络。（Secure Shell 服务器的数量没有限制。如果你想让内部网络更安全，那么你进行交互式通信的每台 Linux 计算机都应该是 Secure Shell。）

- 1. 以 root 身份登录 `atlas`。
- 2. 安装 Secure Shell 包。
  ```
  -ivh /usr/local/src/ssh2*
  ```
- 此命令安装了 `ssh2`、`ssh2-clients`、`ssh2-extras` 和 `ssh2-server` RPM 包。当安装 ssh RPM（基础包）时，它会生成公钥（`hostkey.pub`）和私钥（`hostkey`），所示：

```
Generating 1024 bit host key. This may take a while, and go and have a coffee )
Generating 1024-bit dsa key pair
1 00.000.0000
```

过程取决于计算机的速度，需要几分钟。生成的密钥存储在 `/etc/ssh` 目录中。
- 4. 当安装 `ssh2-server` RPM 时，它会启动 `ssh2` 守护进程（同时在 `/etc/rc/init.d` 目录中安装启动脚本 `ssh2`）。

此时，你的 shell 已经准备好接受连接。然而，你仍然需要配置客户端。

#### 在客户端计算机上安装 SECURE SHELL

在本示例中，Linux 互联网网关和防火墙 `atlas` 将充当 Secure Shell 服务器。网络上的任何 Linux 计算机都可以提供此功能。然而，通过将其放置在网关上，你可以从互联网访问私有网络。（Secure Shell 服务器的数量没有限制。如果你想让内部网络更安全，那么你进行交互式通信的每台 Linux 计算机都应该是 Secure Shell。）

- 1. 以 root 身份登录 `atlas`。
- 2. 安装 Secure Shell 包。
  ```
  -ivh /usr/local/src/ssh2*
  ```
- 此命令安装了 `ssh2`、`ssh2-clients`、`ssh2-extras` 和 `ssh2-server` RPM 包。当安装 ssh RPM（基础包）时，它会生成公钥（`hostkey.pub`）和私钥（`hostkey`），所示：

```
Generating 1024 bit host key. This may take a while, and go and have a coffee )
Generating 1024-bit dsa key pair
1 00.000.0000
```

过程取决于计算机的速度，需要几分钟。生成的密钥存储在 `/etc/ssh` 目录中。
- 4. 当安装 `ssh2-server` RPM 时，它会启动 `ssh2` 守护进程（同时在 `/etc/rc/init.d` 目录中安装启动脚本 `ssh2`）。

### 配置服务器

现在你已经创建了个人私钥，你需要将公钥复制到要访问的服务器。

- 1. 以普通用户身份登录 `atlas`——在本例中为 `frankcastle`（必要时使用 `useradd` 创建用户）。
- 2. 从用户目录 `/home/frankcastle` 创建 `.ssh` 目录。
  ```
  mkdir .ssh2
  ```
- 3. 进入 `.ssh` 目录 `cd ~/.ssh2` 并从客户端拷贝用户的公钥——`id_rsa_1024.pub`。使用你任何想要的方法——FTP 或 `sftp`——进行传输，但请注意，任何在你在安装密钥之前拦截密钥的人理论上能够进行中间人攻击。对于大多数人来说，这可能是一个远程的可能性，但请注意，使用软盘或其他媒介在机器之间携带公钥被认为是一种做法，以避免在可能有漏洞的网络上传输密钥。
- 4. 将 `id_rsa_1024.pub` 文件复制到服务器后，对其进行重命名 `/usr/doc/ssh2/*SSH-QUICKSTART` 文档使用的命名习惯是将其命名为 `Local.pub`。然而，我个人觉得按照使用连接的用户来命名密钥更简单。
  ```
  mv id_rsa_1024.pub key_of_frankcastle
  ```
- 5. 在服务器的 `.ssh2` 目录中按如下创建验证文件。
  ```
  echo "key_of_frankcastle.pub" > authorization
  ```
Secure Shell 守护进程将在服务器 `.ssh2` 目录下的用户验证文件中查找包含用户公钥的文件。

### 配置文件检查

`ssh2` 目录。新名称包含了 `sshd` 端口号—22 以及服务器名称—`atlas`。

检查客户端和服务器的配置文件。用户 `frankcastle` 在客户端和服务器上应该拥有以下配置和密钥文件。注意，这里没有讨论 `random_seed`，因为它是由 Secure Shell 程序使用的，用户并不直接对其配置或使用，且它未包含在表 12-1 中。

#### 表 12-1 安全外壳 (SSH) 2 用户文件

| 计算机 | 目录 | 文件 | 目的 |
| --- | --- | --- | --- |
| chivas | /home/frankcastle/.ssh2/ | id_dsa_1024_a | 客户端私钥 |
| chivas | /home/frankcastle/.ssh2/ | id_dsa_1024_a.pub | 客户端公钥 |
| chivas | /home/frankcastle/.ssh2/ | Identification | 公钥文件名 |
| chivas | /home/frankcastle/.ssh2/hostkeys | key_22_atlas.pub | 服务器公钥 |
| atlas | /home/frankcastle/.ssh2/ | key_from_chivas.pub | 公钥 |
| atlas | /home/frankcastle/.ssh2/ | Authorization | 指向公钥的指针 |
| atlas | /etc/ssh | Hostkey | root 的私钥 |
| atlas | /etc/ssh | hostkey.pub | root 的公钥 |
| atlas | /etc/ssh | ssh2_config | 客户端配置 |
| atlas | /etc/ssh | ssh2d_config | 服务器配置 |

### 连接你的安全外壳服务器

尝试使用密码语（pass phrase）连接到安全外壳服务器。

1. 以普通用户 `frankcastle` 登录客户端计算机 `chivas`。
2. 尝试通过 Secure Shell 连接到你的服务器—`atlas`—
   ```
   ssh2 atlas
   ```

#### 第四部分：管理你的网络

3. 如果你正确配置了客户端和服务器，系统会提示你输入在使用 `ssh-keygen` 创建客户端密钥时输入的密码语。

密钥 "/home/frankcastle/.ssh2/id_dsa_1024_a" 的密码语，注释为 "1024-bit dsa, created by frankcastle@chivas.paunchy.net Sat May 29 19:27:40 1999"：

4. 输入正确的密码语，你应该已经通过安全的加密通道连接到安全外壳服务器。

![](img/1fa05dc2b61f40be78509e4d8bfc1fe_411_0.png)

如果你的客户端机器在第一次连接服务器时没有服务器的公钥，那么 `/etc/ssh2/hostkey.pub` 文件将被复制到你家目录下的 `~/.ssh2/hostkeys` 目录。之后每次连接 `atlas` 时，你都不会在登录提示中看到“接受主机密钥检查”。这是一种潜在的危险情况，因为在双方拥有对方的公钥之前，无法进行完全的主机认证。

如果你没有正确配置密钥和其他文件，你仍然可以连接到远程安全外壳服务器。系统会提示你输入普通密码，就像通过 Telnet 连接一样。

`frankcastle@atlas's password:` 

输入你的密码即可连接。你仍然通过加密通道进行连接，但 Secure Shell 无法正确将你的公钥传回给客户端机器。这意味着你无法验证所连接的服务器是否是正确的。你可能受到中间人攻击的威胁，某些人可能会伪造你正尝试连接的计算机。在这种情况下，你正在使用一个完全加密的连接到一台假机器。

再次强调，你应该根据自己的判断来确定连接到虚假服务器的潜在危险是否严重。如果你在私有网络内使用 Secure Shell 连接，你应该能够判断潜在的危险并采取适当行动。如果你是从互联网连接，那么潜在损害可能会大得多。

然而，在这个示例中，你是从服务器本身连接到自己的安全外壳服务器，你有充分理由相信没有虚假服务器参与。继续连接，Secure Shell 将在你的家目录 `/home/encryptme/.ssh/` 下创建一个 `known_hosts` 文件：

主机 'atlas' 已添加到已知主机列表。

正在创建随机种子文件 `~/.ssh/random_seed`。这可能需要一些时间。
`myuser@password:` 

如果你查看家目录（在本例中为 `/home/frankcastle`）`.ssh` 目录下新创建的 `known_hosts`，你会发现 Secure Shell 为你的主机创建了一个密钥。

### 连接不同的计算机

之前的示例仅提供了从 `chivas` 连接到 `atlas` 的指令。如果你想反反方向操作，或者想连接到多台计算机，则需要更多的配置。

![](img/1fa05dc2b61f40be78509e4d8bfc1fe_412_0.png)

你不希望从其他机器拷贝私钥。这将违反私钥的机密性概念。

你需要在每个新的客户端机器上创建新的私钥。请每台客户端计算机按照之前的指令操作：`/home/frankcastle/.ssh2/id_dsa_1024_a`、`/home/frankcastle/.ssh2/id_dsa_1024_a.pub`、`/home/frankcastle/.ssh2/Identification`、`/home/frankcastle/.ssh2/hostkeys/key_22_atlas.pub`、`/home/frankcastle/.ssh2/key_from_chivas.pub`、`/home/frankcastle/.ssh2/Authorization`、`/etc/ssh/Hostkey`、`/etc/ssh/hostkey.pub`、`/etc/ssh/ssh2_config`、`/etc/ssh/ssh2d_config`。（注：原文中此段存在大量重复的路径，翻译时已按逻辑处理）。

以下规则用于允许从互联网对您的私网进行外部访问。
