
```
### cat /etc/shadow
root:$64:Gra4hiWU1nkSgAbCEBNFThzAc.GaQTUZXYR/djbhoVwZexxkN
AIVIy51Yq5LGwFd3fQt68jMyUagI.Rp3WcapabyFyIs:15368:099999:7:
bin*:15155:099999:7:
daemon*:15155:099999:7:
adm*:15155:099999:7:
lp*:15155:099999:7:
sync*:15155:099999:7:
shutdown*:15155:099999:7:
halt*:15155:099999:7:
mail*:15155:099999:7:
uuc*:15155:099999:7:
gdm::15368:
sshd::15368:
tctdpump::15368:
linda$S6TKN8U1tQvjoo4k$U9fF9ByhINORrbqS15Hv6JR5b75V8kkb06Mqrq
uwSFEfYjwl1XcnkTepPycw6b8.v6/noLKBCAL9KL9::15368:099999:7:
geme::15424:
```

与 `/etc/passwd` 一样，`/etc/shadow` 中的行也存储在不同的字段中。对于大多数管理员来说，前两个字段是最重要的。第一个字段用于存储用户名，第二个字段用于存储加密密码。

在加密密码字段中，使用了 `!` 和 `*`。如果使用了 `!`，则禁用了登录功能。如果使用了 `*`，则它是一个用于启动服务的系统账户，不允许交互式 shell 登录。此外，请注意，默认情况下，那里存储了加密密码，但也有可能存在

## 管理用户和用户组

以下是 `/etc/shadow` 文件的行中使用的字段：

- 登录名
- 加密密码
- 自 1970 年 1 月 1 日以来密码最后一次更改的天数
- 密码必须更改的天数
- 密码更改后允许保留的天数
- 密码过期前提醒用户的天数
- 密码过期后禁用该账户的天数
- 自 1970 年 1 月 1 日以来该账户禁用的天数
- 预留字段，未使用

### /etc/login.defs

`/login.defs` 是一个与用户环境相关的配置文件，但完全在后台运行。该文件中定义了一些通用设置。这些设置决定了与创建用户相关的所有信息。在 `login.defs` 中，你会发现变量。这些变量指定了创建用户时使用的默认值。列表 7.4 显示了该配置文件的部分。

**列表 7-4：** `login.defs` 包含了用户在被创建时所拥有的变量。

```
# 它应该删除任何属于被删除用户的 at/cron/print 任务等
# （要删除的用户将作为第一个参数传递）。
#
#USERDEL_CMD /usr/sbin/userdel_local
#
# 如果默认为用户创建家目录
# 在 RH 系统上，我们是这么的。此选项可以通过用户命令行上的 -m 标志覆盖。
#
CREATE_HOME yes
# 权限掩码初始化为此值。如果未指定，
# 权限掩码将初始化为 022。
UMASK 077
#
# 这允许 userdel 在没有成员的情况下删除用户组。
#
USERGROUPS_ENAB yes
# 使用 SHA512 加密密码。
ENCRYPT_METHOD SHA512
```

现在你已经了解了参与用户管理的所有要素，在练习 7.1 中，你将创建一些用户账户。

### 练习 7.1

#### 创建用户

在本次练习中，你将学习如何创建用户账户。你还将看到这些用户账户是如何写入相关的配置文件的。

1. 打开一个 root shell，并使用命令 `useradd lisa`。
2. 使用命令 `su - lisa`。这打开了一个你以用户 lisa 登录的 shell。该命令还会带你进入家目录。你可以使用 `pwd` 来验证这一点。
3. 使用 `exit` 关闭用户 lisa 所在的 shell。
4. 使用编辑器打开 `/etc/login.defs` 文件。找到变量 `CREATE_HOME` 并将其值改为 `no`。关闭文件并保存更改。
5. 仍以 root 身份，使用命令 `useradd lisa` 创建用户 lisa。
6. 使用 `su lisa` 打开一个用户 lisa 的子 shell。你将收到一条错误消息，显示 lisa 没有家目录。
7. 关闭 lisa 的子 shell，并以 root 身份使用 `cat /etc/passwd` 查看用户 lisa 和 l 是如何定义的。
8. 使用 `userdel lisa` 从你的系统中删除 lisa。
9. 将 `/etc/login.defs` 中的 `CREATE_HOME` 变量恢复为其原始值。
10. 再次创建用户 lisa。此时，你应该有三个用户：linda、lisa 和 kori。
11. 以 root 身份，使用 `passwd` 命令为这三个用户中的每一个设置密码。

