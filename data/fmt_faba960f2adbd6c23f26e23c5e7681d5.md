
`mythread.join();`

这两个标准都提议支持原子操作和内存排序。在 C 中，原子操作通过提供原子类型以及可以在这些类型上执行的操作来支持。列表 10.10 中的代码演示了如何增加原子变量。

# 列表 10.10 C 提案中的原子递增

```cpp
#include <atomic.h>

int count()
{
    static atomic_int value = 0;
    atomic_fetch_add(&value, 1);
    printf("Counter=%d\n", value);
}
```

C++ 将原子类型定义为结构体并提供了访问它们的方法。列表 10.11 显示了等效 C++ 代码。

# 列表 10.11 C++ 提案中的原子递增

```cpp
#include <atomic>
#include <iostream>

int count()
{
    static atomic_int value = 0;
    value += 1;
    printf("Counter:%i\n", value);
}
```

最后一个标准化领域处理互斥锁（mutex）和条件变量。列表 10.12 中的代码演示了在提议的 C 标准下，如何创建互斥锁并使用它为共享变量提供原子访问。`mutex_init()` 调用接收一个参数来描述所需的互斥锁类型，这为互斥锁提供了不同的运行时行为，例如设置超时。

# 列表 10.12 使用 C 中的互斥锁保护共享变量

```c
#include <threads.h>
#include <stdio.h>

int counter = 0;
mtx_t mutex;

int* work(void *)
{
    mtx_lock(&mutex);
    counter++;
    printf("Counter = %i\n", counter);
    mtx_unlock(&mutex);
    return 0;
}

int main()
{
    thrd_t thread;
    mtx_init(&mutex, mtx_plain);
    thrd_create(&thread, work, 0);
    thrd_join(&thread, 0);
    mtx_destroy(&mutex);
}
```

C++ 提议的标准实现了一个不同类型互斥锁的类层次。列表 10.13 显示了保护共享变量的等效代码。

# 列表 10.13 在 C++ 中使用互斥锁对象保护共享变量

```cpp
#include <thread>
#include <iostream>

int counter = 0;
std::mutex mymutex;

struct work
{
    void operator()
    {
        mymutex.lock();
        std::cout << " Counter " << counter << "\n";
        mymutex.unlock();
    }
};

int main()
{
    std::thread mythread{ work() };
    mythread.join();
}
```

## 微软的 C++/CLI

Visual Studio 支持 C++/通用语言基础设施 (CLI)，这是一种派自 C++ 的语言，运行在 .NET 通用语言运行时 (CLR) 上。与所有托管语言一样，它被编译为字节码，然后在虚拟机上运行。该语言提供了一组用于同步和线程的对象。

列表 10.14 中的代码阐明了主线程如何创建子线程。主线程打印一组输出，子线程打印另一组。主线程在退出前等待按键按下。

- 列表 10.14 在 C++/CLI 中创建子线程

```cpp
using namespace System;
using namespace System::Threading;

void work()
{
    Console::WriteLine(L"Work Thread" );
}

int main(Array<String> args)
{
    Thread* thread = new Thread(new ThreadStart(&work) );
    thread->Start();
    Console::WriteLine(L"Main Thread" );
    Console::ReadKey();
    return 0;
}
```

# 第 10 章 其他并行化技术

`Thread` 对象是线程的抽象。要产生一个运行的线程，需要创建一个对象并通过调用其 `Start()` 方法来启动。`gcnew` 函数在垃圾回收堆上创建一个托管对象并返回其句柄。持有特定类型句柄的变量用脱帽符号 (`^`) 字符表示。线程需要一个要执行的例程地址。这通过 `ThreadStart` 对象提供，该对象是用所需例程的地址创建的。

如前所述，该语言提供了熟悉的同步原语。例如，我们可以使用互斥锁来确保主线程在子线程之前打印其输出内容。

代码随后变得更加复杂，因为无法使用托管全局变量。一种方法是将子线程执行的代码转换为对象中的一个方法。10.15 定义了一个 `ThreadWork` 对象，它包含一个 `Mutex` 对象的句柄；该句柄在对象创建时设置。

# 10.15 使用互斥锁确保顺序

```cpp
using namespace System;
using namespace System::Threading;

public class ThreadWork
{
private:
    Mutex^ mymutex;
public:
    ThreadWork(Mutex^ m )
    {
        mymutex = m;
    }
    void work()
    {
        mymutex->WaitOne();
        Console::WriteLine("Child thread");
        mymutex->ReleaseMutex();
    }
};

int main(array<String> ^ args)
{
    Mutex^ mymutex = gcnew Mutex();
    ThreadWork^ T = gcnew ThreadWork(mutex);
    mymutex->WaitOne();
    Thread^ mythread = new Thread(new ThreadStart(T, &ThreadWork::work));
    mythread->Start();
    Console::WriteLine("Main Thread");
    mymutex->ReleaseMutex();
    mythread->Join();
    Console::ReadKey();
    return 0;
}
```

互斥锁通过调用 `WaitOne()` 方法获取，通过调用 `ReleaseMutex()` 方法释放。代码首先创建互斥锁对象，并将其句柄传递给 `ThreadWork` 对象。主线程通过调用 `WaitOne()` 获取互斥锁。这将阻止子线程在主线程打印其输出之前退出。
一旦主线程在控制台打印了输出，它就会释放互斥锁并调用 `Thread` 的 `Join()` 方法等待子线程完成。

## 替代语言

到本章为止描述的语言都是标准 C/C++ 的扩展。在某些方面，C 和 C++ 并不是并行化的理想语言。一个特别的问题是指针的广泛使用，这使得很难证明内存访问没有别名。
由于这种情况，人们设计了其他编程语言，它们专门用于开发并行应用程序，或者不受 C/C++ 这些问题的影响。例如，最初由太阳系统开发的 Fortress 拥有一种默认循环并行的模型。

这两个函数的执行所需时间大约相同，因此并行执行它们是有意义的。列表 10.20 显示了实现这一点的代码。

## Listing 10.20 独立并行程序

```
import Control.Parallel

main = print (parallel 2 20)

fib 0 = 0
fib 1 = 1
n = fib (n-1) + fib (n-2)

fib 0 = -1
fib 1 = 1
n = fib (n-1) + fib (n-2)

parallel a b
  let x = fib a
      y = fib b
  in x `par` `seq` (x+y)
```
