
还有许多其他选项，但这些是你想要测试的。你应该建立两个系统以便测试这些特性。

- a) 测试 `insecure` 选项。当你尝试进行 NFS 挂载时发生了什么？使用 `touch` 命令创建文件的结果如何？
- b) 测试 `unix-rpc` 选项。当你尝试进行 NFS 挂载时发生了什么？使用 `touch` 命令创建文件的结果如何？
- c) 测试 `root_squash` 选项。当你尝试进行 NFS 挂载时发生了什么？使用 `touch` 命令创建文件的结果如何？
- d) 测试 `no-root-squash` 选项。当你尝试进行 NFS 挂载时发生了什么？使用 `touch` 命令创建文件的结果如何？
- e) 测试 `ro` 选项。当你尝试进行 NFS 挂载时发生了什么？使用 `touch` 命令创建文件的结果如何？
- f) 测试 `rw` 选项。当你尝试进行 NFS 挂载时发生了什么？使用 `touch` 命令创建文件的结果如何？

## 2)
当你在本地系统上对远程系统进行挂载时，可以为 `mount` 命令提供多个选项。`mount` 命令的显示格式如下所示：

```
mount various_options system_name:directory_name

local_mount_point
```

这就是你在本章中使用的命令格式。

你已经使用过 `nfs` 作为一个选项。一些可以测试的选项包括：

```
hard

soft

time=n, 其中 n 是秒的分之一
```
