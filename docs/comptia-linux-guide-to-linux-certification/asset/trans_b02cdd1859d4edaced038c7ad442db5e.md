

### 项目 10-6

2. 在命令提示符下，键入 **cat /etc/passwd** 并按 **Enter**（回车）键。记录用于描述用户 **bozo** 的那一行。

3. 在命令提示符下，键入 **cat /etc/shadow** 并按 **Enter**（回车）键。记录用于描述用户 **bozo** 的那一行。

4. 在命令提示符下，键入 **usermod -l bozo2 bozo** 并按 **Enter**（回车）键，将用户 **bozo** 的登录名更改为 **bozo2**。接下来，在命令提示符下键入 **cat /etc/passwd** 并按 **Enter**（回车）键。登录名是否已从 **bozo** 更改为 **bozo2**？UID 是否发生了更改？主目录是否发生了更改？

5. 在命令提示符下，键入 **usermod -l bozo bozo2** 并按 **Enter**（回车）键，将用户 **bozo2** 的登录名改回 **bozo**。

6. 在命令提示符下，键入 **usermod -u 666 bozo** 并按 **Enter**（回车）键，将用户 **bozo** 的 UID 更改为 **666**。接下来，在命令提示符下键入 **cat /etc/passwd** 并按 **Enter**（回车）键。UID 是否发生了更改？

7. 在命令提示符下，键入 **usermod -f 14 bozo** 并按 **Enter**（回车）键，设置密码过期后 14 天禁用 **bozo** 的用户账户。接下来，在命令提示符下键入 **cat /etc/shadow** 并按 **Enter**（回车）键。哪个字段发生了更改？

8. 在命令提示符下，键入 **usermod -e "01/01/2025" bozo** 并按 **Enter**（回车）键，使 **bozo** 的用户账户在 2025 年 1 月 1 日过期。接下来，在命令提示符下键入 **cat /etc/shadow** 并按 **Enter**（回车）键。哪个字段发生了更改？该字段中的数字代表什么？

9. 在命令提示符下，键入 **chage -m 2 bozo** 并按 **Enter**（回车）键，要求用户 **bozo** 在更改密码前至少等待两天。接下来，在命令提示符下键入 **cat /etc/shadow** 并按 **Enter**（回车）键。哪个字段发生了更改？

10. 在命令提示符下，键入 **chage -M 40 bozo** 并按 **Enter**（回车）键，要求用户 **bozo** 每 40 天更改一次密码。接下来，在命令提示符下键入 **cat /etc/shadow** 并按 **Enter**（回车）键。哪个字段发生了更改？

11. 在命令提示符下，键入 **chage -W 5 bozo** 并按 **Enter**（回车）键，在需要更改密码前 5 天警告用户 **bozo**。接下来，在命令提示符下键入 **cat /etc/shadow** 并按 **Enter**（回车）键。哪个字段发生了更改？

12. 键入 **exit** 并按 **Enter**（回车）键注销 shell。

### 项目 10-7

在这个动手项目中，你将使用命令行实用程序在 Fedora Linux 上锁定和解锁用户账户。

1. 在你的 Fedora Linux 虚拟机上，按 **Ctrl+Alt+F2** 切换到命令行终端（tty2），并使用用户名 **root** 和密码 **LNXrocks!** 登录到终端。

2. 在命令提示符下，键入 **cat /etc/shadow** 并按 **Enter**（回车）键。记录 **bozo** 用户账户的加密密码。

3. 在命令提示符下，键入 **passwd -l bozo** 并按 **Enter**（回车）键以锁定 **bozo** 的用户账户。

4. 在命令提示符下，键入 **cat /etc/shadow** 并按 **Enter**（回车）键。与步骤 2 中记录的原始加密密码相比，有什么变化？

![](img/c27875544958897d817484d558c208c8_496_0.png)

5. 按 **Ctrl+Alt+F5** 切换到命令行终端（tty5），并尝试使用用户名 **bozo** 和密码 **LNXRocks!** 登录到终端。你成功了吗？

6. 按 **Ctrl+Alt+F2** 切换回命令行终端（tty2）。

7. 在命令提示符下，键入 `passwd -u bozo` 并按 **Enter**（回车）键以解锁 bozo 的用户账户。

8. 在命令提示符下，键入 `cat /etc/shadow` 并按 **Enter**（回车）键。将 bozo 用户账户的加密密码与步骤 2 中记录的进行比较。

9. 按 **Ctrl+Alt+F5** 切换到命令行终端（tty5），并尝试使用用户名 **bozo** 和密码 **LNXRocks!** 登录到终端。你成功了吗？

10. 键入 `exit` 并按 **Enter**（回车）键注销 shell。

11. 按 **Ctrl+Alt+F2** 切换回命令行终端（tty2）。

