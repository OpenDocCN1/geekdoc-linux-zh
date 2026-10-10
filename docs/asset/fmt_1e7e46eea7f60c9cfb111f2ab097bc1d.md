
```c
struct gendisk {

    int major;    /* 设备主设备号 */

    int first_minor;    /* 起始次设备号 */

    int minors;    /* 次设备号的最大数量。

                   每个磁盘分区有一个次设备号 */

    char disk_name[32];    /* 磁盘名称 */

    /* ... */

    struct block_device_operations *ops;

    /* 块设备操作。

       很快会描述。 */

    struct request_queue *queue; /* 与此磁盘相关联的请求队列。

                                  稍后讨论。 */

    /* ... */

};
```

2. 与每个块驱动程序相关的 I/O 请求队列使用在 `include/linux/bkdev.h` 中定义的 `request_queue` 结构来描述。这是一个很大的结构，但你可能会用到的唯一组成字段是 `request` 结构，将在下文描述。

3. `request_queue` 中的每个请求使用在 `include/linux/bkdev.h` 中定义的 `request` 结构来表示：

```c
struct request {

    /* ... */

    struct request_queue *q; /* 包含的请求队列 */

    /* ... */

    sector_t sector;    /* 请求数据访问的扇区 */

    /* ... */

    unsigned long nr_sectors; /* 剩余需要提交的扇区数量 */

    /* ... */

    struct bio *bio;    /* 关联的 bio。

                        很快会讨论。 */

    /* ... */

    char *buffer;    /* 用于数据传输的缓冲区 */
```

#### 4. `block_device_operations`
`block_device_operations` 是字符驱动中使用的 `file_operations` 结构体的块驱动对应项。它包含以下与块驱动相关的入口点：

- 标准方法，如 `open()`、`release()` 和 `ioctl()`
- 支持可移除块设备的专业方法，如 `media_changed()` 和 `revalidate_disk()`

`block_device_operations` 在 `include/linux/fs.h` 中的定义如下：

```c
struct block_device_operations {

int (*open) (struct inode *, struct file *); /* Open */

int (*release) (struct inode *, struct file *);/* Close */

int (*ioctl) (struct inode *, struct file *, unsigned, unsigned long); /* I/O Control */

/* ... */

int (*media_changed) (struct gendisk *); /* Check if media is available or ejected */

int (*revalidate_disk) (struct gendisk *); /* Gear up for newly inserted media */

/* ... */

};
```

#### 5. `bio`
当我们查看 `request` 结构体时，看到它与一个 `bio` 相关联。`bio` 结构体是页级粒度的块 I/O 操作的低层描述。它定义在 `include/linux/bio.h` 中，如下所示：

```c
struct bio {

sector_t bi_sector; /* Sector from which data access is requested */

struct bio *bi_next; /* List of bio nodes */

/* .. */

unsigned long bi_rw; /* Bottom bits of bi_rw contain the data-transfer direction */

/* ... */

struct bio_vec *bi_io_vec; /* Pointer to an array of bio_vec structures */

unsigned short bi_vcnt; /* Size of the bio_vec array */

unsigned short bi_idx; /* Index of the current bio_vec in the array */

/* ... */

};
```
