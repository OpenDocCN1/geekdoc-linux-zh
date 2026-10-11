
# TCP Dump 输出示例

```text
18:18:51.986230 IP (tos 0x0, ttl 64, id 10907, offset 0, flags [DF],
   length: 513) client.braingia.org.4564 > test.example.com.www:
   P [tcp sum ok] 1:462(461) ack 1 win 5840 <nop,nop,timestamp
   250295308 132004005>
   0x0000: 0090 2741 78f0 0060 1833 2e88 0800 4500    ..Ax......
   0x0010: 0201 2a9b 4000 4006 044b c0a8 010a 455d  **..@........
   0x0020: 0302 11da 0050 0c9b 1ea0 9627 33f8 8018     ...P.G.P....
   0x0030: 16ad 4915 0000 0101 080a 0e2b 340c 4eb4      ..I........N.
   0x0040: 50f5 47455 5420 3f20 4854 5472 2f31 2639      GET /HTTP/1...
   0x0050: 0d0a 48ef 7374 3a20 7777 772e e32f 211e  .Host:.text.exam
   0x0060: 6e87 6961 2e6f 726f 0d0a 4163 6358 7074  ple.com.Accpt
   0x0070: 3a20 74e5 7874 7268 746d 726d 726d 4578      .text/html,...
   0x0080: 742f 706c 6f99 6e2c 2061 7070 6c69 71ation/pdf,applica
   0x0090: 7469 6e5a 2f6d 7377 7265 6201 7078 254a  tion/msword,..x
   0x00a0: 6c69 63at4 6341 7641 6c14cat2 64 6472          location/pdf,
   0x00c0: 7374 726d 7462 7420 6170 695a 6174 6454    stream,applicat
   0x00d0: 6f64 7262 746e 747a 6e61 646c 6e64 7266      x-troff-man
   0x00e0: 6061 7070 6c6d 6341 746e 6f74 2474 7266     .application/x-t
   0x00f0: 6172 2e20 6170 616c 6361 6f74 7266 7261     ar,applicatio
   0x0100: 782d 6974 6474 2d20 6170 6341 6f78 647a      x-gtar,.
   0x0110: 6f6f 6e72 7274 642c 2064 7070 6341 6369      ion/rtf,.applic
```

```text
0x0120: 7469 6f6e 2f70 6f73 7473 6372 6974  742c  tion/postscript,
0x0130: 2061 7070 6c69 6361 7469 6f6e 2f67 6f6f  .application/g
0x0140: 7374 7669 6577 2c20 7465 7874 2f73 7479  le: text/.text..,
0x0150: 34163 63655 7074 3a20 6170 706c 6963 6174  application:
0x0160: 6966 6e66 782d 6465 6269 6c6f 6320 6b6f  io/x/.debianpac
0x0170: 6b61 6f76 2c20 6175 6469 6f62 7369 6f6e  ke,.audio/basi
0x0180: 632c 6020 2f2a 3b71 3d30 2e31 316f 3041  c,/*;^=0.01.A
0x0190: 6363 6557 742d 455e 6366 6469 667d 3a2d  ccept-Encoding:
0x01a0: 677a 6970 2c20 6366 6d70 7265 7373 6f6a  gzip,.Compress.
0x01b0: 34163 63655 7074 2d4c 616e 6775 6167 653e  Accept-Language:
0x01c0: 2065 6e75 6c6c 6173 2c20 3467 656e 3431  .en-User-Agent:
0x01d0: 204c 7976 782f 322e 382e 3420 3420 2e33  lynx/2.8.4rel.1
0x01e0: 206c 6966 7777 772d 4644 2f32 2e31 3420  l:HTTPFM/2.14.
0x01f0: 3533 342d 6464 2f31 2e34 2e31 2046 7065  55334.1.4.1Ope
0x0200: 6653 334c 2f30 2e39 2e36 636f 646f 6d6f  SSL/1.0.9.6..
```

```text
18:18:52.039595 IP tos 0x0, ttl 48, id 25347, offset 0, flags [DF],
        length: 52) test.example.com.ww > client.braingia.org.4564:
        [tcp sum ok] 1:1(0) ack 462 win 6432 <nop,nop,timestamp
        1320440059 250295308>

0x0000: 00e0 1833 2ee8 0090 2741 78f0 0800 4500  ....3.ox..Ax..E.
0x0010: 0034 6302 4000 3006 dbb0 4554 03c2 4c08  .c.0...E..c.0...
0x0020: 010a 0050 11d4 9627 33f8 0c9b 206d 8010  ..P..3...N.P..g...
0x0030: 1920 6799 0000 0101 080a 4e4b 50f8 ee4e  ...P......N..
0x0040: 340c 4854 5450 2f31 2e31 0d 3a3f 0d61  ...P......N.P..o:HTTP/1.1..N..0
0x0050: 4b4d 6044 6174 6533 3a30 2c20 3a37 3320  4.K.Date..Tue,27
0x0060: 204a 755c 6332 3032 3033 3a33 3a31 393a  ..Jul..2004..23:19:
0x0070: 3170 6163 645a 6d64 3535 7272 3650 3a20  1...CACT..Server.
0x0080: 4170 6113 6b53 2f31 2e33 3620 2855 6f34  /....3.3(U
0x0090: 6e69 7829 2044 6562 6d66 6472 665f 6d3e  lnx..Debm..GNU/
0x00a0: 4c69 6e75 672f 646f 6f66 6472 6647 5f38  Linx..modono0
0x00b0: 3e31 3120 6d66 645f 7065 7263 2e31 2e32  ..mfl.per1/1.2
0x00c0: 2e3f6f 3443 61e5 6e65 3434 666a 7233 726f  .connection.c
0x00d0: 6c6f 7365 5064 4366 6f74 4f34 5449 2e78  1.5.4..text/ty
0x00e0: 70e5 3a20 7463 7476 756d 6a2d 2069 757c  ..content-html..
0x00f0: 6861 7273 6f74 3d6f 7366 2d3288 3b35 392d  hset=iso-8859-
```

注意，此输出包含一个实际的请求（见第一个数据包，在 GET 和 HTTP/1.0 附近）以及来自 Web 服务器响应的一部分。所有这些流量都是明文，因为 HTTP 没有加密。此输出同时包含十六进制和 ASCII 字符。如果只想获取纯 ASCII 输出，请从命令中移除 `-x` 和 `-X`，并用单个 `-A` 替换它们。我个人有时觉得双列十六进制和 ASCII 输出很有帮助。
