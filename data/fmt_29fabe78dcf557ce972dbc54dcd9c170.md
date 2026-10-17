
| forks | no | yes |

| postfix_mysql | not found | yes |

| quantum | no | yes |

| volatile | no | yes |

图 3：要查看此内容，请选择 Munin 进程并向下滚动到图表。

## 提示

你可以通过执行 `service munin stop` 退出 Munin 进程，或通过执行 `service munin-node stop` 停止节点。

## 日志文件

如果 Munin 或 Monit 有问题，请检查它们的日志文件。Munin 的日志文件位于 `/var/log/munin/`。Monitor 日志位于 `/var/log/monitor/`。使用 `tail` 命令扫描 Munin 日志。`/var/log/munin/munin.log` 中的每条目都会帮助你了解更多关于 Munin 的状态：

2018-08-01 12:05:00 [INFO] Munin-update failed (4.2 sec)

2018-08-01 12:05:05 [ERROR] Munin-update

要查看如何使用 `munin-update`，获取并进入 `munin-update.log` 内容。这将验证 Munin 及其 Web 界面正在工作：[EEST Aug 10:45:49] info: Munin 5.2.1 with http interface at 127.0.0.1:2882 [EEST Aug 10:45:49] info: 'ubuntu' Munin 5.2.1 started

现在，你必须重启 Munin 以使更改生效。Munin 将开始监控这些 Apache 属性，这可以通过 `service apache2 status` 的输出进行验证。你需要等一会儿，让 Munin 更新并包含关于这些 Apache 属性的信息。

# 快速贴士

- 所有 Munin 工具都是纯文本脚本，你可以轻松地读取和调试、更改它们的输出，并用任何编程语言重写它们。事实上，如果你愿意，可以把 Munin 移植到 Go 或 Rust！

## 为 Munin 配置 Apache

为了在网页浏览器中查看 Munin 的状态，你需要在网络上的虚拟主机上安装 Apache。此外，你必须启用该模块。如果尚未启用，可以通过执行 `apache2ctl -M` 检查 Apache 模块。如果未启用，可以通过执行 `a2enmod` 启用它——该模块可以在 `libapache2-mod` 包中找到。

Munin 配置 Apache 非常简单，因为 Munin 使用位于 `/etc/munin/apache24.conf` 的 Apache 配置文件。因此，你需要执行以下命令：

- `cp /etc/apache2/sites-available/apache24.conf /etc/apache2/sites-enabled/`

- `a2ensite apache2.conf`

- `systemctl restart apache2`

请注意，上述过程创建了 `/etc/munin/apache24.conf` 的新副本，并保留原始版本的 `/etc/munin/apache24.conf`，以便如果你监控不同的 Web 服务器，你需要按照不同的流程为 Munin 的输出添加 Web 服务器支持。

图 2 显示了 Munin 站点的默认输出，可以通过 http:/// 访问

```bash
set indent 4
set log=/var/log/munin.log
set data=/var/lib/munin/data
set status=/var/lib/munin/status
```

图 4 显示了 Munin 站点的默认输出，可以通过 http:/// 访问

Munin 从运行 munin 的机器收集数据，可以在 `/usr/share/munin/munin-update` 找到

## Munin 工具

Munin 带有许多工具——其中一些在 `/usr/bin`，另一些在 `/usr/sbin`：

```bash
$ cd /usr/bin; ls munin-check munin-cron
$ cd /usr/sbin/; ls munin*
```

`munin-check` 工具用于修复 munin 文件，而 `munin-cron` 工具由 `cron` 进程执行。`munind` 工具是 Munin 的文档。新闻是 `munind` 支持插件的配置，在 bash 提示符处按下键：`--help` 显示 `munind` 命令的各种输出功能。

Munin 从运行 munin 的机器收集数据，可以在 `/usr/share/munin/munin-update` 找到

## 配置 Munin

Munin 需要在 `/etc` 中配置文件并修改 munin 配置文件，这将在下一部分加载。本部分关于配置 Munin 以收集你想要的数据。`munin.conf` 文件可能是你为了让 Munin 运行而需要修改的文件。

Munin 支持插件——可以通过查看 `/usr/share/munin/plugins` 目录找到所有可用 Munin 插件列表。此外，你可以通过列出 `/etc/munin/` 的内容找到许多插件。

我们将修改 `/etc/munin/munin.conf` 以适应变量值，这使得 `munin.conf` 比预期的要短。具体来说，`etc/munin/munin.conf` 如下：

```bash
$ cat /etc/munin/munin.conf
include(/etc/munin/d/)
address 127.0.0.1
use_name = yes
```

之后，`munin-configure` 命令将返回 Munin 插件列表，启用取决于你想监控的 munin 系统：命令的输出如下：

| 插件 | 建议 | 进程 |

| :--- | :--- | :--- |

| apache_access | no | yes |

| apache_volume | no | yes |

| cpu | yes | yes |

| disk | no | yes |

| forks | no | yes |

| postfix_mysql | not found | yes |

| quantum | no | yes |

| volatile | no | yes |

