
# BrowseAllow

## 示例

```
BrowseAllow from 192.0.2.0/255.255.255.0
BrowseAllow from *.domain.com
```

## 描述

`BrowseAllow` 指令指定接受浏览包的系统或网络。默认是接受来自所有主机的浏览包。

主机和域名匹配需要你启用 `HostNameLookups` 指令。

IP 地址匹配支持精确匹配、匹配网络掩码为 `255.0.0.0`、`255.255.0.0` 和 `255.255.255.0` 的网络的部分地址，以及具有特定网络或位数的网络地址。

# BrowseDeny

## 示例

```
BrowseDeny from all
BrowseDeny from none
BrowseDeny from 192.0.2
BrowseDeny from 192.0.2.0/24
BrowseDeny from 192.0.2.0/255.255.255.0
BrowseDeny from *.domain.com
```

## 描述

`BrowseDeny` 指令指定拒绝浏览包的系统或网络。默认是不拒绝来自任何主机的浏览包。

主机和域名匹配需要你启用 `HostNameLookups` 指令。

IP 地址匹配支持精确匹配、匹配网络掩码为 `255.0.0.0`、`255.255.0.0` 和 `255.255.255.0` 的网络的部分地址，以及具有特定网络或位数的网络地址。

# BrowseOrder

## 示例

```
BrowseOrder allow,deny
BrowseOrder deny,allow
```

## 描述

`BrowseOrder` 指令指定允许/拒绝处理的顺序。系统会识别以下设置；默认顺序为 `deny,allow`：

- `allow,deny`. 除非被特定拒绝，否则接受浏览包。
- `deny,allow`. 除非被特定允许，否则拒绝浏览包。

# BrowseInterval

## 示例

```
BrowseInterval 0
BrowseInterval 30
```

## 描述

`BrowseInterval` 指令指定浏览更新之间的最大间隔时间。指定值为 `0` 秒将禁用发出的浏览更新，但允许服务器接收来自其他主机的打印机信息。

> 注意：
`BrowseInterval` 的值应始终小于 `BrowseTimeout` 值；否则打印机和类将在更新之间从客户端系统中消失。

# BrowsePoll

## 示例

```
BrowsePoll 192.0.2.2:631
BrowsePoll host.domain.com:631
```

## 描述

`BrowsePoll` 指令每隔 `BrowseInterval` 秒轮询服务器一次可用打印机。可以指定多个 `BrowsePoll` 指令来轮询多个服务器。

如果 `BrowseInterval` 设置为 `0`，则服务器每 `30` 秒轮询一次。

# BrowsePort

## 示例

```
BrowsePort 631
BrowsePort 9999
```

## 描述

`BrowsePort` 指令指定用于浏览包的 UDP 端口号。默认端口号为 `631`。

> 注意：
你必须在所有你想看到的系统中将 `BrowsePort` 设置为相同值。

# BrowseRelay

## 示例

```
BrowseRelay 193.0.2.1 192.0.2.255
BrowseRelay 193.0.2.0/24
BrowseRelay 193.0.2.0/255.255.255.0
BrowseRelay *.domain.com
```

## 描述

`BrowseRelay` 指令指定从一个地方到另一个地方转发浏览信息的源和目的。根据需要指定多个 `BrowseRelay` 指令。这有效地提供了对局域网（LAN）打印机的访问。

# BrowseShortNames

## 示例

```
BrowseShortNames Yes
BrowseShortNames No
```

## 描述

`BrowseShortNames` 指令指定在可能的情况下是否使用短名称进行远程打印。短名称是不带服务器的远程打印机名称。如果检测到多个同名打印机，则会而改用长名称。

# BrowseTimeout

## 示例

```
BrowseTimeout 300
BrowseTimeout 60
```

## 描述

`BrowseTimeout` 指令设置浏览包接收到的打印机或类信息的超时时间。打印机或类超时后，将从可用目标列表中移除。

> 注意：
`BrowseTimeout` 的值应始终大于 `BrowseInterval` 值。否则，打印机和类将在更新之间从客户端系统中消失。

# Browsing

## 示例

```
Browsing On
Browsing Off
```

## 描述

`Browsing` 指令控制是否启用网络浏览。默认设置为 `On`。

# Deny

## 示例

```
Deny from nnn.nnn.nnn.nnn
Deny from nnn.nnn.nnn.nnn/mm
Deny from nnn.nnn.nnn.nnn/mmm.mmm.mmm.mmm
```

## Description

`Deny` 指令指定了允许访问服务器的主机名、IP 地址或网络。`Deny` 指令是累积的，因此可以使用多个 `Deny` 指令来允许多个主机或网络的访问。`/mm` 表示法指定 CIDR 网络掩码，如前面的表 A.1 所示。

