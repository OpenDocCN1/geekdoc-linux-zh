

但是，请避免使用 root 账户或任何等同于超级用户的账户来执行日常任务，例如发送电子邮件、浏览网页、运行 IRC 客户端与朋友或同事交谈、通过 FTP 传输文件等。

![](img/f9ec99365f159bfe663f8ac29732663c_447_0.png)

**提示**
有时，新系统管理员会疑惑为什么他们无法以 root 用户身份 Telnet 到系统。原因在于 */etc/securetty* 文件指定了哪些 tty 设备可用于 root 登录。通常，*/etc/securetty* 将 *tty[0-8]* 列为允许的设备。因为 Telnet 访问将使用伪 tty 设备 *pty[0-f]*，所以 root 无法通过 Telnet 登录。请保持 */etc/securetty* 原样。

- 请勿从任何地方以 root 或等效超级用户身份登录。执行管理任务的首选方法是以普通用户身份登录，然后使用 *su* 命令切换为超级用户（如 root）。这能降低对系统造成意外损坏的几率。

![](img/f9ec99365f159bfe663f8ac29732663c_447_1.png)

**提示**
运行 *su* 命令时带上 *--* 参数，这样会使 shell 成为登录 shell，进而会使 shell 读取 shell 启动文件（如 *.bashrc*）。该参数还会使 *su* 将目录切换到用户的主目录。

- 如果您遇到其他人需要超级用户访问权限来完成工作的情况，请考虑使用 *sudo*，而不是给每个人一个超级用户账户。如果其他人需要运行一些需要超级用户访问权限的程序，您可以在 */etc/sudoers* 文件中指定这些用户，使他们能够以无需以超级用户身份登录的方式运行这些程序。（*sudo* 命令允许普通用户以超级用户身份运行特定命令（由超级用户指定）。这是一种很好的机制，因为它比给予某人完全的超级用户访问权限风险更小。*sudo* 命令本身作为 setuid root 运行。这意味着当 *sudo* 运行时，它作为 root 用户进程运行，从而允许它运行其他需要超级用户特权的程序。Red Hat Linux 不附带 *sudo* 软件包，但您可以从 ftp://ftp.redhat.com/ftp/site 获取。通常，访问 Red Hat 繁忙的 FTP 服务器很困难，所以如果您在那些服务器上碰壁，请尝试 http://www.courtesan.com/sudo/，即官方 sudo 网站，那里有大量关于 sudo 的信息，包括 sudo 的 FTP 站点列表。）

主要思想是尽可能减少超级用户特权。

## 紧急情况或遭受攻击时限制所有访问

在许多情况下，当系统管理员检测到攻击或紧急情况（如磁盘问题）时，首要任务是禁止用户登录，直到问题解决或系统下线。有时，管理员在系统关闭前需要稍作考量。在这种情况下，禁止新登录变得很重要。要快速禁止新登录，请创建一个名为 `/etc/nologin` 的文件，并写入适当的消息，让用户知道您为何阻止他们以及系统预计何时恢复在线。该文件的存在将禁止任何普通用户登录。因为超级用户只允许从控制台登录，请确保您拥有系统的物理控制台访问权限，否则您可能会意外退出当前的 shell 会话并将自己锁在系统之外。

## 使用影子密码

只有少数程序（包括 login、passwd 等）真正需要 /etc/passwd 文件中的加密密码字段。所有其他程序只需要用户信息，如用户名、UID、GID 和 shell。因此，您可以将加密密码从 /etc/passwd 移至另一个文件，并更改需要访问加密密码的程序，使它们能够读取此文件。此文件不会是全局可读的，因为被允许访问的程序将作为 setuid-root 程序运行。换句话说，这些程序将以 root 用户身份运行以读取新密码文件。一个名为 Shadow Utils 的软件包会为您完成所有这些工作。

影子密码支持包含在 Shadow Utils 软件包中，该软件包默认未安装。安装后，该软件包提供实用程序，使您能够将 /etc/passwd 文件转换为无密码文件。加密密码将被移至 /etc/shadow，该文件仅可被 root 和任何作为 setuid root 运行的程序读取。这意味着，利用薄弱程序获取 /etc/passwd 访问权限的恶意用户仍可能访问该文件，但该文件将不提供任何密码信息。影子实用程序包还提供其他有趣的功能，如密码老化、账户过期和锁定功能。下一节介绍如何在您的系统上使用影子密码。

### 安装影子实用程序包

从您的 Red Hat CD-ROM 或 Red Hat FTP 站点获取文件 shadow-utils-(version-release-architecture).rpm（例如 shadow-utils-980403-4.i386.rpm）。使用 rpm 实用程序安装它，如下所示：

```
rpm -ivh shadow utility rpm file
```

安装软件包后，您需要将现有的 /etc/passwd 文件转换为基于影子密码的 /etc/passwd 文件。

### 将 /etc/passwd 和 /etc/group 转换为影子格式

传统的 /etc/passwd 文件具有以下格式：

```
username:passwd:UID:GID:full_name:directory:shell
```

要将 /etc/passwd 和 /etc/group 文件转换为影子 /etc/passwd 格式，只需运行

```
/usr/sbin/pwconv
```

转换 /etc/passwd 后，它将具有以下格式：

```
username:x:UID:GID:full_name:directory:shell
```

第二个字段现在是一个 x，而不是加密密码。您还将拥有另一个名为 /etc/shadow 的文件，其格式如下：

```
username:passwd:last:max:min:warn:expire:disable:reserved
```

加密密码字段（passwd）现在位于此文件中。/etc/shadow 文件中的所有字段均在表 15-1 中描述。

**表 15-1 /etc/shadow 文件中的字段**

| 字段 | 说明 |
|---|---|
| *username* | 用户名 |
| *passwd* | 加密的字符密码 |
| *last* | 最后一次密码更改的日期 |
| *min* | 当前密码可被更改前的最少天数 |
| *max* | 当前密码必须被更改前的最多天数 |
| *warn* | 当前密码过期前警告用户的天数 |
| *expire* | 当前密码过期并禁用账户后的天数 |
| *disable* | 账户过期以来的天数 |

新字段（除 *username* 和 *passwd* 之外的所有字段）可用于提供用户核算功能，如账户过期和密码老化。*/usr/sbin/pwconv* 实用程序使用来自 */etc/login.defs* 文件的 *PASS_MAX_DAYS*（当前密码必须更改前的最大天数）、*PASS_MIN_DAYS*（当前密码可更改前的最小天数）和 *PASS_WARN_AGE*（当前密码过期前警告用户的天数）值。修改 */etc/login.defs* 文件以设置这些字段的理想值。

### 管理用户账户

影子实用程序包安装了 useradd、userdel、usermod、groupadd、groupdel 和 groupmod 等实用程序的替代品，这些程序通常用于管理用户账户。您可以运行以下 *rpm* 命令来查明安装此软件包时实际复制了什么内容：

```
rpm -q -l shadow-utils-version-release
```

将 *version-release* 替换为您的影子实用程序包副本中的实际版本和发布信息。

新的且日益流行的 *linuxconf* 实用程序也能够处理影子密码系统。此对话框成为用户账户创建过程的一部分，并允许您指定信息

