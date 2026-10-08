
都将 `eth0` 接口设置为 `ipsec0`。然而，后者支持通过 PPP 接口使用 IPSEC。如果不使用默认设置 `interfaces=%defaultroute`，指定的接口将是该网关与其他 IPSEC 网关通信的唯一接口。

`klipsdebug=none` 选择 KLIPS（内核 IPSec 代码）的调试输出。默认值 `none` 表示无调试输出，`all` 表示完整输出。

`plutebug=none` 选择 Pluto 密钥的调试输出。默认值 `none` 表示无调试输出，`all` 表示完整输出。

`plutoload=%search` 指定 Pluto 启动时按名称自动加载到内存中的连接。默认值不是空，`%search` 使用 `auto-add` 加载所有连接。

`plutostart=%search` 指定 Pluto 启动时按名称自动协商的连接。默认不是空，`%search` 使用 `auto=start` 启动所有连接。

# FreeSwan/WAN VPN | 1
## 第 3 章

### conn deep-mail
此选项指定用于标识使用 IPSEC 创建的连接规范的名称。通过连接两端来命名连接是一个很好的习惯，可以避免错误。例如，`deep.openapi` 和 `mail.openapi.com` 网关服务器之间的链接可以命名为 "`deep-mail`"，或者蒙特利尔和巴黎办公室之间的链接命名为 "`montreal-paris`"。

请注意，名称 "`deep-mail`" 或你选择的任何名称，在两个网关的 `ipsec.conf` 文件中应该是相同的。换句话说，你对第二个网关的 `/etc/ipsec.conf` 文件中应该做的唯一更改是将 "`interfaces=line`" 修改为与第二个网关用于 IPSec 连接的接口匹配，当然，这与第一个网关是不同的。例如，如果两个网关都使用 `eth0` 接口进行 IPSec 通信，则你不需要更改第二个网关上的 `interfaces=` 这一行。另一种情况下，如果第一个网关使用 `eth0` 而第二个网关使用 `eth1`，则你必须更改第二个网关上的 `interfaces=` 行以匹配接口 `eth1`。

`left=208.164.186.1`
此选项指定用于与另一个网关通信的外部接口 IP 地址。

`leftsubnet=192.168.1.0/24`
此选项指定网关后私有子网的 IP 网络或地址。

`leftnexthop=205.151.222.250`
此选项指定相应方向上的第一个路由器或 ISP 路由器的 IP 地址。

`right=208.164.186.2`
此解释与 "`left=`" 相同，但针对右端。

`rightsubnet=192.168.1.0/24`
此解释与 "`leftsubnet=`" 相同，但针对右端。

`rightnexthop=205.151.222.251`
此解释与 "`leftnexthop`" 相同，但针对右端。

`keyingtries=0`
此选项指定在（重）密钥协商中应进行多少次尝试（整数）。建议默认值为 0（无限重试）。

`auth=ah`
此选项指定是否应单独使用 AH（认证头）进行认证，或将其作为 ESP（封装安全载荷）服务的一部分。当 IP 头部外露以防止中间人攻击时，这种方法是优的。

`auto-start`
此选项指定在 IPSec 启动时是否执行自动启动操作。

> 注意：此 "`ipsec.conf`" 配置中任何地方的数据不匹配都会导致 FreeSwan 失败并记录各种错误信息。

### 步骤 1
- 要创建共享密钥，请使用以下命令：
```bash
root@deep]# ipsec ranbits 256 > temp
```
使用 `ranbits()` 工具在名为 "`temp`" 的文件中创建随机密钥。如果没有可用的熵，`ranbits` 工具可能会暂停几秒钟。完成后，不要忘记立即删除该文件。

