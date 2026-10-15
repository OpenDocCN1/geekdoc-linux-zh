
以下选项将长连接流拆分为 5 分钟的段。你可以选择 1 到 60 分钟之间的任何段长度，但它应该等于或小于`nfdumps`文件轮转周期（默认为 5 分钟）。

```
ios ip flow-export version 5
ios ip flow-cache timeout active 5
```

在 Catalyst 6500/7600 上，除了正常的 NetFlow 导出外，你必须启用 NDE（NetFlow 数据导出）。

## 推荐阅读

方法如下：

```
# ios mls flow ip interface-full
# ios mls flow ipv6 interface-full
# ios mls nde sender version 5
```

在繁忙的路由器上，可以考虑激进地让小流量流超时：

```
# ios mls aging fast time 4 threshold 2
# ios mls aging normal 32
# ios mls aging long 900
```
