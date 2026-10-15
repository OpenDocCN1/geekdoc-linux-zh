
使用 SpamAssassin 扫描还可以做更多更复杂的操作；有关所有细节，请参阅 Exim 规范。

## 认证器

认证器是驱动（drivers），它们与 SMTP AUTH 命令的质询/响应序列交互，并确定客户端和服务器都能接受的身份验证机制。Exim 支持四种机制：

- `AUTH_CRAM_MD5` (RFC2195)
- `AUTH_CYRUS_SASL`，用于 Cyrus IMAP 软件
- `AUTH_PLAINTEXT`，包含 PLAIN 和 LOGIN
- `AUTH_SPA`，支持 Microsoft 的安全密码认证

如果 `exim` 正在接收邮件，它充当 SMTP AUTH 服务器；如果正在发送邮件，则它是客户端。认证器实例定义中出现的选项带有 `server_` 或 `client_` 前缀，以便根据 Exim 所扮演的角色进行不同配置。

认证器在访问控制列表中使用，就像第 817 页 ACL 示例中的以下子句：

```
accept authenticated = *
```

下面是一个同时展示客户端和服务器端 LOGIN 机制的示例。这个简单示例使用固定的用户名和密码，对于小型站点来说可以，但对于大型安装来说可能不可取。

```
begin authenticators
    my_client_fixed_login:
        driver = plaintext
        public_name = LOGIN
        client_send = : myusername : mypasswd

    my_server_fixed_login:
        driver = plaintext
        public_name = LOGIN
        server_advertise_condition = ${if def:tls_cipher}
        server_prompts = User Name : Password
        server_condition = ${if and { {eq ${auth1}{username}} \ {eq ${auth2}{mypasswd}} }}
        server_set_id = $auth1
```

身份验证数据可以来自多种来源：LDAP、PAM、`/etc/passwd` 等。上述 `server_advertise_condition` 子句通过在连接上要求 TLS 安全性（通过 STARTTLS 或 SSL），防止邮件客户端明文发送密码。如果你希望在 `exim` 充当客户端系统时也有相同行为，请在客户端子句中也使用 `client_condition` 选项，同样使用 `tls_cipher`。

有关所有可能的 Exim 身份验证选项的详细信息及示例，请参阅文档。

## 路由器

路由器作用于收件人的电子邮件地址，要么重写这些地址，要么将它们分配给某个传输并发送出去。一个特定的路由器可以有多个实例，每个实例带有不同的选项。

您需要指定一系列路由器。一条消息从第一个路由器开始，依次遍历列表，直到消息被接受或拒绝。接受消息的路由器通常会将消息交给传输驱动程序。路由器同时处理传入和传出的消息。它们有点像编程语言中的子程序。

路由器可以对一条消息返回以下任何处理结果：

- **接受** -- 路由器接受该地址，并将其交给传输驱动程序
- **通过** -- 路由器无法处理该地址；继续转到下一个路由器
- **拒绝** -- 路由器选择不处理该地址；请交给下一个路由器！
- **失败** -- 地址无效；路由器将其排队以生成退回邮件
- **延迟** -- 将消息留在队列中稍后处理
- **错误** -- 路由器配置中存在错误；消息被延迟处理

如果一条消息从序列中的所有路由器都得到通过或拒绝结果，那么它将被作为不可路由的地址退回。

如果一条消息满足了某个路由器的前置条件，而该路由器以 `no_more` 语句结尾，那么这条消息将不会被呈送给任何后续路由器，无论当前路由器对它的处理结果是什么。例如，如果您的远程 SMTP 路由器设置了前置条件 `domains = +local_domains` 并设置了 `no_more`，那么只有发送给本地用户的消息（也就是那些无法通过 `domains` 前置条件的消息）才会继续传给序列中的下一个路由器。

路由器有许多可用的选项；常见的示例包括前置条件、接受或失败条件、要返回的错误消息以及要使用的传输驱动程序。

接下来的几节将详细介绍名为 `accept`、`dnslookup`、`manualroute` 和 `redirect` 的路由器。示例配置代码片段假定 `exim` 运行在 `example.com` 域中的一台本地机器上。它们都很简单；如果您想使用某些更高级的路由器，请查阅相关文档。

### accept 路由器

`accept` 路由器将一个地址标记为 OK，并将相关的消息传递给传输驱动程序。下面是名为 `localusers` 和 `save_to_file` 的 `accept` 路由器实例示例，前者用于投递本地邮件，后者用于追加到归档文件。

```
localusers:
    driver = accept
    domains = example.com
    check_local_user
    transport = my_local_delivery
```

### manualroute 路由器

```
firewall:
  driver = manualroute
  transport = remote-smtp
  route_data = ${lookup{$domain} cdb {/internal/host/routes}}
```

### redirect 路由器

`redirect` 驱动程序负责地址重写，例如系统级别名文件或用户的 `~/.forward` 文件中所要求的重写。它通常不会将重写后的地址分配给传输；这个任务留给链中的其他路由器来完成。

下面的第一个实例 `system_aliases` 使用对 `/etc/aliases` 文件的线性搜索（`lsearch`）来查找别名。对于小的别名文件来说这没问题，但如果您的文件很大，请用数据库查找来替代这种线性搜索。第二个实例 `forwardfile` 首先验证邮件是发送给本地用户的，然后检查该用户的 `.forward` 文件。

```
system_aliases:
  driver = redirect
  data = ${lookup{$local_part} lsearch {/etc/aliases}}

user_forward:
  driver = redirect
  check_local_user
  file = $home/.forward
  no_verify
```

`check_local_user` 选项确保收件人是一个有效的本地用户。`no_verify` 选项表示不验证转发文件将消息重定向到的地址是否有效；直接发送即可。

#### 通过 .forward 文件进行按用户过滤

Exim 不仅允许通过 `.forward` 文件进行转发，还允许根据用户的 `.forward` 文件内容进行过滤。它支持自己的过滤方式，以及由 IETF 正在标准化的 Sieve 过滤。如果用户的 `.forward` 文件的第一行是

```
#Exim filter
```

或

```
#Sieve filter
```

那么后续的过滤命令（大约有 15 个）就可以用来确定消息应投递到何处。过滤实际上并不投递消息——它只是改动投递目的地。例如：

```
#Exim filter
if $header_subject: contains SAGE or $header_subject: contains sysadmin
then
  save $home/mail/sage-sysadmin
endif
```

有很多可用的选项可以控制用户在 **`.forward`** 文件中可以做什么和不可以做什么。选项名称以 `forbid_` 或 `allow_` 开头。它们很重要，可以防止用户在不应该的时候运行 shell、将库加载到二进制文件中或使用嵌入的 Perl 解释器。在升级时检查新的 `forbid_*` 选项，以确保用户不会在他们的 **`.forward`** 文件中变得过于花哨。

## Transports

路由器决定邮件应该去哪里，而传输实际上将邮件送达。本地传输通常附加到文件、管道到本地程序，或通过 LMTP 协议与 IMAP 服务器通信。远程传输通过 SMTP 与互联网上的对应方通信。

Exim 有五种传输：`appendfile`、`lmtp`、`smtp`、`autoreply` 和 `pipe`；我们详细说明 `appendfile` 和 `smtp`。`appendfile` 传输通常用于发送 vacation 消息，而 `pipe` 传输通过 UNIX 管道将邮件作为输入传递给命令。与路由器一样，您必须定义传输的实例，并且拥有同一类型传输的多个实例是可以的。顺序对路由器很重要，但对传输不重要。

### The appendfile transport
