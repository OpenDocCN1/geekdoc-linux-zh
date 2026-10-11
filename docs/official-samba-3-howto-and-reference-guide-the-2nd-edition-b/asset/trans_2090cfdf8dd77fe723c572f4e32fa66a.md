
## 注意

当用户权限和特权被正确设置后，root 用户（或其任何同义词，UID=0）不再需要 Windows 网络账户。初始的用户权限和特权可以由任何属于“域管理员”组的账户分配。权限既可以分配给用户账户，也可以分配给组账户。

![](img/86d74c6cc862465e3a42e6dc3c90935a_259_0.png)

默认情况下，不分配任何特权和权限。这可以通过执行以下命令来验证：

```
root# net rpc rights list accounts -U root%\not24get
BUILTIN\Print Operators
No privileges assigned

BUILTIN\Account Operators
No privileges assigned

BUILTIN\Backup Operators
No privileges assigned

BUILTIN\Server Operators
No privileges assigned

BUILTIN\Administrators
No privileges assigned

Everyone
No privileges assigned
```

可以使用 `net` 命令通过此方法获取当前支持的权限和特权功能：

```
root# net rpc rights list -U root%\not24get
SeMachineAccountPrivilege    Add machines to domain
SePrintOperatorPrivilege    Manage printers
SeAddUserPrivilege          Add users and groups to the domain
SeRemoteShutdownPrivilege   Force shutdown from a remote system
SeDiskOperatorPrivilege     Manage disk shares
SeBackupPrivilege           Back up files and directories
SeRestorePrivilege          Restore files and directories
SeTakeOwnershipPrivilege    Take ownership of files or other objects
```

机器账户特权是必需的，以便允许将 Windows NT 4.0 或更高版本的网络客户端添加到域中。磁盘操作员特权是必需的，以便允许用户管理非由该用户拥有的对象的共享 ACL 以及文件和目录的 ACL。

在这个例子中，所有权限都分配给了“域管理员”组。这是一个好主意，因为通常期望该组的成员拥有全权。这种分配使这一期望成为现实：

```
root# net rpc rights grant "MIDEARTH\Domain Admins" \
SeMachineAccountPrivilege SePrintOperatorPrivilege \
SeAddUserPrivilege SeRemoteShutdownPrivilege \
SeDiskOperatorPrivilege -U root%not24get
Successfully granted rights.
```

接下来，域用户 jht 被授予日常管理所需要的特权：

```
root# net rpc rights grant "MIDEARTH\jht" \
SeMachineAccountPrivilege SePrintOperatorPrivilege \
SeAddUserPrivilege SeDiskOperatorPrivilege \
-U root%not24get
Successfully granted rights.
```

以下步骤可用于验证刚才所做的更改：

```
root# net rpc rights list accounts -U root%not24get
MIDEARTH\jht
SeMachineAccountPrivilege
SePrintOperatorPrivilege
SeAddUserPrivilege
SeDiskOperatorPrivilege

BUILTIN\Print Operators
No privileges assigned

BUILTIN\Account Operators
No privileges assigned

BUILTIN\Backup Operators
No privileges assigned

BUILTIN\Server Operators
No privileges assigned

BUILTIN\Administrators
No privileges assigned

Everyone
No privileges assigned
```

- MIDEARTH\Domain Admins
  - SeMachineAccountPrivilege
  - SePrintOperatorPrivilege
  - SeAddUserPrivilege
  - SeRemoteShutdownPrivilege
  - SeDiskOperatorPrivilege

## 12.6 管理信任关系

信任关系主要有两种类型：第一种是域控制器与域成员机器（网络客户端）之间的信任，第二种是域之间的信任（称为跨域信任）。所有参与域安全的 Samba 服务器都需要一个域成员信任账户，Windows NT/2000/XP 工作站也是如此。

### 12.6.1 机器信任账户

`net` 命令会在 **smb.conf** 文件中查找以获取自身的配置设置。因此，以下命令通过 **smb.conf** 文件“知道”要加入哪个域。

Samba 服务器的域信任账户可以通过以下示例中的方式验证：

```
root#  net rpc testjoin
Join to 'MIDEARTH' is OK
```

如果没有域成员账户，或者账户凭据无效时，将观察到以下结果：

```
net rpc testjoin -S DOLPHIN
Join to domain 'WORLDOCEAN' is not valid
```

将 Samba 服务器加入 Windows ADS 域的等效命令如下：

