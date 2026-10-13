
`passwd password required /usr/lib/security/pam_unix.so.1`

如果没有 `passwd` 服务的条目，则使用下所示其他服务的条目。

```
# Password management

# other password required /usr/lib/security/pam_unix.so.1
```

## 972 passwd

如果列出了多个密码模块，用户可能会被要求输入多个密码。

## 选项

- `-a` 显示所有条目的密码属性。仅配合 `-s` 选项一起使用；你不能指定 name。对于 `nisplus` 存储，此选项仅显示调用者有权读取的本地域 NIS+ 密码表中的条目。对于 `files` 存储，此选项限制为超级用户。
- `-D domainname` 查询 `domainname` 中的 `passwd.org_dir` 表。如果你未指定此选项，将使用 `nis_local_directory(N)` 返回的默认域名名。该域名名与 `domainname(1)` 返回的相同。
- `-e` 更改登录 shell。对于 `files` 存储，此选项仅对超级用户有效。普通用户可以更改 `nis` 或 `nisplus` 存储。
- `-g` 更改注释（指）信息。对于 `files` 存储，此选项仅对超级用户有效。普通用户可以更改 `nis` 或 `nisplus` 存储。
- `-h` 更改主目录。
- `-r` 指定应用操作存储。支持的存储包括 `files`、`nis` 和 `nisplus`。
- `-s name` 显示密码属性。只要使用了 `-r nisplus` 参数，用户就可以显示自己登录名的密码属性。否则，`-s` 参数限制为超级用户。
- `-d` 删除 name 的密码。这仅适用于 `files` 存储。
- `-f` 强制用户在下次登录时更改密码。
- `-l` 锁定 name 条目。
- `-n` 设置 name 的最小字段。min 是密码更改之间的最少天数。如果 min 大于 max，用户无法更改密码。除非 max 设置为 -1，否则始终配合此选项。在这种情况下不需要设置 min。
- `-w` 设置 name 的警告字段。warn 是密码过期前警告的天数。在禁用年龄的情况下，此选项无效。
- `-x` 设置 name 的最大字段。max 是密码 有效的最大天数。如果设置为 -1，则立即禁用年龄。如果设置为 0，则强制用户在下次登录时更改密码并禁用年龄。

## 超级用户选项

只有超级可以使用可以使用选项。

## 973 passwd

### 操作数

- `name` 用户登录名。

## 环境变量

如果环境中没有设置任何 `LC_*` 变量（`LC_TYPE`、`LC_MESSAGES`、`LC_COLLATE`、`LC_NUMERIC`、`LC_MONETARY`）（参见 `environ(5)`），`passwd` 对每个区域设置的操作行为由 `LANG` 的值决定。如果设置了 `LC_ALL`，其内容将用于覆盖 `LANG` 和其他 `LC_*` 变量。

`LC_TYPE` 决定 `passwd` 如何处理字符。当 `LC_TYPE` 设置为有效值时，`passwd` 可以显示和处理包含该区域有效字符的文本和文件名。`passwd` 可以处理扩展 Unicode 编码（EUC），任何单个字符可以是 1、2 或 3 字节。`passwd` 还可以处理更宽的列。在 C 区域中，只有 ISO 8859-1 字符是有效的。

`LC_MESSAGES` 决定诊断和信息的呈现方式。这种呈现包括消息的语言和风格以及肯定的正确形式。在 C 区域中，消息以程序默认的形式显示（通常是美国英语）。

## 退出状态

- `0` 成功。
- `1` 权限拒绝。
- `2` 无效无效。
- `3` 意外失败。密码文件未更改。
- `4` 意外失败。缺少密码文件。
- `5` 密码文件忙。请稍后再试。
- `6` 选项无效。
- `7` 年龄选项已禁用。

## 文件

`/etc/shadow`
`/etc/passwd`

密码文件。

`/etc/shadow`

影子密码文件（Shadow password file）。

`/etc/default/passwd`

为 `/etc/default/passwd` 中的以下标志设置默认值。例如，`MAXWEEKS=26`。

