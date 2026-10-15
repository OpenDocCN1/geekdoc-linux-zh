
## 表 20.26 Exim 中的 DKIM 签名选项

| 选项 | 类型 | 必需 | 内容 |
|---|---|---|---|
| dkim_domain | String | 是 | 用于签名的域名 |
| dkim_selector | String | 是 | 密钥选择器（名称） |
| dkim_private_key | String | 是 | 私钥或包含私钥的文件名 |
| dkim_canon | String | 否 | 规范化方法：simple 或 relaxed |
| dkim_strict | String | 否 | 如果为 true，签名错误会将邮件退回队列 |
| dkim_sign_headers | String | 否 | 要包含在签名中的头部 |

前三个“选项”是必需且必须配置的；其余则是真正可选的。默认情况下，规范化方法（dkim_canon）为 relaxed，导致签名错误的消息会在没有签名的情况下发送（dkim_strict），并且 Exim 使用 RFC4871 中的头部列表进行签名（dkim_sign_headers）。强制选项很直接，但如果你有一个托管多个真实或虚拟域名的复杂站点，你就需要在定义它们时巧妙一些。

## 验证收到的已签名消息

传入的 DKIM 签名邮件消息在 acl_smtp_dkim ACL 中进行验证。该 ACL 对每个签名调用一次，并返回以下代码之一：

- none – 消息未签名
- invalid – 签名无法验证（密钥不可用或无效）
- fail – 签名在头部、正文或两者上验证失败
- pass – 签名有效

状态通过 $dkim_verify_status 变量返回，失败细节则位于 $dkim_verify_reason 中。还有许多其他 $dkim_variable 标签，可让你访问签名的各个字段，并允许你实施特殊策略（例如，标记来自 gmail.com 但没有签名的消息，或拒绝无法验证的 paypal.com 消息）。

## 完整示例

以下示例改编自 Phil Pennock 的 DKIM 设置。22 它包含用于验证签名的 acl_process_dkim 定义，以及用于实际签名的路由器和传输（分别为 dnslookup_signed 和 remote_dksign）。

此配置允许签名多个域，并提供多个密钥以实现密钥轮换。该文件以 CDB 格式存储，并将诸如“example.org”的键映射到诸如“d200912”的值。

密钥选择器命名为 dyyyymm，其中 d 仅表示日期（date）的字母“d”，yyyy 是生成密钥的年份，mm 是生成密钥的月份。密钥文件命名为 rsa.private.selector.domain，并存储在使用宏 DKKEY_DIR 定义的密钥目录中。请确保该目录对 exim 可读，但对其他用户不可读。

```
####### macros to define the directories for databases and keys
CONFIG_DIR = path_to_config_dir
DKKEY_DIR = path_to_key_dir
```

```
####### main section: define the domains to sign and required DKIM acl
domainlist dksign_domains = cdb;CONFIG_DIR/dk_selector.cdb
acl_smtp_dkim = acl_process_dkim
```

```
####### ACL section: verify signature on incoming mail, add a header
acl_process_dkim:
  warn !dkim_status = none
  add_header = :at_start-X-DKIM-Report: $dkim_verify_status \
    {$if eq{$dkim_verify_status}{pass}{$dkim_verify_reason}{}} \
    {Signer=$dkim_cur_signer} (Testing=$dkim_key_testing)
```

```
####### Router section: put just before "dnslookup" router, sign nonlocal
dnslookup signed:
  driver = dnslookup
  domains = !+local_domains
  transport = remote_dksign
  condition = ${if match_domain{$sender_address_domain} \
    {!dksign_domains}{}}
  no_verify
```

```
####### Transport section: does the actual signing
remote_dksign:
  driver = smtp
  dkim_domain = $sender_address_domain
  dkim_selector = ${lookup {$sender_address_domain} \
    cdb{CONFIG_DIR/dk_selector.cdb}{$value}fail}
  dkim_private_key = DKKEY_DIR/rsa.private.$dkim_selector.$dkim_domain
  dkim_strict = 1
```

这些代码片段使外发消息被签名，并让传入消息的签名得到验证，同时添加一个 DKIM 报告头部。以下是该头部的一个示例：

```
X-DKIM-Report: pass (Signer=gmail.com) (Testing=0)
```

如果你打算拒绝或处罚签名无法通过验证的消息，则需要进一步制定策略。

路由器部分中的 no_verify 行并非指 DKIM 验证，而是指验证收件人地址；它在此路由器中被关闭，但在紧接着的 dnslookup 路由器中执行。没有必要做两次。

## Postfix 中的 DKIM

Postfix 使用第 846 页描述的 DKIM-milter 软件包来实现 DKIM。生成你的密钥对并使用 dkim-testkey 进行测试；构建一个
