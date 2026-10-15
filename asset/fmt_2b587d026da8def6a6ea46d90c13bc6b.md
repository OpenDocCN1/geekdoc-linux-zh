
## 控制台配置

```
# LOGDIR=/var/log/consoles
# 我们提供的控制台列表
# name : tty[$host] : baud[parity] : logfile : mark-interval[m|h]
# name : host : port : logfile : mark-interval[m|h]
# name : command : logfile : mark-interval[m|h]

node1:imgels:3001:
node2:imgels:3002:
node3:imgels:3003:
node4:imgels:3004::
```

## SSH 配置

```bash
cat "/.ssh/identity.pub >> "/.ssh/authorized_keys
chmod 600 "/.ssh/authorized_keys"
```

`chmod` 操作非常重要，因为该文件包含敏感信息，除非权限为 `-rw-------`，否则 `ssh` 将不会生效（你可以通过 `ls -l` 进行检查）。

你的密钥对创建已完成。请将这些文件复制到 `/install/post`，它们将在安装时通过以下命令复制到剩余的节点：

```bash
# cd ~/.ssh
# cp -pf identity identity.pub authorized_keys /install/post/.ssh/
```

最后，你为 `xCAT` 准备一些 `ssh` 选项。最简单的配置方法是通过命令从 `/install` 拷贝配置文件：

```bash
# cp /install/post/.ssh/config ~/.ssh/
```

现在 `ssh` 已安装完成，你需要通过以下命令配置其自动启动并立即启动：

```bash
# /etc/rc.d/init.d/sshd start
# /sbin/chkconfig sshd on
```

## 6.5 重启并确保一切运行正常

你现在已经完成了主节点的安装。重启并确保所有服务正常可能是一个好主意。使用命令：

```bash
# shutdown -r now
```

## 计算节点安装

本章描述了第一个计算节点的准备和安装过程，以及剩余计算节点的安装。

我们将介绍到：

- `xCAT` 表格
- 集群服务 (`Cluster Services`)
  - `xntpd`
  - `DNS`
  - `DHCP`
- `MAC` 地址收集
- `ASMA` 设置
- 集群中第一个计算节点的安装
- 集群中剩余节点的安装

### 7.1 填充表格

`xCAT` 几乎完全通过位于 `/usr/local/xcat/etc` 下的若干个表格进行配置。每个表都是纯文本文件，可以使用你喜欢的文本编辑器进行编辑。在这里我们只讨论这些表最常见的用法。完整的参考信息可以参阅第 167 页的附录 B，“xCAT 配置文件”。

在配置 `xCAT` 表之前，请确保你的 `/etc/hosts` 是最新的。许多 `xCAT` 命令都会使用它，并且必须包含网络中所有主机的完整列表。

#### 7.1.1 Site 表 (`site.tab`)

第一张 `xCAT` 表名为 `site.tab`。它包含了集群运行环境的环境信息。示例 7-1 显示了你们实验室使用的 `site` 文件。

**示例 7-1 `site.tab`**

| 字段 | 值 |
| :--- | :--- |
| `rsh` | `/usr/bin/ssh` |
| `rcp` | `/usr/bin/scp` |
| `tftpd` | `/tftpboot` |
| `tftpxatrout` | `xcat` |
| `domain` | `cluster.austin.ibm.com` |
| `nameservers` | `192.168.0.254` |
| `net` | `192.168.0.255.255.0` |
| `gkhfile` | `/usr/local/xcat/etc/gkh` |
| `master` | `master` |
| `pbshome` | `/var/spool/pbs` |
| `pbsprefix` | `/usr/local/pbs` |
| `pbserver` | `mgt1` |
| `scheduler` | `maui` |
| `nisdomain` | `NA` |
| `nismaster` | `NA` |
| `xcatprefix` | `/usr/local/xcat` |
| `timezone` | `US/Central` |
| `offuc` | `-6` |
| `mapperhost` | `nodel` |
| `maxrys` | `10` |
| `clustervlan` | `eth1` |
| `dynamicb` | `172.16` |

