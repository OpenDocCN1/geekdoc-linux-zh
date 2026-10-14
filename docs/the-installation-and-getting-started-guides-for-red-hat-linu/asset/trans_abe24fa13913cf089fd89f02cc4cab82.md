

每个对话框以退出菜单层级。当你来到一个标记为系统状态的对话框时，按 [Enter] 以执行默认操作，即应用你所做的更改。

此时，基于 Web 的访问已启用。要测试它，请前往你已添加到访问控制列表的系统之一。启动你的 Web 浏览器，并输入以下 URL：

```
http://<host>:98/
```

（当然，将 <host> 替换为你的系统主机名。）

你应该会看到主 Linuxconf 页面。请注意，你需要输入系统的 root 密码才能访问第一页之外的内容。

## 添加用户账户 — 快速参考

- 1. 在 shell 提示符下输入 linuxconf 启动 Linuxconf
- 2. 打开 [Config] -> [Users accounts] -> [Normal] -> [User accounts]
- 3. 选择 Add
- 4. 输入账户的登录名和全名
- 5. 仅在必要时在其他字段中输入信息
- 6. 选择 Accept
- 7. 输入账户的初始密码
- 8. 在 Confirmation 字段中重新输入账户的初始密码
- 9. 选择 Accept

## 添加用户账户 — 总体概述

添加用户是你管理系统中会遇到的最基本任务之一。要添加用户：

- 在 shell 提示符下输入 linuxconf 启动 Linuxconf。
- 打开 [Config] -> [Users accounts] -> [Normal] -> [User accounts] 这将打开 Users accounts 选项卡（见图 8-3）。
- 如果系统上有超过 15 个账户，Linuxconf 将为你提供一个筛选屏幕（见图 8-2）。你可以使用它来选择比完整列表更小的账户范围。要获取完整列表，请在不更改任何参数的情况下选择 Accept。有关各种筛选器的详细信息，请在 Filter 控制屏幕上选择 Help 按钮。
- 选择 Add。这将打开 User account creation 选项卡（见图 8-4）。

![](img/46f4935125ba89e12897afbe9d77a097_180_0.png)

### Figure 8-2: Filter Control Screen

User account creation 选项卡是你输入新账户所有信息的地方。有许多字段你应该了解，其中一些是必需的，一些是可选的。

### Figure 8-3: Users Accounts Screen

### Figure 8-4: User Account Creation

## Required Fields:

- **Login name** — 账户的名称。通常全部为小写字母。名字、姓氏、首字母或其组合是相当常见的登录名。对于名为 John T. Smith 的用户，“smith”、“john”、“jts”或“jsmith”都是常见的用户名。当然“spike”或其他名称也完全可以。你也可以使用数字，因此如果有第二个同首字母的人，“jts2”是可以的。此字段没有默认值。

## Optional Fields:

- **Full name** — 这是用户或账户的名称。对于个人，就是他们的名字，例如“John T. Smith”。如果账户代表职位而非个人，全名可能是职称。因此名为“webmaster”的账户的全名可能是“Red Hat Webmaster”或仅“Webmaster”。此字段没有默认值。

- **group** — 在这里你可以指定与账户关联的组。默认是一个与登录名相同的组。因此“jsmith”将有组“jsmith”。

- **Supplementary groups** — 这里是你指定任何附加组的地方。我们建议如果你想将用户添加到一个或多个组，请在此处操作，而不是更改 group 字段。组名应以空格分隔。此字段的默认值为空白，表示没有补充组。

- **Home directory** — 指定账户的主目录或登录目录。默认是 /home/login，其中 login 由登录名替换。主目录是你登录时在目录结构中的起点，或在 X 中，为每个打开的 xterm 窗口。这也是存储账户特定首选项文件的位置。

- **Command interpreter** — 指定命令解释器的位置。命令解释器通常称为 shell。默认显示在下拉框中。

- **User ID** — 与每个用户账户关联的数字。这是系统在创建账户时自动生成的。

**User account creation** 屏幕有许多字段；只有 login name 是必需的，尽管强烈建议填写 **Full name** 字段。输入登录名和任何其他所需信息后，选择屏幕底部的 **Accept** 按钮。如果你决定不创建新用户，则点击 **Cancel** 即可。

