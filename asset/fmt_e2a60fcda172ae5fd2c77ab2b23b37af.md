
### 示例 3

在此示例中，`-h` 选项开启十六进制/ASCII 格式。没有进行 SSL 解析或解码。输出结果被重定向到一个文本文件。

```bash
$ ssltap -h -p 444 interzone.mcom.com:443 > h.txt
```

### 输出

```text
Connected to interzone.mcom.com:443 --> [ 0: 80 40 01 03 00 00 27 00 00 00 10 01 00 80 02 00 | .@..........
10: 80 03 00 80 04 00 80 06 00 40 07 00 c0 00 04 | .
20:...00 ff e0 00 00 00 ff e1 00 00 00 00 03 00 | ........a......
30: 00 06 9b fe 5b 56 96 49 1f 9f ca dd d5 ba b9 52 | ..p[V.I.\xd9..0m\b9R
40: 6f 2d [ o - ] --> [ 0: 16 03 00 03 e5 02 00 00 46 03 00 7f e5 0d 1b 1d | h.:y'...<..F......
10: 68 7f 3a 79 60 d5 17 3c 1d 9c 96 b3 88 d2 69 3b | h.:y'...<..F......
10: 68 7f 3a 79 60 d5 17 3c 1d 9c 96 b3 88 d2 69 3b | h.:y'...<..F......
10: 68 7f 3a 79 60 d5 17 3c 1d 9c 96 b3 88 d2 69 3b | h.:y'...<..F......
```

### 示例 4

在此示例中，`-s` 选项开启 SSL 解析，`-h` 选项开启十六进制/ASCII 格式。每条记录都同时显示两种格式。输出结果被重定向到一个文本文件。

```bash
$ ssltap -hs -p 444 interzone.mcom.com:443 > hs.txt
```

### 输出

```text
Connected to interzone.mcom.com:443 - > [ 0: 80 3d 01 03 00 00 24 00 00 00 10 01 00 80 02 00 | . = . . . . . $ . . . . . . . . .
10: 80 03 00 80 04 00 80 06 00 40 07 00 c0 00 00 04 | .
20: 00 ff e0 00 00 0a 00 ff e1 00 00 09 00 00 03 03 | . . . . . . . . . . a . . . . . .
30: 55 e6 e4 99 79 c7 d7 2c 86 78 96 5d b5 cf e9 | U . . y & Ccedil ; xb0 . . x . ] ß 5 & Iu ; é
allocLen = 63 bytes [ ssl2 ]
ClientHelloV2 { version = { 0x03, 0x00 } cipher-specs-length = 36 ( 0x24 ) sid-length = 0 ( 0x00 ) challenge-length = 16 ( 0x10 )
cipher-suites = {
( 0x010080 ) SSL2 / RSA / RC4 - 128 / MD5
( 0x020080 ) SSL2 / RSA / RC4 - 40 / MD5
( 0x030080 ) SSL2 / RSA / RC2CBC128 / MD5
( 0x040080 ) SSL2 / RSA / RC2CBC40 / MD5
( 0x060040 ) SSL2 / RSA / DES64CBC / MD5
( 0x0700c0 ) SSL2 / RSA / 3DES192EDE - CBC / MD5
( 0x000004 ) SSL3 / RSA / RC4 - 128 / MD5
( 0x00ffeo ) SSL3 / RSA - FIPS / 3DES192EDE - CBC / SHA
( 0x00000a ) SSL3 / RSA / 3DES192EDE - CBC / SHA
( 0x00ff1 ) SSL3 / RSA - FIPS / DES64CBC / SHA
( 0x000009 ) SSL3 / RSA / DES64CBC / SHA
( 0x000003 ) SSL3 / RSA / RC4 - 40 / MD5
}
session - id = { }
challenge = { 0x0355 0xe6e4 0x9979 0xc7d7 0x2c86 0x7896 0x5db 0xcfe9 }
}
]
< additional records in sa formats >
Server socket closed.
```

### 使用技巧

当 SSL 重启之前的会话时，它会利用缓存的信息执行部分握手。如果您希望捕获完整的 SSL 握手过程，请重启浏览器以清除会话 ID 缓存。

如果您在与试图连接到的 SSL 服务器不同的机器上运行该工具，浏览器会抱怨您要连接的主机名与证书不同。如果您使用的是默认的 BadCert 回调，您仍然可以通过对话框进行连接。如果您没有使用默认的 BadCert 回调，那么您提供的回调应允许这种情况发生。

### 另请参阅

NSS 安全工具也在 [1] 中有文档记录。

### 额外资源

有关 NSS 及与 NSS 相关的其他工具（如 JSS）的信息，请访问 NSS 项目 wiki [2]。NSS 网站直接关联到 NSS 代码更改和发布。

邮件列表：

- IRC：Freenode 上的 `#dogtag-pki`

### 作者

NSS 工具由来自 Netscape、Red Hat、Sun、Oracle、Mozilla 和 Google 的开发者编写和维护。

作者：Elio Maldonado `<[3]>`、`Deon Lackey` `<[4]>`。

### 许可

本软件根据 Mozilla 公共许可证 v. 2.0 授权。如果未随此文件分发 MPL 副本，您可在此处获取：[5]。

### 注释

1. Mozilla NSS bug 836477

2. [原始文本中未提供此引用的内容]

### sss_ssh_authorizedkeys

### 名称

`sss_ssh_authorizedkeys` - 获取 OpenSSH 授权密钥

### 概要

`sss_ssh_authorizedkeys` [选项] 用户

### 描述

`sss_ssh_authorizedkeys` 获取用户 `USER` 的 SSH 公钥，并以 OpenSSH authorized_keys 格式（有关更多信息，请参见 (8) 中的“AUTHORIZED_KEYS 文件格式”章节）输出它们。

如果 (8) 编译时支持 “AuthorizedKeysCommand” 或 “PubkeyAgent”(5) 选项，则可以配置为使用 `sss_ssh_authorizedkeys` 进行公钥用户身份验证。

如果支持 “AuthorizedKeysCommand”，可以在 (5) 中放入以下指令来配置 (8) 使用它：

```
AuthorizedKeysCommand /usr/bin/sss_ssh_authorizedkeys
AuthorizedKeysCommandUser nobody
```

如果支持 “PubkeyAgent”，可以通过使用以下指令来配置 (8) 使用它：

```
PubkeyAgent /usr/bin/sss_ssh_authorizedkeys %u
```

### 选项

- `-d, --domain DOMAIN`

  在 SSSD 域 `DOMAIN` 中搜索用户公钥。

- `-?, --help`

  显示帮助信息并退出。

### 退出状态

成功时，返回值为 0。否则，返回 1。

### 参见

(8), (5), (5), (5), (5), (5), (5), (5),(8), (8), (8), (8), (8), (8), (8), (8), (8), (8), (8), (8), (8), (8), (5),(8). (5)

### 作者

SSSD 上游项目 -

### sss_ssh_knownhostsproxy

### 名称

`sss_ssh_knownhostsproxy` - 获取 OpenSSH 主机密钥

### 概要

`sss_ssh_knownhostsproxy` [选项] 主机 [代理命令]

### 描述

`sss_ssh_knownhostsproxy` 获取主机 `HOST` 的 SSH 主机公钥，将它们存储在自定义的 OpenSSH known_hosts 文件中（有关更多信息，请参见 (8) 中的“SSH_KNOWN_HOSTS 文件格式”章节），即 `/var/lib/sss/pubconf/known_hosts`，并建立到该主机的连接。
