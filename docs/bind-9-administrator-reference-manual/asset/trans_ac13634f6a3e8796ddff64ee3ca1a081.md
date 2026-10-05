

$ORIGIN 设置了将附加到任何未限定记录的域名名。当一个区域首次被读取时，会有一个隐式的 $ORIGIN <zone-name>。如果 $ORIGIN 参数指定的域名不是绝对的，则会将当前的 $ORIGIN 附加到 $ORIGIN 参数中指定的域名之后。

```
$ORIGIN example.com.
WWW CNAME  MAIN-SERVER
```

等同于

```
WWW.EXAMPLE.COM. CNAME MAIN-SERVER.EXAMPLE.COM.
```

## 6.3.5.2. $INCLUDE 指令

语法：$INCLUDE filename [ origin][ comment ]

读取并处理文件 filename，就像它被包含在当前位置的文件中一样。如果指定了 origin，则处理文件时会将 $ORIGIN 设置为该值，否则使用当前的 $ORIGIN。
一旦文件被读取，源和当前域名名将恢复到执行 $INCLUDE 之前的值。

> 注意：RFC 1035 规定在 $INCLUDE 之后之后应该恢复当前的源（origin），但对于是否也应该恢复当前域名名未说明。BIND 9 恢复了这两者。这可以被解释为对 RFC 1035 的偏离、一项特性或两者兼有。

## 6.3.5.3. $TTL 指令

语法：$TTL default-ttl [ comment ]

为后续未定义 TTL 的记录设置默认的生存时间（TTL）。有效的 TTL 范围是 0-2147483647 秒。

$TTL 定义在 RFC 2308 中。

## 6.3.6. BIND 主文件扩展：$GENERATE 指令

语法：$GENERATE range lhs type rhs [ comment ]

# 第 6 章节：BIND 9 配置参考

$GENERATE 用于创建一系列的资源记录，这些记录之间的区别仅在于一个迭代器。$GENERATE 可以轻松地生成记录集，以支持 RFC 2317 中描述的子 /24 反向委托（reverse delegations）：无类分类 IN-ADDR.ARPA 描述。

```
$ORIGIN 0.0.192.IN-ADDR.ARPA.
$GENERATE 1-2 NS SERVER1.EXAMPLE.
$GENERATE 1-127 $CNAME .0
```

等同于

```
0.0.192.IN-ADDR.ARPA. NS SERVER1.EXAMPLE.
0.0.192.IN-ADDR.ARPA NS SERVER2.EXAMPLE.
1.0.0.192.IN-ADDR.ARPA CNAME 1.0.0.192.IN-ADDR.ARPA
2.0.0.192.IN-ADDR.ARPA CNAME 2.0.0.192.IN-ADDR.ARPA
...
127.0.0.192.IN-ADDR.ARPA CNAME 127.0.0.192.IN-ADDR.ARPA
```

| range | 这可以有两种形式：start-stop 或 start-stop/step。如果第一种形式被设置为 1，则 start、stop 和 step 的所有必须都是正数。 |
| lhs | **lhs 描述了要创建的资源记录的所有者名称。** lhs 中的任何单个 $ 符号都会被迭代器值替换。若要在输出中获得一个 \$，需要使用反斜杠 \ 转义 $，例如 \$ 后可选地跟随修饰符，这些修饰符更改相对于迭代器的偏移、字段宽度基基。修饰符通过 [offset,width,base] 引入，例如 [-2,3,d] 会从当前值减去 20，并以 3 位零填充十进制字段输出结果。可选输出格式有十进制（d）、八进制（o）和十六进制（x 或大写的 X）。如果 lhs 不是绝对的，则会将当前的 $ORIGIN 附加到该名称上。为了兼容早期版本，$$ 仍被识别为输出中的文字 $。 |
| type | 目前支持的类型只有 PTR、CNAME、A、AAAA 和 NS。其处理方式与 lhs 类似。 |
| rhs | rhs 是一个域名。其处理方式与 lhs 类似。 |

$GENERATE 指令是 BIND 的扩展，不是标准区域文件格式的一部分。

# 第 7 章节：BIND 9 安全考虑

