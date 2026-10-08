
```
tcpdump -vv -x -X -s 1500 'port 80'
```

当此命令正在运行时，我随后生成了更多的 Web 流量。以下是结果中的两个半数据包，从三次握手刚刚结束处开始捕获：

```
18:18:51.986230 IP (tos 0x0, ttl 64, id 10907, offset 0, flags [DF], \
            length: 513) client.braingia.org.4564 > test.example.com.www: \
            P [tcp sum ok] 1:462(461) ack 1 win 5840 <nop,nop,timestamp \
            250295308 1320440053>
```

```
0x0000: 0090 2741 78f0 00e0 1833 2ee8 0800 4500 ...Ax...3...E.
0x0010: 0201 2a9b 4000 4006 044b c0a8 010a 455d ...@.0..K...E]
0x0020: 0302 11d4 0050 0c9b 1ea0 9627 33f8 801b ....P.....'3...
0x0030: 16d0 4915 0000 0101 080a 0eeb 340c 4eb4 ...I......4.N.
0x0040: 50f5 4745 5420 2f20 4854 5450 2f31 2e30 P.GET.HTTP/1.0
0x0050: 0d0a 486f 7374 3a20 7777 7772 6272 6169 ..Host:.www.brai
0x0060: 6e67 6961 2e6f 7267 0d0a 4163 6570 7420 nea.org..Accept
0x0070: 3a20 7465 7874 2f68 746d 6c2c 2074 6578 :.text/html,.tex
0x0080: 742f 7061 696e 742c 2061 7070 6c69 6361 t/paint,.applica
0x0090: 7469 6f6e 2f6d 7377 6f72 642c 2061 7070 tion/msword,.app
0x00a0: 6c69 6361 7469 6f6e 2f70 6466 2c20 6170 lication/pdf,.ap
0x00b0: 706c 6963 6174 696f 6e2f 6f63 7465 7420 plication/octet-
0x00c0: 7374 7265 616d 2c20 6170 706c 6963 6174 stream,.applicat
0x00d0: 696f 6e2f 782d 7472 6f66 662c 2061 7070 ion/x-troff,.app
0x00e0: 6170 6c69 6361 7469 6f6e 2f 7274 6620 application/rtf,
0x00f0: 6369 6f6e 2f70 6f73 7473 6372 6970 742c cion/postscript,
0x0100: 6e2e 2f2f 3b22 2e2a 2c2e 2a20 3b71 3d30 n..//;;.. .;q=0
0x0110: 2e2c 2e2f 3b24 2c2e 2a2a 3b24 2c 20 6163 c.,./;$. .**;.$ .ac
0x0120: 6365 7074 2d65 6e63 6f64 696e 673a 2032 cept-encoding: 2
0x0130: 677a 6970 2c20 636f 6d70 7265 7373 2e67 zip,.compress.g
0x0140: 686f 7374 3a20 7465 7374 2e65 7861 6d70 host:.test.examp
0x0150: 6c65 2e63 6f6d 0d0a 5573 6572 2d41 6765 le.com..User-Age
0x0160: 6e74 3a20 4c69 6e75 7820 322e 342e 340d nt:.Linux.2.4.4.
0x0170: 0a53 534c 2f31 2e30 2e38 0a50 4f53 542e .SSL/1.0.8.POST.
0x0180: 436f 6e74 656e 742d 4c65 6e67 7468 3a20 Content-Length:
0x0190: 302c 2043 6f6e 7465 6e74 2d74 7970 653a 0,.Content-type:
0x01a0: 206d 756c 7469 7061 7274 3b20 626f 756e .multipart;.boun
0x01b0: 6461 7279 3d2d 2d2d 2d2d 2d2d 2d2d 2d2d dary:----------
0x01c0: 2d2d 2d2d 2d2d 2d2d 2d34 3434 3434 3434 ------------444444
0x01d0: 3434 3434 3434 342e 0d0a 436f 6e74 656e 444444444..Conten
0x01e0: 742d 4469 7370 6f73 6974 696f 6e3a 2074 t-Disposition: t
0x01f0: 6578 7420 6e61 6d65 3d22 4d69 6d65 4374 xt.name="MimeCt
0x0200: 7473 4368 6172 7365 7473 6361 7273 6574 tsCharset;charset
```

