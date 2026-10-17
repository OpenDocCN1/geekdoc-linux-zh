
- 7. 单击 `Repeat Task`（重复任务）按钮，并按照步骤 5 中的程序创建 `Bernie Mueller` 的用户账户。
- 8. 单击 `OK`（确定）返回 iManager 主窗口，并保持登录状态以便进行下一个活动。

## 创建组织角色对象

除了减少向多个用户分配权限的需求外，组是为用户提供执行特定工作职责所需权限的便捷方式。然而，通常您不希望创建代表公司职位的组。例如，David Heise 希望 IT 部门为每个部门的数据和用户账户设置一个经理。目前，Kari Means 被指定担任工程部门数据和用户账户的经理，Russ Pence 负责制造部门的数据和用户，行政助理 Lynn Dai 则担任商业部门的管理者。

此外，为了通过限制网络管理员用户名的使用来提高安全性，Eric 创建了单独的账户来执行管理任务，例如 eDirectory 管理和打印机管理。由于分配给这些职位的用户账户会发生变化，并且可能包括多个用户，Eric 不希望向单个用户分配权限。与其为这些类型的职位创建组，Novell 提供了另一种名为 `Organizational Role object`（组织角色对象）的对象类型，它允许您将权限分配给对象，而不是特定的用户。然后，您可以将任何用户设为组织角色对象的参与者，从而获得其相关权限。如果工作职责移交给另一名员工，您只需要让新员工成为该组织角色对象的参与者。例如，为了使其用户账户拥有执行 eDirectory 管理功能的权限，Eric 使 `EKenton` 用户成为 `eDirAdm` 组织角色对象的参与者。图 5-25 列出了 Eric 为 UAS 网络定义的组织角色对象。

**组织角色规划表单**

创建者： | 日期：

| 角色名称 | 上下文 | 用途 | 主要参与者 |
| :--- | :--- | :--- | :--- |
| SysOp | .IT.UAS | 备用系统操作员 | Clark Kent |
| eDirAdm | .IT.UAS | 维护 eDirectory 的管理角色 | EKenton |
| PrintAdm | .IT.UAS | 维护 Internet 打印的管理角色 | EKenton, KThiele |
| EngMgr | Engineering.UAS | 工程部门数据经理 | Kari Means |
| ISSEng | Engineering.UAS | 分配给国际空间站的初级工程师 | Tony Rucci |
| RoverEng | .Mfg.Engineering.UAS | 分配给火星漫游者项目的初级工程师 | Lianne Jarka |
| MfgMgr | .Mfg.Engineering.UAS | 制造部门数据经理 | Russ Pence, Bernie Mueller |
| AdmAss | .Mgmt.UAS | UAS 行政助理 | Lynn Dai, Kari Means |
| AeroMgr | .Mfg.Engineering.UAS | AeroDyn 部门网络对象经理 | Bernie Mueller |

图 5-25 UAS 组织角色规划表单

在第 6 章和第 7 章中，您将学习如何为这些组织角色对象分配职位所需功能所需的权限。在以下活动中，您将学习如何使用 iManager 创建组织角色对象，然后分配用户作为参与者。

### 活动 5-15：创建组织角色对象

**所需时间：** 10 分钟

**目标：** 使用 iManager 创建和管理组织角色对象。

**要求：** 完成活动 5-14

**描述：** 为了满足为每个部门数据设置经理的指令，Eric 为每个部门经理创建了一个组织角色对象，然后指定了一个用户账户作为参与者。在此活动中，您将为 IT 部门创建 Eric 在图 5-25 中定义的组织角色对象。

