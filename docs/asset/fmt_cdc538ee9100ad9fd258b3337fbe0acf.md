
`fs/namespace.c`

```c
1137 void _init_mnt_init(unsigned long mempages)
(
1139     struct list_head *d;
1140     unsigned long order;
1141     unsigned int nr_hash;
1142     int i;
1149     order = 0;
1150     mount_hashtable = (struct list_head *
1151         _get_free_pages(GFP_ATOMIC, order);
1153     if (!mount_hashtable)
1154         panic("Failed to allocate mount table");
1161     nr_hash = (1UL << order) * PAGE_SIZE / sizeof(struct list_head);
1162     hash_bits = 0;
1163     do {
1164         hash_bits++;
1165     } while (nr_hash >> hash_bits) != 0;
1166     hash_bits--;
1172     nr_hash = 1UL << hash_bits;
1173     hash_mask = nr_hash - 1;
1175     printf("Mount-cache: %d (%ld, %ld)\n",
1176     nr_hash, order, PAGE_SIZE);
1179     d = mount_hashtable;
1180     i = nr_hash;
1181     do {
1182         INIT_LIST(d);
1183         d++;
1184         i--;
1185     } while (i);
```

### 第 1139–1144 行

哈希表包含一个页。4 详细解释了 `get_free_pages()` 的工作原理。简而言之，该例程返回一个内存区域。在这种情况下，哈希表包含一个页。

### 第 1161–1173 行

下一个步骤是确定哈希表的大小。`nr_hash` 设置为 2 的幂。`hash_bits` 是 `nr_hash` 的位数。1172 行重新定义了 `nr_hash`。

### 第 1179–1185 行

最后，通过调用 `INIT_LIST` 宏初始化哈希表，其中包含一个内存页。由于 `order` 等于 0，`nr_hash` 等于 500。例如，如果 `order` 是 0，则 `nr_hash` 是 500，这表示 500 个页。`000000000000` 计数。通过循环的每次迭代，得到以下结果：初始值为 `hash_bits` 为 0，`nr_hash` 为 500。

- 第一次迭代：`hash_bits` 为 1，`(500 >> 1) != 0` `(0001 1111 1010)`
- 第二次迭代：`hash_bits` 为 2，`(500 >> 2) != 0` `(0001 1111 1010) = 0000 1111`
- 第三次迭代：`hash_bits` 为 3，`(500 >> 3) != 0` `(0001 1111 1010) = 0000 0111`
- 第四次迭代：`hash_bits` 为 4，`(500 >> 4) != 0` `(0001 1111 1010) = 0000 0001 1111`
- 第五次迭代：`hash_bits` 为 5，`(500 >> 5) != 0` `(0001 1111 1010) = 0000 0000 1111`
- 第六次迭代：`hash_bits` 为 6，`(500 >> 6) != 0` `(0001 1111 1010) = 0000 0000 0111`
- 第七次迭代：`hash_bits` 为 7，`(500 >> 7) != 0` `(0001 1111 1010) = 0000 0000 0011`
- 第八次迭代：`hash_bits` 为 8，`(500 >> 8) != 0` `(0001 1111 1010) = 0000 0000 0001`
- 第九次迭代：`hash_bits` 为 9，`(500 >> 9) != 0` `(0001 1111 1010) = 0000 0000 0000`

## 8.5 起点：`start_kernel()`

```c
222 );
...
237 int __init init_rootfs(void)
238 {
239     return register_filesystem(&rootfs_fs_type);
240 }
```

`rootfs` 文件系统是内核挂载的初始文件系统。它是一个简单且几乎为空的目录，在内核启动过程的后期，会被真实的文件系统挂载（overmounted）。

### 第 218–222 行

此代码块是 `rootfs_fs_type` `file_system_type` 结构体的声明。只定义了获取和杀死关联超级块（superblock）的两个方法。

### 第 237–240 行

`init_rootfs()` 例程仅仅是将此 `rootfs` 注册到内核。这使得内核内部可以使用关于文件系统类型的所有信息（存储在 `file_system_type` 结构体中）。

```c
init_mount_tree()
fs/namespace.c
1107 static void __init init_mount_tree(void)
1108 {
1109     struct vfsmount *mntnt;
1110     struct namespace *namespace;
1111     struct task_struct *g, *p;
1112
1113     mntnt = do_kern_mount("rootfs", 0, "rootfs", NULL);
1114     if (IS_ERR(mntnt))
1115         panic("Can't create rootfs");
1116         namespace = kmalloc(sizeof(namespace), GFP_KERNEL);
1117         if (!namespace)
1118             panic("Can't allocate init namespace");
1119         atomic_set(&namespace->count, 1);
1120         INIT_LIST_HEAD(&namespace->list);
1121         init_rwsem(&namespace->sem);
1122         list_add(&mntnt->mnt_list, &namespace->list);
1123         namespace->root = mntnt;
1124
1125     init_task->namespace = namespace;
1126     read_lock(&tasklist_lock);
1127     do_each_thread(g, p) {
1128         get_namespace(namespace);
1129         p->namespace = namespace;
1130 ) while_each_thread(g, p);
1131     read_unlock(&tasklist_lock);
1132
1133     set_fs_pwd(current->fs, namespace->root,
      namespace->root->mnt_root);
1134     set_fs_root(current->fs, namespace->root,
      namespace->root->mnt_root);
1135 }
```

### 第 1116–1123 行

初始化进程命名空间（namespace）。该结构保留了指向挂载树相关结构和对应 dentry 的指针。命名空间对象被分配，计数设置为 1，类型为 `list_head` 的字段被初始化，锁定命名空间（以及挂载树）的信号量被初始化，对应 `vfsmount` 结构的 `root` 字段被设置为指向我们新分配的 `vfsmount`。

### 第 1125 行

当前任务（init 任务）的进程描述符 `namespace` 字段被设置为指向我们刚刚分配并初始化的命名空间。（当前进程是进程 0。）

### 第 1134–1135 行

以下例程设置了与我们进程关联的 `fs_struct` 中四个字段的值。`fs_struct` 持有由这两个例程设置的用于根目录和当前工作目录条目的字段。

我们刚刚完成了探索了 `mnt_init` 函数中发生了什么。让我们继续探索 `vfs_mnt_init`。
