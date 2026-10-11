
`groupdel`命令用于从系统中删除组的命令。

组标识符（GID）分配给每个组的唯一数字。

`groupmod`命令用于修改系统中组名称或GID的命令。

`groups`命令列出用户组身份的命令。

`id`命令列出用户UID和其所属组的GID的命令。

互联网打印协议（IPP）一种可以使用`HTTP`或`HTTPS`跨越`TCP/IP`网络（如互联网）发送打印任务的打印协议。

行打印机守护进程（LPD）通常用于旧式计算机的打印系统。

锁定账户通过修改系统存储的账户密码信息使账户临时不可用。

日志文件包含`Linux`系统信息的文件。

`logrotate`命令用于轮转日志文件的命令；它使用存储在`/etc/logrotate.conf`中的配置。

`lpadmin`命令用于在`CUPS`打印系统中执行打印机管理的命令。

# 第 10 章 常见管理任务

`lp`命令用于在`LPD`打印系统中查看状态和控制打印机的命令。

`lp`命令用于在`CUPS`打印系统中队列中创建打印任务的命令。

`lpq`命令用于查看`LPD`打印系统中打印队列内容的命令。

`lpr`命令用于在`LPD`打印系统中队列中创建打印任务的命令。

`lprm`命令从队列中移除打印任务的命令。

`lpstat`命令用于查看系统中打印队列内容和信息的命令。

`newgroup`命令用于更改用户主组的命令。

`passwd`命令用于修改与用户关联密码的命令。

即插即用（PnP）一种允许用户向计算机添加硬件而无需配置硬件即可与系统工作的技术。

主组在`/etc/passwd`文件中为用户指定的组，并被指定为用户创建的所有文件的组。

打印将打印任务从打印队列发送到打印机的过程。

打印任务ID用于标记和区分每个打印任务的唯一标识符。

打印队列文件系统上的一个目录，持有等待打印的任务。

打印机类可用于对`CUPS`系统上的打印机应用设置的模板。

打印机配置工具（Printer Configuration tool）用于在系统中配置打印机的图形化界面。

优先级记录系统事件时系统信息的重要性。

`passwd`命令用于启用使用`/etc/shadow`文件的命令。

`passwdlock`命令用于禁用使用`/etc/shadow`文件的命令。

拒绝的打印机不接受打印任务进入队列的打印机。

骨架目录包含会被复制到所有用户主目录文件的目录；`Linux`系统上的骨架目录为`/etc/skeleton`。

轮空将打印任务接受打印队列的过程。

系统日志守护进程（syslog）通过存储在`/etc/syslog.conf`各种文件中记录事件的守护进程。

统一资源标识符（URI）使用类型跟随标识的命名规范。

用户账户存储在系统数据库（`/etc/passwd`和`/etc/shadow`）中的用户信息，用于登录系统并访问资源。

`useradd`命令向系统添加用户账户的命令。

`userdel`命令从系统中删除用户账户的命令。

7. 哪种命令可以将打印任务发送到默认打印机`printer1`？

（选择所有适用项）

- a. `lp -d printer1`
- b. `lp printer1`
- c. `lp file`
- d. `lp -m printer1`

8. 包含系统中所有用户及其主目录的文件名称是？

- a. `/etc/passwd`
- b. `/etc/users`
- c. `/etc/shadow`
- d. `/etc/password`

9. `UID`和`GID`是系统唯一的，且一旦被使用就永远无法重新使用。是/否？

10. 用于轮转日志文件的工具名称是？

- a. `syslog`
- b. `jetpack`
- c. `logrotate`
- d. `logbackup`

11. 你可以通过将`/etc/passwd`中的默认登录shell改为无效shell来锁定用户账户。是/否？

12. 当打印机拒绝请求时，____________________

- a. 打印队列不接受任务并向用户发送消息提示打印机不可用
- b. 打印队列接受任务并保留它们，直到打印机再次接受请求
- c. 当发送`lp`请求时打印机显示为离线
- d. 打印队列将发送给它的任务重定向到`/dev/null`

13. 参考`/etc/syslog.conf`文件时，________________ 指定系统特定区域的信息，而 ________________ 是该信息的重要性水平。

- a. `section`, `priority`
- b. `service`, `precedents`
- c. `process`, `degree`
- d. `facility`, `priority`

+ 14. 系统中的大多数日志文件位于哪个目录？

a. `/etc/logfiles`

b. `/etc/log`

c. `/var/log`

d. `/dev/log`

+ 15. 哪个文件包含了创建用户时使用的默认信息，如`UID`和`GID`范围以及最小密码长度？

a. `/etc/skel`

b. `/etc/passwd`

c. `/etc/login.defs`

d. `/etc/default/useradd`

+ 16. `Fedora Linux`中负责打印的后台进程是哪个？

a. `lp`

b. `cupsd`

c. `lpd`

d. `lpstat`

+ 17. 你会使用哪个命令来解锁用户账户？

a. `unlock username`

b. `open username`

c. `usermod -U username`

d. `useradd -U username`

+ 18. 在用户账户列表中，`/etc/passwd`文件包含账户过期的信息。正确或错误？

19. 使用`lpstat`确定用户`User1`已为`Printer1`队列提交了两个必须打印的大型打印任务。它们的任务ID分别为`Printer-17`和`Printer-21`。你会使用哪个命令从队列中删除这两个任务？

a. `cancel Printer-17 Printer-21`

b. `cancel -u Printer-17 Printer-21`

c. `cancel -a Printer-17 Printer-21`

d. `cancel 17 21`

+ 20. 哪个命令用于删除用户账户？

a. `usermod -d username`

b. `userdel username`

c. `rm username`

## 动手项目

这些项目应按照给出的顺序完成。本章介绍的动手项目总共需要三小时完成。该实验的要求包括：

- 根据“动手项目 2-2”安装了`Fedora 13`的计算机。

## 项目 10-1

在这一动手项目中，你将使用打印机配置工具（Printer Configuration tool）创建一个本地打印机。

+ 1. 开启电脑。在`Linux`系统加载后，以用户身份登录`GNOME`桌面环境。

2. `GNOME`桌面加载后，导航到系统菜单（System）、管理（Administration）、打印（Printing）。

3. 点击添加（Add）按钮创建新打印机。在提示时输入`root`用户密码`secret`并点击身份验证（Authenticate）（你会被提示两次）。

4. 点击向前（Forward）进入添加新打印队列屏幕。

5. 确保左侧面板选了其他（Other），在输入`URI`对话框中输入`parallel:/dev/null`并点击向前（Forward）。

![](img/bafa5678973f896b93838a140b8f7840_495_0.png)
