
b. 滚动到 `HOME` 目录并设置为 `/etc/directory`。

c. 滚动到 `[ CA_default ]` 下的 `dir` 指令。

d. 将 `dir` 的值设置为 `/etc/directory`。

- 保存更改并关闭文件。

- 验证当前目录是否为 `/etc/directory`。

- 在 shell 提示符处输入 `openssl req -newkey rsa:2048 -x509 -days 365 -keyout private/cakey.pem -out cacert.pem` 创建自签名根证书。

- 根据提示，为私钥输入口令。

- 根据提示，输入你的地理位置信息。

- 根据提示，输入你的组织信息。

- 根据提示，输入你的个人信息。

- 在 shell 提示符处，`touch index.txt ; echo 01 > serial`

- 在 shell 提示符处输入 `openssl req -new -keyout private/ca_prv_key.pem -out certs/ca_req.pem -days 365` 创建证书签名请求。

- 根据提示，输入口令。

- 根据提示，输入你的地理位置信息。

- 根据提示，输入你的组织信息。

- 根据提示，输入你的个人信息。

- 根据提示，为证书输入挑战密码。

- 当提示可选的公司名称时，按回车键。

- 输入 `openssl ca -policy policy_anything -notext -out certs/newcertert.pem -infiles certs/ca_req.pem` 签名证书签名请求。

- 根据提示，输入口令。

- 当提示签名证书时，输入 `y`。

- 当提示提交时，输入 `y`。

4. 重复这些步骤，在另一个参与隧道的宿主机上生成证书。

密钥生成后，你就可以准备编辑 VPN 配置文件了。让我们接下来来讨论如何做到这一点。

## 配置 `/etc/ipsec.conf`

你的 VPN 服务器的行为通过 `/etc/ipsec.conf` 文件进行配置，其部分内容如图 11.8 所示。

### 在 SLES9 上实现 VPN 服务器

图 11.8

`/etc/ipsec.conf` 文件：

```
# /etc/ipsec.conf FreeSwan IPsec 配置文件
# RSID: ipsec.conf.in.v 1.11 2003/06/13 23:28:41 sam Exp $

# 这一行：/usr/share/doc/packages/freesman/ipsec.conf-sample

# 手册：
# ipsec.conf

# 帮助：
# http://www.strongsec.com/freesman/install.htm

# 版本 2.0 符合 ipsec 规范
# 基础配置
# 调试控制："none" (对于大多数)，"all" 用于列表。
# 存活
# 证书吊销列表处理
# 关键间隔 600
# 严格策略
# 默认设置 = 0 (关闭)
# 开启 (如果安装了补丁)
```

该文件中包含四个部分：

- 基础配置——该部分包含用于配置 `pluto` 守护进程的基本参数。如图 11.8 所示。
- 默认设置——该部分用于配置连接的默认参数。可以在文件中再次声明以覆盖它们。
- 机会性加密——该部分配置机会性加密。默认情况下禁用机会性加密。
- 连接定义——该部分用于定义和配置连接。

为了深入研究此文件，我们需要花时间讨论所使用的术语：

- 网关到网关 VPN——该术语指的是连接两个网关的 VPN 配置。在这种情况下，假设网关具有静态 IP 地址。
- 漫游者——该术语指的是另一种 VPN 配置，远程用户连接到笔记本电脑或个人电脑（漫游客户端）。此外，漫游者可能在其网络中的某处使用了 NAT 路由器来隐藏其身份。
- 左和右——在整个 `ipsec.conf` 文件中，你会看到左和右这两个术语。它们指的是 VPN 隧道的端点。如果你画出隧道图，左指的是左主机，右指的是右主机。遗憾的是，现实并非如此简单。通常的约定是使用左指向自己的系统（客户端或服务器），右指向隧道另一端的主机。
- 手动密钥——对于手动密钥，VPN 隧道两端的主机共享一个共同密钥。为了实现这一目标，你必须在设置隧道之前手动（安全地！）在主机之间拷贝共同密钥。
- 自动密钥——对于自动密钥，VPN 隧道两端的主机相互进行身份验证并交换密钥。

