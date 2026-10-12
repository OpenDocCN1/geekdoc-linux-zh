
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

Wait that's example. Need actual processing.

Let's produce final output for given text.

I'll produce cleaned markdown.
[content]
```
fs/name.c

/* 普通权限例程序不支持 MAY_APPEND。 */
    submask = mask & ~MAY_APPEND;
    if (inode->i_op && inode->i_op->permission)
        retval = inode->i_op->permission(inode, submask, nd);
else
    retval = generic_permission(inode, submask, NULL);

if (retval)
    return retval;

return security_inode_permission(inode, mask, nd);
```

如果这些中任何一个拒绝以所需方式访问对象的权限，则会立即返回错误代码。如果结果为零，仍然有必要通过 `security_inode_permission` 调用适当的安全钩子，由它给出最终裁决。

注意，大多数文件系统依赖于 `generic_permission`，但可以传递一个特殊的处理程序进行 ACL 检查。因此，`generic_permission` 不仅需要 inode 和权限请求作为参数，还需要回调 `check_acl`。首先，`generic_permission` 需要确定是使用用户、组还是其他权限。

- 如果进程的 UID 与 inode 的 UID 一致，则使用用户权限。
- 如果 inode 的 GID 位于进程所属的组列表中，则使用组权限。
- 如果上述条件都失败，则使用其他权限。

其实现方式如下：

```
int generic_permission(struct inode *inode, int mask,
    int (*check_acl)(struct inode, int))
{
    umode_t mode = inode->i_mode;

    if (current->fsuid == inode->i_uid)
        mode >= 6;
    else {
        if (IS_POSIXACL(inode) && (mask & S_IRWXG)) {
            int error = check_acl(inode, mask);
            if (error == -EACCES)
                goto check_capabilities;
            else if (error != -EAGAIN)
                return error;
        }

        if (in_group_p(inode->i_gid))
            mode >= 3;
    }
}
```

检查 `fsuid` 是简单的。如果 `fsuid` 与 inode 匹配，则需要将模式值移动六位，使得“所有者”位变为最高位。检查 `fsgid` 稍微复杂一些，因为需要考虑进程所属的所有组，因此这被委托给了（未讨论）辅助函数 `in_group_p`。如果成功，则需要将模式值移动三位，使得“组”位变为最低位。注意内核可能需要执行 ACL 检查。

如果 UID 和 GID 检查失败，则不对模式位进行移动，“其他”位保持为最低位。

裁量访问控制（DAC）检查在选定的权限上进行：

```
fs/name.c

    if ((mode & mask & (MAY_READ|MAY_WRITE|MAY_EXEC)) == mask)
        return 0;
    ...
```

如果模式位允许所需的掩码，则返回零。这表示操作是被允许的。

DAC 失败并不意味着所需操作被禁止，因为能力可能仍然允许它。内核如下测试这一点：

```
fs/name.c

check_capabilities:
    /*
     * 读写 DAC 总是可以覆盖的。
     * 可执行 DAC 在设置了至少一个执行位时是可以覆盖的。
     */
    if (!(mask & MAY_EXEC))
        (inode->i_mode & S_IXUGO) || S_ISDIR(inode->i_mode))
            if (capable(CAP_DAC_OVERRIDE))
                return 0;

    /*
     * 搜索包含目录，否则不包含。
     */
    if (mask == MAY_READ || (S_ISDIR(inode->i_mode)) && !(mask & MAY_WRITE))
        if (capable(CAP_DAC_READ_SEARCH))
            return 0;

    return -EACCES;
```

如果进程拥有 `CAP_DAC_OVERRIDE` 能力，只要满足以下任何条件，将授予所需的权限：

+ 请求了读或写访问，但没有请求执行访问。
* 设置了至少一个执行位。
* inode 代表一个目录。

# 第 8 章：虚拟文件系统

另一个发挥作用的是 `CAP_DAC_READ_SEARCH`，它赋予进程在读取文件和搜索目录时覆盖 DAC 决策的权利。如果存在该能力，只要满足以下任一条件即可允许访问：