#### 创建组

正如你已经学到的，所有用户都需要组成员身份。你读过关于主组和其他组之间的区别；然而，你还没有学习如何创建组。

## 使用图形化工具进行用户和组管理

到为止，你仅使用命令行工具进行用户和组管理。Red Hat Enterprise Linux 提供了 system-config 工具，作为命令行工具的图形化解决方案替代方案。对于用户和组管理，该工具的名称为 `system-config-users`。你可以在图 7.1 中看到该工具界面。

**图 7.1** `system-config-users` 为用户和组管理提供了一个方便的界面。

![](img/17f0db741e978e043c6f38c58e661452_230_0.png)

开发 `system-config-users` 工具是为了简化用户和组的管理。要创建新用户，请点击“Add User”（添加用户）。这将打开“Add New User”（添加新用户）窗口，你可以在其中指定创建新用户所需的所有属性。添加新组也很。只需点击“Add Group”（添加组），就会看到一个窗口，提示你添加新组所需的所有属性，如图 7.2 所示。

**图 7.2** 要添加新用户，只需在“Add New”（添加新）窗口中输入所有所需的属性。

![](img/17f0db741e978e043c6f38c58e661452_231_0.png)

创建用户或组后，你可以选择它来设置主界面未显示的属性。只需点击该用户，并在屏幕顶栏中点击“Properties”（属性）。你会看到一个包含四个标签页的窗口，你在其中输入了用户所需的所有属性。

你可以在“User Data”（用户数据）标签页上更改创建用户时输入的属性。如果你想启用账户过期，请选择“Account Info”（账户信息），并设置账户过期日期…………你可以在“Groups”（组）标签页上管理用户的辅助组成员。在图 7.3 中，你可以看到如何使用 `system-configs` 更改用户属性。

**图 7.3** 在 `system-configs` 中更改用户属性

![](img/17f0db741e978e043c6f38c58e661452_231_1.png)

## 使用外部身份验证源

Red Hat Enterprise Linux 的默认安装使用了 `/etc/passwd` 和 `/etc/shadow` 中的本地用户数据库。在企业环境中，可能会使用外部身份验证源，例如 LDAP 目录服务器或网络上 Windows 服务器提供的 Active Directory 服务。要配置你的服务器使用这些源，你可以使用 `system-config-authentication` 工具或使用 `authconfig` 作为替代方案。启动 `system-config-authentication` 工具后，你会看到两个标签页。在“Identity & Authentication”（身份与身份验证）标签页上，你可以指定如何进行身份验证。默认情况下，该工具设置为使用本地账户作为用户账户数据库。在“Advanced Options”（高级选项）标签页上，你可以启用高级身份验证方法，例如使用指纹识别器（见图 7.4）。

**图 7.4** 启用高级身份验证选项

![](img/17f0db741e978e043c6f38c58e661452_232_0.png)

如果网络使用了外部身份验证源，可以通过“Identity & Authentication”标签页上的“User Account Database”（用户账户数据库）下拉列表进行选择。默认提供四个选项：

- **Local Accounts Only (仅本地账户)** 使用此选项使用 `/etc/passwd` 和 `/etc/shadow` 中的本地用户数据库。
- **LDAP**：此选项允许使用外部 LDAP 目录服务器登录。
- **NIS**：在旧的 UNIX 环境中，NIS 可能被用身份验证服务。使用它连接到 NIS 身份验证服务。
- **Winbind**：此选项允许你在 Windows 网络上进行身份验证。
