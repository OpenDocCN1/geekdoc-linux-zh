
| : 为 dekiru.gr.jp 定义名称 | | | |

| router | IN | 210.24.12.98 | | |

| server | IN | MX 10 | server | |

| server | IN | 210.24.12.98 | | |

| server | IN | MX 10 | server | |

| | IN | CNAME | |

|---|---|---|---|

| : 服务别名 | | | |

| ns | IN | CNAME | server |

| smtp | IN | CNAME | server |

| pop | IN | CNAME | server |

| imap | IN | CNAME | server |

| ftp | IN | CNAME | server |

| www | IN | CNAME | server |

| proxy | IN | CNAME | server |

如果使用 `CNAME`，可以为同一个 IP 地址定义多个主机名。

# 创建 DNS 服务器，第 4 部分

## 配置正向查找

在文件中写入 `SOA`、`NS`、`A`、`MX` 和 `CNAME` 等记录。当你想添加新主机名、更改次级服务器地址或设置别名时，需要修改正向查找数据。当你修改此文件时，始终增加 `SOA` 记录的序列号。如果不增加序列号，更改可能长期不会生效。

### 设置域名

不要忘记末尾的句号

`DNS` 服务器配置文件中，所有没有末尾句号 `.` 的主机名都被视为省略了域名部分。这是 `BIND` 配置文件中经常出现的错误之一。一次更改一个字符，以免出错。

对于序列号，使用修改日期和修订次数的组合。

- 输入附加域名的 `postmaster`。确保添加末尾句号。
- 输入服务器主机。确保添加末尾句号。
- 修改序列号。

```
server.dekiru.gr.jp. postmaster.dekiru.gr.jp.
- 序列 (yyyy/mm/dd)
- 1 小时后刷新
- 30 分钟后重试
- 1 周后过期
- 2 小时的最小 TTL
```

注意：通常邮件地址中包含 `(@)`。在这里，它被替换为 `DNS` 配置文件的句号 `.`。

| template -- Dekiru Linux. |

| IN SOA ns |

| 1999070701 |

| 3600 ns-tk022.ocn.ad.jp. |

| 1800 MX |

| 604800 server |

| 7200 ) |

| localhost A 127.0.0.1 |

- 输入次级 `DNS` 服务器。确保添加末尾句号。
- 输入你从 `InterNIC` 获取域名时使用的主 `DNS` 服务器主机名。此处可以省略域名部分。

注意：`vi` 编辑器命令请参见第95页。

> 注意这是一个必须提供给 `ISP` 的相同主机名。

### 指定正向查找设置

`MX` 记录指示传入邮件的目的地

设置主机名和 IP 地址。

`MX` 记录用于查找发送到该域名时作为目的地的邮件服务器。为整个域名和每个主机设置 `MX` 记录。`CNAME` 记录中定义的别名不能用于 `MX` 记录中的主机名。同样，不能为 `CNAME` 记录中定义的别名定义 `MX` 记录。

- 输入为路由器设置的 IP 地址。

为 `dekiru.gr.jp` 定义名称。

| | | | |

|---|---|---|---|

| router | A | 210.48.12.97 | |

| | MX 10 | server | |

| server | A | 210.48.12.98 | |

| | MX 10 | server | |

- 输入服务器的主机名。可以省略域名部分。
- 输入服务器的主机名。可以省略域名部分。
- 输入服务器的 IP 地址。

### 设置主机别名

由于使用了通用别名，因此不需要特定的地址。

- 输入服务器的主机名。可以省略域名部分。

| | | |

|---|---|---|

| ns | CNAME | server |

| smtp | CNAME | server |

| pop | CNAME | server |

| imap | CNAME | server |

| ftp | CNAME | server |

| www | CNAME | server |

| proxy | CNAME | server |

为每个服务定义一个主机别名。

- 保存文件并退出。

### 使用 CNAME 将多个主机名关联到一个 IP 地址

