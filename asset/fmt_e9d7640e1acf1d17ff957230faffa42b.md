
- **默认主目录（Default Home）。** 输入或浏览到新用户主目录的初始路径前缀。用户名将附加在该该值的末尾，以创建用户主目录的默认名称。
- **骨架目录（Skeleton Directory）。** 输入或浏览到骨架目录。当添加新用户时，该目录的内容将复制到用户目录中。
- **默认过期日期（Default Expiration Date）。** 输入用户账户禁用的日期。格式必须为 `YYYY-MM-DD`。如果该账户永不过期，请留空此字段。
- **密码过期后可用天数（Days after Password Expiration Login Is Usable）。** 此设置允许用户在密码过期后登录。设置密码过期后允许登录的天数。输入 `-1` 表示无限访问。

选择 `下一步（Next）` > `完成（Finish）` 以保存配置设置。这些值将被写入文件 `/etc/default/useradd`。

```
da10:-# cat /etc/default/useradd
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
GROUPS=video,dialout
CREATE_MAIL_S=no
```

你也可以使用命令行程序 `useradd` 来查看或更改默认值。`--show-defaults` 选项显示与上述 `cat` 相同的内容。`save-defaults` 选项后跟带有值的选项可以更改它们：

```
dal0: # useradd --save-defaults -d /export/home
dalo0: # useradd --show-defaults
GROUP=100
HOME=/export/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
GROUPS=video,dialout
CREATE_MAIL_SPOOL=no
```

`useradd` 的手册页列出了所有可能的选项。

# 配置安全设置

YaST 提供了一个本地安全（Local Security）模块，允许你为 SUSE Linux Enterprise Server 配置以下本地安全设置：

- 密码设置
- 启动配置
- 登录设置
- 用户创建设置
- 文件权限

你可以从三个预设的安全级别中选择（或修改），或者创建自己的自定义安全设置以满足你企业安全策略和程序的要求。

你可以通过在 YaST 控制中心选择 安全与用户（Security and Users） > 本地安全（Local Security），或者在终端窗口中输入 `root yast2 security` 来访问安全设置模块。

## 显示如下：

### 图 3-5

![](img/84d12236ddfe17cc29fd21173b9904ac_178_0.png)

从此对话框中，你可以选择以下预设配置之一：

- **家庭工作站（Home Workstation）。** 适用于未连接任何类型网络的家庭计算机。此选项代表最低级别的本地安全。
- **网络化工作站（Networked Workstation）。** 适用于连接到任何类型网络或互联网的计算机。此选项提供中间级别的本地安全。
- **网络服务器（Network Server）。** 适用于提供任何类型服务（网络或其他）的计算机。此选项启用了高级别的本地安全。
- 你也可以选择**详情（Details）**或**自定义设置（Custom Settings）**来修改现有的安全级别或创建自己的配置。

# SUSE Linux Enterprise Server 10 管理

通过选择三个预定义安全级别之一并选择**下一步（Next）**，将应用所选的安全级别。通过**详情（Details）**，你可以更改所选安全级别的设置。

如果你选择**自定义设置（Customs Settings）**然后选择**下一步（Next）**，你可以直接更改安全配置的细节。

详细设置的对话框对于每个安全级别看起来都是相同的，但预选选项不同。在以下对话框中，你看到的是第 3 级（网络服务器）的设置。

在第一个对话框中，你可以更改系统接受的默认密码要求：

## 图 3-6

![](img/84d12236ddfe17cc29fd21173b9904ac_179_0.png)

从此对话框中，你可以选择或输入以下密码设置（主要存储在 `/etc/login.defs` 中，某些值在 `/etc/default/passwd` 和 `/etc/security/pam_pwcheck.conf` 中）：

- **检查新密码（Check New Passwords）。** 选择一个不容易猜的密码很重要。
- **测试复杂密码（Test for Complicated Passwords）。** 密码应使用大写字母、小写字母以及数字的混合。
- **加密方法（Encryption Method）。** 从下拉列表中选择之一：
    - DES。这是最低级别。
    - MD5。它在所有当前的发行版中有效。
    - Blowfish。该方法使用 blowfish 算法加密密码。被许多系统使用。
- **最小接受密码长度（Minimum Acceptable Password Length）。** 输入可接受密码的最小字符数。输入 `0` 可禁用此检查。
- **密码年龄（Password Age）。** 最小是指更改密码前必须经过的天数。最大是指密码过期后的天数。
- **密码过期前天数（Days Before Password Warning）。** 在密码过期前若干天数向用户发出警告。

当你完成密码设置后，选择**下一步（Next）**继续。显示如下：

## 图 3-7

![](img/84d12236ddfe17cc29fd21173b9904ac_181_0.png)

从此对话框中，你可以选择以下启动设置（这将更新 `/etc/inittab`）：

- **Ctrl + Alt + Del 的解释（Interpretation of Ctrl + Alt + Del）。** 有时你希望系统忽略组合键，特别是当系统兼工作站和服务器时。按下 Ctrl+Alt+Del 组合键时什么都不会发生。
- **重启（Reboot）。** 按 Ctrl+Alt+Del 组合键时系统重启。
- **停机（Halt）。** 按 Ctrl+Alt+Del 组合键时系统关机。
- **KDM 的关机行为（Shutdown Behavior of KDM）。** 你使用此选项设置谁允许从 KDM 关机：
    - 仅限 root（Only Root）。要关机必须输入 root 密码。
    - 所有用户（All Users）。所有人（包括远程连接的用户）都可以通过 KDM 关机。
    - 无人（Nobody）。没有人能通过 KDM 关机。
    - 本地用户（Local Users）。只有本地连接的用户可以通过 KDM 关机。
    - 自动（Automatic）。系统在注销后自动关机。

# SUSE Linux Enterprise Server 10 管理

当你完成启动设置配置后，继续点击**下一步**。出现以下内容：

## 图 3-8

![](img/84d12236ddfe17cc29fd21173b9904ac_183_0.png)

在此对话框中，你可以输入并选择以下登录设置（主要存储在 `/etc/login.defs`）：

- **登录尝试失败后的延迟（Delay After Incorrect Login Attempt）。** 在登录失败后，通常会有几秒钟的等待才能再次登录。这使得密码破解程序登录变得更加困难。
此选项允许你调整再次尝试登录之前的时间延迟。默认值为 3 秒，这是一个合理的值。
- **记录成功登录尝试（Record Successful Login Attempts）。** 记录成功的登录尝试非常有用，特别是在警告系统发生了未经授权的访问时（例如用户从非正常位置登录）。
选择此选项将成功的登录尝试记录在 `/var/log/wtmp` 文件中。你可以使用 `last` 命令查看谁在什么时间登录过。
- **允许远程图形登录（Allow Remote Graphical Login）。** 你可以选择此选项，允许其他用户通过网络访问你的图形登录界面。
由于此类访问代表了潜在的安全风险，它默认是禁用状态。

当你完成登录设置配置后，继续点击**下一步**。出现以下内容：

## 图 3-9

![](img/84d12236ddfe17cc29fd21173b9904ac_184_0.png)

在此对话框中，你可以输入以下 ID 设置（存储在 `/etc/login.defs`）：

- **用户 ID 限制（User ID Limitations）。** 输入一个最小值和一个最大值以配置可能的用户 ID 数字范围。新用户将获得此范围内的一个 UID。
- **组 ID 限制（Group ID Limitations）。** 输入一个最小值和一个最大值以配置可能的组 ID 数字范围。