- 请求了读取（Read）操作。
- 相关的 inode 是目录，且没有请求访问（No access）。

最后，问题在于 ACL（访问控制列表）是如何被考虑的。如果相关的 inode 关联了 ACL（通过 `IS_POSIXACL` 检查），并且通过 `generic_permission` 传递了 ACL 权限检查回调，则该回调将被一直使用，直到当前任务结束并与涉及文件的 UID 进行比较为止。如果所需的访问被拒绝，进程能力可能仍然允许该操作。（注意，如果提供了 ACL 回调，可以跳过 DAC 检查，因为标准的 DAC 检查已包含在 ACL 检查中）。否则，直接返回 ACL 检查的结果。

## 8.6 总结

Unix 的核心理念之一是每个资源都可以用文件表示，而 Linux 继承了这一观点。因此，文件是内核世界中的重要成员，人们在它们的表示上花费了大量精力。本章介绍了虚拟文件系统，它是一个位于深层内核层和用户态之间的粘接层。它提供了各种抽象数据结构来表示文件和 inode，真实文件的实现必须适应这些结构，以便应用程序无论底层文件系统如何都能使用相同的接口来访问和操作文件。

我讨论了文件系统如何在文件系统树中挂载供用户应用程序使用，并额外展示了如何使用共享子树根据命名空间创建“全局”文件系统的不同视图。你还学习了内核使用了一些用户态不可见的伪文件系统，但这些文件系统仍然包含了一些用于内部目的的信息。

打开文件需要遍历文件树，你已经看到 VFS 层是如何解决这个问题的。一旦文件被打开，就可以对其进行读写操作，你还看到了 VFS 是如何参与这些操作的。

最后，你了解到内核提供了一些通用标准函数，这使得像 Ext3 这样的真实文件系统变得更容易（下一章将讨论），以及内核如何确保只有具有适当权限的用户才能访问文件系统中的对象。

# 扩展文件系统家族

第 8 章讨论的虚拟文件系统的接口和数据结构的结构和布局定义了一个文件系统实现必须遵循运行的框架。然而，这并不意味着当文件组织在块设备上以永久存储内容时，每个文件系统都必须采用相同的思想、方法和概念。恰相反：Linux 支持多种概念，包括易于实现和理解但不是特别强大的概念（例如 Minix 文件系统）；被数百万用户使用的久经考验的 Ext2 文件系统；为支持基于 RAM 和 ROM 的方法设计的特定版本；高可用集群文件系统；以及通过日志快速恢复一致性的现代树形文件系统。没有其他操作系统具有这种多灵活性。

尽管由于虚拟文件系统的存在，它们可以通过相同的接口（无论是从用户态还是内核节点）来处理，但由于它们可以被处理，在所使用的技术上存在显著差异。由于支持的文件系统非常多，这里无法对每一个实现都进行讨论，即使是简要讨论。相反，本章侧重于扩展文件系统，即 Ext2 和 Ext3 文件系统。它们说明了文件系统开发基础的核心概念。

## 9.1 引言

Ext2 和 Ext3 可以简要刻描述如下：

- 第二次扩展文件系统（Second Extended Filesystem）——它从 Linux 早期一直存在，并证明自己是许多服务器和桌面系统的骨干，在这些系统中表现得非常好。Ext2 文件系统的设计使用了与虚拟文件系统使用的非常相似的结构，这是因为它是为了 Linux 中的优化操作而开发的。尽管如此，它可以与其他操作系统一起使用。
- 第三次文件系统（Third Filesystem）——这是 Ext2 的演进发展。它仍然很大程度上兼容 Ext2，但提供了一种扩展——日志记录（journaling），这对于从系统崩溃中恢复非常有帮助。本章也简要看了 Ext3 的日志。与 Ext2 相比，该特性具有几个有趣的选项，但基本文件系统原理没有改变。
