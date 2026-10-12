
# 利用程序标题

| 利用程序标题 | 路径 (`\usr/share/exploitdb/`) |
|---|---|
| MySQL (Linux) - Database Privilege Escalation | `exploits/linux/local/23077.pl` |
| MySQL (Linux) - Heap Overrun (PoC) | `exploits/linux/local/23076.pl` |
| MySQL (Linux) - Stack Buffer Overrun (PoC) | `exploits/linux/dos/23075.pl` |
| MySQL 3.x/4.x - ALTER TABLE/RENAME Forces Old Permi... | `exploits/linux/remote/24669.txt` |
| MySQL 4.0/4.1 (Linux) - User-Defined Function (UDF)... | `exploits/linux/local/11181.c` |
| MySQL 4.1.18/5.0 - Auth - Local/Remote Information Leak | `exploits/linux/remote/1742.c` |
| MySQL 4.1/5.0 - Authentication Bypass | `exploits/multiple/remote/24250.pl` |
| MySQL 4.1/5.0 - Zero-Length Password Authentication | `exploits/multiple/remote/311.pl` |
| MySQL 4.x - CREATE FUNCTION Arbitrary libc Code Exe... | `exploits/multiple/remote/25209.pl` |
| MySQL 4.x - CREATE FUNCTION mysql.func Table Arbitr... | `exploits/multiple/remote/25210.php` |
| MySQL 4.x - CREATE Temporary TABLE SymLink Priviled... | `exploits/multiple/remote/25211.c` |
| MySQL 4.x/5.0 (Linux) - User-Defined Function (UDF) | `exploits/linux/local/1518.c` |
| MySQL 4.x/5.0 (Windows) - User-Defined Function Com... | `exploits/windows/remote/2374.txt` |
| MySQL 4/5 - Server Date_Format Denial of Service | `exploits/linux/dos/28234.txt` |
| MySQL 4/5 - SUID Routine Miscalculation Arbitrary D... | `exploits/linux/remote/28398.txt` |
| MySQL 4/5/6 - UDF For Command Execution | `exploits/linux/local/7856.txt` |
| MySQL 5 - Command Line Client HTML Special Character... | `exploits/linux/remote/32445.txt` |
| MySQL 5.0.18 - Query Logging Bypass | `exploits/linux/remote/27326.txt` |
| MySQL Squid Access Report 2.1.4 - HTML Injection | `exploits/php/webapps/20955.txt` |
| MySQL Squid Access Report 2.1.4 - SQL Injection / C... | `exploits/php/webapps/44483.txt` |
| MySQL User-Defined (Linux) (x32/x86_64) - 'sys'... | `exploits/linux/local/46249.py` |
| MySQL yaSSL (Linux) - SSL Hello Message Buffer Over... | `exploits/linux/remote/16849.rb` |
| MySQL yaSSL (Windows) - SSL Hello Message Buffer Ov... | `exploits/windows/remote/16701.rb` |

# 论文标题

| 论文标题 | 路径 (`\usr/share/exploitdb-papers`)/ |
|---|---|
| MySQL Session Hijacking over RFI | `docs/english/13708-mysql-session-hijacking-ove...` |
| MySQL UDF Exploitation | `docs/english/44139-mysql-udf-exploitation.pdf` |
| MySQL: Secure Web Apps - SQL Injection | `papers/english/12945-mysql-secure-web-apps-s...` |
| Nobel contributions to the field - Ho... | `docs/english/40143-nobel-contributions-to-the-...` |

# 列表 905 - SearchSploit 搜索 MySQL

在搜索 MySQL 漏洞时，我们必须稍微改变一下方法。这一次，我们不是在寻找可能容易受到某个利用程序攻击的确切版本号，因为 MariaDB 和 MySQL 使用不同的版本号。相反，我们试图通过识别公开披露的利用程序中的模式，来判断我们是否可以使用某种类型的攻击。

我们注意到"`UDF`"和"`User Defined`"这两个词经常出现。让我们看看在 `/usr/share/exploitdb/exploits/linux/local/46249.py` 中发现的一个较新的 UDF 利用程序。

```python
# Exploit Title: MySQL User-Defined (Linux) x32 / x86_64 sys_exec function local privilege escalation exploit

# Date: 24/01/2019

...

References:

    https://dev.mysql.com/doc/refman/5.5/en/create-function-udf.html

    https://www.exploit-db.com/exploits/1518

    https://www.exploit-db.com/papers/44139/ = MySQL UDF Exploitation by Osanda Malith Jayathissa (@OsandaMalith)
```

该利用程序一开始就引用了关于 UDF 利用的其他研究，包括一篇就此主题撰写的论文。

审阅这篇论文教会我们，用户定义函数（UDF）类似于 MySQL 的自定义插件。它允许数据库管理员创建可重用的自定义函数以实现特定目标。对我们来说很方便的是，UDF 是用 C 或 C++[^2] 编写的，并且可以运行我们想要的几乎任何代码，包括系统命令。

研究人员发现了如何使用标准的 MySQL（以及 MariaDB）功能以可以利用系统的方式创建这些插件。这个特定的利用程序讨论了使用 UDF 作为提升主机权限的方式。然而，我们应该能够使用相同的原则来获取初始 shell。需要进行一些修改，但在我们开始更改任何东西之前，让我们先看看代码。

```python
shellcode_x32 = "7f454c460101010000000000000000...";

shellcode_x64 = "7f454c46020101000000000000000000...";

shellcode = shellcode_x32

if (platform.architecture()[0] == '64bit'):

    shellcode = shellcode_x64

...

cmd='mysql --u root -p\'' + password + '\'-e "select @@plugin_dir \'\''"'

plugin_str = subprocess.check_output(cmd, shell=True)

plugin_dir = re.search('(@plugin_dir: (\*))', plugin_str)

res = bool(plugin_dir)

...

    print("Trying to create a udf library...");
```
