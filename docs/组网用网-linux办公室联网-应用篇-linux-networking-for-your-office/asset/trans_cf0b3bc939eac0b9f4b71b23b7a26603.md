

一般来说，我建议使用 hosts allow 来通过 IP 地址明确列出授权的主机，至少对于连接到互联网的计算机而言。这种做法使得未经授权的人员入侵你的系统变得更加困难。

为了提高安全性，Samba 通常将自身绑定到单个接口上。然而，如果你的计算机用作网关、防火墙或 IP 伪装计算机，则可能需要指定其要使用的 NIC。你可以通过 interfaces 选项来实现：

```
interfaces = 192.168.1.1/255.255.255.0
```

你在 interfaces 行上指定要绑定到的接口上的主机计算机的 IP 地址和网络掩码。上面的示例将 Samba 设置为在绑定到 192.168.1.1 的 NIC 上为 192.168.1.0 网络提供服务。如果你希望 Samba 为两个或更多 NIC 的网络提供服务，则需要全部列出，以空格分隔。

## Speed Enhancement Options

Samba 通常具有良好的速度，但在某些情况下你可能需要调整其设置，或“取消调整”某些被错误配置的设置。不幸的是，什么效果好因网络而异，因为性能调优因素会与网络硬件类型等问题相互作用。以下是一些具体建议：

- General network performance—如果你的网络负载过重，Samba 的性能就不佳。你可能想通过输入 /sbin/ifconfig 来检查冲突。如果冲突数量与传输的包数（TX）和接收的包数（RX）相比很高，那么你可能需要考虑安装桥接设备或用交换机替换集线器（参见第 4 章“内部网和互联网”，以及第 1 章“网络硬件”）。
- Oplocks—机会锁，或 oplocks，是控制多用户访问文件的一种方式。fake oplocks 选项可以加快对只读介质（如 CD-ROM）的访问，但除此之外是有风险的。oplocks 选项（与 fake oplocks 选项不同）如果设置为 yes，可以大幅加快对所有文件的访问，因此你应确保它未被设置为 no。
- Strict sync—strict sync 参数默认为 no，通常应保持此设置，因为它通过不执行 Linux sync() 操作来提高性能，而许多 Windows 程序在客户端请求时比应有的更频繁地执行此操作。默认的 no 设置会增加在 Linux 本身崩溃时丢失数据的风险。

除这些项目外，你还可以使用 socket options 来影响 Samba 与 TCP/IP 栈的接口，从而影响系统性能。不过，这些选项的确切效果因网络而异，因此我无法提供任何具体建议。如果你想进行实验，可以在 /etc/smb.conf 文件中创建一个 socket options 行并添加或删除以下选项：

- SO_KEEPALIVE
- SO_REUSEADDR
- SO_BROADCAST
- TCP_NODELAY
- IPTOS_LOWDELAY
- IPTOS_THROUGHPUT
- SO_SNDBUF=integer
- SO_RCVBUF=integer
- SO_SNDLOWAT=integer
- SO_RCVLOWAT=integer

## Configuring a Share

在为整个 Samba 服务器设置配置选项后，是时候处理你想要配置的共享了。你可以在要修改的共享名称的节中执行此操作，或在 [homes] 节中为所有用户的主目录创建共享。如果存在 [homes] 节，它会创建一个可以通过名称 homes 或用户名访问的共享。默认情况下，该共享打开到用户的主目录，你不应为此共享指定其他目录。

## Share Availability Options

有几个选项会影响共享的可用性——即其在客户端浏览器中的可见性或用户访问共享的能力：

- comment — 你在共享上输入的注释在从 Windows 以详细信息模式浏览共享时会出现，如图 11.4 所示。
- available — 此选项默认为 yes。如果设置为 no，Samba 不允许任何人连接到共享。你可能会使用此选项在对目录进行维护时使共享暂时不可用。
- guest ok or public — 这些选项是同义词，默认为 no。如果设置为 yes，它们允许任何人即使没有密码也能连接到相关共享。使用这些选项时务必格外谨慎！