`/etc/ipsec.conf` 文件预定义了一个示例连接供你使用。如图 11.9 所示。

图 11.9

示例连接定义。

```
auto-ignore
#conn Osec1
#  auto-ignore
# 在此处添加连接
# 示例 VPN 连接
#            conn sample
#              # 左安全网关，其后的子网，下一跳
#            left=defaultroute
#            right=%defaultroute

#            leftcert=left-Cert.pem
#            leftsubnet=172.16.0.0/24
#              # 右安全网关，其后的子网，下一跳
# 向左，
#            right=10.12.12.1
                   right="(右安全网关的区分识别码)"
#            rightsubnet=192.168.1.0/24
                  # 授权此连接，但并不实际启动 ipsec
  auto=startup
#            # 取消此连接。
```

要配置连接，你需要理解连接定义中的以下元素：

# 在 SLES 9 上实现 VPN 服务器

- `left`—指定隧道左端的 IP 地址。如果系统只有一个接口，可以将其设置为 `%defaultroute`，以使用默认路由接口的 IP 地址。
- `leftcert`—指定用于 VPN 的证书文件。
- `leftsubnet`—如果 VPN 服务器同时用用作路由器，则此参数使用 `ip_address/mask` 语法指定路由器另一侧的子网。
- `lefinthop`—此参数用于指定默认网关的 IP 地址。如果你在 `left` 中使用了 `%defaultroute`，则不需要此参数。
- `leftid`—指定左侧主机的身份。在 SLES 9 中，该身份是从用于加密数据的证书文件中获取的，稍后我们将看到这一点。
- `leftrasagikey`—指定左侧主机使用的公钥。设置为 `%cert` 值会让 `ipsec` 从证书中提取密钥。
- `right`—指定隧道右端的 IP 地址。你可以使用 `%any` 来标识任何可以作为隧道右端的主机。
- `rightsubnet`—如果右侧主机是路由器，此参数使用 `ip_address/mask` 语法指定路由器另一侧的子网。
- `rightcert`—指定用于 VPN 的证书文件。
- `rightthop`—此参数用于指定默认网关的 IP 地址。如果你在 `right` 中使用了 `%defaultroute`，则不需要此参数。
- `rightid`—指定右侧主机的身份。在 SLES 9 中，该身份是从用于加密数据的证书文件中获取的，稍后我们将看到这一点。
- `auto`—此参数可以设置为 `add` 或 `start`。当设置为 `add` 时，`ipsec` 将加载配置但不建立连接；设置为 `start` 时，`ipsec` 将加载配置并尝试建立连接。

让我们来看示例连接定义：

```
conn server2
authby=rasig
auto=add
esp=aes,3des
keytries=3
left=...
leftcert=/etc/ipsec.d/certs/newcert.pem
leftid-emailAddress=root@cle9.com,CN=fs1,OU=IS,NTI,L=Sq,ST=Utah,C=US
leftrsasigkey=%cert
leftsubnet=10.0.0.0/8
pfs=yes
right=192.168.1.48
rightcert=/etc/ipsec.d/certs/cert_01.pem
rightid=emailAddress=root@c69.com,CN=fs2,O=US,OU=NTI,L=Sq,ST=Utah,C=US
rightrsasigkey=%cert
```

在这个示例中，VPN 隧道的左端 IP 地址为 192.168.1.47。它是一个路由器，后面有一个地址为 10.0.0.0 的子网。隧道右端的主机 IP 地址为 192.168.1.48。它不是路由器，后面没有子网。另外请注意，公钥（`leftrsasigkey` 和 `rightrsasigkey`）是从每个主机的相应证书文件中提取的。

