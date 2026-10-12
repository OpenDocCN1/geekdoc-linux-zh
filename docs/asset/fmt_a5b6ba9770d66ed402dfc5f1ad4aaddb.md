
# 第 22 章 LINUX 共享服务：FTP 和 NFS

## 图 22.10 添加共享 NFS 目录

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_672_0.png)

如图 22.10 所示，我们设置了 `/mnt/inst` 目录的共享，并为 `*.example.com` 域内的计算机设置为只读权限。你可以为 `/mnt/inst` 或 `/tmp` 设置独立的共享，并特定的计算机（如 `big.example.com`）赋予读写权限。

## 图 22.11 常规选项选项卡

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_672_1.png)

选择“常规选项”选项卡，如图 22.11 所示。你可以设置表 22.9 中描述的若干选项。默认情况下，只有“按请求同步写入操作”处于激活。表 22.9 列出了每个选项及其对应的命令。

### 表 22.9：添加 NFS 共享常规选项及对应的 NFS/ETC/EXPORTS 命令

| 选项 | NFS 命令 |
| --- | --- |
| 允许从 1024 及更高端口连接 | `insecure` |
| 允许不安全文件锁定 | `insecure_locks` |
| 禁用子树检查 | `no_subtree_check` |
| 按请求同步写入操作 | `sync` |
| 强制立即同步写入操作 | `no_wdelay` |

## 图 22.12 用户访问选项卡

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_673_0.png)

选择“用户访问”选项卡，如图 22.12 所示。表 22.10 列出了每个选项及其对应的命令。

### 表 22.10：NFS 共享用户访问选项及对应的 NFS/ETC/EXPORTS 命令

| 选项 | NFS 命令 |
|---|---|
| 将远程 root 用户视为本地 root | `no_root_squash` |
| 将所有客户端视为匿名用户 | `all_squash` |
| 为匿名用户指定本地用户 ID；User ID | `anonuid=userid` |
| 为匿名用户指定本地组 ID；Group ID | `anongid=groupid` |

你会注意到，此选项卡上的前两个命令是互斥的；换句话说，如果你已经将所有 NFS 客户端配置为匿名用户，就不能将远程用户视为 root。

“指定本地用户 ID”和“指定本地组 ID”选项没有配置对应的 NFS 命令；它们没有意义，因此除非你设置了特定的用户或组 ID，否则它们不会被激活。有关用户 ID 和组 ID 概念的更多信息，请参阅第 9 章。

生成的 `/etc/exports` 文件与之前有所不同。对于之前指定的计算机和网络，只读设置和读/写设置需要单独的行目。

```
# /mnt/inst *.example.com(ro,sync)
# /mnt/inst *.example.com(rw,sync)
# /tmp *(rw,insecure,sync,no_delay,all_squash,anonid=600)
```
