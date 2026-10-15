
## 3. 启用你的 DOS 命令提示符，输入“`ipconfig`”，并“`ping`”你分配的 IP 主机地址 `172.30.0.____`，DHCP 服务器 `172.30.0.10`，以及 IP 默认网关路由器 `172.30.0.1`

## 4. 使用以下凭据登录学生 VM

- 登录 ID：`student`（区分大小写）
- 密码：`ISS316Security`（区分大小写）

## 5. 在 GNOME 桌面上，在左上角，单击“Applications” -> Systems Tools -> Terminal

![](img/73be0eef2ceb12f43f3eb92c420134f5_32_0.png)

### 根据策略要求配置严格密码

## 6. 打开并编辑 `/etc/login.defs` 文件以强制执行

- a. 每 60 天更改一次密码
- b. 在密码过期前 14 天显示警告
- c. 要求最小密码长度为 8 个字符

输入命令：`su -c 'vi /etc/login.defs'` 并按 `<enter>`。

## 7. 密码：`ISS316Security`

```bash
[student@TargetFedora01 ~]$ su -c 'vi /etc/login.defs'
Password: 
```

**图 13 – 以 root 用户身份在 vi 中打开文件**

## 8. 按“ i ”进入 vi 编辑器中的 **INSERT**（插入）模式。

## 9. 更改如下图中所示的密码老化控制

### 密码老化控制

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

## 10. 保存更改并退出文件。按 `escape` 键退出插入模式，然后按“shift”键和“:”键进入命令模式。在命令模式的冒号提示符处，输入 `wq` 以退出并保存更改。

#### 创建用户账户、登录凭据并定义组

## 11. 为管理员创建四个用户账户。两个账户供数据库管理员使用，两个账户供 Web 管理员使用。提供以下 `user` 名称：`dbadmin1`, `dbadmin2`, `webadmin1` & `webadmin2`。使用 `useradd` 命令创建账户

- a) 输入命令：`su -c 'useradd dbadmin1'` 并按 `<enter>`。
- b) 密码：`ISS316Security`
- c) 输入命令：`su -c 'useradd dbadmin2'` 并按 `<enter>`。
- d) 密码：`ISS316Security`
- e) 输入命令：`su -c 'useradd webadmin1'` 并按 `<enter>`。
- f) 密码：`ISS316Security`
- g) 输入命令：`su -c 'useradd webadmin2'` 并按 `<enter>`。
- h) 密码：`ISS316Security`

## 12. 为每个创建的账户设置密码：`passwd` (账户名称)。

**注意：** 如果选择了弱密码，将显示警告消息。然而，由于该命令是以 root 权限运行的，因此允许使用弱密码。

## 13. 输入命令：`su -c 'passwd dbadmin1'` 并按 `<enter>`。

## 14. 密码：`ISS316$Security`

## 15. 系统将提示输入 dbadmin 的新密码。输入密码：`lab3` 并按 `<enter>`

## 16. 再次输入密码 `lab3` 以确认。按 `enter` 键完成。

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

## 17. 强制每个用户在首次登录时更改密码

- a) 输入命令：`su -c 'chage -d 0 dbadmin1'` 并按 `<enter>`。
- b) 密码：`ISS316$Security`
- c) 输入命令：`su -c 'chage -d 0 dbadmin2'` 并按 `<enter>`。
- d) 密码：`ISS316$Security`
- e) 输入命令：`su -c 'chage -d 0 webadmin1'` 并按 `<enter>`。
- f) 密码：`ISS316$Security`
- g) 输入命令：`su -c 'chage -d 0 webadmin2'` 并按 `<enter>`。
- h) 密码：`ISS316$Security`

**注意：** `-d` 后面应该是数字零，而不是字母 `o`。

## 18. 创建两个组账户，一个名为 `dba`，另一个名为 `web`

- a) 输入命令：`su -c 'groupadd dba'` 并按 `<enter>`。
- b) 密码：`ISS316$Security`
- c) 输入命令：`su -c 'groupadd web'` 并按 `<enter>`

```text
[student@TargetFedora01 ~]$ su -c 'groupadd dba'
Password:
[student@TargetFedora01 ~]$ su -c 'groupadd web'
Password:
```

**图 16 — 添加组**

## 19. 将用户 `dbadmin1` 和 `dbadmin2` 添加到“dba”组中

- a) 输入命令：`su -c 'usermod -G dba dbadmin1'` 并按 `<enter>`。
- b) 密码：`ISS316Security`
- c) 输入命令：`su -c 'usermod -G dba dbadmin2'` 并按 `<enter>`。
- d) 密码：`ISS316Security`

## 20. 将用户 `webadmin1` 和 `webadmin2` 添加到“web”组中

## 21. 输入命令：`su -c 'usermod -G web webadmin1'` 并按 `<enter>`。

## 22. 密码：`ISS316Security`

## 23. 输入相同的命令：`su -c 'usermod -G web webadmin2'` 并按 `<enter>`。

## 24. 密码：`ISS316Security`

#### 将学生账户添加到 Wheel 组

## 25. 将学生用户账户添加到“wheel”组中

## 26. 输入命令：`su -c 'usermod -G wheel student'` 并按 `<enter>`。

## 27. 密码：`ISS316Security`

> **注意：** *学生必须是 wheel 组的成员，才能执行 Labs 3 - 10 中的 `su` 和 `sudo` 命令。*

```text
[student@TargetFedora01 ~]$ su -c 'usermod -G wheel student'
Password:
```

**图 17 — 将学生添加到 wheel 组**

#### 创建临时用户账户并设置 90 天后自动过期

Jane Temp 是一名承包商，协助构建为期 90 天的 Linux 在线备份基础设施。

## 28. 创建临时用户账户名称。输入命令：`su -c 'useradd jtemp'` 并按 `<enter>`。

## 29. 密码：`ISS316Security`

## 30. 为临时用户设置密码。输入命令：`su -c 'passwd jtemp'` 并按 `<enter>`。

## 31. 密码：`ISS316Security`

## 32. 确保用户在首次登录时被迫更改密码。输入命令：`su -c 'chage -d 0 jtemp'` 并按 `<enter>`。

## 33. 密码：`ISS316Security`

**注意：** `-d` 后面是数字零。不是字母 `o`。
