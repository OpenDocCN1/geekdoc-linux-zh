
## RAID 阵列故障恢复

### 图 6.3：阵列中的降级磁盘

图 6.3 说明了由于磁盘故障导致的 RAID 阵列降级状态。在典型的 RAID 配置中，内置了冗余性；当一个磁盘故障时，阵列进入降级模式。这意味着尽管数据仍然可用，但性能可能会降低，如果另一块磁盘故障，数据全部丢失的风险将会增加。图中显示受影响的磁盘被标记为故障，强调了主动监控和立即更换以恢复完全冗余并防止潜在系统停机的重要性。这一场景强调了 RAID 在数据保护中的关键作用以及定期维护和备份的必要性。

### 第 2 步：标记故障设备

运行命令：`sudo mdadm /dev/md1 --fail /dev/sdc`

### 第 3 步：移除故障设备

运行命令：`sudo mdadm /dev/md1 --remove /dev/sdc`

### 第 4 步：插入新磁盘

- 假设添加了新磁盘 `/dev/sdd`。
- 使用 `fdisk` 对其进行分区并将类型设置为 `fd`。
- 运行 `sudo fdisk /dev/sdd`。
- 创建一个新的主分区并将类型设置为 `fd`。

### 第 5 步：将新磁盘添加到阵列

运行命令：`sudo mdadm /dev/md1 --add /dev/sdd`

### 第 6 步：监控重建过程

运行命令：`watch cat /proc/mdstat`

输出示例：

```text
md1 : active raid1[2] sdb1
1485632 blocks [2/1] [U _]
=>........................... recovery = 12.4% (1308160/10485632) finish=10.3min
```

### 图 6.4：重建之前失败的磁盘 RAID

图 6.4 展示了重建 RAID 阵列之前故障磁盘的过程。当 RAID 配置中的磁盘故障时，特别是在支持冗余的 RAID 级别中（如 RAID 1、5 或 6），该磁盘可以使用剩余驱动器的校验数据或镜像数据进行更换和重建。在图中，一个新的或之前失败但现已修复的磁盘正在被重新引入阵列。系统会自动开始重建过程，重新分配数据和校验位以恢复完全冗余并确保数据完整性。这一步骤对于维持容错能力以及在发生另一个磁盘故障时尽地减少数据丢失风险至关重要。

### 第 7 步：确认重建完成

运行命令：`sudo mdadm --detail /dev/md1`

预期输出：

```text
/dev/md1:

State : clean

Active Devices : 2

Working Devices : 2

Failed Devices : 0

Spare Devices : 0
```

### 图 6.5：具有 Clean 状态的新 RAID 分区

图 6.5 展示了一个新创建且已达到“clean”（正常）状态的 RAID 分区。此状态表示 RAID 阵列已完全同步，没有降级或缺失设备，并已准备就绪。clean 状态是 RAID 健康状况的关键指标，确认了所有成员磁盘运行正常且冗余机制已到位。在此阶段，可以安全地对 RAID 阵列进行格式化和挂载以存储数据，根据配置的 RAID 级别，确保性能和数据保护。

### 最佳实践

- 使用相同的替换磁盘（大小和类型）。
- 使用 `cron` 定期安排 RAID 健康检查：`@daily mdadm detail /dev/md1 | mail -s "RAID Status" admin@example.com`

## 使用 systemd 进行服务管理

systemd 是 Rocky Linux 9 以及许多其他现代 Linux 发行版使用的默认 init 系统和服务管理器。它的核心作用是控制系统的启动方式、管理后台服务（称为守护进程）以及关机。与逐个启动服务的其他 init 系统不同，systemd 使用并行启动，允许多个服务同时启动，从而加快启动过程。它还能理解依赖关系，确保服务按正确的顺序启动。例如，Web 服务器在网络启动之前不会启动。这种智能管理有助于提高可靠性和启动性能。

