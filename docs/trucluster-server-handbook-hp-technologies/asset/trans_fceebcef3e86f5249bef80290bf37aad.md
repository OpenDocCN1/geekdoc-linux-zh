

evmwatch:
    -i  -  此选项返回所有已加载的事件模板。

我们将输出通过管道传输到 evmsort(8) 命令，以便首先按 cluster_event 然后按名称对事件进行排序。

evmsort:

+   -A  -  此选项调用 evmshow 命令以生成已排序事件的格式化输出。
+   -s  -  此选项是排序规范。在此例中，我们按 cluster_name 的反字母顺序排序，然后按名称的字母顺序排序。
+   -t  -  此选项用于定义“显示模板”，其设置为以五字符（%5）字段显示 cluster_event，然后是一个空格、一个连字符、一个空格以及事件名称。

截至本文撰写时，已定义了 338 个事件，其中 142 个事件为集群范围事件。

```
# evmwatch -A -i -t @cluster_event | wc -l
338
```

```
# evmwatch -A -i -t @cluster_event | grep True | wc -l
142
```

## 12.4.2 如何从成员检索事件？

您可以使用 evmget(8)、evmshow(8) 和 evmwatch 命令以及 "-f [host = hostname]" 选项按成员的主机名过滤事件。

```
> evmget -f "[host molar] AND [age < 1d]" | \
> evmshow -t - @host_name -T "W"
00:00:52 - molari.tcrhb.com: sys.unix.hw.net.niff.alert
00:00:57 - molari.tcrhb.com: sys.unix.hw.net.niff.alert
00:02:57 - molari.tcrhb.com: sys.unix.hw.net.niff.alert
00:03:02 - molari.tcrhb.com: sys.unix.hw.net.niff.alert
00:08:02 - molari.tcrhb.com: sys.unix.hw.net.niff.alert
00:08:07 - molari.tcrhb.com: sys.unix.hw.net.niff.alert
00:09:07 - molari.tcrhb.com: sys.unix.hw.net.niff.alert
00:09:12 - molari.tcrhb.com: sys.unix.hw.net.niff.alert
03:03:12 - molari.tcrhb.com: sys.unix.fs.advsf.sfet.umount
03:03:12 - molari.tcrhb.com: sys.unix.clu.cfa.advsf.not_served
04:10:32 - molari.tcrhb.com: sys.unix.hw.net.niff.alert
04:10:37 - molari.tcrhb.com: sys.unix.hw.net.niff.alert
```

## 12.4.3 EVM 事件过滤器和模板回顾

当安装 *TruCluster Server* 时，会向系统添加额外的事件模板，这些模板特定于 *TruCluster Server*。如果您查看 `/usr/share/evm/templates` 目录，您会发现一个新的 clu 子目录。此外，新的集群过滤器文件也包含在 `/usr/share/evm/filters` 目录中。图 12-3 显示了添加的事件过滤器和模板文件及其位置。

### 12.4.3.1 EVM 事件回顾

在独立系统上，有两个集群事件。

```
## evmwatch -i -f $sys:clu | evmshow -A -a @name -t @name
sys.unix.clu.versw
sys.unix.clu.versw.msg.success
```

在集群上 however，有四十七个集群事件。

![](img/a0df85c2e542a8d6c913113908553aa4_318_0.png)

**Figure 12-3: EVM Additions in a Cluster**

```
# evmwatch -l -f @sys:clu | evmsort -A -s @name -t @name
sys.unix.clu.caa.action_script
sys.unix.clu.caa.app.error
sys.unix.clu.caa.app.modified
sys.unix.clu.caa.app.registered
sys.unix.clu.caa.app.running
sys.unix.clu.caa.app.stopped
sys.unix.clu.caa.app.transition
sys.unix.clu.caa.app.unregistered
sys.unix.clu.caa.cli
sys.unix.clu.caa.err
sys.unix.clu.caa.res_modified
sys.unix.clu.caa.res_registered
sys.unix.clu.caa.res_unregistered
sys.unix.clu.cfs.advsfs_no_server
sys.unix.clu.cfs.advsfs_not_served
sys.unix.clu.cfs.advsfs_served
sys.unix.clu.cfs.fs_no_server
sys.unix.clu.cfs.fs_not_served
sys.unix.clu.cfs.fs_served
sys.unix.clu.clua.config
sys.unix.clu.clua.leave
sys.unix.clu.clua.netroute
sys.unix.clu.clua.no_gated
sys.unix.clu.clua.proxy
sys.unix.clu.clua.routerport
sys.unix.clu.clua.routerstart
sys.unix.clu.clua.routerstop
sys.unix.clu.cnx.member.join
sys.unix.clu.cnx.member.leave
sys.unix.clu.cnx.qdisk.loss
sys.unix.clu.cnx.qdisk.regain
sys.unix.clu.cnx.quorum.gain
sys.unix.clu.cnx.quorum.loss
sys.unix.clu.drd.new_accessnode
sys.unix.clu.drd.no_accessnode
sys.unix.clu.drd.server_add
sys.unix.clu.drd.server_leave
sys.unix.clu.member.add
sys.unix.clu.member.delete
sys.unix.clu.shutdown.abort
sys.unix.clu.shutdown.caa_alert
sys.unix.clu.shutdown.clean
sys.unix.clu.shutdown.private
sys.unix.clu.shutdown.start
sys.unix.clu.versaw
sys.unix.clu.versw.msg_success
sys.unix.clu.wall
```

### 12.4.3.2 EVM 过滤器回顾

所添加的过滤器可以通过使用我们创建的 evf(1) 脚本来查看。我们在第 8 章中讨论了 evf 脚本。

