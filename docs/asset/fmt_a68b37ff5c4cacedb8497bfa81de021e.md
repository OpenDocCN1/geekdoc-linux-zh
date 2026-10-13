
```
$ smbpasswd -j <Domain Name> -r <PDC Name>.
```

现在是时候在服务器上启动 `smbd` 和 `nmbd` 守护进程了。初始化期间 Samba 应登录到域。您可以使用服务器管理器（图 10.2）验证活动成员资格。

## 域控制

尽管 Samba 的域控制器功能尚不及 Windows NT，但您仍可能考虑将 Samba 作为 Windows 9x 客户端的域控制器运行。一个原因是，通过使用 Samba 作为域的身份验证服务，您可以在同一 Windows 9x 平台上将 UNIX 和 NetBIOS 命名空间管理协同放置。也可能是您的内部系统管理技能和平台支持基础设施更倾向于在 UNIX 而非 Windows NT 下运行域控制器。不论原因如何，您会发现 Samba 在 Windows 9x 环境中作为域控制器表现良好。对 Windows NT 客户端的域控制涉及额外的未记录协议支持，仍处于实验性 Samba PDC 工作的范畴。

要让 Samba 成为您 Windows 9x 域的域控制器，您需要验证 WINS 服务已配置并且可用（参见第 8 章）。您可以通过启用 `wins support` 参数在 Samba 下运行 WINS。如果 WINS 服务由另一台机器提供，请使用 `wins server` 参数指定远程服务器的 IP 地址或 DNS 名称。请记住 `wins support` 和 `wins server` 互斥。

```
wins support = yes
```

or

```
wins server = <IP address or DNS name>
```

使用 `netbios name` 和 `workgroup` 参数分别标识服务器的 NetBIOS 名称和域名称。

```
netbios name = <NetBIOS name>
workgroup = <domain name>
```

您还需要配置服务器充当域主浏览器（参见第 9 章）。请记住，在 Windows NT 域控制器环境中，PDC 也是域主浏览器。启用服务器的 `domain master`、`local master` 和 `preferred master` 参数，并将 `os level` 参数设置为“65”，表示 Samba 正在模拟 Windows NT Server。

```
os level = 65
domain master = yes
local master = yes
preferred master = yes
```

接下来您需要创建一个 `netlogon` 共享以支持域登录。该共享将用于存储登录脚本和系统策略文件 `CONFIG.POL`（参见本章后面的“Policies”部分）。以下是 `netlogon` 共享定义的示例。请确保 `netlogon` 共享为“只读”，以确保域的系统策略和登录脚本无法被客户端修改：

```
[netlogon]
comment = Network Logon Service
path = /usr/local/samba/lib/netlogon
public = no
writable = no
locking = no
```

通过使用 `-U<username>` 选项调用 `smbclient` 命令来验证 `netlogon` 共享配置。您可以在命令行中使用“%”字符作为用户名和密码之间的分隔符来包含相关密码：

```
$ smbclient -U <username>[%<password>]
```

如果 Samba 还将为每个客户端提供私有文件存储，请验证 `smb.conf` 中是否定义了 `homes` 共享（参见第 11 章）。`homes` 共享是一种特殊服务，通过在访问共享时引用用户名来提供对用户 UNIX `$HOME` 目录的访问。您还可以通过设置 `logon drive` 和 `logon home` 参数，在登录时指定将主目录挂载为指定的驱动器号：

```
[homes]
comment = Home Directories
browseable = no
writable = yes
```

```
logon drive = <drive letter>
logon home = \\ %N\%U
```

现在您可以通过启用 `domain logons` 参数来允许域登录。您还需要验证 `security` 参数的值为 `user`，并且 `encrypt passwords` 已启用。

```
security = user
encrypt passwords = yes
domain logons = yes
```

![](img/7684008b1d7775727df27d44aed5b3f0_135_0.png)

图 10.2：Samba 域成员资格验证

