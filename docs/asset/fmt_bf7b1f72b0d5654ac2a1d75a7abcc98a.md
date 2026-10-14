
在本示例中，`nameserver` 主机名是 `ns.paunchy.net`，`contact-email` 地址是 `paul@paunchy.net`。注意电子邮件中的 `"@"` 部分被替换为 `""`。刷新频率设置为 `7200` 秒，即两小时。因此，`paunchy.net` 的从服务器将拉取主服务器，以检查序列号是否增加。

# NS: 名称服务器

你使用 `NS` 记录来指定负责某个域名的名称服务器。
语法如下：

```
IN NS name-server-hostname.
```

注意，资源记录中的名称和 `TTL` 字段没有指定，因为名称只需要在 `SOA` 记录中使用 `"@"` 字符来指定，而 `TTL` 值也是在 `SOA` 记录中通过最小秒数来指定的。在下文中，该资源记录指定了 `ns.paunchy.net` 是当前区域文件的名称服务器：

```
IN NS ns.paunchy.net.
```

你可以指定多个 `NS` 记录。事实上，你至少应该有两个 `NS` 记录（一个用于主名称服务器，一个用于从名称服务器）。还要注意名称服务器主机名末尾的点。你必须在区域文件中所有完整的主机名之后插入一个点。

# A: 地址

你可以使用 `Address` 记录为特定的主机名指定 `IP` 地址。
你使用 `A` 记录将主机名翻译为 `IP` 地址。其语法如下：

```
hostname IN A IP-address
```

例如：

```
mail.paunchy.net. IN A 192.168.1.250
```

每个主机至少应该有一个 `A` 记录。你也可以对主机名使用快捷方式。例如：

```
mail IN A 192.168.1.250
```

如果区域是 `paunchy.net`，则它与之前的 `A` 记录相同。换句话说，如果你没有指定完整主机名，域名名将附加到短名称之后。因此，`www` 变成了 `www.paunchy.net`。

# PTR: 域名解析指针

域名名称指针记录 `PTR` 用于将 `IP` 地址翻译为主机名。这也被称为反向域名服务。`PTR` 记录的语法如下：

```
IP-address IN PTR hostname.
```

例如：

```
192.168.1.250 IN PTR mail.paunchy.net.
```

在这里，`IP` 地址 `192.168.1.250` 与主机 `www.paunchy.net` 相关。你可以使用如下简短版本：

```
250 IN PTR mail
```

通常，`ISP` 负责网络的主主反向 `DNS`。

# 第 9 章：配置你的域名服务 231

# CNAME: 规范名称

规范名称记录 `CNAME` 为规范或官方主机名指定别名或主机名。语法如下：

```
Alias IN CNAME Canonical-hostname.
```

例如：

```
webserver.paunchy.net IN CNAME www.paunchy.net.
```

在这里，`webserver.paunchy.net` 是 `www.paunchy.net` 的别名。简短版本如下：

```
webserver IN CNAME www
```

注意，当 `webserver.paunchy.net` 需要解析为 `IP` 地址时，将返回 `www.paunchy.net` 的 `IP` 地址。因此，你必须确保为规范主机名至少有一个 `A` 记录。

# MX: 邮件交换

邮件交换记录 `MX` 用于指定设置为域名 `SMTP` 邮件服务器的主机名。语法如下：

```
IN MX preference-value mail-server-hostname.
```

例如：

```
IN MX 0 mail.paunchy.net.
```

只有当你有多个邮件服务器时，优先级数字才有用处。例如：

```
IN MX 10 fast-mail-server.paunchy.net.

IN MX 20 slow-mail-server.paunchy.net.
```

# 第三部分：设置内网/互联网服务

在这里，较低的优先级数字表示较高的优先级。
现在你已经学习了 `DNS` 资源记录的基础知识，你准备好创建主、从和仅缓存 `DNS` 服务器了。

## 主 DNS 服务器

让我们在 `ns.paunchy.net` 服务器上为 `paunchy.net` 域设置 `DNS` 服务器。回想列表 9-2 中的以下语句：

```
zone "paunchy.net" (

  type master;

  file "classifiedpaunchy.zone";

);
```

上面的示例表示该名称服务器是 `paunchy.net` 域的主名称服务器。接下来，在名称服务器的工作目录 `/var/named` 中创建一个名为 `paunchy.zone` 的区域文件。列表 9-3 是 `paunchy.net` 域的此类区域文件示例。

列表 9-3：`classifiedpaunchy.com` 域的区域文件

| IN SOA paunchy.net. root.paunchy.net. |
| :--- |
| 199609206 : serial |
| 28800 : refresh |
| 7200 : retry |
| 604800 : expire |
| 86400 : default_ttl |
| IN NS ns.paunchy.net. |
| IN MX 10 mail.paunchy.net. |
| veracruz IN A 192.168.1.250 |
| ns IN CNAME veracruzy |
| mail IN CNAME veracruzy |
| atlas IN A 192.168.1.254 |
| chivas IN A 192.168.1.100 |
| tigers IN A 192.168.1.101 |
| atlante IN A 192.168.1.240 |

`SOA` 和 `NS` 记录指向 `paunchy.net` 域的 `ns.paunchy.net`。因为我们希望在 `mail.paunchy.net` 上接收邮件，设置了一个 `MX` 记录来实现。别名 `www.paunchy.net` 指向 `www`。最后，若干 `A` 记录指向其他计算机和打印机。

# 配置你的域名服务

如你所见，使用各种资源记录可以按照你需要配置区域文件。一旦区域文件存储在 `DNS` 服务器的工作目录中，域的主服务器配置就完成了。

## 从 DNS 服务器

配置从 `DNS` 服务器非常简单。你只需要修改的文件是 `/etc/named.conf`。例如，你可能想使用 `DNS` 服务器 `ns2.paunchy.net` 作为 `paunchy.net` 域的从名称服务器。第一步是在 `ns2.paunchy.net` 的 `/etc/named.conf` 中创建如下区域语句：

```
zone "paunchy.net" {

  type slave;

  file "classifiedpaunchy.zone";

}
```

由于这是一个从服务器或从服务器，你可以使用名为 `named-xfer` 的程序从 `paunchy.net` 主服务器获取该文件。因为 `paunchy.net` 域的主名称服务器是 `ns.paunchy.net`，你可以这样运行 `named-xfer`：

```
named-xfer -z paunchy.net -f classifiedpaunchy.zone -s ns.paunchy.net
```

在这里，`-z` 选项用于指定区域名称，`-f` 选项用于指定区域文件，`-s` 选项用于指定信息所在的名称服务器。一旦运行 `named-xfer`，当前目录将创建一个 `classifiedpaunchy.zone` 文件。一旦该文件移动到 `ns2.paunchy.net` `DNS` 服务器的工作目录中，`paunchy.net` 域的从配置就完成了。

### 反向 DNS 服务器

你可以为你的网络创建反向 `DNS`。例如，对于 `192.168.1.0` 网络，你可以如下设置反向区域。首先，修改 `/etc/named.conf` 以包含一个新的区域：

```
zone "192.168.1.in-addr.arpa" {

  type master;

  file "192.168.1.zone";

}
```
