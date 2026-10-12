> Exercise: repeat the HTTP/1.1 session, but while the connection is waiting to terminate, issue another request (or repeat the same one again). Don't forget to include the *host* header again, and the blank line terminating the headers.

Below are the tcpdump traces of two HTTP sessions, side by side, lines truncated to save space. The left-hand trace is HTTP/1.0, the right-hand is HTTP/1.1. In both cases the browser has requested the same small Web page that contains several images. You can see HTTP/1.0 establishes and terminates several connections (S and F flags in the trace), whereas HTTP/1.1 uses a single session:

```
dave 1354 > bob.80: P 1615168000:1615168000(0)
bob.80 > dave.1354: S 1016144448:1016144480(0)
dave 1354 > bob.80: P 30:32(2) ack 1 win 4096
bob.80 > dave.1354: ack 30 win 16060 (DF)
dave 1354 > bob.80: P 1:30(29) ack 1 win 4096
bob.80 > dave.1354: P 1:41(41) ack 1 win 4096
bob.80 > dave.1354: P 41:1461(1460) ack 32 win
bob.80 > dave.1354: P 41:1461(1460) ack 32 win
bob.80 > dave.1354: P 1461:2424(963) ack 32 wi
bob.80 > dave.1354: P 1461:2424(963) ack 32 wi
bob.80 > dave.1354: P 2424:2424(0) ack 32 win
bob.80 > dave.1354: P 2424:2424(0) ack 32 win
dave 1354 > bob.80: P 424:2405(1981) ack 2424 w
dave 1354 > bob.80: P 424:2405(1981) ack 2424 w
dave 1354 > bob.80: F 32:32(0) ack 2425 win 40
bob.80 > dave.1354: P 32:36(4) ack 2405 win 4096
dave 1354 > bob.80: F 32:32(0) ack 2425 win 40
dave 1354 > bob.80: P 33:33(0) ack 16060 (DF)
bob.80 > dave.1354: ack 33 win 16060 (DF)
dave 1355 > bob.80: P 16147672000:16147672000(0)
bob.80 > dave.1355: S 10815183424:10815184942(0)
dave 1355 > bob.80: P 3:37(34) ack 1 win 4096
dave 1355 > bob.80: P 3:37(34) ack 1 win 4096
bob.80 > dave.1355: P 44:64(20) ack 1 win 16060 (DF)
bob.80 > dave.1355: P 34:36(2) ack 1 win 4096
dave 1355 > bob.80: P 34:36(2) ack 1 win 4096
dave 1355 > bob.80: P 1:4461(1460) ack 36 win
dave 1355 > bob.80: P 4461:2921(1460) ack 36 w
bob.80 > dave.1355: P 2921:4381(1460) ack 36 w
bob.80 > dave.1355: P 4381:4382(1)(DF) ack 36 win
bob.80 > dave.1355: P 4381:4382(1)(DF) ack 36 win
dave 1355 > bob.80: P 1619264000:1619264000(0)
ack 136 win
dave 1356 > bob.80: S 1102775340:1102775340(0)
dave 1356 > bob.80: S 1102775340:1102775340(0)
dave 1356 > bob.80: P 35:446(109) ack 1102775440
bob.80 > dave.1356: P 1:4461(1460) ack 37 w
dave 1356 > bob.80: P 4461:2921(1460) ack 37 w
bob.80 > dave.1356: P 2921:3829(908) ack 37 v
dave 1356 > bob.80: P 3830:3830(0) win 2316
dave 1356 > bob.80: ack 3830 win 4096
dave 1356 > bob.80: P 37:37(0) ack 3830 win 40
bob.80 > dave.1356: ack 38 win 16060 (DF)
```

In traces like this you may sometimes see HTTP/1.1 using more than one connection. What's happening is not that the client is using a separate connection per request, but that it's using multiple persistent connections simultaneously, e.g. so that it can download images on one connection at the same time as retrieving the main Web page on another connection. You will see that in HTTP/1.1 the connection terminations all happen together, very close to the end of the session, when they are no longer required because everything has been retrieved.

By contrast, in HTTP/1.0 the terminations happen throughout the trace, as each individual retrieval finishes. Different browsers use different numbers of simultaneous connections to a single server; the recommended number is two, in order to avoid congestion in server traffic, but some browsers use four or six.