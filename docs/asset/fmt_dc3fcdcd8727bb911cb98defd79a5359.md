
Samba 提供了许多自动化服务端活动的工具。通过各种 `include` 参数、变量以及指令，服务器可以根据需求表现出动态行为。Samba 的 VFS 接口提供了编程方式来覆盖操作。

## 问答

- Q 共享可以同时具有 `preex` 和 `postex` 设置吗？

  A 是的，可以配置服务同时具有 `preex` 和 `postex` 设置，或者具有两者和。

- Q `%u`、`%s` 和 `%g` 变量可以在 `include` 参数中使用吗？

  A 这将允许你根据个人或组指定设置。一个示例是添加 `include = %G.conf` 来包含部门共享，其中 `%G.conf` 将包含定义。

## 管理用户账户与单点登录

在讨论 Samba 安装时，无法避免过渡到用户认证主题。我们已经在第 7 小节中花费了大量时间涵盖 Samba 用于验证用户连接请求的各种模型。在本节中，我们将探索当用户在两个领域中都拥有账户时，如何协调这种认证。

其中一些问题在第 7 小节介绍 `username map` `smb.conf` 参数时已经提到过。该选项用于指向一个文件，该文件包含从 Windows 用户名如 Gerald Carter 到 Unix 账户名如 jerry 的映射。我们不仅必须处理登录名称的差异，还可能必须为用户处理两套密码。为了支持 Microsoft 的挑战/响应认证，Samba 要求系统管理员维护一个包含登录名称和密码哈希的 `smbpasswd` 文件。它们之间没有自动或默认的关联

`/etc/passwd` 中的密码和 `smbpasswd` 中的密码。实际上，无法通用地将其中一种转换为另一种。本节要回答的问题是：“我们如何自动同步存储这两个文件中的条目？”

同步 `/etc/passwd` 中的密码条目和 Samba 的 `smbpasswd` 文件的替代方案是建立单点登录（SSO）模型，这允许 Unix Windows 域控制器验证用户，反之亦然。在第 14 小节“替换 Windows NT 文件和打印服务器——全方位方案”中，我们检查了 Windbind 软件包的两个部分：NSS 模块和 windbind 守护进程。在本节中，我们将这两个组件添加一个 PAM 模块。这样做允许我们实现使用 Windows 域用户账户通过 SSH 或 Telnet 登录 Unix 服务器等操作。

另一方面，将 Samba 配置为主域控制器为验证 Windows 服务提供了一种方法，例如通过 Unix 服务器连接 Windows NT 成员服务器。关于 Samba 域控制功能的完整介绍将在第 21 和第 22 小节给出。

### /etc/passwd 与 smbpasswd 之间的密码同步

我们将从一个自诞生以来一直是 Samba 管理员噩梦的话题开始讨论：在本地系统密码数据库与 Samba 的 `smbpasswd` 文件之间同步密码。其思路是捕获 CIFS 客户端的密码更改，并同时更新 Unix 账户的密码。

我们的示例假设 `smb.conf` 中已看到 `encrypt passwords = yes`。特别是，如果不使用密码加密，那么支持来自 Windows 9x/ME 的密码更改可能会非常困难。这是因为客户端传输的是全大写的密码字符串。任何经验丰富的管理员都会对不敏感的字符串立即提高警惕，因为这限制了可用字符的数量，使得密码更容易被破解。

图 16.1 给出了用户密码更新的事件流。

- 1. 首先，客户端发送密码请求。
- 2. Samba 使用存储在 `smbpasswd` 中的副本作为新密码的解密密钥，验证客户端知道旧密码哈希。如果服务器无法解密新密码，则客户端不知道旧密码哈希。
- 3. 如果 `smb.conf` 中启用了 `unix password sync` 参数，`smbd` 将尝试先更改 Unix 密码。如果此步骤失败，将向客户端返回错误消息。
- 4. 如果 Unix 密码成功更改，或者如果 `unix password sync = no`，则 `smbd` 将将更改 `smbpasswd` 条目。

