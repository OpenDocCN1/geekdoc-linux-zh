

Postfix 将电子邮件消息投递到用户账户后，用户可以通过查看目标地址来判断该消息属于哪个类别。或者，用户可以使用 procmail 程序（参见本章后面关于 procmail 的部分）根据目标地址中出现的扩展文本将消息重定向到单独的邮件文件夹。这是一种为特殊场合创建额外邮件账户的好方法。

## IPv4 和 IPv6

Postfix 配置中的最后一个向导窗口允许您选择在 Postfix 配置中激活哪些 Internet 协议。选项有

- all：同时支持 IPv4 和 IPv6 地址。
- ipv6：仅支持 IPv6 地址。
- ipv4：仅支持 IPv4 地址。

Ubuntu 服务器和 Postfix 软件都支持使用 IP 版本 4（IPv4）格式和更新的 IP 版本 6（IPv6）格式。此选项允许您将 Postfix 限制为仅使用其中一种格式，或在配置中允许两种格式。

IPv6 地址使用 128 位值来表示网络和主机地址。通常，该地址表示为八组四位十六进制值的序列：

```
xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx
```

每组之间用冒号分隔。然而，尝试使用此格式可能会变得繁琐，因此在指定 IPv6 地址时允许使用一些快捷方式：

- 省略四位数字组内的前导零：
  2030:0:0:0:30:4c45:0:100
- 用双冒号替换包含全零的组：
  2030::30:4c45:0:100

此设置取决于您在网络上引用网络和主机地址的方式。如果您的网络仅支持 IPv4 样式地址，您可以将此设置为 ipv4。但是，如果您在不久的将来需要支持 IPv6 地址，将其设置为 all 也无妨。

## 修改配置设置

尽管 Ubuntu 安装向导会引导您完成电子邮件服务器环境并自动配置 Postfix，但您可能希望在服务器上自定义一些内容。您可以使用 postconf 程序来完成此操作，而无需触及 main.cf 配置文件。

postconf 程序的格式为

```
postconf [options] parameter = value
```

要查看参数的现有值，只需输入参数名称而不设置值即可：

```
rich@testbox:/etc$ postconf myorigin
myorigin = /etc/mailname
rich@testbox:/etc$ cat /etc/mailname
testbox.localdomain
rich@testbox:/etc$
```

这表明 `myorigin` 参数设置为 `/etc/mailname` 文件的内容。这使您可以在 `main.cf` 配置文件之外定义用于外发电子邮件消息的源地址。您可以使用 `cat` 命令显示 `/etc/mailname` 文件的内容，其中显示了服务器使用的主机名。

## procmail

procmail 程序充当中间件，在邮件从服务器传输到写入邮箱之前过滤每个用户的邮件。procmail 程序功能极其强大。您可以配置 Postfix MTA 直接将所有传入消息发送给 procmail 以进行本地投递，或允许单个邮件用户自定义其邮件环境以使用 procmail。

一旦您决定将所有消息发送给 procmail，单个用户就可以通过在其主文件夹中创建 `.procmailrc` 文件来利用 procmail 的强大功能，以指示 procmail 如何处理传入的邮件消息。

### .procmailrc 文件

`.procmailrc` 文件定义了 procmail 根据文件中定义的配方如何投递邮件。每个 procmail 配方定义一个匹配表达式值和当消息匹配该表达式时 procmail 应采取的操作。procmail 配方的格式为

```
recipe header line
condition line(s)
action line
```

配方头行定义了配方的基本操作。所有配方行都以以下标题开头

```
:0[flags]: locallockfile
```

`flags` 标识配方将执行的基本功能。表 23-5 列出了可用的标志。

| Flag | Description |
|---|---|
| A | 除非满足所有前一个配方的条件，否则不执行该配方 |
| a | 除非满足紧邻前一个配方的条件，否则不执行该配方 |
| B | 搜索消息正文 |
| b | 将消息正文馈送到目标位置（默认值） |
| c | 生成此消息的副本 |
| D | 区分大小写（默认情况下忽略大小写） |
| E | 除非所有前一个配方的条件均未满足，否则不执行该配方 |
| e | 除非紧邻前一个配方失败，否则不执行该配方 |

