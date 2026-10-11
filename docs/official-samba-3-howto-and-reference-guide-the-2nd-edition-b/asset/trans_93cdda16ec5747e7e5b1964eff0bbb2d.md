
### 客户端 NTLMv2 认证
此参数确定 smbclient(8) 是否尝试使用 NTLMv2 加密密码响应来向服务器进行身份验证。

如果启用，则仅发送 NTLMv2 和 LMv2 响应（两者均比早期版本安全得多）。许多服务器（包括 NT4 SP4、Win9x 和 Samba 2.2）与 NTLMv2 不兼容。

同样，如果启用，**NTLMv1**、**客户端 lanman 认证** 和 **客户端明文认证** 将被禁用。这也将禁用共享级认证。

如果禁用，客户端将发送 NTLM 响应（可能还包括 LANMAN 响应），具体取决于 **client lanman auth** 的值。

请注意，某些站点（特别是遵循“最佳实践”安全策略的站点）仅允许 NTLMv2 响应，而不允许较弱的 LM 或 NTLM。

### 客户端明文认证 **(G)**
默认值：*client plaintext auth* = *yes*

指定如果服务器不支持加密密码，客户端是否应发送明文密码。

### 客户端 schannel **(G)**
默认值：*client schannel* = *auto*

示例：*client schannel* = *yes*

此参数控制客户端是否提供甚至要求使用 netlogon 通道。*client schannel* = *no* 不提供该通道，*client schannel* = *auto* 提供该通道但不强制执行，而 *client schannel* = *yes* 则在服务器无法使用 netlogon 通道时拒绝访问。

### 客户端签名 **(G)**
默认值：*client signing* = *auto*

此参数控制客户端是否提供或要求与其通信的服务器使用 SMB 签名。可能的值为 *auto*、*mandatory* 和 *disabled*。

当设置为 auto 时，提供 SMB 签名，但不强制执行。当设置为 mandatory 时，要求 SMB 签名；当设置为 disabled 时，也不提供 SMB 签名。

### 客户端使用 spnego **(G)**
默认值：*client use spnego* = *yes*

此变量控制 Samba 客户端是否尝试与支持该功能的服务器（包括 Windows XP、Windows 2000 和 Samba 3.0）使用简单保护协商（如 rfc2478 中规定）来商定身份验证机制。这特别是使 Kerberos 认证成为可能。

### 注释 **(S)**
默认值：*comment* = *No comment*

示例：*comment* = *Fred’s Files*

这是一个文本字段，当客户端查询服务器时会在共享旁边看到，无论是通过网络邻居还是通过 **net view** 列出可用共享。如果希望设置显示在机器名称旁边的字符串，请参阅 *server string* 参数。

### 配置文件 **(G)**
默认值：*无默认值*

示例：*config file = /usr/local/samba/lib/smb.conf.%m*

此选项允许你覆盖要使用的配置文件，而不是使用默认文件（通常是 *smb.conf*）。这里存在一个先有鸡还是先有蛋的问题，因为这个选项是在配置文件中设置的！

因此，如果在加载参数时配置文件的名称已更改，那么它将从新的配置文件中重新加载参数。

此选项接受通常的替换符，这可能非常有用。

如果配置文件不存在，则不会加载它（允许你仅为少数几个客户端特殊处理配置文件）。

### 复制 **(S)**
默认值：*无默认值*

示例：*copy = otherservice*

此参数允许你“克隆”服务条目。指定的服务将被简单地复制为当前服务的名称。当前部分中指定的任何参数都将覆盖被复制部分中的参数。

此功能让你可以轻松设置一个“模板”服务并创建类似的服务。请注意，被复制的服务必须出现在配置文件中的复制服务之前。

### 创建模式
此参数是 *create mask* 的同义词。

### 创建掩码 **(S)**
默认值：*create mask = 07440755*

示例：*create mask = 0775*

当创建文件时，根据从 DOS 模式到 UNIX 权限的映射计算必要的权限，然后所得的 UNIX 模式与此参数进行按位“AND”运算。可以将此参数视为文件 UNIX 模式的按位掩码。此处未设置的任何位将在文件创建时从设置的模式中移除。

