
## 538 保护密码

MD5 相比旧式密码加密的另一个优势是，旧密码限制为最多八个字符；而新密码（使用 MD5 加密）可以长得多。更长的密码更难破解，即使 `/etc/shadow` 文件落入他人之手也是如此。

你可以判断出 `/etc/shadow` 文件正在使用 MD5 加密。加密后的密码更长，并且在以下示例条目的第二个字段中都以 `$1` 开头：

```
root:$AAANi/ynEShYbUp9qc8foibD5O:1107:0:9999:-1:134540356
```

名为可插拔认证模块（PAM）的程序模块执行实际的 MDS 加密。Fedora Core PAM 提供了一种灵活的用户身份验证方法。通过设置 PAM 配置文件，你可以更改文件的身份验证方法，而无需修改验证用户身份的内核程序（如 `login` 和 `passwd`）。

Fedora Core 广泛使用了 PAM 功能。PAM 存在于许多不同的模块中（大约是如此）；它们的配置文件位于系统的 `/etc/pam.d` 目录下。你可以通过输入以下命令检查该目录的内容：

```
/etc/pam.d
```

此目录中的每个配置文件指定了如何对特定实用程序进行用户验证。例如，你会发现用于 `login`、`passwd` 等的文件。以下是我在系统上输入 `cat /etc/pam.d/passwd` 时看到的内容：

```
#PAM-1.0
auth required pam_stack.so service=system-auth
account required pam_stack.so service=system-auth
password required pam_stack.so service=system-auth
```

这些行表示身份验证、账户管理和密码检查都是通过使用参数 `service=system-auth` 的 `pam_module` (`/lib/security/pam_stack.so`) 完成的。本质上，pam_module 指向 `/etc/` 目录下的另一个配置文件。在这种情况下，配置文件是我 Fedora 电脑上的 `/etc/pam.d/system-auth` 文件：

```
#PAM-1.0
# 此文件是自动生成的。
# 用户更改将在下次运行 auth config 时被覆盖。
auth required /lib/security/$ISA/pam_env.so
```

## 保护密码

```
auth sufficient /lib/security/$ISA/pam_unix.so wellknown nullock
auth required /lib/security/$ISA/pam_deny.so
account required /lib/security/$ISA/pam_unix.so
password required /lib/security/$ISA/pam_cracklib.so retry=3 type=
password sufficient /lib/security/$ISA/pam_unix.so nullock authtok md5
password required /lib/security/$ISA/pam_deny.so
session required /lib/security/$ISA/pam_limits.so
session required /lib/security/$ISA/pam_unix.so
```

以下是配置文件中某些行的简要解释：

- 第一行 `auth` 载入了 PAM 模块 `/lib/security/pam_env.so`。该模块可以设置或取消环境变量（`/lib/security/$ISA/pam_env.so` 中的 `$ISA` 指的是通常未定义的环境变量，因此 PAM 模块的有效路径为 `/lib/security/pam_env.so`）。
- `auth` 行指定了一个身份验证模块，该模块使用参数 `wellknown nullock` 通过 PAM 模块 `/lib/security/pam_unix.so` 检查用户身份。参数字符串中的选项如下：
    - wellknown: 无论该模块是用于设置新凭据还是验证现有用户名，都返回该值。
    - nullock: 允许空密码。
- `/etc/pam.d/system-auth` 文件中的第三行 `auth` 会在 `pam_unix.so` 模块身份验证失败时拒绝访问。
- `/etc/pam.d/system-auth` 文件中的 `account` 行检查用户账户是否过期、是否允许在一天任何时间登录等。
- `/etc/pam.d/system-auth` 文件中的后续两行 `password` 行指定了如何设置密码：
    - 第一行 `password` 使用 `/lib/security/pam_cracklib.so` 模块来创建新密码（如该模块名称所示）。
    - `retry=3` 表示用户最多可以尝试输入三次密码。
    - 第二行 `password` 表示使用 MD5 加密来存储 `/etc/shadow` 文件中的密码。

| 书 VII |
| :--- |
| 第 2 章 |

当你完成 `/etc/pam.d/passwd` 配置文件的设置后，当你使用 `passwd` 命令更改密码时，你的选择就会生效。这里有一个尝试更改密码的示例（注释以*斜体*显示）：![](img/d923b0f1dc0ef80851f63d6f57_0.png)

## 540 保护文件和目录

