
`/etc/passwd` 和 `/etc/group` 文件构成了 UNIX 中访问控制的基础。一般来说，对对象进行操作的权利由对象的所有权或与对象关联的组的成员资格来管理。较新的 UNIX 版本通过包含对访问控制列表（ACL）的支持来增强访问控制机制。ACL 允许比对象上允许的操作更精细的粒度，并允许最终用户设置和控制自定义组。缺点是，ACL 在环境之间不易映射，并且可能无法通过远程文件共享工作。

### 密码

UNIX 密码文件 `/etc/passwd` 是一个表，标识允许登录到系统的所有用户（示例 2.10）。每个用户帐户分配一个文本字符串帐户名称和一个唯一的数字标识符，称为 UID，该标识符唯一对应于单个计算机。与用户关联的另一个数字标识符是默认组标识符 GID。基本上，系统在管理访问控制时使用 UID 和 GID 标签。密码文件可能包含也可能不包含用户群体的加密密码。由于密码文件对所有用户可见，一些系统已将加密密码移至受限访问文件，称为 shadow 密码文件。这挫败了通过可见密码文件轻松使用密码破解程序的能力。当启用 shadow 密码时，占位符字符 `!` 会插入到 `/etc/passwd` 中的密码字段，表明关联的加密密码可以在 shadow 密码文件中找到。密码文件中的其它信息可能包括 gecos 字段中的个人姓名和地址数据、用户的 home 目录和默认 shell。密码文件中的每个字段由冒号分隔。

```
Account Name:UID:GID:<Gecos strings>:<Home Directory>:<Shell>
```

#### 示例 2.10 /etc/passwd

```
root::0:0:System Overseer::/bin/ksh
daemon::1:1::/etc:
bin::2:2::/bin
sys::3:3::/usr/sys:
adm::4:4::/usr/adm
uucp::5:5::/usr/lib/uucp:
stimpy::4084:30:Stimson Cat:/ul/stimpy:/bin/ksh
```

解析大型密码文件可能会导致命令响应时间显著延迟。为了提高响应时间，一些 UNIX 实现支持在索引的 dbm 数据库集中镜像 `/etc/passwd` 信息。`mkpasswd` 命令读取 `/etc/passwd` 并创建键控目录文件 `/etc/passwd.dir` 和数据文件 `/etc/passwd.pag`。密码 dbm 支持不是必需的，但作为选项提供 for sites with large user communities.

```
# mkpasswd /etc/passwd    Create new passwd dbm database.
```

### 组

组提供了一种粗略的机制，用于在用户之间共享信息。与 `/etc/passwd` 文件类似，`/etc/group` 文件是一个表格，用于标识系统上的所有组名、关联的 GID 以及组成组成员资格的账户名称的逗号分隔列表（示例 2.11）。UNIX 假定有限的组集来实现默认访问权限。系统管理员可以将用户添加到这些默认组中或创建新组以促进额外的协作。如果用户基数较小，这可以相对容易地完成。对于大量用户，管理 GID 集可能是一项繁重的工作。

#### 示例 2.11 /etc/group

```
system::!0:root,ops
daemon::!1:
bin::!2:root,bin
sys::!3:root,bin,sys
adm::!4:bin,adm,kenm,root
uucp::!5:uucp
mail::!6:
security::!7:root
cron::!8:root
staff::!10:root,ren,stimpy,daffy,huey,dwewy
user::!30:luge,acadmus,gwyneira,bungi
```

### 网络信息服务

网络信息服务（NIS）是一种管理工具，可用于在机器之间分发通用的系统配置信息。NIS 和 NIS+ 过去通常被称为“黄页（YP）”。对于负责维护实验室或分布式网络中大量机器的系统管理员来说，NIS 是一大福音。参与机器的集合称为 NIS 域。分发集中每个文件都被转换为 ndm 数据库格式并作为 NIS 映射文件存储在服务器上。NIS 映射的集合构成了 NIS 数据库，该数据库会定期分发到 NIS 域中的机器。

正如你可能猜到的那样，使用 NIS commonly 分发的两个文件是 `/etc/passwd` 和 `/etc/group` 文件。NIS 提供了一种便捷的方法，可在多台机器之间同步账户信息。在仅需在机器之间保持部分账户和组共用的情况下，NIS 允许将账户和组划分为本地和分布式类别（表 2.10）。本地信息是每个机器独有的。分布式信息是在主 NIS 服务器上管理的配置信息，并推送到参与机器以实现统一。本地数据会覆盖冲突的分布式数据。

