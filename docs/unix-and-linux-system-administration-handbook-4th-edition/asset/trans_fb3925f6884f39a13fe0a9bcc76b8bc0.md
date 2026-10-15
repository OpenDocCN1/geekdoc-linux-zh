
## localhost 区域

地址 127.0.0.1 指的是主机自身，应该映射到名称“localhost”。²¹ 有些站点将该地址映射到“localhost.localdomain”，有些则两者都映射。相应的 IPv6 地址是 ::1。

如果忘记配置 localhost 区域，您的站点可能会查询根服务器以获取本地信息。根服务器收到大量此类查询，以至于运维人员正在考虑在根级别添加 localhost 和 127.0.0.1 之间的通用映射。根据 2010 年 1 月欧洲 K 根服务器的测量数据（k.root-servers.org/statistics），"local" 是查询量第四大的域名，仅次于 com、arpa 和 net。对于一个繁忙的名称服务器来说，这相当于大量无用的查询（每秒 1,500 次）。在流行的“伪顶级域”类别中，其他不寻常的名称还包括 lan、home、localdomain 和 domain。

名称 localhost 的正向映射可以在域的正向区域文件中定义（使用适当的 $ORIGIN 语句），也可以在其自己的文件中定义。每台服务器，即使是缓存服务器，通常也是其自身反向 localhost 域的主服务器。

以下是 named.conf 中配置 localhost 的行：

```
zone "localhost" {
    type master;
    file "localhost";
    allow-update { none; };
};

zone "0.0.127.in-addr.arpa" {    // localhost reverse zone
    type master;
    file "127.0.0";
    allow-update { none; };
};
```

### 相应的正向区域文件 localhost 包含以下内容：

```
$TTL 30d
; localhost
@   IN  SOA localhost. postmaster.localhost. (
        1998050801    ;serial
        3600          ;refresh
        1800          ;retry
        604800        ;expiration
        3600 )        ;minimum

    NS  localhost.
    A   127.0.0.1
```

以及反向文件 127.0.0：

```
$TTL 30d
; 0.0.127.in-addr.arpa
@               IN      SOA     localhost. postmaster.localhost. (
                                1998050801      ;serial
                                3600            ;refresh
                                1800            ;retry
                                604800          ;expiration
                                3600 )          ;minimum

1               NS      localhost.
                PTR     localhost.
```

localhost 地址（127.0.0.1）的映射永远不会改变，因此超时时间可以设置得较长。注意序列号，它编码了日期；该文件最后修改于 1998 年。还要注意，localhost 域只列出了主名称服务器。这里的 @ 表示“0.0.127.in-addr.arpa.”。

## 一家小型安全公司

我们的第一个真实示例是一家专门从事安全咨询的小公司。他们在较新版本的 Red Hat Enterprise Linux 上运行 BIND 9，并使用视图（views）实现拆分 DNS 系统，内部和外部用户看到不同的主机数据。他们还在内部使用私有地址空间；有关这些地址的查询绝不应泄露到互联网上，以免干扰全球 DNS 系统。以下是他们的 named.conf 文件，稍作重新格式化并添加了一些注释：

```
options {
    directory "/var/domain";
    version "root@atrust.com";
    allow-transfer { 82.165.230.84; 71.33.249.193; 127.0.0.1; };
    listen-on { 192.168.2.10; 192.168.2.1; 127.0.0.1; 192.168.2.12; };
};

include "atrust.key";            // Defn of atkey in mode 600 file

controls {
    inet 127.0.0.1 allow { 127.0.0.1; } keys { atkey; };
};

view "internal" {
    match-clients { 192.168.0.0/16; 206.168.198.192/28; 172.29.0.0/24; };
    recursion yes;
    include "infrastructure.zones";    // Root hints, localhost forw + rev
    zone "atrust.com" {                // Internal forward zone
        type master;
        file "internal/atrust.com";
    };
};
```

```
zone "1.168.192.in-addr.arpa" {    // Internal reverse zone
    type master;
    file "internal/192.168.1.rev";
    allow-update { none; };
};
... 
include "internal/trademark.zones"; // atrust.net, atrust.org, etc. slaves
}; // End of internal view

view "world" {                // External view
    match-clients { any; };
    recursion no;
    zone "atrust.com" {        // External forward zone
        type master;
        file "world/atrust.com";
        allow-update { none; };
    };
    zone "189.173.63.in-addr.arpa" {  // External reverse zone
        type master;
        file "world/63.173.189.rev";
        allow-update { none; };
    };
    include "world/trademark.zones";  // atrust.net, atrust.org, etc. masters
    zone "admin.com" {        // Master zones only in world view
        type master;
        file "world/admin.com";
        allow-update { none; };
    };
    ...                        // Lots of master+slave zones omitted
}; // End of external view
```

文件 atrust.key 定义了名为 atkey 的密钥：

```
key "atkey" {
    algorithm hmac-md5;
    secret "shared secret key goes here";
};
```

文件 infrastructure.zones 包含根提示和 localhost 文件，而 trademark.zones 包含 atrust.com 名称的变体，既包括不同顶级域（net、org、us、info 等），也包括不同的拼写（如 applied-trust.com 等）。

区域按视图（internal 或 world）和类型（master 或 slave）组织，区域数据文件的命名约定反映了这一方案。该服务器对 internal 视图是递归的，该视图包含所有本地主机，包括许多使用私有地址的主机。该服务器对 external 视图不递归，该视图仅包含 atrust.com 的选定主机以及他们提供主或从 DNS 服务的外部区域。