12. 在命令提示符下，键入 `usermod -s /bin/false bozo` 并按 **Enter**（回车）键以将 bozo 的 shell 更改为 `/bin/false`。你收到了什么消息？shell 是否发生了更改？在命令提示符下键入 `cat /etc/passwd` 以验证 bozo 的用户账户的 shell 是否已更改为 `/bin/false`。

13. 按 **Ctrl+Alt+F5** 切换到命令行终端（tty5），并尝试使用用户名 **bozo** 和密码 **LNXRocks!** 登录到终端。你成功了吗？

14. 按 **Ctrl+Alt+F2** 切换回命令行终端（tty2）。

15. 在命令提示符下，键入 `usermod -s /bin/bash bozo` 并按 **Enter**（回车）键以将 bozo 的 shell 更改为 `/bin/bash`。

16. 按 **Ctrl+Alt+F5** 切换到命令行终端（tty5），并尝试使用用户名 **bozo** 和密码 **LNXRocks!** 登录到终端。你成功了吗？

17. 键入 `exit` 并按 **Enter**（回车）键注销 shell。

18. 按 **Ctrl+Alt+F2** 切换回命令行终端（tty2）。

19. 键入 `exit` 并按 **Enter**（回车）键注销 shell。

### 项目 10-8

在这个动手项目中，你将使用命令行实用程序在 Fedora Linux 上删除一个用户账户，并创建一个新用户账户来替代它。

1. 在你的 Fedora Linux 虚拟机上，按 **Ctrl+Alt+F2** 切换到命令行终端（tty2），并使用用户名 **root** 和密码 **LNXRocks!** 登录到终端。

2. 在命令提示符下，键入 `ls -la /home/bozo` 并按 **Enter**（回车）键。谁拥有此目录中的大多数文件？为什么？

3. 在命令提示符下，键入 `userdel bozo` 并按 **Enter**（回车）键。bozo 的主目录也被删除了吗？

4. 在命令提示符下，键入 `ls -la /home/bozo` 并按 **Enter**（回车）键。谁拥有此目录中的大多数文件？为什么？

5. 在命令提示符下，键入 `useradd -m -u 666 bozoette` 并按 **Enter**（回车）键。此命令中 `-m` 和 `-u` 选项的作用是什么？

6. 在命令提示符下，键入 `passwd bozoette` 并按 **Enter**（回车）键。输入密码 LNXrocks! 并按 **Enter**（回车）键。再次输入密码 LNXrocks! 进行确认并按 **Enter**（回车）键。

7. 在命令提示符下，键入 `cat /etc/passwd` 并按 **Enter**（回车）键。bozoette 的主目录是什么？bozoette 的 UID 是什么？

8. 在命令提示符下，键入 `ls -la /home/bozo` 并按 **Enter**（回车）键。谁拥有此目录中的大多数文件？为什么？bozoette 可以管理这些文件吗？

9. 键入 `exit` 并按 **Enter**（回车）键注销 shell。

### 项目 10-9

在这个动手项目中，你将使用命令行实用程序在 Fedora Linux 上创建、使用和删除组。

1. 在你的 Fedora Linux 虚拟机上，按 `Ctrl+Alt+F2` 切换到命令行终端（tty2），并使用用户名 **root** 和密码 LNXrocks! 登录到终端。

2. 在命令提示符下，键入 `vi /etc/group` 并按 **Enter**（回车）键以在 vi 编辑器中打开 /etc/group 文件。在文件底部添加一行，内容如下：

```
groupies:x:1234:root,bozoette
```

这向系统添加了一个 GID 为 1234 的组，成员为 root 和 bozoette。完成后，保存并退出 vi 编辑器。

3. 按 `Ctrl+Alt+F5` 切换到命令行终端（tty5），并使用用户名 **bozoette** 和密码 LNXrocks! 登录到终端。

4. 在命令提示符下，键入 `groups` 并按 **Enter**（回车）键。bozoette 是哪些组的成员？

5. 在命令提示符下，键入 `id` 并按 **Enter**（回车）键。对于用户 bozoette，哪个组是主组？

6. 在命令提示符下，键入 `touch file1` 并按 **Enter**（回车）键以在当前目录中创建一个名为 file1 的新文件。

7. 在命令提示符下，键入 `ls -l` 并按 **Enter**（回车）键。文件 file1 的所有者和组所有者是谁？为什么？

8. 在命令提示符下，键入 `newgrp groupies` 并按 **Enter**（回车）键以暂时将 bozoette 的主组更改为 groupies。

9. 在命令提示符下，键入 `touch file2` 并按 **Enter**（回车）键以在当前目录中创建一个名为 file2 的新文件。

10. 在命令提示符下，键入 `ls -l` 并按 **Enter**（回车）键。文件 file2 的所有者和组所有者是谁？为什么？

