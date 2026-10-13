
```
define('confConnectionCacheSize','2')dnl
```

`ConnectionCacheTimeout` 定义了空闲连接在关闭之前在缓存中保留的时间。默认是 300 秒，在 `/etc/mail/sendmail.cf` 中的设置如下：

+ - `OConnectionCacheTimeout=300`

如果你想更改超时时间，可以在你的 `mc` 文件中使用以下内容设置：

```
define('confConnectionCacheTimeout','600')dnl
```

这告诉 Sendmail 在关闭空闲连接前将其保留 600 秒（10 分钟）。

### 控制消息的最大大小（重复部分）

要控制通过 Sendmail 发送或接收的邮件大小，请在你的 `m4` 文件中使用如下的 `MessageSize` 选项：

```
# maximum message size
define('confMAX_MESSAGE_SIZE','1000000')dnl
```

使用 `m4` 命令重新生成 `/etc/mail/sendmail.cf` 文件后，你将在 `/etc/mail/sendmail.cf` 文件中看到以下行：

+ - `OMessageSize=1000000`

这告诉 Sendmail 将最大消息大小设置为 1,000,000 字节（约 1MB）。当然，你可以根据需求选择不同的数字。任何大于 `MaxMessage` 选项设置值的消息都将被拒绝。

### 连接缓存（重复部分）

Sendmail 在处理队列时，使用 `ConnectionCacheSize` 和 `ConnectionCache` 超时来控制 IPC 连接的连接缓存。

它在缓存中寻找预先存在的活动连接。`ConnectionCacheSize` 定义了允许的并发打开连接数。默认值是两个，在 `/etc/mail/sendmail.cf` 中的设置如下：

+ - `OConnectionCacheSize=2`

你可以在你的 `mc` 文件中使用以下内容设置它：

```
define('confConnectionCacheSize','2')dnl
```

`ConnectionCacheTimeout` 定义了空闲连接在关闭之前在缓存中保留的时间。默认是 300 秒，在 `/etc/mail/sendmail.cf` 中的设置如下：

+ - `OConnectionCacheTimeout=300`

如果你想更改超时时间，可以在你的 `mc` 文件中使用以下内容设置：

```
define('confConnectionCacheTimeout','600')dnl
```

这告诉 Sendmail 在关闭空闲连接前将其保留 600 秒（10 分钟）。

### 控制消息的最大大小（再次重复部分）

要控制通过 Sendmail 发送或接收的邮件大小，请在你的 `m4` 文件中使用如下的 `MessageSize` 选项：

```
# maximum message size
define('confMAX_MESSAGE_SIZE','1000000')dnl
```

使用 `m4` 命令重新生成 `/etc/mail/sendmail.cf` 文件后，你将在 `/etc/mail/sendmail.cf` 文件中看到以下行：

+ - `OMessageSize=1000000`

这告诉 Sendmail 将最大消息大小设置为 1,000,000 字节（约 1MB）。当然，你可以根据需求选择不同的数字。任何大于 `MaxMessage` 选项设置值的消息都将被拒绝。

### 连接缓存（再次重复部分）

Sendmail 在处理队列时，使用 `ConnectionCacheSize` 和 `ConnectionCache` 超时来控制 IPC 连接的连接缓存。

它在缓存中寻找预先存在的活动连接。`ConnectionCacheSize` 定义了允许的并发打开连接数。默认值是两个，在 `/etc/mail/sendmail.cf` 中的设置如下：

+ - `OConnectionCacheSize=2`

你可以在你的 `mc` 文件中使用以下内容设置它：

```
define('confConnectionCacheSize','2')dnl
```

`ConnectionCacheTimeout` 定义了空闲连接在关闭之前在缓存中保留的时间。默认是 300 秒，在 `/etc/mail/sendmail.cf` 中的设置如下：

+ - `OConnectionCacheTimeout=300`

如果你想更改超时时间，可以在你的 `mc` 文件中使用以下内容设置：

