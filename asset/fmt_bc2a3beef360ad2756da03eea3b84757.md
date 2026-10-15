
其他远程过程的参数包括一个或多个文件规范。例如，重命名文件的远程过程需要两个文件名：现有文件的名称和该文件的新名称。重命名过程的参数被声明为 `diropsarg` 结构体：

```
struct renameargs { /* RENAME 操作的参数 */
    diropsarg from;   /* 现有文件 */
    diropsarg to;     /* 文件的新位置/名称 */
};
```

给出旧文件名和新文件名的各个字段被声明为 `diropsarg` 类型。

大多数其他 NFS 参数类型对应于远程过程。例如，NFS 定义了 `writeargs` 结构体，用于指定向文件写入数据调用时使用的参数：

一旦声明了常数和数据类型，只需指定实现协议的远程过程即可。一个 NFS 服务器提供一个实现 18 个过程的远程程序。使用 RPC 语言，可以声明该程序：

```
program NFS_PROGRAM {
    version NFS_VERSION {
        void NFSPROC_NULL(void) = 0;
        attrstat NFSPROC_GETATTR(handle) = 1;
        attrstat NFSPROC_SETATTR(sattargs) = 2;
        void NFSPROC_ROOT(void) = 3;
        diopargres NFSPROC_LOOKUP(diopargs) = 4;
        readlinkres NFSPROC_READLINK(handle) = 5;
        readres NFSPROC_READ(readargs) = 6;
        void NFSPROC_WRITECACHE(void) = 7;
        attrstat NFSPROC_WRITE(writeargs) = 8;
        diopargres NFSPROC_CREATE(createargs) = 9;
        stat NFSPROC_REMOVE(diopargs) = 10;
        stat NFSPROC_RENAME(renameargs) = 11;
        stat NFSPROC_LINK(linkargs) = 12;
        stat NFSPROC_SYMLINK(symlinkargs) = 13;
        diopargres NFSPROC_MKDIR(createargs) = 14;
        stat NFSPROC_RMDIR(diopargs) = 15;
        readdirres NFSPROC_READDIR(readdirargs) = 16;
        statfs NFSPROC_STATFS(handle) = 17;
    } /* NFS 协议当前版本 */
} = 100003; /* 分配给 NFS 的 RPC 程序号 */
```

## 2.6 NFS 操作的语义

大多数 NFS 操作的语义遵循 UNIX 文件操作的语义。以下章节描述了其中一个 NFS 远程过程的操作方式。

### 24.6.1 NFSPROC_NULL (过程 0)

按照惯例，任何 RPC 程序中的过程 0 都称为“空（null）”，因为它不执行任何操作。应用程序可以调用它来测试给定服务器是否有响应。

### 24.6.2 NFSPROC_GETATTR (过程 1)

客户端调用过程 1 以获取文件的属性，包括保护模式、所有者、大小和最后访问时间等项。

### 24.6.3 NFSPROC_SETATTR (过程 2)

过程 2 允许客户端设置文件的某些属性。客户端不能设置所有属性（例如，它无法通过向文件添加字节或将其截断来更改记录的文件大小）。如果调用成功，返回的结果将包含应用更改后的文件属性。

### 24.6.4 NFSPROC_ROOT (过程 3) [在 NFS3 中已废弃]

过程 3 为早期版本的 NFS 定义，但现在已废弃。它已被挂载协议所取代。

### 24.6.5 NFSPROC_LOOKUP (过程 4)

客户端调用过程 4 在目录中搜索文件。如果成功，返回的值将文件句柄和文件的属性。

### 24.6.6 NFSPROC_READLINK (过程 5)

过程 5 允许客户端从符号链接读取值。

### 24.6.7 NFSPROC_READ (过程 6)

过程 6 是最重要的功能之一，因为它允许客户端从目录读取数据。如果操作成功，服务器返回 `readres`；如果操作失败，则返回错误。

### 24.6.8 NFSPROC_WRITECACHE (过程 7) [在 NFS3 中不再使用]

过程 7 不在当前协议中使用。

### 24.6.9 NFSPROC_WRITE (过程 8)

