
```
R@>                         $@ <@>                    special case error msgs
R$* : $* , <@>              $#error $@ 5.1.3 $:
        $: "List; syntax illegal for recipient" $@ < $* >
             catch (@host' bogusity

R@ $+                       $#error $@ 5.1.3 $: "User address required"
R$*                         $: $1
R$* > $* < @ [ $* ] > $*    $: $1 < @ [ $2 ] > $3
R$* > $* < $* > $*          $#error $@ 5.1.3 $: "Colon illegal in host name part"
R$* > $*                    $: $1
R$* < @ . $* > $*           $#error $@ 5.1.2 $: "Invalid host name"
R$* < @ $* . $* > $*        $#error $@ 5.1.2 $: "Invalid host name"
```

紧随这一系列条目之后，添加以下地址重写规则：

```
R$+ < @ $+ .fax >   $#fax $@ $2 $: $1  user@company.fax
```

此条目会将传真消息转发给 Qfax。

### 创建邮件程序定义

`/etc/sendmail.cf` 文件包含一系列邮件程序定义，如第 16 章所讨论。在该文件的这一部分，你需要为传真消息添加以下邮件程序定义：

```
MFax,  P=/usr/bin/qfax, F=lsDFheu, S=14, R=24, M=1000000,  A=qfax $u
```

### 绕过名称服务

`/etc/sendmail.cf` 文件包含一系列用于处理特殊名称情况的规则，称为规则集 96，如第 16 章所讨论。在本节中，你会看到以下条目：

```
R$* < @ $* $~P > $*       $: $1 < @ $* [$2 $3] > $4
```

通过在该行开头放置一个 `#` 来注释掉此条目。

```
#R$* < @ $* $~P > $*      $: $1 < @ $* [$2 $3] > $4
```

此条目通常会将主机名传递给名称服务器以使其规范化。这通常不是必需的，因为名称几乎总是规范化的。通过避免这一操作，`.fax` 域不会引发问题。

### 为传真创建假脱机目录

你需要创建五个目录用于假脱机目的：

- `/var/spool/fax/recvq`：用于保存传入传真的目录。
- `/var/spool/fax/sendq`：用于假脱机传出传真的目录。
- `/var/spool/fax/docq`：用于存储非活动传真（例如无法正确发送的传真）的目录。
- `/var/spool/fax/log`：用于写入日志文件的目录。
- `/var/spool/fax/result`：用于存储最近一次传真操作的目录。

所有这些目录的权限都需要设置为所有用户都可读：

```bash
# mkdir /var/spool/fax
# cd /var/spool/fax
# mkdir recvq sendq docq log result
# chmod 755 recvq sendq docq log result
```

### 创建传真配置目录

Qfax 需要一个目录来存储其配置文件。该目录的可能位置包括 `/conf/fax` 和 `/etc/conf/fax`。我们将使用后者。

创建该目录，然后将 `fax.rc`、`fax.db` 和 `cover-template.ps` 文件从 Qfax 源目录复制到新的配置目录。

### 配置 Qfax

在编译 Qfax 之前，自定义 Qfax 源目录中的 `config.h` 文件以满足你系统的特定要求。该文件包含一系列以下形式的条目：

```c
#define variable_name <value>
```

表 17.1 概述了需要在 `config.h` 文件中设置的变量。

**表 17.1 — QFAX `config.h` 文件中的变量**

| 变量名 | 描述 |
|---|---|
| `DATABASE` | `fax.db` 文件的位置。如果你将该文件复制到 `/etc/conf/fax`，则该值应为 `/etc/conf/fax/fax.db`。 |
| `CONFIG` | `fax.rc` 文件的位置。如果你将该文件复制到 `/etc/conf/fax`，则该值应为 `/etc/conf/fax/fax.rc`。 |
| `TEMPLATE` | `cover-template.ps` 文件的位置。如果你将该文件复制到 `/etc/conf/fax`，则该值应为 `/etc/conf/fax/cover-template.ps`。 |
| `FAXQUEUE` | 用于存储传出传真的目录（本例中为 `/var/spool/fax/sendq`）。 |
| `STOREDIR` | 用于存储非活动传真的目录（本例中为 `/var/spool/fax/docq`）。 |
| `FAXSCRIPT` | `Efax` 传真脚本的位置（通常为 `/usr/bin/fax`）。 |
| `RESULT` | 应包含上次发送传真尝试状态的文件名（本例中为 `/var/spool/fax/result/result`）。 |
| `LS` | 你的 `ls` 命令（通常就是 `ls`）。 |
| `MAXFAXES` | 应在传出传真队列中存储的最大传真数量（默认值为 15）。 |
| `MAXTRIES` | 在放弃之前尝试发送失败传真的最大次数（默认值为 3）。 |

**表 17.1（续）**

| 变量名 | 描述 |
|---|---|
| `LDPERIOD` | 可以拨打长途电话的时间段，格式为 `<start time>-<end time>`，其中时间使用 24 小时制表示，如 `2200-0700`。 |
| `FAXGROUP` | 包含允许立即发送传真而无需等待定期排队处理的用户的用户组名称。默认组名 `faxnow` 是一个不错的选择。 |
| `USE_DAEMON` | 此定义不需要取值。如果您允许 Qfax 接收传入的传真，请保持该条目不变；如果您不打算接收传真，请在该条目的开头添加一个额外的 `#` 将其注释掉。 |

#### 指定特权用户

通常，Qfax 只在处理传出假脱机目录时按计划的时间间隔发送传真。在 Qfax 源目录的 `config.h` 文件中由 `FAXGROUP` 变量指定的组中所列出的用户可以覆盖此设置并立即发送传真。通常，这个组被称为 `faxnow`。您需要在 `/etc/group` 文件中创建相应的条目来创建 `faxnow` 组：

```text
faxnow:: <group ID>:<user1>,<user2>,<user3>,...
```

该组 ID 在 `/etc/group` 文件中的所有组中应该是唯一的。

#### 编辑 fax.rc 文件

`fax.rc` 文件存储在安装过程中早些时候创建的 Qfax 配置目录中，您可以在其中定义显示在传真页眉和传真封面上的信息，并指定封面上使用的字体。

文件中的注释不言自明。请根据您的需要编辑该文件。

#### 创建 fax.db 文件

`fax.db` 文件存储在安装过程中早些时候创建的 Qfax 配置目录中，是全局电话簿文件，其中包含将格式为 `<person>@<company>.fax` 的传真电子邮件地址映射到传真号码所需的信息。该电话簿文件中的条目对所有用户开放。

每个条目长度至少为五行，格式如下：

```text
<company alias>    <company name>
<voice phone number>
<fax number>
<person alias 1>    <person name 1>
<person alias 2>    <person name 2>
...
+
```

单独一行的 `+` 表示条目的结束。公司和人员别名随后用作您通过电子邮件发送传真的地址，格式为 `<person alias>@<company alias>.fax`。电话号码和传真号码可以采用任何标准格式，包括 `1-604-555-1212` 和 `1 416 555 1212`。长途号码前导的 `1` 或 `0` 对于 Qfax 正确拨号至关重要。

#### 创建 .fax 文件

除了全局电话簿 `fax.db` 之外，用户还可以在其主目录中的 `.fax` 文件中创建个人电话簿。此文件的格式与刚才描述的全局电话簿文件格式相同。

#### 编译并安装 Qfax
