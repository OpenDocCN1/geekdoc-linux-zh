
仅返回 `/home` 文件系统为共享状态。

> 注意：不应在 NFS 文件系统上启用 root 权限。如果管理员试图通过 NFS 挂载修改文件系统，这可能会很麻烦，但可以避免灾难性的错误。如果 root 用户想要清除主机上的文件系统 `/data`，如果 `/data` 下有一个 root 权限的 NFS 挂载文件系统，则 `rm -rf` 将是灾难性的。如果 `/data/today` 是 `/data` 下的挂载文件系统，则 NFS 服务器上的文件将被擦除。

> 注意：如果对同一个文件系统多次调用 `share` 命令，最后一次 `share` 调用将取代之前的之前的调用。

## 挂载远程文件系统

第 6 章“文件系统简介”介绍了如何使用 `mount` 命令挂载本地文件系统。你将使用 `mount` 命令通过 NFS 在远程主机上挂载共享文件系统。挂载 NFS 文件系统的语法如下：

```
mount -F nfs <options> -o specific_options <server>:<filesystem> <mount_point>
```
