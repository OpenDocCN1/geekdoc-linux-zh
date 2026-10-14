
- `[homes]`—如果此可选节包含在配置文件中，服务器可以即时创建将客户端连接到其主目录的服务。
- `[printers]`—此节的工作方式与 `[homes]` 类似，但用于打印机。如果配置文件中存在 `[printers]` 节，用户能够连接到本地主机 `printcap` 文件中指定的任何打印机。

列表 8.3 中显示了一个最小的 `smb.conf` 示例。

### 列表 8.3

一个最小的示例 `smb.conf` 文件

```ini
[global]
workgroup = TUX-NET
netbios name = MySambaServer
;The following is the default security setting
#security = user

[junk]
path = /tmp

[docs]
path = /usr/share/doc
#read only defaults to yes so no real need to set it
read only = yes
comment = on-line documentation
```

# 第 8 章：网络服务

在列表 8.3 中，`[global]` 中的默认安全设置告诉 Samba 在验证用户密码时使用 `/etc/passwd` 和 `/etc/samba/smbpasswd`。如果您设置了 Windows 域控制器或 Windows Active Directory 域，您可以通过设置 `security = domain` 或 `security = ads` 改用它们来验证用户名和密码。如果您设置 `security = share`，客户端最初连接到 Samba 服务器时不需要密码；但是，客户端尝试访问共享时可能需要密码。

### `/ETC/SAMBA/SMBPASSWD` 文件

`/etc/samba/smbpasswd` 是 Samba 密码文件。它包含用户名、Unix/Linux 用户 ID 以及用户的哈希密码，以及账户标志信息和密码上次更改的时间。

Samba 2.2 和 3 使用的 `smbpasswd` 文件格式与 `/etc/passwd` 文件类似。它是一个 ASCII 文件，为每个用户包含一行。每行中的每个字段由冒号分隔。以 `#` 开头的任何条目将被忽略。以下是 `smbpasswd` 记录的示例：

```
testuser:6002:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:
➜XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:
➜[DU]:LCT-00000000:
```

第一个字段包含用户名；此名称必须已存在于 `/etc/passwd` 文件中。第二个字段保存用户的 UID，该 UID 必须与 `/etc/passwd` 中同一用户条目的 UID 匹配。第三个字段是用户密码的 LAN 管理器（LANMAN）哈希，以 32 位十六进制数字编码。这是 Windows 9x 系统使用的相同密码。如果该字段的值等于 32 个 X 字符，则用户的账户被视为已禁用，将无法登录到 Samba 服务器。第四个字段也是密码字段。它包含用户密码的 Windows NT/2000/XP 哈希。与 LANMAN 密码哈希类似，如果 NT 值等于 32 个 X 字符，则用户的账户被视为已禁用，将无法登录到 Samba 服务器。

倒数第二个字段包含账户信息。该字段由 `[ ]` 字符括起来，长度始终为 13 个字符，包括打开和关闭括号字符。该字段的内容可以是以下字符中的一个或多个：

- `U` 表示这是一个“用户”账户，即普通用户。`smbpasswd` 文件目前仅支持用户和工作站信任账户。
- `N` 表示账户没有密码（LAN-MAN 密码哈希和 NT 密码哈希字段中的密码将被忽略）。请注意，这仅在 `smb.conf` 文件中设置 `null passwords = yes` 时才允许用户无密码登录。
- `D` 表示该账户已被禁用，此用户将不允许进行 SMB/CIFS 登录。
- `W` 表示该账户是“Workstation Trust”账户。此类账户允许 Windows 工作站和服务器加入由 Samba PDC 主持的域。

最后字段保存账户最后修改的时间。它由字符 `LCT=`（Last Change Time）组成，后跟自纪元（1970）以来最后更改所做的 Unix 时间（以秒为单位）的数字编码。此 LCT 字段之后出现的任何附加冒号分隔字段都会被忽略。

#### NOTE

所有以美元符号 (`$`) 结尾的共享名称都是隐藏的；当用户显示服务器资源时（例如从 Windows 工作站使用 `NET VIEW \\SambaServername` 命令），它们通常不会出现。这也适用于托管在 SLES Samba 服务器上的此类共享。

可以为每个 `[share]` 部分指定多个选项。最常用的选项如下：

- `read only = yes/no` 指定客户端是否可以创建、删除或修改共享上的任何文件。默认值为 `read only = yes`。 （您可以使用 `writable = yes` 代替 `read only = no`。）
- `guest ok = yes/no` 指示访问此共享是否需要密码。默认值为 `guest ok = no`，这意味着需要密码。 `guest ok = yes` 表示不需要密码。 （您也可以使用 `public = yes`，这是 `guest ok = yes` 的一种较旧且更模糊的形式，以及与 `guest ok = no` 同义的 `public = no`。）
- `guest account = username` 是将用于访问指定为 `guest ok = yes` 的服务的用户名。用户必须存在于密码文件（或用于验证用户的任何服务）中。默认值为 `nobody`。
- `comment = description` 提供共享性质的描述，有助于用户选择正确的资源进行访问。
- `hosts allow = host1, host2, ...` 指定允许访问共享的一个或多个机器。默认情况下，所有主机均被授予访问权限。
- `hosts deny = host1, host2, ...` 指定不允许访问共享的一个或多个机器。本地主机 (`127.0.0.1`) 始终被授予访问权限，但您可以使用 `hosts deny = localhost` 来阻止它。

有关所有支持的选项列表以及配置文件中宏的使用，请参阅 `man smb.conf` 或位于 `/usr/share/doc/packages/samba` 中的文档。

### 一个匿名只读服务器配置

您可以使用 Samba 非常轻松、快速地设置文档服务器，以便组织内的任何人都可以访问共享信息。以下配置文件说明了所需的最小设置：

```ini
[global]
workgroup = TUX-NET
netbios name = DocumentServer
security = share

[docs]
path = /usr/share/doc
read only = yes
guest ok = yes
# limit access to your internal network
hosts allow = *.universalexport.ca, 10.0.0.0
comment = on-line documentation
```

如果将安全级别设置为 `share` 并允许访客访问 `docs` 共享，则您的用户无需使用密码即可访问此共享。例如，从 Windows 2000 工作站，所有用户需要做的就是输入以下内容：

```text
net use i: \\documentserver\docs
```

在创建配置文件但在启动 Samba 守护进程之前，运行 `/usr/bin/testparm` 以验证 `smb.conf` 文件的内容。如果 `testparm` 运行正确，它将列出已加载的服务。如果不正常，它将给出错误消息。请确保它运行正确，并且服务看起来合理，然后再继续。命令语法是

```text
/usr/bin/testparm config_file
```

#### TIP

如果省略配置文件的名称，则默认为 `/etc/samba/smb.conf`。因此，您可以复制当前的 `smb.conf` 文件，对其进行修改，对编辑后的文件运行 `testparm`，并且仅在修改后的版本中没有 `testparm` 报告的错误时才覆盖当前文件。

`testparm` 解析您的配置文件并报告任何未知参数或语法错误。以下是检查第 8.3 节中显示的最小 `smb.conf` 文件的 `testparm` 输出：