大多数字段都是显而易见的，许多字段可以保持默认设置。对于任何你不理解的字段，请务必查阅第 167 页的附录 B，“xCAT 配置文件”进行对比，因为纠正文件中的错误可能会非常耗时。

**注意：**

- `net` 段必须是 `192.168.0.255...` 而不是 `192.168.0.0:255...`
- `dynamic` 段意味着 `B` 类网络

`domain` 段必须与 `/etc/hosts` 中使用的相匹配。如果你只想使用节点短名（short name），你仍必须填写此字段；`cluster` 就是一个选项。

#### 7.1.2 节点列表表 (`nodelist.tab`)

要编辑的第二张 `xCAT` 表是节点列表。它包含了集群中所有节点以及每个节点所属的组。与许多 `xCAT` 表格一样，第一个字段必须是节点的短名。第二个字段仅是节点所属组的逗号分隔列表。示例 7-2 显示了我们实验室使用的 `nodelist` 表。

```
示例 7-2 nodelist.tab
node rack1,rn1,mgmas1,all
node2 rack1,rn2,mgmas1,all
node3 rack1,rn3,mgmas1,all
node4 rack1,rn4,mgmas1,all
```

这些分组仅为了管理方便，可以用任何你认为有用的方式指定。我们选择根据节点所在的机架（对于多机架系统有用）、其物理机架位置以及它们连接的高级系统管理适配器 (`ASMA`) 来对节点进行分组。你记得由于 `xCAT` 的工作机制，可以基于这些组来定义节点。

#### 7.1.3 资源表 (`resources.tab`)

下一步是为节点分配资源。示例 7-3 显示了我们实验室使用的资源表。

**示例 7-3 `resources.tab`**

| 字段 | 值 |
| :--- | :--- |
| `TFTP` | `master` |
| `NFS_INSTALL` | `master` |
| `POST_DIR` | `master` |
| `NIS_SERVER` | `master` |
| `TIME_SERVER` | `master` |
| `SERIAL` | `master` |

#### 7.1.4 节点类型表 (`nodetype.tab`)

现在你在节点类型表中指定你想要安装的节点类型。示例 7-4 显示了该表。

**示例 7-4 `nodetype.tab`**

| 节点 | 类型 |
| :--- | :--- |
| `node1` | `compute62` |
| `node2` | `compute62` |
| `node3` | `compute62` |
| `node4` | `compute62` |

#### 7.1.5 节点硬件管理表 (`nodehm.tab`)

`XCAT` 的核心功能之一是硬件管理。节点硬件管理表提供了 `XCAT` 可用的硬件管理方法。示例 7-5 显示了我们实验室使用的表。

**示例 7-5 `nodehm.tab`**

```
#node power,reset,cad,vitals,inv,cons,bioscons,eventlogs,getmacs
node1 asma,asma,asma,asma,conserver,asma,rcons
node2 asma,asma,asma,asma,conserver,asma,rcons
node3 asma,asma,asma,asma,conserver,asma,rcons
node4 asma,asma,asma,asma,conserver,asma,rcons
```

#### 7.1.6 ASMA 表 (`asma.tab`)

为了利用高级系统管理 (`ASM`) 网络，`xCAT` 需要知道其拓扑结构。这在 `ASMA` 表中配置。示例 7-6 显示了我们实验室使用的 `ASMA` 表。

**示例 7-6 `asma.tab`**

```
node1 mgmas1,node1
node2 mgmas1,node2
node3 mgmas1,node3
node4 mgmas1,node4
```

## 7.2 配置集群服务

一旦配置了 `xCAT`，你就必须配置它执行安装时所依赖的服务。这些大部分服务现在都可以根据你刚刚提供的信息自动设置。

### 7.2.1 xntpd