```
passwd
为用户 naba 更改密码。
为 naba 更改密码 (current) UNIX 密码: 输入 "xyz"
bad: 密码太短
新密码: 输入 "transport" 
bad: 密码基于字典
新密码: 输入 "naba12"
bad: 密码基于你的用户名
passwd: 身份验证令牌错误
```

在这种情况下，`passwd` 程序使用 PAM 模块检查身份（当我第一次输入当前密码时），并确保每个密码都是强。最后，如果尝试未能选择良好的密码，PAM 模块将中止程序。

## 保护文件和目录

保护主机的一个重要方面是保护系统文件和包含这些文件的目录。你可以通过所有权权限设置来保护文件，这些设置控制谁可以读取、写入或执行文件。

Fedora Core 安全通过每个文件或目录的以下设置控制：

- 用户所有权
- 组所有权
- 所有者的读、写、执行权限
- 组的读、写、执行权限
- 其他（所有人）的读、写、执行权限

## 查看所有权权限

当你使用 `ls -l` 命令查看列表时，可以看到文件的这些设置。例如，输入以下命令查看 `/etc/passwd` 的详细列表：

```
ls -l /etc/passwd
```

结果列表如下：

```
-rw-r--r--  1 root root  0 Aug 24 10:56 /etc/passwd
```

## 保护文件和目录

第一组字符描述用户、组和其他人的权限。第三和第四字段显示所有文件的用户和组。在这种情况下，用户和组名相同：root。

## 修改所有权

你可以使用 `chown` 命令设置所有权。例如，如果 `/etc/passwd` 文件的用户是 root，组是 disk，则以 root 身份输入以下命令设置此类所有权：

```
chown root /etc/passwd
```

要单独更改组所有权，使用 `chgrp` 命令。例如，以下是如何将文件的组所有权改为 accounting：

```
chgrp accounting /etc/passwd
```

## 修改权限

使用 `chmod` 命令设置权限设置。要有效使用 `chmod`，必须按照表 2-1 所示顺序（对象/动作/权限）指定下表的字母权限：

| 表 2-1 | 动作 | 权限 |
| :--- | :--- | :--- |
| u user | + | r  |
| g group | - | w 写 |
| others | = | x 执行 |
| a all | s | 设置用户 ID |

你可以通过 `chmod a+rw *` 读取并访问目录中的所有文件。另一方面，执行 `文件 +允许 ` +特定`。另一种另一种指定权限设置的方法是使用三位数字序列。在详细列表中，用户、组和其他人的读、写、执行权限显示为序列：

```
rwx rwx rwx
```

## 542 保护文件和目录

当用连字符代替不允许的操作字母时，请将 `rwxrwxrwx` 视为字符串 `rwx` 出现了三次。分配值 r=4, w=2, x=1。要获得序列 `rwx` 的值，只需将 r、w 和 x 的值相加。因此 `rwx = 7`。使用此公式，你可以为任何权限设置分配一个三位值。例如，如果你可以读写文件，但其他人只能读取文件，则权限为 `rw-r----`（这是在列表中显示的方式），其值为 644。因此，如果你希望目录中的所有文件所有人都可以读取，但只有你可以写入，请使用以下命令：

```
chmod 644 *
```

## 设置默认权限

当你（或程序）创建新文件时，文件会获得什么权限？答案是用户文件创建掩码，你可以使用 `umask` 命令查看和设置它。

**输入 umask**，它会输出当前文件创建掩码的数字。默认设置适用于 root 用户和其他普通用户。root 用户用户设置为 022，而普通用户的掩码为 002。要查看此文件创建掩码的效果并解释其含义，请遵循以下步骤：

1. 以 root 身份登录并输入以下命令：

```
touch junkfile
```

此命令创建一个名为 `junkfile` 的空文件。

2. 输入 -l 查看文件的权限。

你会看到类似的一行：

```
-rw-r--r--  1 root root  0 Aug 24 10:56 junkfile
```

通过将第一个字段（排除第一个）中的每个三字母权限转换为 0 到 7 的数字来解释设置的数值。对于每个字母，第二个字母是 4，第三个是 1。例如，`rw-` 转换为 4+2+0（因为缺少第三字母）或 6。同样，`r--` 是 4+0+0=4。权限字符串 `-rw-r--r--` 变为 644。

3. 从 666 减去数值，得到的 umask 设置。

在这种情况下，666-644 得到 umask 为 022。

因此，umask 为 022 导致默认权限设置为 666-022=644。当你将 644 重写为权限字符串时，它变成了 `rw-r--r--`。
