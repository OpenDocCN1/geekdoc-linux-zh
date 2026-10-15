
条目末尾是 `:chkent:` 字段，表示条目已完成。该字段由读取文件的程序用作条目的完整性检查。

以下文本描述了示例选项的含义。

- `default` — 这个第一个选项只是指定此安全数据库的文件名的头，并且是必需的。
- `d_name` — 此选项指定此安全数据库的名称，不应从字符串 `default` 中更改。
- `d_secclass` — 此选项是系统支持的安全类别的信息标识符，应设置为 `c2`。
- `d_boot_authenticate` — 此选项目前未被增强安全使用。

## 以 root 身份登录

执行此过程时，既可以在系统控制台上直接以 root 身份登录，也可以从终端或通过网络以普通非特权用户身份登录后使用 `su` 切换到 root。使用以下命令检查增强安全性是否尚未启用。

```
# /usr/sbin/rcmgr get SECURITY
```

如果返回字符串 `BASE`，则表示您正在运行基本安全性。但如果返回字符串 `ENHANCED`，则表示增强安全性已在此系统上启用，您应跳至第 5 步（“调整系统默认数据库”一节）以调整全局默认值。

## 系统默认数据库文件格式 — 续

`d_pw_expire_warning` 此选项以秒为单位，用于确定在登录时是否给出密码过期警告。如果用户的密码过期时间落在此时间间隔内，则会给出警告。

`d_pw_site_callout` 此选项指定用于站点特定安全策略合规性决策所调用脚本的完整路径名。默认情况下，`/etc/bin/pwpolicy` 除了以正返回码退出外不做任何事。有关此选项的更多信息，请参阅“DEC OSF/1 Security”手册。

`u_minchg#0` 此选项以秒为单位指定两次密码更改之间的最短时间。如果分配值为零（0），则不强制执行最短时间限制。

`u_minlen#8` 此选项指定密码最小长度。

`u_maxlen#12` 此选项指定密码最大长度。

`u_exp#0` 此选项指定在成功更改密码后，帐户密码将过期的秒数。如果指定值为零（0），则密码不会过期。

## 安装增强安全子集

在启用增强安全性之前，必须加载两个增强安全软件子集。这两个子集名为 `OSF C2SECxxx` 和 `OSF XC2SECxxx`。`xxx` 指定子集的版本。要确定这些子集是否已加载，可以通过以下命令和输出进行检查。

```
# /usr/sbin/setld -i | grep -i c2sec
OSFC2SEC350 installed C2-Security (System Administration)
OSFXC2SEC350 installed C2-Security GUI (System Administration)
```

在此示例中，两个子集均已安装。如果您没有收到任何输出，或者缺少 `installed` 关键字，则必须使用 `setld` 命令从操作系统主安装介质安装这两个子集。如需帮助，请参阅与您的操作系统版本相对应的《安装指南》。

## 系统默认数据库文件格式 — 续

`u_pwdepth#0` 此选项指定保存旧加密密码的数量以防止重复使用。值为零（0）表示可以重用旧密码。

`u_nullpw@` 此布尔选项控制用户选择空密码的能力。存在 `u_nullpw` 条目表示可以选择空密码；存在 `u_nullpw@` 条目则表示不能。

`u_genchars@` 此布尔选项控制用户为密码生成随机字符的能力。存在 `u_genchars` 条目表示用户可以生成由随机字符组成的密码；存在 `u_genchars@` 条目表示不能。

`u_genletters@` 此布尔选项控制用户为密码生成随机字母的能力。存在 `u_genletters` 条目表示用户可以生成由随机字母组成的密码；存在 `u_genletters@` 条目表示不能。

`u_maxtries#0` 此选项指定在帐户被锁定之前，对该帐户连续登录失败的最大次数。将此选项设置为零（0）会禁用因登录失败而锁定帐户的功能。

`u_lock@` 此布尔选项用于以管理方式锁定帐户。存在 `u_lock` 条目表示帐户已锁定；存在 `u_lock@` 条目表示未锁定。默认数据库文件中存在 `u_lock@` 条目的目的是全局指示所有帐户均未锁定，除非在各自的受保护密码数据库文件中被锁定。

