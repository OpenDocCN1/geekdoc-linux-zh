
1. `counter++` 不是原子操作，在多线程环境下直接自增会导致竞态条件（Race Condition）。
2. 线程安全：线程安全指的是程序在多线程环境中正确且可预测地运行的能力。可以通过适当的同步技术并尽可能避免共享资源来实现线程安全。

示例：假设你有一个修改全局变量的函数。为了使其具有线程安全，你可以使用互斥锁来确保同一时间只有一个线程可以访问该变量：

```c
#include <pthread.h>

int global_var = 0;

pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;

void modify_global_var() {

    pthread_mutex_lock(&mutex);

    global_var++;

    pthread_unlock(&mutex);

}

int main() {

    // 创建并运行调用 modify_global_var 的线程

    return 0;

}
```
