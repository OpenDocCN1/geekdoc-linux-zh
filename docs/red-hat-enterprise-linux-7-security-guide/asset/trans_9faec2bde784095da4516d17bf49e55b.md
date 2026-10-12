

为了防止系统在多次登录失败后仍不将用户锁定，请在 `/etc/pam.d/system-auth` 和 `/etc/pam.d/password-auth` 中 `pam_faillock` 首次被调用的行的上方添加以下行。同时，将 `user1`、`user2` 和 `user3` 替换为实际的用户名。

```
auth [success=1 default=ignore] pam_succeed_if.so user in user1:user2:user3
```

要查看每个用户的失败尝试次数，请以 `root` 身份运行以下命令：

```
[root@localhost ~]# faillock
john:
When             Type  Source
Valid
2013-03-05 11:44:14 TTY   pts/0
V
```

要解锁用户的账户，请以 `root` 身份运行以下命令：

```
faillock --user <username> --reset
```

## **使用 authconfig 保留自定义设置**

使用 `authconfig` 实用程序修改身份验证配置时，`system-auth` 和 `password-auth` 文件会被 `authconfig` 实用程序的设置覆盖。这可以通过创建符号链接来替代配置文件避免，`authconfig` 会识别这些链接且不会覆盖它们。若要在配置文件中同时使用自定义设置和 `authconfig`，请按照以下步骤配置账户锁定：

1. 检查 `system-auth` 和 `password-auth` 文件是否已经是指向 `system-auth-ac` 和 `password-auth-ac` 的符号链接（这是系统默认设置）：

```
~]# ls -l /etc/pam.d/{password,system}-auth
```

如果输出类似于以下内容，说明符号链接已就位，您可以跳至第 3 步：

```
lrwxrwxrwx. 1 root root 16 24. Feb 09.29 /etc/pam.d/password-auth -> password-auth-ac
lrwxrwxrwx. 1 root root 28 24. Feb 09.29 /etc/pam.d/system-auth -> system-auth-ac
```

如果 `system-auth` 和 `password-auth` 文件不是符号链接，请继续下一步。

2. 重命名配置文件：

```
~]# mv /etc/pam.d/system-auth /etc/pam.d/system-auth-ac
~]# mv /etc/pam.d/password-auth /etc/pam.d/password-auth-ac
```

3. 创建包含自定义设置的配置文件：

```
~]# vi /etc/pam.d/system-auth-local
```

**/etc/pam.d/system-auth-local** 文件应包含以下内容：

```
auth required pam_faillock.so preauth silent audit
deny=3 unlock_time=600
auth include system-auth-ac
auth [default=die] pam_faillock.so authfail silent audit
deny=3 unlock_time=600

account required pam_faillock.so
account include system-auth-ac

password include system-auth-ac

session include system-auth-ac
```

```
~]# vi /etc/pam.d/password-auth-local
```

**/etc/pam.d/password-auth-local** 文件应包含以下内容：

```
auth required pam_faillock.so preauth silent audit
deny=3 unlock_time=600
auth include password-auth-ac
auth [default=die] pam_faillock.so authfail silent audit
deny=3 unlock_time=600

account required pam_faillock.so
account include password-auth-ac

password include password-auth-ac

session include password-auth-ac
```

4. 创建以下符号链接：

```
~]# ln -sf /etc/pam.d/system-auth-local /etc/pam.d/system-auth
~]# ln -sf /etc/pam.d/password-auth-local /etc/pam.d/password-auth
```

有关各种 **pam_faillock** 配置选项的更多信息，请参阅 pam_faillock(8) 手册页。

## 4.1.3. 会话锁定

在日常操作期间，用户可能需要让工作站处于无人看管状态。这可能会给攻击者提供物理接触该机的机会，特别是在物理安全措施不足的环境中（参见第 1.2.1 节，“物理控制”）。笔记本电脑尤其容易受到攻击，因为其移动性干扰了物理安全。您可以通过使用会话锁定功能来缓解这些风险，该功能会在输入正确密码之前阻止对系统的访问。