`t_logdelay#2` 此选项指定失败登录尝试之间的秒数。此字段旨在降低终端设备上登录尝试发生的速率。

`t_maxtries#10` 此选项指定在终端被锁定之前，使用该终端允许的最大连续失败登录尝试次数。终端一旦被锁定，必须由授权管理员解锁。有关其他信息，请参阅 `default(4)` 的手册页。

## 运行 secsetup 实用程序

`secsetup` 实用程序是一个交互式程序，可在 DU 系统上在基本安全和增强安全之间切换。您必须准备好回答以下问题，除选择所需的系统安全级别外。

- 您是否希望禁用段共享？
- 您是否希望此时运行审计设置实用程序？

通常，除非您有特殊要求，否则这两个问题的答案均为否。有关这些选项的更多信息，请参阅 DEC OSF/1 安全手册。

以下显示了一个示例 `secsetup` 会话，其中安全级别从 Base 更改为 Enhanced。

```
# /usr/sbin/secsetup
Enter system security level {BASE ENHANCED ?}[ENHANCED]: <RETURN>
ENHANCED security level will take effect on the next system reboot.
Do you wish to disable segment sharing?(yes no ?)[no]: <RETURN>
Do you wish to run the audit setup utility at this time?(yes no ?)[no]: <RETURN>
Press return to continue: <RETURN>
#
```

请注意，每个提示的默认答案都在方括号中，只需按 Return 键即可选择。

## 重启系统以启用增强安全

在新的安全级别更改生效之前，必须重新启动系统。以下命令是实现此目的的一种简单方法。

```
# /sbin/shutdown -r +2 "System being rebooted to enable Enhanced Security."
```

这将在两分钟宽限时间内关闭并重新启动系统，并向任何已登录用户显示一条信息性消息。

## 调整系统默认数据库文件

系统成功重新启动后，以 root 身份登录并按如下方式对系统默认数据库文件进行之前记录的调整。

```
# cd /etc/auth/system
# cp default default.orig
# vi default (and apply desired changes)
```

## 从 /etc/passwd 中删除加密密码字符串

`secsetup` 实用程序已将 `/etc/passwd` 的密码字段中的加密密码复制到 `/tcb/files/auth` 层次结构下的各个用户安全数据库中。但是，`secsetup` 并未从 `/etc/passwd` 中删除加密密码。当在系统上安装增强安全时，密码字段应包含星号 `*`，因为加密密码不再存储在 `/etc/passwd` 中。一个小型 Korn shell 脚本可安全地从 `/etc/passwd` 的密码字段中删除加密密码字符串并将其替换为星号，如清单 18.1 所示。

### 清单 18.1 remove_passwd.ksh — 一个 Korn shell 脚本，用于将 /etc/passwd 的密码字段中的加密密码字符串替换为星号。

```
#!/bin/ksh
# Short script to replace the encrypted password
# strings in /etc/passwd with an asterisk (*)

if test ! -w /etc/passwd
then
    print 'Please su to root first.'
    exit 1
fi

trap 'rm -rf /etc/ptmp ; exit 1' 1 2

if [[ `rcmgr get SECURITY` = BASE ]]
then
    print 'Security Level is not ENHANCED.'
    exit 1
fi

if mkdir /etc/ptmp
then
    :
else
    print 'The /etc/passwd file is busy. Try again later.'
    exit 1
fi
```

## 测试您的应用程序

此时，您的系统正在运行增强安全，您应在宣布成功之前适当地测试您的应用程序。在用户尝试登录并可能违反系统规则之前，请注意，如果任何用户在基本安全下的密码长于八个字符，则现在只接受前八个字符作为有效密码。例如，如果密码为 `toogood2be`，则用户必须仅输入 `toogood2` 才能成功登录。当用户在增强安全下更改其密码时，全局或用户默认值，如果不同，将决定密码长度。请确保您的用户在登录到新启用的增强安全系统之前了解此密码问题。
