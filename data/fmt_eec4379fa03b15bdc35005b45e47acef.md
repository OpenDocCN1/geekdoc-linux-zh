
| obey pam restrictions | no | Samba 是否强制执行 `/etc/pam.d/samba` 中定义的账户和会话模块类型。 |

| pam password change | no | `smbd` 是否使用 PAM 设施来实现由 unix 控制的密码更改？如果启用，将使用 `/etc/pam.d/samba` 中的 PAM 密码设置代替密码程序。 |

表 16.4 提供了 `smb.conf` 中每个 PAM 相关选项的简要描述。一旦启用了 Samba 的编译 PAM 支持，我们必须回答三个运行时问题以理解 Samba 如何使用此功能：

- `Smdb` 是否使用 `auth` 模块类型进行用户认证（`encrypt passwords = no`）？

- Samba 是否遵循其 PAM 配置文件中的账户和会话模块模块类型（`obey pam restrictions = yes`）？

- `Smdb` 是否使用 `password` 模块类型更改凭据（`password change = yes`）？

只有当 `encrypt passwords = no`（2.2 及之前版本的默认设置）时，Samba 才能使用 `auth` 模块类型。对于所有分发的 PAM 模块，调用应用程序必须提供用户的明文密码传递给 PAM 设施。在使用 NTLM 认证客户端时无法满足这一要求。因此，当 `encrypt passwords = yes` 时，`smbd` 将忽略其 PAM 配置文件中的 `auth` 模块类型，并始终通过 `smbpass` 文件验证用户。

尝试更改用户的系统密码时，除了存储在 `smbpass` 中的 LanMan/NT 哈希值外，新密码的明文是已知的。这些 PAM 模块可以用于更新 Unix 账户密码，但不需要旧密码。由于 `smbd` 并知道原始密码的明文，它会以 root 身份执行 Unix 密码更改以避免提示旧密码。这并不总是有效的。

# 用户账户管理与单点登录

```
[global]
<..>,
## 遵循 PAM 认证模块行
encrypt passwords = no
```

```
## 遵循 PAM 账户和会话模块类型
obey pam restrictions = yes
```

```
## 遵循 PAM 密码模块-type
## 若要使此项生效，必须设置有效的 'passwd chat'
pam password change = yes
```

如果 `smbd` 已经被指示要同步 Unix 密码和 `smbpasswd` 条目，我们可以使用推荐的 `encrypt password = yes` 配置，同时利用 PAM 进行账户、会话和密码管理。

# Windows 域中的 Unix 服务——pam_winbind

图 16.3 最初在第 14 小时介绍，当时我们开始检查 Winbind。我们记得 Winbind 软件包由三个组件组成：

- *winbind 守护进程*，它负责管理 Windows NT SID 与 Unix uids/gids 之间的映射。`winbind` 还为 PAM 模块提供了一些认证“胶水”，因此无需运行 `nmbd` 和 `smbd` 来验证用户凭据。

- 一个 NSS 模块，用于 Windows 域账户生成 `/etc/passwd`（以及 `/etc/group`）风格的条目。

- 一个 PAM 模块，Unix 服务可以使用它验证登录和更改密码。

前两项在第 14 小时已进行了详细介绍。然而，在该小时内跳过了 PAM 模块。

Winbind 的强大之处在于能够实现如图 16.4 所示的场景。在这种环境中，Unix 服务（如 `sshd`）会请求 Windows 域控制器验证用户，而不是在本地查找。这意味着任何账户更改都会被 Winbind 客户端立即看到。因为只有一个账户，所以没有需要同步的账户信息。

![](img/e6dc042fe420c610acdd193e834a4772_315_0.png)

![](img/e6dc042fe420c610acdd193e834a4772_315_1.png)

# 用户账户管理与单点登录

