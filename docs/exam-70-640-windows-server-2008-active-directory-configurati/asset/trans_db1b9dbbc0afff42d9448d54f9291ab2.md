

4.  若要添加新的本地用户账户，请右键单击 **Users** 文件夹，然后单击 **New User**。将显示“新建用户”窗口，如图 5-4 所示。

**图 5-4**
新建用户窗口

![](img/a8ee53dbf1310726255b6fbb9f296fb2_157_0.png)

5.  在以下字段中输入适当的值，然后单击 **Create**：
    - a. 用户名
    - b. 全名
    - c. 描述
    - d. 密码
    - e. 确认密码

6.  若要创建新的组对象，请在左侧窗格中右键单击 **Groups** 文件夹，然后单击 **New Group**。将显示“新建组”窗口，如图 5-5 所示。在以下字段中输入适当的值：
    - a. 组名
    - b. 描述

**图 5-5**
新建组窗口

![](img/a8ee53dbf1310726255b6fbb9f296fb2_157_1.png)

7.  若要向组中添加用户，请单击 **Add**。将显示“选择用户”屏幕。
8.  输入要添加的用户账户名称，然后单击 **OK**。
9.  单击 **Create**，然后关闭计算机管理控制台。
10. 关闭所有打开的窗口，然后注销成员服务器。

## 部分 B – 处理域用户和组对象

1.  使用域管理员凭据登录到域控制器。
2.  单击 **Start** 按钮，单击 **Administrative Tools**，然后单击 **Active Directory Users and Computers**。
3.  展开 <domain name> 节点；在此情况下，展开 lucernepublishing.com。
4.  右键单击 **Users**，选择 **New** → **User**。将显示“新建对象 – 用户”屏幕，如图 5-6 所示。在以下字段中输入适当的值，然后单击 **Next**：
    - a. 名
    - b. 姓
    - c. 用户登录名

![](img/a8ee53dbf1310726255b6fbb9f296fb2_158_0.png)

5.  在 **Password** 字段中输入用户的初始密码。在 **Confirm password** 字段中输入相同的初始密码。单击 **Next**。
6.  单击 **Finish**。
7.  右键单击 **Users**，单击 **New**，然后单击 **Group**。将显示“新建对象 – 组”窗口，如图 5-7 所示。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_158_1.png)

8.  在以下字段中输入适当的值，然后单击 **OK** 以创建组；Group name (pre–Windows 2000) 字段将自动填充：
    - a. **Group name: FinanceUsers**
    - b. **Group scope: Global**
    - c. **Group type: Security**
9.  若要创建命令提示符中的对象，请单击 **Start** 按钮，输入 **cmd**，然后按 **Enter** 键。

10. 在命令提示符处，输入以下命令，然后按 (Enter) 键，替换为适当的域可识别名称，例如 dc=lucernepublishing,dc=com：
    ```
    Dsadd user "cn=Robert Brown,cn=Users,<domain dn>" -samid rbrown -pwd MSPress#1 -mustchpwd yes -disabled no
    ```
11. 若要在命令行创建组对象，请键入以下命令，然后按 (Enter) 键，替换为适当的域可识别名称，例如 dc=lucernepublishing,dc=com：
    ```
    Dsadd group cn=Accounting,cn=Users,<domain dn> -desc "Accounting Users" -secgrp yes -scope g
    ```
12. 在 Active Directory 用户和计算机 MMC 控制台中，单击左侧窗格中的 Users。按 F5 刷新右侧窗格中的列表，以确认刚刚在命令行创建的用户和组对象存在。

停止。关闭所有打开的窗口并注销 Active Directory 域控制器。

在之前的练习中，你使用图形用户界面 (GUI) 和 Windows Server 2008 中可用的一些命令行工具创建了一个单个用户和组对象。在接下来的章节中，我们将研究一些可用于自动化创建大量 Active Directory 对象的机制。

![](img/a8ee53dbf1310726255b6fbb9f296fb2_159_0.png)

## 使用批处理文件

> 批处理文件是常用文件，可以使用任何文本编辑器编写。你可以通过遵循标准批处理文件规则并使用在 Windows Server 2003 及更高版本中可用的 dsadd 命令，编写批处理文件来在 Active Directory 中创建对象。Dsadd 可用于创建、删除、查看和修改 Active Directory 对象，包括用户、组和 OU。