#### 表 2.10 NIS 密码和组文件

| /etc/passwd | /etc/group |
|---|---|
| /etc/passwd.yp | /etc/group.yp |
| /etc/passwd.local | /etc/group.local |

### Kerberos

有许多适用于 UNIX 的身份验证系统可供使用，它们增强了基本密码和组架构的功能和安全性。其中一个系统是 *Kerberos* 身份验证，由 M.I.T. 开发，基于 *Trusted Third-Party* 身份验证模型。原始设计在 1988 年 USENIX 冬季会议上发表的一系列论文中进行了描述。Kerberos 是关于 UNIX 和 NT 共存的重要技术，因为它是 Windows 2000 中的网络身份验证系统。

Kerberos 假定网络中的所有内容都是不可信的，除了 Kerberos 身份验证服务器本身。Kerberos 身份验证服务器称为 *Key Distribution Center (KDC)*。KDC 在客户端和所需服务之间充当中介。客户端必须向 KDC 进行身份验证以获取票据，该票据授予访问分布式服务的权限（图 2.5）。该票据称为 *Ticket Granting Ticket (TGT)*。只需向 KDC 验证一次身份，而非每次访问的服务都需验证一次。各种 Kerberos 票据也仅在特定时间内有效。Kerberos 票据机制消除了通过网络以明文传输密码的需求。客户端和服务器密码由 KDC 知晓并存储。

![](img/7684008b1d7775727df27d44aed5b3f0_32_0.png)

1. 请求用户和服务的身份验证。
2. 返回 TS 会话密钥和标识符。
3. 使用密封的身份验证器请求票据。
4. 返回所请求服务的票据。
5. 使用身份验证器票据连接到服务。

图 2.5：Kerberos 票据交换

每当未经身份验证的客户端请求访问服务时，就会向 KDC 发送一条消息，其中包含客户端名称和 Kerberos 票据授予服务名称。KDC 查找名称并获取客户端和票据服务器的加密密钥。加密密钥仅为拥有方代理和 KDC 所知。然后 KDC 构造一条消息，其中包含客户端和票据服务器名称、地址以及随机会话密钥，并使用客户端的加密密钥对其进行加密。该消息称为票据并发送给客户端。客户端使用其加密密钥解密票据并在票据有效期内存储票据。会话密钥用于加密与 Kerberos 票据服务的票据通信以获取对其他服务和资源的访问权限。

当请求访问服务时，票据服务提供一个新的会话密钥以及使用 KDC 数据库中的服务加密密钥加密的票据。客户端使用新的会话密钥创建身份验证器票据以标识客户端，并将其与加密的服务票据一起发送给新服务。服务使用其加密密钥解密票据。服务票据包含会话密钥，然后用于解密身份验证器票据。现在客户端和服务彼此知晓，真正的任务可以开始了。

这看起来似乎是大量手势挥动以防止明文密码和身份验证信息在网络上传播。另一方面，在线路上窃听极其容易。所有这些协商都在幕后进行，因此对终端用户不可见。请记住，Kerberos 不会限制已经窃取了另一用户登录 ID 和密码的人的访问。

### 摘要

- UNIX 具有三层架构：内核、shell 和命令层。
- 执行任务和程序称为 *processes*，并由 *PID* 号码标识。
- 服务器进程称为 *daemons*。
- *Init*，PID 1，负责生成系统进程，这些进程在 `/etc/inittab` 文件中标识。
- TCP/IP 是一种具有四层的网络协议：*physical*、*internetwork*、*transport* 和 *application*。
- 网络上的每台计算机都由一个四字节的 IP 号码标识。
- 网络计算机组使用 *subnets* 进行划分，以隔离和管理流量并执行安全策略。
- 一种称为 *Domain Name Service (DNS)* 的分层动态网络名称服务将域名解析为 IP 号码。
- UNIX DNS 服务器称为 *named*。
- DNS 服务器地址在 `/etc/resolv.conf` 中标识。
- *inetd* 服务器在由 `/etc/inetd.conf` 定义的客户端请求时启动网络服务器。
