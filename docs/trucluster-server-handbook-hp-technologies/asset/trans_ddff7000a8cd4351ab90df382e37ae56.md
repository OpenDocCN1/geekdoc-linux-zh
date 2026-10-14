

## NOTE:

成员目录主要用作独立系统成员特定的目录。虽然从技术上讲，独立系统不需要成员特定的目录（因为它除了你的计算机房之外不是任何东西的成员），但它保持了独立和集群环境之间的布局一致性。在集群中，它用作成员特定文件的通用版本存储库。集群成员 ID 范围从 1 到 63。

## 6.1 它是成员特定的还是集群通用的？

一旦系统加入或形成集群，它就成为集群的成员。因此，如果某些东西需要唯一配置，例如网络接口，那么其配置信息必须包含在成员特定的文件中。另一方面，如果某些东西需要为集群中的每个成员相同地配置，例如 NIS，那么其配置信息必须位于集群通用文件中。

从 Tru64 UNIX 版本 5.0 开始，/etc/rc.config 文件已被拆分为两个文件，外加一个可选的第三个文件，如下所示：

- rc.config
- rc.config.common
- rc.config.site（可选）

rc.config 文件是成员特定的，而 rc.config.common 文件是，你猜对了，集群通用的。rc.config.site 文件用于任何站点特定的配置信息。

```
# ls /etc/rc.config*
/etc/rc.config      /etc/rc.config.common
```

那么，是什么使 /etc/rc.config 成为成员特定的？让我们更仔细地查看这两个文件。

```
# file /etc/rc.config*
/etc/rc.config: symbolic link to ../cluster/members/{memb}/etc/rc.config
/etc/rc.config.common: /bin/sh shell script -- commands text
```

请注意，rc.config 文件似乎位于 /etc 目录中，而实际上它位于 "../cluster/members/{memb}/etc" 目录中。/etc/rc.config 文件根本不是一个普通文件，而是一种特殊类型的符号链接，被称为上下文相关符号链接（CDSL）。

### 6.1.1 进入 CDSL

那么，这个 CDSL 到底是什么？CDSL 是一个符号链接，其路径中包含 "{memb}" 变量。"{memb}" 是“上下文”，或者更准确地说，是用于确定上下文的内容。图 6-1 显示了 CDSL 的解析方式。

请注意，“{memb}”等于单词“member”加上成员的 ID。成员的 ID 存储在通用子系统中的属性 memberid 中。独立系统始终具有为零的 memberid。因此，在独立系统上，值为 "../cluster/members/{memb}/etc/rc.config" 的 CDSL 将解析为路径 "../cluster/members/member0/etc/rc.config"。

```
[ /etc ]
# ls -i ../cluster/members/{memb}/etc/rc.config
1817 ../cluster/members/{memb}/etc/rc.config
```

```
[ /etc ]
# ls -i ../cluster/members/member0/etc/rc.config
1817 ../cluster/members/member0/etc/rc.config
```

如果你检查 "ls -i" 输出中列出的两个文件，你会看到它们是完全相同的文件。"-i" 选项显示文件序列号（例如 UFS 文件系统中的 inode 或 AdvFS 文件系统中的 tag）。

```
[ /etc ]
# cd ./tags && /sbin/advfs/tag2name 1817
/cluster/members/member0/etc/rc.config
```

![](img/a0df85c2e542a8d6c913113908553aa4_147_0.png)

图 6-1：CDSL 解析

现在我们已经展示了如何区分成员特定文件和集群通用文件，值得一提的是，对于每条规则都有一个例外。换句话说，这不是成员特定文件存在的唯一方式。创建成员特定文件的另一种方法（虽然要少得多）是，而不是将文件放在成员特定目录中并创建指向它的 CDSL，而是简单地用唯一的扩展名重命名文件。第二种方法的示例在第 16 章中提供，其中描述了 Cluster Alias 子系统。Cluster Alias 子系统使用 gated.conf 文件，通过创建成员特定的 gated.conf 文件并在文件名后附加 "membern" 来实现（例如 /etc/gated.conf.member1）。

### 6.1.2 它在 rc.config 还是 rc.config.common 中？

我们之前提到配置网络接口是成员特定的任务，而配置 NIS 是集群范围的任务，那么这在我们的 rc.config 文件中是如何实现的呢？由于 NIS 是集群范围配置的，那么所有 NIS 变量都应该在 /etc/rc.config.common 中，而不在 /etc/rc.config 中。

```
# grep NIS /etc/rc.config
<nothing is returned>
```

```
# grep NIS /etc/rc.config.common
NIS_DOMAIN="DAN"
export NIS_DOMAIN
NIS_CONF="YES"
export NIS_CONF
NIS_TYPE="CLIENT"
export NIS_TYPE
NIS_ARGS="-s -S DAN, bacon.dec.com, gravy.dec.com"
export NIS_ARGS
```

你可能在问的下一个问题是，“这些文件在启动期间按什么顺序被调用？”为了避免不必要的更改，因为许多 init 脚本已经调用 rc.config，所以决定让 rc.config 调用 rc.config.common。

```
# cat /etc/rc.config
#!/bin/sh
#
# Read in the cluster attributes before overriding them with the member
# specific options.
. /etc/rc.config.common
...
```
