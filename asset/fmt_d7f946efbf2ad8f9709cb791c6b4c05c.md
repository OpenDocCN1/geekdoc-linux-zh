
以下命令选项不是扩展选项，也不会设置默认特性。这些账户特性也可以使用 ASU 工具创建。在添加新账户时，使用这些命令选项：

- `pc_username=name_string`  
  Windows NT 域中的用户账户名。该名称可以与用户的 UNIX 账户名相同，也可以不同。
- `pc_unix_username=login_name`  
  同步的 UNIX 账户名。如果没有输入名称，则与 Windows NT 域账户名相同。
- `pc_fullname=text_string`  
  用户的全名或账户的描述。
- `pc_comment=text_string`  
  账户的简短描述，只能由管理员更改。
- `pc_usercomment=text_string`  
  账户的简短描述。用户可以更改。
- `pc_homedir=pathname`  
  用户主目录的路径，指定为 Windows NT 共享格式。
- `pc_primary_group=group`  
  用户所属的主组（Windows NT 域）。
- `pc_secondary_groups=group,group...`  
  用户所属的次级 NT 域。该值以逗号分隔列表的形式指定。
- `pc_logon_workstations=client_name`  
  用户可以登录的客户端主机系统列表。该值以逗号分隔列表的形式指定。空值（`" "`）表示用户可以从所有工作站登录。
- `pc_logon_script=pathname`  
  默认登录脚本所在的目录。（此目录在 ASU 配置期间创建。）
- `pc_account_type=local|global`  
  指定账户在 Windows NT 域中是本地账户还是全局账户。
- `pc_account_expiration=date_string`  
  指定账户过期并防止登录的日期。
- `pc_logon_hours=Dd0000-0000,Dd0000-...`  
  指定登录过期以及允许或拒绝登录的天数和小时。
- `pc_user_profile_path=pathname`  
  指定默认用户配置文件目录的路径。
- `pc_disable_account=0|1`  
  指定账户初始是否锁定（即禁用登录）。
- `pc_passwd=0|1`  
  作为初始账户密码的文本。你必须在此选项之前加上`-x`标志，系统会提示你输入密码，然后确认输入。密码不会显示在屏幕上。
- `pc_passwd_choose_one=0|1`  
  控制用户是否可以自行密码。
- `pc_passwd_change_required=0|1`  
  强制用户在首次登录时更改密码。
- `userdel` - 你可以使用此命令的唯一支持 PC (Windows NT 域) 选项是同步 UNIX/PC 账户。  
  使用此选项同步账户，如下所示：

  ```bash
  # userdel -r -x pc_synchronize=1 studentB
  ```

- `groupadd`, `groupmod`  
  可以使用`-x`标志配合以下扩展来管理 Windows NT 域中的组：
  - `pc_group_description=string`  
    指定提供组描述的文本。
  - `pc_group_members=user,user....`  
    指定组成员的逗号分隔列表。

使用命令行的优势是它对管理任务提供了完全的控制，允许你指定任何和所有命令选项并覆盖默认的账户环境变量。

命令可以作为脚本的一部分来自定义和自动化账户创建。然而，命令选项可能很长，因此使用图形界面工具设置账户通常更方便。

请参`useradd(8)`和`groupadd(8)`以及其中相关的参考页面。

## 7.6.1.4 使用 ASU User Manager 管理域

ASU 提供了用于管理 NT 域、域用户和组的工具。此应用程序必须安装在运行 Windows NT 的系统上，并且只能从该系统使用。它提供了与 `net` 命令行相同的功能。

你可以为所有新创建的账户指定默认环境变量。这些环境变量在 Windows NT 域中被称为账户策略。你无法使用 User Manager for Domains (`usrmgr.exe`) 为同步的 UNIX 账户设置默认环境变量。

请参《ASU 安装与管理指南》和在线 User Manager for Domains 以获取更多信息。

## 7.6.1.5 使用 ASU net 命令

ASU 提供了一套广泛的 `net` 命令，你可以在 UNIX 命令行或从 Windows 服务器上的 DOS 窗口中输入。

例如，以下命令显示 `net user` 的帮助信息，这是你用于添加、修改或删除用户账户的命令：

```bash
# help user | more
```

该命令的语法为：

```text
NET USER [username [password | \* [options]]

username [password | /]/ADD [options]

username [/DELETE]
```

```bash
# net user josef /add
```

以下命令显示用户列表：

```bash
# net user
```
