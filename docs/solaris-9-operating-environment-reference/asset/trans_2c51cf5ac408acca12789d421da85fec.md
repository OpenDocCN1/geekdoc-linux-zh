

# nis+, NIS+, nis 935

此映射可以表示为具有以下语法的替换函数。
principal.domain ->[cname=principal.domain],cred.org_dir.domain

此替换名称是一个 NIS+ 名称，可以提交 nis_list(3NSL) 用于关系表示。NIS+ 实体名称通过 nisadded(1) 命令进行管理。

cred 表包含五个名称：cname、auth_name、auth_type、public_data 和 private_data。该表为每个映射到 NIS+ 实体的身份包含一条记录。当前服务支持三种类型的映射。

- 将给定进程的 UID 映射到与该 UID 关联的 NIS+ 实体名称。如果不存在映射，则返回名称 nbody。当进程的有效 UID 为 0（例如超级用户）时，返回带有主机主机名的 NIS+ 名称。请注意，UID 取决于运行执行该进程的机器的上下文。

- 在 Secure RPC 名称与 NIS+ 实体名称之间进行双向映射。有关关于网名（netnames）的更多信息，请参阅 secure_rpc(3NSL)。注意，网名包含域的概念，它们跨越 NIS+ 目录。

- 为扩展 Diffie-Hellman 密钥映射网名和实体名称，例如 DH640-0、DH024-0。更多信息请参阅 nisautoconconf(1M)。

NIS+ 客户端库函数 nis_local(3NSL) 使用 cred.org_dir 表将身份与 UID 的 UNIX 并集映射到 NIS+ 实体名称。Shell 程序可以使用 nisdefault(1) 程序配合 -option 参数返回此类信息。

将 UID 映射到 NIS+ 实体名称是通过构建如下查询完成的：
[auth_type=LOCAL, auth_name=uid],cred.org_dir.defaultdomain.

此查询返回包含在机器默认域中与 UID 关联的 NIS+ 实体名称的记录。

NIS 服务使用数据加密标准 (DES) 映射将 Secure RPC 请求关联的名称映射到 NIS+ 实体名称。Secure RPC 请求在 RPC 头中包含发起请求的客户端的网名。该网名具有以下格式：

uid.domain

服务使用该名称构造如下格式的查询，其中域是从网名中提取的，而不是默认域。
[auth_type=DES, auth_name=hostname],cred.org_dir.domain.

此查询在网名创建的域中查找该网名到 NIS+ 实体名称的映射。
将 UID 和网名映射到 NIS+ 实体名称的机制确保 NIS+ 服务客户端只有一个实体名称。该实体名称是此类授权的基础。NIS+ 命名空间中的所有对象和 NIS+ 表中的所有条目必须指定所有者。owner 字段始终包含 NIS+ 实体名称。

# 组名称

与 NIS+ 实体名称一样，NIS+ 组名称采用以下格式。
group_name.domain

NIS+ 命名空间中的所有对象和 NIS+ 表中的所有条目都可以可选指定组所有者。此组所有者字段

NIS+ 客户端库定义了与 NIS+ 组的整体接口 (nis_groups(3NSL))。这些接口内部将 NIS+ 组名映射为 NIS+ 简单名称，用于识别与该组名关联的 NIS+ 组对象。映射关系所示：

```
group.domain -> group.groups_dir.domain
```

此映射消除了 NIS+ 组名与 NIS+ 目录名之间的冲突。例如，如果没有映射，一个名为 engineering.foo.com 的目录将无法实现，因为 NIS+ 命名空间内的限制是一个名称必须唯一地标识一个对象。有了此映射，NIS+ 组 engineering.groups_dir.foo.com 映射到 NIS+ 对象名

组所有者的内容是 NIS+ 实体名称列表和其他 NIS+ 组的名称。关于其用法的更完整描述，请参阅 nis_groups(3NSL)。

# NIS 安全

NIS 定义了一个安全模型来控制对服务管理的信息的访问。服务定义了访问权限，并选择性地授予单个客户端或客户端组。实体名称和组名称定义了可能被授予或拒绝访问 NIS+ 的客户端和客户端组。这些实体和组与下文定义的 NIS+ 域相关。
安全模型还使用了一种名为 nobody 的实体类概念，它包含了所有客户端，无论它们是否对服务进行了身份验证。该类包括任何已通过验证的客户端。

# 目录与域

NIS+ 命名空间中的某些目录被称为 NIS+ 域。域是指包含 groups_dir 和 org_dir 子目录的 NIS+ 目录。此外，子实体 org_dir 应该包含名为 cred 的表。NIS+ 组名称和 NIS+ 实体名称始终在第一个标签之后包含 NIS+ 域名

# 身份验证

NIS+ 名称服务使用 Secure RPC 来确保 NIS+ 完整性。Secure RPC 要求服务用户及其机器具有关联的 Secure RPC 密钥对。此密钥最初通过 isaddcred(1M) 或 niscient(1M) 命令生成，并通过 chkey(1) 或 nispasswd(1M) 命令修改。

使用 Secure 允许将不可信用户或网络用户无法获取的私有信息存储在名称服务中。

# nis+, NIS+, nis 937

除了 Secure RPC 密钥外，用户还需要其 UID 到 NIS 实体名称的映射。此映射由系统管理员使用 nisclient(1M) 和 nisaddcred(1M) 命令创建。

在多个 NIS+ 域中使用机器的用户必须确保他们在这些域中的每个域都有一个本地凭据条目。该凭据应使用用户在其“主”域中的 NIS+ 实体名称创建。对于 NIS+ 和 Secure RPC 而言，主域被定义为用户 Secure RPC 密钥对所在的地方。

尽管 Diffie-Hellman 密钥使用 Secure RPC 的替代方案，但管理仍通过相同的命令进行。请参阅 nisauthconf(1M)。

# 授权

NIS+ 服务定义了四种可以授予或拒绝客户端的访问权限。这些权限是：

- 读取 (Read)
- 修改 (Modify)
- 创建 (Create)
- 销毁 (Destroy)

这些访问权限在创建时的对象结构中指定，之后可以使用 nischmod(1) 命令修改。通常情况下，授予对象的权限仅适用于该对象。然而，出于授权目的，授予读取目录和表对象的客户端的权限也会授予这些父对象所“包含”的所有对象的客户端。这种包含的概念是抽象的。对象本身并没有在内部包含其他对象。注意，组对象在其定义中包含了实体列表。

访问权限的解释如下：

- read: 授予对象读取权限。对于目录和表对象，对父对象具有读取权限意味着对目录的所有直接子对象或表中的所有条目具有访问权限。

- modify: 授予现有对象修改权限。修改操作不需要读取权限。但在许多应用程序中，需要在修改对象之前先读取它。如果没有同时授予读取权限，此类修改操作将失败。

- create: 授予客户端在之前不存在的地方创建新对象的权限。create 只与目录和表对象结合使用。拥有表的权限允许客户端向表中添加额外的条目。拥有目录的权限允许客户端向 NIS+ 目录中添加新对象。

- destroy: 授予客户端销毁或移除现有对象或条目的权限。当客户端尝试通过移除条目或目录时，服务首先检查包含该对象的表或目录是否授予了客户端销毁权限。如果是，则继续操作；如果包含对象未授予此权限，则会检查对象本身是否授予了客户端此权限。如果对象授予了权限，则操作继续；否则，请求被拒绝。

