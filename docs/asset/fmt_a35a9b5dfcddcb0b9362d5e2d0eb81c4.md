
要为您的 DNS 服务器创建 TSIG 密钥，您使用如上所述的 `dnssec-keygen` 命令。不使用您用于 DNSSEC 的相同密钥，而是创建一套新的用于传输签名的密钥。对于 TSIG，使用共享私钥而不是公钥/私钥对。对于 TSIG 密钥，您使用 HMAC-MD5 算法，该算法在 `.key` 和 `.private` 文件中生成相同的密钥。使用 `-a` 选项指定要使用的 HMAC-MD5 算法，并使用 `-b` 选项指定比特大小（HMAC-MD5 的范围从 1 到 512）。`-n` 选项用于指定密钥类型，在此情况下为 HOST，表示主机名。比特范围将根据算法而异。以下示例使用 128 位密钥和 HMAC-MD5 加密算法创建一个主机密钥：

```bash
dnssec-keygen -a HMAC-MD5 -b 128 -n HOST turtle.mytrek.com
```

这会创建一个私钥和公钥，分别位于 `.key` 和 `.private` 文件中。在 TSIG 方案中，两个主机都使用相同的私钥进行认证。例如，要启用 DHCP 服务器更新 DNS 服务器，两者都需要 TSIG 认证的私钥（密钥）。HMAC-MD5 密钥用作共享私钥，在 `.key` 和 `.private` 文件中生成相同的私钥和公钥。

### 密钥语句

然后，您在 `named.conf` 文件中使用 `key` 语句指定密钥。对于 `algorithm` 选项，您列出 HMAC-MD5 算法；对于 `secret` 选项，您列出私钥。此密钥将列在 `.private` 和 `.key` 文件中。前面的示例将生成名为 `K turtle.mytrek.com.+157.43080.key` 和 `K turtle.mytrek.com.+157.43080.private` 的密钥和私钥文件。`.key` 文件的内容由这里显示的资源记录组成：

```text
turtle.mytrek.com. IN KEY 512 3 157 ONQAfBLnvWU9H8hRqq/WA==
```

私钥文件的内容显示相同的密钥以及算法。

```text
Private-key-format: v1.2
Algorithm: 157 (HMAC_MD5)
Key: ONQAfBLnvWU9H8hRqq/WA==
```

在 `named.conf` 文件中，您然后使用 `key` 语句为密钥命名。

```code
key myserver {
  algorithm HMAC-MD5;
  secret "CNQAfBBLnvWUSH8hRqq/WA==";
};
```

然后可以使用该密钥的名称在其他命名语句（例如 `allow-update` 语句）中引用该密钥。

```code
allow-update myserver;
```

你要建立通信的 DNS 服务器或 DHCP 服务器也必须拥有相同的密钥。有关 DHCP 和 TSIG 的更多信息，请参阅前面的章节“动态更新：DHCP 和日志文件”以及第 35 章。对于两台 DNS 服务器之间的通信，每台服务器都必须有一个指定共享密钥的 `server` 语句。在以下示例中，位于 192.168.0.1 的 DNS 服务器的 `named.conf` 文件必须包含以下 `server` 语句，以使用共享的 `myserver` 密钥与位于 10.0.0.1 的 DNS 服务器进行通信。10.0.0.1 DNS 服务器上的 `named.conf` 文件必须有一个针对 192.168.0.1 服务器的相应 `server` 语句。

```code
server 10.0.0.1 { keys {myserver;}; };
```

### 拆分 DNS：视图

BIND 9.x 允许你将 DNS 空间划分为内部视图和外部视图。这种划分为独立视图的组织方式被称为拆分 DNS（Split DNS）。这种配置对于管理连接到更大网络（如互联网）的本地网络非常有用。你的内部视图将包含本地网络中主机的 DNS 信息，而外部视图仅显示 DNS 空间中可被其他网络访问的部分。当你有一个希望从更大网络（如互联网）中保护起来的本地网络时，通常会使用 DNS 视图。实际上，你保护了本地网络中主机的 DNS 信息免受像互联网这样更大的外部网络的影响。

