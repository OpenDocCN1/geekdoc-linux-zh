
基于 `/etc/shadow` 文件的存在，按用户实施密码老化功能才真正生效。一旦创建，你可以使用 `chage` 命令为每个用户生成密码老化条目。示例 4-2 展示了一个不完整的影子文件示例（与第 60 页的示例 4-1 无关）。

![](img/7933c44717ab0711177ea7153f959fc5_102_0.png)

与密码文件类似，影子文件为每个用户包含一条记录（一行）。每条记录包含一个由冒号分隔的字段列表。每条记录有九个字段。每个字段的含义在表 4.1 中描述。并没有强制要求必须使用表 4.1 中列出的任何或所有密码老化参数。你可以选择那些适合你的用户和环境的选项。

### 表 4.1 `/etc/shadow` 中的字段

| 字段编号 | 字段名称 | 修改字段所用的命令 | 描述 |
| :--- | :--- | :--- | :--- |
| 1 | 用户名 | `useradd`、`usermod` 和 `userdel` | 用户账号名称。必须与 `/etc/passwd` 中的条目完全匹配，且每个名称必须按相同顺序出现。 |
| 2 | 密码 | `passwd` | 哈希密码。使用 `a-z`、`A-Z`、`0-9`、`.`、`$` 和 `/` 中的任意 ASCII 字符组成的 13 至 34 个字符的条目。 |
| 3 | 最后更改 | `passwd` 或 `chage -d` | 自 `epoch`* 以来密码被更改的天数。 |
| 4 | 最小更改间隔 | `chage -m` | 密码更改后必须经过的天数，之后才能再次更改。 |
| 5 | 最大更改间隔 | `chage -M` | 密码必须在多少天后更改。 |
| 6 | 警告 | `chage -W` | 在密码过期前多少天警告用户。 |
| 7 | 失效过期 | `chage -I` | 密码过期后多少天锁定该账号。 |
| 8 | 过期日期 | `chage -E` | 自 `epoch` 以来该账号将过期的天数。在该日期午夜时，账号将被锁定。 |
| 9 | 保留 | N/A | 保留用于将来使用。 |

*Linux 的 `epoch` 是 1970 年 1 月 1 日。*

### 使用 `chage`

除 `-l` 选项外，`chage` 命令需要 `root` 权限。其他所有选项都在表 4.1 中定义。让我们看一些示例。

-   给用户 `joe` 设置最小 14 天才能更改密码，最大 30 天后必须更改密码。

    ```bash
    # chage -m 14 -M 30 joe
    ```

-   让 `guest` 账号在 1999 年 4 月 4 日过期。

    ```bash
    # chage -E 04/04/99 guest
    ```

-   普通用户检查其密码何时过期的方法如下。

    ```bash
    $ chage -l mary
    Minimum:         7
    Maximum:         30
    Warning:         3
    Inactive:       45
    Last Change:     Feb 18, 1999
    Password Expires: Mar 20, 1999
    Password Inactive: May 04, 1999
    Account Expires: Never
    ```

### `/etc/login.defs` 文件

事实证明，使用 `/etc/shadow` 文件并不是强制执行密码老化的唯一方法。Red Hat 5.2/6.0 发行版包含一个系统级文件 `/etc/login.defs`。它可以为所有用户（除了 `root`）设置密码老化。此文件还包含许多其他条目。让我们来看看它们。

文件的这一部分包含指令，用于确定每个用户邮箱的位置（更多详情参见 `/etc/login.defs` 中的注释）。

文件的下一部分如示例 4-3 所示，涉及系统级的密码老化。`PASS_MAX_DAYS`、`PASS_MIN_DAYS` 和 `PASS_WARN_AGE` 分别完全类似于 `/etc/shadow` 文件中的最大更改间隔、最小更改间隔和警告年龄（参见第 62 页的表 4.1）。如果这些条目和 `/etc/shadow` 条目对于某个特定用户都存在，则 `/etc/shadow` 中的条目优先。如果 `/etc/shadow` 中不存在某用户的条目，则应用 `/etc/login.defs` 中的条目。

#### 示例 4-3 `/etc/login.defs` 中的密码老化指令

