
## 嗅探网络包

嗅探网络包——听起来有点违法，对吗？其实不是，嗅探指的是查看 TCP/IP 网络包。其概念是捕获所有网络包以便你对其进行检查。

如果你喜欢嗅探 TCP/IP 包，可以使用 `tcpdump`，这是 Linux 自带的一个命令行工具。顾如其名，它会转储（打印）TCP/IP 网络包的头部。

要使用 `tcpdump`，请以 root 身份登录并在终端窗口中输入 `tcpdump` 命令。如果你想将输出保存到文件中并在稍后检查该文件，否则 `tcpdump` 将开始在窗口中快速闪过结果。例如，捕获 1000 个包并保存到名为 `tdout` 的文件中，尝试将 IP 地址转换为名称，输入以下命令：

```bash
tcpdump -c 1000 > tdout
```

捕获 1000 个包后，`tcpdump` 会退出。然后你可以检查输出文件 `tdout`。它是一个文本文件，你可以直接在文本编辑器中打开它，或输入 `more tdout` 来查看捕获的包。

## 启动配置网络

为了满足你的好奇心，这里是 `tcpdump` 典型输出中的几行：

```
20:05:57.723261 arp who-has 192.168.0.1 tell LNBECAN.rckov01.md.com.net
20:05:57.723843 arp reply 192.168.0.1 is-at 0:9:54:44:78:fc
20:06:01.732633 LNBECAN.rckov01.md.com.net:1038 > 192.168.0.6.auth: S53632100:53632100 (0) win 5840 <mas 1460,sackOK,timestamp 7300060zero_window: 0 (DP)
20:06:02.773072 LNBECAN.rckov01.md.com.net.ftp > 192.168.0.1596: P 1:72(71) ack win 5840 (DP)
20:06:04.55335 192.168.0.1596 > LNBECAN.rckov01.md.com.net.ftp : ack 72 win 65464 (DP)
20:06:05.462481 192.168.0.1596 > LNBECAN.rckov01.md.com.net.ftp : P 1:12(11) ack win 65464 (DP)
20:06:05.462595 LNBECAN.rckov01.md.com.net.ftp > 192.168.0.1596: ack 12 win 5840 (DP)
20:06:05.465384 LNBECAN.rckov01.md.com.net.ftp > 192.168.0.1596: P lines deleted...
```
