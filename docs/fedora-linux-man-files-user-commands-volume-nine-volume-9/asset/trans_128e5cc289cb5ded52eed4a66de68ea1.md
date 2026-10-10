
## ssh

如果将 **ExitOnForwardFailure** 配置选项设置为 “yes”，则以 **-f** 启动的客户端在将自己置于后台之前，将等待所有远程端口转发成功建立。

### 选项

- **-G**
  使 **ssh** 在评估完 **Host** 和 **Match** 块后打印其配置并退出。

- **-g**
  允许远程主机连接到本地转发端口。如果在复用连接上使用，则必须在主进程上指定此选项。

- **-I pkcs11**
  指定 **ssh** 应使用哪个 PKCS#11 共享库来与提供用户私钥 RSA 密钥的 PKCS#11 令牌进行通信。

- **-i identity_file**
  选择读取公钥认证身份（私钥）的文件。协议版本 1 的默认值是 *~/.ssh/identity*，协议版本 2 的默认值是 *~/.ssh/id_dsa*、*~/.ssh/id_ecdsa*、*~/.ssh/id_ed25519* 和 *~/.ssh/id_rsa*。身份文件也可以在配置文件中按主机指定。可以有多个 **-i** 选项（以及配置文件中指定的多个身份）。**ssh** 还将尝试通过向身份文件名追加 -cert.pub 获得文件名来加载证书信息。

- **-K**
  启用基于 GSSAPI 的认证以及向服务器转发（委派）GSSAPI 凭据。

- **-k**
  禁用向服务器转发（委派）GSSAPI 凭据。

- **-L [bind_address:]port:host:hostport**
- **-L [bind_address:]port:remote_socket**
- **-L local_socket:host:hostport**
- **-L local_socket:remote_socket**
  指定本地（客户端）主机的给定 TCP 端口或 Unix 套接字上的连接将被转发到远程侧的给定主机和端口，或 Unix 套接字。其工作原理是分配一个套接字来监听本地侧的 TCP *port*（可选绑定到指定的 *bind_address*）或 Unix 套接字。每当本地端口或套接字建立连接时，连接通过安全通道转发，并从远程机器连接到 *host* 的 *hostport* 端口或 Unix 套接字 *remote_socket*。

  端口转发也可以在配置文件中指定。只有超级用户可以转发特权端口。可以通过将地址放在方括号中来指定 IPv6 地址。

  默认情况下，本地端口根据 **GatewayPorts** 设置进行绑定。但是，可以使用显式的 *bind_address* 将连接绑定到特定地址。*bind_address* 为 "localhost" 表示监听端口仅用于本地使用，而空地址或 `'*'` 表示端口应从所有接口可用。

- **-l login_name**
  指定在远程机器上登录的用户名。也可以在配置文件中按主机指定。

- **-M**
  将 **ssh** 客户端置于连接共享的"master"（主）模式。多个 **-M** 选项将 **ssh** 置于需要确认后才接受从属连接的 "master" 模式。有关详细信息，请参阅 ssh_config5 中关于 **ControlMaster** 的描述。

- **-m mac_spec**
  此外，对于协议版本 2，可以按优先级顺序指定 MAC（消息认证码）算法的逗号分隔列表。有关更多信息，请参阅 **MACs** 关键字。

- **-N**
  不执行远程命令。这对于仅转发端口非常有用（仅限协议版本 2）。

- **-n**
  将 stdin 重定向到 /dev/null（实际上，阻止从 stdin 读取）。当在后台运行 **ssh** 时必须使用此选项。一个常见的技巧是使用它在远程机器上运行 X11 程序。例如，`ssh -n shadows.cs.hut.fi emacs` 将在 shadows.cs.hut.fi 上启动 emacs，并且 X11 连接将通过加密通道自动转发。**ssh** 程序将被置于后台。（如果 **ssh** 需要询问密码或短语，则此方法不起作用；请参阅 `-f` 选项。）

- **-O ctl_cmd**
  控制活跃的基于连接复用的主进程。当指定 **-O** 选项时，*ctl_cmd* 参数将被解释并传递给主进程。有效命令包括："check"（检查主进程是否在运行）、"forward"（请求转发而不执行命令）、"cancel"（取消转发）、"exit"（请求主进程退出）以及 "stop"（请求主进程停止接受进一步的复用请求）。

