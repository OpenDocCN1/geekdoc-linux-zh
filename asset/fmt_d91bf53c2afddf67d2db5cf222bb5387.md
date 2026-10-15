
- 3. Sam 需要允许标准用户以 `root` 权限运行应用程序。她应该对应用程序应用哪种特殊权限位？

- A. 粘滞位 (Sticky bit)
- B. SUID 位
- C. GUID 位
- D. 执行 (Execute)
- E. 写入 (Write)

- 4. 八进制模式值 `644` 对应的符号模式权限是什么？

- A. `rwxrw-r--`
- B. `-w--w--r-`
- C. `-w-r--r--`
- D. `rx-r-rw-`
- E. `rw-r--r--`

- 5. Fred 被分配任务在公司 Linux 服务器上创建一个新组，现在需要为文件和目录分配权限。他应该使用哪种 Linux 工具来更改分配给文件和目录的组？（选择所有）。

- A. `chgrp`
- B. `chown`
- C. `chmod`
- D. `chage`
- E. `ulimit`

- 6. Sally 需要查看分配给她 Linux 服务器上文件的 ACL 权限。她应该使用什么命令？

- A. `ls -Z`
- B. `ls -l`
- C. `getfacl`
- D. `chmod`
- E. `setfacl`

- 7. 哪种 SELinux 模式跟踪策略违反但不强制执行？

- A. 禁用 (Disabled)
- B. 强制 (Enforcing)
- C. 目标 (Targeted)
- D. 许可 (Permissive)
- E. MLS

- 8. Ted 的任务是记录目录中一组文件分配的 SELinux 安全上下文。他应该使用什么命令？

- A. `getsebool`
- B. `setsebool`
- C. `ls -Z`
- D. `getenforce`
- E. `ls -l`

- 9. Mary 需要以标准用户身份登录她的 Linux 系统，但需要以管理员权限运行应用程序。她可以使用哪些命令来实现此？（选择所有）。

- A. `su`
- B. `wheel`
- C. `visudo`
- D. `sudo`
- E. `adm`

- 10. 哪些用户组通常用于分配组成员以管理员身份运行应用程序的权限？（选择两个。）

- A. `lp`
- B. `adm`
- C. `wheel`
- D. `sudo`
- E. `su`

## 第 16 章

### 查看访问与身份验证方法

- 目标 3.2：在给定场景下，配置并实现相应的访问和身份验证方法。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_494_0.png)

妥善保护系统及其数据的一部分包括提供适当的访问和身份验证方法。有很多工具可以提供这些服务。然而，理解它们如何工作以及如何正确配置它们是至关重要的。

我们将查看各种身份验证和访问方法、它们的配置文件存储在哪里，以及如何正确配置它们。我们还将涵盖一些重要的加密和身份验证主题。

### 了解 PAM

可插件身份验证模块（Pluggable Authentication Modules，PAM）为 Linux 和应用程序提供集中的身份验证服务。PAM 最初由太阳系统公司发明，Linux-PAM 项目始于 1997 年。今天，PAM 通常用于所有的 Linux 发行版。

使用 PAM 服务的程序是用 PAM 库 `libpam` 编译的，并有一个相关的 PAM 配置文件。使用 PAM 的应用程序被称为“PAM 感知”。你可以通过 `ldd` 命令唯一确定一个程序是否是 PAM 感知的。列表 16.1 显示了一个示例。

**列表 16.1：通过 `ldd | grep libpam.so` 确定应用程序是否 PAM 感知**

```
# ldd /bin/login | grep libpam.so
libpam.so => /lib64/libpam.so (0x00007fbf2ce71000)
```

此外，`ldd` 工具用于显示程序所有的共享库依赖。显示输出通过管道传递给 `grep` 以仅搜索 PAM 的 `libpam.so`。在这种情况下，应用程序是用 PAM 库编译的。除了使用 `libpam.so` 库编译外，应用程序还需要一个配置文件来使用 PAM。

### 探索 PAM 配置文件

PAM 配置文件位于 `/etc/pam.d/` 目录。列表 16.2 显示 CentOS 发行版上该目录的文件。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_495_0.png)

**列表 16.2：查看 `/etc/pam.d/` 目录的内容**

```
$ ls /etc/pam.d/
natd gdm-pin postlogin-ac su
chfn gdm-smartcard ppp sudo
chsh ksu remote sudo-i
config-util liveinst runuser su-l
crond login runuser-l system-auth
cups other system-auth-ac
fingerprint-auth password smartcard-auth systemd-user
fingerprint-auth-ac password-auth smartcard-auth-ac vlock
gdm-autlogin password-auth-ac smtp vmtools
gdm-fingerprint pluto smtp.postfix xrdp-sesman
gdm-launch-environment polkit-1 sshd xserver
$
```

注意列表 16.2 中有一个登录配置文件。该文件的片段所示。

**列表 16.3：查看 `/etc/pam.d/login` 文件的内容**

```
$ cat /etc/pam.d/login
##PAM-1.0
[-]
auth include postlogin
account required pam_nologin.so
account include system-auth
password include system-auth
[-]
session optional pam_keyinit.so force revoke
[-]
$
```

PAM 配置文件的记录具有特定的语法。该语法如下：

`TYPE CONTROL-FLAG PAM-MODULE [MODULE-OPTIONS]`

`TYPE`（有时称为上下文或模块接口）指定了特定的 PAM 服务类型。四种 PAM 服务类型如表 16.1 所示。

#### 表 16.1 `/etc/pam.d/` 配置记录中的 `TYPE`

| 接口 | 服务描述 |
| :--- | :--- |
| `account` | 实现账户验证服务，例如强制执行时间限制以及确定账户是否过期 |
| `auth` | 提供账户身份验证管理服务，例如请求密码并验证密码是否正确 |
| `password` | 管理账户密码，例如强制最小密码长度和限制错误密码尝试次数 |
| `session` | 为通过验证的账户提供会话管理，例如记录会话何时开始和结束，以及需要时挂载账户的家目录 |

`/etc/pam.d/` 配置记录中的 `PAM-MODULE` 部分仅仅是执行工作的模块的文件名。例如，`pam_login.so` 就显示在 `/etc/pam.d/` 中。

### 强制执行强密码

通过 `passwd` 命令修改密码时，会调用 PAM。这些不同的 PAM 模块可以帮助执行强密码：

- `pam_unix.so`
- `pam_pwhistory.so`
- `pam_pwquality.so`

通常，你会发现默认安装了 `pam_pwquality.so` 模块。然而，对于 Ubuntu，你需要手动安装它。请使用具有超级权限的账户并在命令行中运行 `sudo apt-get install libpam-pwquality`。

`pam_unix.so` 模块使用存储在 `/etc/passwd` 和 `/etc/shadow` 文件中的账户和密码数据进行认证。

`pam_pwhistory.so` 模块会将用户新输入的密码与历史数据库进行对比，以防止其重用旧密码。密码文件 `/etc/security/passwd` 被锁定。密码也使用加盐和哈希进行存储，采用与 `/etc/shadow` 文件中存储密码相同的哈希算法。

要使用 `pam_pwhistory.so` 模块，你必须修改 `/etc/pam.d/` 配置文件之一。除了指定的类型和模块名外，你还可以设置表 16.3 中列出的一个或多个 `MODULE-OPTIONS`。

#### 表 16.3 防止密码重用的 `MODULE-OPTIONS`

| 模块选项 | 说明 |
|---|---|
| `enforce_for_root` | 如果使用此选项，重置 `root` 账户密码时必须检查其密码是否重用。 |
