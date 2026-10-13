
添加防火墙规则，以允许 NFS 客户端访问该共享。

在 NFS 客户端上使用的 `mount` 命令与第 15 节中用于挂载本地文件系统的命令相同。此外，`fstab` 文件需要在客户端上包含 NFS 共享的条目，以实现持久挂载。

本节的练习演示了这两个命令的使用以及这两个文件的语法。

## 练习 16-1：在 NFS 服务器上导出共享

此练习应在 `server2` 上以用户 `user1` 身份执行，并在需要时使用 `sudo`。

在本次练习中，你将创建一个目录 `/common`，并以读/写模式将其导出到 `server1`。你将确保防火墙允许 NFS 流量通过。你将确认导出情况。

- 1. 安装名为 `nfs-utils` 的 NFS 软件：

```
[user1@server2 ~] sudo dnf -y install nfs-utils
Package nfs-utils-1:2.3.3-14.el18.x86_64 is already installed.
Dependencies resolved.
Nothing to do.
Complete!
```

- 2. 创建要导出为共享的 `/common` 目录：

```
[user1@server2 ~] sudo mkdir /common
```

- 3. 为 `/common` 赋予全权限：

```
[user1@server2 ~] sudo chmod 755 /common
```

- 4. 将 NFS 服务持久化地添加到防火墙配置中以允许 NFS 流量通过，并加载新规则：

```
[user1@server2 ~]$ sudo firewall-cmd --permanent --add-service nfs
success
[user1@server2 ~]$ sudo firewall-cmd --reload
success
```

![](img/5a7f7913ea400cb401f15585f6d1870b_611_0.png)

有关防火墙的详情请参阅第 20 节。

- 5. 启动 NFS 服务并将其设置为开机自启：

```
[user1@server2 ~] systemctl --now enable nfs-server
Created symlink /etc/systemd/system/multi-user.target.wants/nfs-server.service -> /lib/systemd/system/nfs-server.service.
```

- 6. 验证 NFS 服务的状态：

```
[user1@server2 ~]$ systemctl status nfs-server
* NFS-server.service - NFS server and services
Loaded: loaded (active; Sun 2019-11-10 08:32:21 EST; 26m ago)
Active: active (running) since 2019-11-10 08:32:21 EST; 26m ago
Process: 15800 ExecStart=/usr/bin/systemctl -q is-active nonstop; then
Process: 15786 ExecStartPre=/usr/bin/exports -r (code=exited, status=0/SUCCESS)
Main PID: 15800 (code=exited, status=0/SUCCESS)
```

```
Nov 10 08:32:21 server2.example.com systemd[1]: Starting NFS server and services
Nov 10 08:32:21 server2.example.com systemd[1]: Started NFS server and services.
```

- 7. 用文本编辑器打开 `/etc/exports` 文件，并为 `/common` 添加一个条目，以读/写选项将其导出到 `server1`：

```
/common 192.168.0.110(rw)
```

- 8. 导出 `/etc/exports` 文件中定义的条目。`-a` 选项导出文件中列出的所有条目，`-v` 用于显示详细输出。

```
[user1@server2 ~] sudo exports -av
exporting 192.168.0.110:/common
```

NFS 服务现在已在 `server1` 上设置，`/common` 共享可供 `server1`（在此情况下为 NFS 客户端）挂载。

为了练习，你可以通过执行带有 `-u` 标志的 `exportfs` 命令来取消共享：

```
[user1@server2 ~] sudo exportfs -u 192.168.0.110:/common
```

在继续之前，使用 `sudo exportfs -av` 重新导出共享。

## 练习 16-2：在 NFS 客户端上挂载共享

此练习应在 `server1` 上以用户 `user1` 身份执行，并在需要时使用 `sudo`。

在本次练习中，你将挂载练习 16-1 中导出的 `/common` 共享。你将创建一个名为 `/local` 的挂载点，手动挂载远程共享并确认挂载。

你将远程共享添加到文件系统表中以实现持久化。你将重新挂载共享并确认挂载。你将在挂载点创建一个测试文件，并在 NFS 服务器（`server2`）上确认文件已创建。

- 1. 安装名为 `nfs-utils` 的 NFS 软件：

```
[user1@server2 ~] sudo dnf -y install nfs-utils
Package nfs-utils-1:2.3.34-14.x86_64 is already installed.
Dependencies resolved.
Nothing to do.
Complete!
```

- 2. 创建 `/local` 挂载点：

```
[user1@server1 ~] sudo mkdir /local
```

- 3. 使用 `mount` 命令手动挂载共享：

```
[user1@server1 ~] sudo mount 192.168.0.120:/common /local
```

远程共享已成功挂载到 `server1` 上，可以像其他任何本地文件系统一样访问。

- 4. 使用 `mount` 或 `df` 命令确认挂载：

`mount` 命令的输出返回了 NFS 协议版本（NFS4）以及挂载共享时使用的所有选项：

- 5. 打开 `/etc/fstab` 文件并追加以下条目以实现持久化：

```
192.168.0.120:/common /local nfs _netdev 0 0
```

`_netdev` 选项将使系统在尝试挂载此共享之前等待网络建立。

在尝试向挂载点挂载共享时，挂载点应当为空且不能被占用。

- 6. 使用 `unmount` 命令手动卸载共享，并通过 `fstab` 文件将其移除以进行验证

- 7. 运行 `mount -a`

- 8. 在挂载点中创建一个测试文件

- 9. 在 NFS 服务器（`server2`）上确认文件已创建。

```
master_map_name = auto.master
timeout = 300
negative_timeout = 60
mount_nfs_default_protocol = 4
logging = none
```

此文件中还有其他可用的指令，可以添加更多指令来修改 AutoFS 服务的默认行为。[表 16-1]描述了上述指令。

| 指令 | 描述 |
|---|---|
| master_map_name | 定义主映射（master map）的名称。默认是位于 `/etc` 目录下的 `auto.master`。 |
| timeout | 以秒为单位，指定共享自动卸载后的最大空闲时间。默认为五分钟。 |
| negative_timeout | 以秒为单位指定挂载失败尝试的超时值。默认为一分钟。 |
| mount_nfs_default_protocol | 设置用于挂载共享的默认 NFS 版本。 |
| logging | 配置日志级别。选项有 `none`（无）、`verbose`（详细）和 `debug`（调试）。默认是 `none`（禁用）。 |

## 表 16-1 AutoFS 指令

`autofs.conf` 文件中的指令通常保持默认值，但如有需要可以对其进行修改。

## AutoFS 映射

AutoFS 服务需要知道要挂载的 NFS 共享及其位置。它还需要知道挂载时使用的任何特定选项。这些信息定义在称为 *maps*（映射）的 AutoFS 文件中。有三种常见的 AutoFS 映射类型：*主（master）、直接（direct）和间接（indirect）。*

### 主映射 (The Master Map)