- **-o option**
  可用于以配置文件使用的格式提供选项。这对于指定没有单独命令行标志的选项非常有用。有关下文列出的选项及其可能值的完整详情，请参阅 ssh_config5。

  **AddressFamily**
  **BatchMode**
  **BindAddress**
  **CanonicalDomains**
  **CanonicizeFallbackLocal**
  **CanonicizeHostname**
  **CanonicizeMaxDots**
  **CanonicizePermittedCNAMEs**
  **ChallengeResponseAuthentication**
  **CheckHostIP**
  **Cipher**
  **Ciphers**
  **ClearAllForwardings**
  **Compression**
  **CompressionLevel**
  **ConnectionAttempts**
  **ConnectTimeout**
  **ControlMaster**
  **ControlPath**
  **ControlPersist**
  **DynamicForward**
  **EscapeChar**
  **ExitOnForwardFailure**
  **FingerprintHash**
  **ForwardAgent**
  **ForwardX11**
  **ForwardX11Timeout**
  **ForwardX11Trusted**
  **GatewayPorts**
  **GlobalKnownHostsFile**
  **GSSAPIAuthentication**
  **GSSAPIKeyExchange**
  **GSSAPIClientIdentity**
  **GSSAPIDelegateCredentials**
  **GSSAPIRenewalForcesRekey**
  **GSSAPITrustDNS**
  **GSSAPIKexAlgorithms**
  **HashKnownHosts**
  **Host**
  **HostbasedAuthentication**
  **HostbasedKeyTypes**
  **HostKeyAlgorithms**
  **HostKeyAlias**
  **HostName**
  **IdentityFile**
  **IdentitiesOnly**
  **IPQoS**
  **KbdInteractiveAuthentication**
  **KbdInteractiveDevices**
  **KexAlgorithms**
  **LocalCommand**
  **LocalForward**
  **LogLevel**
  **MACs**
  **Match**
  **NoHostAuthenticationForLocalhost**
  **NumberOfPasswordPrompts**
  **PasswordAuthentication**
  **PermitLocalCommand**
  **PKCS11Provider**
  **Port**
  **PreferredAuthentications**
  **Protocol**
  **ProxyCommand**
  **ProxyUseFdpass**
  **PubkeyAcceptedKeyTypes**
  **PubkeyAuthentication**
  **RekeyLimit**
  **RemoteForward**
  **RequestTTY**
  **RhostsRSAAuthentication**
  **RSAAuthentication**
  **SendEnv**
  **ServerAliveInterval**
  **ServerAliveCountMax**
  **StreamLocalBindMask**
  **StreamLocalBindUnlink**
  **StrictHostKeyChecking**
  **TCPKeepAlive**
  **Tunnel**
  **TunnelDevice**
  **UpdateHostKeys**
  **UsePrivilegedPort**
  **User**
  **UserKnownHostsFile**
  **VerifyHostKeyDNS**
  **VisualHostKey**
  **XAuthLocation**

- **-p port**
  连接到远程主机的端口。也可以在配置文件中按主机指定。

- **-q**
  静默模式。抑制大多数警告和诊断消息。

- **-Q cipher | cipher-auth | mac | kex | key | protocol-version**
  查询 ssh 支持的指定版本 2 的算法。可用功能包括：*cipher*（支持的对称加密算法）、*cipher-auth*（支持认证加密的对称加密算法）、*mac*（支持的消息完整性代码）、*kex*（密钥交换算法）、*key*（密钥类型）和 *protocol-version*（支持的 SSH 协议版本）。

- **-R [bind_address:]port:host:hostport**
- **-R [bind_address:]port:local_socket**
- **-R remote_socket:host:hostport**
- **-R remote_socket:local_socket**
  指定远程（服务器）主机的给定 TCP 端口或 Unix 套接字上的连接将被转发到本地侧的给定主机和端口，或 Unix 套接字。其工作原理是分配一个套接字来监听远程侧的 TCP 端口或 Unix 套接字。每当此端口或 Unix 套接字建立连接时，连接通过安全通道转发，并从本地机器连接到 host 的 port hostport 或 local_socket。

  端口转发也可以在配置文件中指定。只有以 root 身份登录到远程机器时才能转发特权端口。可以通过将地址放在方括号中来指定 IPv6 地址。

  默认情况下，服务器上的 TCP 监听套接字仅绑定到回环接口。这可以通过指定 bind_address 来覆盖。空 bind_address 或地址 `*` 表示远程套接字应在所有接口上监听。指定远程 bind_address 仅在启用服务器的 **GatewayPorts** 选项时才会成功（请参阅 sshd_config5）。

  如果端口参数为 `0`，则在服务器上动态分配监听端口，并在运行时报告给客户端。当与 **-O** forward 一起使用时，分配的端口将打印到标准输出。

- **-S ctl_path**
  指定用于连接共享的控制套接字位置，或字符串 `none` 以禁用连接共享。有关详细信息，请参阅 ssh_config5 中关于 **ControlPath** 和 **ControlMaster** 的描述。

- **-s**
  可用于请求在远程系统上调用子系统。子系统是 SSH2 协议的一个功能，促进了将 SSH 用作其他应用程序（例如 sftp）的安全传输。子系统作为远程命令指定。

- **-T**
  禁用伪终端分配。

- **-t**
  强制伪终端分配。这可用于在远程机器上执行任意基于屏幕的程序，这在实施新服务时非常有用，例如。多个 **-t** 选项强制 tty 分配，即使 **ssh** 没有本地 tty。

- **-V**
  显示版本号并退出。

- **-v**
  详细模式。使 **ssh** 打印关于其进展的调试消息。这有助于调试连接、认证和配置问题。多个 **-v** 选项增加详细程度。最大值为 3。

- **-W host:port**
  请求将客户端的标准输入和输出转发到 *host*
