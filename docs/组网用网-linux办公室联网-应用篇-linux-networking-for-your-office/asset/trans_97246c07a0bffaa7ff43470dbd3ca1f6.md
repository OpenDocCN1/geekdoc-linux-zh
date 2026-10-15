

## 表 11.1 继续

| Variable | Description |
|---|---|
| %N | 你的 NIS 主目录服务器的名称，如 auto.map 文件中指定的那样。如果 Samba 未编译 automount 支持，则与 %L 相同。 |
| %p | 服务主目录的路径，从 auto.map 文件中获取。 |
| %P | 当前服务的根目录。 |
| %R | 在连接设置阶段的协议协商期间选择的协议。可能是 CORE、COREPLUS、LANMAN1、LANMAN2 或 NT1。 |
| %S | 当前服务的名称。 |
| %T | 当前日期和时间。 |
| %u | 当前服务的用户名。 |
| %U | 客户端请求的用户名。这可能与 %u 不相同。 |
| %V | Samba 版本号。 |

## 设置全局参数

全局参数控制 Samba 整体的行为——它如何向网络宣告自身、对哪些计算机做出响应等等。正确配置系统的全局参数至关重要，否则你可能甚至无法在 Windows 网络邻居中看到它。

## 标识设置

NetBIOS 即使在 NetBIOS 运行在 TCP/IP 之上时，也不会使用 TCP/IP 机器名来标识计算机。相反，NetBIOS 使用自己的机器名和工作组名。一般来说，你可能希望将服务器设置为使用你的 TCP/IP 机器名作为 NetBIOS 机器名，只是为了让生活不那么复杂。你的工作组名可能与计算机的任何其他网络名称完全无关。但是，如果你在大型组织中设置内部网，你可能有奢侈地将工作组名设置为与你的完全限定域名（FQDN）的一部分相匹配。例如，如果域 erplab.pangaea.edu 中的计算机网络构成一个单一的 NetBIOS 工作组，你可以将工作组名设置为 ERPLAB。

### Note

NetBIOS 工作组通常必须驻留在单个以太网网络上，从而限制了工作组的物理范围。你可以使用桥接来扩展此范围。不过，使用 NetBIOS over TCP/IP，你可以通过指定 IP 地址连接到远程工作组。例如，我曾使用 PPP 拨号连接 ISP 来连接到位于 ISP 网络以外的数英里外的 Samba 服务器。

要设置机器名，你使用 netbios name 选项，要设置工作组名，你使用 workgroup 选项。惯例是以大写形式指定这些值。你还可以设置 server string 选项，它可以提供对系统的更具描述性的标识。netbios name 选项默认为你的计算机的主机名，而 workgroup 名称的默认值取决于编译选项。因此，在许多情况下你可以省略 netbios name 规范，但由于你的工作组名在本地有所不同，你应该确保设置它。

以下是三个选项全部使用的示例：

```
netbios name = SPEAKER
workgroup = RINGWORLD
server string = Workgroup server computer running Samba %v
```

请注意，server string 规范包含一个变量（%v）来宣布 Samba 版本号。实际上，你可能不想透露此信息，因为如果你运行的版本存在安全漏洞，宣传版本号可能是不明智的。

## 身份验证选项

你可以使用 security 选项配置 Samba 使用四种不同的身份验证方法之一：

- share—Samba 要求对每个共享资源进行单独身份验证。在 Windows 中，仅需密码即可访问此类型，但 Linux 中 Samba 也需要用户名。某些客户端会发送用户名，Samba 会尝试使用该用户名。在此尝试失败的情况下，你可以指定一组用于检查密码的用户，如 users = larry, moe, curly。一般来说，共享级安全性在 Linux 中很笨拙，因此除非你有令人信服的理由使用它，否则我建议不要使用它。
- user—Samba 要求客户端同时发送用户名和密码。并且如果获批准，用户可以在 Linux 权限设定的限制范围内访问服务器上的所有共享。

