
```
# zero /etc/defaultrouter
# zero /etc/default/dhcp
# zero /etc/resolv.conf
```

就是这样了。已存在并被清零的文件，其内容已被擦除；原本不存在的文件现在也存在了（特别是 /etc/dhcp.pc0）。

唯一剩下的步骤是把 /etc/inet/hosts 文件中的几乎全部内容删除，只保留一行 localhost，别无其他。它应该像这样：

```
# cat /etc/inet/hosts
127.0.0.1 localhost
```

与该主机相关的其他行会在启动时由 DHCP 客户端分配 IP 时自动填入。

> 如果你想了解如何将 Solaris 系统设置为 DHCP 服务器，最好的做法是从 Internet Software Consortium 网站（www.isc.org）下载与 Solaris 兼容的 dhcpd，并按照他们清晰、连贯的说明进行操作。

- **5.** 在结束 Unix 系统网络连接配置这个话题之前，让我们把注意力转向 Mac OS X。在基于命令行的网络配置方面，Mac 算是相当另类的一种生物。

  坦白说，如果你够理性，最好的方式就是直接使用 Mac OS X 的“系统偏好设置”网络面板，如图 17.1 所示。

  **图 17.1** “系统偏好设置”中的网络面板。

  ![](img/5ced0c78d748bd190e9027e5549a3622_356_0.png)

  但如果我们总是循规蹈矩，用这种简单又聪明的办法解决问题，生活该多无趣啊。

  相反，让我们深入探索一下 Mac OS X，看看这个控制面板中的信息到底保存在哪里：如果能够找到那个具体的存档文件，我们就可以手工修改它，对吧？可以说是，也可以说不是。

- **6.** 存储这些配置值的文件属于 Mac OS X 的系统配置区域，位于 /var/db 下：

```
# head -20 /var/db/SystemConfiguration/preferences.xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist SYSTEM
"file://localhost/System/Library/DTDs/PropertyList.dtd">
<plist version="1.0">
<dict>
<key>CurrentSet</key>
<string>Sets/0</string>
<key>NetworkServices</key>
<dict>
<dict>
<key>0</key>
<dict>
<key>AppleTalk</key>
<dict>
<key>ConfigMethod</key>
<string>Node</string>
</dict>
<key>DNS</key>
<dict>
<key>ServerAddresses</key>
<array>
<string>192.216.138.10</string>
<string>192.216.138.11</string>
</array>
</dict>
```

  这只是一个最终长达 461 行的 XML¹ 文件的开头部分。里面并不是简洁明了的“变量：值”序列，而是一个复杂且令人困惑的 XML 格式文件。不过，一旦你意识到“变量：值”序列更可能看起来像这样：

```
<key>variable</key>
<string>value</string>
```

  然后你就能开始看出前面代码中 preferences.xml 文件里的一点门道。例如，AppleTalk 的 ConfigMethod 是 Node，DNS 服务使用的 ServerAddresses 是 192.216.138.10 和 192.216.138.11。

  ¹XML 是可扩展标记语言（eXtensible Markup Language），是 HTML 的一种变体，专门设计用于以通用格式轻松解析数据。苹果将其用于偏好设置文件，这既堪称高明，同时又令人相当沮丧，因为在命令行中很难处理它。

  有了这些认识，让我们反过来看看能否在这个文件中找出网络配置值，先从 IP 地址开始：

```
# grep -5 198.76.82 preferences.xml
<dict>
<key>IPv4</key>
<dict>
<key>Addresses</key>
<array>
<string>198.76.82.132</string>
</array>
<key>ConfigMethod</key>
<string>Manual</string>
<key>Router</key>
<string>198.76.82.129</string>
<key>SubnetMasks</key>
<array>
<string>255.255.255.128</string>
</array>
</dict>
```

  在这里查找匹配项时，使用 -5 标志来查看 C 类地址（IP 地址中的前三组数字）附近五行的上下文，是个不错的做法。你可以看到网络面板中的所有相关变量：Addresses、Router、SubnetMasks，以及本节前面提到的 DNS ServerAddresses。

  因此，如果你确实愿意、并且不排斥编辑 XML 文件，同时准备好生活在危险的边缘，那么你可以直接编辑这个文件。不过，还是先做个备份，以防万一。

- **7.** 此时正适合尝试使用 sed（流编辑器），它非常适合这类就地编辑任务。

  若要将此配置复制到另一台计算机，你可以通过 scp（安全 cp，能以安全、加密的方式在网络间轻松复制文件）将 preferences.xml 文件传输过去，然后只需改动 IP 地址：

