
`-M 30` 选项告诉系统每 30 天过期 Mary 的密码。`-d 0` 选项欺骗系统认为她的密码从 1 月以来还没有更改过。

## 修改账户

偶尔，用户需要的不仅仅是密码。`usermod` 命令与 `useradd` 命令类似，它不是添加新账户，而是允许你更改各种细节。

### 表 11-3：更改账户的 usermod 选项

| 选项 | 描述 |
| :--- | :--- |
| `-c "comment"` | 账户的描述字段。用文字替换 `comment`。 |
| `-d home_dir` | 将用户的家目录更改为指定位置。用路径替换 `home_dir`。 |
| `-e expire_date` | 为账户分配新的过期日期，用 `MM/DD/YYYY` 替换 `expire_date`。 |
| `-f inactivity` | 设置密码过期后永久禁用的天数。设置为 `-1` 则禁用该选项，这是默认值。 |
| `-g group` | 更改所属的主组（如 `/etc/group` 文件所示）。用新组名替换 `group`。 |
| `-G grouplist` | 设置用户所属的组列表。用组列表替换 `grouplist`。 |
| `-l login_name` | 将账户名称改为 `-l` 之后的名称。用新名称替换 `login_name`。这不会自动更改家目录，请使用 `-d` 和 `-m` 选项。 |
| `-m` | 此选项仅与 `-d` 选项配合。它导致用户家目录的内容复制到新目录。 |
| `-o` | 此选项仅与 `-u` 选项配合。它消除了 `userID` 必须唯一的限制。 |
| `-u user_id` | 更改账户的用户 ID。用新 ID 替换 `user_id`。除非使用 `-o` 选项，否则该 ID 不能被另一个账户使用。 |
| `-s shell` | 为账户指定一个新的 `shell`。用 `shell` 的完整路径替换 `shell`。 |

假设新员工 Jenny Barnes 将接 Mary 的工作。我们要把 `mary` 账户转换为新名称 `-l jenny`、新注释 `-c "Jenny Barnes"` 和家目录 `-d /home/jenny`。你可以通过以下命令实现：

```
# usermod -l jenny -c "Jenny Barnes" -m -d /home/jenny mary
```

此外，如果转换账户后发现 Jenny 偏好使用 `tcsh` shell，你可以通过 `-s /bin/tcsh` 进行此更改：

```
# usermod -s /bin/tcsh jenny
```

相反，你可以使用 `chsh` 命令来更改 `shell`。以下是一个示例：

## 第 11 章：设置与支持用户 483

```
$ chsh -s /bin/bash jenny
```
`chsh` 命令非常实用，因为它允许普通用户将其 `shell` 设置更改为 `/etc/shells` 中列出的任何 `shell`。`root` 用户可以将其自己的 `shell` 更改为他选择的任何命令。在调用该命令时，只需留空用户名参数，`chsh` 就会假设当前登录的用户为要更改的账户。

用户还可以使用 `chfn` 命令更改其用户信息。这些信息存储在 `/etc/passwd` 文件中，并在你输入 `chfn` 命令时（例如 `chfn jenny`）显示出来。在本示例中，全名、办公室名称、办公室、家庭和工作电话均由用户设置：

```
$ chfn -f "J Smith" -o "A-111" -s 555-1212 -h 555-2323 jenny
```

用户还可以向其目录下的 `.plan`、`.project`、`.forward` 和 `.pgpgkey` 文件添加关于自己的信息。这些信息随后将被 `finger` 命令读取。

## 使用用户管理器（User Manager）修改用户账户

要使用桌面环境更改现有账户，你可以使用用户管理器。以下是如何从用户管理器窗口添加新用户的方法：

- 1. 选择 系统 → 管理（Administration）→ 用户和组（或以 `root` 用户身份从终端窗口输入 `system-config`）。出现用户管理器主窗口。
- 2. 选择要修改的账户用户名，然后点击“属性”（Properties）按钮打开用户属性窗口（见图 11-3）。
- 3. 对于你所选的用户，有四个可以修改的信息选项卡：
    - 用户数据（User Data）：此选项卡包含你在首次添加用户账户时创建的信息。
    - 账户信息（Account Info）：如果你希望账户在特定日期后无法访问，请勾选“启用账户过期”（Enable Account Expiration）复选框并输入日期。如果你想防止访问账户但不删除它，请勾选“本地密码锁定”（Local Password is Locked）复选框。（当员工离开公司或你想锁定一个临时禁用的客户账户时，这是一种很好的技术。信息不会被删除，只是无法访问。）

## 第三部分：管理 Fedora 和 RHEL

![](img/74f214fbb2938b570bec5f957507ac66_517_0.png)

- **密码信息（Password Info）** 如果你想控制用户密码的过期，请勾选“启用密码过期”（Enable Password Expiration）。默认情况下，密码不过。以下是你的选项：“允许更改的天数”（Days before change allowed，强制用户在更改密码前至少保留指定天数）；“要求更改的天数”（Days before change required，允许用户至少保留相同密码指定天数）；“更改前的警告天数”（Days before warning change，设置在密码过期前几天提醒用户更改密码）；“账户闲置的天数”（Days before account inactive，设置账户在多少天后停用）。
- **组（Groups）**：从可用组列表中选择，将用户添加到一个或多个组中。
- 点击“确定”将更改应用于用户账户。

## 删除用户账户

有时，需要从你的 Linux 系统中删除用户账户。这可以通过 `userdel` 命令或用户管理器窗口完成。

### 使用 userdel 删除用户账户

`userdel` 命令接受单个参数，即要删除的账户名称。如果你提供了可选的 `-r` 选项，它还会删除用户的家目录以及其中所有的文件。要删除登录名为 `mary` 的用户账户，你需要输入：

```
# userdel mary
```

要彻底删除她的家目录以及账户，请输入：

```
# userdel -r mary
```
