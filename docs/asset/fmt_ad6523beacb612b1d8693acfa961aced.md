
此外，你可以使用 `dsadd` 创建计算机对象。使用 `dsadd` 创建计算机的唯一必需语法是计算机对象的可区分名称，如下例所示：

```
dsadd computer
cn=workstation1,ou=Marketing,ou=Workstations,dc=lucernepublishing,dc=com
```

最后，你还可以使用 `dsadd` 创建组对象。除了组的可区分名称和 SAM 账户名称外，你还可以指定组的范围（本地、全局或通用）以及组是安全组还是分发组。例如，若要创建名为 Trainers 的全局安全组，请使用以下语法：

```
dsadd group
cn=Trainers,ou=HR,dc=lucernepublishing,dc=com -scope g -secgroup yes
-samid trainers
```

若要使用批处理文件创建多个对象（包括用户、组或任何其他对象类型），请打开记事本，并使用这些示例中的语法，每行放置一个命令。输入所有命令后，保存文件并使用 `.cmd` 或 `.bat` 扩展名对其进行命名。当你进入命令提示符处输入批处理文件的名称或在 Windows 资源管理器中双击该文件时，具有 `.cmd` 或 `.bat` 扩展名的文件将按行处理。

## 使用 CSVDE

Microsoft Excel 和 Microsoft Exchange 是两个常见的应用程序，你可以在其中拥有许多用户名、地址和联系信息以添加到 Active Directory 数据库。在这种情况下，你可以通过将这些信息保存为逗号分隔值 `CSV` 格式的文件来导入和导出这些应用程序的信息。`CSV` 格式也可用于从其他第三方应用程序导入和导出信息。例如，你可能需要将用户账户信息导出到文件中，以便用于另一个第三方应用程序，如 UNIX 数据库。`CSVDE` 也可以提供这种功能。

`CSVDE` 命令行实用程序允许管理员导入或导出 Active Directory 对象。它使用基于头记录的 `.csv` 文件，该记录描述了数据的每个部分。头记录只是使用正确属性名称的文本文件的第一行。属性名称必须与 Active Directory 模式允许的属性匹配。例如，如果你有一份想要作为用户导入到 Active Directory 数据库中的人员和电话号码列表，你需要创建一个准确反映你想要创建的物体名称和属性的头记录。审查以下用于创建用户账户的常见属性：

- `dn`。指的是对象的可区分名称，以便该对象可以适当地放置在 Active Directory 中。
- `sAMAccountName`。填充用于 Windows 2000 之前登录名称的 SAM 账户字段。
- `objectClass`。确定要创建的对象类型，例如用户、组或 OU。
- `telephoneNumber`。填充电话号码字段。
- `userPrincipalName`。填充账户的用户主体名称字段。

### 注意

除了创建用户和组对象外，你还可以使用 `dsadd` 创建计算机对象、联系人对象和组织单位。

## 使用 CSVDE

在创建数据库文件时，请按标题记录中属性的顺序排列数据。如果字段和数据顺序错误，运行 `CSVDE` 实用程序时可能会遇到错误，或者在创建的对象中无法获得准确的结果。以下是一个标题记录的示例，使用前面列出的属性来创建用户对象。

```
dn,sAMAccountName, userPrincipalName, telephoneNumber, objectClass
```

使用该标题记录的数据记录将显示如下：

```
"cn=Scott SeeIy, ou=Sales, dc=cohwinery, dc=com", SSeeIy, SSeeIy@cohwinery. com, 586-555-1234, user
```

在为你要创建的每个账户添加记录后，使用 `.csv` 作为扩展名保存文件。假设你创建了一个名为 `Newusers.csv` 的文件，键入以下命令以执行用户账户的创建。

```
csvde.exe -i -f newusers.csv
```

`-i` 开关告知 `CSVDE` 此操作将把用户导入活动目录数据库。`-f` 开关用于指定包含要导入记录的 `.csv` 文件。

## 使用 LDIFDE

