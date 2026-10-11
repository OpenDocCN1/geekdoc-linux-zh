
这是我们第一次遇到许多抽象层之一，即在通用文件系统和特定文件系统之间切换。

```c
42 struct file_operations ext2_operations = (
43     .llseek = generic_file_llseek,
44     .read = generic_file_read,
45     .write = generic_file_write,
46     .aio_read = generic_file_aio_read,
47     .aio_write = generic_file_aio_write,
48     .ioctl = generic_file_ioctl,
49     .mmap = generic_file_mmap,
50     .open = generic_file_open,
51     .release = generic_file_release,
52     .fsync = generic_file_fsync,
53     .readadv = generic_file_readadv,
54     .writeadv = generic_file_writeadv,
55     .sendfile = generic_file_sendfile,
56 );
```

你可以看到，对于大多数文件操作，`ext2` 文件系统使用了通用的实现。由于 `read` 的调用，`ext2` 文件系统需要实现自己的操作。

![](img/65251758f931c5042afa380.png)

FIGURE 6.17 文件操作

当文件创建或挂载时，通用文件系统填充了 `inode` 信息，例如 `ext2` 文件系统。

这里的 `inode` 结构指向了特定文件系统的操作。

图 6.17 解释了通用文件系统如何指向特定文件系统。

![](img/65251758f931c5042afa380.png)

## 6.5 VFS 系统调用与文件系统层

### 第 845–862 行

此 `for` 循环验证了传递的 `iovec` 结构体是由有效段组成的。回想它包含了用户空间的缓冲区信息。

```c
mm/filemap.c
...
863    /* coalesce the iovecs and go direct-to-BIO for O_DIRECT */
864    if (filp->f_flags & O_DIRECT) {
865        loff_t pos = *ppos, size;
866            struct address_space *mapping;
867            struct inode *inode;
868
869
870            mapping = filp->mapping;
871            inode = mapping->host;
872            retval = 0;
873            if (count) {
874                goto out; /* skip item at */
875                size = i_size_read(inode);
876                if (pos < size) {
877                    retval = generic_file_direct_IO(READ, iocb,
878                    iov.pos, nr_segs);
879                    if (retval <= 0 && !is_sync_kio(iocb)) {
880                        retval = -EIOCBQUEUED;
881                    }
882                    if (retval > 0) {
883                        *ppos = pos + retval;
884                    }
885                }
886                file_accessed(filp);
887                goto out;
888            }
}
```

### 第 863–886 行

这段代码只有在读取操作为 I/O 时才会被进入。直接 I/O 会绕过页缓存（`page cache`），这是某些块设备的一个有用特性。然而，对于我们的目的，我们完全不会进入这部分代码。大多数文件 I/O 采用我们的页缓存路径（我们很快就会描述它），这比底层的块设备快得多。

```c
mm/filemap.c
...
887    retval = 0;
888    if (count) {
889        for (seg = 0; seg < nr_segs; seg++) {
```

```c
read_descriptor_t desc;

desc.written = 0;

desc.buf = iov[seg].iov_base;

desc.count = iov[seg].iov_len;

if (desc.count == 0) {

    continue;

}

desc.error = 0;

do_generic_file_read(filp.ppos,&desc.file_read,file_read_actor);

retval += desc.written;

if (!retval) {

    retval = desc.error;

    break;

}

}

out:

return retval;
```