要建立 VPN 隧道，你需要将此文件复制到左右两端主机上，将相应的证书和密钥文件复制到列出的位置，并通过输入 `rcipsec start` 在两个主机上启动 `ipsec`。

你也可以使用 YaST 在 SLES 9 上配置 VPN。让我们看看如何操作。

# 使用 YaST 配置 VPN

YaST VPN 模块用于配置 SLES 9 上 VPN 隧道的末端。要实现此操作，请完成以下步骤：

1. 通过完成以下操作在左右主机之间分发证书和密钥：
   a. 准备一个软盘驱动。
   b. 在磁盘上创建一个名为 `rightCert` 的目录。
   c. 将右侧主机的证书和密钥文件复制到此目录。
   d. 在磁盘上创建另一个名为 `leftCert` 的目录。
   e. 将左侧主机的证书和密钥文件复制到此目录。

2. 在左主机上启动 YaST。

3. 选择“安全与用户”（Security and Users）、VPN。显示如图 11.10 所示。

4. 选择“启用 VPN 服务”（Enable VPN Services）。

5. 当提示选择证书时，选择“是”（Yes）。显示如图 11.11 所示。

# 在 SLES 9 上实现 VPN 服务器

图 11.10

初始 YaST VPN 屏幕。

![](img/9a8db5c8d556a70e5a1096951da47eec_546_0.png)

图 11.11

配置 VPN 证书。

![](img/9a8db5c8d556a70e5a1096951da47eec_546_1.png)

# 第 11 章：使用 SLES 9 实现虚拟专用网络

6. 通过完成以下操作配置你的 VPN 证书：
   a. 在“当前视图”（Current View）下拉列表中，选择“CA 证书”（CA Certificates）。
   b. 选择“导入”（Import）；然后浏览并选择你的 CA 证书。
   c. 在“当前视图”下拉列表中，选择“证书”（Certificates）。
   d. 选择“导入”（Import）；然后浏览并选择你的证书。
   e. 在“当前视图”下拉列表中，选择“密钥”（Keys）。
   f. 选择“导入”（Import）；然后浏览并选择你的私钥。
   g. 选择“下一步”（Next）。显示如图 11.12 所示：

图 11.12

配置 VPN 角色。

![](img/9a8db5c8d556a70e5a1096951da47eec_547_0.png)

7. 通过完成以下操作配置你的 VPN 连接：
   a. 如果你正在为远程客户端配置 VPN 服务器，选择“战士服务器”（Server for Warriors）。如果你正在将系统配置为 VPN 客户端，选择“战士客户端”（Warrior client）。如果你正在连接两个服务器连接（分机构/家庭办公室场景），选择“自定义”（Custom）。出于我们的目的，我们将执行这些步骤。
   b. 选择“下一步”（Next）。
   c. 提示时，为连接输入名称；然后选择“确定”（OK）。显示如图 11.13 所示：

# 在 SLES 9 上实现 VPN 服务器

图 11.13

配置左主机。

![](img/9a8db5c8d556a70e5a1096951da47eec_548_0.png)

d. 在“本地 IP 地址”下拉列表中，选择左服务器的 IP 地址或 `%default`。
e. 如果系统充当子网之间的网关，标记为“网关”（Gateway）；然后从“本地子网”（Local Subnet）下拉列表中选择网关后的子网。
f. 在“证书”（Certificate）字段中，确保已选择你的主机的证书文件。
g. 验证来自证书文件的主机 ID 显示在“标识”（Identification）字段中；然后选择“下一步”（Next）。
h. 在“远程地址”（Remote Address）下拉列表中执行以下操作之一：
   - 如果你正在配置战士服务器，选择 `%any`。
   - 如果你正在配置服务器到服务器连接，输入远程服务器的 IP 地址。
i. 如果远程服务器将作为另一个子网的网关，标记为“网关”（Gateway）；然后从“远程子网”（Remote Subnet）下拉列表中选择子网。
j. 在“证书”字段中，选择“导入”（Import）、“导入”（Import）。
k. 从软盘中浏览并选择右侧主机的证书文件。

