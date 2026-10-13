
Puppet 配置可能会变得非常复杂。一旦设置好，它将完全管理你所有网络系统的配置更改。有关详细的文档和指南，请参考以下内容。这些信息并非专门针对 RHEL6。

`http://docs.puppetlabs.com/`

Puppet 配置位于 `/etc/puppet` 文件夹。Puppet 对资源的操作在位于 `/etc/puppet/manifests` 文件夹的清单文件（manifest）中指定。你可以将 Puppet 的工作想象成数据库，它为资源的字段指定值。Puppet 文档中引用的一个简单示例是你想要为密码文件设置的权限。

```
file '/etc/passwd':
  owner => root,
  group => root,
  mode => 644,
```

定义资源（在本例中为 `file`），然后是资源标题，对于文件来说，标题通常是完整名称（`/etc/passwd`）。对于服务，它可以是服务器守护进程的，如 `vsftpd`。然后为文件、所有者、组和模式指定属性。

你还可以使用类（classes）和定义（definition）将资源收集到聚合中。类定义在 `/etc/puppet/manifest/classes` 文件夹中。例如

在 RHEL6 上，客户端使用 `puppet`（`puppet` 包），服务器使用 `puppetmaster` 守护进程（`puppet-server` 包）。

在客户端上，请确保使用 `system-config-services`（系统 | 管理 | 服务）或 `chconfig` 启用 `puppet` 服务。使用 `service` 命令手动启动和停止。对于服务器，启用 `puppetmaster`。

在防火墙上为 Puppet 端口 `8140` 添加访问。你可以使用 `system-config-firewall`（系统 | 管理 | 防火墙），并在“其他端口”选项卡上点击“添加”按钮添加端口并输入端口 `8140`。服务器使用端口 `8141` 到 `8144`。

在 SELinux 上，确保启用 puppet 客户端访问（系统 | 管理 | SELinux 管理，布尔值选项卡，puppet 条目）。

`puppet` 运行时配置在 `/etc/sysconfig/puppet` 文件中。你在这里指定 puppet 服务器主机、使用的端口和日志文件。默认条目被注释掉了。

客户端必须知道 puppet 服务器所在的主机。对于小型网络，你可以通过设置 `/etc/sysconfig/puppet` 文件中的 `PUPPET_SERVER` 变量来手动完成。

```
PUPPET_SERVER=myserver
```

如果你的网络运行着 DNS 服务器，你可以为 puppet 服务器设置 CNAME puppet 条目。客户端随后可以使用 CNAME 定位 puppet 服务器。

```
puppet IN CNAME turtle.mytrek.com
```

你还可以在每个客户端的 `/etc/host` 文件中为 puppet 服务器添加主机条目。`/etc/sysconfig/puppetmaster` 文件中的 `puppetmaster` 配置允许你设置端口条目和日志服务。默认条目被注释。移除注释字符 `#` 即可启用。

当你首次设置客户端-服务器 puppet 连接时，客户端和服务器必须签署客户端的 SSL 证书。首先在客户端上运行 `puppet`。

# 第 8 章：系统管理访问与配置

## 第 9 章：系统工具与监控 257

![](img/99301381a0d2790a6cdc2798147cbdad_258_0.png)

图 9-1：GNOME 日志查看

`rsyslog` 中的条目由两个字段组成：选择器（selector）和动作（action）（`rsyslog` 使用旧的 `syslog` 以保持兼容性）。选择器是要记录日志的服务类型，例如邮件或新闻，动作是消息存放的位置。动作通常是一个日志文件，但也可以是远程主机或指向另一个程序的管道。服务的类型被称为设施（facility）。`rsyslog` 守护进程使用了几个特定术语来指定某些类型的服务（见表 9-1）。设施可以通过优先级（priority）进一步限定，优先级指定了生成的消息类型。`rsyslog` 使用了几个指定的特定术语来表示不同的优先级。选择器由设施和优先级组成，中间用句点隔开。例如，为了保存邮件系统生成的错误消息，你使用一个由 `mail` 设施和 `err` 优先级组成的选择器，如下所示：

`mail.err`

