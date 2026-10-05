

## 第 6 章 | 管理本地用户和组

### 4. 在登录 shell 中切换到 root 并探索新的 shell 环境。

4.1. 在 shell 提示符处运行 `sudo su -` 以成为 root 用户。

```
[student@servera ~] sudo su
[root@servera #]
```

注意 shell 提示符与上一步中 `sudo su` 相比的区别。
sudo 可能会或可能不会提示你输入 student 密码，这取决于 sudo 的超时时间。默认超时时间为五分钟。如果你在过去五分钟内通过了 sudo 认证，sudo 将不会提示你输入密码。如果距离上次通过 sudo 认证已超过了五分钟，你需要输入 student 密码来通过 sudo 认证。

4.2. 运行 `id` 查看当前的用户和组组信息。

```
[root@servera #] id
uid=0(root) gid=0(root) groups=0(root)
context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

4.3. 运行 `pwd` 显示工作目录。

```
[root@servera #] pwd
root
```

4.4. 打印 `HOME` 和 `PATH` 变量的值，分别确定主目录和用户可执行文件路径。

```
[root@servera #] echo HOME
/root
[root@servera #] echo PATH
/usr/local/sbin:/usr/local/bin:/usr/bin:/root/bin
```

在上一步中，在 sudo 从 student shell 环境设置中重置 PATH 变量后，`su -` 命令运行了 root 的 shell 登录脚本并将 PATH 变量设置为另一个值。不带 `)` 的 `su` 命令没有执行此操作。

4.5. 退出 root 用户的 shell 返回 student 用户的 shell。

```
[root@servera #] exit
logout
[student@servera ~]$
```

5. 验证 operator1 用户已配置为可以使用 sudo 以任何身份运行任何命令。

```
student@servera ~]$ sudo cut /etc/sudoers.d/operator1
operator1-ALL=(ALL)
```

6. 成为 operator1 并查看 /var/log/messages 的内容。将 /etc/motd 复制到 /etc/motd 并删除它 (/etc/motd)。这些操作需要管理员权限，因此你使用 sudo 以超级用户身份运行这些命令。不要通过 `sudo su` 或 `sudo su -` 切换到 root。

### 6.1. 切换到 operator1。

```
[student@servera ~]$ su - operator1
Password: redhat
[operator1@servera ~]
```

6.2. 尝试不用 sudo 查看 /var/log/messages 的五行。这应该会失败。

```
[operator1@servera ~]$ tail -5 /var/log/messages
tail: cannot open '/var/log/messages' for reading: Permission denied
```

6.3. 尝试使用 sudo 查看 /var/log/messages 的五行。这应该成功。

```
[operator1@servera ~]$ sudo tail -5 /var/log/messages
[sudo] password for operator1: redhat
Jan 23 15:53:36 server su(2394): FAILED SU (to operator1) student on pts/1
Jan 23 15:53:51 servera su(2310): FAILED SU (to operator1) student on pts/1
Jan 23 15:53:58 servera su(2310): FAILED SU (to operator1) student on pts/1
Jan 23 15:54:12 server su(2322): (to operator1) student on pts/1
Jan 23 15:54:25 servera su(2853): (to operator1) student on pts/1
```

> 注意
> 上述输出在你的系统上可能有所不同。

6.4. 尝试不用 sudo 将 /etc/motd 复制为 /etc/motd。这应该会失败。

```
[operator1@servera ~]$ cp /etc/motd /etc/motd
cp: cannot create regular file '/etc/motd': Permission denied
```

6.5. 尝试使用 sudo 将 /etc/motd 复制为 /etc/motd。这应该成功。

```
[operator1@servera ~]$ sudo cp /etc/motd /etc/motd
[operator1@servera ~$]
```

6.6. 尝试不用 sudo 删除 /etc/motd。这应该会失败。

```
[operator1@servera ~$] rm /etc/motd
rm: remove write-protected regular empty file '/etc/motd'
rm: cannot remove '/etc/motd': Permission denied
[operator1@servera ~$]
```

6.7. 尝试使用 sudo 删除 /etc/motd。这应该成功。

```
[operator1@servera ~$] sudo rm /etc/motd
[operator1@servera ~$]
```

6.8. 退出 operator1 的 shell 返回 student 用户的 shell。

```
[operator1@servera ~$] exit
logout
[student@servera ~]$
```

6.9. 从服务器注销。

```
[student@servera ~]$ exit
logout
Connection to server closed.
```

### 完成。

在工作站上，运行 `lab-finish` 完成练习。

## 第 6 章 | 管理本地用户和组

### 管理用户账户

### 目标
完成本节后，你应该能够创建、修改和删除用户账户。

## 管理用户

### 从命令行创建用户
- `useradd` 命令创建一个新用户。它设置了主目录和账户信息。此时账户还没有设置有效密码。
- `useradd --help` 显示可使用的选项。

### 从命令行修改现有用户
- `usermod --help` 显示可使用的选项：

| 选项 | 用法 |
| :--- | :--- |
| -c, --comment | 将姓名添加到注释字段。 |
| -g, --group | 指定用户的主组。 |
| -G, --groups | 指定逗号分隔的辅助组列表。 |
| -a, --append | 与 -G 使用，添加辅助组而不是替换。 |
| -d, --home_DIR | 为用户指定特定的主目录。 |
| -m, --move-home | 将用户的主目录移动到新位置。必须配合 -d 使用。 |
| -s, --shell | 为用户账户指定特定的登录 shell。 |
| -L, --lock | 锁定账户 |

### 从命令行删除用户
- `userdel username` 从 /etc/passwd 中删除用户的详细信息，但保留用户的主目录。
- `userdel -r username` 从 /etc/passwd 中删除用户的详细信息并删除用户的主目录。

> 警告
当不带 -r 选项使用 userdel 删除时，系统将拥有属于分配 UID 的文件。当已删除用户的所有者文件存在于其主目录之外时，也会发生这种情况。这可能会导致信息泄露和其他安全问题。在 Red Enterprise Linux 7 和 Red Enterprise Linux 8 中，`useradd` 命令分配大于 1000 的第一个空闲 UID，除非你使用 -u 选项指定它。这就是信息泄露发生的情况。如果第一个空闲 UID 之前分配给已删除的用户账户，则旧用户的 UID 将重新分配给新用户，从而让新用户拥有旧用户文件的所有权。

### 从命令行设置密码
- `password username` 命令设置用户的初始密码或更改 username 的现有密码。

