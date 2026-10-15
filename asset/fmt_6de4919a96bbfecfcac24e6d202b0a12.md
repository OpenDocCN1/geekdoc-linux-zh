
### Sat Oct 6 20:52:55 2001 : Conflict details of entries from map file and existing entries in AD. map file = 'passwd'

target container = `LDAP://localhost/CN=Users,DC=linuxrainer,DC=info'`

conflicts with existing object = 'rbrunson'

existing object = rbrunson, CN=Users,DC=linuxrainer,DC=info'

YES

可以迁移。对象 = 'root'。要迁移的容器 =

`LDAP://localhost/CN=Users, DC=linuxrainer, DC=info.`

YES

可以迁移。对象 = 'bin'。要迁移的容器 =

`LDAP://localhost/CN=Users, DC=linuxrainer, DC=info.`

YES

可以迁移。对象 = 'daemon'。要迁移的容器 =

`LDAP://localhost/CN=Users, DC=linuxrainer, DC=info.`

CONFLICT

object key = 'rbrunson'

# 在 Windows 2000 中配置映射服务

让我们完成让本地 Windows 用户的 AD 匹配 Linux 用户的工作。这是为了确保所有访问权限都正确映射。

1. 点击“开始 | 程序 | Services for Unix | Services for Unix Administration”打开 Services for Unix GUI 控制台。
2. 在左面板中选择“用户名映射服务（Username Mapping Service）”，这将显示图 13.4 所示的屏幕。
3. 在右面板中有一个蓝色条，带有“配置（Configuration）”、“映射（Maps）”和“映射维护（Map Maintenance）”，其中“配置”颜色较浅。点击“映射（Maps）”菜单，该对话框将刷新显示新内容。
4. 在新对话框中，你应该勾选“简单映射（Simple Maps）”复选框，这将启用其余对话框选项。如何填写请参见图 13.5。

| 点击“开始 | 程序 | Services for Unix | Services for Unix Administration”打开 Services for Unix GUI 控制台。 |
| :--- | :--- | :--- |
| 5. 如你所示，我正在使用 AD Domain BRSON 作为目标 Windows 服务器，我的 NIS 域名称已正确填写。 |

# 使用映射服务映射用户

使用映射服务的映射步骤如下：

1. 点击“开始 | 程序 | Services for Unix | Services for Unix Administration”打开 Services for Unix GUI 控制台。
2. 在左面板中选择“用户名映射服务（Username Mapping Service）”，这将显示图 13.4 所示的屏幕。
3. 在右面板中有一个蓝色条，带有“配置（Configuration）”、“映射（Maps）”和“映射维护（Map Maintenance）”，其中“配置”颜色较浅。点击“映射（Maps）”菜单，该对话框将刷新显示新内容。
4. 在新对话框中，你应该勾选“简单映射（Simple Maps）”复选框，这将启用其余对话框选项。如何填写请参见图 13.5。
5. 如你所示，我正在使用 AD Domain BRUNSON 作为目标 Windows 服务器，我的 NIS 域名称已正确填写。

| 日期 | 大小 | 文件 |
| :--- | :--- | :--- |
| 03/28/2000 06:04a | 1,600,000 | `nis2ad.exe` |
| 03/28/2000 06:04a | 1,455,110 | `nisadmin.exe` |
| 03/28/2000 06:04a | 1,600,512 | `nismap.exe` |
| 03/28/2000 06:38a | 69,200 | `nissvc.exe` |

6. 点击右上角的“Apply”（应用）按钮，然后点击右侧格底部的“Show User Maps”（显示用户映射）文本。你将看到图13.6所示的对话框，现在我们可以获取实际映射，并开始用户与组之间的匹配。

## 高级映射

要映射用户名，点击“Show User Maps”（显示用户映射）。要映射组名，点击“Show Group Maps”（显示组映射）。

- Hide User Maps（隐藏用户映射）
- Show Group Maps（显示组映射）

| Windows 域名称: | | NIS 域名称: |
|---|---|---|
| BRUNSON | example.com |
| NIS 服务器名称（可选）： | |
| nsserver | |
| List Windows Users（列出 Windows 用户） | List UNIX Users（列出 UNIX 用户） |
| Windows 用户: | UNIX 用户: |
| Windows 用户 | UID |
| Windows 用户名: | UNIX 用户名: |

要创建映射，输入想要映射的用户名，并点击“Add”（添加）。

高级映射列在下方。若要在“Mapped users”（已映射用户）列表中显示简单映射，请勾选下方的复选框。如果多个 Windows 用户名映射到一个 UNIX 用户名，你必须选择一个映射作为主映射。要将某个映射设置为主映射，选择该映射并点击“Set Primary”（设置主映射）。

| Windows User | UNIX Dom... | UNIX User | UID | Prim... |
|---|---|---|---|---|
| Set Primary | Remove（移除） | | | |
- Display simple maps in Mapped users list（在已映射用户列表中显示简单映射）

图13.6 显示用户映射的对话框。

## Linux 的 NIS 和微软的 NIS 服务器

7. 点击“List Windows Users”（列出 Windows 用户）按钮，这将填充 Windows 用户列表框；然后对“List Users”（列出用户）按钮执行相同操作，列表框将从 NIS 服务器填充。
8. 接下来选择你想要映射的 Windows 用户，以及与你映射目标对应的 Linux 用户。图13.7 显示了配置后的外观。

## 映射映射

要映射用户名，点击“Show User Maps”（显示用户映射）。要映射组名，点击“Show Group Maps”（显示组映射）。

- Hide User Maps（隐藏用户映射）
- Show Group Maps（显示组映射）

| Windows 域名称: | NIS 域名称: |
|---|---|
| BRUNSON | example.com |
| NIS 服务器名称（可选）： | nsserver |
| List Windows Users（列出 Windows 用户） | List UNIX Users（列出 UNIX 用户） |
| Windows 用户: | UNIX 用户: |
| Windows 用户 | UID |
| unmapped | |
| Guest | |
| krbtgt | |
| rbrunson | 30080 |
| sfuser | |
| InternetUser | |
| Windows 用户名: | UNIX 用户名: |
| rbrunson | rbrunson |

要创建映射，输入想要映射的用户名，并点击“Add”（添加）。

高级映射列在下方。若要在“Mapped users”（已映射用户）列表中显示简单映射，请勾选下方的复选框。如果多个 Windows 用户名映射到一个用户名，你必须选择一个映射作为主映射。要将某个映射设置为主映射，选择该映射并点击“Set Primary”（设置主映射）。

| Windows User | UNIX Dom... | UNIX User | Uid | Prim... |
|---|---|---|---|---|
| Set Primary | Remove（移除） | | | |
- Display simple maps in Mapped users list（在已映射用户列表中显示简单映射）

图13.7 映射 Windows 用户的示例。

高级映射列在下方。若要在“Mapped users”（已映射用户）列表中显示简单映射，请勾选下方的复选框。如果多个 Windows 用户名映射到一个 UNIX 用户名，你必须选择一个映射作为主映射。要将某个映射设置为主映射，选择该映射并点击“Set Primary”（设置主映射）。