## 图 16.1 通过 Samba 同步密码。

![](img/e6dc042fe420c610acdd193e834a4772_306_0.png)

表 16.1 展示了几个与密码更改相关的全局 `smb.conf` 选项。由于已经提到了 `unix password sync` 参数，我们将从那里开始。

## 表 16.1 密码更改参数

| 名称 | 默认值 | 描述 |
|---|---|---|
| `passwd chat` | *newpassword* `%n`\n *newpassword* `%n`\n *changed* | 定义 `smbd` 与 `passwd` 程序之间的对话。 |
| `passwd chat debug` | no | 是否应在调试模式下运行对话？如果启用且日志级别设置为大于 100 的值，新密码的明文将写入进程的日志文件中。 |
| `passwd program` | `/bin/passwd` | 指定更改 Unix 用户密码时要调用的程序。 |
| `unix password sync` | no | `smbd` 是否应尝试更新用户的 `/etc/passwd` 条目以及 `smbpasswd` 文件中的哈希？ |
| `min passwd length` | 5 | 定义新密码允许的最小字符数。 |

292 第 16 小节

为了开始对 `smb.conf` 进行密码同步更改，我们必须启用 `unix password sync` 参数，否则表 16.1 中的其余选项将被忽略。同时，我们必须指定用于更改 Unix 账户凭据的程序。

由于由于 `passwd` 程序是以 root 身份执行的，使用 `%u` 变量来指定要更新密码的用户名。

```
[global]
<...
## 启用密码同步功能
unix password sync = yes
```

```
## 使用 'passwd' 程序更改凭据
passwd program = /usr/bin/passwd %u
```

![](img/e6dc042fe420c610acdd193e834a4772_307_0.png)

如果没有在 `/usr/bin/passwd` 字符串后面附加 `%u`，此示例将在你不知情情的情况下更改 root 的密码。更糟糕，它会将密码更改为用户发送的密码字符串（我们知道破解像 "steve123" 这样的密码有多困难）。

下一步是要定义特定站点的值。`passwd chat` 选项定义了 `smbd` 与 `passwd` 程序之间成功更改密码时的预期对话。需要引入两个 `passwd chat` 脚本特有的新变量。

- `%n`—旧密码字符串。在使用加密密码时，该字符串是未知的。
- `%n`—新密码的明文。

为了开发一个可运行的 `passwd chat` 脚本，我们必须知道成功更改密码的预期结果。捕获这些最简单的方法是手动运行 `passwd` 程序。在这里，我们为名为 jerry 的用户更改密码。

```
root# /usr/bin/passwd jerry
Changing password for user
New UNIX password:
Retype UNIX password:
passwd: all updated
```

Samba 允许我们使用控制字符，如 `\n`（换行）、`\t`（制表符）和 `\s`（空格），加上通配符来匹配任何序列。从已显示的密码更改来看，我们可以将其简化为

```
passwd chat = *d:%n\n*d:%success
```

## 管理用户账户和单点登录

花几分钟观察 `passwd chat` 值和 `passwd` 程序的输出，以让自己相信此脚本是有效的。

![](img/e6dc042fe420c610acdd193e834a4772_308_0.png)

> 为了密码 chat 在未知旧密码的情况下成功，系统上的超级用户必须能够更改账户的密码。如果 Samba 服务器使用 NIS/YP，它必须是 NIS 主。寻找 `smbd` 与你的密码程序之间的连接字符串可能是困难的。如果你遇到困难，在 `smb.conf` 的全局部分设置这三个选项会有帮助。

```
passwd chat debug = yes
log level = 100
log file = /var/log/log.%m
```

将在 Samba 的日志文件中记录密码 chat 的明文。这包括密码以及响应字符串。这些参数仅在排查密码更改时使用，随后应立即禁用 passwd chat并将日志级别设置为更合适的值。

## Samba -with-pam