- 1. 如有必要，登录您的本地计算机，打开您的 Web 浏览器以启动 iManager，并使用您的管理用户名和密码登录 iManager。
- 2. 如有必要，单击展开 `eDirectory Administration`（eDirectory 管理）标题，然后单击 `Create Object`（创建对象）链接。
- 3. 在 Available object classes（可用对象类）列表框中，单击 `Organizational Role`（组织角色），然后单击 `OK`（确定）以显示创建组织角色窗口。
- 4. 请按照以下步骤创建一个名为 `eDirAdm` 的组织角色对象：
  - a. 在 Organizational Role name（组织角色名称）文本框中输入 `eDirAdm`。
  - b. 单击 Context（上下文）文本框旁边的 `Object Selector`（对象选择器）按钮，并将上下文设置为 `IT OU`。
  - c. 单击 `OK`（确定）以显示“Complete: The Create Organizational Role request succeeded”（完成：创建组织角色请求成功）消息。
- 5. 单击 `Repeat Task`（重复任务）按钮。按照步骤 4 中的程序在 `IT OU` 中创建一个名为 `PrintAdm` 的组织角色对象。
- 6. 单击 `OK`（确定）返回 iManager 主窗口。
- 7. 请按照以下步骤将 `EKenton` 添加为 `eDirAdm` 组织角色的参与者：
  - a. 如有必要，单击展开 `eDirectory Administration`（eDirectory 管理）标题。
  - b. 单击 `Modify Object`（修改对象）链接以打开修改对象窗口。
  - c. 单击 Object name（对象名称）文本框旁边的 `Object Selector`（对象选择器）按钮，然后导航到 `IT OU`。单击 `eDirAdm` 对象以将其放置在 Object name（对象名称）文本框中。
  - d. 单击 `OK`（确定）以打开 `eDirAdm` 对象的修改对象窗口。
  - e. 单击 `Role occupant`（角色参与者）链接以显示图 5-26 中所示的 Role occupant（角色参与者）列表框。
  - f. 单击 `Object Selector`（对象选择器）按钮，如有必要，导航到 `IT OU`（参见图 5-27）。
  - g. 单击 `EKenton` 用户账户，以将其添加到 Object Selector（对象选择器）窗口底部的 Selected Objects（已选对象）列表框中。

![](img/840007e8f98ea6653e5877e945c27dc6_213_0.png)

> 您可以使用 Object Selector（对象选择器）窗口将多个用户添加到 Selected Objects（已选对象）列表框中。

  - h. 单击 `OK`（确定）。然后，`EKenton` 应出现在 Role occupant（角色参与者）列表框中。
  - i. 单击 `OK`（确定）保存您的更改并返回 iManager 主窗口。
- 8. 重复步骤 7，将 `EKenton` 和 `KThiele` 都添加为 `PrintAdm` 组织角色对象的参与者。
- 9. 保持 iManager 登录状态以便进行下一个活动。

![](img/840007e8f98ea6653e5877e945c27dc6_214_0.png)

![](img/840007e8f98ea6653e5877e945c27dc6_214_1.png)

## 更新多个用户账户

作为网络管理员，您经常会发现，在创建用户账户后，需要对多个不同的用户进行修改，例如禁止用户在午夜至凌晨 4:00 之间登录网络，以便您执行登录限制。为了简化这项工作，您可以使用 iManager 或 ConsoleOne 同时修改多个用户账户。在 ConsoleOne 中，若要更改多个用户的通用属性，例如地址或登录限制，您可以通过按 Ctrl 键高亮显示用户名称、选择组、模板或容器，然后从菜单中选择“文件”、“多用户属性”来选中多个用户。如果您选择的是组或容器对象，则该组或容器中的所有用户都会被修改。如果您选择的是模板对象，则所有使用该模板创建的用户账户都可以被修改。您还可以使用 iManager 来修改多个用户账户。在以下活动中，您使用 ConsoleOne 和 iManager 来修改容器中的所有用户并更新特定用户。

### 活动 5-16：更新容器或模板中的所有用户

**所需时间：** 10 分钟

**目标：** 使用 ConsoleOne 更新多个用户账户。

**要求：** 完成活动 5-14，以及一台安装了 Novell 客户端的 Windows XP 计算机

**描述：** IT 部门的用户共用一台传真机，管理层希望将该传真号码设置在所有 IT 用户账户中。在此活动中，您将学习如何更新 IT OU 中的所有用户账户。
