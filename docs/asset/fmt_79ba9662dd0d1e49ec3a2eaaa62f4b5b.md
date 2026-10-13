
- 打开 `Config` => `Users accounts` => `Normal` => `User accounts`。这将打开用户账户标签页（见第 126 页的图 8.3）。

- 如果系统上的账户超过 15 个，`Linuxconf` 将为你提供一个过滤屏幕（见下一页的图 8.2）。你可以用此从完整列表中选择范围较小的账户。要获取完整列表，请在不更改任何参数的情况下选择 `Accept`。有关各种字段的详字体信息，请选择 `Filter` 控制屏幕上的 `Help` 按钮。

- 选择 `Add`。这将打开用户账户创建标签页（见第 127 页的图 8.4）。

账户创建标签页是你为新账户输入所有信息的地方。有许多字段你需要注意，有些是必填的，有些是可选的。

### 必填字段

- `Login name` – 账户名称。通常全全小写。姓、名、缩写或它们的组合都是常见的登录名。对于用户 John T. Smith，“smith"、"john"、its" 或 "jsmith" 都是常见的用户名。当然，“spike" 或其他名称也可以。你也可以使用数字，例如如果你有一个具有相同缩写的第二个个人，那么 "its2" 也是可以。此字段没有默认值。

### 可选字段

- `Full name` – 这是用户或账户的全名。对于个人来说，这将是他们的名字，例如 "John T. Smith"。如果账户代表的是职位而非个人，全名必须是职称。一个名为 "webmaster" 的账户全名可能是 "Red Hat Webmaster" 或简单的 "Webmaster"。此字段没有默认值。

## 8.1 使用 Linuxconf 进行系统配置

![](img/6f1d66e9f0dd8a64781e93022eb9e8cc_140_0.png)

- `group` – 在此处你可以指定与账户相关的组。默认是与该账户关联的组。默认是登录名。

- `Supplementary groups` – 在此处你可以指定任何额外的组。默认为空。

- `Home directory` – 指定账户的家目录。默认是 `/home/`。

- `Command interpreter` – 指定命令解释器的位置。命令解释器通常是 shell。

- `User ID` – 与账户关联的数字。由系统自动生成。

账户创建屏幕有许多字段；只有登录名是必填的，强烈建议填写 `Full name`。一旦输入了任何所需信息，请选择 `Accept` 按钮。如果你决定不创建新用户，请点击 `Cancel`。

点击 `Accept` 后，`Linuxconf` 将提示你输入密码。还有一个名为 `Confirmation` 的字段，你需要在其中再次输入密码。这是为了防止你输错密码。密码长度必须为 6 个字符。它们可以是数字以及小写和大写字母。完成后点击 `Accept`。

## 修改用户账户 – 快速参考

**注意：** 尽管你可以更改任何账户的设置，但更改预创建账户的设置通常不是个好主意。最好在你创建的账户中更改设置并探索选项。

1. 在 shell 提示符处启动 `linuxconf`。
2. 打开 `Config` => `Users accounts` ⇒ `Normal` ⇒ `User accounts`
3. 选择用户账户。
4. 按需要修改条目。
5. 选择 `Accept`。

# 系统配置

![](img/6f1d66e9f0dd8a64781e93022eb9e8cc_143_0.png)

图 8.5：修改密码界面

在用户信息屏幕上，可以根据需要更改信息。要应用更改，请选择 `Accept`（接受）。如果您决定不进行任何更改，请选择 `Cancel`（取消）。这将确保不发生任何更改。

# 修改用户密码 – 快速参考

1. 在 shell 提示符输入 `linuxconf` 启动 `Linuxconf`。
2. 打开 `Config`（配置）-> `User accounts`（用户账户）-> `Normal`（普通）-> `User accounts`（账户）。
3. 选择用户账户。
4. 选择 `Passwd`（密码）。
5. 输入用户的新密码。
6. 在 `Confirmation`（确认）字段再次输入用户的新密码。
7. 选择 `Accept`（接受）。

# 8.1 使用 Linuxconf 进行系统配置

![](img/6f1d66e9f0dd8a64781e93022eb9e8cc_144_0.png)

## 修改用户密码 – 概述