图 3：要查看此内容，请选择 Munin 进程并向下滚动到图表。

## 提示

你可以通过执行 `service munin stop` 退出 Munin 进程，或通过执行 `service munin-node stop` 停止节点。

## 日志文件

如果 Munin 或 Monit 有问题，请检查它们的日志文件。Munin 的日志文件位于 `/var/log/munin/`。Monitor 日志位于 `/var/log/monitor/`。使用 `tail` 命令扫描 Munin 日志。`/var/log/munin/munin.log` 中的每条目都会帮助你了解更多关于 Munin 的状态：

2018-08-01 12:05:00 [INFO] Munin-update failed (4.2 sec)

2018-08-01 12:05:05 [ERROR] Munin-update

要查看如何使用 `munin-update`，获取并进入 `munin-update.log` 内容。这将验证 Munin 及其 Web 界面正在工作：[EEST Aug 10:45:49] info: Munin 5.2.1 with http interface at 127.0.0.1:2882 [EEST Aug 10:45:49] info: 'ubuntu' Munin 5.2.1 started

现在，你必须重启 Munin 以使更改生效。Munin 将开始监控这些 Apache 属性，这可以通过 `service apache2 status` 的输出进行验证。你需要等一会儿，让 Munin 更新并包含关于这些 Apache 属性的信息。

# 快速贴士

- 所有 Munin 工具都是纯文本脚本，你可以轻松地读取和调试、更改它们的输出，并用任何编程语言重写它们。事实上，如果你愿意，可以把 Munin 移植到 Go 或 Rust！

## 为 Munin 配置 Apache

为了在网页浏览器中查看 Munin 的状态，你需要在网络上的虚拟主机上安装 Apache。此外，你必须启用该模块。如果尚未启用，可以通过执行 `apache2ctl -M` 检查 Apache 模块。如果未启用，可以通过执行 `a2enmod` 启用它——该模块可以在 `libapache2-mod` 包中找到。

Munin 配置 Apache 非常简单，因为 Munin 使用位于 `/etc/munin/apache24.conf` 的 Apache 配置文件。因此，你需要执行以下命令：

- `cp /etc/apache2/sites-available/apache24.conf /etc/apache2/sites-enabled/`

- `a2ensite apache2.conf`

- `systemctl restart apache2`

请注意，上述过程创建了 `/etc/munin/apache24.conf` 的新副本，并保留原始版本的 `/etc/munin/apache24.conf`，以便如果你监控不同的 Web 服务器，你需要按照不同的流程为 Munin 的输出添加 Web 服务器支持。

图 2 显示了 Munin 站点的默认输出，可以通过 http:/// 访问

```bash
set indent 4
set log=/var/log/munin.log
set data=/var/lib/munin/data
set status=/var/lib/munin/status
```

图 4 显示了 Munin 站点的默认输出，可以通过 http:///

## 其他监控

Munin 并不是唯一的可用监控软件。其他的包括 Nagios (`nagios.org`)、`MRTG` (`oss.opteler.org`)、`Cacti` (`cacti.net`)、`Zabbix` (`zabbix.org`) 和 LGTT (`org`)。Icing (`icing.com`)、`OpenNMS` (`opnms.org`) 等都可监控你的服务器。

所有工具都有依赖项——在这些监控工具之间选择的最佳方法是尝试它们，然后决定什么最适合你的需求。Munin 非常简单易用，然而，它只能监控事物而无法调试 Linux 机器的服务。Cacti（带有 RFTIS）、MRTG 和 MuninRRRD 用于图表，这意味着它们需要你。

另一方面，Nagios 功能强大但需要更多时间来学习和配置。然而，Nagios 可以监控多个服务器并在出现问题时提醒你。此外，它拥有巨大的插件库，允许你监控数据库服务器和 Web 应用程序。尽管如此，从像 Munin 这样简单的工具开始总是个好主意。对于此类企业级解决方案

# Munin 和 Monit 教程

`etc/conf-enabled/apache2` 具有让 Monit 监控 apache 的权限——你可以查看 `/etc/conf-enabled/apache2` 的内容，如果你的 apache 使用了不同的端口或其他自定义参数，可以对其进行任何修改。然后，你需要重启 Monit 以使更改生效。

在这个最终版本中，我们将修改所使用的 Monit 配置文件，其中还包含了启用 Monit Web 界面的细节。现在你可以管理 Monit 你的服务器（这需要一个运行良好的邮件服务器作为后盾），我们将留给已经在 Linux 机器上拥有可用邮件服务器的读者作为练习。

你也可以在你的机器上监控数据库服务器。列出数据库服务器的 TCP 端口列表非常有帮助。为了获取 Monit 的当前状态，你应该使用 `monit status` 命令。如果 Monit 的 Web 界面尚未启用，将得到以下输出：

Monit: The HTTP interface is not enabled, please enable the web server and use the option “allow to connect” to monit

如果 Web 界面配置不当，`monit` 将成功运行并在 `monit status` 显示以下内容时返回有用信息：

# Process ‘apache’

| status | does not exist |

