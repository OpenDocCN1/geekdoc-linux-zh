

# 本地信息部分 (Local Info Section)

数据库位于 `/etc/mail/access`。所有这些信息——内部名称、基础类型以及持有数据库的文件——由 `K` 命令定义，这是我们示例宏配置文件中 `FEATURE(`access_db`)` 命令的直接结果。用于控制邮件中继和递送的访问数据库将在第 6 章介绍。

两个 `K` 命令定义了 `virtualable` 和 `mailertable` 数据库，这些数据库源于示例宏配置文件中找到以下命令：

```
FEATURE(`mailertable`, `hash -o /etc/mail/mailertable`)
FEATURE(`virtualable`, `hash -o /etc/mail/virtualable`)
```

两者都是哈希（hash）数据库，并且都带有 `-o` 选项，这意味着即使没有找到这些文件，Sendmail 也会运行。访问数据库的 `K` 命令没有使用 `-o` 选项。如果找不到 `/etc/mail/access.db`，当命令尝试使用访问数据库时，Sendmail 将失败。即使你没有访问数据库的条目，也请创建一个空的 `/etc/mail/access.db` 文件，以增强 Sendmail 的健壮性，如下例所示：

```
[root]# touch /etc/mail/access
[root]# makemap /etc/mail/access < /etc/mail/access
```

`mailertable`、`virtualable` 和访问数据库在第 6 章中介绍。然而，其他数据库未在该章介绍。`ar` 和 `devote` 数据库都是伪数据库。这意味着它们不是真实的数据库。相反，它们是 Sendmail 内部程序，重写规则像访问数据库一样访问它们。已经讨论过的 `devote` 映射用于从地址中删除引号映射。`arith` 映射用于为 STARTTLS 安全执行数学函数。STARTTLS 将在第 12 章介绍。

这四个命令 `D`、`C`、`F` 和 `K` 阐明了 `sendmail.cf` 文件中“本地信息”部分的所有内容。对于试图配置 `sendmail.cf` 的系统管理员来说，“本地信息”部分是该文件最重要的部分，因为它定义了随系统而异的配置信息。我们已经涵盖了示例系统本地信息部分的每一个命令，但在移动到“选项 (Options)”部分之前，我们应该涵盖位于本地信息之前的唯一配置命令——版本 (version) 命令。

# 版本级别命令 (The Version Level Command)

版本级别 (V) 定义了 `sendmail.cf` 文件的版本。这不应与标识 Sendmail 源代码数字的 `Z` 变量或定义宏修订控制信息的 `m4 VERSIONID` 宏混淆。

![](img/9639113aa446fb8976cb3d377f7aafdd_220_0.png)

`V` 命令告诉 Sendmail 支持该配置所需的语法层级和命令层级。如果 Sendmail 程序无法支持请求的命令和语法，它会就其不理解的命令进行报错，并显示以下版本错误消息：

```
[root]# sendmail -v -t
/etc/sendmail.cf: line 83: readcf: map arith: class arith not available
/etc/sendmail.cf: line 211: DaemonPortOptions parameter
  "Name=MTA" unknown
/etc/sendmail.cf: line 212: DaemonPortOptions parameter
  "Name=MSA" unknown
/etc/sendmail.cf: line 212: DaemonPortOptions parameter "M=E" unknown
```

警告：.cf 版本级别 (9) 超过 sendmail 版本 8.9.3 功能 (8)

另一方面，如果 Sendmail 程序比配置新，程序可以支持比配置所使用的更多功能。在这种情况下，Sendmail 会显示我们在第 3 章中首次看到的错误，“正在运行 Sendmail”。

```
[root]# sendmail -v -t -C /etc/sendmail.cf
Warning: .cf file is out of date: sendmail 8.11.0 supports version 9,
  .cf file is version 8
No recipient addresses found in header
^D
```

版本级别命令是警告 Sendmail 潜在不兼容性的关键组件。

你不需要更改 `sendmail.cf` 文件中的 `V` 命令。与 `sendmail.cf` 文件中的大多数其他内容不同，你无法使用宏控制文件中的 `m4` 宏来控制 `V` 命令的设置。`V` 命令在首次由 `m4` 构建 `sendmail.cf` 文件时被插入。列表 7.7 显示了出现在本地信息部分之前的命令，包括 `V` 命令。

# 列表 7.7 示例 sendmail.cf 中的 V 命令

```
# level 9 config file format
V9/Berkeley

# override file saf - 设置此选项会损害安全性
# 优于解决实际的文件配置问题
# 需在 cf 文件中遇到任何文件操作之前设置
#0 DontBlameSendmail=safe

# 默认 LDAP 映射规范
# 需在定义任何 LDAP 映射之前现在设置
#0 LDAPDefaultSpec=-h localhost
```

`V` 命令的格式为 `V1/厂商名称`。层级数字表示配置语法的版本。`V9` 是 Sendmail 8.11.0 支持的版本。`V` 命令的厂商部分标识是否支持任何特定特定的语法。Sendmail 发行版的默认值是 `Berkeley`，这是 Linux 使用的厂商值。

`V` 命令和本地信息部分之后的所有内容都是注释，如以 `#` 字符开头的行所示。然而，这些行中有两行是被注释掉的选项：

```
#0 DontBlameSendmail=safe
#0 LDAPDefaultSpec=-h localhost
```

`V` 命令的格式是 `V1/vendor`。层级数字表示配置语法的版本。`V9` 是 Sendmail 8.11.0 支持的版本。`V` 命令的厂商部分标识是否支持任何特定特定的语法。Sendmail 发行版的默认值是 `Berkeley`，这是 Linux 使用的厂商值。

`V` 命令和本地信息部分之后的所有内容都是注释，如以 `#` 字符开头的行所示。然而，这些行中有两行是被注释掉的选项：

```
#0 DontBlameSendmail=safe
#0 LDAPDefaultSpec=-h localhost
```

访问数据库用于控制邮件中继和递送，将在第 6 章介绍。数据库位于 `/etc/mail/access`。所有这些信息——内部名称、基础类型以及持有数据库的文件——由 `K` 命令定义，这是我们示例宏配置文件中 `FEATURE(`access_db`)` 命令的直接结果。

