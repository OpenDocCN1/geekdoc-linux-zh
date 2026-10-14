
- 12. 选择创建（Create）。

返回用户和组管理对话框。

- 13. 使用表 2-1 所示的参数创建第二个数据库管理员账户。

### 表 2-1

| 字段 | 取值 |
| --- | --- |
| 用户全名 | Database Admin 2 |
| 用户登录名 | `dba2` |
| 密码 | `suse2` |

### 表 2-1（续）

| 字段 | 取值 |
| --- | --- |
| 组 | 默认组加 `dba` 组 |
| 过期日期 | 今天 5 天后（如 2007-07-06） |
| 主目录 | `/export/home/dba2` |

- 14. 完成创建 `dba1` 和 `dba2` 后，选择完成（Finish）结束流程。

- 15. 验证用户 `dba` 是否可用：

  - a. 按 `Ctrl+Alt+F2` 切换到虚拟控制台 2。
  - b. 输入 `dba` 和密码 `suse1` 登录。

    注意出现了团队欢迎消息（来自 `/etc/motd`）。
  - c. 输入 `exit` 退出。

    注意出现了来自 `/etc/issue` 文件的消息。
  - d. 输入 `dba2` 和密码 `suse2` 登录；然后输入 `exit` 退出。
  - e. 按 `Ctrl+Alt+F7` 返回 KDE 桌面。

用户 `dba` 是数据库管理员组的组长，应该拥有数据库管理员组的所有权。

- 16. 从终端窗口，将 `dba` 设置为目录的所有者：

```
chown dba:dba /export/data2
```

- 17. 通过输入 `ls -l /export/data2` 验证更改。

## 第 2 管理用户访问与安全

2. 输入以下命令将 `dba1`、`dba2` 和 `dba3` 添加到 `party` 组：

```bash
usermod -G uucp,dialout,audio,video,dba,party,dbabackup dba1
usermod -G uucp,dialout,audio,video,dba,party,dbabackup dba2
usermod -G uucp,dialout,audio,video,dba,party,dbabackup dba3
```

确保每个命令都单独占占一行，且逗号后没有空格。

3. 输入以下命令验证这些用户是否已添加到 `party` 组：

```bash
groups dba1
groups dba2
groups dba3
```

## 第七部分：从命令行管理用户账户

在终端窗口中，执行以下操作：

1. 输入以下内容检查 `shadow` 文件中 `dba3` 的条目：

```bash
grep dba3 /etc/shadow
```

2. 使用 `passwd` 命令锁定 `dba3` 账户：

```bash
passwd -l dba3
```

3. 输入以下内容再次检查 `shadow` 中的条目：

```bash
grep dba3 /etc/shadow
```

注意 "`dba3`" 后面有一个 "`!`"。这表示该账户已锁定。

4. 切换到虚拟控制台尝试登录 `dba3`，以验证账户已锁定。

显示登录错误（Login）。

5. 返回 KDE 桌面 (`Ctrl+Alt+F7`)，输入以下内容解锁 `dba3` 账户：

```bash
passwd -u dba3
```

6. 输入以下内容检查 `shadow`：

```bash
grep dba3 /etc/shadow
```

注意 "`!`" 已从账户信息中移除。

## 管理 Linux 用户和组

7. 切换到虚拟控制台尝试登录 `dba3`，以验证账户已解锁。

你现在可以登录了。注意上次登录以来的失败次数。

8. 输入 `exit` 退出 `dba3` 登录。

9. 返回 KDE 桌面 (`Ctrl+Alt+F7`)。

10. 输入以下内容以 GECOS 格式更改 `dba2` 账户的信息：

```bash
passwd -f dba2
```

11. 当提示全名时，按回车键继续。

12. 根据提示输入以下信息：

- 房间：Classroom
- 电话：555
- 电话：444
- 其他：Level

13. 输入 `finger dba2` 验证你为 `dba2` 添加的信息。

14. 输入 `groupdel party` 删除 `party` 组。

15. 输入以下内容删除 `dba3` 账户及其家目录：

