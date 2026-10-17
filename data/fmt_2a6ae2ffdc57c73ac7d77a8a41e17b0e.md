
### 输出示例

`F_RDLOCK` - Lock would succeed

...

Testing `F_WRLOCK` on region from 10 to 15

Lock would fail. `F_GETLK` returned:

`1_type 0, 1_whence 0, 1_start 10, 1_len 20, 1_pid 1534`

Testing `F_RDLOCK` on region from 10 to 15

`F_RDLOCK` - Lock would succeed

Testing `F_WRLOCK` on region from 15 to 20

Lock would fail. `F_GETLK` returned:

`1_type 0, 1_whence 0, 1_start 10, 1_len 20, 1_pid 1534`

Testing `F_RDLOCK` on region from 15 to 20

`F_RDLOCK` - Lock would succeed

...

Testing `F_WRLOCK` on region from 25 to 30

Lock would fail. `F_GETLK` returned:

`1_type 0, 1_whence 0, 1_start 10, 1_len 20, 1_pid 1534`

Testing `F_RDLOCK` on region from 25 to 30

`F_RDLOCK` - Lock would succeed

...

Testing `F_WRLOCK` on region from 40 to 45

Lock would fail. `F_GETLK` returned:

`1_type 1, 1_whence 0, 1_start 40, 1_len 10, 1_pid 1534`

Testing `F_RDLOCK` on region from 40 to 45

Lock would fail. `F_GETLK` returned:

`1_type 1, 1_whence 0, 1_start 40, 1_len 10, 1_pid 1534`

...

Testing `F_RDLOCK` on region from 95 to 100

`F_RDLOCK` - Lock would succeed

## 工作原理

对于文件中的每组五个字节，`lock4` 会设置一个区域来对文件进行加锁测试，然后使用它来检查该区域是否可以写入或读取。返回的信息显示了从字节0开始偏移的区域，该区域会导致请求失败。由于返回结构体中的 `1_pid` 部分包含当前持有锁的程序的进程标识符，程序将其设置为 `-1`（一个无效值），然后在 `fcntl` 调用返回时检查它是否发生了变化。如果该区域当前未被锁定，则 `1_pid` 将保持不变。

为了理解输出内容，我们需要在文件中包含 `fcntl.h`（通常为 `/usr/include/fcntl.h`），以便知道 `1_type` 为 `1` 是由于 `F_WRLOCK` 的定义为 `1`，而 `1_type` 为 `0` 是由于 `F_RDLOCK` 的定义为 `0`。因此，`1_type` 为 `1` 告诉我们由于已存在写锁导致加锁失败，而 `1_type` 为 `0` 则是由已存在的读锁引起的。在 `lock3` 未锁定的文件区域上，共享锁和排占锁都将成功。

从字节 `10` 到 `30`，我们可以看到可以获得共享锁，因为现有的 `lock3` 程序持有的是共享锁，而不是排占锁。在字节 `40` 到 `50` 的区域上，两种类型的锁都会失败，因为 `lock3` 在该区域上有一个排占锁（`F_WRLOCK`）。

## 第7章：竞争锁

现在我们已经看到了如何测试文件上的现有锁，让我们来看看当两个程序竞争文件同一部分的锁时会发生什么。我们将首先使用 `lock3` 程序对文件锁定，然后使用一个新程序尝试再次锁定。为了完成示例，我们将添加一些解锁的调用。

### 尝试一下——竞争锁

这里有一个程序 `lock5-c`，它尝试锁定已经锁定的文件区域，而不是测试文件不同部分的锁状态。

1. 在包含文件和声明之后，打开一个文件描述符：

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <fcntl.h>

const char *test_file = "tmp/test_lock";

int main() {
    int file_desc;
    struct flock region_to_lock;
    int res;

    file_desc = open(test_file, O_RDWR | O_CREAT, 0666);
    if (!file_desc) {
        fprintf(stderr, "Unable to open %s for read/write\n", test_file);
        exit(EXIT_FAILURE);
    }
```

2. 部分指定了文件的不同区域并尝试对它们进行不同的锁定操作：

```c
    region_to_lock.l_type = F_RDLCK;
    region_to_lock.l_whence = SEEK_SET;
    region_to_lock.l_start = 10;
    region_to_lock.l_len = 5;

    printf("Process %d, trying F_RDLCK, region %d to %d\n", getpid(),
           (int)region_to_lock.l_start, (int)region_to_lock.l_start + region_to_lock.l_len);

    res = fcntl(file_desc, F_SETLK, &region_to_lock);

    if (res == -1) {
        printf("Process %d - failed to lock region\n", getpid());
    } else {
        printf("Process %d - obtained lock region\n", getpid());
    }

    region_to_lock.l_type = F_UNLCK;
    region_to_lock.l_whence = SEEK_SET;
    region_to_lock.l_start = 10;
    region_to_lock.l_len = 5;
```