# 第 11 章：使用 SLES 9 实现虚拟专用网络

图 11.14

配置右主机。

![](img/9a8db5c8d556a70e5a1096951da47eec_549_0.png)

l. 选择“下一步”（Next）。
m. 在“证书”下拉列表中，选择刚刚导入的证书。
n. 验证从证书获取的主机 ID 显示在“标识”字段中。
o. 选择“下一步”（Next）。
p. 在“启动期间”（During Boot）下拉列表中，选择以下之一：
   - 启动连接（Initiate Connection）：此选项将立即尝试连接远程系统。如果远程不可用，将导致连接失败。
   - 准备连接（Prepare Connection）：此选项将打开并监听连接请求。（大多数情况下是此选项。）
   - 忽略连接（Ignore Connection）：此选项将不会加载连接。
q. 选择“确定”（OK）
r. 选择“完成”（Finish）。

此时，VPN 隧道的左端已经建立。现在你需要配置隧道的右端。完成以下操作：

1. 在右主机上启动 YaST。
2. 选择“安全与用户”、VPN。
3. 选择“启用 VPN 服务”。
4. 提示选择证书时，选择“是”（Yes）。
5. 通过完成以下操作配置你的 VPN 证书：
   a. 在“当前视图”下拉列表中，选择“CA 证书”。
   b. 选择“导入”（Import）；然后浏览并选择你的 CA 证书。
   c. 在“当前视图”下拉列表中，选择“证书”。
   d. 选择“导入”（Import）；然后浏览并选择你的证书。
   e. 在“当前视图”下拉列表中，选择“密钥”。
   f. 选择“导入”（Import）；然后浏览并选择你的私钥。
   g. 提示时，输入你的 RSA 密钥密码。
   h. 选择“下一步”（Next）

6. 通过完成以下操作配置你的 VPN 连接：
   a. 配置正在创建的连接类型（我们假设为“自定义”）。
   b. 选择“下一步”（Next）。
   c. 提示时，为连接输入名称；然后选择“确定”（OK）。
   d. 在“本地 IP 地址”下拉列表中，选择右服务器的 IP 地址（或 `%default`）。
   e. 如果系统充当子网之间的网关，标记为“网关”（Gateway）；然后从“本地子网”下拉列表中选择网关后的子网。
   f. 在“证书”字段中，确保已选择你的右主机的证书文件。
   g. 验证从证书获取的主机 ID 显示在“标识”字段中；然后选择“下一步”（Next）。
   h. 在“远程地址”下拉列表中，输入左服务器的 IP 地址。
   i. 如果远程服务器将作为另一个子网的网关，标记为“网关”（Gateway）；然后从“远程子网”下拉列表中选择其子网。

## 第 11 章：使用 SLES 实现私有网络

- i. 选择“下一步”（Next）。
- m. 在“证书”（Certificate）下拉列表中选择您刚刚导入的证书。
- n. 验证“标识”（Identification）字段中已从证书中正确提取左侧主机的 ID。
- o. 选择“下一步”（Next）。
- p. 在“启动期间”（During Boot）下拉列表中，选择以下其中之一：
  * 启动连接（Initiate Connection）
  * 准备连接（Prepare Connection）
  * 忽略连接（Ignore Connection）
- q. 点击“确定”（OK）
- r. 点击“完成”（Finish）。

如果您是第一次执行此操作，我强烈建议使用 YaST 在两个主机上设置连接。完成后，仔细检查两个系统上的 `ipsec.conf` 文件，查看 YaST 是如何形成连接的。

此外，检查对 `ipsec.secrets` 文件所做的更改。您应该会看到末尾添加了一个条目，指定了私钥的位置及其口令，如图 11.15 所示。

## 图 11.15

`ipsec.secrets` 的更改。
