
# 表 A.1 仅全局部分的参数（续）

| `allow trusted domains` | 允许在 DOM2 中拥有账户的用户访问其他 NT 资源，即使该用户在 DOM1 中没有账户。这种域安全的定义可能有点开放。此 Samba 参数将允许管理员根据需要限制访问。默认值为 `Yes`。 |

| 参数 |  |
| :--- | :--- |
| `change notify timeout` | 检查文件名和目录更改之间间隔的秒数。默认值为 `60`。较小的值可能会影响性能。 |
| `config file` | 额外的 Samba 配置文件的 Unix 路径。这可以用于重定向用户的 Samba 配置，或与 `%macros` 配合使用定义用户或组配置文件。默认值为空字符串。 |
| `deadtime` | 检查不再活跃的会话之间间隔的分钟数；Samba 会杀死达到此限制的会话。默认值为 `0`。 |
| `debug level` | 日志级别的值。默认值为 `0`。大于 `3` 的日志级别可能会影响性能；`10` 以上的级别用于开发调试。 |
| `debug timestamp` | 每条调试（debug）消息都可以包含日期和时间戳。此项用于开启或关闭该功能。默认值为 `Yes` (B)。 |
| `default` | 当请求一个不存在的连接或被拒绝访问权限时，会话应连接的默认服务名称。默认值为空字符串。 |
| `default service` | `default` 的同义词 |
| `delete user script` | 此参数的值是 `smbd` 将以 ROOT 身份运行的删除 Unix 用户账户的脚本完整路径。安全参数必须设置为 `security=server` 或 `security=domain`。脚本必须能够仅通过一个参数（当前会话用户名 `%u`）来删除 Unix 用户账户。此参数没有默认值。 |
| `dfree command` | 需要的用于返回可用磁盘空间的系统命令。 |
| `dns proxy` | 与 `servers=Yes` 配合使用，将为 WINS 数据库中未找到的主机开启 DNS 名称查找 (B)。 |
| `domain admin group` | 此参数是未完成的 Samba NT 域控制器代码的一部分。 |
| `domain admin users` | 此参数是未完成的 Samba NT 域控制器代码的一部分。 |
| `domain controller` | 此参数在 Samba 源码中不再使用，应从你的 `smb.conf` 文件中删除。出于兼容性原因仍然存在。 |
| `domain groups` | 此参数是未完成的 Samba NT Domain 代码的一部分。 |
| `domain guest group` | 此参数是未完成的 Samba NT 域控制器代码的一部分。 |
| `domain guest users` | 此参数是未完成的 Samba NT 域控制器代码的一部分。 |
| `domain logons` | 开启或关闭 Windows 9x 或 NT 风格的域登录。(B)。 |
| `domain master` | 设置服务器将作为域主浏览器（domain master browser）。(B)。 |
| `encrypt passwords` | 设置或关闭 NT 风格的密码加密。要求 Samba 服务器上存在一个 `smpasswd` 文件。(B)。 |
| `getwd cache` | 开启或关闭当前目录信息的缓存。如果也开启了宽链接（wide links），这对性能很有帮助。(B)。 |
| `homedir map` | 如果参数 `homedir = Yes`，则此参数指定服务器上主目录的 NIS（或 YP）映射位置。该值格式为：`username server/some/file/system`，程序将从第一个 `'.'` 之后提取服务器名称。默认值为 `auto.home`。 |
| `hosts equiv` | 如果此参数的值为非空字符串，它将包含一个文件名，通过读取该文件获取可以在不指定密码的情况下访问服务器的主机和用户。设置此参数具有重大的安全风险，因为你信任了一个外部主机以及所有从该主机登录的用户。默认值为空字符串。 |
| `include` | 此值指定要在当前配置文件中包含的另一个配置文件。该参数可以使用任何宏替换，但 `%U`、`%P` 和 `%S` 除外，因为这些值在读取时尚未被设置。 |
| `interfaces` | Samba 可以在多个网络接口上运行；值将指定 Samba 应该运行的接口列表。这些值由一组 `/netmask` 接口组成。网络掩码可以是位图（bitmap）也可以是位长度（bitlength）。默认情况下，Samba 会尝试定位主网络接口（通常是 `eth0`），如果没有设置任何值，它将仅为该接口进行配置。如果你有多个托管在多个子网上的服务，这将非常有用。 |
| `keepalive` | 该值（整数）表示检查确定任何客户端是否崩溃之间间隔的秒数。如果也设置了 `socket options = SO_KEEPALIVE`，则不应设置 `keepalive` 参数。默认值为 `0`。如果需要，建议设置为 `4` 小时或 `3600`。 |
| `kernel oplocks` | Samba 2.0 的新功能，当 Unix 客户端访问一个已加了操作性锁（oplockocks）的文件时，它会破坏该文件的 oplocks，以防止文件损坏。目前只有 SGI 支持此项；Linux 和 BSD 很快也会支持。一旦设置（安装时自动设置），你就不需要更改它。(B)。 |
| `ldaps filter` | 此参数是未完成的 Samba LDAP 支持的一部分，目前是占位符 |
| `ldaps port` | 此参数是未完成的 Samba LDAP 支持的一部分，目前是占位符 |
| `ldaps root` | 此参数是未完成的 Samba LDAP 支持的一部分，目前是占位符 |
| `ldaps root passwd` | 此参数是未完成的 Samba LDAP 支持的一部分，目前是占位符 |
| `ldaps server` | 此参数是未完成的 Samba LDAP 支持的一部分，目前是占位符 |
| `ldaps suffix` | 此参数是未完成的 Samba LDAP 支持的一部分，目前是占位符 |
| `announce` | 开启 LAN 渲染器公告。有三种状态：`Yes`、`No` 和 `Auto`。 |
| `interval` | 指定缓存打印队列状态的秒数。默认值为 `10`。将其设置为 `0` 将禁用缓存。 |
| `load printers` | 开启加载系统中存在的打印机。默认值为 `Yes`。 |
| `local master` | 在选举中开启 `nmbd` 作为本地浏览器。 |
| `lock dir` | `lock directory` 的同义词 |
| `lock directory` | Samba 可写且全局可读的目录。默认值为 `/samba/var/locks` |
| `log file` | 日志路径和文件名。 |
| `log level` | `debug level` 的同义词 |
| `logon drive` | 设置 NT 的驱动器名称。默认值为空字符串。 |
| `logon home` | 设置 Windows 9x 或 NT 的主目录。默认值为 `\%N\%U` |
| `logon path` | 指定相对于 `[logon]` 共享的路径，包含标准的 USER.DAT、USER MAN 以及开始菜单、网络邻域和程序文件夹。 |
| `logon script` | 指定在客户端运行的 DOS 脚本路径。此参数允许所有 `%宏`。默认值为空字符串。 |
| `machine password timeout` | 请求更改机器密码之间间隔秒数。用于 NT 域控制。默认设置为 `604800` 秒，即 `1` 周。 |
| `mangled stack` | 指定最近重命名文件的缓存大小。默认值为 `50` |
| `map to guest` | 当使用 `security-share` 以外的安全模式（如 `server` 和 `domain`）时，使用此参数将告知 `smbd` 如何处理无效登录请求。该参数有三个可能的值：

- `Never`（从不）：拒绝密码错误的用户登录请求。默认值。
- `Bad User`（用户错误）：拒绝密码错误的用户登录请求，除非用户名不存在，此时将其视为访客并映射到 `guest` 账户。
- `Bad Password`（密码错误）：将所有密码错误的用户登录都视为访客并映射到 `guest` 账户。 |
| `max disk size` | 指定返回给客户端的磁盘/可用磁盘空间的最大兆字节（MB）。此默认值为 `0`，意味着无限制。 |
| `max log size` | 指定 Samba 开始创建新日志文件的大小（单位为千字节 K）。同时，当前日志文件将被重命名为 `.old` 扩展名。默认值为 `5000`。 |
| `max mux` | 指定 Samba 服务器客户端可以进行的并发操作的最大数量。默认值为 `50`。 |

## 表 A.1 仅全局部分的参数（续）。

| 参数 | 说明 |
|---|--- |
| `max open files` | 指定 Samba 进程尝试同时打开的文件最大数量。默认值为 `10,000`。 |
