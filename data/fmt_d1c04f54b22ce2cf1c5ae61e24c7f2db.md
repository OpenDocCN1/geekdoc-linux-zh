
```
53-a965c6e-e227-4f9b-a76d-c3b5c208d4e61
e8414623-b3c9-44bc-a135-0356e8b3341f
f711b976-7e61-43eda-08114556e08a134b
e08d6e0b1-2e0c-4771-9455-39f4159940f
  key = 00000000-0000-0000-0000-000000000000
  secret = 0777777-777-4478-88---7777110011
nnnn 77777777-7777-7777-7777-777777777777
  ike = 11111111-1111-1111-1111-111111111111
  enc = aes256-cbc
  auth = sha256
  modp = 2048

  key = 88888888-8888-8888-8888-888888888888
  secret = 2222222-222-3322-99--222222000000

  conn =-v1-with-sha256
  key = c1c2c3c4-c5c6-c7c8-c9c0-c1c2c3c4c5c6
  secret = d1e2f3a4-b5c6-d7e8-f9a0-b1c2d3e4f5a6

  conn =-v1-with-sha256
  key = e1f2a3b4-c5d6-e7f8-a9b0-c1d2e3f4a5b6
  secret = 0a1b2c3d-4e5f-6a7b-8c9d-0e1f2a3b4c5d

  conn =-v1-with-sha256
  key = 9a8b7c6d-5e4f-3a2b-1c0d-9e8f7a6b5c4d
  secret = 5a6b7c8d-9e0f-1a2b-3c4d-5a6b7c8d9e0f

  conn =-v1-with-sha256
  key = 3a4b5c6d-7e8f-9a0b-1c2d-3a4b5c6d7e8f
  secret = 1a2b3c4d-5e6f-7a8b-9c0d-1a2b3c4d5e6f
```

- 不要更改 "that" 的标识：

  `rsa /etc/ipsec.secrets;key="key123"`

  `secrets expires = 12-20-28 (UTC)`

为了安全起见，您应该保持此文件的安全。

让我们在实验 11.1 中练习在两个主机之间建立 VPN 连接。

## 实验 11.1：使用 YaST 创建 VPN

在本次实验中，您将使用 YaST 在两个主机之间创建 VPN 连接。要完成此项练习，您需要您的 SLES 9 服务器以及您的 NLD 系统。我们将使用来自 SLES 9 系统的 ipsec 模块对 NLD 中的 YaST 进行调优。请完成以下操作：

- 1. 通过完成以下步骤在 NLD 系统上配置 YaST ipsec 模块：

  a. 启动您的 NLD 系统并身份验证。

  b. 将您的 SLES 9 CD 2 插入 NLD 系统的光驱驱动器。

  c. 切换到 `/media/cdrom/noarch` 目录。

  d. 将 `yast2-ipsec-2.9.noarch.rpm` 文件拷贝到工作站的 `/tmp` 目录。

  e. 移除 SLES 9 CD。

  f. 选择“系统”（System）、“管理员设置”（Administrator Settings）。

  g. 在提示时输入您的密码。

  h. 选择“软件”（Software）、“安装源”（Source of Installation）。

  i. 在软件源屏幕上，选择“添加”（Add）、“本地目录”（Local Directory）。

  j. 在目录路径输入 `/tmp`；然后选择。

  k. 在提示产品信息时选择“继续”（Continue）。

  l. 选择“完成”（Finish）。

  m. 选择“安装软件”（Install and Software）。

  n. 在字段中输入 `ipsec`；然后选择。

  o. 勾选 FreeSwan、`ipsec-tools` 和 `yast2-ipsec` 包，然后选择“接受”（Accept）。

  p. 在“自动更改”（Automatic Changes）屏幕上选择“继续”。

  q. 按提示进行安装。

  r. 完成后，关闭 YaST。

- 2. 通过以下步骤准备您的 SLES 9 服务器：

  a. 启动 SLES 9 服务器并使用 `tux` 身份验证。

  b. 打开 shell 符并使用 `su` 切换到 root，密码为 `tux`。

  c. 在 shell 符输入 `service stop`。

  d. 在 shell 符输入 `firewall stop -t nat`。

  e. 在 shell 符输入 `iptables -F`。

  f. 使用 `iptables -L` 验证表均为空。

  g. 输入 `echo 1 > /proc/sys/ipv4/ip_forward` 启用转发。

