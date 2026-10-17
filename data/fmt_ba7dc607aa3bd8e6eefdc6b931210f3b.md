
```
$signed_header_fields{'received'} = 0;
$signed_header_fields{'sender'} = 1;
$signed_header_fields{'to'} = 1;
$signed_header_fields{'cc'} = 1;
```

### sendmail 中的 DKIM

你可以通过使用 `milters`（用于内联过滤；参见第 767 页）或与 `amavisd` 结合的双服务器设置来实现 `sendmail` 的 DKIM。在此，我们介绍使用 `DKIM-milter` 来签名和验证消息。

`sendmail` 的配置原语 `masquerade_as` 和 `generictable` 会重写头部，因此这些原语必须在添加任何 DKIM 签名之前实现；否则，签名将不再有效。

要支持 DKIM，`sendmail` 必须使用 `milter` 支持构建，具有 `OpenSSL` 和 `Berkeley DB` 库可用，并且已安装 `DKIM-milter` 包（在 `sourceforge.net` 上找到）。使用 `OpenSSL` 生成密钥，并按第 591 页所述将其添加到你的 DNS 区域，或使用第 846 页所示的 `dkim-genkey`。

在此示例中，我们的域名是 `example.com`。我们选择了选择器 “email” 并将私钥存储在 `email.private` 中，将公钥存储在 `email.key.pem` 中。我们可以用 `dkim-testkey` 测试密钥，如下所示：

```
$ dkim-testkey -d example.com -k /var/db/dkim/email.key.pem -s email
```

如果一切正常，`dkim-testkey` 不会输出任何内容。

在你的 `sendmail` 配置文件 `sendmail.mc` 中，添加以下行

```
INPUT_MAIL_FILTER(`dkim-filter', `S=inet:8891@localhost')
```

然后重建 `sendmail.cf` 文件（`./Build sendmail.cf; sudo make install-cf`）。然后重启 `sendmail` 并启动 `dkim-filter` 程序。

### Exim 中的 DKIM

`Exim` 4.70 版本（2009 年底）添加了对 DKIM 的原生支持，并放弃了对 Yahoo! 的 DomainKeys 的支持。随着 `Exim` 开发人员修复错误并积累 DKIM 使用经验，预计功能集会继续演进。

`Exim` 的 DKIM 支持默认启用。要关闭它，请在 `Local/Makefile` 中设置 `DISABLE_DKIM=yes` 并重建并重新安装软件包。

`Exim` 实现在 SMTP 传输配置中签名传出消息，并在新 ACL `acl_smtp_dkim` 中验证传入消息的签名。集线器机器可以通过为这些消息设置 `dkim_disable_verify` 来禁用对它们为本地主机中继的消息的签名验证。

#### 签名传出消息

第一个 DKIM 实现任务是使用第 591 页所述的 `OpenSSL`（在 DNS 章节中）生成你的加密密钥。必须为 SMTP 传输定义几个新的 `Exim` 选项。选项可以包括在调用传输时进行展开的变量。表 20.26 包含 DKIM 相关签名选项的列表。

### 表 20.26 Exim 中的 DKIM 签名选项

| 选项 | 类型 | 必需 | 内容 |
|---|---|---|---|

| `dkim_domain` | String | 是 | 用于签名的域名 |
| `dkim_selector` | String | 是 | 密钥选择器（名称） |
| `dkim_private_key` | String | 是 | 私钥或包含私钥的文件名 |
| `dkim_canon` | String | 否 | 规范化方法：simple 或 relaxed |
| `dkim_strict` | String | 否 | 如果为 true，签名错误会将邮件退回队列 |
| `dkim_sign_headers` | String | 否 | 要包含在签名中的头部 |

前三个“选项”是必需且必须配置的；其余则是真正可选的。默认情况下，规范化方法（`dkim_canon`）为 `relaxed`，导致签名错误的消息会在没有签名的情况下发送（`dkim_strict`），并且 `Exim` 使用 `RFC4871` 中的头部列表进行签名（`dkim_sign_headers`）。强制选项很直接，但如果你有一个托管多个真实或虚拟域名的复杂站点，你就需要在定义它们时巧妙一些。

#### 验证收到的已签名消息

传入的 DKIM 签名邮件消息在 `acl_smtp_dkim` ACL 中进行验证。该 ACL 对每个签名调用一次，并返回以下代码之一：

- `none` – 消息未签名
- `invalid` – 签名无法验证（密钥不可用或无效）
- `fail` – 签名在头部、正文或两者上验证失败
- `pass` – 签名有效

状态通过 `$dkim_verify_status` 变量返回，失败细节则位于 `$dkim_verify_reason` 中。还有许多其他 `$dkim_variable` 标签，可让你访问签名的各个字段，并允许你实施特殊策略（例如，标记来自 `gmail.com` 但没有签名的消息，或拒绝无法验证的 `paypal.com` 消息）。

#### 完整示例

以下示例改编自 Phil Pennock 的 DKIM 设置。22 它包含用于验证签名的 `acl_process_dkim` 定义，以及用于实际签名的路由器和传输（分别为 `dnslookup_signed` 和 `remote_dksign`）。

此配置允许签名多个域，并提供多个密钥以实现密钥轮换。该文件以 CDB 格式存储，并将诸如“example.org”的键映射到诸如“d200912”的值。

密钥选择器命名为 `dyyyymm`，其中 `d` 仅表示日期（date）的字母“d”，`yyyy` 是生成密钥的年份，`mm` 是生成密钥的月份。密钥文件命名为 `rsa.private.selector.domain`，并存储在使用宏 `DKKEY_DIR` 定义的密钥目录中。请确保该目录对 `exim` 可读，但对其他用户不可读。

```
#### macros to define the directories for databases and keys
CONFIG_DIR = path_to_config_dir
DKKEY_DIR = path_to_key_dir
```

```
#### main section: define the domains to sign and required DKIM acl
domainlist dksign_domains = cdb;CONFIG_DIR/dk_selector.cdb
acl_smtp_dkim = acl_process_dkim
```

```
#### ACL section: verify signature on incoming mail, add a header
acl_process_dkim:
  warn !dkim_status = none
  add_header = :at_start-X-DKIM-Report: $dkim_verify_status \
    {$if eq{$dkim_verify_status}{pass}{$dkim_verify_reason}{}} \
    {Signer=$dkim_cur_signer} (Testing=$dkim_key_testing)
```

```
#### Router section: put just before "dnslookup" router, sign nonlocal
dnslookup signed:
  driver = dnslookup
  domains = !+local_domains
  transport = remote_dksign
  condition = ${if match_domain{$sender_address_domain} \
    {!dksign_domains}{}}
  no_verify
```

```
#### Transport section: does the actual signing
remote_dksign:
  driver = smtp
  dkim_domain = $sender_address_domain
  dkim_selector = ${lookup {$sender_address_domain} \
    cdb{CONFIG_DIR/dk_selector.cdb}{$value}fail}
  dkim_private_key = DKKEY_DIR/rsa.private.$dkim_selector.$dkim_domain
  dkim_strict = 1
```

这些代码片段使外发消息被签名，并让传入消息的签名得到验证，同时添加一个 DKIM 报告头部。以下是该头部的一个示例：
