
# 第 16 章 域名系统 435

DNS 的动态更新是很危险的。它们可能会导致对你重要系统数据的产生不受控制的访问。不要尝试使用 IP 地址进行访问控制——它们太容易伪造了。使用共享密钥的 TSIG 认证更好；它是可用的且易于配置。BIND 8 和 9 都是：

```
% nsupdate -k keydir:keyfile
```

BIND 9 还能理解

```
% nsupdate -y keyname:secretkey
```

有关 TSIG 的更多细节，请参见从第 438 页开始的章节。

`named.conf` 中通过 `allow-update` 或 `update-policy` 子句启用区域的动态更新。`allow-update` 允许根据源 IP 地址或基于密钥的认证更新任何记录。`update-policy` 是 BIND 9 的扩展，允许根据主机名或记录类型对更新进行细粒度的控制。它需要基于密钥的认证。

`use-policy` 允许客户端更新其 A 记录或 PTR 记录，但不更改 SOA 记录、NS 记录或 KEY 记录。你可以使用它来。`allow-update` 允许根据源 IP 地址或基于密钥的认证更新任何记录。`update-policy` 是一个 BIND 9 的扩展，允许根据主机名或记录类型对更新进行细粒度的控制。它需要基于密钥的认证。

### 表 16.11 区域.conf 中的安全功能

### 访问控制列表（ACLs）重温

ACLs 用于 `named.conf`。其语法在第 389 页描述。ACLs 有助于防止欺骗和拒绝服务攻击。例如：

```
acl ourselves {
    128.138.0.0/16; // Colorado大学
    198.11.16/24; // 主校
    204.228.69/24;
}
```

在配置文件的全局选项部分，你随后可以包含

```
allow-recursion { };
blackhole { };
```

将区域传输限制到我们自己的从服务器是一个好主意。ACL 让一切变得很整洁。

```
acl ourselves {
    128.138.242.1;
}
```

```
acl measurements {
    128.9.160.157; // manning 的测量
    198.32.4.0/24; // manning 的测量
    192.5.5.0/24;
}
```

实际限制通过如下行实现：

```
allow-transfer { ourselves; measurements; };
```

传输被限制在自己的从服务器以及互联网测量项目的机器上，这些项目允许反向 DNS 树确定互联网的大小和配置错误的服务器百分比。通过这种方式限制传输，其他站点无法使用 `nslookup`、`dig` 或 `host` 导出你的整个数据库。

例如，使用 `dig` @server domain-to-dump axfr：

```
% dig @128.138.143.151 cs.colorado.edu axfr
:; connection timed out
: <<>> dig 8.3 <<@128.138.143.151 cs.colorado.edu axfr
:; (1 server found)
:; FROM: chateau.caida.org to SERVER: 128.138.143.151
:; WHEN: Feb 19 17:16:53 2002
```

你仍然应该在较低级别通过访问控制列表和每个主机的正常安全防护来保护你的网络。如果这些措施不可，你可以拒绝来自你密切监控的网关机器的 DNS 数据包。

# 限制 named

为了限制某人在入侵你的服务器时可能造成的破坏，你可以将 `named` 运行在 `chrooted` 环境中并作为非特权用户运行。`-t` 标志指定要 chroot 的目录，`-u` 和 `-g` 标志指定

# Linux 管理手册

运行 BIND 的 UID 和 GID。BIND 9 支持 `-u` 标记，但不支持 `-g` 标记。例如，以下命令：

```
# named -u 53 -g 53 -t /var/named      /* BIND 8 */
# named -u 53 -t /var/named                /* BIND 9 */
```
