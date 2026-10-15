
<IfDefine> <IfDefine [!]parameter-name> ...

```
该集合中的任何其他指令都仅在 `parameter-name` 为真时处理——如果使用了感叹号 (`!`)，则在为假时处理。标签类型结构的存在意味着它必须有一个闭合标签。
```

<IfModule> <IfModule [!]module-name> ...

```
这使得包含在起始和结束标签内的任何指令都仅在模块激活时被处理——如果使用了感叹号 (`!`)，则在模块未激活时处理。
```

Include Include <file-path|wildcard-path>

```
这告诉 Apache 包含位于适当路径或目录下的任何其他配置文件。
```

## KeepAlive KeepAlive max-requests

```
KeepAlive On|Off
```

这用于控制 Apache 中的持久连接。你可以指定是否开启此功能，以及适用于连接的最大请求数。

## KeepAliveTimeout KeepAliveTimeout seconds

此指令允许你指定保持请求活跃所需的秒数。默认值为 15。

```
<Limit> <Limit method [method] ... > ...
```

这用于将访问控制的影响限制到 HTTP 方法。任何其他方法将无法根据 `<Limit>` 内部提供的指令起作用。

```
<LimitExcept> <LimitExcept method [method] ... > ...
```

这是 `<Limit>` 的相反操作；任何不符合提供方法的都将应用带有该标签的指令。

## LimitInternalRecursion LimitInternalRecursion number [number]

这防止 Apache 在模块中的查找请求不断尝试应用查找命令时进入无限循环。默认值为 20。

## 第 8 章 • Apache 服务器：安装与配置

## LimitRequestBody LimitRequestBody bytes

这允许你限制客户端向 Apache 发送的请求大小。这通常用于限制表单中的信息。

## LimitRequestFields LimitRequestFields number

这允许你限制允许传递到页面的字段或变量的数量。默认设置为 100。

## LimitRequestFieldsSize LimitRequestSize bytes

此指令允许你指定请求头内请求的最大 own。Apache 文档指出，这允许对客户端请求行为进行更强大的控制，并有助于避免某些类型的拒绝服务 (DoS) 攻击。

## LimitRequestLine LimitRequestLine bytes

这限制了 HTTP 请求行允许的字节数。默认值为 8190。

## Listen Listen [IP-address:]port

`Listen` 可以代替之前讨论的 `BindAddress`。根据需要多次提供 `Listen` 指令，可以使用任何 IP 地址和/或端口。

## ListenBacklog ListenBacklog backlog

此值设置为 511。`ListenBacklog` 设置了等待连接队列的最大长度。

```
<Location> <Location URL-path|URL>
```

这通过 URL 而不是实际路径或文件提供访问控制。与 `<Directory>` 或 `<File>` 一样，你可以指定应用于请求的额外指令。

```
<LocationMatch> <LocationMatch regex> ...
```