#### 内部和外部视图

要实施拆分 DNS 空间，你需要为内部视图和外部视图设置不同的 DNS 服务器。内部 DNS 服务器将存储关于本地主机的 DNS 信息。外部 DNS 服务器通过网关维护与互联网的连接，并管理允许外部访问的本地主机的 DNS 信息（例如 FTP 或 Web 站点）。网关和可访问互联网的站点构成了网络中主机的外部视图。内部服务器处理所有针对本地主机或子域的查询。发送到外部主机（如互联网站点）的查询会被发送到外部服务器，然后由外部服务器将其转发到互联网。发送到运行外部服务器（如互联网 FTP 和 Web 站点）的那些本地主机的查询会被发送到外部 DNS 服务器进行处理。从互联网发送到本地主机的邮件首先由外部服务器处理，然后由外部服务器将消息转发到内部服务器。通过拆分 DNS 配置，本地主机可以访问其他本地主机、互联网站点以及维护互联网服务器的本地主机。另一方面，互联网用户只能访问那些对互联网开放的主机（由外部服务器提供服务），例如拥有 FTP 和 HTTP 等互联网服务器的主机。然而，互联网用户可以向来往于内部和外部任何本地主机发送电子邮件消息。

你还可以使用 DNS 视图来管理私有网络与大网络之间的连接，该私有网络可能仅使用一个互联网地址将其主机连接到互联网。在这种情况下，内部视图持有私有地址（192.168...），外部视图将具有互联网地址的网关机连接到互联网。这增加了另一层安全性，提供了类似 IP 伪装的结果（参见第 38 章）。

#### 配置视图

DNS 视图使用允许语句（如 `allow-query` 和 `allow-transfer`）进行配置。通过这些语句，你可以指定区域可以向哪些主机发送和接收查询及传输。例如，内部区域可以接受来自其他本地主机的查询，但不接受来自具有外部访问权限（如互联网服务器）的本地主机的查询。尽管这样，本地互联网服务器可以接受来自本地主机的查询。所有互联网查询都会转发到网关。在外部配置中，本地互联网服务器可以接受来自任何地方的查询。网关接收来自本地主机和本地互联网服务器的查询。在以下示例中，一个包含三个内部主机和一个外部主机的网络被设置为拆分视图。有两个 DNS 服务器：一个用于内部网络，另一个基于外部主机用于外部访问。实际上这些构成了一个网络，但被分割成两个视图。内部视图被称为 `mygolf.com`，外部视图被称为 `greatgolf.com`。在每个配置中，内部主机在标记为 `internals` 的 ACL 中指定，外部主机在标记为 `externals` 的 ACL 中指定。如果你想将整个 IP 地址范围指定为内部，可以简单地使用网络地址，如 `192.168.0.0/24`。在 `options` 部分，`allow-query`、`allow-recursion` 和 `allow-transfers` 限制了网络内的访问。

#### 拆分视图示例

以下示例仅显示了实施内部视图所需的配置条目。在 `mygolf.com` 区域中，仅允许在内部主机之间进行查询和传输。全局 `allow-recursion` 选项允许在内部主机之间进行递归。

```code
acl internals { 192.168.0.1; 192.168.0.2; 192.168.0.3; };
acl externals {10.0.0.1;};
options {
    forward only;
    forwarders {10.0.0.1;}; // 转发到外部服务器
    allow-transfer { none; }; // 默认不允许向任何人进行 allow-transfer
    allow-query { internals; externals; };// 限制查询访问
    allow-recursion { internals; }; // 将递归限制在内部主机
}
zone "mygolf.com" {
    type master;
    file "mygolf";
    forwarders { };
    allow-query { internals; };
    allow-transfer { internals; }
};
```

在外部 DNS 服务器的配置中，为 `internals` 和 `externals` 设置了相同的 ACL。在 `options` 语句中，现在允许 `externals` 和 `internals` 进行递归。在 `mygolf.com` 区域中，允许来自任何地方的查询，并允许 `externals` 和 `internals` 进行递归。完全不允许传输。

#### 外部 DNS 服务器
