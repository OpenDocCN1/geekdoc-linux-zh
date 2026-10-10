

本任务假设你正在使用 OpenSSH，这是 Linux 中最常见的 SSH 实现。SSH Tectia（http://www.ssh.com）是原始的 SSH 实现，但由于它是商业软件包，因此在 Linux 中并不常见。还存在各种较少见的 SSH 实现，但大多数它们的配置方式与 OpenSSH 不同。

## 注意事项

由于你必须以 **root** 身份配置 OpenSSH，因此通常适用于 **root** 用户的注意事项同样适用。由于 SSH 是一个授予用户完整 shell 访问权限的服务器，SSH 中的配置错误或 bug 可能会迅速导致安全问题。因此，你应当小心避免犯错，并且如果系统确实不需要 SSH 服务器，你应该在完成任务后禁用它，或者更好的做法是卸载该软件包。

## 操作过程

本任务需要完成两个子任务。首先，你必须配置基本的 SSH 服务器选项。这个任务相当简单直接，但需要 **root** 权限。本任务的第二部分是设置 SSH 密钥以启用更快的登录。这一部分稍微复杂一些，但你可以作为普通用户来完成。

## 配置 SSH 服务器

SSH 服务器通过 `/etc/ssh/sshd_config` 文件进行配置，而 SSH 客户端通过 `/etc/ssh/ssh_config` 文件进行配置。这两个文件名非常相似，因此务必不要混淆它们！这两个文件均由注释（以井号 # 标记）和关键字/参数对组成，如下例所示：

```
PermitRootLogin no
```

就大多数情况而言，大多数发行版的客户端和服务器配置都是合理的。不过，你可能想更改一些选项。表 6.1 总结了一些你可能想要更改的额外的 SSH 服务器选项（在 `sshd_config` 中）。请特别留意 `PermitRootLogin` 服务器选项（为了符合本任务场景概述的要求，应将其设置为 no）以及 X 转发选项。使用 SSH 发起支持基于 X 应用程序的连接是一种便捷的远程 GUI 访问方法，但这种配置需要客户端和服务器都提供支持。

在 Linux 中，主要的 SSH 客户端自然地被命名为 `ssh`。在其最简单的形式中，你输入程序名，后接你想要连接的系统名称。通常，远程服务器随后会提示你输入密码。首次连接时，系统还会告知你无法验证远程站点的真实性。为了测试你目前的配置，你可以从第二个 Linux 系统执行如下操作：

```
alfred@werner:~$ ssh mail.pangaea.edu
```

```
The authenticity of host 'mail.pangaea.edu (192.168.1.6)' can't be established.
RSA key fingerprint is 4b:68:c1:a8:75:5e:b4:76:7b:a6:a2:0d:1a:8b:5f:48. Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mail.pangaea.edu,192.168.1.6' (RSA) to the list of known hosts.
alfred@mail.pangaea.edu's password:
[alfred@mail alfred]$
```

## 常见的 SSH 服务器配置选项

| 关键字 | 参数类型 | 描述 |
|---|---|---|
| Protocol | 整数 | SSH 协议版本号。OpenSSH 4 支持版本 1 和 2。若要指定两个版本，请用逗号分隔，例如 `Protocol 1,2` |
| ListenAddress | 主机名或 IP 地址及可选端口号 | 绑定服务器仅监听与指定地址相关的网络接口。如果指定了端口号，则端口号跟在地址和冒号之后，例如 `ListenAddress 172.26.7.3:22`。（默认的 SSH 端口号是 22。） |
| PermitRootLogin | 布尔值、without-password 或 forced-commands-only | 是否接受作为 root 的直接登录。此选项默认为 yes。将其更改为 no 将通过要求入侵者使用普通账户登录然后使用 `su`，从而需要两个密码，来提高系统的安全性。without-password 选项禁用了密码认证，意味着必须提供另一种认证方法。此选项并不意味着用户可以在没有任何认证的情况下登录 root 账户。forced-commands-only 选项仅启用公钥认证以远程执行命令，这对于执行远程备份等操作可能很有用。 |
| RhostsAuthentication | 布尔值 | 如果将此选项设置为 yes，服务器将接受基于协议级别 1 会话的 rhosts 可信主机认证模型的认证。这种认证方法 inherently 存在危险，因此我强烈建议你保持此选项的默认值 no。 |
| RsaAuthentication | 布尔值 | 如果将此选项设置为 yes（默认值），服务器将接受协议级别 1 会话的 Rivest/Shamir/Adleman (RSA) 认证。根据使用方式不同，这种方法可以提高安全性或消除输入密码的需要。 |
| PubKeyAuthentication | 布尔值 | 如果将此选项设置为 yes（默认值），服务器将接受协议级别 2 会话的公钥认证。根据使用方式不同，这种方法可以提高安全性或消除输入密码的需要。 |
| AuthorizedKeysFile | 文件名 | 存储客户端公钥认证密钥的文件的名称。 |
| KerberosAuthentication | 布尔值 | 如果设置为 yes，此选项使 SSH 接受 Kerberos 票据并通过 Kerberos 服务器对用户进行认证。如果你的网络使用 Kerberos，此选项非常有用，但其默认设置为 no。以 Kerberos 开头的其他选项可以微调配置；有关详细信息，请参阅 `sshd_config` 手册页。 |
| X11Forwarding | 布尔值 | 如果设置为 yes，此选项启用服务器转发 X 会话数据。默认值为 no。 |
| Compression | 布尔值 | 如果将此选项设置为 yes（默认值），服务器将接受客户端启用压缩的请求。此选项会消耗 CPU 时间，但减少网络带宽使用。 |

