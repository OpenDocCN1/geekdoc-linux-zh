

至此，你的本地/服务器仓库已创建完成，并且网络中的任何客户端都应能够访问该仓库以进行 yum 安装或更新。
服务器端的设置已经完成。
现在，让我们来看看客户端的设置。

# 第 5 步：YUM 客户端端设置

在客户端机器上，你需要做的唯一更改位于 `/etc/yum.repos.d/` 目录：在此处，你可以拥有一个包含上述参数的 client.repo 文件。

# 示例 client.repo 文件：

在 `/etc/yum.repos.d/` 目录中创建一个仓库文件 [你可以将文件命名为任意名称，但请确保后续添加了 .repo 扩展名]

```text
[root@netmon ]#vi /etc/yum.repos.d/client.repo

[client]
  name=Client
  baseurl=ftp://172.16.100.1/pub/server (Ip address choice is left to you)
  gpgcheck=0
[vt]
  name=vt
  baseurl=ftp://172.16.100.1/pub/vt
  gpgcheck=0
```

第一行是为你指定的仓库设置的别名。这有助于指示/查找软件包来自哪个仓库。第二行是你的仓库名称，你可以填写任何内容。接下来是 baseurl，它支持不同的协议，如 file:// ftp:// httpd:// 等。如果你是从本地系统运行仓库，请在 file:// 后提供绝对路径。

![](img/f3b9cff79e19317416c12eaf5ded7245_281_0.png)

下一行是 enabled，它指定是否应启用该仓库服务器用于安装，1 表示启用，0 表示禁用。gpgcheck 用于检查 gpg 密钥。
之后，保存该仓库文件并运行以下命令

```bash
[root@netmon]#yum clean all [will clean yum database]
[root@netmon]#yum list [will list the files / packages available on that server or local directory]
```

![](img/f3b9cff79e19317416c12eaf5ded7245_281_1.png)

我们使用了 RHEL 服务器 5 版本。该过程对于 RHEL 4、5 或 Fedora 是相同的。

# 附录：TCL 示例脚本

### 停止等待协议 TCL 脚本

“停止等待”（有时被称为“带重传的正向确认”）是在不可靠的数据包传输系统中提供可靠传输的基本技术。在传输一个数据包后，发送方等待接收方的确认（ACK），然后才传输下一个数据包。通过这种方式，发送方可以识别出之前的数据包已成功传输，我们可以说“停止等待”保证了节点之间的可靠传输。

```tcl
# stop and wait protocol in normal situation
# features : labeling, annotation, nam-graph, and window size monitoring
set ns [new Simulator]
set n0 [$ns node]
set n1 [$ns node]
$ns at 0.0 "$n0 label Sender"
$ns at 0.0 "$n1 label Receiver"
set nf [open AI-stop-n-wait.nam w]
$ns namtrace-all $nf
set f [open AI-stop-n-wait.tr w]
$ns trace-all $f
$ns duplex-link $n0 $n1 0.2Mb 200ms DropTail
$ns duplex-link-op $n0 $n1 orient right
$ns queue-limit $n0 $n1 10
Agent/TCP set nam_tracevar_ true
set tcp [new Agent/TCP]
$tcp set window_ 1
$tcp set maxcwnd_ 1
$ns attach-agent $n0 $tcp
set sink [new Agent/TCPSink]
$ns attach-agent $n1 $sink
$ns connect $tcp $sink
set ftp [new Application/FTP]
$ftp attach-agent $tcp
$ns add-agent-trace $tcp tcp
$ns monitor-agent-trace $tcp
$tcp tracevar cwnd_
$ns at 0.1 "$ftp start"
$ns at 3.0 "$ns detach-agent $n0 $tcp ; $ns detach-agent $n1 $sink"
$ns at 3.5 "finish"

$ns at 0.0 "$ns trace-annotate ""Stop and wait with normal operation"""

$ns at 0.05 "$ns trace-annotate ""FTP starts at 0.1""
$ns at 0.11 "$ns trace-annotate ""Send_Packet_0""
$ns at 0.35 "$ns trace-annotate ""Receive_Ack_0""
$ns at 0.56 "$ns trace-annotate ""Send_Packet_1""
$ns at 0.79 "$ns trace-annotate ""Receive_Ack_1""
$ns at 0.99 "$ns trace-annotate ""Send_Packet_2""
$ns at 1.23 "$ns trace-annotate ""Receive_Ack_2""
$ns at 1.43 "$ns trace-annotate ""Send_Packet_3""
$ns at 1.67 "$ns trace-annotate ""Receive_Ack_3""
$ns at 1.88 "$ns trace-annotate ""Send_Packet_4""
$ns at 2.11 "$ns trace-annotate ""Receive_Ack_4""
$ns at 2.32 "$ns trace-annotate ""Send_Packet_5""
$ns at 2.55 "$ns trace-annotate ""Receive_Ack_5""
$ns at 2.75 "$ns trace-annotate ""Send_Packet_6""
$ns at 2.99 "$ns trace-annotate ""Receive_Ack_6""
$ns at 3.1 "$ns trace-annotate ""FTP stops""
proc finish {} {
    global ns nf
    $ns flush-trace
    close $nf
    
    puts "filtering..."
    exec tclsh /ns-allinone-2.31/nam-1.13/bin/namfilter.tcl A1-stop-n-wait.nam 
        puts "running nam..."
        exec nam A1-stop-n-wait.nam &
        exit 0
}
$ns run
```

