
然而，系统管理员可能希望使用密码登录的用户也能获得。在 `pam_ssh` 语句中添加 `want_agent` 选项，可以在没有加载任何密钥的情况下，触发在登录时启动代理。`want_agent` 选项出现在 FreeBSD 的语句中。

## 密钥选择

FreeBSD 的 `pam_ssh` 自动尝试解密用户 `~/.ssh` 目录下的 `identity`、`id_rsa`、`id_dsa` 和 `id_ecdsa` 密钥文件。不同名称的密钥不会被登录过程解密。

你无法从 `pam_ssh` 检查中移除任何这些密钥。要这样做，你需要使用不同版本的 `pam_ssh`，例如 CentOS 中的版本。

## CentOS pam_ssh

CentOS 的 EPEL 仓库包含了 `pam_ssh` 软件包。与 FreeBSD 和 Debian 不同，CentOS 的软件包没有包含任何 PAM 策略语句。你必须决定如何使用 `pam_ssh` 并为你的认证和会话策略创建规则。

在这里，我将 `pam_ssh` 添加到 `/etc/pam.d/login`，这是 CentOS 7.2 明文控制登录的 PAM 配置。我们从认证策略开始。

```
[user_unknown=ignore success=ok ignore=ignore \
default=bad] pam_securetty.so
auth [success=1 default=ignore] pam_ssh.so
auth substack system-auth
auth include postlogin
```

认证策略的第一条是检查安全终端的常规 `pam_security` 规则。

第二个语句将 `pam_ssh` 插入策略中。然而，我并没有使用标准控制，而是使用了 Linux-PAM 扩展控制。如果 `pam_ssh` 返回 `PAM_SUCCESS` 以外的内容，我们将忽略 `pam_ssh` 和会话策略。如果用户成功输入密码短语且 `pam_ssh` 可以解密用户的私钥，PAM 将跳过下一条规则。

## 第 10 章：使用 SSH 密钥访问控制台

下一个规则是普通系统身份验证的子栈。给 `pam_ssh` 提供一个可用的短语可以让策略跳过整个标准的 Unix 风格身份验证过程。

最后一条规则包含了标准的登录后处理。无论用户是使用短语还是密码登录，CentOS 都会执行日志记录和计数。

会话规则简单得多。将你的 `pam_ssh` 语句放在包含 `system-auth` 文件之前，这样你的 SSH agent 会会在其他环境启动之前启动。在会话策略中，它它可以放在 `pam_selinux.so open` 规则之后的任何位置。

```
session optional pam_ssh.so
session include system-auth
```

在 PAM 级别，你已经准备好了。

但在现代 CentOS 上，你几乎肯定正在使用 SELinux。如果你的 SSH agent 遇到问题，请检查 `/var/log/secure`。启动代理时的权限错误几乎都与 SELinux 相关。第 6 章讨论了与 SELinux 相关的 PAM 问题，并以 `pam_ssh` 为例。

## CentOS pam_ssh 登录提示

与 OpenPAM 不同，CentOS 的 `pam_ssh` 不会向用户显示“passphrase”提示。用户看到的是始终出现的 `Password:` 提示。CentOS 让 `pam_ssh` 变得完全隐形。用户需要知道输入他们的 SSH 短语是一个选项。

凭借本节之前提供的语句，如果用户没有输入短语，其身份验证尝试将回退到 `system-auth` 子栈，在那里 `pam_unix` 的 `try_first_pass` 选项意味着它将尝试使用用户输入的任何内容作为密码。

## 选择密钥文件

使用 `keyfiles` 选项指定 `pam_ssh` 尝试解密的哪些 SSH 私钥文件。CentOS 默认检查 `id_dsa`、`id_rsa` 和 `identity` 文件。`identity` 文件仅用于过时的 SSH 版本 1 协议，我建议你在 `pam_ssh` 中禁用它。

```
[success=1 default=ignore] pam_ssh.so \
keyfiles=id_dsa,id_rsa
```

你可以根据需要在此添加非标准的密钥文件。

如果你需要复杂的密钥选择，请查看 Debian 的 `pam_ssh`。

