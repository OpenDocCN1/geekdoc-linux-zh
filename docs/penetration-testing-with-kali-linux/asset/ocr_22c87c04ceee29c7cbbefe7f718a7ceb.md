# OffSec

```
192.168.50.63.4124 > 192.168.118.4080: [Flags P.], cksum 0xc2b (correct), seq
len 225, ack 1, win 502, options [nop,nop,TS 1290578437, len 224]
HTTP, length: 224
```

```
GET /HTTP/1.1
Host: 192.168.118.4080
User-Agent: Go-http-client/1
Connection: Upgrade
Sec-WebSocket-Key: LF8Ct3mW1Hg8/CRnQP==
Sec-WebSocket-Protocol: chisel-v3
Sec-WebSocket-Version: 13
Upgrade:
```

```
0000 0414 02d0 4860 37f6 3f4b 0c33 023f E.....@?.7?..22
0010 c8a8 76d0 a1f6 015d a1b0 f5d3 244e 3412 e.....v.v.......$F1.
0020 881b 01fc 622b 00b0 01d1 08a4 c2ec aeb f0
0030 8e30 08b6 08d2 41f7 3426 3120 3450 2f31 ......//HTTP/1
0040 2e31 0086 47f3 347a 3429 3320 31d9 31f1.Host:192.
0050 381e 3231 3132 3833 34a0 38d3 0850 05f7 811.4.168.0080
0060 6572 24d1 6675 672e 3470 67f6 26d8 7474 chisel-v
0070 702d 63c6 69c5 67f6 2f33 23f1 03d6 4f Upgrade:Go-ht
0080 6e6e 6563 7446 72f6 3570 5278 6164 6574 e.Sec-WebSocket
0090 2d0b 4579 81d7 46c3 4864 53d1 0731 -LF8Ct3mW1
00a0 3867 4864 62f3 6742 65f7 3951 03d0 08d3 //cr/wOP==.Sec-WebSocket-P
00b0 53d6 6325 57d6 67f5 62b6 67f3 74d2 0572 otocol.chisel-3
00c0 67f4 66f6 05c2 6320 63b8 6973 62d6 6368 3.Sec-WebSocket
00d0 33d0 08d3 6561 2567 6562 31d3 0850 -Version.:13..up
00e0 0100 6772 6361 2277 65d6 6537 73f6 6374 grade.websockets
00f0 0110 0d0a 0d0
```

```
18:13:56.687745 (ip 0x4a, ttl 64, id 66084, flags [DF], proto TCP (6),
length 225
192.168.118.4080 > 192.168.50.63.4124: [Flags -], cksum 0x46ca (correct), seq
ack 1, win 505, options [nop,nop,TS
```

519 - Inbound chisel traffic logged by tcpdump

The traffic indicates that the chisel client has created an HTTP WebSocket connection with the

Our chisel server logged an inbound connection.

```
kali@kali: chisel server --port 8080 --reverse
2022/08/21 17:57:52: Server route tunneling enabled
2022/08/21 17:57:52: Fingerprint PrAuAFgGUnExYKI14RMMeItaCcmJ6kj4zsa9S2LXc7=
2022/08/21 17:57:52: Listening on http://0.0.0.0:8080
2022/08/21 18:13:54: session:2; proxy:XR:127.0.0.1:10880=>socks: connecting
519 - Connecting inbound connection logged by the chisel.
```

Next, we check the status of our SOCKS proxy with.

```
kali@kali: ss -ntlpu
Netid State Recv-Q Send-Q Local Address:Port Peer
Address:Port Process
udp UNCONN 0 0.0.0.0:34877
0.0.0.0:*
tcp LISTEN 0 4096 127.0.0.1:1080
```

PWK - Copyright ©2023 OffSec Services. All rights reserved. 619