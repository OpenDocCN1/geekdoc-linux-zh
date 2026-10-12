
```
IN NS ns2.yourdomain.com.
; 该域的邮件服务器
IN MX 10 mail.yourdomain.com.
; 公共服务器
ns1 IN A 123.45.67.1
ns2 IN A 123.45.67.2
mail IN A 123.45.67.2
www IN A 123.45.67.3
ftp IN A 123.45.67.4
; 局域网内的私有客户端
red IN A 10.0.0.2
blue IN A 10.0.0.3
green IN A 10.0.0.4
yellow IN A 10.0.0.5
; 文件结束
```

yourdomain.com 的区域文件包含包含该区域信息的资源记录。你的 DNS 服务器使用 TTL（生存时间）记录来告知存储你为该域名提供信息的名称服务器，在需要丢弃这些记录并获取新信息之前，可以保留这些记录多长时间。第一个值是整个区域的默认值，时间以秒为单位。因此，值为 86400 秒表示使用这些信息的客户端应每 24 小时获取一次关于该域名的新记录。

SOA 行标识了该域名的授权起点。@ 符号代表 yourdomain.com 名称。域名末尾必须有一个句点 (.)。该句点代表 Internet 的根服务器。如果你省略了句点，DNS 服务器会追加域名，因此 DNS 服务器将使用名称 yourdomain.com.yourdomain.com。hostmaster.yourdomain.com 行表示负责接收关于该域名电子邮件的人员的电子邮件地址。（第一个点变为 @ 符号，结果变为 hostmaster@yourdomain.com。）关于 SOA 记录的其他信息如下：

- **Serial（序列号）：** 可以从任意数字开始。如果区域记录发生更改，请增加序列号，以提醒其他服务器它们需要获取关于你域名的新数据。

> **注意：** 如果在更改区域记录后忘记增加序列号，缓存此数据的其他服务器将永远不会获取你的更改。

- **Refresh（刷新）：** 定义用于该区域的从 DNS 服务器检查更改的频率。（此处，28800 秒代表 8 小时。）
- **Retry（重试）：** 如果从服务器无法联系到主服务器，它会在此重试间隔之后再次尝试。（此处，14400 秒代表 4 小时。）
- **Expire（过期）：** 如果从服务器无法在过期时间内（此处为 3600000 秒，或 1000 小时）联系到主服务器，从服务器将丢弃数据。
- **Minimum（最小值）：** 定义负面答案的缓存生存时间。（此处为 86400 秒，或 240 小时。）

名称服务器记录（NS）定义了代表此区域的名称服务器。在这种情况下，NS 记录定义了 *yourdomain.com* 中名为 *ns1* 和 *ns2* 的主机。MX 记录指示该域名的邮件服务器位置，以便 DNS 服务器可以将电子邮件转发给 *yourdomain.com* 中的用户。文件的其余部分定义了与该域名关联的私有客户端和公共服务器的 IP 地址。请注意，位于地址 123.45.67.2 的服务器既作为邮件服务器，也作为从 DNS 服务器。

示例中的另一个新文件是 *yourlan.db* 文件，其中包含为你的局域网上的计算机执行反向 IP 查找所需的信息。以下是一个示例：

```
$TTL		86400
@	IN	SOA	yourdomain.com. hostmaster.yourdomain.com.
	(
		2002052701		; 序列号
		28800		; 刷新
		14400		; 重试
		3600000		; 过期
		86400 		) ; 最小值
	IN	NS	ns1.yourdomain.com.
1	IN	PTR	yourdomain.com.
2	IN	PTR	red.yourdomain.com.
3	IN	PTR	blue.yourdomain.com.
4	IN	PTR	green.yourdomain.com.
5	IN	PTR	yellow.yourdomain.com.
; 文件结束
```

SOA 记录与 *yourdomain.com.db* 文件中的相同。NS 行将 *ns1* 定义为 *yourdomain.com* 域的名称服务器。其余记录是指向主机名的指针，这些主机名从 10.0.0. 网络进行反向映射。这些记录代表 DNS 服务器（*yourdomain.com*）以及局域网（*red、blue、green 和 yellow*）上每个客户端的地址。

