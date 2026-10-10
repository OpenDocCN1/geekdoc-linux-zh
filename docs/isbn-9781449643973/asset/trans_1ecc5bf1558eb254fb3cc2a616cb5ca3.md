
### 密码老化控制：

```text
#
#    PASS MAX DAYS  密码最大使用天数。
#    PASS MIN DAYS  两次修改密码之间允许的最小天数。
#    PASS MIN LEN   可接受的最小密码长度。
#    PASS WARN AGE  密码过期前发出警告的天数。
#
PASS_MAX_DAYS 60
PASS_MIN_DAYS 0
PASS_MIN_LEN 8
PASS_WARN_AGE 14
```

![](img/73be0eef2ceb12f43f3eb92c420134f5_33_0.png)

- 10. 保存更改并退出文件。按 `escape` 键退出插入模式，然后按“shift”键和“:”键进入命令模式。在命令模式的冒号提示符处，输入 `wq` 以退出并保存更改。

### 创建用户账户、登录凭据并定义组

- 11. 为管理员创建四个用户账户。两个账户供数据库管理员使用，两个账户供 Web 管理员使用。提供以下 `user` 名称：dbadmin1, dbadmin2, webadmin1 & webadmin2。使用 `useradd` 命令创建账户：
    - a) 输入命令：`su -c 'useradd dbadmin1'` 并按 `<enter>`。
    - b) 密码：`ISS316Security`
    - c) 输入命令：`su -c 'useradd dbadmin2'` 并按 `<enter>`。
    - d) 密码：`ISS316Security`
    - e) 输入命令：`su -c 'useradd webadmin1'` 并按 `<enter>`。
    - f) 密码：`ISS316Security`
    - g) 输入命令：`su -c 'useradd webadmin2'` 并按 `<enter>`。
    - h) 密码：`ISS316Security`

- 12. 为每个创建的账户设置密码：`passwd` (账户名称)。

**注意：** 如果选择了弱密码，将显示警告消息。然而，由于该命令是以 root 权限运行的，因此允许使用弱密码。

- 13. 输入命令：`su -c 'passwd dbadmin1'` 并按 <enter>。
- 14. 密码：ISS316$Security
- 15. 系统将提示输入 dbadmin 的新密码。输入密码：lab3 并按 <enter>
- 16. 再次输入密码 lab3 以确认。按 enter 键完成。

