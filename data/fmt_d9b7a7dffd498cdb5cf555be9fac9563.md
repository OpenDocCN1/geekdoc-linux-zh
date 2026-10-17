
正如你将看到的 `true`，`/etc/sudoers` 文件可以包含空行（会被忽略）和注释——行中紧随哈号 (`#`) 之后的任何字符都会被解释为注释。标准 Ubuntu 系统中 `sudoers` 文件中有意义的条目如下：

```bash
Defaults env_reset
root=(ALL) ALL
%admin=(ALL) ALL
```

这些行中的第一个指定了 `sudo` 命令行为的默认选项。`/etc/sudoers` 文件中唯一的选项是：

- `env_reset`：重置环境，使其仅包含 `LOGNAME`、`SHELL`、`USER` 和 `SUDO` 环境变量。这防止了其他变量传播到特权环境中。

你可能想在 `sudoers` 文件中更改 sudo 缓存 root 用户凭据的默认时间，这样你就不需要在设规定时间内再次输入密码。这些命令持续 15 分钟，许多管理员认为太长了。要显式设置此缓存周期，请修改（或添加）`sudoers` 文件中的 `Defaults` 条目如下所示：

```
Defaults env_reset, timestamp_timeout=XX
```

将 `XX` 改为你希望缓存权限而无需再次输入密码的分钟数。要要求所有用户在执行任何这些命令时始终输入密码，请将 `XX` 设置为 0。

接下来的两行非常有意思。以下条目表示 root 可以做任何事情并在系统上执行任何命令：

```bash
root=(ALL) ALL
```

# 第三部分：面向系统管理员的 Ubuntu

## 修复损坏的 sudo 命令

在专家模式下安装某些版本的 Ubuntu 使用标准的 root 机制，这可能导致你的系统处于普通用户无法使用 `sudo` 命令执行特权命令的状态。同时，即使在普通的 Ubuntu 系统上，某种情况下你的 `/etc/group` 或 `/etc/sudoers` 文件的内容也导致任何人无法执行任何特权操作。在后的情况下，你可以重启系统，按 Escape 键查看 GRUB 启动菜单，并从 GRUB 菜单选择恢复模式（Recovery Mode）。这将重启你的系统并进入 root shell。

一旦你以 root 身份登录 Ubuntu 系统，请检查 `/etc/group` 是否包含 `admin` 组，并且任何希望执行管理操作的用户都是该组的成员。如果你没有 `admin` 组，可以使用本章之前介绍过的“用户和组”或通过命令行界面（作为 root 用户）使用如下命令来添加：

```bash
# addgroup --system admin
```

接下来，确保你的 `/etc/sudoers` 文件包含授予 `admin` 组管理权限的条目：

```bash
%admin=(ALL) ALL
```

如果你的 `/etc/sudoers` 命令中不存在此条目，你可以使用 `visudo` 命令编辑该文件并添加该条目。

在确保 `admin` 组存在并在 `/etc/sudoers` 文件中被引用后，你只需要将任何你希望能够运行受保护应用程序的用户添加到 `admin` 组。你可以通过本章之前讨论的“用户和组”或通过命令行使用如下命令来做到这一点：

```bash
# usermod -aG admin username
```

## 在 Ubuntu 系统上安装 Kerberos

在 Ubuntu 系统上，很少需要从源码编译 Kerberos，因为 Ubuntu 仓库已经提供了最新版本的 Kerberos 软件包，你可以在作为 Kerberos 服务器的系统以及任何 Kerberos 服务器的客户端上使用你需要的这些包。要安装 Kerberos，你必须使用包管理工具安装以下软件包：