- 在 shell 提示符下输入 `linuxconf` 启动 `Linuxconf`。
- 打开 `Config` -> `Users accounts` -> `Normal` -> `User accounts`。这将打开 `Users accounts` 选项卡（参见第 126 页的图 8.3）。
- 如果系统上的账户超过 15 个，`Linuxconf` 将为您提供一个过滤屏幕（参见第 125 页的图 8.2）。您可以使用它来选择比完整列表更小的账户范围。要获取完整列表，请在不更改任何参数的情况下选择 `Accept`。有关各种过滤器的详细信息，请选择过滤器控制上的 `Help`（帮助）按钮。
- 选择您想要更改密码的账户。这将打开 `User`信息选项卡（参见图 8.6）。
- 从底部的选项中选择 `Passwd`。

`Linuxconf` 将会提示您输入新密码。还有一个名为 `Confirmation`（确认）的字段，您需要在其中再次输入密码。这是为了防止您输入错误密码。密码长度至少为 6 个字符。它们可以包含大小写字母的混合。如果您决定不更改密码，只需点击 `Cancel`。一旦输入了新密码，请选择 `Accept`。

# 修改 root 密码 – 快速参考

1. 在 shell 提示符输入 `linuxconf` 启动 `Linuxconf`。
2. 打开 `Config` -> `Users accounts` -> `Change root password`（更改 root 密码）
3. 输入当前的 root 密码。
4. 选择 `Accept`（接受）。
5. 输入新的 root 密码。
6. 在 `Confirmation`（确认）字段再次输入新的 root 密码。
7. 选择 `Accept`（接受）。

# 修改 root 密码 – 概述

更改 root 密码的方式与更改用户密码的方式不同。由于涉及 root 访问的重要性和安全性考虑，`Linuxconf` 要求您验证当前确实拥有访问 root 账户的权限。

- 在 shell 提示符输入 `linuxconf` 启动 `Linuxconf`。
- 打开 `Config` -> `Users accounts` -> `Change root password`

该界面有点令人困惑，因为标题和描述都没有真正解释界面的目的。`Linuxconf` 似乎在要求新密码，但实际上并非如此。`Linuxconf` 想要的是访问 root 账户的 root 密码。`Linuxconf` 确实需要访问 root 的权限，但一旦使用 `Linuxconf` 的人离开电脑一分钟，没有任何东西阻止别人坐在电脑前。陷阱显而易见：如果原来使用 `Linuxconf` 的人退出了 root，他们将无法再次进入。缺乏验证将导致任何更改 root 密码的人获得电脑的控制权。

一旦输入了 root 密码，它将提示您输入新密码。还有一个名为 `Confirmation`（确认）的字段，您需要在其中再次输入密码（参见第 128 页的图 8.5）。这是为了防止您输入错误密码。密码长度至少为 6 个字符。它们可以包含数字以及大小写字母混合。如果您决定不更改 root 密码，只需点击 `Cancel`。一旦输入了新密码，请选择 `Accept`。更改立即生效，不仅适用于登录 root，也适用于使用 `su` 命令变为 root。

# 8.1 使用 Linux 进行系统配置

![](img/6f1d66e9f0dd8a64781e93022eb9e8cc_146_0.png)

图 8.7：root 密码验证界面

# 禁用用户账户 – 快速参考

1. 在 shell 提示符输入 `linuxconf` 启动 `Linuxconf`。
2. 打开 `Config` -> `Users accounts` -> `Normal` -> `User accounts`
3. 选择账户。
4. 取消勾选 `account is enabled`（账户已启用）复选框。
5. 选择 `Accept`（接受）。

# 禁用用户账户 – 概述

为什么要禁用账户？问得好！没有单一的答案，但我们可以提供提供此选项的原因。最大的原因是安全。例如，您可能创建了一个特殊账户，供客户、同事或朋友访问系统上的特定文件。该账户偶尔会被使用，但应该只在知道有需要时才使用。留下一个未使用的账户会成为想要入侵您系统的人的目标。

删除它需要您……

要禁用账户：

- 在 shell 提示符输入 `linuxconf` 启动 `Linuxconf`。
- 打开 `Config` -> `Users accounts` -> `Normal` -> `User accounts`
- 选择账户。
- 取消勾选 `account is enabled`（账户已启用）复选框。