某些配置会自动将先前未知的站点添加到密钥文件中，因此你可能无需授权连接。无论哪种情况，对同一系统的后续连接将不再出现提示，也不需要通过输入 yes 来授权连接。不过，除非你按照下文所述的修改配置，否则你仍需要输入密码。（密码不会在屏幕上回显。）

Linux 的 ssh 客户端将当前用户名作为连接协议的一部分传递。如果服务器系统上的用户名与客户端系统上的用户名不同，你必须传递此信息。你可以通过在主机名前加上用户名和 at 符号 (@) 或使用 `-l` 参数来实现。例如，以下两条命令都会让你登录到 mail1.pangaea.edu 上的 al 账户：

```
$ ssh al@mail1.pangaea.edu
$ ssh -l al mail1.pangaea.edu
```

## 配置 SSH 密钥

在默认配置中，SSH 在建立连接时会提示输入密码。不过，你可以使用替代认证工具；表 6.1 总结了若干此类选项。当你激活这些方法时，它们会在密码提示之前被尝试。例如，考虑使用公钥认证。正如这里所描述的，这种方法将允许你在不输入密码的情况下登录远程系统。相反，SSH 将使用存储在客户端和服务器上的私钥和公钥。结果，入侵者无法伪装成你，除非他们入侵你的计算机并窃取你的公钥。你可以使用类似的方法，但进行一些修改，以要求在登录时使用特定的 SSH 短语（passphrase）而不是客户端的常规密码。要实施一个无需密码的公钥系统，请遵循以下步骤：

- 1. 登录到 SSH 客户端系统（例如 wegener.pangaea.edu）。
- 2. 输入以下命令以生成客户端系统的公钥和私钥：
  ```
  $ ssh-keygen -q -t rsa -f ~/.ssh/id_rsa -C '' -N ''
  ```
  
  ![](img/f430a19bdf014c43ad7c2d594afd5b21_310_0.png)
  
  如果在此命令中省略 `-N ''` 参数，程序会提示输入短语。然后，当你连接到服务器时，将需要使用短语而不是密码。如果在提示输入密码时按两次 Enter 键，其效果与包含 `-N ''` 相同。
- 3. 将 `~/.ssh/id_rsa.pub` 文件从客户端计算机复制到服务器计算机。你可以通过软盘、使用 `scp`（基于 SSH 的文件复制实用程序）或通过你选择的任何其他手段传输此文件。如果使用 `scp`，你必须输入密码。
- 4. 登录到 SSH 服务器系统（例如 mail1.pangaea.edu）。你可以使用 SSH 来完成此操作，但此时你仍需要使用密码。
- 5. 确保 `~/.ssh` 目录存在并具有 0700（`-rw-------`）权限。如有必要，输入 **mkdir** `~/.ssh` 以创建目录，或输入 **chmod** **0700** `~/.ssh` 以设置目录的适当权限。
- 6. 将从客户端传输的 `id_rsa.pub` 文件的内容添加到服务器上的 `~/.ssh/authorized_keys` 文件中。（此文件名可能不同；请检查 SSH 服务器配置中的 `AuthorizedKeysFile` 选项。）如果这是第一次