### 步骤 2
现在我们已经在 "`temp`" 文件中创建了密钥密钥，我们必须将其放入 `/etc/ipsec.secrets` 文件中。在编辑 `ipsec.secrets` 文件时，你应该会在编辑器中看到类似下面的的内容。每行都包含两个网关的地址加上密钥。它看起来应该是这样的：
```bash
# 此文件保存密钥，目前是唯一的 Inter-Pluto
# 认证机制。请查看 ipsec-pluto($) 管理。每个密钥
# (稍微简化了) 对应一对协商的主机。
# 共享密钥是任意字符字符串，并且应该足够长
# 且难以猜测。
```
```bash
# 注意，所有密钥绝不能包含在引号中，即使它们内部
# 没有空格。
```
```bash
10.0.0.1 11.0.0.1 "jXVs1kVTulkVRNTjSum444jRuU1mlkkku2nkW3VuVWZJRnnRukeU1WnnRT"
```
编辑 `ipsec.secrets` 文件：
```bash
10.0.0.1 11.0.0.1 "jXVs1kVTulkVRNTjSum444jRuU1mlkkku2nkW3VuVWZJRnnRukeU1WnnRT"
```
更改默认密钥：
读取：
```bash
208.164.186.1 208.164.186.2
"0x97a8cc31_2e9914f_d230589_cd84b57_dc07b1_74b6f3_19c401a80496ed"
```
"`208.164.186.1`" 和 "`208.164.186.2`" 是两个网关的 IP 地址，而 "`0x97a8cc31_2e9914f_d230589_cd84b57_dc07b1_74b6f3_19c401a80496ed`"（注意需要引号）是我们在通过命令 `ipsec ranbits 256 > temp` 在 "`temp`" 文件生成的共享密钥。

### 步骤 3
`ipsec.conf` 和 `ipsec.secrets` 文件必须复制到第二个网关，并在两端保持相同。唯一的例外是 `ipsec.conf` 文件，它必须包含带有第二个网关正确设置的 `config` 部分。

> 注意：`/etc/ipsec.secrets` 文件的权限应为 600，所有者为 "`root`"。`ipsec.conf` 文件权限应为 644，所有者为 "`root`"。

## 配置私密钥
回 FreeSwan 软件有两种密钥：预共享密钥和 RSA 私密钥。某些人倾向于使用 RSA 私密钥对对方主机进行认证。在这种情况下，你必须按照描述修改你的 `ipsec.conf` 和 `ipsec.secrets` 文件。你需要为每个网关创建一个独立的 RSA 密钥。每个网关在自己的 `ipsec.secrets` 文件中获取密钥，公钥进入 `ipsec.conf` 的 `config` 描述中。

为每个网关创建一个 RSA 密钥：使用以下命令：
- 在第一个网关 (`deep`) 使用以下命令：
```bash
root@deep]# cd /
root@deep]# ipsec rsagkey --verbose 1024 > deep-keys
```
计算质数和模数...
从 `/dev/random` 获取 64 个随机字节
寻找质数...
30 次尝试后找到
从 `/dev/random` 获取 64 个随机字节
寻找质数...
230 次尝试后找到
交换质数使 p 较大
计算 `(p-1)*(q-1)`...
计算 `d`...
计算指数、系数...
输出...

- 在第二个网关 (`main`) 使用以下命令：
```bash
root@main]# cd /
root@main]# ipsec rsagkey --verbose 1024 > main-keys
```
计算质数和模数...
从 `/dev/random` 获取 64 个随机字节
寻找质数...
30 次尝试后找到
从 `/dev/random` 获取 64 个随机字节
寻找质数...
230 次尝试后找到
交换质数使 p 较大
计算 `(p-1)*(q-1)`...
计算 `d`...
计算指数、系数...
输出...

`rsagkey` 工具生成一对 1024 位签名的 RSA 公私密钥，并将其放入第二个网关的 `deep-keys (main-keys)` 中。私钥可以原封地插入 `ipsec.secrets` 文件，公钥插入 `ipsec.conf` 文件。

> 注意：如果无法立即获得熵，`rsagkey` 工具可能会暂停几秒。你可能想进行一些额外的活动，如随机移动鼠标。完成后，应立即删除临时 RSA "`deep-keys`" 和 "`main-keys`" 文件。不要忘记删除 `deep-keys` 和 `main-keys` RSA 文件。

### 步骤 2
修改你的 `/etc/ipsec.conf` 文件以便每个网关使用 RSA 公钥：编辑原始 `ipsec.conf` 文件 (`vi /etc/ipsec.conf`) 并在两个网关的 `ipsec.conf` 节点描述中添加以下与 RSA 相关的参数：
```bash
# 示例连接
conn deep-mail
left=208.164.186.1
leftsubnet=192.168.1.0/24
leftnexthop=205.151.222.250
right=208.164.186.2
rightsubnet=192.168.1.0/24
rightnexthop=205.151.222.251
keyries=0
authby=rsa
leftrsigkey=<Public key of deep>
rightrsigkey=<Public key of mail>
auto=start
```
`authby=rsa`
此参数指定两个安全网关如何相互认证。默认值是 `secret`（用于共享密钥）。由于我们决定使用 RSA 数字签名，我们必须指定 `rsa`。

