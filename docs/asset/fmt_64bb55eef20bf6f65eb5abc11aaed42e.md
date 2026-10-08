
上述命令将创建一个新账户，没有密码、没有有效的 shell、不拥有任何文件，但为程序提供了 UID 和 GID。记住，ISC BIND & DNS 守护进程不需要在服务器上拥有 shell 账户。

### 第 4 步
现在，编辑 shells 文件 (`vi /etc/shells`) 并添加一个不存在的 shell 名称 `/bin/false`，这就是我们在 `useradd` 命令中使用的那个。

```
[root@deep tmp]# vi /etc/shells
```

### 第 5 步
进入新创建的目录后，执行以下步骤。

- 进入新创建的目录，使用以下命令：

  `[root@deep tmp]# cd bind-9.2.1`

### 第 6 步
需要修改的源码是 `globals.h`。

编辑 `globals.h` 文件以某些默认值：

```
[root@deep tmp]# vi globals.h
```

### 第 7 步
一旦对源码进行了修改，就是进行配置和优化的时间了。

- 配置并优化您的系统，使用以下行：

  `./configure --prefix=/usr --sysconf=/etc --localstated=/usr/share --with-openssl --with-libtool --disable-ipv6`

### 第 8 步
在此阶段，程序准备准备构建并安装。

```
[root@deep root]# make
[root@deep root]# find /* > DNS2
[root@deep root]# diff DNS1 DNS2 > ISC-BIND-DNS-Installed
```

上述命令将配置服务器以确保您的系统拥有编译包所需的库，编译所有源文件为可执行文件，并将二进制文件和任何支持文件安装到相应的位置。

### 第 9 步
软件编译、优化和完成后完成后可以通过删除压缩包和相关的源码目录来释放磁盘空间，因为这些不再需要。

删除 BIND & DNS 及其相关的源码目录，使用以下命令：

  `[root@deep root]# cd /var/tmp/`

  `[root@deep tmp]# rm -rf bind-9.2.1/`

  `[root@deep tmp]# rm -f bind-version.tar.gz`

# ISC BIND & DNS 第 8 章

## 运行 ISC BIND & DNS & 仅缓存服务器

本节仅适用于你选择在系统中安装并使用 ISC BIND & DNS 作为名称服务器的情况。仅缓存服务器除了 `0.0.127.in-addr.arpa`（本地主机 `localhost`）之外，对任何域名都不具有权威性。仅缓存名称服务器可以像主名称服务器和从用名称服务器一样，在你的区域内部和外部进行查找。区别在于，当仅缓存名称服务器最初查找你区域内的某个名称时，它最终会向你区域的一个主或从用名称服务器请求答案。

请记住，仅缓存名称服务器应该运行在任何不是主或从用名称服务器的系统上。这就是为什么我开始 ISC BIND & DNS 的配置是从仅缓存服务器的配置开始。这非常重要，必须安装在所有服务器上，因为书中描述的许多服务都依赖它才能正常工作。如果没有 DNS，互联网上的任何人都将无法找到你的网站。

# /etc/named.conf: ISC BIND & DNS 配置文件

`/etc/named.conf` 文件是 ISC BIND & DNS 的主配置文件。ISC BIND & DNS 正通过此配置文件获取所有的网络信息。对于你网络中所有不作为主或从用名称服务器的服务器，请使用此配置。为本地客户端机器设置简单的缓存服务器可以减少网络主服务器的负载。

## 第 1 步

通过此仅缓存名称服务器的配置，所有来自外部客户端的查询将被拒绝。粗体文本是配置文件中必须根据你的需求进行自定义和调整的部分。

- 创建 `named.conf` 文件（`touch /etc/named.conf`）并在文件中添加以下行。以下是我建议你使用的内容。

```bind
// 授权的源地址。
acl "trusted" {
    localhost;
};

// 已知的虚假源地址不应给予回复。
acl "bogon" {
    0.0.0.0/8;
    1.0.0.0/8;
    2.0.0.0/8;
    192.0.2.0/24;
    224.0.0.0/3;
    162.254.0.0/16;
    // 企业网络或可能并非虚假的。
    10.0.0.0/8;
    172.16.0.0/12;
    192.168.0.0/16;
};

options {
    directory "/var/named";
    allow-transfer ( none );
    allow-query ( trusted );
    allow-recursion ( trusted );
    blackhole ( bogon );
    tcp-clients any;
    forwarders ( 207.35.78.5; 207.35.78.6 );
    version "OpenLinux";
}

logging {
  category lame-servers { null };
}

// 根服务器提示
zone "." { type hint; file "db.cache"; };

// 为环回地址 127.0.0.1/24 提供反向映射
zone "localhost" {
  type master;
  file "db.localhost";
  notify no;
}

zone "0.0.127.in-addr.arpa" {
  type master;
  file "0.0.127.in-addr.arpa";
  notify no;
}
```

