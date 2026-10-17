
## Finger 查询
`Finger` 查询是一个客户端守护程序模块，它向接受并处理 `Finger` 请求的 `finger-d`（`Finger` 守护程序）进行查询。如果可以 `Finger` 某个账户，检查该账户将返回预设信息，例如账户持有人的真实姓名、其最近登录该账户的时间，有时还有更多。通常，`.edu`、`.net` 和 `.org` 账户使用可以被查询的 `Finger` 服务器守护程序。然而，某些账户由于主机系统安全或操作策略的原因，不使用 `Finger` 服务器守护程序。由于标准 `Finger` 守护程序会乐意查找类似匹配项，`Finger` 守护程序已成为 `NIS` `DoS` 攻击的流行目标。

## DNS 查询（图 12.18）
`DNS` 主要用于在域名与其 `IP` 地址之间进行转换，并控制 `Internet` 电子邮件传递、`HTTP` 请求和域转发。`DNS` 目录服务由 `DNS` 数据、`DNS` 服务器以及从服务器获取数据的 `Internet` 协议组成。`DNS` 目录中的记录被分割到称为区域（`zones`）的文件中。区域保存在分布在整个 `Internet` 上的权威服务器上，这些服务器根据 `DNS` 网络协议回答查询。此外，大多数服务器是某些区域的权威服务器，并针对所有其他 `DNS` 信息执行缓存功能。此模块执行 `DNS` 查询，目的是获取不可或缺的发现信息；这通常是黑客行动过程中的第一步。`DNS` 资源记录类型包括：

![](img/ba85bb40c695c02adae8cbd6666f2e0c_684_0.png)

**图 12.18** `DNS` 查询模块。

- `A`：地址。定义于 `RFC 1035`。
- `AAAA`：`IPv6` 地址。定义于 `RFC 1886`。
- `AFSDB`：`AFS` 数据库位置。定义于 `RFC 1183`。
- `CNAME`：规范名称。定义于 `RFC 1035`。
- `GPOS`：地理位置。定义于 `RFC 1712`。已废弃。
- `HINFO`：主机信息。定义于 `RFC 1035`。
- `ISDN`。定义于 `RFC 1183`。
- `KEY`：公钥。定义于 `RFC 2065`。
- `KX`：密钥交换器。定义于 `RFC 2230`。
- `LOC`：位置。定义于 `RFC 1876`。
- `MB`：邮箱。定义于 `RFC 1035`。
- `MD`：邮件目的地。定义于 `RFC 1035`。已废弃。
- `MF`：邮件转发器。定义于 `RFC 1035`。已废弃。
- `MG`：邮件组成员。定义于 `RFC 1035`。
- `MINFO`：邮箱或邮件列表信息。定义于 `RFC 1035`。
- `MR`：邮件重命名域名。定义于 `RFC 1035`。
- `MX`：邮件交换器。定义于 `RFC 1035`。
- `NS`：名称服务器。定义于 `RFC 1035`。
- `NSAP`：网络服务访问点地址。定义于 `RFC 1348`。在 `RFC 1637` 和 `RFC 1706` 中重新定义。
- `NSAP-PTR`：网络服务访问协议。定义于 `RFC 1348`。已废弃。
- `NULL`。定义于 `RFC 1035`。
- `NXT`：下一个。定义于 `RFC 2065`。
- `PTR`：指针。定义于 `RFC 1035`。
- `PX`：指向 `X.400/RFC822` 信息的指针。定义于 `RFC 1664`。
- `RP`：负责人。定义于 `RFC 1183`。
- `RT`：经由路由。定义于 `RFC 1183`。
- `SIG`：加密签名。定义于 `RFC 2065`。
- `SOA`：授权开始。定义于 `RFC 1035`。
- `SRV`：服务器。定义于 `RFC 2052`。
- `TXT`：文本。定义于 `RFC 1035`。
- `WK5`：知名服务。定义于 `RFC 1035`。
- `X25`。定义于 `RFC 1183`。

针对最流行的 `Internet` 搜索引擎之一 `Yahoo` (`http://www.yahoo.com`) 的 `DNS` 查询请求示例将显示：

```text
-->HEADER<!-- opcode: QUERY, status: NOERROR, id: 13700
;; flags: qr rd ra; QUERY: 1, ANSWER: 7, AUTHORITY: 3, ADDITIONAL: 19
;; yahoo.com, type = ANY, class = IN
yahoo.com.        12h44m31s IN NS  NS3.EUROPE.yahoo.com.
yahoo.com.        12h44m31s IN NS  NS1.yahoo.com.
yahoo.com.        12h44m31s IN NS  NS5.DCX.yahoo.com.
yahoo.com.        23m3s IN A    204.71.200.243
yahoo.com.        23m3s IN A    204.71.200.245
yahoo.com.        3m4s IN MX    1 mx2.mail.yahoo.com.
yahoo.com.        3m4s IN MX    0 mx1.mail.yahoo.com.
yahoo.com.        12h44m31s IN NS  NS3.EUROPE.yahoo.com.
yahoo.com. 12h44m31s IN NS NS1.yahoo.com.
 yahoo.com. 12h44m31s IN NS NS5.DCX.yahoo.com.
 NS3.EUROPE.yahoo.com. 1h13m23s IN A 194.237.108.51
 NS1.yahoo.com. 7h18m19s IN A 204.71.200.33
 NS5.DCX.yahoo.com. 1d2h46m6s IN A 216.32.74.10
 mx2.mail.yahoo.com. 4m4s IN A 128.11.23.250
 mx2.mail.yahoo.com. 4m4s IN A 128.11.68.213
 mx2.mail.yahoo.com. 4m4s IN A 128.11.68.139
 mx2.mail.yahoo.com. 4m4s IN A 128.11.68.144
 mx2.mail.yahoo.com. 4m4s IN A 128.11.23.244
 mx2.mail.yahoo.com. 4m4s IN A 128.11.23.241
 mx2.mail.yahoo.com. 4m4s IN A 128.11.68.146
 mx2.mail.yahoo.com. 4m4s IN A 128.11.68.158
 mx1.mail.yahoo.com. 4m4s IN A 128.11.68.218
 mx1.mail.yahoo.com. 4m4s IN A 128.11.68.221
 mx1.mail.yahoo.com. 4m4s IN A 128.11.23.238
 mx1.mail.yahoo.com. 4m4s IN A 128.11.68.223
 mx1.mail.yahoo.com. 4m4s IN A 128.11.68.100
 mx1.mail.yahoo.com. 4m4s IN A 128.11.23.198
 mx1.mail.yahoo.com. 4m4s IN A 128.11.23.250
 mx1.mail.yahoo.com. 4m4s IN A 128.11.23.224
```

## IP/主机名查找器
该模块非常简单，用于查询 `Internet` 上的主要 `IP` 地址（给定主机名）或反之亦然。此模块的特定用法是在发现阶段快速确定网络的主要地址或主机名。只需输入主机名，例如 `www.yahoo.com`，然后单击“获取 `IP` 地址”，如图 12.19 所示。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_686_0.png)

**图 12.19** `IP/主机名` 查找器模块。

## NS 查找
该模块是上述 `IP/主机名` 查找器的一个高级分支，因为它会搜索与单个主机名相关的多个次要地址，如图 12.20 所示。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_687_0.png)

**图 12.20** `NS` 查找模块。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_687_1.png)

**图 12.21** 使用 `TigerSuite` 进行路由跟踪。
