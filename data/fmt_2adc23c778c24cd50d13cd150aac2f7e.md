
## 第 8 章 • DNS 的攻击与防御

全局区域传输访问列表是允许或限制区域传输的地方（也可以为每个区域设置——区域设置将覆盖全局设置）：

```
allow-transfer

{

# 几种格式都是有效的

192.168.0.0/24;

127.0.0.1;

ACL_NAME;

KEY_ID;

}
```

`allow-query` 与 `allow-transfer` 类似，但它限制了可以使用此服务器进行解析的客户端：

```
allow-query

{

# 几种格式都是有效的

192.168.0.0/24;

127.0.0.1;

ACL_NAME;

KEY_ID;

}
```

`blackhole` 选项指定了不回复/通信的地址范围：

```
blackhole

{}
```

多种格式都是有效的。建议在 `blackhole` 列表中包含 Bogons 列表：

```
192.168.0.0/24;

127.0.0.1;

ACL_NAME;
```

![](img-729efc56f204a2ebffb8295c3a2dfdfb_456_0.png)

### DNS 的攻击与防御 • 第 8

尽可能进行限制和监控。由 Rob Thomas 编写的 [Secure Bind Template](http://www.cynru.com/Documents/secure-bind-template.html) 是一个很好的开始。定期检查 cynru 网站以获取更新或更改。当然，任何指南都不应该盲目执行。理解这些设置及其工作原理是必不可少的。

`BIND` 配置文件遵循简单的 Unix 配置文件语法。特定选项在括号内设置，其关联参数也设置在其中。后续章节解释了与安全相关的配置，随后是代码示例。为了方便 Windows 用户使用，某些语法可能会省略或修改。欲了解易于理解的 `BIND` 配置细节，请参阅 `www.nlias/reference/bind-doc/html/config.html`。

### 访问控制列表 (ACLs)

虽然 `ACL` 可能会对公众提供良好的服务限制，但不建议使用单个服务器托管内部和外部区域。尽管很流行，但如果托管多个区域，应该将执行权威和和器职责的服务器分开。

### 日志

`BIND` 支持不同的级别。应该定期检查日志。日志的一个良好原则是：太少会不起作用，太多则会影响维护。

### 独立区域文件

每个区域文件都可以包含自己的 `ACL` 列表和自定义设置以覆盖全局设置。这是一个正向和反向区域的示例：

```
zone "example.com"

{

type master;

file "foo/bar/example.com.db";

allow-query {

  any;

}

allow-transfer {

  none;

}

}
```

### 访问控制列表列表

`BIND` 支持在配置文件中使用 `ACL`。`ACL` 可用于限制访问的组：

```
acl "internal-network" {

  192.168.0.0/24;

  127.0.0.1;

}
```

### 日志

`BIND` 支持不同的级别。应该定期检查日志。日志的一个良好原则是：太少会不起作用，太多则会影响维护。

```
{

channel "detailed"

{

file "/foo/bar/0.168_192_detailed.log"

syslog local0;

severity dynamic;

};

}
```

### 调试日志

如果你想密切关注 `192.168.0.0/24` 的查询怎么办？你可以针对该记录实现调试日志（过度日志会导致系统崩溃，因此请确保你理解后果）

---

### DNS 的攻击与防御 • 第 8

尽可能进行限制和监控。由 Rob Thomas 编写的 [Secure Bind Template](http://www.cynru.com/Documents/secure-bind-template.html) 是一个很好的开始。定期检查 cynru 网站以获取更新或更改。当然，任何指南都不应该盲目执行。理解这些设置及其工作原理是必不可少的。

`BIND` 配置文件遵循简单的 Unix 配置文件语法。特定选项在括号内设置，其关联参数也设置在其中。后续章节解释了与安全相关的配置，随后是代码示例。为了方便 Windows 用户使用，某些语法可能会省略或修改。欲了解易于理解的 `BIND` 配置细节，请参阅 `www.nlias/reference/bind-doc/html/config.html`。

### 通用 BIND 选项

所需的配置包含在 `options` 字段中。需要指定文件目录和通用操作设置。记住同时记录内存和通用统计信息以建立基准。当问题出现时，基准将有助于排除故障。

```
statistics-file "/bind_directory/named.stats"

memstats-file "/bind_directory/named.memstats"

dump-file "/var/adm/bind.dump"

zone-statistics yes;
```

通过 `DNS NOTIFY` 消息进行 DoS 攻击是有可能的，因此应关闭或限制为仅可通过信任介质（SSH 隧道）访问的系统：

```
notify no;
```

区域传输的最大超时时间应设置为低值：
```
max-transfer-time-in 60;
```

如果 `BIND` 运行在静态接口上，应将动态接口选项设置为 0：
```
interface-interval 0;
```

## 第 8 章 • DNS 的攻击与防御

全局区域传输访问列表是允许或限制区域传输的地方（也可以为每个区域设置——区域设置将覆盖全局设置）：

```
allow-transfer

{

# 几种格式都是有效的

192.168.0.0/24;

127.0.0.1;

ACL_NAME;

KEY_ID;

}
```

`allow-query` 与 `allow-transfer` 类似，但它限制了可以使用此服务器进行解析的客户端：

```
allow-query

{

# 几种格式都是有效的

192.168.0.0/24;

127.0.0.1;

ACL_NAME;

KEY_ID;

}
```

`blackhole` 选项指定了不回复/通信的地址范围：

```
blackhole

{}
```

多种格式都是有效的。建议在 `blackhole` 列表中包含 Bogons 列表：

```
192.168.0.0/24;

127.0.0.1;

ACL_NAME;
```

![](img-729efc56f204a2ebffb8295c3a2dfdfb_456_0.png)

# 436 第 8 章 · DNS 的攻击与防御

日志语句位于配置中，第一条日志语句决定日志记录，其余语句仅发出警告。如果没有日志语句，日志配置将默认为以下内容：

```
logging

{

  category default ( default_syslog, default_debug );

  category panic ( default_syslog, default_stderr );

  category packet ( default_debug );

  category eventlib ( default_debug );

}
```