`Deny` 指令必须出现在 `Location` 指令内部。

# DocumentRoot

### 示例

```
DocumentRoot /usr/share/doc/cups
DocumentRoot /foo/bar/doc/cups
```

### Description

`DocumentRoot` 指令指定了 CUPS 中 HTTP 服务器的 Web 内容的位置。如果没有指定绝对路径，则假设它相对于 `ServerRoot` 目录。默认目录为 `/usr/share/doc/cups`。

文档会首先在客户端请求的主要语言的子目录中查找（例如，法语对应 `/usr/share/doc/cups/fr/...`），然后直接在 `DocumentRoot` 目录下查找（例如，`/usr/share/doc/cups...`），因此可以通过为所需的种语言提供子目录来实现 Web 内容的本地化。

# Encryption

### 示例

```
Encryption Never
Encryption IfRequested
Encryption Required
Encryption Always
```

### Description

`Encryption` 指令必须出现在 `Location` 部分内部，并指定该位置的加密设置。所有位置的默认设置为 `IfRequested`。

注意：

由于基于位置的加密需要支持 HTTP Upgrade 协议，你必须使用 `SSLPort` 指令才能配合大多数 Web 浏览器使用加密。

# ErrorLog

### 示例

```
ErrorLog /var/log/cups/error_log
ErrorLog /var/log/cups/error_log-%s
ErrorLog syslog
```

### Description

`ErrorLog` 指令设置错误日志文件名。如果文件名是绝对路径，则假设它相对于 `ServerRoot` 目录。默认错误日志文件为 `/var/log/cups/error_log`。

要在文件名中包含服务器名称，请在名称中使用 `%s`。

特殊名称 `syslog` 可将错误信息发送到系统日志而不是普通文件。

# FilterLimit

### 示例

```
FilterLimit 0
FilterLimit 200
FilterLimit 1000
```

### Description

`FilterLimit` 指令设置所有运行作业过滤器的最大成本。它可以限制在服务器上运行的过滤器程序数量，从而最大限度地减少磁盘、内存和 CPU 资源问题。设置为 `0` 则禁用过滤器限制。

到非 PostScript 打印机的平均打印需要大约 `200` 的过滤器限制。PostScript 打印机需要大约其的一半（`100`）。

将限制设置在这些阈值以下可以限制调度器在任何时间打印单个作业。

默认限制为 `0`。

# FontPath

### 示例

```
FontPath /foo/bar/fonts
FontPath /usr/share/cups/fonts:/foo/bar/fonts
```

### Description

`FontPath` 指令指定了搜索字体时使用的字体路径。多个目录之间用冒号（`:`）隔开。默认字体路径为 `/usr/share/cups/fonts`。

# Group

### 示例

```
Group sys
Group system
Group root
```

### Description

`Group` 指令指定用于过滤器和 CGI 程序的 Unix 组。根据操作系统的，默认组为 `sys`、`system` 或 `root`。

# HostNameLookup

### 示例

```
HostNameLookups On
HostNameLookups Off
HostNameLookups Double
```

### Description

`HostNameLookups` 指令控制 CUPS 是否查找用于连接的主机名。`Double` 设置会导致 CUPS 验证从地址解析的主机名是否与该主机名返回的地址之一匹配。双重查找还可以防止未注册地址的客户端连接到你的服务器。默认值为 `Off`。

## 文件指令

注意：

主机查找会延迟处理来自客户端机器的新连接。如果你的客户端和名称服务器在小型局域网内，这种延迟可能很小。

对于较大的网络或当你允许访问互联网上的系统时，名称查找时间可能会成为严重的性能问题。

默认设置为 `Off`，以避免随主机查找的潜在服务器性能问题。仅在绝对需要时才将此选项设置为 `On` 或 `Double`。

# ImplicitClasses

### 示例

```
ImplicitClasses On
ImplicitClasses Off
```

### Description

`ImplicitClasses` 指令控制是否根据可用网络打印机和类创建隐式类。默认设置为 `On`，但如果 `Browsing` 被关闭，会自动设置为 `Off`。

# KeepAlive

### 示例

```
KeepAlive On
KeepAlive Off
```

### Description

`KeepAlive` 指令控制是否支持持久 HTTP 连接。默认值为 `On`。

注意：

HTTP/1.1 客户端自动支持持久连接，而 HTTP/1.0 客户端必须通过每个请求的 `Connection:` 字段中的 `Keep-Alive` 属性显式请求连接。

# KeepAliveTimeout

### 示例

```
KeepAliveTimeout 60
KeepAliveTimeout 30
```

### Description

`KeepAliveTimeout` 指令控制在最后一个请求后持久 HTTP 连接保持开启多长时间。默认值为 `60` 秒。

# Limit

### 示例

```
<Limit GET POST>
...
</Limit>
```

