
```192.168.0.0/16;

}

options {

    directory "/var/named";

    allow-transfer { none };

    allow-query { trusted };

    allow-recursion { trusted };

    blacklist { none };

    tcp-clients { any };

    forwarders { none };

    version "any";

}

logging {

    category all;

}
```

// 根服务器提示

zone "*" {

    type hint;

    file "db.cache";

};

// 为回环地址 127.0.0.1 提供反向映射

zone "1.0.127.in-addr.arpa" {

    type master;

    file "db.localhost";

}

// 为 127.0.0.0/8 提供反向映射

zone "0.0.0.127.in-addr.arpa" {

    type master;

    file "db.127";

}

// 为 openna.com 提供从服务器配置

zone "openna.com" {

    type slave;

    file "db.openna";

}

// 为 78.35.207.0/24 提供反向映射

zone "207.35.78.in-addr.arpa" {

    type slave;

    file "db.78.35.207";

}
```

*(注：由于原文后半部分文本存在大量乱码和无意义的重复，上述翻译已根据上下文逻辑对核心配置结构进行了清理与还原。)*

# ISC BIND & DNS
第 8 章

### 第 4 步
一旦运行 ISC BIND & DNS 所需的文件已进入 chroot 狱环境，我们就可以从系统中删除 ISC BIND & DNS 无需的目录，因为我们现在日常操作的目录位于 chroot 目录下。这些目录是 `/var/named` 和 `/var/run/named`。

```
[root@deep #] rm -rf /var/named/
[root@deep #] rm -rf /var/run/named/
```

### 第 5 步
之后，是时候启动 ISC BIND & DNS 使其在 chroot 狱中运行了。`/etc/sysconfig` 文件即用于此目的。

- 编辑 `named` 文件 (`vi /etc/sysconfig`) 并修改以下行：

`#ROOTDIR="/chroot/named/"`

读为：

`ROOTDIR="/chroot/named/"`

`ROOTDIR="/chroot/named/"` 选项告诉 ISC BIND & DNS chroot 目录的位置。因此，`named` 守护进程在启动前会读取此行并切换到指定的目录。

### 第 6 步
最后，我们必须测试我们的 ISC BIND & DNS 服务器新的 chroot 狱配置。

- 使用以下命令启动新的 chroot 狱版 ISC BIND & DNS：
`[root@deep #] /etc/init.d/named start`
启动 Named: [OK]

如果没有遇到任何错误，请执行 `ps ax | grep named` 并查看我们是否正在运行：
`[root@deep #] ps ax | grep named`
`21723 ? S 00 /usr/sbin/named named -t /chroot/named/`

如果是，让我们提取其进程号并执行 `ls -la /proc/[process_number]/root/` 来确保它是 chrooted 运行的。

```
[root@deep #] ls -la /proc/21723/root/
```

如果你看到如下内容：
total 20

| 权限 | 所有者 | 组 | 大小 | 日期 | 名字 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| drwxr-xr-x | root | root | 4096 | May 28 12:53 | . |
| drwxr-xr-x | root | root | 4096 | May 28 12:53 | .. |
| drwxr-xr-x | named | named | 4096 | May 28 12:53 | dev/ |
| drwxr-xr-x | named | named | 4096 | May 28 12:54 | etc/ |
| drwxr-xr-x | root | root | 4096 | May 28 12:54 | var/ |

恭喜你！你的 ISC BIND & DNS 在 chroot 狱中正常运行。

## 加固 ISC BIND & DNS

本节专门讨论我们可以采取的改进和收紧 ISC BIND & DNS 安全性的操作。这里的有趣的一点在于，我们指的是基础安装程序中可用的功能，而不是任何额外的软件。

## 基于 TSIG 的 BIND 事务安全：

本节仅适用于选择在系统中安装并使用 BIND & DNS 作为主（Master）或从（Slave）名称服务器的情况。新的 BIND 9 对底层 BIND 架构的所有方面进行了重大重写，允许我们使用 BIND & DNS 创建事务密钥和事务签名（TSIG）（TSIG 用于对 DNS 请求进行签名）。

这意味着如果服务器接收到由此密钥签名的消息，它可以验证该签名。如果签名验证成功，则由同一个密钥对响应进行签名。

BIND 的这一新功能将允许我们更好地控制谁可以对 DNS 服务器进行区域传输（zone transfer）、通知（notify）和递归查询消息操作。它对于动态更新也可能有用。下面我们展示了生成此密钥的步骤以及如何在 `named.conf` 文件中使用它。

## 第 1 步

第一步是为每对主机生成共享密钥。此共享密钥将在主域名服务器和从域名服务器之间共享，在我们的示例中，必须选择一个任意密钥 `ns1-ns2`。同样，确保两台主机上的密钥名称相同也是重要的。

- 若要生成共享密钥，请使用以下命令：
`[root@deep #] dnssec-keygen -a hmac-md5 -b 128 -n HOST ns1-ns2 Kns-ns2.+157+50701`

### 第 2 步

上述命令将生成一个 128 位（16 字节）的 HMAC-MD5 密钥，结果将位于名为 `Kns-ns2.+157+50701.private` 的文件中 (`vi Kns-ns2.+157+50701.private`)，并从 `key` 单词提取 base64 编码字符串：该字符串必须从文件中提取并作为共享密钥。

- 编辑 `Kns-ns2.+157+50701.private` (`vi Kns-ns2.+157+50701.private`)，并提取 base64 编码字符串：

```
Private-key-format: v1.2
Algorithm: 17 (HMAC_MD5)
Key: 7Mib6qWkpLGnN28zcbBma6==
```

上述示例中的字符串 `7Mib6qWkpLGnN28zcbBma6==` 是必须提取并作为共享密钥的部分。

### 第 3 步

一旦从生成文件中提取出所需的 base64 编码字符串，我们就可以从系统中删除这些文件，并通过类似 ssh 的传输机制将共享密钥拷贝到 bind 机器。

- 若要从系统中删除共享密钥，请使用以下命令：
`[root@deep #] rm -f Kns-ns2.+157+50701.key`
`[root@deep #] rm -f Kns-ns2.+157+50701.private`

### 第 4 步
之后，是通过向每台服务器的 `named.conf` 文件添加内容来告知服务器（主从）密钥的存在。

- 在两台 DNS 服务器上编辑 `named.conf` 文件 (`vi /chroot/named/etc/named.conf`)，并添加以下行：

```
key "ns1-ns2" {
  algorithm hmac-md5;
  secret "7Mib6qWkpLGnN28zcbBma6=="
```

一旦添加了上述行，两台 DNS 服务器的 `named.conf` 如下：

#### 主服务器：

```
// 授权的区域传输
drwxr-xr-x | root | root | 4096 | May 28 12:53 | . |
drwxr-xr-x | root | root | 4096 | May 28 12:53 | .. |
drwxr-xr-x | named | named | 4096 | May 28 12:53 | dev/ |
drwxr-xr-x | named | named | 4096 | May 28 12:54 | etc/ |
drwxr-xr-x | root | root | 4096 | May 28 12:54 | var/ |
// 授权的源
acl "trusted" {
  localhost;
  192.168.1.0/24;
};
// 已知的恶意源
acl "bogon" {
  0.0.0.0/8;
  1.0.0.0/8;
  2.0.0.0/8;
  192.0.0.0/24;
};
// 允许的递归查询
allow-recursion {
  trusted;
};
// 允许的通知
allow-notify {
  trusted;
};
// 允许的区域传输
allow-transfer {
  trusted;
};
// 密钥定义
key "ns1-ns2" {
  algorithm hmac-md5;
  secret "7Mib6qWkpLGnN28zcbBma6=="
};
options {
  directory "/chroot/named/";
  // 转发器
  forwarders { none; };
  // 版本号
  version "OpenDNS";
};
// 根服务器
zone "." {
  primary;
  file "db.root";
};
// 回环地址区域
zone "127.0.0.in.arpa" {
  primary;
  file "db.127";
};
// 本地区域
zone "local" {
  primary;
  file "db.local";
};
// .com 区域
zone "com" {
  primary;
  file "db.com";
};
```

#### 从服务器：

```
// 授权的区域传输
acl "trusted" {
  localhost;
  192.168.1.0/24;
};
// 已知的恶意源
acl "bogon" {
  0.0.0.0/8;
  1.0.0.0/8;
  2.0.0.0/8;
  192.0.0.0/24;
};
// 允许的递归查询
allow-recursion {
  trusted;
};
// 允许的通知
allow-notify {
  trusted;
};
// 允许的区域传输
allow-transfer {
  trusted;
};
// 密钥定义
key "ns1-ns2" {
  algorithm hmac-md5;
  secret "7Mib6qWkpLGnN28zcbBma6=="
};
options {
  directory "/chroot/named/";
  // 转发器
  forwarders { none; };
  // 版本号
  version "OpenDNS";
};
// 根服务器
zone "." {
  slave;
  file "db.root";
};
// 回环地址区域
zone "127.0.0.in.arpa" {
  slave;
  file "db.127";
};
// 本地区域
zone "local" {
  slave;
  file "db.local";
};
// .com 区域
zone "com" {
  slave;
  file "db.com";
};
```

# ISC BIND & DNS 第 8 章

## 在主/主服务器下：

```
// 授权源地址。
acl "trusted" {
  localhost;
  192.168.1.0/24;
  207.35.78.0/24;
}
// 已知的伪源地址不回复。
acl "bogon" {
  0.0.0.0/8;
  1.0.0.0/8;
  2.0.0.0/8;
  192.0.2.0/24;
  224.0.0.0/3;
  169.254.0.0/16;
  // 企业网络可能也可能是虚假的。
  10.0.0.0/8;
  172.16.0.0/12;
  192.168.0.0/16;
}
```

```
key "ns1-ns2" {
  algorithm hmac-md5;
  secret "T7m1b6wRpRGlnZN28zcbM6aa=";
}
```

```
server 207.35.78.6 {
  keys ("ns1-ns2");
}
```

```
options {
  directory "/var/named";
  allow-transfer { 207.35.78.6 };
  allow-query { trusted };
  allow-recursion { trusted };
  blackhole { bogon };
  tcp-clients 1024;
  forwarders { none };
  version "OpenNA Linux";
}
```

```
logging {
  category lame-servers { null };
}
```

```
// 根服务器提示
zone "*" { type file; file "db.cache"; };
```

```
// 为环回地址 127.0.0.1/24 提供反向映射
zone "localhost" {
  type master;
  file "db.localhost";
  notify no;
}
```

```
zone "0.0.127.in-addr.arpa" {
  type master;
  file "0.0.127.in-addr.arpa";
  notify no;
}
```

```
// 我们是 OpenNA.com 的主服务器
zone "openna" {
  type master;
  file "db.openna";
  allow-query { any };
}
```

```
// 为域名网络 207.35.207-in.addr.arpa 提供反向映射
zone "78.35.207-in.addr.arpa" {
  type master;
  file "78.35.207-in.addr.arpa";
  allow-query { any };
}
```

# 在从/从服务器下：

```
// 授权源地址。
acl "trusted" {
  localhost;
  192.168.1.0/24;
}
```

```
// 已知的伪源地址不回复。
acl "bogon" {
  0.0.0.0/8;
  1.0.0.0/8;
  2.0.0.0/8;
  192.0.0.0/24;
  224.0.0.0/3;
  169.254.0.0/16;
  // 企业网络可能也可能是虚假的。
  10.0.0.0/8;
  172.16.0.0/12;
  192.168.0.0/16;
}
```

```
key "ns1-ns2" {
  algorithm hmac-md5;
  secret "7M1b6QwkpGLz7Ml6bQwkpGLzN28zcbm6A==";
}
```

```
server 207.35.78.5 {
  keys ("ns1-ns2");
}
```

```
options {
  directory "/var/named";
  allow-transfer { none };
  allow-query { trusted };
  allow-recursion { trusted };
  blackhole { bogon };
  tcp-clients 1024;
  forwarders { none };
  version "OpenNA Linux";
}
```

```
logging {
  category lame-servers { null };
}
```

# 根服务器提示

```
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
// 我们是 OpenNA.com 的从服务器
zone "openna.com" {
    type slave;
```