### 移动和无线环境 TCL 脚本

在无线网络拓扑中，当并非所有节点都在彼此的范围内时，载波侦听仅提供关于发送方冲突的信息，而不包括接收方。这会导致诸如“隐藏终端”的问题（即两个超出彼此范围的发送节点同时向同一个接收方传输数据包，导致接收方发生冲突）。为了解决这类问题，使用控制数据包（RTS & CTS）作为载波侦听协议的替代方案。当节点希望传输数据包时，它首先向接收方发送 RTS（Request To Send，请求发送）数据包。发送方范围内的所有节点都会收到此 RTS 数据包。听到 RTS 数据包的每个节点都会推迟传输。如果接收方没有从其他任何节点接收数据，它会响应一个 CTS（Clear To Send，清除发送）数据包。该数据包再次被接收方范围内的每个节点收到。因此，范围内的所有节点都会推迟传输。发送节点在收到 CTS 后发送数据包。如果发送节点没有听到 CTS，它将超时并安排 RTS 的重传。收到数据包后，接收方向发送方发送 ACK。链路层 ACK 用于促进更快地从冲突中恢复。RTS 和 CTS 数据包非常短，因此发生冲突的可能性非常小。如果来自 2 个发送节点的 RTS 数据包在接收方发生冲突，发送节点将不会收到 CTS 数据包，节点因此会在一定时间内退避，从而检测到冲突。该协议解决了隐藏终端问题，尽管两个发送节点可能超出彼此的通信范围，但它们都在它们想要发送数据包的接收方的范围内。因此，当接收方向一个节点响应 CTS 数据包时，另一个发送节点也会听到该数据包，并将推迟传输。在我们的动画中，我们有 3 个节点 0、1、2。

我们在以下 3 种情况下观察节点的行为：

- 案例 1：（无竞争）------- 只有一个节点（节点 2）发送数据，因此没有竞争
- 案例 2：（因 RTS 而退避）

两个发送节点，节点 0 和 2 在彼此的范围内，但节点 1 在节点 2 的范围之外。当节点 2 想要向节点 0 发送数据，而节点 0 想要向节点 1 发送数据时。在这种情况下，节点 0 和 2 都执行载波侦听。然后节点 0 向节点 1 和 2 发送 RTS 数据包。节点 2 在听到该 RTS 数据包后退避。节点 1 向节点 0 发送 CTS，节点 0 执行其数据传输，在传输结束时，节点 2 再次执行载波侦听并执行其数据传输，发现介质空闲。

- 案例 3：（再次因 RTS 而退避）

两个发送节点 0 和 2 在彼此的范围内，也在节点 1 的范围内。因此，它们都可以听到彼此的 RTS 和 CTS 数据包。在这种情况下，当节点 2 想要向节点 1 发送数据，同时节点 0 也想向节点 1 发送数据时，节点 2 听到节点 0 的 RTS 并退避，从而推迟其传输直到节点 0 完成传输，因此避免了接收端的冲突。

- 案例 4：因 CTS 而退避

两个发送节点 0 和 2 在彼此的通信范围之外，但在接收方节点 1 的范围内。在这种情况下，节点无法听到彼此的 RTS 数据包，但能够听到接收方的 CTS 数据包，因此退避，推迟传输直到另一个节点完成传输。

```tcl
#Copyright (c) 1997 Regents of the University of California.
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
# 1. Redistributions of source code must retain the above copyright
# notice, this list of conditions and the following disclaimer.
# 2. Redistributions in binary form must reproduce the above copyright
# notice, this list of conditions and the following disclaimer in the
# documentation and/or other materials provided with the distribution.
# 3. All advertising materials mentioning features or use of this software
# must display the following acknowledgement:
# This product includes software developed by the Computer Systems
# Engineering Group at Lawrence Berkeley Laboratory.
# 4. Neither the name of the University nor of the Laboratory may be used
# to endorse or promote products derived from this software without
# specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE REGENTS AND CONTRIBUTORS ``AS IS'' AND
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED. IN NO EVENT SHALL THE REGENTS OR CONTRIBUTORS BE LIABLE
```