```
<Limit ALL>
...
</Limit>
```

### Description

`Limit` 指令将特定类型 HTTP 请求的访问控制指令分组，并必须出现在 `Location` 部分内部。可以对单个类型（`DELETE`, `GET`, `HEAD`, `OPTIONS`, `POST`, `PUT`, `TRACE`）或所有类型（`ALL`）限制访问。请求类型在 Apache 中是大小写敏感的。

# LimitExcept

### 示例

```
<LimitExcept GET POST>
...
</LimitExcept>
```

### Description

`LimitExcept` 指令将特定类型 HTTP 请求的访问控制指令分组。与 `Limit` 指令不同，`LimitExcept` 限制排除列表之外的所有请求的访问。

# LimitRequestBody

### 示例

```
LimitRequestBody 1048570
LimitRequestBody 10m
LimitRequestBody 0
```

### Description

`LimitRequestBody` 指令控制打印文件、IPP 请求和 POST 请求中 HTML 表单数据的限制。默认限制为 `0`，禁用限制检查。

另见 `MaxRequestSize` 指令。

# Listen

### 示例

```
Listen 127.0.0.1:631
Listen 192.0.2.1:80
Listen foo.bar.com:631
```

### Description

`Listen` 指令指定监听连接的网络地址和端口。可以提供多个 `Listen` 指令以启用监听多个地址。

`Listen` 指令与 `Port` 指令类似，但它允许你监听特定的接口或网络。

# Location

### 示例

```
<Location />
...
</Location>
<Location /admin>
...
</Location>
```

```
<Location /printers/name>
..
</Location>
```

### Description

`Location` 指令为指定的 HTTP 资源或路径指定访问控制和认证选项。`Allow`、`AuthClass`、`AuthGroupName`、`AuthType`、`Deny`、`Encryption`、`Limit`、`LimitExcept`、`Order`、`Require` 和 `Satisfy` 指令均可出现在位置内部。

# LogLevel

### 示例

```
+ Level none
LogLevel emerg
LogLevel alert
LogLevel crit
LogLevel error
LogLevel warn
LogLevel notice
LogLevel info
LogLevel debug
LogLevel debug2
```

### Description

`LogLevel` 指令指定 `ErrorLog` 文件的日志级别。每个错误级别都会记录其之前级别的所有日志。识别以下值：

+ `none`. 不记录任何日志。
+ `emerg`. 记录阻止服务器运行的紧急状况。
+ `alert`. 记录必须立即处理的警报。
+ `crit`. 记录阻止服务器运行的严重错误。
+ `error`. 记录普通错误。
+ `warn`. 记录错误和警告。
+ `notice`. 记录临时错误状况。
+ `info`. 记录所有请求和状态更改（默认值）。
+ `debug`. 记录基础调试信息。
+ `debug2`. 记录所有调试信息。

# MaxClients

## Examples

```
MaxClients 100
MaxClients 1024
```

## Description

`MaxClients` 指令控制服务器允许的最大并发客户端数量。默认值为 `100` 个客户端。

> NOTE：
由于由于每个打印作业都需要一个用于状态管道（status pipe）的文件描述符，CUPS 服务器在内部会将 `MaxClients` 的值限制为可用文件描述符的 `1/3`，以避免在大量作业正在打印时可能出现的问题。

# MaxJobs

## Examples

```
MaxJobs 100
MaxJobs 9999
MaxJobs 0
```

## Description

`MaxJobs` 指令控制保留在内存中的最大作业数量。当作业数量达到限制时，最老旧的已完成作业将自动从系统中清除，以为新作业腾出空间。如果所有已知作业仍处于等待处理或活动状态，则新作业将被拒绝。

将最大值设置为 `0` 将禁用此功能。默认设置为 `0`。

# MaxJobsPerPrinter

## Examples

```
MaxJobsPerPrinter 100
MaxJobsPerPrinter 9999
MaxJobsPerPrinter 0
```

## Description

`MaxJobsPerPrinter` 指令控制每个打印机或类别允许的最大活动作业数量。当打印机或类别达到限制时，新作业将被拒绝，直到其中一个活动作业完成、停止、中止或取消。

将最大值设置为 `0` 将禁用此功能。默认设置为 `0`。

# MaxJobsPerUser

## Examples

```
MaxJobsPerUser 100
MaxJobsPerUser 9999
MaxJobsPerUser 0
```

## Description

`MaxJobsPerUser` 指令控制每个用户允许的最大活动作业数量。当用户达到限制时，新作业将被拒绝，直到其中一个活动作业完成、停止、中止或取消。

将最大值设置为 `0` 将禁用此功能。默认设置为 `0`。

# MaxLogSize

## Examples

```
MaxLogSize 1048576
MaxLogSize 1m
MaxLogSize 0
```
