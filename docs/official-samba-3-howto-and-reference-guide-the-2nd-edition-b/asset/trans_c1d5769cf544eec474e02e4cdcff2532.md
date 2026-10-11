

不一致的安全数据。必须牢记的是，Windows 工作站会定期更新（更改）机器信任账户的密码——管理员通常意识不到这种情况的发生，也不知道它何时发生。

使用 LDAP 同时处理 POSIX（UNIX 用户和组）账户以及 SambaSAMAccount 数据，自动确保了所有账户变更信息都会写入共享目录。这消除了同步账户信息所需的任何特殊操作，因为 LDAP 本身就能满足这一要求。

- netlogin 共享目录必须从 PDC 复制到 BDC。这可以在登录脚本每次更改时手动完成，也可以自动执行，例如使用 *cron* 作业利用 *rsync* 等工具来复制该共享目录的目录结构。使用 *rsync* 复制 netlogin 数据对网络安全性并非至关重要，鉴于管理员会有意识地将对 netlogin 共享目录的所有更改作为整体移动的一部分进行处理，因此这一过程可以手动管理。

## 5.3.1 配置示例

最后，BDC 必须具备被工作站找到的能力。这可以通过配置 Samba *smb.conf* 文件的 *[global]* 部分来实现，如示例 5.3.1 所示。

> 示例 5.3.1 作为 BDC 的最小化配置
>
> ```
> workgroup = MIDEARTH  
> passdb backend = ldapsam:ldap://slave-ldap.quenya.org  
> domain master = no  
> domain logons = yes  
> ldap suffix = dc=abmas,dc=biz  
> ldap user suffix = ou=Users  
> ldap group suffix = ou=Groups  
> ldap machine suffix = ou=Computers  
> ldap idmap suffix = ou=IDmap  
> ldap admin dn = cn=sambaadmin,dc=quenya,dc=org  
> ldap backend = ldap://master-ldap.quenya.org  
> ldap uid = 10000-20000  
> ldap gid = 10000-20000
> ```

使用 OpenLDAP 和 Samba 的完整文档化且可用的网络配置示例，可在书籍³《Samba-3 by Example》中获得，该书可从当地和在线书店购买。

此配置导致 BDC 仅在 WINS 服务器上注册名称 MIDEARTH\<1C>。这不是一个问题，因为名称 MIDEARTH\<1C> 是一个 NetBIOS 组名称，旨在由多台机器注册。参数 *domain master = no* 强制 BDC 不注册 MIDEARTH\<1B>，而 MIDEARTH\<1B> 是保留给 PDC 的唯一 NetBIOS 名称。

³ <http://www.samba.org/samba/docs/Samba-3-ByExample>

**idmap backend** 将引导 **winbindd** 实用程序使用 LDAP 数据库，以在共享存储库中将 Windows SID 映射为 UNIX 账户的 UID 和 GID。然而，BDC 将依赖通过 NSS 和 nss_ldap 实用程序在本地解析 UID 和 GID。

# 注意

![](img/86d74c6cc862465e3a42e6dc3c90935a_128_0.png)

Samba-3 引入了新的 ID 映射功能。该功能的一个特点是，它允许在处理与 NT 域用户和组 SID 相关的用户和组 ID 时提供更大的灵活性。其中一个新功能明确规定，确保 UNIX/Linux 的 UID 和 GID 值在 PDC、所有 BDC 以及所有域成员服务器上保持一致。控制此功能的参数称为 *idmap backend*。有关其行为的更多信息，请参阅 smb.conf 的手册页。

仅在 BDC 上使用 *idmap backend* = ldapsam:ldap://master.quenya.org 选项，只有在 PDC 上使用 ldapsam 时才有意义。基于 LDAP 的 idmap 后端的另一个目的是允许域成员（没有自己的 passdb）后端使用 winbindd 将 Windows 网络用户和组解析为通用的 UID/GID。换句话说，该选项通常旨在用于 BDC 和域成员服务器。

## 5.4 常见错误

域控制是 Samba 的一个新领域，但现在有许多可供参考的示例。随着新信息的发布，它们将在后续的 Samba 版本或 Samba 网站上找到⁴；特别请参考 Samba 发行版压缩包中的 **WHATSNEXT.txt**。书籍《Samba-3 By Example》详细记录了经过充分测试和验证的配置示例。您可以在 Samba 网站上获取该书的副本⁵。