```text
[student@TargetFedora01 ~]$ su -c 'useradd dbadmin1'
Password:
[student@TargetFedora01 ~]$ su -c 'passwd dbadmin1'
Password:
Changing password for user dbadmin1.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

**图 15 – 添加用户账户并设置密码**

- 17. 强制每个用户在首次登录时更改密码。
    - a) 输入命令：`su -c 'chage -d 0 dbadmin1'` 并按 <enter>。
    - b) 密码：ISS316$Security
    - c) 输入命令：`su -c 'chage -d 0 dbadmin2'` 并按 <enter>。
    - d) 密码：ISS316$Security
    - e) 输入命令：`su -c 'chage -d 0 webadmin1'` 并按 <enter>。
    - f) 密码：ISS316$Security
    - g) 输入命令：`su -c 'chage -d 0 webadmin2'` 并按 <enter>。
    - h) 密码：ISS316$Security

**注意：** `-d` 后面应该是数字零，而不是字母 `o`。

- 18. 创建两个组账户，一个名为 `dba`，另一个名为 `web`。
    - a) 输入命令：`su -c 'groupadd dba'` 并按 <enter>。
    - b) 密码：ISS316$Security
    - c) 输入命令：`su -c 'groupadd web'` 并按 <enter>。

```text
[student@TargetFedora01 ~]$ su -c 'groupadd dba'
Password:
[student@TargetFedora01 ~]$ su -c 'groupadd web'
Password:
```

**图 16 — 添加组**

- 19. 将用户 `dbadmin1` 和 `dbadmin2` 添加到“dba”组中。
    - a) 输入命令：`su -c 'usermod -G dba dbadmin1'` 并按 <enter>。
    - b) 密码：ISS316Security
    - c) 输入命令：`su -c 'usermod -G dba dbadmin2'` 并按 <enter>。
    - d) 密码：ISS316Security
- 20. 将用户 `webadmin1` 和 `webadmin2` 添加到“web”组中。
- 21. 输入命令：`su -c 'usermod -G web webadmin1'` 并按 <enter>。
- 22. 密码：ISS316Security
- 23. 输入相同的命令：`su -c 'usermod -G web webadmin2'` 并按 <enter>。
- 24. 密码：ISS316Security

### 将学生账户添加到 Wheel 组

- 25. 将学生用户账户添加到“wheel”组中。
- 26. 输入命令：`su -c 'usermod -G wheel student'` 并按 <enter>。
- 27. 密码：ISS316Security

> **注意：** *学生必须是 wheel 组的成员，才能执行 Labs 3 - 10 中的 su 和 sudo 命令。*

```text
[student@TargetFedora01 ~]$ su -c 'usermod -G wheel student'
Password:
```

**图 17 — 将学生添加到 wheel 组**

### 创建临时用户账户并设置 90 天后自动过期

Jane Temp 是一名承包商，协助构建为期 90 天的 Linux 在线备份基础设施。

- 28. 创建临时用户账户名称。输入命令：`su -c 'useradd jtemp'` 并按 <enter>。
- 29. 密码：ISS316Security
- 30. 为临时用户设置密码。输入命令：`su -c 'passwd jtemp'` 并按 <enter>。
- 31. 密码：ISS316Security
- 32. 确保用户在首次登录时被迫更改密码。输入命令：`su -c 'chage -d 0 jtemp'` 并按 <enter>。
- 33. 密码：ISS316Security

**注意：** `-d` 后面是数字零。不是字母 o。

```text
[student@TargetFedora01 ~]$ su -c 'useradd jtemp'
Password:
[student@TargetFedora01 ~]$ su -c 'passwd jtemp'
Password:
Changing password for user jtemp.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
[student@TargetFedora01 ~]$ su -c 'chage -d 0 jtemp'
Password:
```

![](img/73be0eef2ceb12f43f3eb92c420134f5_36_0.png)

- 34. 设置账户在 90 天后过期。输入命令：`su -c 'chage -E 2011-12-31 jtemp'` 并按 <enter>。当系统提示时，输入 root 的密码 (ISS316Security)。

**注意：** 将命令中的日期替换为实验室当天起 90 天后的日期。如果 2011-12-31 是较早的日期，用户账户将立即过期！日期格式为 YYYY-MM-DD。例如，如果希望的过期日期是 2011 年的最后一天，则如上图所示输入命令。

```text
[student@TargetFedora01 ~]$ su -c 'chage -E 2011-12-31 jtemp'
Password:
[student@TargetFedora01 ~]$ su -c ' chage --list jtemp'
Password:
Last password change                : password must be changed
Password expires                    : password must be changed
Password inactive                   : password must be changed
Account expires                     : Dec 31, 2011
Minimum number of days between password change    : 0
Maximum number of days between password change    : 60
Number of days of warning before password expires : 14
[student@TargetFedora01 ~]$ 
```

![](img/73be0eef2ceb12f43f3eb92c420134f5_37_0.png)

> **重要：** 在完成本实验的最后一项任务之前，学生账户应当是“wheel”组的成员，如本实验第 14 步所述（Lab 3）。否则将导致学生用户账户无法使用未来的任何 ‘su -c’ 或 sudo 命令！

### 限制 su 命令的使用

- 35. 打开 /etc/pam.d/su 进行编辑。输入命令：`su -c 'vi /etc/pam.d/su'` 并按 `<enter>`。
- 36. 密码：ISS316Security
- 37. 按“i”键进入 INSERT（插入）模式。
- 38. 找到行：“#auth required pam_wheel.so use_uid”。
- 39. 删除行开头的井号（#）。将光标定位在 # 上并按“x”键。

```bash
##PAM-1.0
auth     sufficient    pam_rootok.so
# Uncomment the following line to implicitly trust users in the "wheel" group.
#auth    sufficient    pam_wheel.so trust use_uid
# Uncomment the following line to require a user to be in the "wheel" group.
auth     required      pam_wheel.so use_uid
auth     include       system-auth
account  sufficient    pam_succeed_if.so uid = 0 use_uid quiet
account  include       system-auth
password include       system-auth
session  include       system-auth
session  optional      pam_xauth.so
```

**图 20 – 限制 su 命令的使用**

- 40. 保存更改并退出文件。按 escape 键退出 INSERT（插入）模式，然后按“shift”键和":”键进入命令模式。在命令模式的冒号提示符处，输入 wq 以退出并保存更改。

### 交付物

完成实验 #3：应用加固的用户账户管理与安全控制后，学生需要提供以下交付物：

- 1. 实验 #3 - 学生需提交以下文件的截图：
    - a. /etc/login.defs 文件的输出
    - b. “groups” 命令的输出
    - c. 新修改的 /etc/pam.d/su 文件的输出
- 2. 实验 #3 – 实验评估问题及答案

### 评估标准和评分细则

以下是学生必须完成的实验 #3 的评估标准和评分细则：

- 1. 学生是否能够通过编辑 /etc/login.defs 文件并在 Fedora Linux 服务器上实施严格的密码安全措施来配置密码策略？– [20%]
- 2. 学生是否能够强制执行每 60 天更改一次密码，并在密码过期前 14 天向系统内所有用户发出警告？– [20%]
- 3. 学生是否能够将最小密码长度配置为 8 个字符并满足严格的复杂性要求？– [20%]
