
当然，可以使用上述描述的覆盖机制添加更多的顶层控制项。内核也会选择此选项，适用于所有分配给 ABI（应用二进制接口）并属于 `CTL_ABI` 类的所有 `sysctl`。

`root_table` 定义中引用的表（如 `kern_table`、`net_table` 等）被定义为静态数组；它们持有 `sysctl` 的值，我们在这里忽略冗长的定义，因为除了额外的 `ctl_table` 实例外它们意义不大。它们的内容可以在内核源码中查看，其定义包含在 `kernel/sysctl.c` 中。

## 注册 Sysctl

除了静态初始化的 `sysctl`，内核还提供了一个接口用于动态注册和使用新的系统控制函数。`register_sysctl_table` 用于注册控制项，其对应的 `remove_sysctl_table` 通常在需要时使用。

`register_sysctl_table` 函数需要一个参数——指向 `ctl_table` 条目数组的指针，在该数组中定义了新的 `sysctl`。该函数还包含几个步骤：首先，实例化一个新的 `ctl_table_header` 并将其与 `sysctl` 表关联。生成的结构被添加到现有的 `sysctl` 列表中。

辅助函数 `sysctl_check_table` 用于检查新条目是否包含正确信息。基本上，它确保不会获取无意义的组合（例如，包含可写目录的目录），并确保普通文件具有有效的读取策略。

注册 `sysctl` 不会自动创建连接 `sysctl` 条目与 `proc` 条目的节点。大多数 `sysctl` 是通过 `proc` 使用的，但这会浪费内存。相反，与 `proc` 文件的连接是动态创建的。在初始化时会创建 `/proc/sys` 目录：

```c
fs/proc/sysctl.c

int proc_init(void)

{

  proc_sys_root = mkdir("sys", NULL);

  proc_sys_root->proc_iops = &proc_sys_inode_operations;

  proc_sys_root->proc_fops = &proc_sys_file_operations;

  proc_sys_root->nlink = 0;

  return 0;

}
```

`proc_sys_inode_operations` 中创建的节点确保了 `/proc/sys` 下的文件和目录在需要时动态生成。该结构的内容如下：

```c
fs/proc/proc_sysctl.c

static struct inode_operations proc_sys_inode_operations = {

    .lookup = proc_sys_lookup,

    .permission = proc_sys_permission,

    .setattr = proc_sys_setattr,

};
```

查找操作由 `proc_sys_lookup` 处理。使用以下方法为 `proc` 条目动态构建节点：

- `do_proc_sys_lookup` 获取 `dentry` 和文件或目录的名称，以查找所需的 `sysctl` 表条目。这主要涉及对之前展示的数据结构的迭代。
- 给父目录的 `inode` 和 `sysctl` 表，使用 `proc_sys_make_inode` 来构建所需的 `inode` 实例。由于新 `inode` 的操作也由 `proc_sys_inode_operations` 实现，因此确保了该方法也适用于子目录。

`/proc/sysctl` 条目的文件定义如下：

```c
kernel/sysctl.c

static struct file_operations proc_sys_file_operations = {

    .read = proc_sys_read,

    .write = proc_sys_write,

    .readdr = proc_sys_readdr,

};
```

所有条目的读写文件操作通过标准操作实现。

## /proc/sys 文件操作

`proc_sys_read` 和 `proc_sys_write` 的实现非常相似。它们都包含三个简单的步骤：

1. `do_proc_sys_lookup` 找到与 `/proc/sys` 中文件关联的 `sysctl` 表。
2. 不能保证 `sysctl` 条目的所有权限都已授予 `root` 用户。例如，某些条目只可读不可修改（即不可写）。因此需要使用 `sysctl_perm` 进行额外的权限检查。虽然 `proc_sys_read` 需要读取权限，但 `proc_sys_write` 则需要写入权限。
3. 调用 `sysctl` 表中的 `proc_handler` 完成操作。

在定义 `sysctl` 表时会为 `proc_handler` 分配一个函数指针。由于各种 `sysctl` 分布在几个标准类别中（根据其参数和返回值），内核提供了标准的实现，通常用于替代特定的函数实现。最常用的函数包括：

- `proc_dointvec` 从内核读取或写入整数值（具体值的数量由 `table->maxlen/sizeof(unsigned int)` 决定）。如果 `maxlen` 表示单个无符号整数的字节数，则可能只涉及单个整数（而不是向量）。
- `proc_dintvec_minmax` 工作工作与 `proc_dointvec` 相同，但它确保每个数字都在 `table->extra`（最小值）和 `table->extra2`（最大值）指定的最小和最大值范围内。范围之外的值都会被忽略。
- `proc_longvec_minmax` 目的相同，但使用类型为 `long` 的值代替它。
- `proc_dintvec_jiffies` 读取整数表。值会被转换为 `jiffies`。
- `proc_dintvec_ms` 值被解释为毫秒。
- `proc_dostring` 在内核和用户空间之间传输字符串，反之亦然。长于条目输入的字符串会被截断。当数据复制到用户空间时，会自动附加一个回车符（'n'），以便在输出后（例如使用 `cat` 时）添加换行。

## 第 10 章：无持久化存储的文件系统

### 编写顺序文件处理程序

基本上，`file_operations` 实例提供了指向某些 `seq_routines` 的指针，但必须实现这些程序才能从顺序文件标准实现中受益。`kprobes` 子系统是这样执行的：

```c
kernel/kprobes

static struct file_operations debugfs_kprobes_operations = (

    .open = kprobes_open,

    .read = seq_read,

    .lseek = seq_lseek,

    .release = seq_release,

);
```

此 `file_operations` 实例可以通过第 8 章讨论的方法与文件关联。在 `kprobes` 的情况下，文件将在调试会话中创建；请参见第 10.2.3 节。

唯一需要实现的方法是 `open`。该函数不需要花费太多精力；简单的单行代码即可连接文件与顺序文件接口：

```c
kernel/kprobes

static struct seq_operations kprobes_seq_ops = (

    .start = kprobes_seq_start,

    .next = kprobes_seq_next,

    .stop = kprobes_seq_stop,

    .show = show_kprobes_addr

);
```

```c
static int __kprobes kprobes_open(struct inode *inode, struct file *filp) {

    return seq_open(filp, &kprobes_seq_ops);

}
```

`seq_open` 设置了顺序文件机制所需的数据结构。结果如图 10-8 所示。回想第 8 章，`struct file` 中的 `private_data` 元素可以指向文件私有的任意数据，这些数据不会被通用 VFS 函数接触。在这种情况下，`seq_open` 使用该指针建立与 `struct seq_file` 实例的连接，该实例包含了关于顺序文件的状态信息：

```c
<seq_file.h>

struct seq_file {

    char *buf;

    size_t size;

    size_t from;

    size_t count;

    loff_t index;

    ...

    const struct seq_operations *op;

};
```