```
root#  net ads testjoin
Using short domain name -- TAKEAWAY
Joined 'LEMONADE' to realm 'TAKEAWAY.BIZ'
```

如果 ADS 信任未建立，或者因某种原因已损坏，可能会获得以下错误消息：

```
root#  net ads testjoin -UAdministrator%secret
Join to domain is not valid
```

以下展示了在目标域中为执行该命令的 Samba 服务器创建机器信任账户的过程：

```
root#  net rcp join -S 13000 -Uroot%not24get
Joined domain MIDEARTH.
```

将 Samba 服务器加入 Samba 域会导致创建机器账户。下面是一个示例：

```
root#  pdbedit -Lw merlin$
merlin$:1009:9B4489D6B90461FDBA3E3C3AB96147E16:\
      176DC8554E99914BDF3407DEA2231D80:[S          ]:LCT-42891919:
```

方括号中的 S 表示这是一个服务器（PDC/BDC）账户。可以将域加入类型设置为仅作为工作站加入，此时 S 将被 W 替代（表示工作站账户）。可以使用以下命令来实现这一点：

```
root#  net rcp join member -S 13000 -Uroot%not24get
Joined domain MIDEARTH.
```

请注意，命令行参数 *member* 使此加入操作具有特定性。默认情况下，类型是从 *smb.conf* 文件的配置中推导出来的。若要特定地作为 PDC 或 BDC 加入，命令行参数将是 [PDC | BDC]。例如：

```
root#  net rcp join bdc -S 13000 -Uroot%not24get
Joined domain MIDEARTH.
```

最好让 Samba 根据 *smb.conf* 文件中的设置来确定域加入类型。

将 Samba 服务器加入 Windows ADS 域的命令如下：

```
root#  net ads join -UAdministrator%not24get
Using short domain name -- GDANSK
Joined 'FRANDIMITZ' to realm 'GDANSK.ABMAS.BIZ'
```

没有特定选项可以从 NT4 域中移除机器账户。当作为 Windows 机器的域成员被从域中撤回时，域成员账户也不会自动删除。可以使用任何便捷工具移除非活动的域成员账户。如有必要，可以使用以下 **net** 命令删除机器账户：

```
root#  net rpc user delete HERRING\$ -Uroot%not24get
Deleted user account.
```

之所以能够移除，是因为机器账户就像带有尾随 $ 字符的用户账户一样。账户管理操作以类似的方式处理用户账户和机器账户。

作为 Windows ADS 域成员的 Samba-3 服务器可以执行以下命令以脱离域：

```
root#  net ads leave
```

Samba DMS 机器可以通过执行以下命令获取有关 ADS 域的详细信息：

```
root#  net ads status
```

信息的数量非常庞大。有关其使用的更多信息，请参阅书籍“Samba-3 by Example”的第 7 章。这本书可以以印刷版或在线形式从 Samba-3 by Example<sup>1</sup> 获取。

### 12.6.2 跨域信任

跨域信任关系是授予一个域中的用户在另一个域中访问权限和特权的主要机制。

要查看当前生效的信任关系，请执行此命令：

```
root#  net rpc trustdom list -Uroot%not24get
Trusted domains list:

none

Trusting domains list:
```

此时没有跨域信任；以下步骤将创建它们。

有必要在本地域中创建一个信任账户。第二个域中的域控制器可以使用该账户创建受信任连接。这意味着外部域被信任以访问本地域中的资源。此命令创建本地信任账户：

```
root# net rpc trustdom add DAMNATION f00db4r -Uroot%\not24get
```

可以使用 **pdbedit** 显示该账户，如下所示：

```
root# pdbedit -Lw DAMNATION\$
DAMNATION\$ 1016 9ACF121DF897689AAD3B435B51404EE 7F845808B91BB9F7FEF44B247D9DC9A6 [I ] LCT-428934B1:
```

信任账户在方括号内的字段中始终会有一个 I。

如果无法连接到信任域，以下命令将失败：

```
root# net rpc trustdom list -Uroot%\not24get
Trusted domains list:

none

Trusting domains list:

DAMNATION S-1-5-21-1385457007-882775198-1210191635
```

上述命令执行成功；当获得以下响应时，表示失败：

```
net rpc trustdom list -Uroot%\not24get
Trusted domains list:

DAMNATION S-1-5-21-1385457007-882775198-1210191635

Trusting domains list:

DAMNATION domain controller is not responding
```

> <sup>1</sup><http://www.samba.org/samba/docs/Samba3-ByExample.pdf>

