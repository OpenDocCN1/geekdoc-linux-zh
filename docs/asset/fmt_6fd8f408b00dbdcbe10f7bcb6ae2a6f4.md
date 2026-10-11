
`/opt/app1 -anon=65534`

`/opt/app2 -access=system2`

如果你在 UNIX 系统上添加了要导出的文件系统，你可能需要运行如 `exportfs -a` 之类的程序。虽然我们在本章中将重点介绍导出 UNIX 系统，但我认为没有理由我们不能执行相反的操作。挂载到 UNIX 系统上的 Windows 文件系统，与 UNIX 系统挂载到 Windows 中是类似的。挂载到 UNIX 系统本地的远程文件系统存放在 `/etc/fstab` 中。以下是 `/etc/fstab` 中一个挂载到本地的远程文件的项示例。`system2` 上的远程目录 `/opt/app3` 挂载在本地的 `/opt/app3` 下：

```
system2:/opt/app3 /opt/app3 nfs rw,suid 0
```
