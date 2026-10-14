
虽然大多数连接选项可以在命令行上设置，但我建议将永久信息存储在 `ssh_config` 中。`scp(1)` 和 `sftp(1)` 等程序（见第 6 章）会读取 `ssh_config`，而这些程序各自的命令行选项略有不同。使用配置文件可以集中配置。

The user’s personal configuration overrides the global configuration. Options set on the command line override both.

用户的个人配置覆盖全局配置。命令行上设置的选项覆盖两者。

### Per-Host Configuration

### 每主机配置

You can use the `Host` keyword to change how `ssh` connects to certain hosts. Here, I use the `Port` keyword to change the TCP port `ssh` connects to, but only for hosts in the `mwl.io` domain. It uses port 22 for all other hosts, as specified in `/etc/services`.

你可以使用 `Host` 关键字来更改 `ssh` 如何连接到某些主机。在这里，我使用 `Port` 关键字来更改 `ssh` 连接到的 TCP 端口，但仅适用于 `mwl.io` 域中的主机。对于所有其他主机，它使用端口 22，如 `/etc/services` 中指定。

```
Host *.mwl.io
Port 2222
```

I could also specify an IP address, or a network of IP addresses.

我也可以指定 IP 地址，或一组 IP 地址。

```
Host 192.0.2.*
Port 2224
```

Note that `ssh` matches these `ssh_config` entries based on what the user enters on

注意 `ssh` 根据用户输入的内容匹配这些 `ssh_config` 条目

命令行。`Host` 条目必须与用户输入的内容完全且区分大小写地匹配。假设我的 `ssh_config` 中包含上面两个 `Host` 条目，我们来看看实际效果。

```
$ ssh gluttony.mw1.io
```

这匹配第一个 `Host` 条目，因此 `ssh` 连接到 2222 端口。

我的桌面上的 `/etc/resolv.conf` 会自动为任何单独的主机名附加域名 `mw1.io`，因此我可能不会输入完全限定域名。相反，我会这样做。

```
$ ssh gluttony
```

这不会匹配我的第一个 `Host` 条目，因为我没有显式输入 `ssh_config` 中给出的域名。如果主机 `gluttony` 的 IP 地址在 `192.0.2.0/24` 中，那么第二个 `Host` 条目会匹配吗？不会，因为 `Host` 条目是在命令行上匹配的；不会对 DNS 进行检查。要基于 `Host` 条目中的 IP 地址进行匹配，我需要显式运行 `ssh 192.0.2.whatever`。对此主机的自定义设置需要像这样的 `Host` 条目。

```
Host gluttony
Port 2222
```

条件是按首次匹配的顺序解析。`Host` 条目之后列出的配置选项会一直生效，直到下一个 `Host` 条目为止。这个 `ssh_config` 可能是错误的。

```
Host *.mw1.io
Host 192.0.2.*
Port 2222
```

用户可能希望 `Port` 关键字适用于 `mw1.io` 域中的所有主机以及 `192.0.2.0/24` 中的所有 IP 地址。我们有一个针对 `mw1.io` 域中任意主机的条目，但对它没有特殊配置。`192.0.2.0/24` 中的任何主机都在 2222 端口运行 `sshd`。与其这样做，不如在同一行列出多个主机，用空格分隔。这里我列出了我的域名、我的 IP 地址和我的服务器。

```
Host 192.0.2.* mw1.io *.mw1.io gluttony avarice lust pride wrath envy sloth
Port 2222
```

我同时列出了 `*.mw1.io` 和 `mw1.io`，因为有一个名为 `mw1.io` 的特定机器。域名前面的星号和句点不会匹配该主机。

将任何全局默认值放在配置文件开头。假设你的组织有在 981 端口运行 SSH 的策略，因为他们喜欢通过模糊性来提高安全性，但你的特殊服务器使用不同的端口以获得更多模糊性。

```
Port 981
Host *.mw1.io
Port 2222
```

