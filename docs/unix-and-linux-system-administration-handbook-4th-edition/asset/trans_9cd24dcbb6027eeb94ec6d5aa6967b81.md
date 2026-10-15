

早期版本的 BIND 仅在区域的 SOA 记录中的刷新超时过期时，才会在主服务器和从服务器之间同步区域文件。如今，只要将 notify 设置为 yes，主服务器 **named** 在对应的区域数据库重新加载时就会自动通知其对等服务器。然后从服务器可以与主服务器会面以查看文件是否已更改，如果已更改，则更新其区域数据的副本。

你既可以将 notify 用作全局选项，也可作为区域特定选项。它能让区域文件在你进行更改后更快地收敛。默认情况下，每个授权服务器都会向每个其他授权服务器发送更新（Paul Vixie 将此系统称为“splattercast”）。如果将 notify 设置为 master-only，这种“话多”行为就会被遏制，通知仅发送给此服务器是主服务器的区域的从服务器。如果将 notify 选项设置为 explicit，则 **named** 仅通知 also-notify 子句中列出的服务器。

**named** 通常通过查看区域的 NS 记录来判断哪些机器是该区域的从服务器。如果指定了 also-notify，则一组未通过 NS 记录公布的额外服务器也可以被通知。当你的站点拥有内部服务器时，有时需要此调整。不要 also-notify stub 服务器；它们只关心区域的 NS 记录，可以等待常规更新周期。

also-notify 的目标是一组 IP 地址，以及可选的端口。对于具有多个网络接口的服务器，附加选项指定用于传出通知的 IP 地址和端口。localhost 区域是关闭通知的好地方，因为它们永远不会更改。如果你希望除主服务器之外的名称服务器通知二级服务器，则必须使用 allow-notify 子句。

```
recursion yes | no;                  [yes]
allow-recursion { address_match_list };  [all hosts]
```

recursion 选项指定 **named** 是否应代表你的用户递归处理查询。你可以在你的区域数据的授权服务器上启用此选项，但这是不被提倡的。最佳实践建议将授权服务器和缓存服务器分开。

如果此名称服务器应为你的客户端提供递归服务，请将 recursion 设置为 yes 并包含一个 allow-recursion 子句，以便 **named** 区分源自你站点的查询和远程查询。**named** 将对前者进行递归处理，对后者进行非递归处理。如果你的名称服务器为所有人回答递归查询，则它被称为开放解析器，可能成为某些攻击的反射器；请参阅 RFC5358。

```
recursive-clients number;             [1000]
max-cache-size number;                [unlimited]
```

如果你的服务器内存有限，你可能需要调整 recursive-clients 和 max-cache-size 选项。recursive-clients 控制服务器同时处理的递归查找数量；每个查找大约需要 20KiB 内存。max-cache-size 限制服务器用于缓存查询答案的内存量。如果缓存增长过大，named 会在记录的 TTL 到期前删除记录，以保持内存使用在限制之下。

## IP 端口利用

use-v4-udp-ports { range beg end; }; [range 1024 65535]
use-v6-udp-ports { range beg end; }; [range 1024 65535]

avoid-v4-udp-ports { port_list }; [empty]
avoid-v6-udp-ports { port_list }; [empty]

query-source v4-address [ port ] [any] # CAUTION, don’t use port
query-source v6-address [ port ] [any] # CAUTION, don’t use port

源端口在 DNS 世界中变得重要，因为 Dan Kaminsky 发现了 DNS 协议中的一个弱点，该弱点允许在名称服务器使用可预测的源端口和查询 ID 时进行 DNS 缓存中毒。UDP 端口的 use- 和 avoid- 选项与 named 软件的更改一起缓解了此攻击。不要使用 query-source 地址选项指定 DNS 查询的固定传出端口，否则你将撤销由大量随机端口提供的 Kaminsky 保护。

use-v*-udp-ports 的默认值是合适的，你通常不需要更改它们。如果你的防火墙阻止了此范围内的某些端口（例如，SunRPC 的端口 2049），那么你会遇到一个小问题。当你的名称服务器发送查询并使用被阻止的端口作为源时，防火墙会阻止答案，名称服务器最终会停止等待并再次发送查询。并非致命，但对卷入其中的用户来说很烦人。

为避免此问题，请使用 avoid-v*-udp-ports 选项使 BIND 避开被阻止的端口。防火墙阻止的任何高编号 UDP 端口都应包含在列表中。19 如果你因某些威胁攻击而更新防火墙，也请在此处更新端口列表。

query-source 选项让你可以指定传出查询时使用的 IP 地址。例如，你可能需要使用特定的 IP 地址才能通过防火墙或在内部和外部视图之间进行区分。

查询从随机的高编号端口发出，答案返回到这些相同的端口。因此，你的防火墙必须准备好接受随机高编号端口上的 UDP 数据包。一些系统管理员过去会设置特定的传出端口号，以便他们可以配置防火墙以识别该端口并仅接受该端口的 UDP 数据包。然而，在 Kaminsky 时代之后，此配置已不再安全。

如果你使用 query-source 选项，请仅指定你希望查询发送的 IP 地址；不要指定端口号。

