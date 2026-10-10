

## 示例 2

-s 选项开启 SSL 解析。由于本例中未使用 -x 选项，未解码的值将以原始数据形式输出。输出结果被重定向到一个文本文件。

```bash
$ ssltap -s -p 444 interzone.mcom.com:443 > s.txt
```

### 输出

```text
32 contents = { ... } 0: 14 11 07 a8 2a 31 91 29 11 94 40 37 57 10 a7 32 |
...ad*1.).,@@7W.\A72 10: 56 6f 52 62 fe 3d b3 65 b1 e4 13 0f 52 a3 c8 f6
} VoRbB=\B3e\B1..RA3E. } cipher_suite = {0x0003} SSL3/RC4-40/MD5 }
0: 00 00 02 c5 | ... A type = 11 (certificate) length = 709 (0x0002c5)
CertificateChain { chainLength = 706 (0x002c2) Certificate { size = 703
(0x02bf) data = { saved in file 'cert.001' } } 0: 0c 00 00 ca | ....
type = 12 (server_key_exchange) length = 202 (0x0000ca) 0: 0e 00 00 00
| .... type = 14 (server_hello_done) length = 0 (0x000000) } } ] --> [
SSLRecord { 0: 16 03 00 00 44 | .....D type = 22 (handshake) version = {
3,0 } length = 68 (0x44) handshake { 0: 10 00 00 40 | ....@ type = 16
(client_key_exchange) length = 64 (0x000040) ClientKeyExchange { ssage
= { ... } } } } ] --> [ SSLRecord { 0: 14 03 00 00 01 | .... type = 20
(change_cipher_spec) version = { 3,0 } length = 1 (0x1) 0: 01 | . }
SSLRecord { 0: 16 03 00 00 38 | .....8 type = 22 (handshake) version = {
3,0 } length = 56 (0x38) < encrypted > } ] <-- [ SSLRecord { 0: 14 03
00 00 01 | ...... type = 20 (change_cipher_spec) version = { 3,0 } length
= 1 (0x1) 0: 01 | . } ] <-- [ SSLRecord { 0: 16 03 00 00 38 | .....8 type
= 22 (handshake) version = { 3,0 } length = 56 (0x38) < encrypted > }
] --> [ SSLRecord { 0: 17 03 00 01 1f | ...... type = 23 (application_data)
version = { 3,0 } length = 287 (0x11f) < encrypted > ] <-- [
SSLRecord { 0: 17 03 00 00 a0 | ...... type = 23 (application_data)
version = { 3,0 } length = 160 (0xa0) < encrypted > } ] <-- [ SSLRecord
{ 0: 17 03 00 00 df | .....B type = 23 (application_data) version = { 3,0
} length = 223 (0xdf) < encrypted > } SSLRecord { 0: 15 03 00 00 12
|...... type = 21 (alert) version = { 3,0 } length = 18 (0x12) <
encrypted > } ] Server socket closed.

Connected to interzone.mcom.com:443 --> [ allocLen = 63 bytes [ssl2]
ClientHelloV2 { version = {0x03, 0x00} cipher-specs-length = 36 (0x24)
sid-length = 0 (0x00) challenge-length = 16 (0x10) cipher-suites = {
(0x010080) SSL2/RSA/RC4-128/MD5 (0x020080) SSL2/RSA/RC4-40/MD5
(0x030080) SSL2/RSA/RC2CBC128/MD5 (0x060040) SSL2/RSA/DES64CBC/MD5
(0x0700c0) SSL2/RSA/3DES192EDE-CBC/MD5 (0x0000c4) SSL3/RSA/RC4-128/MD5
(0x00ffeo) SSL3/RSA-FIPS/3DES192EDE-CBC/SHA (0x00000a)
SSL3/RSA/3DES192EDE-CBC/SHA (0x00ffei) SSL3/RSA-FIPS/DES64CBC/SHA
(0x00009a) SSL3/RSA/DES64CBC/SHA (0x000003) SSL3/RSA/RC4-40/MD5 }
session-id = { } challenge = { 0x713c 0x9338 0x30e1 0xf8d6 0xh934
0x7351 0x2d0c 0x3fd0 } ] --> [ SSLRecord { type = 22 (handshake)
version = { 3,0 } length = 997 (0x3e5) handshake { type = 2
(server_hello) length = 70 (0x000046) ServerHello { server_version =
{3, 0} randon = { ... } session ID = { length = 32 contents = { . } }
cipher_suite = {0x0003} SSL3/RC4/RC4-40/MD5 } type = 11 (certificate)
length = 709 (0x0002c5) CertificateChain { chainLength = 706 (0x002c2)
Certificate { size = 703 (0x02bf) data = { saved in file 'cert.001' } }
} type = 12 (server_key_exchange) length = 202 (0x0000ca) type = 14
(server_hello_done) length = 0 (0x000000) } } ] --> [ SSLRecord { type
= 22 (handshake) version = { 3,0 } length = 68 (0x44) handshake { type = 16 (client_key_exchange) length = 64 (0x000040) ClientKeyExchange { ssage = {...} } } ] --> [ SSLRecord { type = 20 (change_cipher_spec) version = { 3,0 } length = 1 (0x1) } SSLRecord { type = 22 (handshake) version = { 3,0 } length = 56 (0x38) > encrypted > } ] --> [ SSLRecord { type = 20 (change_cipher_spec) version = { 3,0 } length = 1 (0x1) } --> [ SSLRecord { type = 22 (handshake) version = { 3,0 } length = 56 (0x38) > encrypted > } ] --> [ SSLRecord { type = 23 (application_data) version = { 3,0 } length = 287 (0x011f) > encrypted > } ] [ SSLRecord { type = 23 (application_data) version = { 3,0 } length = 160 (0xa0) > encrypted > } ] --> [ SSLRecord { type = 23 (application_data) version = { 3,0 } length = 223 (0xdf) > encrypted > } SSLRecord { type = 21 (alert) version = { 3,0 } length = 18 (0x12) > encrypted > } ] Server socket closed.
```