将这些消息保存到 `/var/log/mailillog` 文件，你需要指定该文件为动作，得到如下条目：

```
mail.err */var/log/mailillog
```

`rsyslog` 守护进程还支持使用 `*` 作为匹配字符，用于匹配扇区中的所有设施或所有优先级：`cron`。`.*` 会匹配所有 `cron` 消息，无论优先级如何。`*.err` 会匹配所有设施的错误消息，而 `.*` 会匹配所有消息。以下示例将所有邮件消息保存到 `/var/log/mailillog` 文件，并将所有关键消息保存到 `/var/log/mycritical` 文件：

```
mail.* *.crit /var/log/mycritical
```

258 第 3 部分：管理说明

| 设施 (Facilities) |or |

| --- | --- |

| auth-priv | 安全/授权消息（私有） |

| cron | 时钟守护进程（cron 和 at）消息 |

| daemon | 其他系统守护进程消息 |

| kern | 内核消息 |

| lpr | 线路打印机子系统消息 |

| mail | 邮件子系统消息 |

| news | Usenet 新闻子系统消息 |

| syslog | syslog 内部消息 |

| user | 通用用户级消息 |

| uucp | UUCP 子系统消息 |

| local0 到 local7 | 留作本地使用 |

| 优先级 (priorities) | 说明 |

| debug | 7, 调试消息，优先级最低 |

| info | 6, 信息性消息 |

| notice | 5, 通知，正常但重要的状态 |

| warning | 4, 警告 |

| err | 3, 错误消息 |

| crit | 2, 关键状态 |

| alert | 1, 警报，必须立即采取行动 |

| emerg | 0, 紧急消息，系统无法使用 |

| 操纵符 (Operators) | 说明 |

| * | 匹配扇区中的所有设施或优先级 |

| = | 限制为指定的优先级 |

| ! | 排除指定的优先级及更高优先级 |

| / | 用于保存消息的文件 |

| @ | 用于发送消息的主机 |

| | | 用于发送消息的 FIFO 管道 |

表 9-1：rsyslog 设施、优先级和操纵符

### 优先级

当你为设施指定优先级时，所有优先级更高的消息也会被包含在内。`err` 优先级包含了 `crit`、`alert` 和 `emerg` 优先级。如果你只想选择特定优先级的消息，可以使用 `=` 运算符对优先级进行限定。例如，`mail=.err` 将仅选择错误消息，而不包含 `crit`、`alert` 或 `emerg` 消息。你也可以用 `!` 运算符限制优先级。`crit` 将排除指定优先级及更高优先级的消息。例如，`mail.crit` 将排除该消息以及更高优先级的 `alert` 和 `emerg` 消息。要专门排除整个设施的消息，你需使用 `none` 优先级；例如，`mail.none` 排除所有消息。这通常用于在同一个条目中定义多个扇区时。

你可以通过逗号分隔，在给定的扇区中列出多个优先级或设施。你还可以通过分号分隔，在同一个条目中设置多个扇区。第一个示例向 `/var/log/messages` 文件保存 `info` 优先级的消息，排除了所有邮件和认证消息（authpriv）。第二个示例向 `uucp` 和 `/var/log/spool` 保存所有 `crit` 及更高优先级的消息：

```
* info.mail.none;news.none;authpriv.none /var/log/messages
uucp,news.crit /var/log/spool
```

### 动作与用户

在动作字段中，你可以指定文件、远程系统、用户或管道。文件的动作条目必须以 `/` 开头并指定其全路径，例如 `/var/log/messages`。要将消息发送到远程主机，你通过 `@` 符号指定主机名。以下示例将所有内核消息保存到 `rabbit.trek.com`：

```
* @rabbit.trek.com
```

要将消息发送给用户，列出他们的登录名。以下示例将关键新闻消息发送到用户 `chris` 和 `aleina` 的控制台：

```
news.=crit aleina
```

你还将消息输出到命名文件（FIFO）。动作的管道条目以 `|` 开头。以下示例将内核消息管道到 `adm/debug`：

```
* |adm/debug
```

### rsyslog.conf 示例
