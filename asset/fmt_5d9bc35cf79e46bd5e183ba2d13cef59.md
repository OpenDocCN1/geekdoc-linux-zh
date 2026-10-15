
互斥锁的属性可以通过以下机制设置：

- 互斥锁类型。这可以是普通互斥锁、在多次尝试锁定时检测错误的互斥锁，或者可以多次锁定的递归互斥锁。
- 当另一个线程等待互斥锁时的协议。这可以是默认的不改变优先级、持有互斥锁的线程继承等待它的高优先级线程的优先级，或者线程获取其持有互斥锁中的最高优先级。
- 互斥锁的优先级上限。这是低优先级线程在持有互斥锁时提升的优先级。

控制优先级的属性（`PTHREAD_PRIO_INHERIT` 和 `PTHREAD_PRIO_CEILING`）旨在避免高优先级线程等待低优先级线程释放互斥锁时的优先级反转问题。

# 线程间的数据共享

## 使用自旋锁

自旋锁和互斥锁的关键区别在于，自旋锁在获取锁之前会在密循环中不断旋转并消耗处理器资源。互斥锁在无法获取锁时会立即让线程睡眠，或者自适应互斥锁会在睡眠前短时间旋转等待锁释放。

自旋锁的接口与互斥锁的接口非常相似。调用 `pthread_spin_init()` 将初始化自旋锁。自旋锁可以在进程之间创建，也可以为创建它的进程创建。进程私有的自旋锁通过向调用 `pthread_spin_init()` 传递 `PTHREAD_PROCESS_PRIVATE` 值创建，传递 `PTHREAD_PROCESS_SHARED` 值则创建一个可以在进程间共享的自旋锁。

创建锁的进程中的多个线程始终能够访问它。然而，如果自旋锁被创建为进程私有，则如果被其他进程使用，锁的行为是未定义的。默认情况下，锁对于创建进程是私有的。

调用 `pthread_spin_lock()` 将旋转直到获取锁，最后调用 `pthread_spin_unlock()` 将释放锁。列表 5.22 演示了使用自旋锁允许在自旋锁控制下访问局部变量；但在该示例中，变量并没有在线程间共享，因此实际上不需要使用任何锁定。

### 列表 5.22 使用自旋锁保护变量访问的代码

```c
#include <thread.h>
```

```c
pthread_spinlock_t lock;

void lockandunlock()
{
    int i = 10000;
    while ( i>0 )
    {
        pthread_spin_lock(& lock );
        i--;
        pthread_spin_unlock(& lock );
    }
}

int main()
{
    pthread_spin_init(&lock, PTHREAD_PROCESS_PRIVATE);
    lockandunlock();
    pthread_spin_destroy(&lock);
}
```

如果将代码修改为创建一个在多个进程共享的自旋锁，则应该只由进程来初始化和销毁自旋锁。列表 5.23 所示的修改将创建一个可以在进程间共享的自旋锁。

#### 列表 5.23 创建可以在进程间共享的自旋锁

```c
int main()
{
    pthread_spin_init(&lock, PTHREAD_PROCESS_SHARED);
    lockandunlock();
    pthread_spin_destroy(&lock);
}
```

此外，调用 `pthread_spin_trylock()` 将尝试获取锁，但它会立即返回是否成功获取锁。由于自旋会使用处理器资源，尝试获取锁并在失败时，在重复测试之前完成某些其他任务，可能会更有用。列表 5.24 显示了对前面的代码进行修改，以使用 `pthread_spin_trylock()` 并记录线程未能获取锁的次数。

### 列表 5.24 统计自旋锁获取失败的次数

```c
void lockandunlock()
{
    int i = 0;
    int count = 0;
    while ( i == 0 ) {
        if ( pthread_spin_trylock(&lock) ) {
            i++;
            pthread_spin_unlock(&lock);
        } else {
            count++;
        }
    }
    printf("Failed tries = %i\n", count);
}
```

## 读写锁

读写锁允许多个线程同时读取资源，但在任何时间只允许单写写入者更新该资源。它们与互斥锁具有相似的初始化和销毁语法，它们接受一组属性，并且可以通过调用 `pthread_rwlock_init()` 或通过赋值值 `PTHREAD_RWLOCK_INITIALIZER` 进行静态初始化来实现。列表 5.25 显示了这两种方法。

### 列表 5.25 初始化读写锁

```c
pthread_rwlock_t lock1, lock2;

...
pthread_rwlock_init(&lock1, 0);
lock2 = PTHREAD_RWLOCK_INITIALIZER;
...
```

如果传递给初始化例程的属性为零，则锁将以默认属性初始化，即对创建它的进程私有。要创建一个在进程间共享的读写锁，必须创建并使用一组属性。调用 `pthread_rwlockattr_init()` 初始化属性，而调用 `pthread_rwlockattr_setpshared()` 将共享属性设置为所需的值。然后可以将这组属性传递给 `pthread_rwlock_init()`，以为正在创建的读写锁设置属性。列表 5.26 演示了这一点。

### 列表 5.26 创建可以在进程间共享的读写锁

```c
pthread_rwlockattr_t attributes;
pthread_rwlock_t lock;

...
  pthread_rwlockattr_init(&attr);
  pthread_rwlockattr_setpshared(&attr, PTHREAD_PROCESS_SHARED);
  pthread_rwlock_init(&lock, &attr);
  pthread_rwlockattr_destroy(&attr);
...
  pthread_rwlock_destroy(&lock);
```

一旦锁被创建，它就不再引用属性，因此这些属性可以重用于不同的锁或销毁。销毁属性的调用是 `pthread_rwlockattr_destroy()`。读写锁消耗的资源通过调用 `pthread_rwlock_destroy()` 释放。

读写锁的接口比互斥锁更复杂，因为它们可以为了读取或写入而被锁定。因此，有两对锁和解锁调用：用于读取的 `pthread_rwlock_rdlock()` 和 `pthread_rwlock_rdunlock()` 对，以及用于写入的 `pthread_rwlock_wrlock()` 和 `pthread_rwlock_wunlock()` 对。列表 5.27 显示了如何使用读写锁来访问共享资源。

### 列表 5.27 使用读写锁保护共享资源的访问

```c
int readMatrix(int x, int y)
{
  int result;
  pthread_rwlock_rdlock(&lock);
  result = matrix[x,y];
  pthread_rwlock_rdunlock(&lock);
  return result;
}
```

```c
void updateMatrix(int x, int y, int value)
{
  pthread_rwlock_wrlock(&lock);
  matrix[x,y] = value;
  pthread_rwlock_wunlock(&lock);
}
```

在这个短代码段中，读写锁是不必要的，因为对对齐整数变量的加载或存储访问是原子的。如果更新和读取的是需要多次写入的结构，那么锁将是关重要的。

获取锁的调用的行为是线程阻塞直到获取锁。然而，也有尝试获取锁的调用。这些调用会立即返回或在没有获取锁的情况下返回。尝试获取锁的调用是 `pthread_rwlock_trylock()`，而作为写入者获取锁的调用是 `pthread_rwlock_wlock()`。列表 5.28 显示了这些调用的示例。

### 列表 5.28 仅在获取读写锁时更新共享值

```c
void Update(int value)
{
```
