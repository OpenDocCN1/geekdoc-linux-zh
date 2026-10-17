
## 11.6.2 使用两个互斥量

```c
#include <stdlib.h>
#include <pthread.h>

#define NHASH 29
#define HASH(id) ((unsigned long)id)%NHASH)
struct foo *fh[NHASH];

pthread_mutex_t hashlock = PTHREAD_MUTEX_INITIALIZER;
struct foo {
    int f_count;
    pthread_mutex_t f_lock;
    int f_id;
    struct foo *f_next; /* protected by hashlock */
    /* ... more stuff here */
};

struct foo *
foo_alloc(int id) /* allocate the object */
{
    struct foo *fp;
    int idx;

    if ((fp = malloc(sizeof(struct foo))) != NULL) {
        fp->f_count = 1;
        fp->f_id = id;
        if (pthread_mutex_init(&fp->f_lock, NULL) != 0) {
            free(fp);
            return(NULL);
        }
        idx = HASH(id);
        pthread_mutex_lock(&hashlock);
        fp->f_next = fh[idx];
        fh[idx] = fp;
        pthread_mutex_lock(&fp->f_lock);
        pthread_mutex_unlock(&hashlock);
        /* continue initialization ... */
        pthread_mutex_unlock(&fp->f_lock);
    }
    return(fp);
}

void
foo_hold(struct foo *fp) /* add a reference to the object */
{
    pthread_mutex_lock(&fp->f_lock);
    fp->f_count++;
    pthread_mutex_unlock(&fp->f_lock);
}

struct foo *
foo_find(int id) /* find an existing object */
{
    struct foo *fp;
    pthread_mutex_lock(&hashlock);
    for (fp = fh[HASH(id)]; fp != NULL; fp = fp->f_next) {
      if (fp->f_id == id) {
        foo_hold(fp);
        break;
      }
    }
    pthread_mutex_unlock(&hashlock);
    return(fp);
}

void foo_rele(struct foo *fp) /* release a reference to the object */
{
  struct foo *tfp;
  int idx;
  pthread_mutex_lock(&fp->f_lock);
  if (fp->f_count == 1) { /* last reference */
    pthread_mutex_unlock(&fp->f_lock);
    pthread_mutex_lock(&hashlock);
    pthread_mutex_unlock(&fp->f_lock);
    /* need to recheck the condition */
    if (fp->f_count != 1) {
      fp->f_count--;
      pthread_mutex_unlock(&fp->f_lock);
      pthread_mutex_unlock(&hashlock);
      return;
    }
    /* remove from list */
    idx = HASH(fp->f_id);
    tfp = fh[idx];
    if (tfp == fp) {
      fh[idx] = fp->f_next;
    } else {
      while (tfp = tfp->f_next != fp) {
        tfp = tfp->f_next;
      }
      tfp->f_next = fp->f_next;
    }
    pthread_mutex_unlock(&hashlock);
    pthread_mutex_unlock(&fp->f_lock);
    pthread_mutex_destroy(&fp->f_lock);
    free(fp);
  } else {
    fp->f_count--;
    pthread_mutex_unlock(&fp->f_lock);
  }
}
```

图 11.1 使用两个互斥量

将图 11.1 与图 11.10 对比，我们看到分配函数现在锁定哈希列表，将新结构体添加到哈希桶，并在解锁哈希列表之前锁定新结构中的互斥量。由于新结构被放置在全局列表中，其他线程在尝试访问新结构时需要锁定该互斥量，直到我们完成初始化。`foo_find` 函数锁定哈希列表并搜索请求结构。如果找到了，增加引用计数并返回结构指针。注意我们通过在锁定哈希列表之前锁定结构的 `f_lock` 来遵循锁顺序。

现在有了两个互斥量，`foo_rele` 函数变得更加复杂。如果是最后一个引用，我们需要解锁结构以便获取哈希锁，因为我们需要将结构从哈希列表中移除。然后重新获取结构的互斥量。由于我们在持有互斥量时可能被阻塞，我们需要重新检查是否还需要释放结构。如果另一个线程在我们遵守锁顺序阻塞时发现了结构并为其添加了引用，我们只需要减少引用计数，解锁一切并返回。

这种锁定方法非常复杂，我们需要重新审视设计。通过使用哈希列表来保护引用计数，可以大大简化问题。图 11.12 反映了这一变化。

