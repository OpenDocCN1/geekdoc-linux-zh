
`log_on_success`  += `HOST_DURATION`

`log_on_failure`  += `HOST`

`disable`          = `no`

``` 
# 示例所示：
```

`log_on_success` += `DURATION USERID`

`log_on_failure` += `USERID`

`nice` = `10`

``` 
# 示例所示：
```

`log_type` = `SYLOG authpriv`

`log_on_success` = `HOST PID`

`log_on_failure` = `HOST RECORD`

``` 
# 示例所示：
```

`only_from` = `192.168.1.0`

`only_from` = `localhost`

`no_access` = `192.168.1.15`

`instances` = `60`

``` 
# 示例所示：
```

```
defaults {

  instances = 60

  log_type = FILE /var/log/servicelog

  log_on_success = HOST PID

  log_on_failure = HOST RECORD

  only_from = 192.168.1.0

  only_from = localhost

  no_access = 192.168.1.15

}
```

``` 
# 示例所示：
```

`included /etc/xinetd`

``` 
# 示例所示：
```

```
# Simple configuration file for xinetd

# Some defaults, and include /etc/xinetd.d/

defaults {

    instances       = 60

    log_type        = SYSLOG authpriv

    log_on_success = HOST PID

    log_on_failure = HOST

}

included /etc/xinetd.d/
```

``` 
# 示例所示：
```

```
# default: off

# 描述: POP3 服务允许用户\

# 使用 POP3 客户端（如 Netscape Communicator，\

# 或 fetchmail）访问他们的邮件。
```

``` 
# 示例所示：
```

```
# default: off

# 描述: The POP3 服务允许用户\

# 使用 POP3 客户端（如 Netscape Communicator，\

# 或 fetchmail）访问他们的邮件。

service pop3

socket_type      = stream

wait             = no

user             = root

server           = /usr/sbin/ipop3d

log_on_success  += HOST_DURATION

log_on_failure  += HOST

disable          = no
```

``` 
# 示例所示：
```

`log_on_success` += `DURATION USERID`

`log_on_failure` += `USERID`

`nice` = `10`

``` 
# 示例所示：
```

`log_type` = `SYLOG authpriv`

`log_on_success` = `HOST PID`

`log_on_failure` = `HOST RECORD`

``` 
# 示例所示：
```

`only_from` = `192.168.1.0`

`only_from` = `localhost`

`no_access` = `192.168.1.15`

`instances` = `60`

``` 
# 示例所示：
```

```
defaults {

  instances = 60

  log_type = FILE /var/log/servicelog

  log_on_success = HOST PID

  log_on_failure = HOST RECORD

  only_from = 192.168.1.0

  only_from = localhost

  no_access = 192.168.1.15

}
```

``` 
# 示例所示：
```

`included /etc/xinetd`

``` 
# 示例所示：
```

```
# xinetd 的简单配置文件

# 某些默认值，并包含 /etc/xinetd.d/

defaults {

    instances       = 60

    log_type        = SYSLOG authpriv

    log_on_success = HOST PID

    log_on_failure = HOST

}

included /etc/xinetd.d/
```

## TCP 包装器 (Wrappers)

为了安全限制，你可以使用 `only_from` 来限制某些远程主机的访问。`no_access` 属性拒绝来自列出的主机的访问，但允许其他主机访问。这些控制以 IP 地址作为值。你可以使用网络地址列出单个 IP 地址、一个 IP 地址范围或一个网络。`instances` 属性限制了特定服务可以同时运行的服务器进程数量。以下示例限制了对本地网络 `192.168.1.0` 和本地回环（`localhost`）的访问，拒绝了 `192.168.1.15`，并使用 `instances` 属性将一次的服务器进程数量限制为 `60`。

```
only_from = 192.168.1.0

only_from = localhost

no_access = 192.168.1.15

instances = 60
```

## xinetd 默认值和内部服务

此处显示了一个默认块示例：

```
defaults {

  instances = 60

  log_type = FILE /var/log/servicelog

  log_on_success = HOST PID

  log_on_failure = HOST RECORD

  only_from = 192.168.1.0

  only_from = localhost

  no_access = 192.168.1.15

}
```

`xinetd` 程序提供了几个内部服务，包括 `time`、`services` 和 `servers`，其中 `services` 提供当前活跃服务的列表，`servers` 提供服务器的信息；`admin` 提供 `xinetd` 管理支持。

## xinetd.d 目录中的服务文件

与其拥有一个巨大的 `xinetd.conf` 文件，不如将其拆分为多个配置文件，每个服务一个。你可以通过创建一个包含 `included` 属性的 `xinetd.conf` 文件来实现此，该属性指定一个存放不同配置文件的目录。在以下示例中，`xinetd.d` 目录存放 `swat` 等服务的 `xinetd` 配置文件。Fedora Core 使用了这种实现。这种方法的优势是只需为服务创建新的配置文件即可添加服务。修改服务只需编辑其配置文件，而不是整个 `xinetd.conf`。

```
included /etc/xinetd
```

![](img/70a65fc8f3408711ddea7ea368f31720_470_0.png)

## 第五部分：网络服务器

以下示例显示了 Fedora Core Linux 使用的 `xinetd.conf` 文件：

```
# xinetd 的简单配置文件

# 某些默认值，并包含 /etc/xinetd.d/

defaults {

    instances       = 60

    log_type        = SYSLOG authpriv

    log_on_success = HOST PID

    log_on_failure = HOST

}

included /etc/xinetd.d/
```

## TCP 包装器 (Wrappers)

为了安全限制，你可以使用 `only_from` 来限制某些远程主机的访问。`no_access` 属性拒绝来自列出的主机的访问，但允许其他主机访问。这些控制以 IP 地址作为值。你可以使用网络地址列出单个 IP 地址、一个 IP 地址范围或一个网络。`instances` 属性限制了特定服务可以同时运行的服务器进程数量。以下示例限制了对本地网络 `192.168.1.0` 和本地回环（`localhost`）的访问，拒绝了 `192.168.1.15`，并使用 `instances` 属性将一次的服务器进程数量限制为 `60`。

```
only_from = 192.168.1.0

only_from = localhost

no_access = 192.168.1.15

instances = 60
```