```
18:18:52.039595 IP (tos 0x0, ttl 48, id 25346, offset 0, flags [DF], \
            length: 52) test.example.com.www > client.braingia.org.4564: \
            [tcp sum ok] 1:1(0) ack 462 win 6432 <nop,nop,timestamp \
            1320440059 250295308>
```

```
0x0000: 00e0 0090 2741 78f0 0800 4500 ...3...'Ax...E.
0x0010: 0034 6302 4000 306e 0db0 1b5d 0302 4088 .4c@...n.]..@
0x0020: 010a 0050 11d4 9627 33f8 0c9b 206d 8010 ...P..34...m...
0x0030: 1920 6799 0000 0101 080a 4eb4 50fb 0eeb ..g......N.P...
0x0040: 340c              4.
```

```
18:18:52.047021 IP (tos 0x0, ttl 48, id 25347, offset 0, flags [DF], \
            length: 1500) test.example.com.www > client.braingia.org.4564: \
            . 1:1449(1448) ack 462 win 6432 <nop,nop,timestamp \
            1320440059 250295308>

0x0000: 00e0 1833 2ee8 0090 2741 78f0 0800 4500 ...3...'Ax...'E.
0x0010: 05dc 6303 4000 3006 d807 455d 032c c0a8 ...C.@...E]...
0x0020: 010a 0050 11d4 9627 33f8 0c9b 206d 8010 ...P..'3....m.
0x0030: 1920 b9f7 0000 0101 080a 4eb4 50fb 0eeb ..N.P...
0x0040: 340c 4854 5450 2f31 2e31 2032 3030 204f 4.HTTP/1.1.20.O
0x0050: 4b0d 0a44 6174 653a 2054 7565 2c20 3237 K.Date:'Tue',.27
0x0060: 204a 756e 2032 3030 3420 3233 3a31 3a30 .Jun.2004.23:19:
0x0070: 3030 2047 4d54 0d0a 5365 7276 6572 3a20 00.GMT..Server: :
0x0080: 4170 6163 6865 2f31 2e33 2e32 202855 Apac he/1.3.26. (U
0x0090: 6e69 7829 2e44 6562 6961 6e2e47 4e55 00..GNU
0x00a0: 4c69 6e75 78206d 6f64 6572 742f 302e 3131 Linux mod perl/0.11
0x00b0: 2e31 3120 6d6f 645f 7065 726c 2f31 2e32 .mod_perl/1.2
0x00c0: 360d 0a43 6f6e 6e65 6374 696f 6e3a 2063 .Connection: c
0x00d0: 6c6f 7365 0d0a 436f 6e74 656e 742d 5479 .lose. Content-Ty
0x00e0: 7065 3a20 7465 7874 2f68 746d 6c3b 2063 pe.text/html;.c
0x00f0: 6861 7273 6574 3d69 736f 3b38 3835 392d harset=iso;8859-
```

请注意，此输出包含一个实际的请求（参见第一个数据包，靠近 `GET / ..HTTP/1.0` 的位置），还包含来自 Web 服务器响应的一部分。所有这些流量都是明文，因为 HTTP 未加密。此输出同时包含十六进制和 ASCII。要获取仅包含 ASCII 的输出，请从命令中移除 `-x` 和 `-X`，并用单个 `-A` 替换它们。我个人认为，在某些情况下，双十六进制和 ASCII 输出很有帮助。

这就是使用 TCPDump 捕获 HTTP 流量的全部内容。该命令明显的改进方法是扩展表达式，以查找特定的源或目标。理解这一点很重要：按照给出的命令，只能找到端口 80 上的流量。如果您在另一个端口上运行 HTTP 流量，请用该端口替换（或除了）示例命令中找到的端口。

## 捕获 SMTP 会话

捕获 SMTP 会话与捕获 HTTP 会话并无不同。从您想使用的基本 TCPDump 选项开始，然后构建一个表达式来获取合适类型的数据，包括协议、端口以及源或目标主机。例如，以下是捕获端口 25 流量的简单示例，并附带我惯用的 TCPDump 选项：

```
tcpdump -vv -x -X -s 1500 'port 25'
```

正如您可能预期的那样，TCP 三次握手再次出现：

