

```
/* Time to set up the memory maps */
if ( ( source_addr = mmap(NULL, filesize , PROT_READ,
		MAP_SHARED, in_fd, 0) ) == (void *) -1 )
	die( "Error mapping file ", argv[1]);

if ( ( dest_addr = mmap(NULL, filesize , PROT_WRITE,
		MAP_SHARED, out_fd, 0) ) == (void *) -1 )
	die( "Error mapping file ", argv[2]);

/* copy the input to output by doing a memcpy */
memcpy( dest_addr, source_addr, filesize );

/* unmap the files */
munmap(source_addr, filesize);
munmap(dest_addr, filesize);

/* close the files */
close(in_fd);
close(out_fd);

return 0;
}
```

## 2.9 返回到 who

我们之前的 who 实现一次读取一条 utmp 记录。每次读取都需要一次系统调用，即使单个 utmp 记录非常小，而且数量很多。我们现在知道这是低效的。就像 cp 命令可以通过增大缓冲区大小受益一样，who 也可以。我们将对其进行修改，使其一次读取多条 utmp 记录并将它们存储在内部数组中。我们现在已经到了第 5 个版本，这个版本将被称为 who5。

### 2.9.1 用户定义的缓冲

当进程在一次输入操作中请求的数据多于它能处理的数据，并将多余的数据存储在其自己的内存空间中直到准备好使用时，就称该进程执行了输入缓冲。输入缓冲是一种减少输入操作成本的方法，因为它减少了进程花费在系统调用上的时间。

为了使 who 执行输入缓冲，它需要一个地方来存储多余的记录直到准备好使用它们。逻辑上的位置是在一个记录数组中。例如，如果它一次读取 20 条记录，那么这 20 条记录将被放入其内部数组中。它可以维护一个指向当前记录的指针。每次需要检查新记录时，它都会检查当前记录指针是否已超出数组边界。如果超出，它会尝试从 utmp 文件中获取下一批 20 条记录并用它们填充数组。如果文件中没有剩余记录，它就无法获取新记录，并且已完成。否则，它会尽可能多地获取，最多 20 条，然后从数组中获取当前记录并推进当前记录指针。

输入缓冲的逻辑被封装到一个用于与 utmp 记录交互的独立库例程中，称为 utmp_utils.c。该库的接口由三个函数组成：open_utmp()、next_utmp() 和 close_utmp()。open_utmp() 函数打开给定的 utmp 文件，next_utmp() 函数提供下一条记录，如果缓冲区为空则从文件中读取新块，close_utmp() 关闭文件。接口如下。

```
Listing utmp_utils.h
typedef struct utmp utmp_record;

int open_utmp( char * utmp_file );
// opens the given utmp_file for buffered reading
// returns: a valid file descriptor on success
//
//          -1 on error

utmp_record *next_utmp();
// returns: a pointer to the next utmp record from the
//          opened file and advances to the next record
//
//          NULL if no more records are in the file

void close_utmp();
// closes the utmp file and frees the file descriptor
```

该库的实现如下。它使用全局变量（静态变量）以便函数之间可以通信。我们不想将它们作为参数传递，因为那样客户端代码也必须这样做，从而破坏抽象。如果这用 C++ 编写，这个库将是一个类，而全局变量将是成员变量。

```
Listing utmp_utils.c
#include <stdio.h>
#include <fcntl.h>
#include <sys/types.h>
#include <utmp.h>

#define NUM_RECORDS          20
#define NULL_UTMP_RECORD_PTR ((utmp_record *) NULL)
#define SIZE_OF_UTMP_RECORD  (sizeof(utmp_record))
#define BUFSIZE             (NUM_RECORDS * SIZE_OF_UTMP_RECORD)

static char utmpbuf[BUFSIZE];   // buffer of records
static int  number_of_recs_in_buffer; // num records in buffer
static int  current_record;     // next rec to read
static int  fd_utmp = -1;       // file descriptor for utmp file
```