## 7.1. 访问控制列表

访问控制列表（ACLs）是地址列表，你可以设置并为其取别名，以便以后在 allow-notify、allow-query、blackhole、allow-transfer 等处使用。
使用 ACLs 允许你控制谁可以访问你的名称服务器，而无需用巨大的 IP 地址列表弄乱配置。使用 ACLs 并控制对服务器的访问是一个*好主意*。限制外部对你服务器的访问可以防止伪欺和 DoS 攻击。以下是如何正确应用 ACLs 的示例：

```
// 设置一个名为 "bogusnets" 的 ACL，它将阻止 RFC1918 空间
acl bogus-nets { 0.0.0.0/8; 10.0.0.0/8; 172.16.0.0/12; 192.168.0.0/16; 127.0.0.
// 设置一个名为 our-nets 的 ACL。将此替换为真实的 IP 数字
acl our-nets ( x.x.x.x/24; x.x.x.x/21 );
options {
allow-query { our-nets };
allow-recursion { our-nets };
...
blackhole { bogusnets; };
}
zone "example.com" {
type master;
file "example.com";
allow-query { any };
};
```

这允许从外部对服务器进行递归查询，除非之前禁用了递归。有关如何使用 ACLs 保护你的服务器的更多信息，请参阅 **AUSCERT** 的公告，地址：http://auscert.org/pub/advisory/dns_dos

## 7.2. chroot 和 setuid（用于 UNIX 服务器）

在 UNIX 服务器上，可以通过指定 -t 选项在 chroot 环境（`chroot`）中运行 BIND。这可以通过将 BIND 放置在“沙箱”中来帮助提高安全性，从而限制服务器被攻破时的损害。UNIX 版本 BIND 的另一个有用功能是可以作为非特权用户（`-u`）运行守护进程。我们建议在 chroot 时作为非特权用户运行。以下是一个在 chroot 沙箱 `/var/named` 中加载 BIND 并运行 named setuid 的命令行示例：

```
/usr/local/bin/named -u -t /var/named
```

### 7.2.1. chroot 环境

为了让 chroot() 在特定目录（例如 `/var/named`）中正常工作，你需要设置一个包含 BIND 运行所需一切的环境。从 BIND 的角度来看，`/var/named` 是文件系统的根。你需要调整 pid-file 等选项的值来适应这一点。与 BIND 的早期版本不同，你不需要编译 named 的静态共享库。但是，取决于你的操作系统，你可能需要设置像 `/dev/zero` 等项。

### 7.2.2. 使用 setuid

在运行非特权用户之前，使用 touch 工具（更改访问修改时间）或 chown 工具（更改所有者和组）对你需要 named 写入的文件。

## 7.3. 动态更新安全

动态更新的访问应该被严格限制。在早期版本中，这种方法是基于请求更新的主机 IP 地址，这很容易被伪造。由于这些原因，我们强烈建议通过事务签名（TSIG）对更新进行验证。也就是说，allow-update 选项应该列出 TSIG 名称，而不是 IP 地址。或者，可以使用新的 update-policy 选项。某些站点将所有动态更新数据放在子域中并将子域委托给独立的区域。这样，包含关键数据的顶级区域就不需要任何动态更新。

# 第 8 章节：故障排除

## 8.1. 常见问题

### 8.1.1. 它无法工作；我如何发现哪里错了？

解决安装和配置问题的最佳方案是预先设置日志措施。日志文件提供了用于发现问题以及如何修复的提示和信息。

## 8.2. 递增和更改序列号

区域序列号只是数字——与日期无关。许多人将其设置为一个代表日期的数字，通常格式为 YYYMMDD。许多人为了测试 Y2K 合规性将其设置为 2000 年看看是否有效。然后他们尝试恢复旧的序列号。这将导致问题，因为序列号用于指示区域已更新。如果从服务器上的序列号小于主服务器上的序列号，从服务器将尝试更新其副本。

解决此问题是将该数字加上 2147483647 (2^31-1)，重新加载区域并确保所有从都更新到新的区域序列号，将其重置为你想要的数字，然后重新加载区域。