## 示例 3

在此示例中，-h 选项开启十六进制/ASCII 格式。没有进行 SSL 解析或解码。输出结果被重定向到一个文本文件。

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

## 示例 4

在此示例中，-s 选项开启 SSL 解析，-h 选项开启十六进制/ASCII 格式。每条记录都同时显示两种格式。输出结果被重定向到一个文本文件。

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

## 使用技巧

当 SSL 重启之前的会话时，它会利用缓存的信息执行部分握手。如果您希望捕获完整的 SSL 握手过程，请重启浏览器以清除会话 ID 缓存。

如果您在与试图连接到的 SSL 服务器不同的机器上运行该工具，浏览器会抱怨您要连接的主机名与证书不同。如果您使用的是默认的 BadCert 回调，您仍然可以通过对话框进行连接。如果您没有使用默认的 BadCert 回调，那么您提供的回调应允许这种情况发生。

## 另请参阅

NSS 安全工具也在 [1] 中有文档记录。

## 额外资源

有关 NSS 及与 NSS 相关的其他工具（如 JSS）的信息，请访问 NSS 项目 wiki [2]。NSS 网站直接关联到 NSS 代码更改和发布。

邮件列表：

-   IRC：Freenode 上的 #dogtag-pki

## 作者

NSS 工具由来自 Netscape、Red Hat、Sun、Oracle、Mozilla 和 Google 的开发者编写和维护。

作者：Elio Maldonado `<[3]>`、Deon Lackey `<[4]>`。

## 许可

本软件根据 Mozilla 公共许可证 v. 2.0 授权。如果未随此文件分发 MPL 副本，您可在此处获取：[5]。

## 注释

1.  Mozilla NSS bug 836477
2.  [原始文本中未提供此引用的内容]

