
在作为 Kerberos 服务器的系统中安装 `ntp` 包会自动将你的服务器配置为 `ntp.ubuntu.com` 的客户端服务器。在这种情况下，如果主机宕机或不可用，你可能希望配置你的时间服务器能够从互联网上可公共 NTP 服务器池咨询一个或多个时间服务器。

# 第四部分

## 附章节

关于服务器以及关于它们的使用信息，请参见 http://support.ntp.org/bin/view/Servers/WebHome。

NTP 服务器的配置信息存储在配置文件 `/etc/ntp.conf` 中。使用你喜欢的文本编辑器编辑此文件，搜索默认的 `ntp.ubuntu.com` 条目，并在其之后添加类似下面的行：

```
server north-america.pool.ntp
server pool.ntp
```

如果你不在北美洲（像我一样），你需要将第一行更改为更适合你地理位置的时间服务器名称，正如在 http://support.ntp.org/bin/view/Servers/NTPpoolServers 中解释的那样。

在输入了额外时间服务器的条目后，保存文件，退出文本编辑器，并使用如下命令重启 NTP 服务器：

```
/etc/init.d/ntp restart
```

这将使用新的配置条目重启你的时间服务器。

## 配置 NTP 客户端

如前所述，所有的 Ubuntu 和 Kubuntu 桌面系统都安装了 `ntp` 客户端软件。当客户端系统上启用 Kerberos 时，确保每个客户端系统上的 NTP 客户端从你的 NTP 服务器获取同步信息。这确保了 Kerberos 票据上的时间戳在全年都是同步的。与大多数系统不同，`ntp` 客户端会在每次启动以太网接口时激活。每当你启动以太网接口时，都会执行脚本 `/etc/ntp.run`。该脚本会在后台运行 `/usr/sbin/ntpdate-deb`，它会根据 `/etc/default` 配置文件中 Ubuntu 和 Linux 桌面系统用于 `ntp` 应用程序定义的参数执行 `/usr/sbin/ntpdate`。

在 Ubuntu 和 Ubuntu 系统上，你的 NTP 客户端配置信息存储在 `/etc/default/ntpdate` 文件中。默认情况下，此文件告诉 `ntp` 客户端查找与 NTP 服务器相同的信息，即 `/etc/ntp.conf`。遗憾的是，除非你在这些系统上安装了 NTP 服务器，否则该文件并不存在，而这是没必要的。因此，我们需要修改 `/etc/default/ntp` 配置文件以忽略此 NTP 服务器。操作如下：

1. 修改定义 `NTP_USE_CONF` 变量的行来设置该变量的值，以便 `ntp` 客户端连接到 `/etc/ntp.conf` 或要使用的时间服务器列表，因为除非你在该包中安装了 NTP 服务器，否则该文件在你的系统中并不存在。
2. 在 `.NTPSERVERS` 变量定义的时间服务器列表开头添加你的 `ntp` 服务器的 IP 地址。该条目应与 `ntp.ubuntu` 的默认值用逗号隔开。

编辑此文件后，每当系统（或你）启动以太网接口时，“正确的事情”就会发生，但当时不会为你同步时钟，因为此时你的以太网接口（们）可能已经处于启动状态。要做到这一点，请在命令行手动运行 `/usr/sbin/ntpdate-debian`，将你的系统时与你的 NTP 服务器同步。

## 管理用户、组、身份验证和高级权限

> 提示 如果你的客户端系统运行时间很长（例如几天或几周），它们的可能会可能会与服务器产生偏差，因为 `nptdate` 应用（或更准确地说 `nptdate-debian` 脚本）只在你启动以太网接口时运行。这意味着你的时钟没有定期与 NTP 服务器同步，这可能会给 Kerberos 令牌带来问题。为了消除这个潜在问题，你可以简单设置一个定时 `cron` 任务，按预定的间隔将系统时钟与服务器同步。我发现每日同步是足够的，所以我使用 `sudo` 命令执行我喜爱的文本编辑器并创建 `/etc/cron.daily/nptdate-debian` 文件，内容如下：

```
/usr/sbin/nptdate-debian
```

