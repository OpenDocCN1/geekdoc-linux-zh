
| `security group list` | 列出已创建的现有安全组。 |

| `security group delete` | 删除现有的安全组。 |

| `security group show` | 显示指定安全组的所有信息，包括分配的规则。 |

| `security group set` | 设置安全组的不同参数，例如名称或描述。 |

| `security group rule delete` | 从安全组中删除现有的安全组规则。 |

表 16.9：与安全组相关的典型任务

### 公钥

为了访问虚拟机，必须使用 SSH 密钥认证方法。为 Linux 发行版提供的云映像没有默认密码。OpenStack 允许上传公钥以注入虚拟机，从而允许远程访问。请参阅图 16.18：

```bash
[stack@client ~]$ openstack keypair create --public-key ~/.ssh/id_rsa.pub mykey
+------------+------------------------------------------------------+
| Field | Value                                      |
+------------+------------------------------------------------------+
| fingerprint | f1:1a:36:55:5c:7f:38:5f:ef:2b:5d:85:61:1b:d8:e6 |
| name | mykey                                      |
| user_id | 6c1f154be7c14eb3b137e73910fad113           |
+------------+------------------------------------------------------+
```

### 虚拟机

在拥有可用的网络、已定义的 `规格` 以及包含所需操作系统的 `镜像` 后，即可运行 `虚拟机`。该计算服务被称为 `nova`。安全组可以是项目中的 `默认` 组，也可以是集群中创建的自定义组。可选地，可以指定要使用的公钥。使用参数 `server create` 进行创建。`图 16.19` 展示了创建过程的示例：

```
[stack@Client ~]$ openstack server create myfirstvm --network overlay_network \
> --flavor m1.small --image debian10 \
> --key-name mykey --security-group allowssh --wait
```

![](img/863afa537de4eed7deb11978bfbfa90e_577_1.png)

使用选项 `--wait`，该命令将创建 `虚拟机`，或者显示创建失败的原因。输出包括分配的 `IP 地址` 以及其他有用信息。`表 16.10` 展示了上述命令的输出示例：

| 字段 | 值 |

| :--- | :--- |

| `OS-DCF:diskConfig` | `MANUAL` |

| `OS-EXT-SRV-ATTR:instance_name` | `instance-00000004` |

| `OS-EXT-STS:power_state` | `Running` |

| `OS-EXT-STS:task_state` | `None` |

| `OS-EXT-STS:vm_state` | `active` |

| `OS-SRV-USD:launched_at` | `2022-12-05T18:49:38.000000` |

| `addresses` | `overlay_network=172.16.0.64` |

| `adminPass` | `f8P3jTtgBffZ` |

| `config_drive` | |

| `created` | `2022-12-05T18:49:21Z` |

| `flavor` | `m1.small` |

| `hostId` | `ce58aff5b3d82cc6e61b(..)` |

| `id` | `ab12fad7-5dca-(..)` |

| `image` | `debian10 (..)` |

| `key_name` | `mykey` |

| `name` | `myfirstvm` |

| `security_groups` | `name='allowssh'` |

| `status` | `ACTIVE` |

| `updated` | `2022-12-05T18:49:38Z` |

| `user_id` | `6c1f154be7c14eb3b137e73910fad113` |

| `volumes_attached` | |

表 16.10：创建服务器时的输出字段示例

可以通过参数 `server list` 查看正在运行的虚拟机，如 `图 16.20` 所示：

```bash
[stack@client ~]$ openstack server list -c Name -c Status -c Networks -c Image
+-------+--------+--------------------------+---------+
| Name  | Status | Networks                 | Image   |
+-------+--------+--------------------------+---------+
| myfirstvm | ACTIVE | overlay_network=172.16.0.64 | debian10 |
+-------+--------+--------------------------+---------+
```

图 16.20：列出虚拟机示例

表 16.11 展示了与安全组相关的常见任务。

| 参数 | 描述 |

| :--- | :--- |

| `server delete` | 删除现有的虚拟机。 |

| `server show` | 显示指定虚拟机的所有信息。 |

| `server set` | 设置虚拟机的不同参数，例如名称或描述。 |

| `server console log show` | 显示虚拟机在启动过程期间相关的日志。 |

| `server stop` | 停止虚拟机。 |

| `server reboot` | 重启虚拟机。 |

表 16.11：与虚拟机相关的常见任务

### 浮动 IP

连接到 Overlay 网络的虚拟机无法从集群外部访问。为了获得与外部世界的连接，需要在外部网络中创建浮动 IP 并将其附加到虚拟机。使用参数 `floating ip create` 创建一个新的浮动 IP，以便稍后在 `虚拟机` 上使用。使用参数 `server add floating ip` 将该 `IP` 附加到 `虚拟机`。`图 16.21` 展示了该过程：

```
[stack@client ~]$ openstack floating ip create external -c floating_ip_address
+-------------+-----------------+
| Field       | Value           |
+-------------+-----------------+
| floating_ip_address | 10.0.0.225 |
+-------------+-----------------+
[stack@client ~]$ openstack server add floating ip myfirstvm 10.0.0.225
[stack@client ~]$ openstack server list -c Name -c Status -c Networks
+-------------+--------+-------------------------------------------------
| Name        | Status | Networks                                          |
+-------------+--------+-------------------------------------------------
| myfirstvm   | ACTIVE | overlay_network=172.16.0.64, 10.0.0.225 |
+-------------+--------+-------------------------------------------------
```

`图 16.21`：`创建和分配浮动 IP`

现在，可以使用从外部网络分配的 `IP 地址` 访问该 `虚拟机`。`图 16.22` 展示了使用默认用户名 `debian` 和正确的 SSH 密钥进行连接的过程。
