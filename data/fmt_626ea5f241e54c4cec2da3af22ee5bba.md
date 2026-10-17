
`/etc/exports` 包含将要导出（向客户端提供）的资源列表

以下是你在操作 NFS 时将使用的一些其他文件：

- `/var/lib/nfs/stab` 包含当前导出的资源列表
- `/var/lib/nfs/rmtab` 包含远程挂载资源的列表

对于第一个配置步骤，你需要对主配置文件进行一些更改。

### 步骤 1. 打开主配置文件进行编辑：

`# nano /etc/sysconfig/nfs`

### 步骤 2. 取消以下行的注释：

```
MOUNT_NFS_V1="no"
MOUNT_NFS_V2="no"
MOUNT_NFS_V3="no"
```

前三行禁挂载守护进程接受低于版本 4 的请求。最后一行禁用 NFS 服务甚至不发布版本 4。

### 迁移提示

如果你仍然在使用 RHEL5，存在一个未解决的错误，会导致你禁用所有挂载守护进程的发布。对于 RHEL5，我建议只取消以下行的注释：

```
MOUNT_NFS_V1="no"
MOUNT_NFS_V2="no"
```

### 步骤 3. 保存文件并退出。

接下来，让我们处理 `/etc/exports` 文件，因为它定义了哪些资源将对你的客户端可用。如果该文件不存在，你可以创建它。`/etc/exports` 文件的语法为

`<mountpoint> <host><permissions/options>`

> 警告：注意 `<host>` 字段与 `<permissions/options>` 字段之间没有空格。如果你包含了空格，将收到语法错误，且资源将无法正常导出。

### 挂载选项：

| 选项 | 说明 |
| :--- | :--- |
| rw | 设置读写权限 |
| ro | 设置只读权限 |
| insecure | 允许使用 1024 以上的端口 |
| sync | 规定所有更改在命令完成之前必须写入磁盘 |
| no_wdelay | 强制立即写入更改（当发生崩溃时很有用） |
| root_squash | 防止 root 用户 |

例如，你可以使用以下两个位置向客户端导出：

`/home` 包含你用户数据的家目录

`/opt/company_data` 书中之前创建的存放公司数据的目录

### 步骤 4. 在 `/etc/exports` 文件中设置导出，以便网络上的任何客户端可用：

```
# nano /etc/exports
/home               * (ro,sync)
/opt/company_data   * (rw,sync)
```

在这里，你定义了两个将提供的资源。第一行定义了 `/home` 目录允许所有客户端只读。第二行行为所有客户端提供读写的 `/opt/company_data` 目录。完成所有要导出的资源定义后，保存文件。

### 步骤 5. 启动两个 NFS 服务，`rpcbind` 已经在运行：

```
# service nflock start
Starting NFS statd:         [ OK ]

# service nfs start
Starting NFS services:      [ OK ]
Starting NFS quotas:        [ OK ]
Starting NFS daemon:        [ OK ]
Starting NFS mountd:        [ OK ]
```

### 步骤 6. 验证服务已成功启动：

```
# service rpcbind status
rpcbind (pid 2568) is running...

# service nflock status
rpc.statd (pid 1726) is running...

# service nfs status
rpc.cgssd is stopped
rpc.mountd (pid 1780) is running...
nfsd (pid 17777 17776 17775 17773 17772 17771 1770) is running...
rpc.quotad (pid 1764) is running...
```
注意：第一次启动 NFS 服务并不总是产生输出。如果你想验证它们已启动，可以重启服务并在控制台上查看正确输出。如果在创建 `/etc/exports` 文件之前已经启动了服务，可以使用 `exportfs` 命令手动导出 `/etc/exports` 中的新资源。

语法：`exportfs [options]`

选项：

- `-a` 导出所有目录
- `-r` 重新导出所有目录
- `-u` 取消导出一个或多个目录
- `-v` 详细输出

### 步骤 1. 这里是手动导出资源的示例：

```
# exportfs -a
exporting *:/opt/company_data
exporting *:/home
```

### 步骤 2. 或者，你也可以通过仅重启 NFS 服务来实现相同的效果，这会重启所有守护进程：

```
# service nfs restart
Shutting down NFS mountd: [ OK ]
Shutting down NFS daemon: [ OK ]
Shutting down NFS quotas: [ OK ]
Shutting down NFS services: [ OK ]
Starting NFS services: [ OK ]
Starting NFS quotas: [ OK ]
Starting NFS mountd: [ OK ]
```

### 世界提示

手动导出目录比重启服务更好，因为在导出新目录时不会断开客户端连接，而重启服务时会。现在所有资源已正确导出且 NFS 服务已启动，你可以使用 `rpcinfo` 命令验证 NFS 服务的所有部分是否运行正常。

语法：`rpcinfo -p [host]`

你可以使用 `rpcinfo` 命令查看本地和远程信息。由于你在寻找本地服务器的信息，调用命令时不需要指定 `host`。查看当前运行的 NFS 守护进程：

`# rpcinfo -p`

| program | vers | proto | service |
| :--- | :--- | :--- | :--- |
| 100000 | 4 | tcp | portmaster |
| 100000 | 3 | tcp | portmaster |
| 100000 | 2 | tcp | portmaster |
| 100000 | 4 | udp | portmaster |
| 100000 | 3 | udp | portmaster |
| 100000 | 2 | udp | portmaster |
| 100024 | 1 | udp | status |
| 100024 | 1 | tcp | status |
| 100011 | 1 | udp | rquotad |
| 100011 | 2 | udp | rquotad |
| 100011 | 1 | tcp | rquotad |
| 100011 | 2 | tcp | rquotad |
| 100003 | 4 | tcp | nfs |
| 100003 | 4 | udp | nfs |
| 100021 | 1 | udp | nlockmgr |
| 100021 | 3 | udp | nlockmgr |
| 100021 | 4 | udp | nlockmgr |
| 100021 | 1 | tcp | nlockmgr |
| 100021 | 3 | tcp | nlockmgr |
| 100021 | 4 | tcp | nlockmgr |

在你看到 `nfs` 守护进程运行时，注意它只列出了版本 4。这是因为你在配置文件中禁用了所有其他版本。虽然列出的其他守护进程也使用了其他版本，但你应该验证至少 `nfs` 守护进程显示版本 4。

### 防火墙和 SELinux 配置

NFS 是许多 Red Hat 产品之一，可以利用 TCP Wrappers 作为安全防火墙规则。我们在这里不使用 TCP-Wrappers，但如果你在考试中遇到 NFS 服务无法工作的问题，不要忘记检查是否有内容被 TCP Wrappers 过滤。由于你使用的是 NFS 版本 4，你只需要创建一个防火墙规则。

### 步骤 1. 使用 `iptables` 创建额外的防火墙规则：

```
# iptables -I INPUT 5 -p tcp --dport 2049 -j ACCEPT
```

### 步骤 2. 保存你创建的防火墙规则：

```
# service iptables save
saving /etc/config/iptables: [ OK ]
```

### 步骤 3. 重启 `iptables` 服务：