这告诉 `named.conf` 文件为这种特定的配置进行自设：

- `acl "trusted" {`

  `localhost; };`

`acl` 语句设置了供 ISC BIND & DNS 使用的访问控制列表（ACL），它可以在配置文件中出现多次。我们使用此语句来定义想要在配置文件某些部分应用新的访问控制列表。这对于在配置 `named.conf` 文件的过程中复制示例值非常有用。

在上面的 `acl` 语句中，我们定义了一个名为 `"trusted"` 的新 ACL，它将处理我们配置中允许的所有 IP 地址或主机名。通过这种方式，我们只需要用 `"trusted"` 这个名称就可以引用它，软件将自动我们将此 ACL 名称内定义的内容应用到配置中。值 `"localhost"` 是此 ACL 定义内部使用的唯一值。对于仅缓存名称服务器来说，这足够让它工作起来了。

```bind
acl "bogon" {
  0.0.0.0/8;
  1.0.0.0/8;
  2.0.0.0/8;
  192.0.2.0/24;
  224.0.0.0/3;
  162.254.0.0/16;
  // 企业网络或并非虚假的
  10.0.0.0/8;
  172.16.0.0/12;
  192.168.0.0/16;
}
```

在这里我们定义了另一个 `acl` 语句，用于所有我们想要拒绝访问 DNS 服务器的 IP 地址。如你所示，我将此 ACL 命名为 `"bogon"` 并添加所有应该拒绝的 IP 地址。上面的 IP 是 RFC 建议我们阻止的，但你可以自由添加任何 IP 地址。我们将在以后需要时在配置中引用此 ACL。

## 选项

`options` 语句设置了供 ISC BIND & DNS 使用的全局选项。

```bind
directory "/var/named";
```

`directory` 语句指定了目录。

```bind
allow-transfer ( none );
```

`allow-transfer` 语句设置了哪些主机允许区域传输，它在配置文件中只出现一次。

```bind
allow-query ( trusted );
```

`allow-query` 语句设置了哪些主机允许查询，它在配置文件中只出现一次。

```bind
allow-recursion ( trusted );
```

`allow-recursion` 语句设置了哪些主机允许递归查询，它在配置文件中只出现一次。

```bind
blackhole ( bogon );
```

`blackhole` 语句指定了哪些主机被丢入“黑洞”。

```bind
tcp-clients any;
```

`tcp-clients` 语句用于定义服务器接受的并发 TCP 连接数，这有助于限制服务器资源。

```bind
forwarders ( 207.35.78.5; 207.35.78.6 );
```

`forwarders` 语句指定了用于转发的 IP 地址。

```bind
version "OpenLinux";
```

`version` 语句允许我们隐藏 ISC BIND & DNS 的真实版本。这当有人从互联网尝试扫描我们的名称服务器以寻找软件的某些漏洞时是非常有用的。

# ISC BIND & DNS 2

## 第 8 章

```
zone "localhost" {
    type master;
    file "db.localhost";
    notify no;
}
# 用于定义系统上 localhost 地址的区域。"type master" 选项告知软件 "db.localhost" 文件是该区域的主文件，"notify no" 选项用于避免将此 localhost 配置文件传输到其他名称服务器（Name Servers）。这是一项安全特性。
```

```
zone "0.0.127.in-addr.abba" {
    type master;
    file "0.0.127.in-addr.abba";
    notify no;
}
```

# "zone" 完成了我们对仅缓存名称服务器（Caching-Only Name Server）的配置，并用于为环回地址 127.0.0.1/24 提供反向映射。如上述定义，"type master" 选项告知软件 "0.0.127.in-addr.abba" 文件是该区域的主文件，"notify no" 选项用于避免将此配置文件传输到其他名称服务器。这是一项安全特性。

### 步骤 2
现在，将 `named.conf` 文件的权限设置为 `(0600/-rw--)`，并由用户 `'named'` 所有，组权限设置为 `'named'`，出于安全考虑。

- 使用以下命令更改 `named.conf` 文件的模式和所有者：

  `[root@deep]# chmod 600 /etc/named.conf`

  `[root@deep]# chown named /etc/named.conf`

# /var/named/db.cache: 根服务器提示提示文件 (Root Server Hints File)

