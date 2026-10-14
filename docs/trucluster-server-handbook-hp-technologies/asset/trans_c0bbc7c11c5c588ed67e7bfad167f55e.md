

下面输出中显示的子系统属性没有参考页面支持。我们给出的是对这些属性含义的最佳估计。在查看它们之前，这里有一些额外的术语和概念。

首先发起“set”的成员将是“synchronizer”成员（可以把它想成锁管理器中的导演——它使用类似的策略）。对 set 的其他引用是通过将 set 名称哈希成一个数字来解析的，使用该数字作为目录权重表中的偏移量，该表包含集群系统 ID（csids）。在哈希表中计算出的偏移位置找到的 csid 将是该 set 的 synchronizer 成员的导演的 ID。请注意，导演成员也可能是 synchronizer。导演成员（通过目录权重表找到）检查其“set”信息，以查看它是否知道请求的 set 的“synchronizer”是哪个成员。“director”响应“initiator”并指出“synchronizer”成员是谁。对该 set 的后续请求将直接发送给 synchronizer。其思想是将 KGS 活动分布在集群的成员上。如果集群中有一个成员的容量远大于其他成员，你可以通过增加下面的 kch_dirwt 属性来提高它被选为“synchronizer”的几率（最大值是 4）。请注意，截至本文撰写时，kch_dirwt 的值固定为 1。

## CAUTION:

这些属性不应被更改，除非由 HP 工程部门指示这样做。

```
# sysconfig -q kch
kch:
kch_enabled = 1
kch_sets_allocated = 25
kch_mbrs_allocated = 25
kch_lstnrs_allocated = 0
kch_dirwt = 1
kch_set_tbl_hash_size = 8192
```

- Service enabled (1=yes)
- Existing set count
- Members are active set participants
- Listeners are nonvoting members of a set
- Directory table weighting factor
- Hash table size

```
# sysconfig -Q kch
kch:
kch_enabled - type=INT op=CQ min_val=0 max_val=1
kch_sets_allocated - type=UINT op=Q min_val=0 max_val=4294967295
kch_mbrs_allocated - type=UINT op=Q min_val=0 max_val=4294967295
kch_lstnrs_allocated - type=UINT op=Q min_val=0 max_val=4294967295
kch_dirwt - type=INT op=Q min_val=0 max_val=4
kch_set_tbl_hash_size - type=UINT op=CQ min_val=8192 max_val=32768
```

## 18.5 Cluster Mount Services (CMS)

到现在你可能已经意识到，集群背后有许多组件在努力使整个复杂环境的运行尽可能透明。其中一个默默完成工作的组件是 Cluster Mount Services (CMS)。不知怎么的，神奇的是，当你在集群的一个成员上挂载文件系统时，所有其他成员都能看到挂载点。并不是说我们要把它变成内部讨论，但每个已挂载的文件系统都在内核中由一个挂载结构支持。没什么大不了，对吧？考虑到该活动是在一个集群成员上发起的，但最终却写入了所有集群成员的内核地址空间！这是一项非常令人印象深刻的壮举，需要所有集群成员之间进行同步（是的，它确实涉及 DLM 来实现部分同步——但你已经在想了，对吧？）。

以下输出显示了限制每种文件系统类型可用的集群范围挂载数量的 CMS 子系统属性。

```
# sysconfig -q cms

cms:
  cmsdbg_flags = 0
  cfs_advs_mount_limit = 4096
  cfs_cdf_mount_limit = 512
  cfs_dvfs_mount_limit = 512
  cfs_nfs_mount_limit = 8192
  cfs_ufs_mount_limit = 512
  cfs_vxfs_mount_limit = 512
```

```
# sysconfig -Q cms

cms:
  cmsdbg_flags = type=ULONG op=CRQ min_val=0 max_val=18446744073709551615
  cfs_advs_mount_limit = type=INT op=CRQ min_val=0 max_val=2147483647
  cfs_cdf_mount_limit = type=INT op=CRQ min_val=0 max_val=2147483647
  cfs_dvfs_mount_limit = type=INT op=CRQ min_val=0 max_val=2147483647
  cfs_nfs_mount_limit = type=INT op=CRQ min_val=0 max_val=2147483647
  cfs_ufs_mount_limit = type=INT op=CRQ min_val=0 max_val=2147483647
  cfs_vxfs_mount_limit = type=INT op=CRQ min_val=0 max_val=2147483647
```

挂载活动始于涉及 CFS 的本地挂载命令，最终通过 RPC 传播到其他集群成员。CMS 活动大量涉及 KGS（第 18.4 节）。事实上，我们可以说 CMS 是 KGS 的客户端。CMS 从 KGS 接收挂载提案（以及成员变更信息）。挂载成员可能会被告知（通过 KGS）该文件系统已被另一成员挂载。在这种情况下，CMS 只是“加入”KGS set。如果尚未被另一成员挂载，则该成员会提议其他成员“加入”代表该文件系统的新 KGS set。

KGS 是 CMS 的核心，并使用 DLM 进行同步。