## Debian pam_ssh

Debian 在 `libpam-ssh` 包中提供了 `pam_ssh`。我们在本章之前讨论了 Debian 的 `pam_ssh` 策略，现在让我们直接进入该模块的工作原理。请记住，Debian 的 `pam_ssh` 配置期望你的 SSH 短语与你的密码相同。

Debian `pam_ssh` 有趣之处在于，它允许用户很好地控制哪些密钥可以用于身份验证，以及哪些密钥被添加到 SSH agent。

### Debian pam_ssh 密钥选择

Debian 的 `pam_ssh` 忽略所有常用的密钥文件，而是依赖 `$HOME/.ssh/login-keys.d` 和 `$HOME/.ssh/session-keys.d` 目录。这些目录默认不存在；用户必须创建它们。`login-keys.d` 目录包含可用于验证的 SSH 私钥文件。这里的文件可以是实际私钥，也可以指向标准 SSH 密钥的软链接。

```
$ cd .ssh/login-keys.d
$ ln -s ../id_rsa
```

当我登录系统时，`pam_ssh` 会检查此目录并尝试使用用户提供的密码来解密它找到的任何私钥。它会将任何能解密的密钥添加到用户的 SSH agent。`session-keys.d` 目录也包含密钥文件或软链接。与 `login-keys.d` 不同，`pam_ssh` 不使用这些密钥文件进行身份验证。然而，`pam_ssh` 会尝试使用密码解密会目录中的密钥，并将解密后的密钥添加到 agent。

## 绕过密码

也许你不想长密码，而是仅依赖短语进行控制台访问。这将允许你将 FTP 这样的明文协议与通过 SSH 或控制台登录分开。你可以通过重新排列 Debian 的认证策略来实现这一点。

```
auth sufficient pam_ssh.so
auth [success=1 default=ignore] pam_unix.so nullok_secure
auth requisite pam_deny.so
auth required pam_permit.so
```

我将 `pam_ssh` 规则移动到了认证策略的最顶部，甚至在 `pam_unix` 之前，但 `sufficient` 表达了预期的行为。实际上，由于手动编辑此文件使其不利于自动化管理，我更有可能重做整个策略，并移除永远不会被触发的语句。

```
auth sufficient pam_ssh.so
auth required pam_unix.so nullok_secure
```

不过，别人的安全意识没有我这么。他们的机器需要某些东西来确保他们有良好的密码，正如我们在下一章中看到的。

## 第 11 章：密码质量检查

“password”（密码）这个词很糟糕。每个人都知道，用户除外。几个 PAM 模块允许你对密码实施质量标准，以防止用户使用明显糟糕的密码。这些质量检查器不会消除密码，但会要求用户在设置密码时更有创意。

虽然大家都同意短密码会导致草率的密码，但使密码变得良好的特质是一个充满争议的话题。即使是冷静理性的系统管理员，在与其他理性明智的人讨论密码质量措施时，升级到刀肉斗，据已知也会失去他们的冷静和理智……有些人完全反对今天使用的密码质量检查概念。出于如此，我们不会讨论什么特征使密码变得良好。相反，我们将涵盖允许你对用户施加特定偏见的 PAM 模块。

最常见的密码质量检查模块是 `pam_passwdqc`。CentOS 7 删除了 `pam_passwdqc`，用 `pam_pwquality` 取而代之。Debian 同时提供了这两个包。我们将使用 `pam_passwdqc` 来解释密码质量检查的配置和概念，然后简要提到 `pam_pwquality`。

### 配置密码检查

当用户更改密码时测试密码质量。这使得质量检查成为密码策略中极少数功能之一，如下：

```
password requisite pam_passwdqc.so
password required pam_unix.so
```

在大多数系统中，`passwd(1)` 有它自己的 PAM 配置 `/etc/pam.d/password`。系统默认的更改不会影响 `passwd(1)`，除非 `/etc/pam.d/password` 显式包含了默认值。

当 `pam_unix` 认为应该更改密码时，它会修改 `/etc/password` 和相关文件。将任何密码质量检查放在 pam 语句之前，以便在更改之前对密码进行审计。

## 密码轮