在系统上安装可用的 Windbind 模块的第一步，是遵循第 14 小时 `smbd` 的说明将 Samba 加入 Windows 域。对于我们的目的来说，不需要运行 `smbd` 和 `nmbd`。`windbind` 守护进程本身将处理与 Windows DC 的所有通信。

加入域后，在 `/lib` 中安装 `libssnd_windbind.so.2` 库，将其添加到 `/etc/nsswitch.conf` 中的 `passwd` 和 `group` 数据库行，并启动 `windbind`，我们就可以专注于为您配置 PAM 组件了。Samba 2.2.2 使用的 `make install` 脚本不会将 `pam windbind` 库拷贝到 `/lib/security`。我们必须通过执行来实现：

```
root# cp /usr/local/src/samba-2.2.2/source/nsswitch/pam_windbind.so /lib
```

这假设 Samba 源码树位于 `/usr/local/src/samba-2.2.2/`。如果本地 Samba 源码树在不同的文件夹，请替换为相应的路径。

> Linux 和 Solaris 使用 `.so` 扩展作为共享库。`pam_windbind` 共享库的实际名称可能取决于服务器的操作系统。

同时，确保所有权和权限设置防止用户篡改也是一个好主。

```
root# chown root /lib/security/pam_windbind.so
root# chgrp root /lib/security/pam_windbind.so
root# chmod 755 /lib/security/pam_windbind.so
```

现在 PAM 模块已正确安装，我们可以开始配置服务以使用它。OpenSSH 项目是由 Tatu Yönen 开发的 SSH 协议的免费实现。作为传统 telnet 服务器的安全替代品，它正成为许多网络中的常见成员（这出于充分的理由）。

现在是时候提到，所有的 Unix 应用程序都包含了对 PAM 的支持。在使用 PAM 配置遇到问题时，要检查的第一个细节是验证应用程序是否支持此接口。OpenSSH 包含对 PAM 的支持，但默认未启用。通常，供应商提供的 OpenSSH 二进制分发版在构建时已包含 PAM 支持。然而，如果需要从源码构建 `sshd` 二进制文件，只需在配置脚本中添加 `--with-pam` 选项，并按所示验证该参数已被识别。

```
root# pwd
/usr/local/src/openssh-2.9.9p2
root# ./configure --with-pam
<...output deleted...>
OpenSSH 已通过以下选项配置:
  User binaries: /usr/local/bin
  System binaries: /usr/local/sbin
  Configuration files: /usr/local/etc
  Askpass program: /usr/local/libexecec/ssh-askpass
  Manual pages: /usr/local/man/manX
  PID file: /var/run
sshd default PATH: /usr/bin:/bin:/usr/sbin:/usr/local/bin
Random number collection: Device (/dev/urandom)
  Manpage format: doc
  PAM Support: yes
<...output deleted...>
```

输出的最后一行表示 OpenSSH 能够加载使用 PAM 认证连接所需的文件。剩余的安装过程如下：

```
root# make
root# install
```

在 Linux 系统上，OpenSSH 从 `/etc/pam.d/sshd` 读取其 PAM 配置信息。Winbind 仅支持认证、账户和密码会话类型，为了支持本地用户，`/etc/pam.d/sshd` 包含一个包含 `unix.so` 的单行。

> 在 PAM 配置遇到问题时，要检查的第一个细节是验证应用程序是否支持此接口。OpenSSH 包含对 PAM 的支持，但默认未启用。通常，供应商提供的 OpenSSH 二进制分发版在构建时已包含 PAM 支持。然而，如果需要从源码构建 `sshd` 二进制文件，只需在配置脚本中添加 `--with-pam` 选项，并按所示验证该参数已被识别。

在 Linux 系统上，OpenSSH 从 `/etc/pam.d/sshd` 读取其 PAM 配置信息。Winbind 仅支持认证、账户和密码会话类型，为了支持本地用户，`/etc/pam.d/sshd` 包含一个包含 `unix.so` 的单行。