⁴ <http://samba.org>  
⁵ <http://www.samba.org/samba/docs/Samba3-ByExample.pdf>

### 5.4.1 机器账户不断过期

当 passdb (SAM) 文件从中心服务器复制，但本地 BDC 正在充当 PDC 时，会出现此问题。这导致本地机器信任账户密码更新应用到本地 SAM。这些更新不会复制回中心服务器。当从 PDC 接收 SAM 时，较新的机器账户密码将被覆盖。结果是，域成员机器在启动时会发现其密码与数据库中的当前密码不匹配，由于启动安全检查将失败，该机器将不允许登录尝试继续，并报告账户过期错误。

解决方案是使用更健壮的 passwd 后端，例如 ldapsam 后端，为每个 BDC 设置从属 LDAP 服务器，为 PDC 设置主 LDAP 服务器。

### 5.4.2 Samba 可以作为 NT4 PDC 的备份域控制器吗？

不可以。原生 NT4 SAM 复制协议尚未完全实现。

我可以通过 Samba 获得 BDC 的好处吗？可以，但仅针对 Samba PDC。实施 BDC 的主要原因是可用性。如果 PDC 是 Samba 机器，可以设置第二台 Samba 机器在 PDC 停机时处理登录请求。

### 5.4.3 如何复制 smbpasswd 文件？

smbpasswd 文件的复制非常敏感。每当对 SAM 进行更改时都必须执行。每个用户的密码更改都在 smbpasswd 文件中完成，并且必须复制到 BDC。因此，非常频繁地复制 smbpasswd 文件是必要的。

由于 smbpasswd 文件包含明文密码等价物，因此不得以未加密的形式通过网络传输。从 PDC 到 BDC 设置 smbpasswd 复制的最佳方法是使用 rsync 实用程序。rsync 可以使用 ssh 作为传输协议。ssh 本身可以设置得仅接受 rsync 传输，而不需要用户输入密码。

如前所述多次，此方法是有缺陷和错误的。机器信任账户会失去同步，导致域损坏。不推荐此方法。请尝试使用 LDAP 代替。

### 5.4.4 我可以全部使用 LDAP 来完成吗？

简单的回答是肯定的。Samba 的 pdb_ldap 代码支持绑定到副本 LDAP 服务器，并且如果需要修改数据库，也会跟随引用并重新绑定到主服务器。（通常 BDC 是只读的，因此这种情况不会经常发生）。

## 6. 域成员资格

域成员资格是一个至关重要的主题。Samba 必须能够作为成员服务器参与 Microsoft 域安全环境，并且 Samba 必须能够提供商域机器成员信任账户；否则，它无法为许多用户提供可行的选择。

本章涵盖有关域成员资格的背景信息、Samba 配置以及 MS Windows 客户端加入域的程序。为什么这是必要的？因为在当前的 MS Windows 网络世界中，特别是 UNIX/Linux 网络和管理领域，存在相当程度的错误信息、错误理解和知识匮乏。希望本章能填补这些空白。

### 6.1 特性和优势

希望参与域安全的 MS Windows 工作站和服务器必须成为域成员。参与域安全通常被称为 *单点登录*，或简称 SSO。本章描述了使工作站（或其他服务器——无论是 MS Windows NT4/200x 服务器）或 Samba 服务器成为 MS Windows 域安全环境成员所需遵循的过程。

Samba-3 可以作为原生成员服务器加入 MS Windows NT4 风格的域，作为原生域服务器加入 MS Windows Active Directory 域，或加入 Samba 域控制网络。域成员资格有许多优势：

- MS Windows 工作站用户可享受 SSO 带来的好处。
- 域用户访问权限和文件所有权/访问控制可以从单一的域安全账户管理器（SAM）数据库进行设置（既适用于域成员服务器，也适用于作为域成员的 MS Windows 工作站）。
- 只有作为域成员的 MS Windows NT1/200x/XP Professional 工作站才能使用网络登录功能。
- 通过策略文件（`NTConfig.POL`）和桌面配置文件的使用，可以更好地控制域成员工作站。