过程 8 允许客户端向文件写入数据。如果操作成功，返回 `attrbuf` 联合体；如果操作失败，则返回错误。

### 24.6.10 NFSPROC_CREATE (过程 9)

客户端调用过程 9 在目录中创建文件。如果操作成功，返回返回文件的属性；如果操作失败，则返回错误。

### 24.6.11 NFSPROC_REMOVE (过程 10)

过程 10 允许客户端删除文件。如果操作成功，返回一个 `stat` 值。

### 24.6.12 NFSPROC_RENAME (过程 11)

过程 11 允许客户端重命名文件。NFS 保证重命名是原子的，这意味着重命名操作期间文件将不可见。

### 24.6.13 NFSPROC_LINK (过程 12)

客户端调用过程 12 为现有文件创建硬链接。NFS 保证如果文件有多个链接，可以通过 magic cookie 访问它。

### 24.6.14 NFSPROC_SYMLINK (过程 13)

过程 13 创建符号链接。如果调用成功，返回 `attrstat` 联合体；如果调用失败，则返回错误。

### 24.6.15 NFSPROC_MKDIR (过程 14)

客户端调用过程 14 创建目录。如果调用成功，返回新目录的句柄及其属性；如果失败则返回错误。

### 24.6.16 NFSPROC_RMDIR (过程 15)

客户端可以使用过程 15 移除目录。像 UNIX 一样，目录必须为空才能被移除。要移除子树，客户端必须遍历子树并移除所有文件。通常，空目录的移除是通过后序遍历完成的。

### 24.6.17 NFSPROC_READDIR (过程 16)

客户端调用过程 16 从目录读取条目。参数结构 `readdirargs` 指定要读取的目录句柄、magic cookie 以及最大字符数。在初始调用时，客户端指定的 magic cookie 为 0，这导致服务器从目录开始读取。返回值的类型为 `readdirdata`，包含一个或多个目录条目的列表以及一个指示是否到达末尾的布尔值。
成功返回后，列表中的每个条目包含文件名、文件的唯一标识符、文件在目录中位置的 magic cookie 以及指向下一个条目的指针。
要读取目录条目序列，客户端首先调用 `NFSPROC_READDIR`，并将 magic cookie 置 0，字符数等于其内部缓冲区的大小。服务器返回尽可能多放入缓冲区的条目。如果返回值显示客户端已到达目录末尾，则停止处理。否则，客户端使用最后一个条目的 magic cookie 再次调用服务器以获取更多条目。客户端继续读取条目组，直到完成读取。

### 24.6.18 NFSPROC_STATFS (过程 17)

过程 17 允许客户端获取文件所在远程文件系统的信息。返回的结果是 `statfs` 类型的结构体，包含指定优化传输大小（即产生最佳传输速率的读写请求大小）、存储设备上的块大小、设备上的块数、当前未使用的块数以及特权用户可用的空闲块数的字段。

复杂的客户端程序可以使用 `NFSPROC_STATFS` 来优化传输，或者估计磁盘上是否留有足够的空间来满足写入请求。

## 24.7 挂载协议 (The Mount Protocol)

第 22 章描述的挂载协议也是使用 RPC 定义的。尽管 NFS 服务器必须有一个配套的挂载服务器，但它们被定义为两个独立的远程程序。因此，挂载协议的标准规定了常量、类型以及构成该服务器的一组远程过程。

### 24.7.1 挂载常量定义

虽然这两个协议是分别定义的，但为挂载协议定义的许多常量和类型的值都源自 NFS 协议中使用的对应常量。事实上，如果这两个协议不对文件句柄等对象使用通用的表示，它们将无法协同工作。例如，挂载按如下定义了文件名、路径名和文件句柄的大小：

```
const MNAMELEN = 255;
```

```
const NFTPATHLEN = 1024;
```

```
const FSIZE = 32;
```

这些声明使用 RPC 语法，每个声明将长度表示为字节数。

### 24.7.2 挂载类型定义

挂载协议还规定了与 NFS 协议中的计数对应的类型定义。例如，挂载规定了文件句柄的类型：
