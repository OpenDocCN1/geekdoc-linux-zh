
输出表明两个文件都是正确的，并且 `named-checkzone` 命令能够加载新的序列号。在这种情况下，序列号代表 2008 年 4 月 27 日的第一个序列号（`2008042701`）。

注意：你可以使用 `named-compilezone` 命令来代替使用 `named-checkzone` 命令。这两个命令之间的区别在于 `named-compilezone` 将区域内容转储到你选择的文件中。

验证 DNS 服务器是否正常工作的最佳方法是观察它的运行。以下是你可以使用的的一些命令来检查你的 DNS 服务器。第一个示例使用 `host` 命令获取本地局域网中主机 `blue` 的 IP 地址：

```
# host blue
blue.yourdomain.com has address 10.0.0.3
```

与其使用简单的主机名来获取计算机的 IP 地址，你可以输入 IP 地址（而不是名称）或完全限定主机名。在示例中，命令使用域名来获取有关域名地址的信息：

```
# dig yourdomain.com
; >>> DIG 9.5.02<<< yourdomain.com
;; global options: printcmd
;; Got answer:
;; -->>HEADER<< opcode: QUERY, status: NOERROR, id: 43728
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 0
;; QUESTION SECTION:
yourdomain.com. IN A
;; AUTHORITY SECTION:
yourdomain.com. 604800 IN NS ns1.yourdomain.com.
yourdomain.com. 604800 IN NS ns2.yourdomain.com.
;; Query time: 24 msec
;; SERVER: 127.0.0.1#53
;; WHEN: Mon Jun 9 12:32:15 2008
```

请记住，当你修改 `named.conf` 或任何区域文件时，必须增加序列号，以便检查你的域名记录能够获取到这些更改。之后，你应该按照如下方式（作为 root 用户）重启 `named` 服务：

```
# /etc/init.d/named restart
```

然后你应该考虑将服务器的本地地址写入其自身的 `/etc/resolv.conf` 文件。例如，`/etc/resolv.conf` 文件可以包含以下内容：

```
yourdomain.com
nameserver 127.0.0.1
```

如果你看到“Starting”消息，你的 DNS 服务器可能已经启动并正在运行。如果你想确保你的服务器正确解析了地址，下一节“检查 DNS 是否工作”描述了一些你可以用来检查 DNS 名称服务器的工具。

## 检查 DNS 是否工作

验证 DNS 服务器是否正常工作的最佳方法是观察它的运行。以下是你可以使用的的一些命令来检查你的 DNS 服务器。第一个示例使用 `host` 命令获取本地局域网中主机 `blue` 的 IP 地址：

```
# host blue
blue.yourdomain.com has address 10.0.0.3
```

与其使用简单的主机名来获取计算机的 IP 地址，你可以输入 IP 地址（而不是名称）或完全限定主机名。在示例中，命令使用域名来获取有关域名地址的信息：

```
# dig yourdomain.com
; >>> DIG 9.5.02<<< yourdomain.com
;; global options: printcmd
;; Got answer:
;; -->>HEADER<< opcode: QUERY, status: NOERROR, id: 43728
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 0
;; QUESTION SECTION:
```