| MAXWEEKS | 密码有效的最大时间段。 |
| :--- | :--- |
| MINWEEKS | 更改密码的最短时间段。 |
| PASSLENGTH | 密码的最小长度，以字符为单位。 |
| WARNWEEKS | 密码即将过期警告的时间段。 |

## 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| Availability (可用性) | SUNWcs |
| CIS | Enabled (启用) |

## 参见

`finger(1)`, `login(1)`, `nispasswd(1)`, `nistbladm(1)`, `ypppasswd(1)`, `domainname(1M)`, `eeprom(1M)`, `id(1M)`, `passmgmt(1M)`, `pwconv(1M)`, `su(1M)`, `useradd(1M)`, `userdel(1M)`, `usmod(1M)`, `pam(3)`, `crypt(3C)`, `getpnam(3C)`, `getspnam(3C)`, `nis_local_directory(3)`, `loginlog(4)`, `nswitch.conf(4)`, `pam.conf(4)`, `passwd(4)`, `shadow(4)`, `attributes(5)`, `environ(5)`, `pam_unix(5)`

# paste — 合并文件的对应或后续行

### 概要

```
/usr/bin/paste [-s][-d list] file...
```

## 描述

`paste` 命令按行合并文件，并将输出写入到标准输出。你可以使用 `paste` 通过合并来自 1 到 12 个文件的字段或列来创建新表格。每个输入文件被视为输出行中的一个字段。默认情况下，`paste` 在每个文件的贡献之间插入一个制表符。`paste` 接受一个或多个文件名作为参数，从每个文件中读取一行，并将这些行合并成单行。如果某些文件的行数少于其他文件，`paste` 仅放置分隔符并留空字段。你可以指定一个连字符 `-` 作为一个或多个文件名之一来读取标准输入。

## 选项

- `-` 除非在列表中使用反斜杠字符 (`\`)，否则将列表中的每个字符指定为分隔符。如果你使用反斜杠，请按下述指定其随后的一个或多个字符作为分隔符。这些元素指定使用一个或多个分隔符，以替换每个输入行换行符的默认制表符（Tab）。列表中的元素是循环使用的；即当列表耗尽时，将重用列表中的第一个元素。

当你指定 `-s` 选项时：

- `-` 不修改文件中的换行符。
- 在处理完每个操作数后，将分隔符重置为列表的第一个元素。

当你不指定 `-s` 选项时：

- `-` 不修改最后一个指定的文件中的换行符。
- 每从每个文件处理一行时，都将分隔符重置为列表的第一个元素。

如果列表中出现反斜杠，则使用它和随后的字符表示后续分隔符。

```
n 换行符。

t 制表符。

\ 反斜杠字符。

\ 空字符串（不是空字符）。如果 \0 紧随字符 x、Z 或由 LC_ctype 关键字定义的任何字符，则结果不确定。
```

如果反斜杠后跟随任何其他字符，则结果不确定。

# -s

按照命令行顺序连接每个单独输入文件的所有行。除非 `-d` 选项另有指定，否则将每个输入文件中最后一行之外每一行的换行符替换为制表符。

### 操作数

`file`
输入文件的路径名。如果你将一个或多个文件指定为 `-`，则使用标准输入；对于每个 `-` 实例，循环地一次从标准输入读取一行。实现上支持至少 12 个操作数的合并。

## 用法

`largefile(5)` 用于描述 `paste` 在遇到大于或等于 2 Gbytes (31 字节) 的文件时的行为。

## 示例

以下示例使用 `paste` 命令在一列中列出目录中的文件，使用空格字符作为分隔符。

```
case$ ls | paste -d " " -

085X01.DOC

085X02.DOC

085X03-1.DOC

085X042.DOC

085X08R.DOC

085X09E.RTF

085DOC.ZIP

085FILE.ZIP

085XINTR.ZIP

a.out

ibliography

ibliography.ig

C.str

DeadLetters

examples

file1

kookurra-1\ltr

Mail

new

case$
```

以下示例用四列列出目录的内容，使用默认的制表符分隔符。

```
case$ ls | paste - - - -

085X01.DOC 085X03-1.DOC 085X042.DOC

085X08R.DOC 085X09E.RTF 085DOC.ZIP 085FILE.ZIP

085XINTR.ZIP a.out bibliography bibliography.ig
```
