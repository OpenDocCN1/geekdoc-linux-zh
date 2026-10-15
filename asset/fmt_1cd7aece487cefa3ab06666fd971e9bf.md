
如果应用程序资源正在运行的集群成员发生故障，该资源将自动迁移到可用的集群成员。但是，有时您可能希望手动迁移该资源。应用程序资源可以迁移到另一个成员（包括非优先成员）。这可以通过使用 `caa_relocate` 命令来实现。

```
# caa_relocate memberUP
Attempting to stop 'memberUP' on member 'sheridan'
Stop of 'memberUP' on member 'sheridan' succeeded.
Attempting to start 'nicUP' on member 'molari'
Start of 'nicUP' on member 'molari' succeeded.
Attempting to start 'memberUP' on member 'molari'
Start of 'memberUP' on member 'molari' succeeded.
```

请注意，只有应用程序资源可以被迁移。

如果要将应用程序资源重新定位到特定成员，可以使用 `-c` 选项（未显示输出）。

```
# caa_relocate -c sheridan memberUP
```

可以在重新定位资源时修改用户定义的资源属性。

```
# caa_relocate USR_ATLAS_IP=192.168.0.74 atlasAPP
```

有关用户定义资源属性的更多信息，请参阅第 23.5.3.3 节。

如果应用程序资源的 `PLACEMENT` 设置为 `restricted`，并且没有其他可用的 `HOSTING_MEMBER`，则会看到以下错误：

```
# caa_relocate memberUP
molari : Resource memberUP (application) cannot run on molari
Resource memberUP has placement error.
```

资源将继续在当前所在的成员上运行。

关于重新定位的最后说明：你可以使用 `-s` 选项将该成员上当前运行的所有资源重新定位到另一个成员。

```
# caa_relocate -s molari
Attempting to stop 'memberUP' on member 'molari'
Stop of 'memberUP' on member 'molari' succeeded.
Attempting to start 'memberUP' on member 'sheridan'
Start of 'NICUP' on member 'sheridan' succeeded.
Attempting to start 'memberUP' on member 'sheridan'
Start of 'memberUP' on member 'sheridan' succeeded.
Attempting to stop 'cluster_lockd' on member 'molari'
Stop of 'cluster_lockd' on member 'molari' succeeded.
Attempting to start 'cluster_lockd' on member 'sheridan'
Start of 'cluster_lockd' on member 'sheridan' succeeded.
```

`注意`，`PLACEMENT` 为 `restricted` 的资源只有在 `HOSTING_MEMBER` 属性中存在另一个可用成员时才会被重新定位。此外，资源的 `REQUIRED_RESOURCES` 必须在目标成员上可用，重新定位才能成功。

有关资源重新定位的更多信息，请参阅 `caa_relocate(8)` 参考页。

## 23.4.17 负载均衡资源

基于特定集群成员的负载对应用程序资源进行放置，可以使用表 23-12 中所示的方法之一来实现。

### 应用程序资源放置和负载均衡

| 方法 | V5.1B | V5.1A | V5.1 | V5.0A |
|---|---|---|---|---|

| 命令 | `caa_start` | 集群管理员运行 `caa_start` 命令，资源会根据其 `PLACEMENT` 在可选 (`OPTIONAL_RESOURCES`) 和/或必需 (`REQUIRED_RESOURCES`) 依赖关系修改后进行最优放置。 | ✓ | ✓ | ✓ | ✓ |

| 命令 | `caa_relocate` | 集群管理员运行 `caa_relocate` 命令，资源会根据其 `PLACEMENT` 在可选 (`OPTIONAL_RESOURCES`) 和/或必需 (`REQUIRED_RESOURCES`) 依赖关系修改后进行最优放置。 | ✓ | ✓ | ✓ | ✓ |

| 命令 | `caa_balance` | 集群管理员运行 `caa_balance` 命令，资源管理器会重新评估资源的放置情况。负载均衡可以针对列出的应用程序资源集、列出的成员上的应用程序资源或集群中的所有应用程序资源进行重新评估。 | ✓ | x | x | x |

| 集群 | 形成 | 当集群形成时，所有 `TARGET` 状态为 `ONLINE` 的资源，或 `TARGET` 状态为 `OFFLINE` 且 `AUTO_START` 设置为 1 的资源将被启动并根据其 `PLACEMENT` 在可选 (`OPTIONAL_RESOURCES`) 和/或必需 (`REQUIRED_RESOURCES`) 依赖关系修改后进行最优放置。 | ✓ | ✓ | ✓ | ✓ |

| 集群 | 成员加入 | 当成员加入集群时，任何 `ACTIVE_PLACEMENT` 值为 1 的资源都将根据其 `PLACEMENT` 在可选 (`OPTIONAL_RESOURCES`) 和/或必需 (`REQUIRED_RESOURCES`) 依赖关系修改后进行重新评估并可能被重新定位。请注意，`AUTO_START` 也会被评估（参见形成） | ✓ | ✓ | ✓ | ✓ |

| 集群 | 成员离开 | 当成员离开集群时，任何在该成员上运行的资源都将根据资源的 `PLACEMENT` 在可选 (`OPTIONAL_RESOURCES`) 和/或必需 (`REQUIRED_RESOURCES`) 依赖关系修改后在另一个成员上进行最优放置。这可能导致资源不被重新定位到另一个成员，而是被停止。 | ✓ | ✓ | ✓ | ✓ |

| 时间 | 如果设置了 `REBALANCE` 属性，则应用程序资源的放置将在该属性设置的时间进行重新评估以实现最优放置。 | ✓ | x | x | x |

### 23.4.17.1 命令触发

有三个命令可使 CAA 评估应用程序资源的放置和平衡：

- `caa_balance` 命令。
- `caa_start` 命令（参见第 23.4.14 节）。
- `caa_relocate` 命令（参见第 23.4.16 节）。

从 V5.1B 开始，可以随时使用 `caa_balance` 命令重新评估集群中应用程序资源的放置。

- 重新评估集群中的所有应用程序资源。

```
# caa_balance -all
Attempting to stop `cluster_lockd` on member `alph11`
Stop of `cluster_lockd` on member `alph11` succeeded.
Attempting to start `cluster_lockd` on member `alph12`
Start of `cluster_lockd` on member `alph12` succeeded.
Resource clustercron is already well placed
Resource memberUP is already well placed
clustercron is placed optimally. No relocation is needed.
memberUP is placed optimally. No relocation is needed.
powerUP is placed optimally. No relocation is needed.
```

- 重新评估特定集群成员上的资源。