```
define('confConnectionCacheTimeout','600')dnl
```

这告诉 Sendmail 在关闭空闲连接前将其保留 600 秒（10 分钟）。

### 控制消息的最大大小（第三次重复部分）

要控制通过 Sendmail 发送或接收的邮件大小，请在你的 `m4` 文件中使用如下的 `MessageSize` 选项：

```
# maximum message size
define('confMAX_MESSAGE_SIZE','1000000')dnl
```

使用 `m4` 命令重新生成 `/etc/mail/sendmail.cf` 文件后，你将在 `/etc/mail/sendmail.cf` 文件中看到以下行：

+ - `OMessageSize=1000000`

这告诉 Sendmail 将最大消息大小设置为 1,000,000 字节（约 1MB）。当然，你可以根据需求选择不同的数字。任何大于 `MaxMessage` 选项设置值的消息都将被拒绝。（*注：由于原文中存在大量重复段落，此处已按要求保留翻译内容，以确保不漏掉原文任何行。*）

# maximum message size

define('confMAX_MESSAGE_SIZE','1000000')dnl

使用 `m4` 命令重新生成 `/etc/mail/sendmail.cf` 文件后，你将在 `/etc/mail/sendmail.cf` 文件中看到以下行：

+ - `OMessageSize=1000000`

这告诉 Sendmail 将最大消息大小设置为 1,000,000 字节（约 1MB）。当然，你可以根据需求选择不同的数字。任何大于 `MaxMessage` 选项设置值的消息都将被拒绝。

### 连接缓存（第三次重复部分）

Sendmail 在处理队列时，使用 `ConnectionCacheSize` 和 `ConnectionCache` 超时来控制 IPC 连接的连接缓存。

它在缓存中寻找预先存在的活动连接。`ConnectionCacheSize` 定义了允许的并发打开连接数。默认值是两个，在 `/etc/mail/sendmail.cf` 中的设置如下：

+ - `OConnectionCacheSize=2`

你可以在你的 `mc` 文件中使用以下内容设置它：

```
define('confConnectionCacheSize','2')dnl
```

`ConnectionCacheTimeout` 定义了空闲连接在关闭之前在缓存中保留的时间。默认是 300 秒，在 `/etc/mail/sendmail.cf` 中的设置如下：

+ - `OConnectionCacheTimeout=300`

如果你想更改超时时间，可以在你的 `mc` 文件中使用以下内容设置：

```
define('confConnectionCacheTimeout','600')dnl
```

这告诉 Sendmail 在关闭空闲连接前将其保留 600 秒（10 分钟）。

### 控制消息的最大大小（第四次重复部分）

要控制通过 Sendmail 发送或接收的邮件大小，请在你的 `m4` 文件中使用如下的 `MessageSize` 选项：

```
# maximum message size
define('confMAX_MESSAGE_SIZE','1000000')dnl
```

使用 `m4` 命令重新生成 `/etc/mail/sendmail.cf` 文件后，你将在 `/etc/mail/sendmail.cf` 文件中看到以下行：

+ - `OMessageSize=1000000`

这告诉 Sendmail 将最大消息大小设置为 1,000,000 字节（约 1MB）。当然，你可以根据需求选择不同的数字。任何大于 `MaxMessage` 选项设置值的消息都将被拒绝。

# maximum message size

define('confMAX_MESSAGE_SIZE','1000000')dnl

使用 `m4` 命令重新生成 `/etc/mail/sendmail.cf` 文件后，你将在 `/etc/mail/sendmail.cf` 文件中看到以下行：

+ - `OMessageSize=1000000`

这告诉 Sendmail 将最大消息大小设置为 1,000,000 字节（约 1MB）。当然，你可以根据需求选择不同的数字。任何大于 `MaxMessage` 选项设置值的消息都将被拒绝。（*注：由于原文中存在大量重复段落，此处已按要求保留翻译内容，以确保不漏掉原文行行。*）
