
这意味着每个成员的`cron`都是与其他所有成员独立运行的，备份数据目录的`cron`任务将在集群中所有成员的同一时间在相同的文件上运行。显然这不是一个好的安排！

这个问题可以在 HP 最佳实践（Best Practices）中的一个文档中解决：http://www.tru64unix.com/docs/best_practices/cluster_cron.html

关于`rc.config`的更多信息，请参阅第 6 章和第 12 章。

## 21.7 关键服务监控 (`esmd`)

有时集群会因为某个守护进程崩溃而停止正常运行。这个问题可以在 HP 最佳实践中的一个文档中解决：http://www.tru64unix.com/docs/best_practices/cluster_cron.html

`esmd`监控集群服务并确保它们运行。如果服务失败，`esmd`将尝试重启它。更多信息，请参阅第 23 章和第 24 章。

## 21.8 重要文件备份

正如童子军所说，“做好准备。”将某些文件备份到磁带或其他在从安装光盘启动时可以访问：

- `volsave`：可以帮助重建 LSM 配置。
- `sys_check` 的 `escalate.tar`：包含了大量的有用配置。
- `/etc/*`：包含许多系统配置文件且相对较小。
- `/var/cluster/caa/`：CAA 配置和配置。
- `/cluster/admin`：集群日志文件和配置信息。
- 磁盘 CNX 分区的配置数据：保存 `clu_bdmgr.conf` 文件，该文件位于 `/cluster/members/member<ID>/boot/partition/etc` 目录。
- Site 特定 CDSL 的清单：保存 `/var/admin/cdsl_admin.inv` 文件。
- 存储 AdVFS 域的组成：

  ```
  ls -lR /etc/fdmnns > etc_fdmnns_links
  ```
- 存储映射（如果是 SAN 则非常重要，需要图片）：你提供的图片应包括控制器、交换机、存储控制器以及使用了哪些端口及其用途。

`esmd`监控集群服务并确保它们运行。如果服务失败，`esmd`将尝试重启它。更多信息，请参阅第 23 章和第 24 章。

## 保存许可证 PAK

在 Korn shell 中：

```bash
# for i in $( lmf list | awk '/^[A-Z0-9][A-Z0-9].* / { print $1 } )
#do
lmf issue \
/.root/PAKS/$$(i).pak i lmf register - \
/.root/PAKS/$$(i).pak
done
```

## `lmf` 重置

当需要重新注册许可证时。

- 保存磁盘标签

  在 Korn shell 中：

  ```
  # for i in $( hwmgr view devices \
    awk '//disk/ ( print $2 )'\
    cut -d/ -f4 )
  do
    i=${1%c}
  disklabel -r $i $i.lbl
  done
  ```