```c
#include <stdlib.h>
#include <pthread.h>

#define HASH 29
#define HASH(id) ((unsigned long)id)%HASH

struct foo *fh[HASH];
pthread_mutex_t hashlock = PTHREAD_MUTEX_INITIALIZER;

struct foo {
    int f_count; /* protected by hashlock */
    pthread_mutex_t f_lock;
    int f_id;
    struct foo *f_next; /* protected by hashlock */
    /* ... more stuff here */
};

struct foo *
foo_alloc(int id) /* allocate the object */
{
    struct foo *fp;
    int idx;

    if ((fp = malloc(sizeof(struct foo))) != NULL) {
        fp->f_count = 1;
        fp->f_id = id;
        if (pthread_mutex_init(&fp->f_lock, NULL) != 0) {
            free(fp);
            return(NULL);
        }
        idx = HASH(id);
        pthread_mutex_lock(&hashlock);
        fp->f_next = fh[idx];
        fh[idx] = fp;
        pthread_mutex_lock(&fp->f_lock);
        pthread_mutex_unlock(&hashlock);
        /* ... continue initialization */
        pthread_mutex_unlock(&fp->f_lock);
    }
    return(fp);
}

void
foo_hold(struct foo *fp) /* add a reference to the object */
{
    pthread_mutex_lock(&hashlock);
    fp->f_count++;
    pthread_mutex_unlock(&hashlock);
}

struct foo *
foo_find(int id) /* find an existing object */
{
    struct foo *fp;
    pthread_mutex_lock(&hashlock);
    for (fp = fh[HASH(id)]; fp != NULL; fp = fp->f_next) {
      if (fp->f_id == id) {
        fp->f_count++;
        break;
      }
    }
    pthread_mutex_unlock(&hashlock);
    return(fp);
}

void
foo_rele(struct foo *fp) /* release a reference to the object */
{
    struct foo *tfp;
    int idx;
    pthread_mutex_lock(&hashlock);
    if (--fp->f_count == 0) { /* last reference, remove from list */
      idx = HASH(fp->f_id);
      tfp = fh[idx];
      if (tfp == fp) {
        fh[idx] = fp->f_next;
      } else {
        while (tfp = tfp->f_next != fp) {
          tfp = tfp->f_next;
        }
        tfp->f_next = fp->f_next;
      }
      pthread_mutex_unlock(&hashlock);
      pthread_mutex_lock(&fp->f_lock);
      pthread_mutex_unlock(&fp->f_lock);
      pthread_mutex_destroy(&fp->f_lock);
      free(fp);
    } else {
      pthread_mutex_unlock(&hashlock);
    }
}
```

图 11.12 简化锁

```c
tfp = tfp->f_next;
tfp->f_next = fp->f_next;
pthread_mutex_unlock(&hashlock);
pthread_mutex_destroy(&fp->f_lock);
free(fp);
} else {
    pthread_mutex_unlock(&hashlock);
    }
```

注意图 11.12 中的程序比图 11.11 中的程序简单得多。当我们使用同一个锁来完成这两个目的时，围绕哈希列表和引用计数的锁顺序问题就消失了。多线程软件设计涉及这类权衡。如果你的粒度太粗，会导致大量的线程阻塞在同一个锁上，并发性提升微乎其微。如果粒度太细，你可能会因为过多的锁定开销而遭受性能影响，并导致代码复杂。作为程序员，你需要在……的同时满足你的锁定需求。

### 11.6.3 `pthread_mutex_timedlock` 函数

另一个互斥锁原语允许我们限制线程在尝试获取的互斥锁被锁定时的阻塞时间。`pthread_mutex_timedlock` 函数等同于 `pthread_mutex_lock`，但如果达到了超时值，`pthread_mutex_timedlock` 将返回错误代码 `TIMEDOUT` 而不锁定互斥锁。

```c
#include <pthread.h>
#include <time.h>
int pthread_mutex_timedlock(pthread_mutex_t *restrict mutex,
                           const struct timespec *restrict tspec);

// 返回：成功时为 0，失败时返回错误号
```

超时指定了我们在绝对时间上愿意愿等待多长时间（与相对时间相比，我们指定的是愿意阻塞到时间 X，或者说我们愿意阻塞 Y 秒）。超时由 `timespec` 结构体表示，该结构体用秒和纳秒来描述时间。

#### 示例

在图 11.13 中，我们看到如何使用 `pthread_mutex_timedlock` 来避免无限阻塞。

```c
#include "apue.h"
#include <pthread.h>

int
main(void)
{
    int err;
    struct timespec tout;
    struct tm *tmp;
    char buf[64];
    pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;

    pthread_mutex_lock(&lock);
    printf("mutex is locked\n");
    clock_gettime(CLOCK_REALTIME, &tout);
    tmp = localtime(&tout.tv_sec);
    strftime(buf, sizeof(buf), "%R", tmp);
    printf("the time is %s", buf);
    tout.tv_sec += 10; /* 现在之后 10 秒 */ /* 注意：这可能导致死锁 */
    err = pthread_mutex_timedlock(&lock, &tout);
    clock_gettime(CLOCK_REALTIME, &tout.tv_sec);
    strftime(buf, sizeof(buf), "%R", tmp);
    printf("the time is now %s\n", buf);
    if (err == 0)
        printf("mutex locked again!\n");
    else
        printf("can't lock mutex again: %s\n", strerror(err));
    exit(0);
}
```

图 11.13 使用 `pthread_mutex_timedlock`

`$` `./.out`

```
mutex is locked

current time is 11:41:58 AM

the time is now 11:42:08 AM

can't lock mutex again: Connection timed out
```

该程序故意锁定它已经拥有的互斥锁，以演示 `pthread_mutex_timedlock` 的工作原理。这种策略在实践中是不推荐的，因为它可能导致死锁。

注意，时间被阻塞可能有几个原因：开始时间可能在秒的中间，系统时钟的精度可能不足以支持我们超时的精度，或者调度延迟可能会延长程序继续执行的时间。

`Mac OS X 10.6.8` 不支持 `pthread_mutex_timedlock`，但 `FreeBSD 8.0`、`Linux 3.2.0` 和 `Solaris 10` 支持它，尽管 `Solaris` 将其包含在实时库 `librt` 中。`Solaris 10` 还提供一个使用相对超时的替代函数。

### 11.6.4 读写锁

读写锁与互斥锁类似，不同在于它们允许更高程度的并行性。使用互斥锁时，状态要么锁定要么未锁定，且同一时间只能有一个线程加锁。读写锁有三种状态：读模式锁定、写模式锁定和未解锁。同一时间只有一个线程可以以写模式持有读写锁，但多个线程可以同时以读模式持有读写锁。