```
20:40:08.638690 murphy.debian.org.45772 > test.example.com.smtp: \\
S [tcp sum ok] 1485971964:1485971964(0) win 5840 <mss 1460, \\
sackOK,timestamp 795074473 0,nop,wscale 0> (DF) \\
(ttl 57, id 65109, len 60)
0x0000 4500 003c fe55 4000 3906 deae 9252 8a06 E..<.U@9.....R..
0x0010 455d 0302 b2cc 0019 5892 21fc 0000 0000 E]......X.!....
0x0020 a002 16d0 8ffe 0000 0204 05b4 0402 080a
0x0030 2f63 dfa9 0000 0000 0103 0300 /c.......
```

```
20:40:08.638769 test.example.com.smtp > murphy.debian.org.45772: S \\
[tcp sum ok] 2853594323:2853594323(0) ack 1485971965 win 5792 \\
<mss 1460,sackOK,timestamp 1321286843 795074473,nop,wsscale 0> \\
(DF) (ttl 64, id 0, len 60)
0x0000 4500 003c 0000 4000 4006 d604 455d 0302 E.<.@...E].@.E]..
0x0010 9252 8a06 0019 b2cc aa16 64d3 5892 21fd .R........d.X..!
0x0020 a012 16a0 f5b6 0000 0204 0402 080a .........
0x0030 4ec1 3cbb 2f63 dfa9 0103 0300 N.</c....
```

```
20:40:08.640600 murphy.debian.org.45772 > test.example.com.smtp: . \\
[tcp sum ok] 1:1(0) ack 1 win 5840 <nop,nop,timestamp \\
795074473 1321286843> (DF) (ttl 57, id 65110, len 52)
0x0000 4500 0034 fe56 4000 3906 deb5 9252 8a06 E.4.V@9.....R..
0x0010 455d 0302 b2cc 0019 5892 21fd aa16 63d4 E]......X.!...d.
0x0020 8010 16d0 244c 0000 0101 080a 2f63 dfa9 ....$L......../c..
0x0030 4ec1 3cbb N.<.
```

在三次握手过程中，确实没有什么新奇的有趣内容。不过，请注意，在三次握手期间，ASCII 输出并没有太大用处。

与 HTTP 一样，在初始 TCP 握手完成后，SMTP 会话也随之展开：

```
20:40:08.683352 test.example.com.smtp > murphy.debian.org.45772: P \\
[tcp sum ok] 1:51(50) ack 1 win 5792 <nop,nop,timestamp \\
1321286848 795074473> (DF) (ttl 64, id 22639, len 102)
0x0000 4500 0066 586f 4000 4006 77db 455d 0302 E..fx@.0.0...E].fx@.]...]..
0x0010 9252 8a06 0019 b2cc aa16 64d4 5892 21fd .R........d.X..!
0x0020 8018 16a0 bd07 0000 0101 080a 4ec1 3cc0 .........N<
0x0030 2f63 dfa9 3232 3020 6466 7730 2e69 6367 /c..22 0df fw0.ei cg
0x0040 6d65 6469 611e 636f 6d20 4553 5020 204c mpe.dia.co m ESP. ll
0x0050 506f 7374 6669 7820 2844 6562 6961 6e2f Postfix. (Debian/
0x0060 474e 5529 000a GNU)
```

```
20:40:08.684581 murphy.debian.org.45772 > test.example.com.smtp: . [tcp sum ok]
1:1(0) ack 51 win 5840 <nop,nop,timestamp 795074478 1321286848> (DF) (ttl 57, i
d 65111, len 52)
0x0000 4500 0034 fe57 4000 3906 deba 9252 8a06 E.4.W@9.....R..
0x0010 455d 0302 b2cc 0019 5892 21fd aa16 6506 E]......X.!...e.
0x0020 8010 16d0 2410 0000 0101 080a 2f63 dfa9 ....$......./c..
0x0030 4ec1 3cc0 N<.
```

```
20:40:08.685428 murphy.debian.org.45772 > test.example.com.smtp: P [tcp sum ok]
1:25(24) ack 51 win 5840 <nop,nop,timestamp 795074478 1321286848> (DF) (ttl 57,
id 65112, len 76)
```