`leftrsigkey=<Public key of deep>`
此参数指定左端用于用于签名认证的密钥。在我们的示例中，`left` 是 `208.164.186.1`，代表 `deep.opens.com`，因此我们必须将 `deep` 的公钥放入此处。

`rightrsigkey=<Public key of mail>`
此参数指定右端用于用于签名认证的密钥。在我们的示例中，`right` 是 `208.164.186.2`，代表 `mail.opens.com`，因此我们必须将 `mail` 的公钥放入此处。

# RSA 网关深层 (deep-keys):
```
# @deep # vi cd
# @deep # vi deep-keys
```
```
# 1024 bits, 2000年2月4日周五 05:05:19
# 用于签名，对于加密极不安全
# @nist-ecp-031003391a5e8b3f53d8a529ef26648fd79f51b1f62309cceaf801ea9cb74
bcbfc5b1a4e660889d3a2b54e470c3546c3a5b2ce9d1145ff0b35427e0c4a38f9a78fe729cdcb
d476892fd7a6919a931b483c4a2e5d944f6b8144a5f4b41a4a5544211113333333111677777777888811088502a1c111
```
```
Main:
09a5e5b10df5f5038a52e4f79687f15b1f62309cceaf801ea9cb74bcfb5470c3546c3a5b2ce9d1145ff0b35427e0c4a38f9a78fe729cdcb
92e431b8c4a2e5d944f6b8144a5f4b41a4a55442111133333331111677777777888811088502a1c111
085a1111
```
```
Public: 0x3
# 除此部分外的所有内容均为秘密
```
```
Private:
0x5c71a8b508d2d3f1b6481b0402d192db7b75c11eb4b731229903ae7f729cdcb
6f5d2e111172224117775555554c3334777774444447777700
0x99a99977772222209999333711111a66999999999777788888880000000066666663366666666666666222111111111111111111
```
```
Exponent:1
0x816c65a5a4f4b4b2c1426e27f9a44e11f49965371b8f96c9d90a503c3e8ec50557
4c2c2a5555e6f6f3355110806c13337f97781d1a8cb8
```
```
Coefficient:
0x10d9a45c2298d411dbdb4b2333b3237f0a3ccaff82da9b5d51449b800705f7e33f183cd
d80f550462d67f2f637f7a531a737853018650f173a725
```
# RSA 网关邮件 (mail-keys):
```
# @mail # cd
# @mail # vi mail-keys
```
```
# 1024 bits, 2000年2月4日周五 05:46:59
# 用于签名，对于加密极不安全
# @nist-ecp-031003391a5e8b3f53d8a529ef26648fd79f51b1f62309cceaf801ea9cb74
bcbfc5b1a4e660889d3a2b54e470c3546c3a5b2ce9d1145ff0b35427e0c4a38f9a78fe729cdcb
d476892fd7a6919a931b483c4a2e5d944f6b8144a5f4b41a4a5544211113333333111677777777888811088502a1c111
```
Main:
0xb3f7c111100d5f5e8875c442d3814444117777377772222888800000077777777111177755555442222227777777777777111111111666666664444444444444444
Public: 0x3 # 除此部分外的所有内容均为秘密
```
Private:
0x5c71a8b508d2d3f1b6481b0402d192db7b75c11eb4b731229903ae7f729cdcb
6f5d2e111172224117775555554c3334777774444447777700
0x99a99977772222209999333711111a66999999999777788888880000000066666663366666666666666222111111111111111111
```
```
Exponent:1
0x816c65a5a4f4b4b2c1426e27f9a44e11f4996531b8f96c9d90a503c3e8ec50557
4c2c2a5555e6f6f3355110806c13337f97781d1a8cb8
```
```
Coefficient:
0x10d9a45c2298d411dbdb4b2333b3237f0a3ccaff82da9b5d51449b800705f7e33f183cd
d80f550462d67f2f637f7a531a737853018650f173a725
```