若要使用 dsadd 实用工具创建用户，你需要知道用户和用户的登录 ID 的可区分名称，该登录 ID 在 Active Directory 中也被称为 SAM 账户名称属性。对象的可区分名称表示其在 Active Directory OU 结构中的相对位置。例如，可区分名称 cn=jsmith,ou=accounts, dc=lucernepublishing,dc=com 指的是位于 Accounts OU 中的 jsmith 账户，该 OU 位于 lucernerpublishing.com Active Directory 域中。每个对象都有唯一的 DN，但如果你将对象移动到 Active Directory 结构中的不同位置，该 DN 可能会改变。如果你在 Lucerne Publishing 中为各个部门创建单独的 OU，那么即使它是具有相同权利和权限的相同用户对象，上述 DN 也可能变为 cn=jsmith,ou=Marketing,ou=Accounts,dc=lucerneppublishing,dc=com。SAM 账户名称指的是每个用户的登录名称——即用户主体名称 (@) 左侧的部分——即 jsmith@lucerneppublishing.com。SAM 账户名称在整个域中必须是唯一的。

当你拥有这两项内容时，你可以使用以下语法通过 dsadd 实用工具创建用户：

```
dsadd user username DN -samid SAM account name
```

例如，你可以按以下方式创建上述提到的 jsmith 账户：

```
dsadd user
cn=jsmith,ou=Marketing,ou=Accounts,dc=lucernepublishing,dc=com -samid jsmith
```

你也可以使用 dsadd 工具添加字段。以下语法将 MySecretC0de 指定为 jsmith 账户的密码：

```
dsadd user
cn=jsmith,ou=Marketing,ou=Accounts,dc=lucernepublishing,dc=com -samid
jsmith -pwd MySecretC0de
```

此外，你可以使用 dsadd 创建计算机对象。使用 dsadd 创建计算机的唯一必需语法是计算机对象的可区分名称，如下例所示：

```
dsadd computer
cn=workstation1,ou=Marketing,ou=Workstations,dc=lucernepublishing,dc=com
```

最后，你还可以使用 dsadd 创建组对象。除了组的可区分名称和 SAM 账户名称外，你还可以指定组的范围（本地、全局或通用）以及组是安全组还是分发组。例如，若要创建名为 Trainers 的全局安全组，请使用以下语法：

```
dsadd group
cn=Trainers,ou=HR,dc=lucernepublishing,dc=com -scope g -secgroup yes
-samid trainers
```

若要使用批处理文件创建多个对象（包括用户、组或任何其他对象类型），请打开记事本，并使用这些示例中的语法，每行放置一个命令。输入所有命令后，保存文件并使用 .cmd 或 .bat 扩展名对其进行命名。当你进入命令提示符处输入批处理文件的名称或在 Windows 资源管理器中双击该文件时，具有 .cmd 或 .bat 扩展名的文件将按行处理。

## 使用 CSVDE

Microsoft Excel 和 Microsoft Exchange 是两个常见的应用程序，你可以在其中拥有许多用户名、地址和联系信息以添加到 Active Directory 数据库。在这种情况下，你可以通过将这些信息保存为逗号分隔值 (CSV) 格式的文件来导入和导出这些应用程序的信息。CSV 格式也可用于从其他第三方应用程序导入和导出信息。例如，你可能需要将用户账户信息导出到文件中，以便用于另一个第三方应用程序，如 UNIX 数据库。CSVDE 也可以提供这种功能。

CSVDE 命令行实用程序允许管理员导入或导出 Active Directory 对象。它使用基于头记录的 .csv 文件，该记录描述了数据的每个部分。头记录只是使用正确属性名称的文本文件的第一行。属性名称必须与 Active Directory 模式允许的属性匹配。例如，如果你有一份想要作为用户导入到 Active Directory 数据库中的人员和电话号码列表，你需要创建一个准确反映你想要创建的物体名称和属性的头记录。审查以下用于创建用户账户的常见属性：

- • **dn**。指的是对象的可区分名称，以便该对象可以适当地放置在 Active Directory 中。
- • **sAMAccountName**。填充用于 Windows 2000 之前登录名称的 SAM 账户字段。
- • **objectClass**。确定要创建的对象类型，例如用户、组或 OU。
- • **telephoneNumber**。填充电话号码字段。
- • **userPrincipalName**。填充账户的用户主体名称字段。

## 注意

除了创建用户和组对象外，你还可以使用 dsadd 创建计算机对象、联系人对象和组织单位。