```bash
userdel -r dba3
```

出现信息消息显示 `dba3` 没有 `crontab` 任务。

16. 输入以下内容查看 `dba2` 账户的密码策略：

```bash
chage -l dba2
```

## 第八部分：为新用户恢复默认组

在创建新用户时，通过以下操作恢复默认组分配：

1. 从 YaST 控制中心，选择安全（Security）> 用户（Users）> 创建组（Edit and create groups）。
2. 从专家（Expert）下拉列表中选择新用户默认（Defaults for New Users）。
3. 从默认组（Default Group）下拉列表中选择用户（users）。
4. 点击下一步（Next）继续。
5. 点击完成（Finish）保存配置更改。
6. 关闭所有窗口。

## 目标 3 管理并安全 Linux 用户环境

除了管理单独的用户账户，还需要知道如何执行以下操作来管理和安全用户环境：

- 以 root 身份执行任务
- 使用 `sudo` 委托任务
- 设置新用户默认
- 配置安全设置

### 以 root 身份执行任务

作为系统管理员，建议以普通用户登录，仅在执行需要 root 权限的任务时切换到 root。

在执行任务时于普通用户和 root 之间切换，可以执行以下操作：

- 使用 `su` 切换到用户
- 使用 `newgrp` 切换到另一个组
- 从 KDE 以其他用户启动程序

### 使用 su 切换到用户

可以使用 `su`（切换用户）命令来假设 root 或其他用户的 UID。

以下是 `su` 的语法：

```bash
su [options] [user]
```

例如，切换到 `geeko` 用户，输入 `su geeko`；切换到 root 用户，输入 `su`（不带名称）。

注意：root 可以在不知道用户密码的情况下切换到任何用户。

如果你在切换用户时启动登录 shell，可以输入 `su -`。切换到 root 用户并执行单个命令，可以使用选项 `-c`：

```bash
su -c "grep /etc/shadow"
```

关于 `su` 命令的更多信息，输入 `su --help`。

### 使用 newgrp 切换到另一个组

用户可以是许多组的成员，但任何时候只有一个 GID 是其有效（当前）组。通常，主组指定在 `/etc/passwd` 文件中。

如果用户创建了目录或文件，它们属于该用户和有效组。你可以使用 `newgrp` 或 `sg` 命令更改有效 GID。只有组成员可以执行此更改，除非定义了组密码。在这种情况下，任何知道组密码的用户都可以更改。你可以通过输入 `exit` 或按 `Ctrl+D` 消更改（返回原始 GID）。

### 从 KDE 以其他用户启动程序

在 KDE 中，可以通过以下操作以不同的 UID 启动任何程序（只要知道密码）：

1. 从 KDE 桌面，按 `Alt+F2` 打开命令行对话框，然后选择选项（Options）。

## 第 2 管理用户访问与安全

如图 2-13 所示的对话框。从此对话框，你可以输入想要运行（或查看）的命令。还有选项，包括以不同用户运行命令的选项。

2. 选择**以不同用户运行 (Run as a different user)**：输入用户名（如 root）和密码。

3. 输入你想以 root 身份运行的命令；然后选择**运行 (Run)**。你也可以输入 `program_name` 以 root 身份启动程序。程序启动前会提示输入 root 密码。

## 使用 sudo 委托任务

有时需要允许普通用户访问通常留给 root 的命令。例如，你可能希望在休假期间让同事接管关闭电脑和创建用户等任务。

## 管理和安全 Linux 用户环境

要允许普通用户运行某个命令，可以使用 `sudo` 命令（如下所示）：

```bash
geeko@earth:~ > sudo /sbin/shutdown -h now
```

我们相信你已经收到了管理员的常规说明。这通常涉及以下两点：

1) 尊重他人的隐私。
2) 输入前思考。

系统提示输入密码，即用户密码。作为管理员，你可以使用 `visudo` 指定用户可以或不能进入的文件。

以下是配置文件的通用语法：

```
user/group = command1, command2 ...
```

例如：

```
geeko ALL = /sbin/shutdown
```
