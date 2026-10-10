
```c
    printf("I read from location\n");

    exit(EXIT_SUCCESS);

}
```

输出为：

```bash
$ ./memory5b

Segmentation fault (core dumped)
```

## 工作原理

这一次我们尝试直接从位置零读取。这次我们和内核之间没有 GNU libc 库，我们的程序被终止了。你应该注意，某些版本的 UNIX 允许从位置零读取，但 Linux 不允许。

## 释放内存

到为止，我们一直在简单地分配内存，然后希望在程序结束时我们使用的内存没有丢失。幸运的是，Linux 内存管理系统非常有能力可靠地确保在程序结束时将内存返回系统。然而，大多数程序并不仅仅是想分配一些内存、使用一段时间然后释放。更常见的用法是根据需要动态使用内存。

基于动态使用内存的程序在不再需要时需要释放它。这是通过使用 `free()` 函数实现的，它接受指向内存块的指针。

## 试一——释放内存

这个程序展示了如何分配内存并在不再需要时释放它，`memory6.c`：

```c
#include <stdlib.h>

#define ONE_K (1024)

int main()

{

    char *some_memory;

    some_memory = (char *)malloc(ONE_K);

    if (some_memory == NULL) exit(EXIT_FAILURE);

    // ... 使用内存 ...

    free(some_memory);

    exit(EXIT_SUCCESS);

}
```

## 工作原理

`free()` 函数告诉内存管理器某块内存不再需要。管理器随后可以将其标记为可用以供未来分配。重要的是不要在释放后使用该指针，这会导致未定义行为。

## 其他分配函数

除了 `malloc` 之外，还有其他分配内存的函数。常用的 `calloc` 和 `realloc`。

| 函数 | 描述 |
| :--- | :--- |
| `calloc(n, size)` | 为 `n` 个 `size` 大小的元素分配内存并初始化零。 |
| `realloc(ptr, size)` | 将内存内存块调整为 `size` 字节。 |

`calloc` 在你需要将分配的内存初始化零时有用。`realloc` 在你需要扩大或缩小现有内存块时有用。如果 `realloc` 失败，它返回 NULL 且原始块保持不变。

## 文件锁

文件锁对于多用户、多任务系统非常重要。程序经常需要共享数据（通常通过文件），对于这些程序来说，拥有某种控制文件的方法非常重要。这样可以安全地更新文件，或者第二个程序可以停止读取另一个程序正在写入的瞬态文件。

Linux 提供了几种可以用于文件锁的功能。最简单的方法是一种原子化创建锁文件的技术，这样在创建锁期间不会发生其他事情。这为程序提供了一种创建唯一且不会被另一个程序同时创建的方法。

第二种方法更高级；它允许程序对文件的部分区域进行独占访问。实现这种形式的锁有两种方法。我们将详细介绍一种，因为另一种非常相似——只是接口略有不同。

### 创建锁文件

许多应用程序只需要为资源创建一个锁文件。其他程序可以通过检查该文件来判断是否允许访问资源。

通常这些锁文件位于特殊位置，名称与控制的资源有关。例如，当调制解调器在使用中时，Linux 会创建一个锁文件，通常位于 `/usr/spool` 或 `/var/spool` 目录。

记住，锁文件仅作为指示器；程序需要协作使用它们。它们被称为锁，相对于强制锁（后者由系统强制执行锁行为）。

为了创建一个作为锁指示器的文件，我们使用了在 `fcntl.h` 中定义的 `open` 系统调用，我们在之前的章节中遇到过这个调用，并配合了 `O_CREATE` 和 `O_EXCL` 标志。这允许我们检查文件是否已经存在，并在单个原子操作中创建它。

## 尝试一一看——创建锁文件

让我们通过 `lock1.c` 来观察它的工作：

```c
#include <unistd.h>

#include <stdlib.h>

#include <stdio.h>

#include <fcntl.h>

#include <errno.h>

int main() {

    int file_desc;

    int save_errno;

    file_desc = open("/tmp/LCK.test", O_RDWR | O_CREATE | O_EXCL, 0444);

    if (file_desc == -1) {

        save_errno = errno;

        printf("Open failed with error %d\n", save_errno);

    } else {

        printf("Open succeeded\n");

    }

    exit(EXIT_SUCCESS);

}
```

当我们第一次运行程序时，输出是：

- lock1
Open succeeded

但当我们下次尝试时，我们得到了：

- lock1
Open failed with error 17

## 工作原理

该程序调用 `open` 来创建文件 `/tmp/LCK.test`，使用了 `O_CREATE` 和 `O_EXCL` 标志。当我们第一次运行程序时，文件不存在，因此 `open` 调用成功。后续对程序的多次调用会失败，因为文件已经存在了。为了让程序再次成功，我们必须删除该锁文件。

至少在 Linux 系统上，错误 17 指的是 `EEXIST`，这是一个表示文件已存在的错误。错误码定义在 `errno.h` 头文件中，或者更常见的是定义在包含它的头文件中。在这种情况下，该定义（实际上在 `/usr/include/asm/errno.h` 中）读取内容如下：

```c
#define EEXIST 17 /* File exists */
```

## 第 7 章

这是 `open(O_CREAT | O_EXCL)` 失败的一个合适错误。

如果一个程序只需要在执行的短时间内独占某个资源（通常称为*临界区*），它应该在进入临界区之前创建锁文件，并在退出临界区后使用 `unlink` 将其删除。

我们可以通过编写一个简单的程序并同时运行它的副本，来演示程序如何与这种锁定机制协作。我们将使用在第 4 章中见过的 `getpid` 调用；它返回进程标识，这是每个执行程序的唯一数字。

## 尝试一一看——协作锁文件

1. 这里是我们测试程序的源码：`lock2.c`：

```c
#include <unistd.h>

#include <stdlib.h>

#include <stdio.h>

#include <fcntl.h>

#include <errno.h>

const char *lock_file = "/tmp/LCK.test2";

int main() {

    int file_desc;

    int tries = 10;

    while (tries--) {

        file_desc = open(lock_file, O_RDWR | O_CREAT | O_EXCL, 0444);

        if (file_desc == -1) {

            printf("%d - Lock already present\n", getpid());

            sleep(3);

        }

    } else {

    }

}
```

2. 临界区从这里开始：

```c
printf("%d - I have exclusive access\n", getpid());

sleep(1);

(void)close(file_desc);
```

3. 在这里结束：

```c
sleep(2);

}

exit(EXIT_SUCCESS);
```

要运行该程序，我们应该先使用这个命令确保锁文件不存在：

```bash
$ rm -f /tmp/LCK.test2
```

然后我们使用这个命令运行两个程序的副本：

```bash
$ ./lock2 & ./lock2
```

这会在后台启动一个 `lock2` 副本，并在前台运行第二个副本。这是我们得到的输出：

```
1284 - I have exclusive access

1283 - Lock already present

1283 - I have exclusive access

1284 - Lock already present

1284 - I have exclusive access

1283 - Lock already present

1284 - I have exclusive access

1284 - Lock already present

1283 - I have exclusive access
```
