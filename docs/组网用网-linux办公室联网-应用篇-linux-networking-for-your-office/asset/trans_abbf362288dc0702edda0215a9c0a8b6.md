
1. 切换到适合构建软件的目录，例如 /usr/src。
2. 使用类似 tar xvfz ~/socks5-v1.0r10.tar.gz 的命令解压原始源代码压缩包。
3. 进入新创建的 SOCKS 源代码目录：cd socks5-v1.0r10/
4. 输入 ./configure
这将运行一个自动配置脚本，为你的系统设置合适的编译变量。
5. 输入 make，为你的系统编译 SOCKS5 软件包。如果编译器报告任何错误，你需要在继续之前修正这些错误。

## 注意

> 编译器错误和警告是两回事。如果看到编译器警告，不必担心，因为警告是次要的。不过，错误会阻止程序正常编译。

6. 输入 make install，将 SOCKS5 客户端和服务器程序安装到你的系统上。
如果你愿意，可以通过输入 make clean 或删除源代码目录来进行清理。

## 配置 SOCKS 服务器

你可以通过创建一个名为 /etc/socks5.conf 的文件来配置 SOCKS 服务器。这个文件包含告诉服务器如何处理访问请求的规则。该文件包含六个部分的各行：

- 禁止主机（Ban host）——你可以通过包含一行形如 ban source-host source-port 的内容来禁止来自特定主机或主机组的连接，例如 ban blue.beard.com 80 或 ban 10.323. [100,1000]。（后者禁止来自 10.323.0.0 网络的所有计算机使用 100 到 1000 端口。）
- 身份验证（Authentication）——你可以通过包含一行形如 auth source-host source-port auth-method 的内容来配置 SOCKS 要求传输经过身份验证，例如 auth gingko.biloba.com 80 u。auth-method 通常是 n（无身份验证）、u（用户名/密码对）、k（Kerberos）或 ·（任何方法）之一。
- 接口（Interfaces）——SOCKS 允许你通过使用一行形如 interface hostpattern portpattern iface 的内容将某些网络接口链接到某些地址，其中 hostpattern 是要绑定的 IP 地址模式，portpattern 是一个端口或端口范围，iface 是接口。例如，interface 192.168.1. - eth0 将 eth0 绑定到 192.168.1.0 网络。使用接口行可以防止 IP 欺骗。
- 变量和标志（Variables and flags）——你可以通过创建一行形如 set variable value 的内容来设置环境变量。
- 代理（Proxies）——在某些情况下，你可能希望配置两个独立的网络，通过两端的 SOCKS 代理相互接受连接。你可以通过在 socks5.conf 文件中包含一行形如 proxy-type dest-host dest-port proxy-list 的内容来实现。proxy-type 是协议类型（socks5、socks4 或 noproxy），dest-host 和 dest-port 分别是目标地址和端口号，proxy-list 是以逗号分隔的服务器守护进程列表。
- 访问控制（Access control）——你可以通过使用一行形如 permit|deny auth command src-host dest-host src-port dest-port [user-list] 的内容来允许或拒绝服务。auth 是一种身份验证方法，如前所述。command 是允许的命令的逗号分隔列表。主机和端口是主机和端口标识符，user-list 是可选用户列表。

下面是一个 socks5.conf 示例文件：

```
interface 192.168.1. - eth0
interface - - eth1
permit - - - - -
```

这些接口行各自设置相应的接口——eth0 链接到 192.168.1.0 网络，而 eth1 适用于所有地址。permit 行相当宽松，允许任何用户进行任何连接。这一点加上没有禁止行或身份验证行，导致了一个非常宽松的代理服务器配置。

SOCKS 配置中一个非常重要的方面是禁用常规路由操作。毕竟，如果流量可以不经过 SOCKS 就直接通过路由器，那么运行 SOCKS 防火墙还有什么意义呢？有几种方法可以禁用路由：

- 除了代理服务器防火墙之外，再配置一个数据包过滤防火墙。如果数据包过滤器配置得足够严格，它可以几乎不放过任何流量，使 SOCKS 或其他某种应用层程序成为从内网到互联网的唯一路径。这种方法的优点是，如果某些服务是必要的且 SOCKS 处理得不好，你可以开放少数服务。例如，你可能希望让一个自定义服务器通过防火墙到达某些地址，而不是其他地址。
