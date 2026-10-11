
#### 示例 11-1 QMGR1.DEF

此脚本在源端的队列管理器 `QMGR1` 中创建以下对象：

**一个本地管理队列**
`DEF QLOCAL('SAMPLE_ADMINQ') DESCR('Capture Admin Queue') REPLACE`

**一个本地重启队列**
`DEF QLOCAL('SAMPLE_RESTARTQ') DESCR('Capture Restart Queue') REPLACE`

**用于放置 Q 队列数据消息的远程队列定义**
`DEF REMOTE('SAMPLE2TGTDBQ') XMITQ('QMGR2') RNAME('SAMPLE2TGTDBQ') RQNAME('QMGR2') REPLACE`

**一个本地传输队列**
`DEF QLOCAL('QMGR2') USAGE(XMITQ) REPLACE`

**通过传输队列从 QMGR1 到队列管理器 QMGR2 的发送通道**
将 ip 替换为你的 ip，并将端口号替换为你的端口号
`DEF CHANNEL('QMGR1.TO.QMGR2') CHLYPE(SDR) TRPTYPE(TCP) CONNAME('9.43.86.78 (14116)') XMITQ('QMGR2') REPLACE`

**来自 QMGR2 的接收通道**
`DEF CHANNEL('QMGR2.TO.QMGR1') CHLYPE(RCVR) TRPTYPE(TCP) REPLACE`

- 3. 在目标服务器上设置 WebSphere MQ 对象：

a. 从命令行窗口创建一个与源端名称不同的队列管理器：
`strmqm QMGR2`

b. 启动你刚刚创建的队列管理器：
`strmqm QMGR2`

c. 要创建所需的 MQ 对象，请使用示例 11-2 所示的脚本运行以下命令。记得将 IP 和端口号替换为所需的 IP 和端口号：
`runmqsc QMGR2 < QMGR2.DEF`

#### 示例 11-2 QMGR2.DEF

此脚本在目标端的队列管理器 `QMGR2` 中创建以下对象：

**一个指向源端管理队列的远程队列定义**
```
DEF REMOTE('SAMPLE_ADMINQ') XMITQ('QMGR1') RNAME('SAMPLE_ADMINQ') QNAME('QMGR1') REPLACE
```

**一个用于在加载期间存放 Q Capture 数据消息的溢出队列模型队列定义**
```
DEF MODEL('IBMQ.SPILL.MODELQ') DEFSOPT(SHARED) + MAXDEPTH(500000) MGLDVSQ(FIFO) DETYPE(PERMDYN) REPLACE
```

**一个用于 Q Apply 从源端的 Q Capture 程序中获取数据消息的本地队列**
```
DEF QLOCAL('SAMPLEGTDBQ') REPLACE
```

**一个本地传输队列**
```
DEF QLOCAL('QMGR1') USAGE(XMITQ) REPLACE
```

**通过传输队列 QMGR1 从 QM2 到队列管理器 QMGR1 的发送通道**
将 ip 替换为你的 ip，并将端口号替换为你的端口号
```
DEF CHANNEL('QMGR2.TO.QMGR1') CHLYPE(SDR) TRPTYPE(TCP) + CONNAME('9.43.86.75(1415)') XMITQ('QMGR1') REPLACE
```

**来自 QMGR1 的接收通道**
```
DEF CHANNEL('QMGR1.TO.QMGR2') CHLYPE(RCVR) TRPTYPE(TCP) REPLACE
```

- 4. 在源端和目标端启动监听器和通道：
a. 在源端，从命令行窗口启动监听器：
`RUNMQSR -T TCP - QMGR1 -P 1415`
b. 在目标端，从命令行窗口启动监听器：
`RUNMQSR -T TCP - QMGR2`
c. 在源端，从命令行窗口启动通道：
要启动通道，首先使用 `RUNMQSC` 命令进入交互式界面：
`RUNMQSC QMGR1`
此命令启动通道：
`START CHANNEL(QMGR1.TO.QMGR2)`
d. 在目标端，从命令行窗口启动通道：
```
RUNMQSC QMGR2
START CHANNEL(QMGR2.TO.QMGR1)
```

- 5. 可选：测试队列：

我们通过在源端发送消息并在目标端获取消息来测试队列设置。

a. 在源端，按照示例 11-3 所示将“Test message to send”放入队列。

i. 回车发送消息。

ii. 回车发送消息。

# 示例 11-3
```
amput SAMPLE2DBQ QMGR1
target is SAMPLE2DBQ
Test message to send
```

b. 示例 11-4 显示如何从目标端接收消息。
回车结束提示。

# 示例 11-4
```
amqsget SAMPLE2DBQ QMGR2
no more messages
```