- `krb5-admin-server`: 你必须在所有的 Kerberos 服务器和从机系统中安装此包。该包提供了必须安装在 Kerberos 5 服务器或服务器备用机上的程序。
- `krb5-config`: 此包提供了 Kerberos 的模板配置和相关文档，并在安装 `krb5-admin-server` 或 `krb5-user` 软件包时会自动安装。
- `krb5-kdc`: 此包提供了 Kerberos 密钥分发中心 (`KDC`) 提示、相关实用程序、模板配置以及相关文档，并在安装 `krb5-admin-server` 软件包时会自动安装。
- `krb5-user`: 你必须在所有客户端系统中安装此包。该包提供了基础 Kerberos 程序（`kinit`, `klist`, `kdestroy`, `kpassword`）以及经过 Kerberos 处理的 telnet 和 ftp 应用。
- `libpam`: 你必须在所有的 Kerberos 客户端和服务器系统中安装此包，以便安装 Kerberos PAM，从而你可以将 Kerberos 集成到这些系统的 PAM 认证过程中。
- `ntp`: 如本节引言所述，你应该在 Kerberos 服务器上安装一个网络时间协议 (`NTP`) 服务器，以确保其时间计时准确。用于通过 Kerberos 服务验证客户端的票据带有时间戳，因此，Kerberos 服务器和所有客户端之间的时钟同步至关重要。
- `ntpdate`: 如本节引言所述，你应该在所有的 Kerberos 客户端系统中安装一个网络时间协议 (`NTP`) 客户端，以确保它们的时间计时准确。`ntpdate` 客户端默认安装在所有 Ubuntu 桌面系统中——我在这里在这里列出是为了确保你理解它在你的系统中是可用的，并与你 Kerberos 服务器上的 NTP 服务器进行同步。

安装 `krb5-admin-server` 软件包会显示一条警告信息，解释在你在使用 Kerberos 认证之前必须对你的站点进行配置。这没什么意外的！

## 在服务器和客户端上配置 NTP

在配置和启动你的 Kerberos 服务器之前，你应该首先确保你的 Kerberos 服务器拥有正确的时间。你还应该配置你的 Kerberos 服务器的每个客户端，使其在启动任何 Kerberos 客户端之前从 Kerberos 服务器获取时间信息。你可以在客户端系统上安装和配置 Kerberos 软件时（或之前）配置客户端使用 Kerberos 服务器的时间——本节提供了客户端 NTP 配置的说明，以帮助确保你不会忘记这一步。

### 配置 NTP 服务器

在将作为 Kerberos软件服务器的系统上安装 `ntp` 软件包，会自动配置你的服务器去查询 `ntp.ubuntu.com` 的时间服务器。在这种情况下该服务器宕机或不可用，你可以配置你的时间服务器，能够查询互联网上可用的公共 NTP 服务器池中的一个或多个时间服务器。有关公共 NTP 服务器列表以及使用它们的信息，请参阅 http://support.ntp.org/bin/view/Servers/WebHome。

NTP 服务器的信息存储在配置文件 `/etc/ntp.conf` 中。使用你喜欢的文本编辑器编辑此文件，搜索默认的 `ntp.ubuntu.com` 条目，并在之后添加如下行：

```
server north-america.pool.ntp.org
server pool.ntp.org
```

如果你不在北美洲，你应该将第一行更改为更适合你地理位置的时间服务器名称，具体见 http://support.ntp.org/bin/view/Servers/NTPoolServers 的解释。

在输入额外时间服务器的条目后，保存文件，退出文本编辑器，并使用如下命令重启 NTP 服务器：

```
/etc/init.d/ntp restart
```

这将使用新的配置条目重启你的时间服务器。

### 配置 NTP 客户端

如前所述，`ntpdate` NTP 客户端软件默认安装在所有 Ubuntu 桌面系统中。在客户端系统上安装 Kerberos 时，你应该确保每个客户端系统上的 NTP 客户端软件从你的 NTP 服务器获取时间同步。这确保了 Kerberos 票据在整的一天中都是同步的。

与大多数系统不同，`ntpdate` 服务实际上在你每次启动以太网接口时都会运行。当你启动以太网接口时，会执行脚本 `/etc/network/ifup.d/ntp`。该脚本运行 `/usr/sbin/ntpdate-debian` 脚本，该脚本转而执行 `/usr/sbin/ntp` 程序，并使用 Ubuntu Linux 桌面系统中 `ntpdate` 应用的 `/etc/default/ntpdate` 文件中指定的时间服务器。

默认情况下，Ubuntu 系统使用的 `/etc/default/ntpdate` 配置文件告诉 `ntpdate` 客户端去与 NTP 服务器相同的配置文件文件中查找信息，即 `/etc/ntp.conf` 文件。遗憾的是，除非你在这些系统上也安装了 NTP 服务器软件，否则该文件在客户端系统中不存在，而这是没有必要的。由于由于原因，我们将修改 `/etc/default/ntpdate` 配置文件以忽略此文件并显式引用你的 NTP 服务器。操作如下：
