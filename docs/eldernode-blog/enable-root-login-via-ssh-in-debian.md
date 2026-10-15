
# 在 Debian 10 中通过 SSH 启用 Root 登录

> 原文：<https://blog.eldernode.com/enable-root-login-via-ssh-in-debian/>

![Enable Root Login Via SSH In Debian 10](img/0ff6eb23c1db1cff4349df97e0ffe0e2.png)

安全 Shell 允许您处理网络服务，以控制任何不安全的情况。在 Linux 和 Unix 之类的操作系统上，root 用户充当超级用户，可以执行许多普通用户无法执行的操作。要远程连接到您的系统并执行管理任务，您需要以 root 用户身份登录。在本文中，您将了解如何在 Debian 10 中通过 SSH 启用 Root 登录。如果您准备购买自己的 [Linux VPS](https://eldernode.com/linux-vps/)，可以访问 [Eldernode](https://eldernode.com/) 的可用套餐来购买合适的产品。

为了让本教程更好地发挥作用，请考虑以下先决条件：

- 拥有 sudo 权限的非 root 用户。
- 按照 Debian 10 的[初始设置](https://blog.eldernode.com/initial-setup-with-debian-10/)完成相关配置。

## 在 Debian 10 和 Debian 9 中通过 SSH 启用 Root 登录

Debian [Linux](https://blog.eldernode.com/tag/linux/) 不允许以 root 用户身份通过 `ssh` 协议登录服务器，并且默认情况下，该功能在主 SSH 配置文件中处于禁用状态。因此，当您尝试以 root 用户身份登录时，会收到一条错误消息。这是出于安全原因，错误消息为“权限被拒绝，请重试”。请阅读本文，了解通过 `ssh` 启用 root 登录的过程。

### 以 root 身份登录

当您使用 root 帐户登录时，您是具有管理权限的特殊用户。然而，您必须确保了解所运行的命令，因为任何粗心或格式错误的命令都可能导致整个操作系统无法使用。这就是出于安全原因不允许您以 root 身份登录的原因，您需要手动启用该功能。

在 [Debian](https://blog.eldernode.com/tag/debian/) 上，该功能最初作为安全预防措施处于启用状态，这意味着您不能通过 [SSH](https://blog.eldernode.com/enable-root-login-via-ssh-in-ubuntu-20-04/) 直接以 root 用户身份登录。

### 允许 SSH root 登录 Debian

由于 `PermitRootLogin` 参数控制 `ssh` root 权限，因此您必须更改该参数的值。该参数位于`/etc/ssh/sshd_config`文件中，`PermitRootLogin` 的值为“无密码”。因此，您需要将 `PermitRootLogin` 设置为 `yes`，以允许超级用户登录。

### 如何通过 SSH 启用 root 登录

在下文中，您可以查看本指南所需的简单步骤。通过这些步骤，您可以将默认的禁用模式更改为启用模式，并通过 SSH 登录。

打开 SSH 配置文件，使用您喜欢的文本编辑器。

```bash
nano /etc/ssh/sshd_config
```

然后搜索 `PermitRootLogin`，将其值改为 `yes`。如果该行存在并且以 `#` 开头被注释掉，则删除 `#`。

```text
PermitRootLogin yes
```

现在，您可以保存更新后的`/etc/ssh/sshd_config`文件，然后重启 SSH 服务器。使用下面的命令完成此操作：

```bash
systemctl restart sshd
```

如果没有出现新的错误，您应该能够通过 SSH 协议使用 root 用户帐户访问您的 Debian 服务器。

## 结论

在本文中，您了解了如何在 Debian 10 中通过 SSH 启用 Root 登录。如您所知，默认情况下，SSH root 登录在 Debian 中处于禁用状态，因为不建议通过 SSH 使用 root 密码。因此，您可以作为普通 Linux 用户通过 `ssh` 登录服务器，然后使用 `su` 命令以 root 用户身份登录。如果您有兴趣阅读更多内容，可以查看我们关于[在 Linux 上安装 SSH 服务器并允许 root 用户登录](https://blog.eldernode.com/install-ssh-server-on-linux-and-allow-root-user-login/)的相关文章。
