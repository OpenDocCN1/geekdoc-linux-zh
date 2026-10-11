
```
total 9094
drwxr-xr-x 2 root               1024 Nov  8 18:37
drwxr-xr-x 28 root               3072 Jan 22 23:57
drwxr-xr-x  1 root               230 230 Nov  8 15:40 chfn
-rw-r--r--  1 root                580 230 Nov  8 15:48 flpd
-rw-r--r--  1 root                437 230 Nov  8 23:54 gdm
-rw-r--r--  1 root                500 230 Nov  8 15:46 login
-rw-r--r--  1 root                443 230 Nov  9 09:49 other
-rw-r--r--  1 root               258 230 Nov  8 15:40 password
-rw-r--r--  1 root               311 230 Nov  8 16:52 pomp
-rw-r--r--  1 root               265 230 Nov  8 14:52 root
-rw-r--r--  1 root               292 230 Nov  8 14:30 rsh
-rw-r--r--  1 root               108 230 Nov  8 17:05 us
-rw-r--r--  1 root                60 230 Nov  8 17:16 sudo
-rw-r--r--  1 root               265 230 Nov  8 08:57 xdm
-rw-r--r--  1 root                 67 230 Nov  8 17:53 vck
-rw-r--r--  1 root                 67 230 Nov  8 17:59 screensaver
```

```
#PAM-1.0
auth    required      /lib/security/pam_unix.so  nullok
account required      /lib/security/pam_unix.so
password required      /lib/security/pam_unix.so  strict=false
session required      /lib/security/pam_unix.so
```

每个 `/etc/pam.d` 条目的语法由如下格式的独立行组成：

`module-type` 可以是四种之一：`auth`, `account`, `session`, `password`。`control-flag` 告诉如何响应成功或失败。`module-path` 是可加载模块的路径。`args` 是传递给模块的令牌。

左侧列显示文件类型及其权限。第一个字符 - 表示普通文件。如果该字符是 d，则文件类型为目录。字母 l 表示链接。

其余九列指定了所有者、组和“世界”的权限。这些字符中的每一个都有三组：r 表示读取，w 表示写入，x 表示执行。如果字母存在，则权限被视为开启；否则，它是关闭的并由 - 字符表示。

考虑上一个列表中的 debugfs。debugfs 的条目权限为 rwxr-xr-x，为所有者产生 rwx，为组和“世界”产生 r-x。

加密提供了另一层安全保护。Kerberos 认证是接下来要讨论的第一种加密形式，它提供了强效的安全。

# Kerberos 认证

Kerberos 开发于20 世纪 80 年代中麻省理工学院（MIT），用作分布式认证服务。当用户登录系统时，Kerberos 会对用户进行认证。如果网络上的主机或服务器需要认证，Kerberos 提供了一种证明用户身份的方法。通过 Kerberos，客户端进程代表用户运行。该进程被用于证明用户的身份。Kerberos 在不向网络发送数据的情况下完成此操作，从而防止了攻击者获取密码或认证包。

Kerberos 通过通过为网络用户分配一个唯一密钥来实现认证。这个唯一密钥被称为票据（ticket）。随后，票据被嵌入网络消息中以通知发送者。

欺骗（Spoofing）一直是一个网络安全问题。欺骗是指客户端欺骗服务器使其认为客户端是别人的行为。Kerberos 在这方面提供了帮助，可以防止用户对系统进行欺骗。

你可以在 `http://web.mit.edu/kerberos/www` 找到更多关于 Kerberos 的信息。

# 可插拔认证模块 (PAM)

系统中使用最基础的认证和授权方法是用户名和密码。当你登录时，输入用户名，系统会要求你验证是否提供了正确的密码。如果匹配成功，系统将授权你访问系统。此时，你的环境将进行调整，以反映你在认证点时的授权级别。

可插拔认证模块 (PAM) 是一个实现为共享库套的系统，允许系统管理员选择应用程序如何执行用户认证。PAM 允许你更改认证方法，并以可加载模块的形式提供此功能。因此，你可以在不重写和重新编译 PAM 应用程序的情况下切换认证机制。这意味着你可以在不修改 PAM 应用程序的情况下完全修改你的认证系统。

以下列出了 PAM 的一些亮点：

- 你可以在系统运行的特定时段内识别特定的用户登录系统。
- 你可以为用户设置资源限制（内存量、最大进程数等），从而禁用拒绝服务攻击。拒绝服务攻击是指攻击者试图让资源过忙，使其无法回答合法的网络请求，或尝试拒绝对你机器的合法访问。
- 你可以使用 DES 以外的密码加密方法。
- 你可以完全启用影子密码。

PAM 库通过 `/etc/pam.d` 目录下的组合文件进行本地配置。动态加载的模块通常位于 `/usr/lib/security` 目录。旧版本的 Linux 使用 `/etc/pam.conf` 文件配置 PAM。以下是 SUSE 6.3 下 `/etc/pam.d` 中的其中一个；其他可能将文件位于另一个目录树。

```bash
bash~2.03# ls -al
drwxr-xr-x 2 root               1024 Nov  8 18:37
drwxr-xr-x 28 root               3072 Jan 22 23:57
drwxr-xr-x  1 root               230 230 Nov  8 15:40 chfn
-rw-r--r--  1 root                580 230 Nov  8 15:48 flpd
-rw-r--r--  1 root                437 230 Nov  8 23:54 gdm
-rw-r--r--  1 root                500 230 Nov  8 15:46 login
-rw-r--r--  1 root                443 230 Nov  9 09:49 other
-rw-r--r--  1 root               258 230 Nov  8 15:40 password
-rw-r--r--  1 root               311 230 Nov  8 16:52 pomp
-rw-r--r--  1 root               265 230 Nov  8 14:52 root
-rw-r--r--  1 root               292 230 Nov  8 14:30 rsh
-rw-r--r--  1 root               108 230 Nov  8 17:05 us
-rw-r--r--  1 root                60 230 Nov  8 17:16 sudo
-rw-r--r--  1 root               265 230 Nov  8 08:57 xdm
-rw-r--r--  1 root                 67 230 Nov  8 17:53 vck
-rw-r--r--  1 root                 67 230 Nov  8 17:59 screensaver
bash~2.03#
```

以下列表显示了 `/etc/pam.d/passwd` 文件的内容，取自之前的列表：

```
#PAM-1.0
auth    required      /lib/security/pam_unix.so  nullok
account required      /lib/security/pam_unix.so
password required      /lib/security/pam_unix.so  strict=false
session required      /lib/security/pam_unix.so
```

每个 `/etc/pam.d` 条目的语法由如下格式的行组成：
