

auth sufficient /lib/security/$1SA/pam_unix.so likeauth nullok
auth required /lib/security/$1SA/pam_deny.so
account required /lib/security/$1SA/pam_unix.so
password required /lib/security/$1SA/pam_cracklib.so retry=3 type=
password sufficient /lib/security/$1SA/pam_unix.so nullok use_authtok md5 shadow
password required /lib/security/$1SA/pam_deny.so
session required /lib/security/$1SA/pam_limits.so
session required /lib/security/$1SA/pam_unix.so

以下是配置文件中部分行的简要说明：

- 第一行 auth 行加载了 PAM 模块 /lib/security/pam_env.so。该模块可以设置或取消设置环境变量（/lib/security/$1SA/pam_env.so 中的 $1SA 指代一个通常未定义的环境变量，因此 PAM 模块的有效路径名为 /lib/security/pam_env.so）。
- 第二行 auth 行指定了一个认证模块，该模块使用 PAM 模块 /lib/security/pam_unix.so 和参数字符串 likeauth nullok 来检查用户身份。参数字符串中的选项含义如下：
  - likeauth：无论模块是用于设置新凭证还是认证现有用户名，都返回相同的值。
  - nullok：允许使用空白密码。
- /etc/pam.d/system-auth 文件中的第三行 auth 行规定，如果 pam_unix.so 模块的认证不成功，则拒绝访问系统。
- /etc/pam.d/system-auth 文件中的 account 行检查用户账户是否已过期、用户是否被允许在特定时间登录等。
- /etc/pam.d/system-auth 文件中的接下来两行 password 行指定了如何设置密码：
  - 第一行 password 行使用 /lib/security/pam_cracklib.so 模块尝试破解新密码（这正是模块名称中 cracklib 所指示的）。
  - retry=3 部分表示用户最多可以尝试输入新密码三次。第二行 password 行表示使用 MD5 加密将密码存储在 /etc/shadow 文件中。

当设置完 /etc/pam.d/passwd 配置文件后，当你使用 passwd 命令更改密码时，你的选择将生效。下面是一个示例，说明我试图更改我的密码（我的注释以斜体显示）：

```
passwd
Changing password for user naba.
Changing password for naba
(current) UNIX password: 我输入我的当前密码
New password: 我输入 "xyz" 
BAD PASSWORD: it is too short
New password: 我将 "transport" 作为密码
BAD PASSWORD: it is based on a dictionary word
New password: 我将 "naba12" 作为新密码
BAD PASSWORD: it is based on your username
passwd: Authentication token manipulation error
```

在这种情况下，`passwd` 程序使用 PAM 模块来检查我的身份（当我第一次输入当前密码时），并确保我尝试的每个新密码都是强密码。最后，当我在三次尝试中都未能选择一个好密码后，PAM 模块终止了 `passwd` 程序。

# 保护文件和目录

保护主机安全的一个重要方面是保护重要的系统文件——以及包含这些文件的目录。你可以通过文件所有权以及控制谁可以读取、写入或（对于可执行程序）执行文件的权限设置来保护文件。

默认的 Fedora Core 文件安全由以下设置针对每个文件或目录进行控制：

- 用户所有权
- 组所有权
- 所有者的读、写、执行权限
- 组的读、写、执行权限
- 其他人（其他所有人）的读、写、执行权限

# 查看所有权和权限

当你使用 `ls -l` 命令查看详细列表时，你可以看到文件的这些设置。例如，输入以下命令查看 `/etc/inittab` 文件的详细列表：

```
ls -l /etc/inittab
```

生成的列表看起来像这样：

```
-rw-r--r-- 1 root root 1666 Feb 16 07:57 /etc/inittab
```

第一组字符描述了用户、组和其他人的文件权限。第三个和第四个字段显示了拥有此文件的用户和组。在这种情况下，用户名和组名都是：`root`。

## 更改文件所有权

你可以使用 `chown` 命令设置用户和组的所有权。例如，如果文件 /dev/hda 由用户 `root` 和组 `disk` 拥有，那么作为 `root` 输入以下命令来设置此所有权：

```
chown root.disk /dev/hda
```

如果仅更改组所有权，请使用 `chgrp` 命令。例如，以下是如何将文件的组所有权更改为名为 `accounting` 的组：

```
chgrp accounting ledger.out
```

## 更改文件权限

使用 `chmod` 命令设置文件权限。要有效地使用 `chmod`，你必须指定权限设置。一种方法是将下表中的一个或多个字母按所示顺序（Who/Action/Permission）连接起来，如表 2-1 所示。

| **Who** | **Action** | **Permission** |
| :--- | :--- | :--- |
| u user | + add | r read |
| g group | - remove | w write |
| o others | = assign | x execute |
| a all | s set user ID | |

若要授予目录中所有文件以读取和写入权限，请输入 `chmod a+rw *`。另一方面，若要允许所有人执行特定文件，请输入 `chmod a+x filename`。

指定权限设置的另一种方法是使用三位数字序列。在详细列表中，用户、组和其他人的读、写和执行权限设置显示为序列

```
rwxrwxrwx
```

对于不允许的操作，用破折号代替字母。将 `rwx rwx rwx` 视为字符串 `rwx` 的三次出现。现在分配值 r=4，w=2，x=1。要获取序列 `rwx` 的值，只需将 r、w 和 x 的值相加。因此，`rwx` = 7。使用此公式，你可以为任何权限设置分配三位数值。例如，如果用户可以读取和写入文件，但其他人只能读取文件，则权限设置为 `rw- r-- r--`（这就是它在列表中的显示方式），值为 644。因此，如果你希望目录中的所有文件都可以被所有人读取，但只有用户可以写入，请使用以下命令：

```
chmod 644 *
```

# 设置默认权限

当你（或程序）创建一个新文件时，该文件获得什么权限设置？答案在于众所周知的用户文件创建掩码，你可以使用 `umask` 命令查看和设置它。

输入 `umask`，它会打印出一个显示当前文件创建掩码的数字。默认设置对于 *root* 用户和其他普通用户是不同的。对于 *root* 用户，掩码设置为 022，而对于普通用户，掩码为 002。要查看此文件创建掩码的效果并解释掩码的含义，请遵循以下步骤：

1. **以 *root* 身份登录并输入以下命令：**
   ```bash
   touch junkfile
   ```
   此命令创建一个名为 `junkfile` 的文件，其中没有任何内容。

2. **输入 `ls -l junkfile` 以查看该文件的权限。**
   你会看到类似以下的一行：
   ```
   -rw-r--r-- 1 root root 0 Aug 24 10:56 junkfile
   ```

3. **从数值权限设置 666 中减去，得到的就是 *umask* 设置。**
   在这种情况下，666 - 644 得出的 `umask` 为 022。

通过将第一字段中每个三个字母的权限（不包括最开始的第一个字母）转换为 0 到 7 之间的数字来解释权限设置的数值。对于存在的每个字母，第一个字母的值为 4，第二个字母为 2，第三个为 1。例如，`rw` 转换为 4+2=6（因为第三个字母缺失）或 6。同样，`r-` 是 4+0+0 = 4。因此权限字符串 `rw- r-- r--` 变为 644。

因此，`umask` 为 022 会导致默认权限设置为 666-022 = 644。当你将 644 重写为权限字符串时，它变为 `rw- r-- r--`。