`LDIFDE` 是一个具有与 `CSVDE` 相同基本功能的实用程序，并提供修改活动目录中现有记录的能力。因此，`LDIFDE` 是一个更灵活的选项。考虑这样一个示例：你必须将 200 个新用户导入到你的活动目录结构中。在这种情况下，你可以使用 `CSVDE` 或 `LDIFDE` 来导入这些用户。然而，你可以稍后使用 `LDIFDE` 来修改或删除这些对象，而 `CSVDE` 不提供此选项。

你可以使用任何文本编辑器创建 `LDIFDE` 输入文件，该文件按照 LDAP 数据交换格式 `LDIF` 标准进行格式化。包含希望创建的对象记录的数据文件的格式与 `CSVDE` 的格式有显著差异。以下示例展示了创建与 `CSVDE` 部分讨论的相同 `jsmith` 用户账户的数据文件语法。

```
Dn:
cn=jsmith, ou=Marketing, ou=Accounts, dc=Lucernepublishing, dc=com
changetype: add
objectClass: user
sAMAccountName: jsmith
userPrincipalName: jsmith@Lucernepublishing. com
telephoneNumber: 586-555-1234
```

使用 `LDIFDE`，你可以指定由 LDIF 文件执行的三种操作之一：

- **添加**。指定该记录包含一个新对象。
- **修改**。指定将修改现有对象的属性。
- **删除**。指定该记录将删除指定的对象。

创建数据文件并使用 `.LDF` 文件扩展名保存后，键入以下语法以执行 `LDIFDE` 脚本并修改活动目录对象。

```
ldifde -i -f newobjects.ldf
```

下一个示例说明了修改之前创建的用户对象的电话号码所需的语法。请注意，最后一行中的连字符对于文件正确运行是必需的。

```
On:
cn=jsmith,ou=Marketing,ou=Accounts,dc=cohowinery,dc=com
changetype: modify
replace: telephoneNumber
telephoneNumber: 586-555-1111
-
```

## 使用 Windows 脚本宿主

Windows 脚本宿主 `WSH` 支持 Microsoft VBScript 和 JScript 引擎。它具有从 Windows 界面或命令提示符运行脚本的灵活性。`WSH` 内置于所有版本的 Windows Vista、Windows 2000、Windows XP、Windows Server 2003 和 Windows Server 2008 中。它提供了一种强大的脚本方法，支持多种管理任务，包括创建活动目录对象、映射驱动器、连接打印机、修改环境变量以及修改注册表项。

以下示例是一个使用 `WSH` 为 Scott Seely 创建用户账户的 VBScript。你可以使用任何文本编辑器编写和编辑脚本。脚本应保存为 `.vbs` 扩展名。请注意，前几行准备了在 `cohowinery.com` 的 Sales OU 中创建用户对象的脚本。第四行文本开始了指定 Scott Seely 及其账户活动目录信息的内容。空白行用于视觉目的，并在文件处理期间被忽略。

```vbscript
Option Explicit
Dim ldapP, acctUser

Set ldapP = GetObject("LDAP://OU=sales,DC=cohowinery,DC=com")

Set acctUser = ldapP.Create("user", "CN=" & "Scott Seely")
Call acctUser.Put("sAMAccountName", "sseely")
Call acctUser.Put("userPrincipalName", "sseely@cohowinery.com")
Call acctUser.Put("TelephoneNumber", "586-555-1234")
Call acctUser.Put("userAccountControl", &H200)
acctUser.SetPassword ("Mpress#1")
acctUser.SetInfo
Set acctUser = Nothing
```

假设之前脚本文件的名称是 `Newusers.vbs`，在命令提示符下键入以下命令以运行它。

```
cscript c:\newusers.vbs
```

## 技能矩阵总结

### 在本课中你学到了：

- Windows Server 2008 中存在三种类型的用户账户：本地用户账户、域用户账户和内置用户账户。本地用户账户驻留在本地计算机上，并且不会由活动目录复制到其他计算机。域用户账户在活动目录中创建和存储，并复制到域内的所有域控制器。内置用户账户在操作系统安装时自动创建，当成员服务器提升为域控制器时也会创建。
