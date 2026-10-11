
## Kerberoasting 的关键组件

要理解 Kerberoasting 攻击，我们需要理解 Kerberos 本身的工作原理。让我们看看涉及 Kerberos 应用于 Kerberoasting 时的一些重要组件：

-   **票据授予票据（TGT）** - 当用户登录 Windows 系统时，他们从密钥分发中心（KDC，Active Directory 的一部分）获得一个票据授予票据（TGT）。
-   **服务票据** - TGT 可用于请求特定资源（如网络中的服务器或服务）的服务票据。
-   **服务账户** - 服务账户常成为攻击目标，因为它们是与在后台运行的服务关联的账户。它们通常拥有特权访问权限，许多时候是域管理员组的成员。它们的密码很少更改，或者根本不更改。此外，很多时候它们的密码长度仅满足域的最小密码长度要求。这使得它们成为攻击者的主要目标。

Kerberos 在认证过程中签发这些票据。TGT 在初始认证过程中获取，可用于请求网络中特定服务的服务票据。当签发服务票据时，它使用服务账户的秘密密钥进行加密。这是一种加密形式，包含关于票据的信息，包括时间戳和其他详细信息。

在 Kerberoasting 攻击中，攻击者试图捕获特定服务的服务票据，特别是那些与服务账户关联的服务。这些服务票据包含加密的信息，攻击者可以尝试在离线状态下进行破解。一旦破解成功，加密的服务票据将揭示该账户的明文密码。

## 攻击 Kerberos

执行 Kerberoasting 攻击涉及几个步骤，攻击者通常使用多种技术来实现其目标。为了避免被检测，攻击者可能以隐蔽的方式执行攻击，限制服务票据请求的数量，并确保他们的操作不会触发安全警报。

![](img/4a03f08556c51a14a3b88fe549a54ca8_23_0.png)

以下是与 Kerberoasting 攻击相关的一些常见技术：

1.  **识别服务账户**
    攻击者在 Active Directory 环境中识别服务账户。服务账户通常与后台服务相关联，由于其通常具有较长且复杂的密码，因此是诱人的目标。

2.  **枚举服务主体名称（SPN）**
    服务主体名称（SPN）与服务账户相关联。攻击者可能会使用诸如 BloodHound 或 PowerView 等工具来枚举和识别具有关联 SPN 的账户。

3.  **请求服务票据**
    攻击者为已识别的服务账户请求服务票据。他们通常使用在初始认证期间获取的票据授予票据（TGT）来请求特定服务的服务票据。

4.  **捕获服务票据**
    一旦获得服务票据，攻击者就会捕获票据授予票据（TGT）以及与目标服务账户关联的加密服务票据。

5.  **破解票据**
    攻击者使用离线技术，如暴力破解或字典攻击，试图解密服务票据。目标是揭示与服务账户关联的明文密码。这通常使用诸如 Hashcat 或 John the Ripper 等工具来完成。

6.  **票据传递（Pass-the-Ticket）攻击**
    在某些情况下，攻击者可能会使用票据传递攻击来访问资源，而无需破解票据。这涉及呈现捕获的服务票据以获得未授权的访问权限。

这是标准的攻击流程，但不是唯一的流程。现在的许多工具都自动化了这个过程的大部分。使用 Mimikatz 等工具从内存中提取 Kerberos 票据也是可能的。Mimikatz 是从内存中提取各种密码和有用信息（包括导出 NTLM 哈希值）的常用工具。

## Kerberos 攻击工具

话虽如此，了解攻击者可能使用的工具对于防御者意识潜在威胁并采取适当措施至关重要。一些与 Kerberoasting 攻击常见的工具有：

-   **PowerShell 脚本**
    PowerShell 是内置于 Windows 中的强大脚本语言。有各种 PowerShell 脚本，如 PowerView 和 Invoke-Kerberoast，可用于识别服务账户、请求服务票据以及执行 Kerberoasting 过程中的其他步骤。许多这些脚本作为模块包含在命令和控制（C2）框架中。有关 C2 及其攻击模块的更多信息，请参见我的书《使用 Kali Linux 进行高级安全测试》。

-   **Rubeus**
    Rubeus 是一个强大的后利用工具，攻击者经常将其用于 Kerberoasting 攻击。它可以用于请求 TGT、请求服务票据以及执行票据相关攻击。它包含票据提取和离线破解的功能。

-   **Mimikatz**
    Mimikatz 是一个著名的后利用工具，可用于提取 Kerberos 票据并执行票据传递攻击。它还可以用于提取 NTLM 和其他安全哈希值。

-   **Kerberoast 工具包**
    Kerberoast 是一组用于攻击 Kerberos 的工具。它包括用于提取服务主体名称（SPN）、请求票据以及破解票据的工具（tgsrepcrack）。

-   **破解工具（Hashcat、John the Ripper）**
    这些是通用的密码破解工具。虽然它们不是专门针对 Kerberoasting 的，但可以用于尝试离线破解 Kerberos 票据。

-   **BloodHound**
    BloodHound 是一个用于 Active Directory 分析的工具。虽然它不是专门的 Kerberoasting 工具，但它可以用于识别服务账户及其关联的特权，可能有助于攻击者规划 Kerberoasting 攻击。

![](img/4a03f08556c51a14a3b88fe549a54ca8_26_0.png)

BloodHound 可以检测并显示 AD 域中可执行 Kerberoasting 的账户

攻击者使用这些工具试图破坏目标的安全并获取用户凭证。安全专业人员也可以使用这些工具进行道德黑客行为或渗透测试，以识别和解决安全漏洞。希望这个快速概述能有助于阐明 Kerberos 和 Kerberoasting 的基础知识。

你做到了！花几分钟时间深呼吸一下。正如我之前所说，如果你不理解票据创建过程的每个部分，也没关系。目前，只需知道 Windows 创建并使用加密数据用于认证过程——包括票据（Kerberos）和密码哈希（NTLM）。接下来，我们将查看黑客用于获取这些秘密以进行破解的一些工具。

废话不多说，让我们开始动手实践！

## RUBEUS

**工具 GitHub：** [https://github.com/GhostPack/Rubeus](https://github.com/GhostPack/Rubeus)

**工具 Wiki：**
[https://specterops.gitbook.io/ghostpack/rubeus/introduction](https://specterops.gitbook.io/ghostpack/rubeus/introduction)

Rubeus 是一个基于 C# 的用于交互和攻击 Kerberos 的工具。该工具最初基于 Benjamin Delpy（Mimikatz 的创建者）的 Kekeo 开发，但随后演变成其独立的创造。Rubeus 可以通过许多不同的方式攻击 Kerberos，我们只简要介绍一种。我强烈建议读者查阅该工具的 Wiki，以获取广泛的文档和使用信息。

你会注意到 Rubeus 的 GitHub 页面上没有可执行文件下载。你需要自己编译该工具。显然，就其当前形式而言，它会被大多数（如果不是所有）防病毒系统检测到并立即阻止。经验丰富的红队攻击者需要在编译前修改部分代码以避开反病毒检测。

### Kerberoasting 快速演练

1.  **获取初始访问权限**
    在使用 Rubeus 之前，攻击者需要获得系统或网络的初始访问权限。这可以通过多种方式实现，例如利用漏洞、使用钓鱼攻击或利用其他攻击向量。我在我的《使用 Kali Linux 进行基础和安全测试》书籍中详细涵盖了这些技术。

2.  **部署 Rubeus**

