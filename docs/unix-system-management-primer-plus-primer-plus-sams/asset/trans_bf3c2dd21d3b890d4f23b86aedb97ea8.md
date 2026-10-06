

# 38 UNIX 系统管理入门进阶

新用户 ID："Joe User <joeuser@example.com>"。
来自密钥 ID 0XA38C5D0 的新签名，用户 ID Joe User <joeuser@example.com>

已添加：

- 新密钥(s)
- 新签名(s)
- 新用户 ID(s)

# 列出密钥环内容

你可以通过输入 `ppg -kv` 来列出密钥环的内容。有些人有许多电子邮件地址，如果你忘记了某个密钥是注册在哪个人的密钥环中的，可以使用此命令。

Nancy 现在为 Joe 的公钥签名，这证明了该公钥确实属于 Joe。否则，PGP 会不断警告你该公钥未证明属于 Joe。`ppg -ks` 对密钥进行签名，如下所示：

```bash
pgp -ks joeuser@example.com
Pretty Good Privacy(tm) Version 6.5.8
(c) 1999 Network Associates Inc.
Uses the RSAREF(tm) Toolkit, which is copyright RSA Data Security, Inc.
Export of this software may be restricted by the U.S. government.
```

用于签名的私钥。
你没有指定用户 ID 来选择你的私钥，将使用默认签名密钥集，否则将使用默认用户 ID 以及私钥密钥环中最近添加的密钥。
用户 ID 的密钥：Joe User <joeuser@example.com>
1024 位 DSS 密钥 0XA38C5D0，创建于 2002/04/20

```
Key fingerprint = 0A 16 68 8B FD D9 0F 01 ID EF 08 AD 12 53 64 6E C
```

易读性确认：根据你的直接第一手知识，你是否绝对确定已准备好庄重承诺，上述公钥确实属于上述用户 ID 所指定的的用户 (y/N)？y
你需要一个短语来解锁你的私钥。
用户 ID "nancy@example.com" 的密钥
输入短语：
短语正确

最后，Nancy 现在可以使用 `ppg -ea` 使用 Joe 的公钥加密文件（`a` 是必要的，将加密文件存储为 ASCII 格式以便通过电子邮件传输）。`ppg -ea` 的语法如下：

ppg -ea file userid [other users]
如果 Nancy 想要加密每条消息，用 Joe 的公钥加密的命令看起来像这样：

```bash
pgp -ea message joeuser@example.com
Pretty Good Privacy(tm) Version 6.5.8
(c) 1999 Network Associates Inc.
```

# 第13 章 实现系统安全

使用了 RSAREF(tm) Toolkit，版权归 RSA Data Security, Inc. 所有。
该软件的导出可能受到美国政府的限制。

接收者的公钥将用于加密。

用户 ID 的密钥：Joe User <joeuser@example.com>
1024 位 DSS 密钥，密钥 ID 0CA38C5D0，创建于 2002/04/20

传输装甲文件：message.asc
加密后的文件存储在 message.asc 中，其格式如下：

```
--- BEGIN PGP MESSAGE ---
Version: PGP 6.5.8
QAN1RDBE4DL509YCrvxQBAQ6/s0xizuenQ+Y7e2Ij3JQ0C9gecuUwboSBi4
G5N4B81p4F3ZL3u00KZt44pA2ulIFGkhzthuuyY8SAYJokKMF400pgn5mtP
Y1JB5A689Y71f17M9uAELK+kqtIGHYpJpauVv01ss38Yw7Hcd0b6dpl1gc4+cx
CCZNPGQ022XhI4FXRAE1Qub4D1Y2RAWW86HK69YwaXRfGPUSC3siJs16
JApKmIMQgN45g5ffipYk15axWI5knf1Te65S3YUR4a908f6Jb7EY/Q+L1kDG8
GyukltUA/Q2WIFFAXRI3BYXVYwLznkf1Te65SR9rwGy5hZ59yrhu5UJ9TZCL+bLIN1T9w40QibBuEI3XIa
C14MgowGpcfpkBBRGI4M55Nhm9iF50CguGh5Qhm3Mr321JnU0Y3BH4+40QibEu3XIa
N67iYEFJ3LB14/cr12/YTvVsek9w4R9055cltXv4```
易读性确认：根据你的直接第一手知识，你是否绝对确定已准备好庄重承诺，上述公钥确实属于上述用户 ID 所指定的的用户 (y/N)？y
你需要一个短语来解锁你的私钥。
用户 ID "nancy@example.com" 的密钥
输入短语：
短语正确

最后，Nancy 现在可以使用 `ppg -ea` 使用 Joe 的公钥加密文件（`a` 是必要的，将加密文件存储为 ASCII 格式以便通过电子邮件传输）。`ppg -ea` 的语法如下：

[content]
Pretty Good Privacy(tm) Version 6.5.8
(c) 1999 Network Associates Inc.
Uses the RSAREF(tm) Toolkit, which is copyright RSA Data Security, Inc.
Export of this software may be restricted by the U.S. government.
