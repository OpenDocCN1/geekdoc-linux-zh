
| 18 | Chart | Sequence | TCP | Connection establish request (SYN+ACK): server port host |
| 27 | Chart | Sequence | TCP | Connection update |
| 32 | Chart | Sequence | TCP | Connection acknowledge (SYN+ACK): server port host |
| 52 | Chart | Sequence | HTTP | GET `/main.html/1.in` |
| 53 | Chart | Sequence | TCP | Window update |
| 61 | Chart | Sequence | HTTP | HTTP/1.1 304 Not Modified |
| 63 | Chart | Sequence | TCP | Window update |
| 65 | Chart | Sequence | HTTP | GET `/styles.css/1.in` |
| 67 | Chart | Sequence | HTTP | HTTP/1.1 304 Not Modified |
| 68 | Chart | Sequence | HTTP | HTTP/1.1 304 Not Modified |
| 69 | Chart | Sequence | HTTP | HTTP/1.1 304 Not Modified |
| 70 | Chart | Sequence | HTTP | GET `/images/gif/1.in` |
| 71 | Chart | Sequence | HTTP | HTTP/1.1 304 Not Modified |

图 8-2: Expert Info 窗口显示警告和备注。

默认情况下，Expert Info 显示警告和注释。通过 Expert Info 窗口，我们可以看到类似图 8-3 所示的内容。

`img/ae85f2fa699ec68c8cd6b402e11c40d7_121_0.png`

图 8-3: Expert Info 窗口显示异常流量。

### 慢速下载的解剖分析

| No. | Severity | Group | Protocol | Summary |
|---|---|---|---|---|
| 4 | Chart | Sequence | TCP | Connection establish request (SYN): server port host |
| 6 | Chart | Sequence | TCP | GET `/HTTP/1.1` |
| 8 | Chart | Sequence | HTTP | GET `/HTTP/1.1` |
| 9 | Chart | Sequence | HTTP | HTTP/1.1 304 Object Not Modified |
| 11 | Chart | Sequence | HTTP | GET `Default.aspx?check=1&/HTTP/1.in` |
| 18 | Chart | Sequence | TCP | Connection establish request (SYN+ACK): server port host |
| 27 | Chart | Sequence | TCP | Connection update |
| 32 | Chart | Sequence | TCP | Connection acknowledge (SYN+ACK): server port host |
| 52 | Chart | Sequence | HTTP | GET `/main.html/1.in` |
| 53 | Chart | Sequence | TCP | Window update |
| 61 | Chart | Sequence | HTTP | HTTP/1.1 304 Not Modified |
| 63 | Chart | Sequence | TCP | Window update |
| 65 | Chart | Sequence | HTTP | GET `/styles.css/1.in` |
| 67 | Chart | Sequence | HTTP | HTTP/1.1 304 Not Modified |
| 68 | Chart | Sequence | HTTP | HTTP/1.1 304 Not Modified |
| 69 | Chart | Sequence | HTTP | HTTP/1.1 304 Not Modified |
| 70 | Chart | Sequence | HTTP | GET `/images/gif/1.in` |
| 71 | Chart | Sequence | HTTP | HTTP/1.1 304 Not Modified |

# 8

## 对抗慢网络

![](img/ae85f2fa699ec68c8cd6b402e11c40d7_120_0.png)

作为一名网络管理员，你的大部分时间将花在修复那些运行速度比预期要慢的计算机和服务上。IT 人员听到的最常见的抱怨是网络很慢。然而，仅仅有人说网络运行缓慢，并不意味着问题就出在网络上。
