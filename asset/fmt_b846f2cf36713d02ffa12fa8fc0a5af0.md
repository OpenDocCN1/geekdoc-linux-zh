
此命令读取名为 `/etc/mail/access` 的文本文件并使用它们构建 `/etc/mail/access.db` 哈希数据库。本地主机名、域名文件以及访问数据库可能是 Sendmail 中配置的最重要的数据库。另外还有两个，虚拟数据库是最有用的。默认情况下，只有当邮件来自指定网络时才会采取动作。

内容也意味着...

`VIRTUSER_DOMAIN_FILE('/etc/mail/virtual-domains')`

在宏配置文件中添加 `VIRTUSER_DOMAIN` 命令后，重新运行 `m4` 以构建新的 `sendmail.cf` 文件。然后，将列表 6.9 中的虚拟域名添加到新的 `virtual-domains` 文件中，每行一个域名，如下所示：

```
[craig]$ cat /etc/mail/virtual-domains
bridal-gowns.com
patient-rights.com
imaginary.com
```

每当向文件中添加新的虚拟域名时，向 Sendmail 发送 `SIGHUP` 信号，以确保它读取新值并将它们加载到类（`VirthHost`）中。

> **提示**：`VIRTUSER_DOMAIN` 和 `VIRTUSER_DOMAIN_FILE` 宏都需要修改并重新构建示例配置。由于我们已经在配置中拥有了 `local-host-names` 文件，将虚拟域名添加到该文件中会更简单。这种方法同样有效，因为 Sendmail 在处理虚拟域名时会同时检查 `w` 和类（`VirthHost`）。

## 定义 virtetable 投递地址

列表 6.9 中三个示例条目的投递地址都是简单的电子邮件地址。它不需要是输入地址，也不是 Sendmail 返回给发送者的错误消息。列表 6.10 显示了一个更大的 `virtetable`，其投递地址字段包含多种不同的值。

### 列表 6.10 示例 virtetable

```
sales@bridal-gowns.com  jill
info@patient-rights.org  sara@hawk.foobirds.org
@imaginary.com  david@lion.mammals
sales@outbusiness.com  error:user address is not valid
sales@webroke.com  error:5.1.5 Destination address invalid
@other.org  %1@local.org
+*@thatplace.com  %2@newplace.com
```

前三个条目已经解释过了。带有虚拟域名地址的邮件路由到真实的电子邮件地址时会被接受。第二个字段中的电子邮件地址必须是真实地址；不能是另一个虚拟域名地址。例如，以下 `virtuosable` 条目的作用可能不像你想象的那样：

```
sales@bridal-gowns.com sales@imaginary.com
@imaginary.com david@lion.mammals.org
```

这不能用于将发给 `sales@bridal-gowns.com` 的邮件转发到 `david@lion.mammals.com`。与可以指向其他别名的别名不同，虚拟域名不能指向其他虚拟域名。

列表 6.10 中的接两行说明了错误消息的使用。发给 `sales@outofbusiness.com` 的邮件不会被投递。相反，向发送者返回一条错误消息“User address is not valid”。发送到 `sales@webroker.com` 的邮件会向发送者返回错误消息“Destination invalid”。

错误消息必须以错误代码开头，错误代码是内置在 Sendmail 中的一个特殊邮件的名称。与错误代码用冒号隔开的是错误条件，该条件可以指定为关键字或 DSN 代码。DSN 代码可以是 RFC 1893 中定义的任何有效代码。错误条件关键字必须是错误邮件识别的关键字。有效错误条件关键字列表可以在第 8 章“理解重写规则”中关于错误邮件的讨论中找到。

> **提示**：DSN 代码是互联网标准，在 RFC 中有明确定义。对 Sendmail 的更改在未来的发布中可能会发生变化。

列表 6.10 中的两行提供了如何将输入地址中的值用于输出地址的示例。`@other.org` 实体提供了类的示例。输入地址的用户名部分通过 `%` 变量传递，因此输出地址中的 `%` 就会被来自输入地址的用户名替换。使用列表 6.10 所示的 `virtuunable`，发给 `pat@other.org` 的邮件将投递到 `pat@local.org`，发送到 `doris@other.org` 的邮件将转发到 `doris@local.org`。

这是一个非常强大的功能。显然，它可以用于在更改域名时缓解过渡，但这种情况非常罕见。更重要的是，当你销售的产品与你的官方域名没有明确关联性时，可以使用此功能。假设你有一个销售派对产品的在线商城。你的域名真实名称是 `stuffycorporation.com`，但你还拥有 `funstuff.com` 和 `happythings.com` 域名。`virtuertable` 中的以下两行无论邮件发往哪个域名，都会将邮件路由到正确的员工：

```
@funstuff.com               %1stuffycorporation.com
@happythings.com         %1stuffycorporation.com
```

列表 6.10 的最后一行显示，`+detail` 语法中的 `+detail` 值可以传递到输出地址，例如发送到 `sales+info@thatplace.com` 的邮件将投递到 `info@newplace.com`，发送到 `sales+orders@thatplace.com` 的 `+detail` 邮件将投递到 `orders@newplace.com`。注意，使用 `+detail` 语法必须在 `virtuertable` 的第一个字段通过在虚拟地址域名之前放置 `+` 来指示。仅使用电子邮件地址即可，无需使用 `+detail` 语法。出于这个原因，除非你有一个自动为用户生成这种语法的程序，否则这种语法很少使用。为了完整性，在这里介绍了它，但你可能不会在配置中用到它。

在 Sendmail 使用 `virtetable` 之前，必须使用 `makedmap` 将其转换为数据库。列表 6.11 显示了 `virtetable` 数据库的成功构建和测试。

## 列表 6.11 构建和测试 virtetable

```
[root]# cat local-host-names
## include all aliases for your machine.
/etc/mail/virtual-domains
bridal-gowns.com
patient-rights.org
imaginary.com
outofbusiness.com
werbroke.com
other.org
thatplace.com
```

## 第 6 章 使用 Sendmail 数据库

```
[root]# cat local-host-names
## include all aliases for your machine.
/etc/mail/virtual-domains
bridal-gowns.com
patient-rights.org
imaginary.com
outofbusiness.com
werbroke.com
other.org
thatplace.com
[root]# cat virtetable
sales@bridal-gowns.com  jill
info@patient-rights.org  sara@hawk.foobirds.org
@imaginary.com  david@lion.mammals
sales@outbusiness.com  error:user address is not valid
sales@webroke.com  error:5.1.5 Destination address invalid
@other.org  %1@local.org
+*@thatplace.com  %2@newplace.com
```
