
# make install

```
Installing OPIE server software...
Copying OPIE user programs
Changing ownership
Changing file permissions
Installing OPIE system programs...
Renaming existing /bin/login to /bin/login.opie.old
Clearing permissions on old /bin/login
Copying opielogin to /bin/login
Changing ownership of /bin/login
Changing file permissions of /bin/login
Renaming existing su to su.opie.old
Clearing permissions on old su
Copying opieusd to su
Changing ownership of su
Changing file permissions of su
Copying OPIE ftp daemon
Changing ownership of ftpd
Changing file permissions of ftpd
Making sure OPIE database file exists
Changing permissions of OPIE database file
Changing ownership of OPIE database file
Creating OPIE lock directory
Installing manual pages
REMEMBER to run opiepasswd on your users immediately.
#
```

> 注意

> 我们本可以跳过第 137 页示例 6-19 中的 `make`，直接如示例 6-20 所示执行 `make install` 来完成这两个步骤。

### 实施和使用 OPIE

在本节中，我们将查看 OPIE OTP 程序 `opiepasswd` 和 `opiekey`。然后我们将查看一些与第 121 页 *S/Key Version 1.1b* 中出现的类似示例。

使用 OPIE 初始化用户和管理 OTP 列表的过程与 S/Key 非常相似。在 OPIE 中，服务器端程序是 `opiepasswd`，而不是 `keyinit`。客户端程序是 `opiekey`，而不是 `key`。

正如示例 6-20 底部所指出的，我们需要做的第一件事是使用 `opiepasswd` 来初始化我们的用户。与仅提供 *-s* 选项的 `keyinit`（参见示例 6-13）不同，`opiepasswd` 提供了多个选项，如表 6.4 所述。

| 选项 | 描述 |
|---|---|
| `-v` | 显示版本和编译时选项。 |
| `-h` | 显示帮助信息。 |
| `-c` | 设置控制台模式。请求秘密短语，而不是强制使用本地 OTP 生成器。如果通过不安全的连接请求，将自动失败，除非包含编译时选项 `--enable-insecure-override`。 |
| `-d` | 禁用指定账户的 OTP 登录。任何用户都可以禁用其自己的账户。只有 `root` 可以禁用其他用户的账户。此选项只是在 `/etc/opiekeys` 中为用户的最后一个 OTP 输入一个无效字符串。当用户确定其秘密短语已泄露时，此选项特别有用。 |
| `-f` | 强制 `opiepasswd` 通过不安全通道继续运行。仅在编译时包含 `--enable-insecure-override` 时才有效。不推荐。 |
| `-n sequence number` | 手动指定初始序列号。默认为 499。 |
| `-s seed` | 手动指定种子。通常种子是伪随机生成的。不推荐。 |
| `username` | 可选地指定用户。只有 `root` 可以成功使用此选项。 |

`opiekey` 程序是 OTP 生成程序。与它的 S/Key 对应物 *key* 不同，`opiekey` 有若干可用选项，如表 6.5 所述。

| 选项 | 描述 |
|---|---|
| `-4` | 生成 MD4 列表。MD4 列表与 S/Key Version 1.1b 兼容。注意：`opiekey -4` 等同于 `otp-md4`。 |
| `-5` | 生成 MD5 列表。注意：`opiekey -5` 等同于 `otp-md5`。 |
| `-v` | 显示版本和编译时选项。 |
| `-h` | 显示帮助信息。 |
| `-f` | 强制 `opiekey` 通过不安全通道继续运行。仅在编译时包含 `--enable-insecure-override` 时才有效。不推荐。 |
| `-n count` | 指定要打印的一次性密码数量。默认为一个。 |
| `-x` | 以十六进制记数法输出 OTP。 |
| `-t type` | 使用 RFC2243 中定义的扩展响应代码。 |
| `-a` | 允许任意的秘密短语（不进行任何检查）。尚未实现。 |
| `sequence number` | 必需参数。请求的序列号，通常从 OTP 挑战中获得。这是将在列表中显示的 OTP 的编号。 |
| `seed` | 必需参数。与您正在计算的列表相关联的种子。通常从 OTP 挑战中获得。 |

既然我们已经描述了两个基本命令，让我们来看一些示例。再次，我们将系统管理员称为 *bill*，我们的示例用户将是 *mary*。我们的服务器系统将是 *topcat*。与之前一样，Mary 或 Bill 都可以使用 `opiepasswd` 命令来初始化或重新初始化 Mary 的 OTP 列表。作为 `root`，Bill 在示例 6-21 中于 `topcat` 系统控制台初始化用户 `mary`。当然，Bill 必须告诉 Mary 他使用了什么秘密短语，这样她才能使用 `opiekey` 生成一个列表。OPIE 秘密短语的长度必须在 10 到 127 个字符之间。假设 Bill 告诉 Mary 该短语是什么，她现在可以通过在一个窗口中执行 `telnet`、`rlogin` 或 `ftp`，并在另一个窗口中使用 `opiekey` 计算 OTP 来登录 `topcat`。这两个步骤分别如示例 6-22 和示例 6-23 所示。正如第 129 页的示例 6-11 和 6-12 所描述的那样，Mary 首先在一个窗口中执行 `telnet`，如示例 6-22 所示。当她在登录提示符下输入用户名后，OPIE 请求 OTP 序列号 498 和种子 `to0967`。在另一个窗口中，如示例 6-23 所示，她使用 `opiekey`，以序列号和种子作为参数，然后在提示时输入她的秘密密码。这导致 `opiekey` 计算出适当的 OTP，然后她从示例 6-23 中剪切并粘贴到示例 6-22 的 `Response:` 提示符下。现在她已登录到 `topcat`。

## 示例 6-21 管理员在控制台初始化 OPIE 用户

```
# opiepasswd -c mary
Adding mary:
Only use this method from the console: NEVER from remote. If you are
using telnet, xterm, or a dial-in, type ^C now or exit with no password.
Then run opiepasswd without the -c parameter.
Using NDS to compute responses.
Enter new secret pass phrase:
Again new secret pass phrase:
ID mary OTP key is 499 to0967
HOME BOHR COIN HUM BUFF RAT
```

## 示例 6-22 Mary 从 roadrunner telnet 到 topcat

```
roadrunner$ telnet topcat
Trying 172.19.31.104...
Connected to topcat.
Escape character is ‘^]’.
Red Hat Linux release 5.2 (Apollo)
Kernel 2.0.36 on an i686
login: mary
otp-md5 498 to0967 ext
Response: USES LUGE BALM PAN KANE NUT
[mary@topcat]$ 
```

## 示例 6-23 Mary 使用 opiekey 计算 OTP

```
roadrunner$ opiekey 498 to0967
Using the MD5 algorithm to compute response.
Reminder: Don't use opiekey from telnet or dial-in sessions.
Enter secret pass phrase:
USES LUGE BALM PAN KANE NUT
roadrunner$ 
```

### 注意
