
```
// 554 / TCP
RTSP/1.0 200 OK
Cseq: 1
Server: Ripcam RealServer/V1.0
Public: OPTIONS, DESCRIBE, SETUP, FLAT, TEARDOWN, SET_PARAMETER, GET_PARAMETER
```

说严肃一点，通过稍作搜索，使用搜索字符串“`authentication disabled`”（禁用身份验证）并过滤 `screenshot.label:ics`，你将获得更有趣的结果（注意那些“停止”按钮）。

```
// 5900 / TCP
-715840854 | 2024-04-11T23:50:33.484987

RFB 003.008
Authentication Disabled

85.57 Y
System 4
Reset Fan
Fan Hours
161 Hours
3118300 L
00:00:15.000 co)
Manual Enabled Stop Pump Reset
Le -
pump Hi Hours
162 Hours
```

![](img/0add480ffb73b6bc89b65d99f7d6b37a_673_0.png)

如果你对工业控制系统（ICS）感兴趣，并寻找运行某些常用 ICS 服务但不运行其他类型常用服务的设备，你可以使用搜索字符串“`port:502,102,20000,1911,4911,47808,448,18,18245,1825094,1962,5006,5007,9600,789,2455,2404,20547 country:US -ssh -htp -html -ident`”，这将产生图 19-1 所示的视图。

从该视图可以看出，有 672,501 个潜在的 ICS 主机运行 ICS 服务，但不运行 HTTP、HTML、SSH 和 IDENT（这些都是常用服务）。此外，我们可以知道托管这些 ICS 服务的最常见城市、顶级和服务顶级组织。当然，我们需要进行进一步的过滤并排除蜜罐（honeypots）——这一点稍后会详细介绍。

可以使用 Facets（分面）来细化搜索结果并获取统计数据，它允许用户深入查看与搜索相关的更多统计数据。例如，通过点击图 19-1 所示左侧面板“Top Ports”（顶级端口）下的“More...”，你将看到以下产品列表及其数量。可以通过下拉菜单进行进一步的细分。

| RESULTS | 672,501 |

| TOPICS | |

| Kansas City | 317,822 |

| Redwood | 112,717 |

| Mountain View | 50,706 |

| Seattle | 50,706 |

| Los Angeles | 21,838 |

| PORTS | |

| 20000 | 399,953 |

| 9600 | 133,008 |

| 1911 | 30,335 |

| 47808 | 13,967 |

| 20547 | 13,014 |

| View Report | Download Results | View on Map |

| New Service: Keep track of what you have connected to the Internet. Shodan Monitor | | |

| 107.154.150,160 | 2024-01-14T04:26:329605 | |

| 107.154.150.1 | No data returned | |

| ip.incdn | | |

| c.googleusercontent.com | | |

| Incula Inc | | |

| United States, Redwood City | | |

| 35.190.70.24 | 2024-01-14T04:47:551277 | |

| 24.70.190.35.b | No data returned | |

| c.googleusercontent.com | | |

| Google LLC | | |

| United States, Kansas City | | |

| 34.117.87.40 | 2024-01-14T04:28:642895 | |

| 40.87.117.34.b | No data returned | |

| c.googleusercontent.com | | |

| Google LLC | | |

| United States | | |

## 图 19-1 常用服务

### Facet 分析

`port:502,102,20000,1911,4911,47808,448,18,18245,182` TOTAL: 676,284

| | |

| :--- | :--- |

| Niagara Fox | 111 |

| Niagara4 Station | 399 |

| Red Lion Controls | 1,348 |

| NiagaraAX Station | 748 |

| MACH-ProWebCom | 416 |

| Tracer SC | 320 |

| eBMGR | 290 |

| LGR25 | 275 |

| AAM-Router | 273 |

## Shodan 命令行界面

对于喜欢命令行的人来说，Shodan 不会失望。它提供了一个功能完备的强大命令行工具，正如你将在下一个实验中看到的。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_676_0.png) 本的实验是在 Kali Linux 2021.1 (64位) 上进行的，但也适用于其他版本的 Linux。此外，还需要 Shodan 的 API key，你可以在那里注册并免费获取。

### 实验 19-1: 使用 Shodan 命令行

在本实验中，我们将探索 Shodan 命令行。当前版本的 Kali 安装了 Shodan CLI，按照如下方式使用你的 API key 初始化：

```
% shodan init <YOUR API KEY>
Successfully initialized
```

接下来，测试账户中的余额：

```
% shodan info
Query credits available: 100
Scan credits available: 100
```

最后，对 VNC 服务 (`RFB`) 进行扫描，显示 IP、端口、组织和主机名：

```
% shodan search --fields ip_str,port,org,hostnames RFB > results.txt
wc -l results.txt
101 results.txt
# head -3 results.txt
186.10.40.11 8334 ENTEL CHILE S.A. z210.entel chile.net
68.51.127.103 5901 Comcast Cable Communications, Inc. c-68-51-127-103.hsdn.in.comcast.net
169.229.136.161 5900 University of California at Berkeley tol2mac5.soe.berkelely.edu
```

命令行工具的一个功能是能够检查 honeyscore（蜜罐分）——使用 Shodan 开发的启发式算法测试站点是否为蜜罐的分数：

```
% shodan honeyscore 54.187.148.155
Not a honeypot
Score: 0.5
% shodan honeyscore 52.24.188.77
Honeypot
Score: 1.0
```

这是一个使用类似图 19-1 中所示 Facet 的示例：

```
% shodan states --facet city:3,product:3 "port:502,102,20000,1911,4911,47808,448,18,18245,18246,5094,1962,5006,5007,9600,789,2455,2404,20547 country:US -ssh -http -html -ident"
```

| Top 3 Results for Facet: city |

| :--- | :--- |

| Kansas City | 317,769 |

| Redwood City | 112,706 |

| Mountain View | 63,421 |

| Top 3 Results for Facet: product |

| :--- | :--- |

| Niagara Fox | 10,047 |

| Niagara4 Station | 1,391 |

| Red Lion Controls | 1,337 |

### 实验 19-2: 测试 Shodan API