这里默认端口是 981，但指定的主机使用 2222 端口。有时你想在不破坏现有配置的情况下测试更改，或者也许你有一个自动化流程需要特殊的配置文件。要使用除 `ssh_config` 之外的配置文件，请在命令行上使用 `-F` 选项指定它。

```
$ ssh -F test-config avarice
```

你现在可以实验功能，而不会破坏你的工作配置。

如果你有足够多的主机，你可以考虑在 `ssh_config` 中建立规范主机名。

### Canonical Hostnames

在足够大的网络中，或在服务器动态创建和销毁的编排环境中，列出所有 SSH 服务器很快就会变得不切实际。`CanonicalizeHostname` 关键字告诉 `ssh` 将 `ssh_config` 中的独立 `Host` 条目重写为特定域名，然后如果存在则使用该主机名进行配置和密钥管理。这让你可以消除许多冗长的 `Host` 关键字。将 `CanonicalizeHostname` 设置为 `yes` 并将 `CanonicalDomains` 设置为你的域名。考虑以下配置：

```
CanonicalizeHostname yes
CanonicalDomains mwl.io
Host *.mwl.io
Port 2222
```

下次我运行 `ssh gluttony` 时，`ssh` 会检查是否存在主机名 `gluttony.mwl.io`。如果该主机名存在，`ssh` 会像我运行 `ssh gluttony.mwl.io` 一样评估 `ssh_config`。此连接会获得适用于 `mwl.io` 域中主机的特殊规则。

你可以列出多个规范域名。规范名称会按列出的顺序进行测试，第一个匹配项获胜。考虑如下条目。

```
CanonicalDomains mwl.io michaelwlucas.com
```

当我运行 `ssh wrath` 时，`ssh(1)` 会搜索 `wrath.mwl.io`。如果它找到该主机，就会打开连接。如果找不到该主机，`ssh` 会搜索 `wrath.michaelwlucas.com`。

如果你激活主机名规范化，`ssh` 默认会尝试规范化其中包含一个或更少点的主机。这让规范化可以捕获子域，例如 `www.detroit.mwl.io` 对应 `www.detroit`。要更改主机名中的最大点数，请使用 `CanonicalizeMaxDots` 关键字。这里我允许零个或更少的点。

```
CanonicalizeMaxDots 0
```

OpenSSH 还有一些其他的主机名规范化功能，在 `ssh_config(5)` 中讨论。

### Common SSH Options

人们最常用的功能是更改用户名、端口或添加 SSH 选项。

#### Changing Usernames

大多数 SSH 客户端假设客户端和服务器上的用户名相同，并尝试使用本地机器上的用户名登录远程系统。在我的大多数系统上，我的用户名是 `mwl`。偶尔有人会为我创建一个不同的用户名账户，比如 `mlucas` 或 `lucas` 或 `michael` 或 `jerkface`。我必须告诉 `ssh` 在远程系统上使用该用户名。通过将用户账户名、@ 符号，然后是远程机器名放在一起来实现。

```
$ ssh jerkface@devio.us
```

你也可以使用 `-l` 指定用户名。

```
$ ssh -l jerkface devio.us
```

如果这是持续性的操作，请在 `ssh_config` 中使用 `User` 选项指定用户名。

```
Host devio.us
User jerkface
```

通过将用户名存储在 `ssh_config` 中，我可以忘记它们并释放宝贵的脑力空间。

#### Changing Port

一些站点在除 22 之外的端口上运行 SSH，通常是为了提供改进安全性的外观。它实际上并不能保护 SSH，但确实可以减少日志噪音。

使用 `-p` 和端口号来更改 `ssh` 连接的端口。如果你的服务器在 2222 端口运行 `sshd`，请使用以下方式连接：

```
$ ssh -p 2222 gluttony
```

你可以在 `ssh_config` 中指定端口。

```
Port 2222
```

同样，我建议将永久连接信息存储在 `ssh_config` 中。

### SSH Options on the Command Line
