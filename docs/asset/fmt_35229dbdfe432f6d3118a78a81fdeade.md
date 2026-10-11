
# 298

# 附录 C: Samba 帮助页

请注意，`smbd` *始终* 会使用一个有效的 UNIX 用户来代表客户端执行操作，即使在“安全共享”级安全模式下也是如此。

由于在共享级安全模式下，客户端不需要向服务器发送用户名，`smbd` 使用了多种技术来确定代表客户端使用的正确 UNIX 用户。

使用以下方法构建一个可能与客户端密码匹配的可能 UNIX 用户列表：

- 如果设置了“仅来”(`guest only`)参数，将跳过所有其他阶段，仅检查“访客账户”(`guest account`)用户名。
- 如果在共享连接请求设置了用户名，则该用户名（映射后——参见“用户名映射”(`username map`)）将作为潜在用户名添加。
- 如果客户端之前有过“登录”请求（`SessionSetup` SMB 调用），则此 SMB 中发送的用户名将作为潜在用户名添加。
- 所请求的客户端 NetBIOS 名称将作为潜在用户名添加到列表中。
- “user”列表中的任何用户都将作为潜在用户名添加。

如果未设置“仅来”参数，将使用提供的密码尝试此列表。密码匹配的用户将用作 UNIX 用户。

如果设置了“仅来”参数，或者无法确定用户名，那么如果该共享被标记为“访客账户”可用，则将使用该访客用户，否则将被拒绝。

请注意，在共享级安全模式下，最终使用哪个 UNIX 用户授予访问权限可能会*非常*令人困惑。

另见“关于用户名/密码验证的注意”（`NOTE ABOUT USERNAME/PASSWORD VALIDATION`）章节。

- `security=user`

这是 Samba2 的默认设置。在用户级安全模式下，客户端必须使用有效的用户名和密码进行“登录”（可以使用“用户名映射”参数进行映射）。在此模式下也可以使用加密密码（参见“加密密码”(`encrypted passwords`) 参数）。诸如“user”和“仅来”等参数，如果设置，则会被应用并可能更改此连接使用的 UNIX 用户，但仅在用户通过身份验证后进行。

请注意，在服务器成功验证客户端之前，所请求的资源名称*并不是*服务器。这就是为什么在允许服务器自动将未知用户映射到“访客账户”的情况下，访客在共享级安全模式下无法工作。有关此操作的详细信息，请参见“映射到访客”(`map to guest`) 参数。

另见“关于用户名/密码验证的注意”章节。

- `security=server`

在这种模式下 Samba 将尝试通过将用户名/密码传递给另一个 SMB 服务器（作为 NT 节点）来验证它们。如果失败，它将回退到 `security = user`，但由于已经协商了加密密码，Samba 无法回退检查 UNIX 密码文件，它必须有一个有效的 `smbpasswd` 来检查用户。请查看 `docs/` 目录下的文档 `ENCRYPTION.txt` 了解如何设置的详情。

## smb.conf (5)

请注意，从客户端的角度来看，`security=server` 与 `security=user` 是相同的。它只影响服务器处理身份验证的方式，不会以任何方式影响客户端看到的内容。

请注意，在服务器成功验证客户端之前，所请求的资源名称*不会*发送给服务器。这就是为什么在允许服务器自动将未知用户映射到访客账户的情况下，访客共享在服务器级安全模式下无法工作。有关此点的详细信息，请参见“映射到访客”(`map to guest`) 参数。

参见“关于用户名/密码验证的注意”章节。另参见“密码服务器”(`password server`) 参数以及“加密密码”(`encrypted passwords`) 参数。

- `security=domain`

只有在用 `smbpasswd` 将此机器加入 Windows NT 域后，此才能正常工作。它期望“加密密码”(`encrypted passwords`) 参数被设置为“true”。在此模式下，Samba 通过将用户名/密码传递给 Windows NT 主域控制器或备份域控制器来验证它们，方法与 Windows NT Server 的完全相同。

# 附录 C：Samba 手页

- `SO_RCVBUF`
- `SO_SNDLOWAT`
- `SO_RCVLOWAT`

标记为 * 的项接受一个整数参数。其他项可以可选地接受 1 或 0 参数来启用或禁用选项；默认情况下，如果不指定 1 或 0，它们将被启用。

要指定参数，请使用 `SOME_OPTION=VALUE` 语法，例如 `SO_SNDBUF=8192`。请注意，等号前后不能有任何空格。

如果你处于局域网中，一个合理的选项可能是：

```
socket options = IPTOS_LOWDELAY
```

如果你处于局域网中，你可以尝试：

```
socket options = IPTOS_LOWDELAY TCP_NODELAY
```

如果你处于广域网中，也许可以设置 `IPTOS_THROUGHPUT`。注意，某些选项可能会导致你的 Samba 服务器完全无法运行。请谨慎使用这些选项！

默认：`socket options = TCP_NODELAY`

示例：`socket options = IPTOS_LOWDELAY`

- `ssl` (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

请注意，由于出口限制，此代码在你当前的 Samba 二进制版本中**没有**默认启用。

此变量启用或禁用 SSL 模式。如果设置为 "no"，则 SSL samba 的行为将与非 SSL 的 Samba 完全相同。如果设置为 "yes"，则取决于 `ssl hosts` 和 `ssl hosts resign` 变量来是否需要 SSL 连接。

默认：`ssl=no` 示例：`ssl=yes`

- `CA certDir` (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

请注意，由于出口限制，此代码在你当前的 Samba 二进制版本中**没有**默认启用。

此变量定义了查找证书颁发机构（CA）的位置。通用目录应该包含每个 samba 信任的 CA 的一个文件。文件名必须是 CA 的“发行名称”（Distinguished Name）的哈希值。如何设置此目录将在本文稍后部分解释。目录中所有不符合此方案的文件都将被忽略。如果你不需要验证客户端证书，则不需要此变量。

默认：`CA certDir = /usr/local/ssl/certs`

- `ssl CA certFile` (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

请注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

此变量是定义 CA 的另一种方法。受信任 CA 的证书被收集在一个大文件中，此变量指向该文件。你可能会使用定义 CA 的两种方法之一。如果你有许多 CA 或希望保持灵活，首种选择更优；如果你只有一个 CA 且想保持简单，第二种更优（你不需要创建哈希命名的文件）。如果你不验证客户端证书，则不需要此变量。

默认：`ssl CA certFile = /usr/local/ssl/certs/trustedCAs.pem`

- `ssl ciphers` (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

请注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

此变量定义了在 SSL 协商期间应提供的加密算法。除非你清楚自己在做什么，否则不应设置此变量。

- `ssl client key` (G)

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

如果存在，文件中的证书将被 `smclient` 使用。如果服务器需要证书，则需要此文件。

默认：`ssl client key = /usr/local/ssl/certs/smclient.pem`

此变量是启用 SSL 的 Samba 的部分。只有当你的系统上编译了 SSL 库且在配置时提供了 `--with-ssl` 配置选项时，它才可用。

注意，由于出口控制原因，此代码在任何当前的 Samba 二进制版本中**没有**默认启用。

这是 `smclient` 的私钥。如果客户端应该拥有证书，则需要此文件。

默认：`ssl client key = /usr/local/ssl/private/smclient.pem`

- `ssl compatibility` (G)