| 指令 | 值 |
| :--- | :--- |
| `PASS_MAX_DAYS` | 30 |
| `PASS_MIN_DAYS` | 10 |
| `PASS_MIN_LEN` | 5 |
| `PASS_WARN_AGE` | 7 |

`PASS_MIN_LEN` 指令规定了除 `root` 外所有用户密码的最小长度（字符数）。如果你已实施 PAM，PAM 设置将优先（参见第 5 章）。

请记住，`/etc/login.defs` 中的条目是按用户划分的，因此，如果在 `/etc/login.defs` 中设置了条目，且并非每个用户都有相应条目，那么对于没有 `/etc/shadow` 条目的那些用户，密码老化将遵循此处列出的指令。这意味着你可以使用此文件来设置标准的密码老化参数，然后针对特定用户进行微调。

文件的剩余部分包含示例 4-4 中显示的条目。

`CHFN_AUTH` 和 `CHFN_RESTRICT` 指令可以设置为 `yes` 或 `no`。如果 `CHFN_AUTH` 为 `yes`，每当用户执行 `chfn` 或 `chsh` 命令时，系统将提示他们输入密码。如果你将此值更改为 `no`，用户将可以在不提供密码的情况下更改其 `fingerprint`（此处指 `chfn` 允许修改的用户信息，如全名、办公室等，直译为 fingerprint 较突兀，但为了忠实于原文语境及可能的术语误用，保留原意或解释性翻译。考虑到 Linux 语境，`chfn` 修改的是 GECOS 字段，常被俗称，此处暂译为“相关个人信息”或保留原词意。鉴于原文用词 `fingerprint`，可能是作者术语习惯，译为`指纹信息`略显不当，但需忠实原文，故译为`指纹信息`或`个人标识信息`。这里参考常见教材翻译，`chfn` 通常修改“全名、办公室、办公电话、家庭电话”，这里暂译为`相关个人信息*，或者更准确的`身份指纹`。让我们看上下文：“change his or her fingerprint information”，在 Linux 上下文中极有可能是指 `chfn` 管理的字段。为了避免歧义，译为`身份指纹信息`或`相关标识信息*。这里选择`相关标识信息*以便理解。）而不需要密码。只有 `root` 可以更改其他用户的 `相关标识信息`。如果 `CHFN_RESTRICT` 设置为 `yes`，系统将禁止用户使用 `chfn -f` 更改其“真实”姓名。

其余条目与 `useradd` 和 `userdel` 命令相关。`useradd`、`usermod` 和 `userdel` 命令是用于管理用户账号的命令行实用程序。在 Red Hat 5.2/6.0 发行版中，

#### 示例 4-4 `/etc/login.defs` 中的其余指令

```bash
UID_MIN 500
UID_MAX 60000
GID_MIN 500
GID_MAX 60000
#
CHFN_AUTH yes
#
CHFN_RESTRICT yes
#
#USERDEL_CMD /usr/sbin/userdel_local
CREATE_HOME yes
```

`/etc/login.defs` 文件中的 `UID_MIN`、`UID_MAX` 和 `CREATE_HOME` 指令为 `useradd` 命令设置默认行为，而 `USERDEL_CMD` 是 `userdel` 命令的一个可选增强指令。

使用这些设置，如果你在使用 `useradd` 命令时未指定 UID，`useradd` 将为你创建的第一个用户分配 UID 500，为第二个用户分配 UID 501，以此类推，直到最大 UID 60000。`CREATE_HOME` 指令可以取值为 `yes` 或 `no`。如果设置为 `yes`，调用 `useradd` 时，它将在 `/home` 中自动为该用户创建主目录。如果设置为 `no`，你必须使用 `-m` 标志调用 `useradd` 才能创建用户的主目录。`useradd` 的其他默认值在 `/etc/default/useradd` 中指定。如果存在冗余，`/etc/login.defs` 文件优先。有关系统中 `useradd(8)` 的更多信息，请参阅其手册页。

`USERDEL_CMD` 指令指定在删除用户账号之前调用的脚本或程序（绝对路径名）。默认情况下，不存在此类脚本或程序。如果该用户已登录和/或存在由该用户拥有的正在运行的进程，`userdel` 命令将不会删除该用户。管理员可以使用此指令指定一个自定义脚本或程序，该程序将检查并可能处理任何阻止删除用户账号的因素。