此部分适用于你可能安装在系统上的所有类型的名称服务器（缓存、主或从）。`db.cache` 文件也称为“根服务器提示文件”，它告诉你的服务器（缓存、主或从）根区域 `"."` 的服务器在哪里。你必须获取 `db.cache` 文件的副本并将此文件复制到 `/var/named` 目录。所有类型的 DNS 服务器都需要此配置文件才能正常工作。

### 步骤 1
在你组织的 Unix 系统上使用以下命令为你的名称服务器查询新的 `db.cache` 文件，或从你的 Linux CD-ROM 源发行版中选择一个：

- 使用以下命令查询新的 `db.cache` 文件：

  `[root@deep named]# dig @root-servers.net ns > db.cache`

- 使用 IP 地址查询新的 `db.cache` 文件，使用以下命令：

  `[root@deep named]# dig @198.41.0.4 ns > db.cache`

`db.cache` 文件应该如下所示。如果你愿意，可以使用这一个开始。

```
; <<>> DIG 9.2.1 <<>> @198.41.0.4 ns
;; global options: printcmd
;; Got answer:
;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 55980
;; flags qr aa rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 13

; QUESTION SECTION:
```

IN  NS

```

; ANSWER SECTION:
```

518400 IN NS  I.ROOT-SERVERS.NET.

518400 IN NS  E.ROOT-SERVERS.NET.

518400 IN NS  D.ROOT-SERVERS.NET.

518400 IN NS  A.ROOT-SERVERS.NET.

518400 IN NS  H.ROOT-SERVERS.NET.

518400 IN NS  C.ROOT-SERVERS.NET.

518400 IN NS  G.ROOT-SERVERS.NET.

518400 IN NS  P.ROOT-SERVERS.NET.

518400 IN NS  B.ROOT-SERVERS.NET.

518400 IN NS  J.ROOT-SERVERS.NET.

518400 IN NS  K.ROOT-SERVERS.NET.

518400 IN NS  L.ROOT-SERVERS.NET.

```

;; ADDITIONAL SECTION:
```

I.ROOT-SERVERS.NET  360000 IN A  192.36.148.17

E.ROOT-SERVERS.NET  360000 IN A  192.230.10

D.ROOT-SERVERS.NET  360000 IN A  128.80.90

A.ROOT-SERVERS.NET  360000 IN A  198.41.0.4

H.ROOT-SERVERS.NET  360000 IN A  128.63.53

C.ROOT-SERVERS.NET  360000 IN A  192.33.4.12

G.ROOT-SERVERS.NET  360000 IN A  192.11.36

F.ROOT-SERVERS.NET  360000 IN A  128.5.24

B.ROOT-SERVERS.NET  360000 IN A  128.30.10

J.ROOT-SERVERS.NET  360000 IN A  198.41.1.0

K.ROOT-SERVERS.NET  360000 IN A  193.0.14.12

L.ROOT-SERVERS.NET  360000 IN A  198.32.64

M.ROOT-SERVERS.NET  360000 IN A  202.12.27.33

```
; Query time: 25 msec
;; SERVER: 198.41.0.4 (198.41.0.4)
;; WHEN: Tue 28 11:07:43
;; SIZE rcvd: 43

注意：从互联网获取后，忘记将 `db.cache` 文件复制到名称服务器的 `/named` 目录。互联网上的服务器并不经常变化，但偶尔会有。良好的做法是每隔两个月更新一次 `db.cache` 文件。

### 步骤 2
现在，将 `db.cache` 文件的权限设置为 `(0644--rw--)`，并由用户 `'named'` 所有，组设置为 `'named'`。

- 使用命令更改 `db.cache` 文件的模式和所有者：
  `[root@deep]# chmod 644 /var/named/db.cache`
  `[root@deep]# chown named:named /var/named/db.cache`

# /var/named/db.localhost: 映射文件
此部分适用于你可能安装在系统上的所有类型的名称服务器（缓存、主或从）。"`db.localhost`" 文件通过为你的服务器提供映射来覆盖系统的 localhost 网络。所有类型的 DNS 服务器都需要此配置文件才能正常工作。

### 步骤 1
在 `/var/named` 目录下创建文件。

- 创建 `db.localhost` 文件 (`touch /var/named/db.localhost`) 文件中添加以下内容：

```
$TTL 86400

      IN SOA      localhost. root.localhost. (

                    00 ; Serial

                  10800 ; Refresh after 3 hours

                  3600 ; Retry after 1 hour

                  60480 ; Expire after 1 week

                  86400 ) Minimum

      IN NS       localhost.

      IN A        127.0.0.1
```