当 Samba 登录到域时，它会收到与发送给 Windows 客户端相同的身份验证和授权信息。数据包括诸如安全标识符（SIDs）和域组成员身份之类的结构。在 Samba 的未来版本中，此信息将用于自动生成 UNIX UID 和 GID。敬请期待。

## 登录脚本

在第 6 章中我们介绍了如何使用 `preexec` 和 `postexec` 参数在客户端连接和断开共享时自动执行命令或脚本。也可以使用 `logon script` 参数在域登录处理期间运行脚本。通过在 `logon script` 名称的值中使用替换变量，可以根据连接客户端的 SMB 信息调用不同的登录脚本。例如，通过在登录脚本名称中使用 `%U` 参数，您可以标识每个用户的登录脚本。请确保在脚本中使用 `crlf` 格式，以免混淆 DOS 客户端。示例 10.2 中列出了一个示例登录脚本。该示例脚本将客户端系统时间与时间服务器同步，并将共享目录挂载为驱动器号 S:。将登录脚本与 `preexec` 和 `postexec` 结合使用，可进一步定制域连接/断开处理。

```
logon script = \\ %N\netlogon\scripts\%U.bat
```

### 示例 10.2 示例登录脚本

```
# Sample logon script
ECHO Domain Logon Setup
NET TIME \\<server-name> /YES /SET
NET USE S: \\<server-name>\workspace
```

## 漫游配置文件

我们大多数人花费太多时间艺术化地定制 Windows 桌面。我们选择的显示背景、文字字体、应用程序快捷方式、图标和屏幕保护程序都反映了我们网络人格的一部分。屏幕上的所有东西都必须放在合适的位置。投入了这么多努力之后，当我们精心打造的桌面世界在我们从一台工作站移动到下一台时不能自动跟随我们时，我们都会感到有点恼火。

解决这个难题的方案称为漫游配置文件，即存储在网络驱动器上并在登录时复制到本地工作站的 Windows 桌面配置文件。配置文件本身是一组 Windows 环境设置，与已安装的应用程序和文件夹一起使用以创建用户的桌面工作区。配置文件是 Windows 注册表项 `HKEY_CURRENT_USER` 的缓存副本，在 Windows 9x 下存储为名为 `user.DAT` 的文件，而在 Windows NT 下为 `NTuser.DAT`。`HKEY_CURRENT_USER` 结构反映了当前登录用户设置的桌面首选项。

用户配置文件的集合通常按用户名存储在域控制器系统根目录下的 `PROFILES` 目录中。当用户登录到域时，Windows 会检查存储在域控制器上的远程配置文件的时间戳与存储在工作站上的本地副本。最近的副本随后用于设置用户的初始桌面环境。当用户注销时，配置文件会被复制回域控制器。假设域注销期间未出现问题，配置文件的最新副本将驻留在域控制器上，并在用户从任何域工作站登录时可用。

配置文件还为系统管理员提供了一种为用户配置通用或默认桌面规则的手段。如果将配置文件文件的扩展名从 `DAT` 改为 `MAN`，配置文件将成为强制配置文件，并将用于设置初始桌面环境。最终用户可以在会话期间修改桌面，但这些更改不会反映在存储在域控制器上的强制配置文件中。

Samba 通过 `logon path` 参数指定漫游配置文件。默认路径是将配置文件存储在用户的主目录中。由于 Windows 客户端可能在用户注销后仍保持主目录挂载，因此建议指定用于存储漫游配置文件的替代存储库。一种简单的解决方案是创建一个用于存储漫游配置文件（示例 10.3）的独立共享。

```
logon path = <profile path>
```

### 示例 10.3 备用漫游配置文件共享

```
logon path = \\N\profiles\%U
[profiles]
    path = /usr/local/samba/profiles
    create mode = 600
    directory mode = 0770
    browseable = no
    writeable = yes
```

您也可能由于文件名大小写而遇到解析配置文件名的问题。建议您同时启用 `preserve case` 和 `short case preserve` 参数，并禁用 `case sensitive` 参数：
