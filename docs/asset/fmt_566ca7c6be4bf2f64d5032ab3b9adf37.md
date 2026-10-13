
```
$TTL  86400
@       IN      SOA     @ root.localhost (
                            1 ; serial
                            28800 ; refresh
                            7200 ; retry
                            604800 ; expire
                            86400 ; ttl
)

@       IN      NS      localhost.

@       IN      A       127.0.0.1
```

分号 (`;`) 表示注释。分号后面的所有字符都被视为注释，并且不影响 DNS 配置文件的运行。

- 3. 通过选择 **文件** ▸ **另存为** 保存配置。

- 4. 在 **选择** 框中输入 `/var/named/local.zone`，然后点击 **确定**。

### 创建私有网络 zone 文件

接下来，你创建 `paunchy.zone` 文件，该文件服务于私有网络。此文件包含你的 zone 中所有机器的 A 和 C 记录（在这种情况下，zone 直接映射到 `paunchy.net` 域。）

- 1. 从 Gedit 文本编辑器中，从菜单选择 **文件** ▸ **新建**。

- 2. 输入以下配置。（当然，你可以选择你自己的机器名称。名称是任意的。事实上，IP 地址也是任意的。你可以选择任何你想要的不可路由地址空间。）

```
$TTL  86400
@       IN      SOA     paunchy.net.
                        root.paunchy.net. (
                            200112211
                            10800
                            3600
                            86400
                            3600
)
IN NS ns.paunchy.net.
IN A 192.168.1.254
; servers
veracruz IN A 192.168.1.254
www CNAME veracruz
ns CNAME veracruz
; workstations
chivas IN A 192.168.1.1 ; Linux
pumas IN A 192.168.1.2 ; Linux
tigres IN A 192.168.1.100 ; Windows
```

- 3. 通过选择 **文件::另存为** **保存配置**。

- 4. 在 **选择框** 中输入 **`/var/named/paunchy.zone`**，然后点击 **确定**。

### 创建反向 zone 文件

最后一步是为你的 zone 创建反向 DNS 查找文件。此文件是可选的，但非常有用。通过为网络提供反向查找功能，你可以指定一个数字 IP 地址并获取一个名称：

- 1. 回到 **Gedit** 文本编辑器，从菜单选择 **文件::新建**。

- 2. 创建反向 DNS 配置文件参数：

```
$TTL 86400
@ IN SOA paunchy.net root.paunchy.net
(
2002030801
28800
7200
604800
86400
)
@ IN NS paunchy.net.
; servers
254 IN PTR veracruz
; Linux workstations
1 IN PTR cancun
2 IN PTR veracruz
; Windows workstations
101 IN PTR cozumel
```

- 3. 选择 **文件::另存为**。

- 4. 在 **选择框** 中输入 **`/var/named/1.168.192.zone`**，然后点击 **确定**。

- 5. 创建 rndc 配置和密钥文件。`rndc` 实用工具用于控制名称服务器。输入此命令以自动创建配置和密钥：

- 6. 打开一个 GNOME 终端窗口，通过输入此命令创建 rndc 配置和密钥文件：

```
rndc-confgen
```

再次说明，文件名 `1.168.192.zone` 是任意的。你可以将其命名为 `reverse.zone` 或你想要的任何其他名称，只要你与 `/etc/named.conf` 文件中的名称匹配——也就是说，`named.conf` 需要调用反向 IP 地址数据库 `reverse.zone`，而不是 `1.168.192.zone`。

### 启动你的 DNS 服务器

在你创建了 DNS 配置和 zone 文件之后，你可以启动你的服务器：

- 1. 点击 GNOME 菜单并选择 系统设置→服务器设置→服务。

- 2. 找到 `named` 服务并点击其单选按钮。

此步骤选择服务器在启动时开始运行。

- 3. 点击 重新启动 按钮。

- 4. 点击弹出的信息窗口中的 确定 按钮。

你现在拥有一个 DNS 服务器。

![](img/8c094d1b36276212c03d10d898508a6e_255_0.png)

或者，你可以通过运行以下命令来启动 DNS 服务器：`/etc/init.d/named start`。

### 配置你的 DNS 客户端

要使用你新的 DNS 服务器，你必须配置你 LAN 上的主机，并修改你的 Linux 计算机上的 `/etc/resolv.conf` 文件。修改你的 Windows 机器上的网络设置。

修改 Linux 计算机上的 `resolv.conf` 文件，使其看起来像这样：

```
search paunchy.net
nameserver 192.168.1.254
```

你可以指定多达三个名称服务器，因此可以将 ISP 的名称服务器作为备用添加：

```text
search paunchy.net
nameserver 192.168.1.254
nameserver 198.59.115.2
```

打开一个 **GNOME 终端** 窗口并运行以下命令。

```text
host cancun
```

你将看到此结果：

```text
cancun.paunchy.net  has  address 192.168.1.121
```

**host** 命令提供了许多选项，可提供有关查询的更多信息。例如，你可以查看 *host* 命令获取信息的位置。在前面的示例中添加 verbose (`-v`) 选项，你就能看到以下信息。

```text
Trying "cancun.paunchy.net"
; ->HEADER<- opcode: QUERY,  status: NOERROR,  id: 18016
;  flags: qr aa rd ra;  QUERY: 1,  ANSWER: 1,  AUTHORITY: 1,
;       ADDITIONAL: 0

;  QUESTION  SECTION:
;cancun.paunchy.net.     IN     A

;  ANSWER  SECTION:
cancun.paunchy.net.     86400  IN  A  192.168.1.1

;  AUTHORITY  SECTION:
paunchy.net.            86400  IN  NS   ns.paunchy.net.1
Received 69 bytes from 192.168.1.120#53  in 263 ms
```

此列表说明了前面输出中各个部分的含义。

- **Question section（问题部分）：** 你可以在问题部分看到查询是 `cancun.paunchy.net`。请注意，我们只询问 `cancun` 的地址，但 `resolv.conf` 文件中的 `search` 参数指定将 `paunchy.net` 域追加到 `cancun`。你还可以看到 A 记录是查询的一部分——你正在请求一个 IP 地址。

- **Answer section（答案部分）：** 这是对你查询的回应。答案包括主机名和域名——`cancun.paunchy.net`——及其数字 IP 地址。答案部分还包括生存时间（TTL）值。

- **Authority section（授权部分）：** 这些数据显示了前面的答案部分中信息是在哪里找到的。你从刚刚构建的名称服务器——`192.168.1.254`——那里获得了答案。

你网络上的所有计算机都可以使用你的 DNS 服务器。你的 DNS 为所有内部机器提供地址。服务器会在必要时转发对外部地址的请求。

# 第 17 章

## 保护你的未来

### 本章内容

- 安全思维

- 防止入侵者

- 更新 Red Hat Linux 软件包

- 使用 `chkconfig` 停用服务

- 使用 Secure Shell 客户端