此参数的默认值会从 UNIX 模式中移除 *group* 和 *other* 的写和执行位。

随后，Samba 会将从此参数生成的 UNIX 模式与 *force create mode* 参数的值进行按位“OR”运算，后者默认设置为 *000*。

此参数不影响目录掩码。详情请参见参数 `directory mask`。

请注意，此参数不适用于由 Windows NT/2000 ACL 编辑器设置的权限。如果管理员希望同时对访问控制列表强制应用掩码，他们需要设置 `security mask`。

### csc 策略 **(S)**
默认值：`csc policy = manual`

示例：`csc policy = programs`

这代表 `客户端缓存策略`，指定能够离线缓存的客户端将如何缓存共享中的文件。有效值为：manual, documents, programs, disable。

这些值对应于在 Windows 服务器上使用的值。

例如，包含漫游配置文件共享可以使用 `csc policy = disable` 禁用离线缓存。

### cups 选项 **(S)**
默认值：`cups options = "raw,media=a4,job-sheets=secret,secret"`

示例：`cups options = "raw,media=a4,job-sheets=secret,secret"`

此参数仅在将 `printing` 设置为 `cups` 时适用。其值是传递给 cups 库的选项自由格式字符串。

你可以传递任何 CUPS 已知的通用打印选项（如 CUPS“软件用户手册”中列出的）。你还可以传递任何适用于目标队列的特定打印机选项（如 `loptions -d printername -I` 中列出的）。

如果你的 CUPS 服务器 `error_log` 文件在通过 Samba 从 Windows 客户端打印时包含诸如“Unsupported format \ application/octet-stream”等消息，你应该将此参数设置为 `raw`。不再需要在 `/etc/cups/mime.{conv,types}` 中启用系统范围的 raw 打印。

### cups 服务器 **(G)**
默认值：`cups server = MYCUPSSERVER`

示例：`cups server = MYCUPSSERVER`

此参数仅在将 `printing` 设置为 `cups` 时适用。

如果设置，此选项将覆盖 CUPS `client.conf` 中的 ServerName 选项。如果你拥有连接到不同 CUPS 守护程序的虚拟 Samba 服务器，这是必要的。

### deadtime **(G)**
默认值：`deadtime = 0`

示例：`deadtime = 15`

参数的值（十进制整数）表示在连接被视为断开并断开之前，无活动的分钟数。仅当打开的文件数为零时，deadtime 才生效。

这对于防止服务器资源被大量非活动连接耗尽非常有用。

大多数客户端在连接断开时具有自动重连功能，因此在大多数情况下，此参数对用户应是透明的。

建议大多数系统使用几分钟的超时无效时间。

deadtime 为零表示不应执行自动断开连接。

### 调试高分辨率时间戳 **(G)**
默认值：*debug hires timestamp = no*

有时需要日志消息中的时间戳具有高于秒的分辨率，此布尔参数在开启时为时间戳消息头添加微秒分辨率。

请注意，要使其生效，参数 *debug timestamp* 必须处于开启状态。

### 调试 pid **(G)**
默认值：*debug pid = no*

当多个 forked smbd(8) 进程仅使用一个日志文件时，可能很难跟踪哪个进程输出了哪条消息。此布尔参数在开启时会将进程 ID 添加到日志文件中的时间戳消息头中。

请注意，要使其生效，参数 *debug timestamp* 必须处于开启状态。

### 时间戳日志
此参数是 *debug timestamp* 的同义词。

### 调试时间戳 **(G)**
默认值：*debug timestamp = yes*

Samba 调试日志消息默认带有时间戳。如果你正在运行高 *debug level*，这些时间戳可能会造成干扰。此布尔参数允许关闭时间戳功能。

### 调试 uid **(G)**
默认值：*debug uid = no*

Samba 有时以 root 身份运行，有时以连接用户身份运行。如果开启，此布尔参数会将当前的 euid、egid、uid 和 gid 插入日志文件中的时间戳消息头中。

请注意，要使其生效，参数 *debug timestamp* 必须处于开启状态。

### 默认大小写 **(S)**
默认值：*default case = lower*

请参阅 *name mangling* 章节。也请注意 *short preserve case* 参数。

### 默认 devmode **(S)**
默认值：*default devmode = no*