```
scp referencehost:/var/db/SystemConfiguration/preferences.xml . | \
sed 's/198.76.82.132/198.76.82.133/' > \
/var/db/SystemConfiguration/preferences.xml
```

  这样会从主 referencehost 复制文件，将旧的 .132 IP 地址改为新的 .133 IP 地址，然后把修改后的文件保存到正确的位置。我们仍然需要确保文件的所有权和权限正确：

```
# cd /var/db/SystemConfiguration
# ls -l preferences.xml
-rw-r--r-- 1 root wheel 11151 Apr 6 22:46 preferences.xml
```

  但除此之外，这个方法是可行的，而且还能让我们从单个 DHCP 客户端参考系统快速复制 DHCP 配置。

还有其他一些关于 Mac OS X 网络配置的问题，我们在这里就不赘述了，因为正如你所见，在 Mac OS X 中基于命令行的网络配置并非易事。事实上，这确实是第一个能让你看出 Mac OS X 中 Mac 部分已经比其底层的 Unix（Darwin）更重要的领域。

![](img/5ced0c78d748bd190e9027e5549a3622_359_0.png)

> 不要误以为 Mac OS X 底层有 Darwin，就认为它与 Darwin 或其前身 FreeBSD 完全兼容。并非如此。后者使用 /etc/iftab 和 /etc/hostconfig 来指定网络参数，但如果存在 SystemConfiguration/preferences.xml 文件，Mac OS X 在网络配置问题上会忽略这些文件。如果你想真正地“折腾”一番，可以删除该文件看看会发生什么，但那时你就完全没有保修了，而且几乎没有人能帮你把客户端救回来。哦，用户可能也不会感激你！

不同 Unix 变体在网络代码方面的差异令人惊叹。这有点奇怪，因为网络连接是 Unix 的“杀手级能力”，也是它在首次交付给客户 25 多年后仍被广泛使用的原因。你能想象在 2020 年还运行 Windows 95 吗？或者 2024 年还在用 Mac OS 9？

然而，无论关键与否，这都是你需要研究特定 Unix 变体所附带的手册和文档的领域，以确保你对启动过程和网络配置顺序的理解与你所管理的操作系统保持一致。

## 测试与评估连通性

在本小时结束之前，值得讨论的最后一个主题是 Unix 自带的一组网络诊断工具。不同的 Unix 变体大多有不同的程序，但有一些核心应用程序和系统实用程序信息量很大，尤其是 ifconfig、netstat 和 ping。

这些命令每一个都值得比本书所能提供的更多篇幅来介绍，因此我们鼓励你阅读每个命令的手册页，并通过实验来更深入地了解其功能。

### 任务 17.3：评估连通性

评估连通性的第一步是查看当前系统的配置，然后连上互联网，使用 ping 和 traceroute 来查看网络传输状况……

- **1.** 要评估你的网络配置，第一个也是唯一重要的落脚点就是 ifconfig。使用 -a 标志查询本机的所有接口，或者直接指定以太网接口的名称：

```
# /sbin/ifconfig -a
eth0      Link encap:Ethernet  HWaddr 00:A0:C9:AD:20:E2
          inet addr:10.10.2.200  Bcast:10.10.2.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:37310  errors:0 dropped:0 overruns:0 frame:0
          TX packets:36045  errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:100
          RX bytes:4134689 (3.9 Mb)  TX bytes:15175268 (14.4 Mb)
          Interrupt:5 Base address:0xa000

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:98 errors:0 dropped:0 overruns:0 frame:0
          TX packets:98 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:7176 (7.0 Kb)  TX bytes:7176 (7.0 Kb)
```

Red Hat 很值得一提，因为它的 ifconfig 提供的信息相当多（大多数发行版都比这简洁）。eth0 就是以太网接口，你可以看到这台特定服务器的互联网地址是 10.10.2.200，广播地址是 10.10.2.255，网络掩码是 255.255.255.0。

一个重要的调优值是最大传输单元（MTU），这里为 1500。对于以太网来说，根据协议，最大 MTU 是 1500 字节；但如果你使用 FDDI 令牌环，可以将其提高到 4500 以获得更好的网络吞吐量。如果你使用的是以太网，而 MTU 小于 1500，请使用 ifconfig 将其恢复为正确的值（例如，ifconfig eth0 mtu 1500）。

输出第三行开头的 UP 也很重要——它表明系统认为以太网连接已启动并且活跃。这总是好事。还要注意，eth0 接口已接收（RX）37,310 个信息包，没有错误、没有丢包、也没有溢出。这同样令人欣慰，并且它还发送（TX）了 36,045 个包，毫无差错。