### 4.1.3.1. 使用 vlock 锁定虚拟控制台

用户可能还需要锁定虚拟控制台。可以使用名为 vlock 的实用程序来完成此操作。要安装此实用程序，请以 root 身份执行以下命令：

```bash
~]# yum install vlock
```

安装完成后，可以使用 vlock 命令锁定任何控制台会话，无需任何额外参数。这将锁定当前活动的虚拟控制台会话，同时仍允许访问其他会话。要阻止访问工作站上的所有虚拟控制台，请执行以下操作：

```bash
vlock -a
```

在这种情况下，vlock 锁定当前活动的控制台，-a 选项阻止切换到其他虚拟控制台。

有关其他信息，请参阅 vlock(1) man 手册页。

## 4.1.4. 强制只读挂载可移动媒体

若要强制只读挂载可移动媒体（如 USB 闪存盘），管理员可以使用 udev 规则检测可移动媒体，并使用 blockdev 实用程序将其配置为只读挂载。这对于强制物理媒体的只读挂载已足够。

### 使用 blockdev 强制可移动媒体只读挂载

若要强制所有可移动媒体只读挂载，请在 /etc/udev/rules.d/ 目录中创建一个名为 80-readonly-removables.rules 的新 udev 配置文件，内容如下：

```
SUBSYSTEM=="block",ATTRS{removable}=="1",RUN{program}="/sbin/blockdev --setro %N"
```

上述 udev 规则确保任何新连接的可移动块（存储）设备都会自动使用 blockdev 实用程序配置为只读。

### 应用新的 udev 设置

为了使这些设置生效，需要应用新的 udev 规则。udev 服务会自动检测到其配置文件的更改，但新设置不会应用于已存在的设备。只有新连接的设备会受到新设置的影响。因此，您需要卸载并拔掉所有已连接的可移动媒体，以确保在下次插入时应用新设置。

若要强制 udev 重新应用所有规则到已存在的设备，请以 root 身份输入以下命令：

```bash
~# udevadm trigger
```

请注意，使用上述命令强制 udev 重新应用所有规则不会影响已挂载的存储设备。

若要强制 udev 重新加载所有规则（以防新规则因某种原因未被自动检测），请使用以下命令：

```
~# udevadm control --reload
```

## 4.2. 控制 root 访问权限

在管理家用机器时，用户必须作为 **root** 用户执行某些任务，或者通过使用 setuid 程序（如 **sudo** 或 **su**）获取有效的 **root** 权限。setuid 程序是指以程序拥有者的用户 ID（*UID*）而非操作该程序的用户身份运行的程序。此类程序在长格式列表的所有者部分由一个 **s** 表示，如以下示例所示：

```
-]$ ls -l /bin/su
-rwsr-xr-x. 1 root root 34904 Mar 10 2011 /bin/su
```

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_37_0.png)

> **注意**
> 
> **s** 可以是大写或小写。如果显示为大写，则表示未设置底层权限位。

然而，对于组织的系统管理员来说，必须决定组织内用户对机器的管理访问权限应有多少。通过一个名为 *pam_console*.so 的 PAM 模块，通常仅限 root 用户执行的一些活动，如重启和挂载可移动媒体，允许第一个在物理控制台登录的用户执行。然而，其他重要的系统管理任务，如更改网络设置、配置新鼠标或挂载网络设备，在没有管理权限的情况下是无法完成的。因此，系统管理员必须决定网络上的用户应获得多少访问权限。

### 4.2.1. 禁止 root 访问

如果管理员由于上述原因或其他原因而不允许用户以 **root** 身份登录，应保持 root 密码的机密性，并且通过引导加载程序密码保护（有关此主题的更多信息，请参见第 4.2.5 节，“保护引导加载程序”）禁止访问运行级别 1 或单用户模式。

以下是管理员可以进一步确保禁止 **root** 登录的四种不同方法：

#### 更改 root shell

为了防止用户直接以 **root** 身份登录，系统管理员可以在 */etc/passwd* 文件中将 **root** 账户的 shell 设置为 */sbin/nologin*。

表 4.2. 禁用 Root Shell

