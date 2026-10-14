
这些脚本经过了修改，最终会在底层执行 `svcadm` 命令。`ncd` 守护进程还缓存了切换信息。在某些情况下，你可能想要检查命名服务数据库。你可以使用 `getent` 命令完成操作。

## 使用 getent 命令

你可以使用 `getent` 命令检索命名服务信息，其语法如下：

```
getent <database> [<key>]
```

参数 `<database>` 指定了要检查的命名服务数据库的名称。它可以是以下任意一个：

- `/etc/ethers`. 以太网地址到主机名的映射数据库
- `/etc/group`. 组文件
- `/etc/inet/hosts`. IP 版本 4 主机名的数据库
- `/etc/inet/ip6hosts`. IP 版本 4 和 6 主机名的数据库
- `/etc/netmasks`. 网络掩码数据库
- `/etc/networks`. 网络名称数据库
- `/etc/passwd`. 密码文件
- `/etc/project`. 项目文件
- `/etc/protocols`. 协议名称数据库
- `/etc/services`. 互联网服务和别名数据库

参数 `<key>` 指定了与要搜索数据库相关的键——例如，`passwd` 的用户名或数字 uid。`getent` 命令显示与所提供的每个键匹配的数据库条目，每行一个。
例如，考虑以下命令：

```
getent passwd dang
```
