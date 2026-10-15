
你可以使用 `timesync` RHEL 系统角色在多个目标机器上管理时间同步。

`timesync` 角色会安装并配置 NTP 或 PTP 实现，作为 NTP 客户端或 PTP 副本运行，以便系统时与 NTP 服务器或 PTP 域中的主时（grandmasters）同步。

注意，使用 `timesync` 角色还便于迁移到 `chronology`，因为你可以在从 RHEL 6 开始的所有 Red Hat Enterprise Linux 版本上使用相同的 playbook，无论系统是使用 `ntp` 还是 `chronology` 来实现 NTP 协议。

## 14.2. 为单个服务器池应用 TIMESYNC 系统角色

以下示例展示了如何在仅有一个服务器池的情况下应用 `timesync` 角色。

> 警告：
>
> `timesync` 角色将替换被管理主机上给定的或检测到的提供服务的配置。之前的设置将丢失，即使它们没有在角色变量中指定。只有在未定义 `timesync_ntp_provider` 变量的情况下，才会保留对提供者的选择。

### 前提条件

- 你在想要运行 playbook 的系统上安装了 Red Hat Ansible Engine。
- 你在想要部署存储解决方案的系统上安装了 Red Hat Ansible Automation Platform。
- 你在想要运行 playbook 的系统上安装了 `rhel-system-roles` 软件包。
- 你有一个清单文件，详细列出了你想要配置 `timesync` 的系统。

### 步骤

- 1. 创建一个新的 `playbook.yml` 文件，内容如下：

```yaml
- hosts: timesync
vars:
  timesync_ntp_servers:
    - hostname: pool.ntp.org
      pool: yes
      iburst: yes
roles:
  - rhel-system-roles.timesync
```

- 2. 验证 playbook 语法：

```bash
#### ansible-playbook --syntax-check playbook.yml
```

- 3. 在你的清单文件上运行 playbook：

```bash
# ansible-playbook -i inventory.file/path/to/file/playbook.yml
```

## 14.3. TIMESYNC 系统变量

你可以向 `timesync` 角色传递变量 `timesync_ntp_servers`:

| 角色设置 | 描述 |
|--- |--- |
| hostname | 服务器的主名或地址 |
| minpoll | 最小轮询间隔。默认：6 |
| maxpoll | 最大轮询间隔。默认：10 |
| iburst | 快速同步标志。默认：no |
| pool | 表示该地址为独立服务器的标志。默认：no |

其他资源

- 如需 `timesync` 变量的详细参考，请安装 `rhel-system-roles` 软件包，并查看 `/usr/share/doc/rhel-system-roles/timesync` 目录下的 `README.md` 或 `README.html` 文件。

## 第 15 章 使用 RHEL 系统角色监控性能

作为系统管理员，你可以使用 `metrics` RHEL 系统角色来监控系统性能。

## 15.1. METRICS 系统角色简介

RHEL System Roles 是 Ansible 角色和模块的集合，提供了远程管理多个系统的统一接口。`metrics` 系统角色为本地系统配置性能分析服务，并可选包含本地系统监控的远程系统列表。`metrics` 角色允许你使用 `pcp` 监控性能，而无需单独配置 `pcp`，因为 `pcp` 的设置和部署由 playbook 处理。

表 15. Metrics 角色变量

| 角色变量 | 描述 | 使用示例 |
|---|---|---|
| metrics_monitored_hosts | 由目标主机分析的远程主机列表。这些主机将在目标主机上记录指标，请确保每个主机 `/var/log` 下有足够的磁盘空间。 | `_monitored_hosts: ["webserver.example.com","database.example.com"]` |
| metrics_retention_days | 配置性能数据删除前的保留天数。 | `metrics_retention_days: 14` |
| metrics_graph_service | 开启通过 `pcp` 和 `grafana` 进行性能数据可视化的布尔标志。默认为 false。 | `metrics_graph_service: false` |
| metrics_query_service | 开启通过 `redis` 记录指标的时间序列查询服务的布尔标志。默认为 false。 | `metrics_query_service: false` |
| metrics_provider | 指定使用的指标采集器。目前 `pcp` 是唯一支持的指标提供者。 | `metrics_provider: "pcp"` |

> 注意：
>
> 有关 `metrics_connections` 中使用的参数以及关于 `metrics` 系统角色的更多信息，请参 `/usr/share/ansible/roles/rhel-system-roles.metrics/README.md` 文件。

## 15.2. 使用指标系统角色通过可视化监控您的本地系统

本过程描述了如何使用指标系统角色（metrics System Role）监控您的本地系统，同时通过 `grafana` 提供数据可视化。

前提条件

- 您在想要监控的机器上安装了 Red Hat Ansible Engine。
- 您在想要监控的机器上安装了 `rhel-system-roles` 软件包。

步骤

- 1. 通过在 `/etc/ansible/hosts` Ansible 清单中添加以下内容来配置 localhost：

```yaml
localhost ansible_connection=local
```

- 2. 创建包含以下内容的 Ansible 剧本（playbook）：

```yaml
---
- hosts: localhost
vars:
  metrics_graph_service: yes
roles:
  - rhel-system-roles.metrics
```

- 3. 运行 Ansible 剧本：

```bash
# ansible-playbook name_of_your_playbook.yml
```

> 注意
>
> 由于 `metrics_graph_service` 布值设置为 "yes"，`grafana` 会自动安装并配置 `pcp` 作为数据源进行配置。

![](img/7076193df8761a1565038e17afc88b0b_93_0.png)

- 4. 要查看机器上收集的指标的可视化结果，请按照“访问 Grafana web UI”所述的方法访问 `grafana` 界面。

## 15.3. 使用指标系统角色设置一组独立系统进行监控

本过程描述了如何使用指标系统角色设置一组机器以便其进行监控。

前提条件

- 您在用于运行剧本的机器上安装了 Red Hat Ansible Engine。
- 您在用于运行剧本的机器上安装了 `rhel-system-roles` 软件包。

步骤

- 1. 通过剧本将您想要监控的机器的名称或 IP 添加到 `/etc/ansible/hosts` Ansible 清单文件中，并置于方括号括的标识组名下：

```ini
[remotes]
webserver.example.com
database.example.com
```

- 2. 创建包含以下内容的 Ansible 剧本：

```yaml
-
hosts: remotes
vars:
  metrics_retention_days: 0
roles:
  - rhel-system-roles.metrics
```

- 3. 运行 Ansible 剧本：

```bash
# ansible-playbook name_of_your_playbook.yml
```

## 15.4. 通过本地机器使用指标系统角色集中监控机器机器

本过程描述了如何使用指标系统角色设置您的本地机器，以集中监控一组机器，同时通过 `grafana` 提供数据可视化并通过 `redis` 进行数据查询。

前提条件

- 您在用于运行剧本的机器上安装了 Red Hat Ansible Engine。
- 您在用于运行剧本的机器上安装了 `rhel-system-roles` 软件包。

步骤

- 1. 创建包含以下内容的 Ansible 剧本：