- 3. 通过以下步骤在 SLES 9 服务器上生成证书和密钥：

  a. 在 shell 符切换到 `/etc` 目录。

  b. 在 shell 符输入 `mkdir ca-left`。

  c. 切换到 `/etc/ca-left` 目录。

  d. 创建以下目录：

    - `certs`

    - `newcerts`

    - `private`

    - `crl`

  e. 在 shell 符输入 `vi /etc/ssl/opens.cnf`。

  f. 滚动到 `HOME` 指令并将其设置为 `/etc/ca-left`。

  g. 滚动到 `| CA_default |` 下的 `dir` 指令。

  h. 将 `dir` 的值设置为 `/etc/ca-left`。

  i. 按 Esc 键，然后输入 `:exit`。

  j. 验证当前目录为 `/etc/ca-left`；然后输入 `openssl req -newkey rsa:2048 -x509 -days 365 -keyout private/cake.pem -out cacert.pem` 创建自签名根证书。

  k. 在提示时，为私钥输入口令 `test`。

  l. 在提示时，输入您的组织信息。

  m. 在提示通用名称（Common Name）时，输入服务器的 DNS 名称或 IP 地址。

  n. 在提示电子邮件时，输入 `tux@cle9.com`。

  o. 在 shell 符输入 `touch index.txt ; echo 1 > serial`。

  p. 在 shell 符输入 `openssl req new -keyout private/ca_prv_key.pem -out certs/ca_req.pem -days 365` 创建证书请求。

  q. 在提示时，输入口令 `test`。

  r. 在提示时，输入您的组织信息。

  s. 在提示通用名称时，输入服务器的 DNS 名称或 IP 地址。

  t. 在提示电子邮件时，输入 `tux@cle9.com`。

  u. 在提示时，为证书输入挑战密码（challenge password）`test`。

  v. 在提示可选公司名称时，按回车。

  w. 输入 `openssl ca -policy policy_anything -notext -out certs/newcert.pem -infiles certs/ca_req.pem` 证书请求。

  x. 在提示时，输入口令 `test`。

  y. 在提示签名证书时，输入 `y`。

  z. 在提示提交时，输入 `y`。

- 4. 将磁盘插入 SLES 9 服务器的软驱驱动器并挂载。

- 5. 将 `/etc/ca-left` 目录拷贝到软盘；然后挂载磁盘。

- 6. 通过以下步骤在您的 NLD 工作站上生成证书和密钥：

  a. 打开终端会话并使用 `su -` 切换到 root。

  b. 切换到 `/etc` 目录。

  c. 在 shell 符输入 `mkdir ca-right`。

  d. 切换到 `ca-right` 目录。

  e. 创建以下目录：

    - `certs`

    - `newcerts`

    - `private`

    - `crl`

  f. 在 shell 符输入 `vi /etc/ssl/openssl.cnf`。

  g. 滚动到 `HOME` 指令并将其设置为 `/etc/ca-right`。

  h. 滚动到 `| CA_default |` 下的 `dir` 指令。

  i. 将 `dir` 的值设置为 `/etc/ca-right`。

  j. 按 Esc 键，然后输入 `:exit`。

  k. 验证当前目录为 `/etc/ca-right`，然后输入 `openssl req -newkey rsa:2048 -x509 -days 365 -keyout private/cakey.pem -out cacert.pem` 创建自签名根证书。

  l. 在提示时，为私钥输入口令 `test`。

  m. 在提示时，输入您的组织信息。

  n. 在提示通用名称时，输入 NLD 工作站的 DNS 名称或 IP 地址。

  o. 在提示电子邮件时，输入 `tux@cle9.com`。

  p. 在 shell 符输入 `openssl req new -keyout private/ca_prv_key.pem -out certs/ca_req.pem -days 365` 创建证书请求。

  q. 在提示时，输入口令 `test`。

  r. 在提示时，输入您的组织信息。

  s. 在提示通用名称时，输入 NLD 工作站的 DNS 名称或 IP 地址。

  t. 在提示电子邮件时，输入 `tux@cle9.com`。

  u. 在提示时，为证书输入挑战密码 `test`。

  v. 在提示可选公司名称时，按回车。

  w. 输入 `openssl ca -policy policy_android -notext -out certs/newcert.pem -infiles certs/ca_req.pem` 证书请求。

  x. 在提示时，输入口令 `test`。

  y. 在提示签名证书时，输入 `y`。

  z. 在提示提交时，输入 `y`。

- 7. 将您的磁盘插入 NLD 工作站的软盘驱动器并挂载它。

- 8. 将 `/etc/ca-right` 目录拷贝到软磁盘；然后卸载磁盘。

- 9. 通过完成以下步骤，在您的 SLES 9 系统上配置隧道的左端：

  a. 将您的磁盘插入 SLES 9 服务器的软盘驱动器。

  b. 在 shell 提示符下输入 `mount -t vfat /dev/fd0@ /media/floppy` 挂载软盘。

  c. 在您的 SLES 9 服务器上启动 YaST。

  d. 当提示时，提供 root 密码 `tuX123`。

  e. 选择安全与用户（Security and Users）、VPN。

  f. 如果提示需要安装 FreeSAWAN，选择继续（Continue）；然后按照提示插入光盘。

  f. 选择启用 VPN 服务（Enable VPN Services）。

- 10. 通过完成以下步骤，配置 VPN 证书：

  a. 当提示导入证书时，选择是（Yes）。

  b. 在“当前视图”（Current View）下拉列表中，选择 CA 证书（CA Certificates）。

  c. 选择导入（Import）；然后浏览并选择 `/etc/ca-left/cacert.pem`。

  d. 在“当前视图”（Current View）下拉列表中，选择证书（Certificates）。

  e. 选择导入（Import）；然后浏览并选择 `/etc/ca-left/certs/newcert.pem`。

  f. 在“当前视图”（Current View）下拉列表中，选择密钥（Keys）。

  g. 选择导入（Import）；然后浏览并选择 `/etc/ca-left/private/cakey.pem`。

  h. 当提示 RSA 密码时，输入 `test`；然后选择下一步（Next）。

