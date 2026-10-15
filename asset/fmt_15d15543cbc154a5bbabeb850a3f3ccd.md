
| ./samba <version>/docs/Win98_PlainPassword.zip |

### 示例 7.3 用于明文密码支持的注册表编辑

#### Windows NT

```
Find:HKEY_LOCAL_MACHINE\system\CurrentControlSet /
    \Services\rdr\parameters
Add:    EnablePlainTextPassword, dword:00000001
```

#### Windows 9x

```
Find:HKEY_LOCAL_MACHINE\System\Current\ControlSet /
    \Services\VxD\NETSUP
```

```
Rename: "New Value #1" to
"EnablePlainTextPassword", dword:00000001
```

## 加密密码

在 SMB 会话设置期间，通过在 Samba 中启用 NTLM 加密密码支持，可以消除明文密码选项。

该功能通过消除线路上密码窃听的可能性来提高整体网络安全性；然而它增加了维护和同步 UNIX 与 NTLM 密码空间的复杂性。启用加密密码需要维护一个包含 NTLM 密码的额外密码文件。这必须与标准的 UNIX 密码维护活动一起进行。

NTLM 加密密码选项通过将 `encrypt passwords` 参数设置为 `true` 来启用。在启用加密密码支持之前，您需要创建一个 Samba `smbpasswd` 文件的实例，其中包含每个用户的条目。

通常，最简单的方法是使用现有的 UNIX 或 NIS 密码文件作为输入，提供给 Samba 发行版中的 `mksmbpasswd.sh` shell 脚本。

该过程在示例 7.4 中有描述。

```
encrypt passwords = <true, false>
```

### 示例 7.4 启用 Samba NTLM 加密支持

```
$ cat /etc/passwd | mksmbpasswd.sh > \
/usr/local/samba/private/smbpasswd
$ chown -R root:root /usr/local/samba/private/smbpasswd
$ chmod 500 /usr/local/samba/private
$ chmod 600 /usr/local/samba/private/smbpasswd
```

更新 `smb.conf` 参数。

```
encrypt passwords = true
```

`smbpasswd` 文件默认存储在 `/usr/local/samba/private` 目录中。您可以通过将目录路径指定为 `smbpasswd file` 参数的值来指示替代位置：

```
smbpasswd file = <path>
```

`smbpasswd` 文件中每个条目的格式在表 7.2 中列出。一般来说，它与标准的 UNIX 密码文件格式相似。像其 UNIX 对应物一样，它使用 `:` 来分隔每个字段。请特别注意包含 32 个 `X` 字符的两个字段。这两个字段分别是 LAN Manager 和 NT 版本哈希密码的占位符。如果要被 `smbd` 识别，则字段最初必须包含 32 个 `X` 字符，这一点至关重要。

### 表 7.2 smbpasswd 格式

```
username:uid:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX: \
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX: [Account type]: \
LCT-<last-change-time>:<Long name>
```

最初，所有用户的密码条目都由 32 个 `X` 字符组成。这有效地拒绝了对该帐户的访问，直到管理员更改密码为止。您可以通过用字符串 `NO PASSWORD` 覆盖前 10 个 `X` 字符来允许用户自行更改密码（示例 7.5）。您还需要启用 `null passwords` 参数，以便 `smbpasswd` 命令无需密码即可连接到 `smbd` 守护进程。请注意，这会带来安全风险，因为在设置新密码值之前不会提示用户输入现有密码。

### 示例 7.5 允许首次更改密码

#### smb.conf

```
null passwords = true
```

#### smbpasswd

```
deroest:1004:NO PASSWORDXXXXXXXXXXXXXXXXXXXX: \
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX: [U ]: \
LCT-00000000:Jim DeRoest:/home/deroest:/usr/bin/ksh
```

#### smbpasswd 命令

`smbpasswd` 命令用于设置和更新 `smbpasswd` 文件中的两个 32 字节字段。请注意，与 UNIX `passwd` 命令不同，从版本 1.9.18p4 开始的 Samba 版本中，`smbpasswd` 不应具有 `setuid root` 权限。此版本的 `smbpasswd` 充当客户端，请求权威的 Samba `smbd` 守护进程或 NT 域 PDC 代表最终用户更新密码。与其 UNIX 对应物一样，`smbpasswd` 命令首先请求现有密码，然后两次提示输入新密码（示例 7.6）。具有 root 权限的用户可以包含 `-u <username>` 选项来设置指示用户的密码。

### 示例 7.6 smbpasswd 命令

| 命令 | 描述 |
|---|---|
| $ smbpasswd <-u username> | 如为 root 则添加 -u。 |
| old password > | 如非 root 则为旧值。 |
| New SMB password: | 新值。 |
| Repeat New SMB Password: | 再次输入新值。 |

## 从明文迁移到加密密码

对于最初使用明文密码并希望迁移到加密密码的站点，Samba 可以通过设置 `update encrypted` 参数来自动化此过程。

```
security = user
encrypt passwords = no
update encrypted = yes
```

在会话设置时，Samba 使用默认的 UNIX 身份验证过程将客户端的明文密码与 `/etc/passwd` 进行验证。验证成功后，Samba 然后将明文密码加密为 LAN Manager 和 NT 哈希格式并将它们存储在 `smbpasswd` 文件中。请注意，用户必须已在 `smbpasswd` 文件中拥有现有条目。`smbpasswd` 文件中的任何现有密码信息都将被新密码覆盖。一旦明文到加密密码的迁移过程完成，请关闭 `update encrypted` 参数并打开 `encrypt passwords` 参数。

```
encrypt passwords = yes
update encrypted = no
```

## 密码同步

此时，您已完成 Samba 加密密码支持的设置，现在在服务器上维护两个独立的密码文件，即 UNIX 的 `/etc/passwd` 和 Samba 的 `/usr/local/samba/private/smbpasswd`。您可能更喜欢一种自动方式来保持这两个文件的同步。对一个密码文件所做的更新会自动反映在另一个文件中。Samba 可以为您处理这个问题的一方面。通过使用 `unix password sync`、`passwd program` 和 `passwd chat` 参数，`smbd` 将在收到 `smbpasswd` 更改时更新 UNIX `/etc/passwd` 文件（示例 7.7）。UNIX `passwd` 命令的值和 `password chat` 文本需要根据您的特定 UNIX 操作系统进行调整。对于 UNIX 老手来说，这类似于为 UUCP 连接设置 `login chat`。您可以使用 `passwd chat debug` 参数来自定义聊天序列。在正常操作期间不要保持此选项打开，因为它会使密码以明文形式可见。

```
passwd chat debug = <true, false>
```
