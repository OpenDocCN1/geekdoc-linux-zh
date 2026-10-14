

## 11.1 准备

据说准备不足就是在为失败做准备。牢记这一点，请花时间规划和准备集群的部署。从第 4.8 节的集群准备清单和工作表开始制定部署计划，然后执行该计划。

### 11.1.1 规划添加另一个集群成员

有关向集群添加成员的所有要素均在第 4 章中进行了详细讨论。请查阅第 4 章以获取更多信息，并且请再次使用集群准备清单和工作表作为规划集群的指南。

### 11.1.2 准备就绪

您应该从至少一个已成功配置的单节点集群开始。假设您已计划并准备好向集群添加成员，那么您就可以准备向集群添加新成员了。以下小节涵盖了一些最后的事项。

#### 11.1.2.1 一次添加或删除一个成员

由于添加新成员或删除成员非常容易，因此需要注意的是，您应在启动对另一个集群成员的添加或删除操作之前，完全完成对一个集群成员的添加或删除。为什么？为了避免任何集群法定人数问题。在集群的上下文中，保持法定人数并在添加或删除集群成员时根据需要进行调整至关重要。

#### 11.1.2.2 新成员引导磁盘

此时应已确定要添加的集群成员的引导磁盘或 boot_partition。如果尚未确定，请查阅第 4 章以及集群部署计划。

此时，使用第 10.1.2 节中的信息正确分区成员引导磁盘并为其写入适当的 disklable。写入 disklable 后，它应具有成员 boot_partition、swap 和集群状态分区所使用的适当 in-use fstype。如果不是这种情况，请参阅第 10.1.2 节，审查集群部署计划，并再次创建适当的 disklable。

#### 11.1.2.3 初始化 SRM 控制台变量

如果新集群成员的与引导相关的 SRM 控制台变量尚未初始化以防止新集群成员在安装期间启动，则应在开始将该成员添加到集群的过程之前完成此操作。有关更多信息，请参阅第 4.5.3 节。

## 11.2 添加新集群成员

要向集群添加新系统或新成员，我们在现有集群成员上执行 clu_add_member(8) 命令。clu_add_member 命令执行以下操作：

- 在 cluster_root、cluster_usr 和 cluster_var 文件系统中为新成员创建目录和文件。
- 为新成员标记并填充引导磁盘。
- 配置分层产品软件子集。
- 构建新内核并将其复制到新成员的 boot_partition 中。
- 将会话记录写入日志文件 clu_add_member.log，该文件位于 /cluster/admin 目录中。它还将新成员的配置信息写入同一目录中的 .membern.cfg 文件（其中 n 为新成员的 memberid）。
- 新集群成员上没有软件安装。由于这是一个集群，我们只需安装一次软件，而这是在集群首次创建时完成的。

在现有集群成员上执行 clu_add_member 命令。请注意，与第 10 章中的 clu_create 命令类似，clu_add_member 命令会告诉我们需要哪些信息以及它将执行哪些操作来创建新的集群成员。

```
# /usr/sbin/clu_add_member

This is the TruCluster Add Member Program

You will need the following information in order to add a member to the cluster:
- Hostname
- Member ID (1-63)
- Members Votes
- Member's boot disk (for example, dsk7)
- Member's virtual cluster interconnect IP name
- Member's virtual cluster interconnect IP address
- Member's physical cluster interconnect devices
- Member's NetRAIN device name
- Member's physical cluster interconnect IP address
- Member's cluster license

The program will prompt for this information, offering a default value when one is available. To accept the default value, press Return if you need help responding to a prompt, either type the word 'help' or type a question mark (?) at the prompt.

The program does not begin to add the member until you answer all the prompts, and you confirm that the answers are correct.
```