| :--- | :--- |

| monitoring status | active |

| monitoring mode | active |

| on reboot | start |

| data | Tue Jul 21 2018 22:54:28 |

之前的输出显示：Apache 目前未在运行。Monit 将启动 Apache，因此之前的输出将被替换为以下内容：

# Process ‘mysql’

| status | OK |

| :--- | :--- |

| monitoring status | Monitored |

| monitoring mode | active |

| on reboot | start |

| pid | 6304 |

| data collected | Tue Jul 21 2018 22:54:28 |

所以你应该检查以获取 Monit 的摘要状态，你应该执行带有路由的 `monit summary` 命令——其输出大致与你从 Monit 界面获得的内容相似。

## Monit 的 Web 界面

Monit 有一个 Web 界面，应该通过它启用——本节将说明该过程。但你们都应该意识到，Monit 有它自己的 Web 服务器，你不需要做任何操作来添加对 Monit 的支持。毕竟，如果 Monit 的 Web 界面未启用，它如何监控你的服务器并获取信息呢？

`monit` 文件中启用 Monit Web 界面的命令如下：

```
set http port 2082
allow use 127.0.0.1
allow localhost
allow admin monit
```

第一条命令设置 Web 界面使用 TCP 端口 2082，这是 `monit` 的默认端口号。第二个命令指定 `monit` Web 服务器监听的地址，第三条命令仅接受来自本地机器的 TCP 连接。最后一个命令要求每个 HTTP 连接都使用用户名 (`admin`) 和密码 (`monit`)。以下输出验证了 Monit 连接到端口 2082 (127.0.0.1)，这是正确的配置；结果如下：

```bash
# monit netstat -tupln | grep monit
0 0 127.0.0.1:2082 *:* 671/monit
```

图 5 显示了 Web 界面的截图，整洁且专业。如果你熟悉 HTTP，可以编辑 `/etc/monit.conf` 来使用 HTTP 连接到 Monit Web 服务器。你现在应该会被 Munin 和 Monit 的用处所说服。然而，困难并不在于知道监控的用处，而在于决定使用哪种监控软件（参见相关书籍页面）。

# 监控！现在订阅 http://LinuxForum

Linux Forum Annual 2020

# OpenVPN

### 创建秘密密钥和安全服务器

Dennis Jaredcke 在他的家庭服务器上托管了一个网站，对所有人可见但只有他亲近的朋友知道谁在看……为了防止黑客攻击你的系统并破坏你的生活，保持互联网安全可能变得困难，特别是当你除了少数信任的用户之外隐藏了内容时。这是我们要做的点。我们将向你展示如何从世界上任何地方访问 Web 服务器。

有几种方法可以创建安全连接，但对于两台电脑，使用 OpenVPN 是最可用的解决方案之一，因为它是加密的且具有高度可配置性。运行 `ip addr` 命令将显示你的 ip 地址。OpenVPN 随后会附加 10.8.0.0。Dennis Jaredcke 是一个使用 Linux 自 1990 年起的爱好者。这里是发生什么的总结：

> 快速提示：OpenVPN 的加密使用 BF-CBC，但由于攻击向量的原因，不再推荐使用。最好使用类似 AES-256。

### 虚拟和物理适配器

假设你正在使用 OpenVPN 访问网络而无需他人知晓。这就像运行你的你的脚。发出的数据包在虚拟网络 (`tun0`) 上加密，通过路由表转发到物理适配器 (`eth0`)，然后发送到。来自物理适配器 (`eth0`) 的传入数据包通过 OpenSSL 解密并发送到 Apache 等程序。

下面的图显示了数据如何流：

- 物理 (`eth0`)

- 防火墙 (转发)

- 虚拟 (`tun0`)

- 防火墙 (输入与输出)

- OpenVPN 认证、加密和解密，由 `tun0` 处理。

OpenSSL 是一个用于创建和管理公钥基础设施 (PKI) 的通用密码库。虽然你可能熟悉，但它是 OpenVPN 配置过程中的主要组件。当两个人想要创建私钥和公钥时，交换公钥，同时保持他们的信息使用公钥加密并仅通过匹配的私钥解密。消息可以使用私钥签名并使用公钥验证。这些消息可以使用任何框架加密和解密。公钥通常被称为证书，或 CA。

这种情况通常由证书颁发机构或 CA 引起，CA 是一个个人或组织。CA 的作用是签署其他人的证书。换句话说，CA 增加了额外的验证层。对于 OpenVPN 服务器，当通过 HTTPS 连接 Web 服务器时，服务器发送由 CA 签名的证书到你的浏览器。浏览器将使用 CA 的公证书验证证书。服务器随后使用服务器的公钥加密数据并发送给你。浏览器和网站之间的通信将使用该对称加密。使用 OpenVPN 时，客户端机器将拥有 CA 证书以及公私钥来验证其自身（如下所示）。当客户端连接到 OpenVPN 服务器时，双方交换证书并用 CA 验证。然后，两台电脑将生成密钥，用彼此的数据进行加密并交换。数据随后使用这些密钥加密。
