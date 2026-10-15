
10/5/2022 1:33:32 AM CORP\stepanie

## 列表 763 - 使用 Psloggedon 查看 CLIENT74 上的用户

似乎 `jeffadmin` 在 `CLIENT74` 上有一个打开的会话，输出揭示了一些有趣的信息。如果我们的列举是准确的，我们确实拥有 `CLIENT74` 上的管理员权限，我们应该能够登录那里并窃取 `jeffadmin` 的凭据！立即尝试这样做很有诱惑力，但最佳实践是

坚持下去并继续我们的列举。毕竟，我们的目标不是获得快速胜利，而是提供详尽的分析。

输出中另一个值得注意的有趣现象是 `Stephanie` 登录了资源共享。这是因为 `PsLoggedOn` 使用了 `NetSessionEnum` API，在这种情况下，它需要登录才能工作。这可能解释了为什么之前在使用 `PowerView` 时 `stephanie` 有过登录记录。

到此，我们对受影响用户的列举结束，包括对域内活动会话的列举。根据我们收集的信息，我们有一个非常有趣的攻击路径，如果继续进行，可能会引导我们通往域管理员。

在下一节中，我们将专注于另一种类型的用户继续列举，特别是服务账户（Service Accounts）。

### 21.3.3 通过服务主体名称 (SPN) 进行列举

到目前为止，我们已经获得了一些信息，并开始看到域内事物是如何连接的。为了结束对用户列举的讨论，我们将重点转向服务账户，¹1042，它们也可能是高权限组的成员。

应用程序必须在操作系统的上下文中执行。如果用户启动应用程序，则由用户账户定义上下文。然而，服务是由系统本身在服务账户上下启动的。

换句话说，隔离的应用程序可以使用一组预定义的服务账户，例如 `LocalSystem`，¹1043 `LocalService`，¹1044 和 `NetworkService`。¹1045

对于更复杂的应用程序，可以使用域用户账户来提供所需的上下文，同时保持对域内资源的访问权限。

当像 `Exchange`，¹1046、`MS SQL` 或 `Internet 信息服务 (IIS)` 等应用程序集成到 AD 时，一种称为服务主体名称 (SPN）¹1047 的唯一服务标识符会将服务与 Active Directory 中的特定服务账户关联。

> 托管服务账户（Managed Service Accounts）¹1048 随 Windows Server 2008 R2 引入，专为需要与 Active Directory 深度集的复杂应用程序设计。

- ¹1042 (Microsoft, 2022), https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/service-accounts-on-premises
- ¹1043 (Microsoft, 2021), https://learn.microsoft.com/en-us/windows/win32/services/localsystem-account
- ¹1044 (Microsoft, 2021), https://learn.microsoft.com/en-us/windows/win32/services/localservice-account
- ¹1045 (Microsoft, 2021), https://learn.microsoft.com/en-us/windows/win32/services/networkservice-account
- ¹1046 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Exchange
- ¹1047 (Microsoft, 2021), https://learn.microsoft.com/en-us/windows/win32/services/service-accounts
- ¹1048 (Microsoft, 2021), https://learn.microsoft.com/en-us/windows/win32/services/service-accounts

当像 `Exchange`、`MS SQL` 或 `Internet 信息服务 (IIS)` 等大型应用程序集成到 AD 时，一种称为服务主体名称 (SPN) 的唯一服务标识符会将服务与 Active Directory 中的特定服务账户关联。

### 21.3.4 列举对象权限

在本节中，我们将列举与 Active Directory 对象关联的权限。虽然这些权限的技术细节非常复杂且超出了模块的范围，但在开始列举之前，讨论基本原理是重要的。

简而言之，AD 可能应用了一组包含多个访问控制项（ACE）¹1049。这些 ACE 构成了访问控制列表（ACL）¹1050。每个 ACE 定义了允许还是拒绝对特定对象的访问。

作为一个非常基本的例子，假设一个域用户尝试访问域共享（这也是一个对象）。目标对象（在这种情况下）将通过一个验证检查

- ¹1049 (Microsoft, 2021), https://learn.microsoft.com/en-us/windows/win32/secauthz/access-control-entries
- ¹1050 (Microsoft, 2020), https://learn.microsoft.com/en-us/windows/win32/secauthz/access-control-lists

# OffSec

使用 Kali Linux 进行渗透测试

基于 ACL（访问控制列表）来确定用户是否具有共享的权限。此 ACL 验证涉及两个主要步骤。在尝试共享时，用户将使用访问令牌（access token），该令牌由身份和权限组成。目标将根据权限列表（ACL）对令牌令牌。如果 ACL 允许用户访问共享，则授予访问权限。我们的请求被拒绝了。

AD 包含了丰富的权限类型，可用于配置 ACE（访问控制实体）¹。然而，从攻击者的角度来看，我们主要对少数权限类型感兴趣。以下是最感兴趣的权限列表以及它们提供的权限描述：

```
- GenericAll: 对对象具有完全权限
- GenericWrite: 编辑对象上的某些属性
- WriteOwner: 更改对象的所有者
- WriteDACL: 编辑应用于对象的 ACEs
- AllExtendedRights: 更改密码、重置密码等
- ForceChangePassword: 对象的密码更改
- Self (自成员身份): 将我们添加到某个组中
```

列表 767 - AD 权限类型

我们使用 `PowerView` 中的 `Get-ObjectACL`² 来列举 ACEs。首先，让我们枚举我们自己的用户，以确定哪些 ACEs 应用于它。我们可以通过过滤 `-identity` 来实现。

```powershell
PS C:\Tools>Get-ObjectACL -identity stephanie
```

| ObjectDN | CN=Users,DC=corp,DC=com |
| ObjectSID | S-1-5-21-1987370200-658909505-178184369-1104 |
| ActiveRights | ReadProperty |
| ObjectFlags | ObjectPresent |
| ObjectType | 4c164a28-20c0-11d0-a768-00a006e529 |
| InheritedObjectType | 00000000-0000-0000-0000-000000000000 |
| BinaryLength | 56 |
| AceQualifier | AccessAllowed |
| IsCallback | False |
| OpaLength | 0 |
| AccessMask | 16 |
| SecurityIdentifier | S-1-5-21-1987370200-658909505-17814369-553 |
| AceType | AccessAllowed |
| AceFlags | None |
| IsInherited | False |
| InheritanceFlags | None |
| AuditFlags | None |

列表 768 - 指定用户运行 Get-ObjectACL

输出量可能让人应接 overwhelming，因为它列举了每个授予或拒绝 `stephanie` 某些权限的 ACE。这里有很多用的属性，我们主要对列表 768 截断输出中显示的那些感兴趣。¹(Microsoft), https://learn.microsoft.com/en-us/dotnet/api/system.directoryservices.activedirectories?view=framework-4.2 ²(Microsoft, 2022), https://learn.microsoft.com/en-us/windows/32/secauth/access-rights-and-access-masks
