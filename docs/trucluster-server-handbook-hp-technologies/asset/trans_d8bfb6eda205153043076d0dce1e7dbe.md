

然后创建一个分区文件系统资源。或者你可能有一个应用程序希望使用内存文件系统（MFS）。在 V5.1A 中，MFS 作为分区文件系统得到支持。

什么是分区文件系统资源？它是一个挂载和卸载一个或多个文件系统的应用程序资源。

实现分区文件系统资源相对直接。

- 创建一个应用程序资源。

在创建应用程序资源时，一个需要考虑的潜在实现细节是如第 24.4.1.1 节所示，将文件系统和挂载点放在资源配置文件中。

- 在“start”入口点，挂载文件系统。

```
# mount -o server_only kits@kits /kits
```

- 在“stop”入口点，卸载文件系统。

- 如果在应用程序停止后文件系统上可能仍有打开的文件，你可能需要考虑使用 fuser(8) 命令来处理这种情况。

## 24.6 Cluster Alias Resource

对于大多数应用程序，默认的集群别名应该足够。对于那些需要限制在成员子集上或更改负载均衡行为的应用程序，可以定义备用集群别名。一般来说，管理集群别名与 CAA 无关，除了资源可能会管理使用集群别名的应用程序。

那么我们为什么要有这一节呢？在某些情况下，你可能希望对集群别名的处理有比集群别名子系统单独提供的更精细的控制。例如，如果你想将别名限制为运行应用程序资源的成员，但应用程序没有启动可以设置为 clua_services(4) 文件中 "in_single" 服务的网络守护进程。

例如，你有一个应用程序（我们称之为“widget”），你希望你的用户使用它。widget 运行在 member1 上。用户通过 telnet(1) 连接到 member1 并开始使用 widget。如果 member1 不可用，则应用程序不可用。

如果你实现一个应用程序资源来管理 widget，你将希望将一个集群别名绑定到资源上，这样如果资源被迁移，别名会跟随 widget。

使别名跟随 widget 有几种可能的解决方案：

- 使用 cluamgr(8) 命令。
- 使用 ifconfig(8) 命令。

### 24.6.1 Alias Resource Using `cluamgr`

使用 `cluamgr(8)` 命令将 widget 别名“加入”到 widget 资源动作脚本的“start”入口点。当资源迁移到另一个集群成员时，使用 `cluamgr` 命令在 widget 资源动作脚本的“stop”入口点“离开”widget 别名。

- 保存一份原始 application.tdf 文件的副本。
- 按如下方式向 application.tdf 文件添加一个属性：
  - 如果你想使用别名名称，创建一个“name_string”属性。
  
    ```
    attribute: USR_ALIAS_NAME
    type: name_string
    switch: -o an
    default:
    required: no
    ```
  
  - 如果你想使用别名 IP 地址，创建一个“internet_address”属性。
  
    ```
    attribute: USR_ALIAS_IP
    type: internet_address
    switch: -o aa
    default:
    required: no
    ```
  
  - 如果你需要多个别名，创建一个“name_list”属性。
  
    ```
    attribute: USR_ALIAS_NAMES
    type: name_list
    switch: -o al
    default:
    required: no
    ```
- 在“start”入口点：
  
  ```
  # cluamgr -a alias=$(USR_ALIAS_NAME),join,rpri=1
  ```
  
  ```
  # cluamgr -x start
  ```
- 在“stop”入口点：
  
  ```
  # cluamgr -a alias=$(USR_ALIAS_NAME),leave,rpri=0
  ```

### NOTE:

截至本文撰写时，一旦创建了集群别名，它会一直存在直到集群关闭，无论当前是否有任何集群成员加入该别名。换句话说，即使最后一个集群成员使用 cluamgr 命令“离开”别名，别名仍然存在。最后一个为别名路由的成员将继续响应别名请求。

然而，如果 widget 资源被停止的可能性很小，并且你不希望用户在资源不可用时连接到集群，你可能需要考虑以下章节中的选项。

有关集群别名子系统的更多信息，请参阅第 16 章。

### 24.6.2 Alias Resource Using ifconfig

使用 ifconfig(8) 命令的 "alias" 选项。

此选项不使用集群别名子系统，尽管它允许你向网络接口添加别名。

使用 ifconfig 命令的 "alias" 选项有一些限制：

- 1. 定义别名时必须使用 IP 地址而不是别名名称。
- 2. 每个接口只能有一个别名。

为了使用 ifconfig 实现别名：

- 保存一份原始 application.tdf 文件的副本。
- 如第 24.6.1 节所示，将 USR_ALIAS_IP 属性添加到 application.tdf 文件中。
- 创建一个“name_string”属性（命名为 USR_ALIAS_INTERFACE）并按如下方式将其添加到 application.tdf 文件中：

```
#!===========================
attribute: USR_ALIAS_INTERFACE
type: name_string
switch: -o ai
default:
required: no
```

在“start”入口点：

```
# ifconfig ${USR_ALIAS_INTERFACE} alias ${USR_ALIAS_IP}
```

在“stop”入口点：

```
# ifconfig ${USR_ALIAS_INTERFACE} -alias ${USR_ALIAS_IP} abort
```

