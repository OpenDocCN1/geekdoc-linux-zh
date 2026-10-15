
Now the zone is running, and an invocation of `zlogin -C proprietary-zone` will connect to its console. The boot process for a zone is much like that of a physical system, so connecting with `zlogin` before bootstrapping is complete displays output from the boot process. We must perform all the normal configuration for a new system, such as choosing language options and an authentication method.

The remaining task is to create a zone for our web server. Since the web server zone will share the default resource pool with the global zone, it isn't necessary to create a new pool. Instead, we would just create the zone with `zoneconfig` as shown above, but with `set pool=default`.

There is considerably more depth to zones and containers than we've shown here. Advanced features that administrators should be aware of include migration of zones between physical systems (although live migrations are not supported), ZFS resources for smaller whole-root zones, and "branded zones" that support running binaries from other platforms (e.g., Linux) on a Solaris kernel.

## 24.6 AIX WORKLOAD PARTITIONS

IBM has been in the virtualization game a long time. They pioneered the concept in the 1960s, but it wasn't until the release of AIX 6.1 in late 2007 that software virtualization was included in AIX. Any system capable of running AIX 6 supports workload partitions (WPARs). (This technology is distinct from IBM's various logical partition implementations found in versions as early as 4.3.)

WPARs run in an isolated execution environment. Processes can only communicate with peers in the same partition. Signals and events in the global environment do not affect the partition, and vice versa. WPARs can have their own dedicated network addresses.

WPARs are served in two delicious flavors: system and application.

- A system WPAR shares only the AIX kernel with the global environment (the host, essentially). An application running in a system WPAR believes it is running in an independent AIX installation with its own `inetd` daemon for networking autonomy.

- An application WPAR runs a single application in an isolated environment. It shares all filesystems with the global environment and cannot provide remote access capabilities. The application WPAR exits when the application completes.

IBM provides several tools for managing WPARs, continuing the AIX tradition of convenient administration. We discuss the command-line interface here, but administrators should be aware that in typical AIX fashion, there is a full SMIT interface as well as WPAR Manager, a web-based management interface for centralized management of multiple servers and their workload partitions.

你可以使用 `mkwpar` 命令创建一个系统 WPAR。唯一必需的参数是 `-n`，用于指定名称。因此，命令 `mkwpar -n mario` 会创建一个名为“mario”的分区。`mkwpar` 会创建相关的文件系统，安装适当的文件集，并准备子系统和服务。这个过程只需很短时间；完成后，运行 `startwpar mario` 即可启动该 WPAR。

全局环境中的 `/wpars` 目录将包含 `mario` 的文件系统。你可以使用 `lswpar` 从全局环境列出 WPAR：

```
aix$ sudo lswpar
```

| Name | State | Type | Hostname | Directory |
|------|-------|------|----------|-----------|
| mario | A | S | mario | /wpars/mario |

要以 root 身份连接到控制台，请使用 `clogin mario`。还有比这更简单的吗？

这个简单的示例忽略了许多重要的考虑因素和自定义选项。首先，由于 `/usr` 和 `/opt` 文件系统默认以只读方式挂载以节省空间，因此无法在 `mario` WPAR 中安装新软件。也没有可用的网络接口。上述简化流程还忽略了 IBM 出色的资源管理功能，这些功能有助于管理员控制 WPAR 对 CPU、内存、虚拟内存和其他资源的使用。

要创建一个更实用的实例，你可以为 `mkwpar` 命令添加一些额外的参数。下面的版本创建了一个具有以下属性的 WPAR：

- WPAR 的名称为 `mario`（`-n`）。

- 名称解析设置继承自全局实例（`-r`）。

- 创建私有的、可写的 `/opt` 和 `/usr` 文件系统（`-l`）。

- WPAR 在全局 WPAR 的 `en0` 接口上使用 IP 地址 `192.168.10.15`（`-N`）。

- 分配给此 WPAR 的 CPU 最低为 5%，软上限为 15%，绝对限制为 25%（`-R`）。

```
aix$ sudo mkwpar -n mario -r -l -N interface=en3 address=192.168.10.15 netmask=255.255.255.0 broadcast=192.168.10.255 -R active=yes CPU=5%-15%,25%
```

这个调用比基本的 `mkwpar` 稍微复杂一些，并且由于要复制 `/usr` 和 `/opt`，执行时间也更长。

要修改已创建的分区，请使用 `chwpar` 命令。你可以使用 `stopwpar` 停止分区，并使用 `rmwpar` 永久删除它。
