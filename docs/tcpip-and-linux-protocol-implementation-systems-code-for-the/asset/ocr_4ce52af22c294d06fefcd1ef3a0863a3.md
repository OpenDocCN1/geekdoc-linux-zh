# Transport 489

```
1 browser.4298 > server.http S 799139388:799139388(0) in 5840 <<ms 1460,sackOK,timestamp
69053329,nop,wcale O (DF)
```

```
2 server.http > browser.4297: S 864694739:864694739(0) ack 1460,sackOK,
timestamp 187462286 69053329,nop,wcale O (DF) 31220
```

```
3 browser.4297 > server.http: 1:111(0) ack 1 in 5840 <<nop,timestamp 69053329 187462286) (DF)
```

```
4 browser.4297 > server.http: P 1:111(140) ack 1 in 5840 <<nop,timestamp
69053329 187462286) (DF)
```

```
5 server.http > browser.4278: 1:111(0) ack 111 in 31220,nop,timestamp
187462286 69053329)
```

```
6 server.http > browser.4297: P 1:461(450) ack 111 in 31220 <<nop,timestamp
69053329 187462286)
```

```
7 browser.4298 > server.http: 1141:111(0) ack 45 in 642 <<nop,timestamp
69053330 187462287) (DF)
```

```
8 server.http > browser.4278: F 1:451(450) ack 111 in 31220 <<nop,timestamp
187462287 69053329) (DF)
```

```
9 browser.4297 > server.http: F 1141:111(0) ack 45 in 642 <<nop,timestamp
69053330 187462287) (DF)
```

```
10 server.http > browser.4297: 452:452(0) ack 112 in 31220 <<nop,timestamp
187462287 69053330) (DF)
```

# Congestion Control

In the preceding discussion of flow control, we recall that there can be network-related problems to systems sending too fast. If a sender with a high bandwidth connection to its network is sending to a receiver, and at some point in the path there is a lower bandwidth link, then as soon as the sender starts too fast for the lower bandwidth link there will be loss. This is called congestion. Congestion can also occur when a number of connections are sharing a link and is trying to make as much as possible of the available bandwidth. TCP congestion control makes that a TCP connection in either of the two preceding cases receives a fair share of the available bandwidth. Definition of fair in these cases is generally a contentious issue.

Congestion control employs another window in the data to be transmitted. This window is called congestion window and controls the amount of data that can be sent into the network unacknowledged. The congestion window increases in size while the network is uncongested and decreases when congestion is detected. Currently congestion is detected by detection of a lost packet. Explicit Congestion Notification (ECN) is a technique where congestion in the network is detected and the sending sites identified by the setting of a TCP header in the returning data stream.

The increases and the decreases in the congestion window size are specified in RFC 2581. A TCP connection can be in one of two states: slow start or congestion