在你完成创建自己的区域文件后，可以使用 *named-checkzone* 命令确保每个区域文件格式正确。以下是如何运行 *named-checkzone* 命令（作为 root 用户）来检查 *yourdomain.com.db* 文件：

```
# named-checkzone yourdomain.com /var/named/yourdomain.com.db
区域 yourdomain.com/IN: 已加载序列号 2002052701
OK
```

## 启动 named (DNS) 守护进程

若要立即启动 `named` 守护进程以检查其是否正常工作，请输入以下内容（作为 root 用户）：

```
# /etc/init.d/named start
```

如果 `named` 守护进程成功启动，你的 DNS 服务器的客户端应开始获取关于你域名的信息。若要设置 `named` 守护进程在系统每次启动时都运行，请输入以下内容：

```
# chkconfig named on
```

请记住，每当你对 `named.conf` 或任何区域文件做出更改时，你都必须增加序列号，以便检查你域名记录的人能够获取这些更改。之后，你还应该重启 `named` 服务（作为 root 用户），如下所示：

```
# /etc/init.d/named restart
```

如果你看到 `Starting` named 消息，你的 DNS 服务器可能已启动并正在运行。如果你想确保你的服务器正在正确解析地址，下一节描述了你可以用来检查 DNS 名称服务器的一些工具。

## 检查 DNS 是否工作

确保你的 DNS 服务器正常工作的最佳方法是观察其实际操作情况。以下是一些可用于检查 DNS 服务器的命令。第一个示例使用 `host` 命令来确定本地域中名为 `blue` 的主机的 IP 地址。

```
# host blue
blue.yourdomain.com 的地址为 10.0.0.3
```

除了使用简单主机名来获取计算机的 IP 地址外，你还可以输入 IP 地址（而非名称）或完全限定主机名。在以下示例中，使用 `dig` 命令配合域名来获取有关域地址的信息：

```
# dig yourdomain.com
; <<>> DiG 9.2.0 <<>> yourdomain.net
; 全局选项: printcmd
; 收到答案:
; ->>HEADER<- opcode: QUERY, status: NOERROR, id: 63309
; 标志: qr aa rd ra; 查询: 1, 答案: 1, 权威: 2, 附加: 2
; 问题部分:
;yourdomain.com.            IN A

; 答案部分:
yourdomain.com.        604800 IN A 123.45.67.1

; 权威部分:
yourdomain.com.        604800 IN NS ns1.yourdomain.com.
yourdomain.com.        604800 IN NS ns2.yourdomain.com.

; 附加部分:
ns1.yourdomain.com.    604800 IN A 123.45.67.1
ns2.yourdomain.com.    604800 IN A 123.45.67.2

; 查询时间: 24 毫秒
; 服务器: 123.45.67.1#53(123.45.67.1)
; 时间: 2002年5月9日 星期四 02:12:32
; 消息大小 接收: 129
```

dig 输出中的部分包括问题部分、答案部分、权威部分和附加部分。结果显示你正在查询的域名相关的名称服务器分配和地址。nslookup 命令是另一个可用于查找域名信息的工具。在以下示例中，nslookup 查找正在解析 mail.yourdomain.com 地址的服务器：

```
# nslookup www.yourdomain.com
服务器:			123.45.67.1
地址:		123.45.67.1#53

名称:	mail.yourdomain.com
地址: 123.45.67.3
```

nslookup 命令产生的输出包括正在处理请求的计算机名称及其 IP 地址，以及你正在询问的计算机的名称和地址。

若要检查在本地系统上运行的 named 服务器的状态，你可以使用启动 named 守护进程相同的脚本。输入以下内容以检查你的 DNS 服务器守护进程的状态：

```
# /etc/init.d/named status
区域数量: 6
调试级别: 0
传输运行中: 0
传输延迟: 0
正在进行中的 SOA 查询: 0
查询日志记录已关闭
服务器已启动并正在运行
```
