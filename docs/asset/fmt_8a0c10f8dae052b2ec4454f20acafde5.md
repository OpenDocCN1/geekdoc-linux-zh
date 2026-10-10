
指定本地“动态”应用层端口转发。这通过分配一个 socket 在本地监听 `port` 来实现，可选地绑定到指定的 `bind_address`。每当有连接到此端口时，连接将通过安全通道转发，然后使用应用程序协议来确定从远程机器连接到哪里。目前支持 `SOCKS4` 和 `SOCKS5` 协议，并且 `ssh` 将充当 SOCKS 服务器。只有 root 可以转发特权端口。动态端口转发也可以在配置文件中指定。

IPv6 地址可以通过将地址括在方括号中指定。只有超级用户可以转发特权端口。默认情况下，本地端口根据 `GatewayPorts` 设置进行绑定。但是，可以使用显式的 `bind_address` 将连接到特定地址。值为 “localhost” 的 `bind_address` 表示监听端口仅绑定用于本地使用，而空地址或 “*” 表示端口应从所有接口可用。

- `-E` `log_file`
将调试日志追加到 `log_file` 而不是标准错误。

- `-e` `escape_char`
设置具有 pty 会话的转义字符（默认：`~`）。转义字符仅在行首被识别。转义字符后跟点号（`.`）会关闭连接；后跟控制-Z 会挂起连接；后跟其自身则发送一次转义字符。将字符设置为“none”可禁用任何转义并使会话完全透明。

- `-F` `configfile`
指定替代的用户级配置文件。如果在命令行中提供了配置文件，则系统级配置文件（`/etc/ssh/ssh_config`）将被忽略。用户级配置文件的默认值为 `~/.ssh/config`

- `-f`
请求 `ssh` 在命令执行前进入后台。这在 `ssh` 将询问密码或口令但用户希望其在后台运行时很有用。这隐含了 `-n`。在远程站点启动 X11 程序的推荐方式是使用类似 `ssh -f host xterm` 的命令。

如果 `ExitOnForwardFailure` 配置选项设置为“yes”，则以 `-f` 启动的客户端将等待所有远程端口转发成功建立后再转入后台运行。

- `-G`
使 `ssh` 在评估 `Host` 和 `Match` 块后打印其配置并退出。

- `-g`
允许远程主机连接到本地转发端口。如果在复用连接上使用，则必须在主进程中指定此选项。

- `-I` `pkcs11`
指定 `ssh` 应使用的 PKCS#11 共享库，用于与提供用户 RSA 私钥的 PKCS#11 令牌通信。

- `-i` `identity_file`
选择用于读取公钥认证身份（私钥）的文件。协议版本 1 的默认文件是 `~/.ssh/identity`，协议版本 2 的默认文件是 `~/.ssh/id_dsa`、`~/.ssh/id_ecdsa`、`~/.ssh/id_ed25519` 和 `~/.ssh/id_rsa`。身份文件也可以在配置文件中按主机指定。可以指定多个 `-i` 选项（以及在配置文件中指定多个身份）。`ssh` 还会尝试从通过在身份文件名后附加 -cert.pub 得到的文件中加载证书信息。

- `-K`
启用基于 GSSAPI 的身份验证以及 GSSAPI 凭证到服务器的转发（委托）。

- `-k`
禁用 GSSAPI 凭证到服务器的转发（委托）。

- `-L` `[bind_address:]port:host:hostport`
`-L` `[bind_address:]port:remote_socket`
`-L` `local_socket:host:hostport`
`-L` `local_socket:remote_socket`
指定本地（客户端）主机上到给定 TCP 端口或 Unix 套接字的连接将被转发到远程端的主机和端口，或 Unix 套接字。其工作原理是分配一个套接字来监听本地一侧的 TCP `port`（可选绑定到指定的 `bind_address`），或者监听一个 Unix 套接字。每当有连接建立到本地端口或套接字时，该连接将通过安全通道转发，并从远程机器建立到 `host` 的端口 `hostport` 或 Unix 套接字 `remote_socket` 的连接。

端口转发也可以在配置文件中指定。只有超级用户可以转发特权端口。IPv6 地址可以通过将地址放在方括号中指定。

默认情况下，本地端口的绑定遵循 `GatewayPorts` 设置。然而，可以使用显式的 `bind_address` 将连接绑定到特定地址。`bind_address` 为 "localhost" 表示监听端口仅绑定用于本地使用，而空地址或 `'*'` 表示端口应对所有接口可用。

- `-l` `login_name`
指定在远程机器上登录的用户。也可以在配置文件中按主机指定。

- `-M`
将 `ssh` 客户端置于连接共享的“主”模式。多次使用 `-M` 选项将使 `ssh` 进入“主”模式，并在接受从属连接之前需要确认。详情请参阅 ssh_config5 中关于 `ControlMaster` 的描述。

- `-m` `mac_spec`
此外，对于协议版本 2，可以指定逗号分隔的 MAC（消息认证码）算法列表，按优先级排序。有关更多信息，请参阅 `MACs` 关键字。

- `-N`
不执行远程命令。这对于仅转发端口非常有用（仅限协议版本 2）。

- `-n`
将标准输入重定向到 /dev/null（实际上，阻止从标准输入读取）。当 `ssh` 在后台运行时必须使用此选项。一种常见的技巧是使用此选项在远程机器上运行 X11 程序。例如，`ssh -n shadows.cs.hut.fi emacs` 将在 shadows.cs.hut.fi 上启动 emacs，并且 X11 连接将通过加密通道自动转发。`ssh` 程序将被放入后台。（如果 `ssh` 需要询问密码或口令，此方法不起作用；另见 `-f` 选项。）

- `-O` `ctl_cmd`
控制活动的连接复用主进程。当指定 `-O` 选项时，`ctl_cmd` 参数将被解释并传递给主进程。有效命令包括："check"（检查主进程是否正在运行）、"forward"（请求转发而不执行命令）、"cancel"（取消转发）、"exit"（请求主进程退出）和 "stop"（请求主进程停止接受进一步的复用请求）。

- `-o` `option`
可用于以配置文件中使用的格式提供选项。这对于指定没有单独命令行标志的选项非常有用。有关下方列出的选项的完整详细信息及其可能的值，请参阅 ssh_config5。

- `AddressFamily`
- `BatchMode`
- `BindAddress`
- `CanonicalDomains`
- `CanonicizeFallbackLocal`
- `CanonicizeHostname`
- `CanonicizeMaxDots`
- `CanonicizePermittedCNAMEs`
- `ChallengeResponseAuthentication`
- `CheckHostIP`
- `Cipher`
- `Ciphers`
- `ClearAllForwardings`
- `Compression`
- `CompressionLevel`
- `ConnectionAttempts`
- `ConnectTimeout`
- `ControlMaster`
- `ControlPath`
- `ControlPersist`
- `DynamicForward`
- `EscapeChar`
- `ExitOnForwardFailure`
- `FingerprintHash`
- `ForwardAgent`
- `ForwardX11`
- `ForwardX11Timeout`
- `ForwardX11Trusted`
- `GatewayPorts`
- `GlobalKnownHostsFile`
- `GSSAPIAuthentication`
- `GSSAPIKeyExchange`
- `GSSAPIClientIdentity`
- `GSSAPIDelegateCredentials`
- `GSSAPIRenewalForcesRekey`
- `GSSAPITrustDNS`
- `GSSAPIKexAlgorithms`
- `HashKnownHosts`
- `Host`
- `HostbasedAuthentication`
- `HostbasedKeyTypes`