systemd 使用单元文件（unit files）组织配置，这些文件存储在 `/etc/systemd/system/` 和 `/usr/lib/systemd/`。这些文件定义了服务、设备和其他组件的行为。管理员使用 `systemctl` 命令控制服务——例如，使用 `systemctl start http` 启动 Web 服务器，或使用 `systemctl enable firewall` 确保防火墙在启动时运行。我们还可以使用 `journalctl` 查看日志，它提供了有关系统事件和服务行为的详细信息。systemd 支持自定义单元文件和定时器，允许用户实现任务自动化并根据需求定制系统行为，使其成为管理 Rocky Linux 9 等企业级 Linux 系统的强大灵活工具。

systemd 的核心概念包括：

- Units（单元）：基础构建块，如服务、套、定时器和挂载点。
- Targets（目标）：单元组，如运行级别（runlevels），用于定义状态，如 `multi-user.target` 或 `graphical.target`。
- Journal（日志）：由 `journal` 提供的集中日志记录机制。

## Systemd 命令

systemctl 是一个集中的命令行工具，用于管理实现 systemd init 系统的 Linux 系统（如 Rocky Linux 9）上的服务。它允许管理员以简单且一致的方式启动、停止、启用和禁用服务。例如，要启动 Apache Web 服务器，使用 `systemctl start httpd` 命令，而使用 `systemctl stop httpd` 则停止该服务。当配置更改生效时，可以执行 `systemctl restart httpd` 来在无需重启系统的情况下重新加载服务。

若要配置服务在系统启动时自动运行，使用 `systemctl enable` 命令。相反，`systemctl disable` 则防止服务在启动时运行。这些控制对于确保服务仅在需要时运行至关重要，可以优化系统性能和可靠性。

除了服务管理外，systemctl 还方便了系统级操作。`systemctl reboot` 和 `systemctl poweroff` 命令提供了安全的重启或关机方法。此外，systemd 使用 targets 来组织运行模式，其作用与早期 Linux 发行版中传统的运行级别类似。targets 定义了特定状态，如多用户模式或图形模式。切换这些状态的操作通过 `systemctl list-units --type=target` 完成。

理解并有效使用 systemctl 对于使用 Rocky Linux 的系统管理员至关重要。它提供了强大的工具，用于控制服务、管理系统状态，并在各种计算环境中维持平稳、安全且稳定的运行。

## systemctl 命令及其描述

| 命令 | 描述 |
|---|---|
| `systemctl start <service>` | 启动服务。 |
| `systemctl stop <service>` | 停止服务。 |
| `systemctl restart <service>` | 重启服务。 |
| `systemctl reload <service>` | 在不停止服务的情况下重新加载配置。 |
| `systemctl enable <service>` | 启用服务在启动时自动运行。 |
| `systemctl disable <service>` | 禁用服务在启动时自动运行。 |
| `systemctl status <service>` | 显示服务的当前状态、日志和运行详情。 |
| `systemctl is-enabled <service>` | 检查服务是否已启用。 |
| `systemctl list-units` | 列出所有活动单元。 |
| `systemctl daemon-reload` | 重新加载 systemd 配置。 |

图 6.6 提供了 Rocky Linux 中最常用 systemctl 命令的快速参考。

## 实践示例：管理服务：Apache 服务器

1. 安装 Apache：`sudo dnf install httpd`
2. 启动 Apache：`sudo systemctl start httpd`
3. 设置 Apache 自启：`sudo systemctl enable httpd`
4. 检查 Apache 状态：`sudo systemctl status httpd`

输出：

```text
● httpd.service - The Apache HTTP Server

   Loaded: loaded (/lib/systemd/system/httpd.service; enabled; preset=enabled)

   Active: active (running) Mon 2024-12-23 21:09:55 UTC; 1h ago

   Main PID: 1039

   Status: total: 0/0; Requests/sec: 0; Bytes/sec: 0 B/sec

   Tasks: 17 (limit: 1111)

   Memory: 20M
```