- 11. 通过完成以下步骤配置连接定义：

  a. 当提示定义连接时，选择是（Yes）。

  b. 在“选择连接类型”（Choose the Connection Type）下，选择自定义（Custom）；然后选择下一步（Next）。

## 第 11 章：使用 SLES 9 实施虚拟专用网络

c. 当提示时，输入连接名称 `host2host`。

d. 在“本地 IP 地址”（Local IP Address）下拉列表中，选择您的服务器的 IP 地址。

e. 勾选“作为网关”（Act as Gateway）；然后在“本地子网”（Local Subnet）下拉列表中选择 `10.0.0.0/8` 子网。

f. 在“证书”（Certificate）字段中，确保已选择您的左主机的证书文件。

g. 验证证书文件中的主机 ID 是否显示在“标识”（Identification）字段中；然后选择下一步（Next）。

h. 在“远程地址”（Remote Address）下拉列表中，输入您的 NLD 工作站的 IP 地址。

i. 在“证书”（Certificate）字段中，选择导入（Import）、导入（Import）。

j. 浏览并选择右主机的证书文件 `/media/floppy/ca-right/certs/newcert.pem`。

k. 选择下一步（Next）。

l. 在“证书”（Certificate）下拉列表中，选择您刚刚导入的证书。通常它命名为 `cert_02.pem`。

m. 验证“标识”（Identification）字段是否已从证书中正确提取了右主机的 ID；然后选择下一步（Next）。

n. 在“启动期间”（During Boot）下拉列表中，选择“准备连接”（Prepare Connection）。

o. 选择确定（OK），然后选择完成（Finish）。

此时，VPN 隧道的左端已经建立。现在，您需要在您的 NLD 工作站上配置隧道的右端。

1. 通过完成以下步骤，在您的 NLD 工作站上配置 VPN：

a. 在您的 NLD 工作站上启动 YAST

b. 当提示时，提供您的 root 密码。

c. 选择安全与用户（Security and Users）、VPN

d. 选择启用 VPN 服务（Enable VPN Services）。

e. 当提示导入证书时，选择是（Yes）。

2. 通过完成以下步骤配置您的 VPN 证书：

a. 在“当前视图”（Current View）下拉列表中，选择 CA 证书（CA Certificates）

b. 选择导入（Import）；然后浏览并选择 `/etc/ca-right/cacert.pem`。

c. 在“当前视图”（Current View）下拉列表中，选择证书（Certificates）。

d. 选择导入（Import）；然后浏览选择 `/etc/ca-right/certs/newcert.pem`

e. 在“当前视图”（Current View）下拉列表中，选择密钥（Keys）。

f. 选择导入（Import）；然后浏览选择 `/etc/ca-right/private/cakey.pem`

g. 当提示您的 RSA 密钥密码时，输入 `test`

h. 选择下一步（Next）。

3. 通过完成以下步骤配置您的 VPN 连接：

a. 当提示定义连接时，选择是（Yes）。

b. 选择自定义（Custom）；然后选择下一步（Next）。

c. 当提示输入连接名称时，输入 `host2host`；然后选择确定（OK）

d. 在“本地 IP 地址”（Local IP Address）下拉列表中，选择您的工作站的 IP 地址。

e. 在“证书”（Certificate）字段中，确保已选择您的右主机的证书文件。

f. 验证证书文件中的主机 ID 是否显示在“标识”（Identification）字段中；然后选择下一步（Next）。

g. 在“远程地址”（Remote Address）下拉列表中，输入您的 SLES 9 服务器的 IP 地址。

h. 勾选“作为网关”（Act as Gateway）；然后在“远程子网”（Remote Subnet）下拉列表中输入 `10.0.0.0/8`。

i. 在“证书”（Certificate）字段中，选择导入（Import）、导入（Import）。

j. 浏览选择 `/media/floppy/ca-left/newcert.pem`

k. 选择下一步（Next）。

l. 在“证书”（Certificate）下拉列表中，选择您刚刚导入的证书。通常它命名为 `cert_02.pem`。

m. 验证“标识”（Identification）字段是否已从证书中正确提取了右主机的 ID；然后选择下一步（Next）。

## 第 12 章：整合汇总：为你的服务器添加 OpenSLP 和 Tomcat

协议，例如互网络数据交换 (`IPX`) 协议或 `NetBIOS`——换句话说，就是让网络上的主机尽可能容易地找到它们需要使用的服务。

为了理解 SLP 在 IP 网络上是如何运作的，我们必须先回溯过去，看看以前是如何使用基于 IPX 的网络进行服务广告的。这是通过服务公告协议（SAP）实现的。

## 使用 SAP 广播服务
