
# 无锁算法 321

## 第 8 章 手编码同步与共享

对于当前的代码有几点说明。第一，环形缓冲区有 16 个条目，虽然这对于单个生产者-消费者对可能足够，但随着线程数量的增加，这可能无法维持。第二也是更重要的一点，代码现在会产生死锁。假设环形缓冲区是空的，消费者线程获取了锁并等待缓冲区出现某些内容。生产者最终到达，但没有锁来向缓冲区中添加任何内容。两个线程最终都在自旋，等待一个永远不会发生的事件。

针对该问题的特定情况有两种解决方案。第一种方案可能是最好的，即提供两个锁——一个用于等待向缓冲区添加元素的线程，另一个用于等待从列表中移除项的线程。在这种情况下，这种解决方案将问题简化为之前描述的系统中仅存在线程的情况。一个锁确保一次只有一个生产者可以访问环形缓冲区。其他生产者和消费者线程不会相互干扰并破坏正确性。

该解决方案依赖代码的原始语义，在存在两个线程的情况下提供线程安全的版本。为了说明目的，我们如何修改代码使得只需要一个锁。

实现这一点的方法是将关键区域放在另一个循环内部，该循环重复执行直到关键区域成功执行。这需要修改 `addtobuffer()` 和 `removebuffer()` 例程，使它们不再在关键区域内部循环，而是快速返回成功或失败。`8.24` 显示了修改后的代码，移除了关键区域内部的循环。

### 列表 8.24 使用互斥确保对环形缓冲区的独占访问

```c
void addtobuffer( int value )
{
    int success = 0;
    while(! success)
    {
        spinlock( &lock );
        if ( buffer[ next(addhere) ] == 0 )
        {
            buffer[addhere] = value;
            addhere = next(addhere);
            success = 1;
        }
        free_spinlock( &lock );
    }
}
```

```c
int removebuffer()
{
    int value;
    int success = 0;
    while(! success)
    {
        spinlock( &lock );
        if ( ( value = buffer[removehere] ) != 0 )
        {
            buffer[removehere] = 0;
            removehere = next(removehere);
            success = 1;
        }
        free_spinlock( &lock );
    }
    return value;
}
```

### 列表 8.25 避免缓存行的无效失效

```c
void addtobuffer( int value )
{
    int success = 0;
    while(! success)
    {
        spinlock( &lock );
        if ( buffer[ next(addhere) ] == 0 )
        {
            buffer[addhere] = value;
            addhere = next(addhere);
            success = 1;
        }
        free_spinlock( &lock );
    }
}
```

```c
int removebuffer()
{
    int value;
    int success = 0;
    while(! success)
    {
        spinlock( &lock );
        if ( ( value = buffer[removehere] ) != 0 )
        {
            buffer[removehere] = 0;
            removehere = next(removehere);
            success = 1;
        }
        free_spinlock( &lock );
    }
    return value;
}
```

## 324 第 8 章 手动编码的同步与共享

### 列表 8.26 使用 `try_spinlock()` 避免缓存行的无效失效

```c
int try_spinlock(volatile int* lock)
{
    if (CAS(lock, 0, 1) == 1) { return 0; }
    else
    {
        acquire_memory_barrier();
        return 1;
    }
}
void addtobuffer(int value)
{
    int success = 0;
    while (!success)
    {
        if (buffer[next(addhere)] == 0)
        {
            if (try_spinlock(&lock))
            {
                if (buffer[next(addhere)] == 0)
                {
                    buffer[addhere] = value;
                    addhere = next(addhere);
                    success = 1;
                }
                free_spinlock(&lock);
            }
        }
    }
}
```

```c
void removefrombuffer()
{
    int value;
    int success = 0;
```
