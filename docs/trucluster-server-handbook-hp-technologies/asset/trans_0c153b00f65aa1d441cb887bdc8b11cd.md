

## 10.4.1 clu_create(8) 命令

让我们从执行 clu_create 命令开始这一过程。clu_create 命令的一个贴心功能是，它会准确告诉你它将执行哪些操作，然后提示你确认这些操作是否确实是你想要执行的。

```
# /usr/sbin/clu_create

This is the TruCluster Creation Program

You will need the following information in order to create a cluster:
- Cluster name (a hostname which is also used as the default cluster alias)
- Cluster alias IP address
- Clusterwide root disk and partition (for example, dsk4b)
- Clusterwide usr disk and partition (for example, dsk4g)
- Clusterwide var disk and partition (for example, dsk4h)
- Quorum disk device (for example, dsk4)
- Number of votes assigned to the quorum disk
- Member ID
- Number of votes assigned to this member
- First member's boot disk (for example, dsk5)
- First member's virtual cluster interconnect IP name
- First member's virtual cluster interconnect IP address
- First member's physical cluster interconnect devices
- First member's NetRAIN device name
- First member's physical cluster interconnect IP address

The program will prompt for this information, offering a default value when one is available. To accept the default value, press Return. If you need help responding to a prompt, either type the word 'help' or type a question mark (?) at the prompt.

The program does not begin to create a cluster until you answer all the prompts, and confirm that the answers are correct.

Cluster creation involves the following steps:
- Labeling disks (when required)
- Creating AdvFS domains
- Copying the files on the current root, usr, and var partitions to the clusterwide partitions
- Creating additional CDELs
- Updating configuration files
- Building a kernel and copying it to the first member's boot disk

After the kernel is built and copied, you will halt the system and boot it using the first member's boot disk.

Do you want to continue creating the cluster? [yes]:
```

### 10.4.1.1 输入集群别名

首先，系统会提示我们输入集群别名。这里，我们查看集群准备检查表和工作表，找到我们计划使用的集群别名和 IP 地址。

```
Each cluster has a unique cluster name, which is a hostname used to identify the entire cluster.
Enter a fully-qualified cluster name []:babylon5.dec.com
Checking cluster name: babylon5.dec.com
You entered 'babylon5.dec.com' as your cluster name.
Is this correct? [yes]:
```

该值将成为 clu_base:cluster_name 属性的值，也称为默认集群别名（更多信息请参阅第 16 章）。

### 10.4.1.2 输入集群别名 IP 地址

```
The cluster alias IP address is the IP address associated with the default cluster alias. (192.168.168.1 is an example of an IP address.)
Enter the cluster alias IP address []: 
Checking cluster alias IP address: 192.168.0.70
You entered '192.168.0.70' as the IP address for the default cluster alias.
Is this correct? [yes]:
```

集群别名 IP 地址会被写入 /etc 目录下的 hosts 文件中。

### 10.4.1.3 输入 cluster_root、cluster_usr 和 cluster_var 分区

根据集群准备检查表和工作表中的磁盘及分区规划信息，我们输入为 cluster_root、cluster_usr 和 cluster_var 预留的分区。

```
The cluster root partition is the disk partition (for example, dsk4b) that will hold the clusterwide root (/) file system.
Note: The default 'a' partition on most disks is not large enough to hold the clusterwide root AdvFS domain.
```