创建此文件后，通过执行以下命令确保它是可执行的：

```
sudo chmod 755 /etc/cron.daily/nptdate-debian
```

现在，你的系统会自动与你在 `/etc/default/ntpdate` 中识别的时间服务器进行同步。

## 设置 Kerberos 服务器

在你的服务器上安装 Kerberos 服务器包（`krb5-admin-server`）及其依赖项会显示一些基本配置信息，并提示你输入领域（realm）的 Kerberos 服务器名称或 IP 地址。遗憾的是，它请求的信息不足以实际启动和使用域中的 Kerberos 服务器，因此本节将引导你完成在服务器上实际使用 Kerberos 所需的步骤。

在要在成为 Kerberos 服务器的系统上安装 `krb5-admin-server` 和依赖项后，执行以下操作：

1. 使用文本编辑器编辑 `/etc/krb5.conf` 并执行以下操作：
   * 在 `[libdefs]` 部分中，修改 `default_realm` 条目，使其设置为你的领域名称（全大写）。在我的情况下，我使用的是 `VONHAGEN.ORG` 领域，该条目看起来如下：
   `default_realm = VONHAGEN.ORG`
   * 在 `[reuses]` 部分中，添加一个条目来标识你的 Kerberos 服务器的主机名或 IP 地址（即运行主 Kerberos 守护进程的系统）以及主密钥分发中心（KDC）。我的主 Kerberos 服务器的条目如下：
   `VONHAGEN.ORG = {`
   `kdc = 192.168.6.140`
   `admin_server = 192.168.6.140`
   `}`
   * 在 `[kdc]` 部分中，添加条目来识别你的 Kerberos 服务器的主机名或 IP 地址（即运行主 Kerberos 守护进程的系统）以及你的主密钥分发中心。我的主 Kerberos 服务器的条目如下：
   `VONHAGEN.ORG = {`
   `kdc = 192.168.6.140`
   `admin_server = 192.168.6.140`
   `}`
   * 在 `[domain]` 部分中，添加条目来识别你的 Kerberos 服务器的主机名或 IP 地址（即运行主 Kerberos 守护进程的系统）以及你的主密钥分发中心（KDC）。我的主 Kerberos 服务器的条目如下：
   `VONHAGEN.ORG = {`
   `kdc = 192.168.6.140`
   `admin_server = 192.168.6.140`
   `}`
   * 在 `[cap]` 部分中，添加条目来识别你的 Kerberos 服务器的主机名或 IP 地址（即运行主 Kerberos 守护进程的系统）。我的主 Kerberos 服务器的，该条目看起来如下：
   `VONHAGEN.ORG = 192.168.6.140`
   * 在 `[acl]` 部分中，添加条目来识别你的 Kerberos 服务器的主机名或 IP 地址（即运行主 Kerberos 守护进程的系统）以及你的主密钥分发中心（KDC）。我的主 Kerberos 服务器的，条目看起来如下：
   `VONHAGEN.ORG = 192.168.6.140`
   * 在 `[princip]` 部分中，添加条目来识别你的 Kerberos 服务器的主机名或 IP 地址（即运行主 Kerberos 守护进程的系统）以及你的主密钥分发中心（KDC）。我的主 Kerberos 服务器的，看起来如下：
   `VONHAGEN.ORG = 192.168.6.140`
   * 在 `[dbdb]` 部分中，添加条目来识别你的 Kerberos 服务器的主机名或 IP 地址（即运行主 Kerberos 守护进程的系统）以及你的主密钥分发中心（KDC）。我的主 Kerberos 服务器的，条目看起来如下：
   `VONHAGEN.ORG = 192.168.6.140`

安装这些软件包后，你使用喜喜欢的文本编辑器编辑 `/etc/pam.d/common-auth` 文件，在调用 `pam_unix.so` 的行之后添加以下行：
`auth sufficient pam_krb5.so use_first_pass forwardable`

确保此条目不包含任何类型定义！保存此文件后，你现在可以使用 `klist` 命令来测试 Kerberos 是否正常工作，该命令会尝试为指定用户（在此例中 `vwh`）获取 Kerberos 令牌：

```
klist vwh
```