`CNAME` 记录定义了一个主机别名。如果你使用 `CNAME`，可以为同一个 IP 地址定义多个主机名，例如为 `server.dekiru.gr.jp` 的 IP 地址定义 `dekiru.gr.jp` 或 `www.dekiru.gr.jp`。

# 创建 DNS 服务器，第 5 部分

## 配置反向查找信息

在配置文件中编写反向查找信息的 `SOA`、`NS` 和 `PTR` 记录。当你添加使用新 IP 地址的设备时，确保在修改正向查找数据时也能执行反向查找。

当你修改此文件时，请务必增加 `SOA` 记录的序列号 `serial number`。由于正向和反向查找的序列号是独立的，此数字不需要与正向查找配置文件 `SOA` 记录的序列号匹配。

### 修改反向查找配置文件

打开反向查找配置文件

注意：`vi` 文本编辑器命令请参阅第 95 页。

- 输入命令。

```
root@server namedb# vigr dekiru.gr.jp
```

> 警告：如果你在指定配置文件内容时出错，`DNS` 服务器将无法正常运行。请务必一个字符一个字符修改，以防出错。

修改此配置文件以匹配你的环境。

对于序列号，请使用文件修改日期和当天修订次数的组合。

- 输入服务器主机名。请务必添加最后的句号。
- 输入带有域名的 `master` 名称。请务必添加最后的句号。
- 修改序列号。

```
template.rev -- Dekiru Linux. July 1999
```

| IN SOA server.dekiru.gr.jp master.dekiru.gr.jp. |

| :--- |

| 599070701 : (yyyy/mm/dd/nn) |

| 3600 : 1 小时后刷新 |

| 1800 : 30 分钟后重试 |

| 604800 : 1 周后过期 |

| 7200 ) : 2 小时最小 TTL |

- 输入服务器主机名。请务必添加最后的句号。

| IN NS ns.dekiru.gr.ad.jp. |

| IN NS ns-tk022.ocn.ad.jp. |

- 输入辅助 `DNS` 服务器的主机。请务必添加最后的句号。

### 指定反向查找设置

- 输入 IP 地址的最后数字。例如，如果 IP 地址是 `210.248.12.97`，则输入 `97`。
- 输入与 IP 地址对应的主机名。请务必添加最后的句号。
- 保存文件并退出。

```
:: 为 dekiru.gr.jp. 定义地址。
97 IN PTR router.dekiru.gr.jp.
98 IN PTR server.dekiru.gr.jp.
```

`PTR` 指针

这是用于执行反向查找的信息。编写从 IP 地址查找主机名的数据。由于区域名称与域名不同，你必须编写主机名，且不能省略最后的句号 `.`。

### 重新加载 BIND

配置完成。重新运行 `BIND`。

输入命令。

> 注意：`ndc` 命令用于指定 `BIND` 的停止、启动或重启、读取配置文件等。

```
[root@server namedb# ndc reload
[root@server namedb# -
```

# 提示

## 配置完成后报告配置

在完成 `DNS` 服务器的配置并启动后，请通知你的 `ISP`。

- 记录列表
- 与域名本身相关的 `SOA` 信息
- `NS DNS` 服务器信息
- 正向查找信息
- `MX` 邮件服务器信息
- `CNAME` 主机别名
- `PTR` 反向查找信息

# 测试 DNS 服务器，第 1 部分

### nslookup 实用

`nslookup` 工具可用于测试你的 `DNS` 服务器。你可以使用 `nslookup` 向 `DNS` 服务器发送请求。本节使用 `nslookup` 命令来确认 `DNS` 服务器配置。如果 `DNS` 服务器配置无效，请检查配置文件。大多数配置失败都是由于简单的输入错误，例如忘记添加最后的句号。

## 从主机名查询 IP 地址

| 验证是否可以从主机名查询 IP 地址 | 输入命令。 | 验证是否可以查询你创建的 DNS 的 IP 地址或主机名 | 请务必在你要查询的主机名添加最后的句号。 |

| :--- | :--- | :--- | :--- |

```
[root@server namedb# nslookup.dekiru.gr.jp]
```
