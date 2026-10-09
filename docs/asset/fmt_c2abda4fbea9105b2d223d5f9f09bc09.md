
# App8 - C++ 异常、残留、处理

## 构建
```bash
g++ main.cpp -pthread -static -o App8
```

## 代码
```cpp
// main.cpp

// App8 - C++ 异常、残留、处理

// Copyright (c) 2015 - 2022 Software Diagnostics Services. 保留所有。

// Build:

// g++ main.cpp -pthread -static -o App8

#include <string>

#include <unistd.h>

#define def_call(name,x) void name_##x() {

#define def_final(name,x) void name_##x() {

#define def_init(name,size) void name_##y() { int arr[size]; name_##y(); arr=0; }

def_final(work,9)

def_call(work,8,9)

def_call(work,7,8)

def_call(work,6,7)

def_call(work,5,6)

def_call(work,4,5)

def_call(work,3,4)

def_init(work,256)

class Exception

{

    int _code;

    std::string description;

public:

    Exception(int _code, std::string _desc) : _code(_code), description(_desc) {

};

void procB()

{

    throw Exception(5, "Denied");

}

void procNB()

{

    work();

}

void procA()

{

    procB();

}

void procNA()

{

    procNB();

}

void procCH()

{

    try {

        procA();

    } catch (...) {

        sleep(-1);

    }

}

void procNH()

{

    sleep(10);

    procA();

}

void procNE()

{

    try {

        procNA();

    } catch (...) {

        sleep(-1);

    }

}

#define THREAD_DECLARE(num,func) void bar_##num()

{

    func;

}

void foo##num()\

{

    bar_##num();

}

void * thread##num(void *arg)

{

    foo##num();

    return 0;

}

THREAD_DECLARE(one,procNH())

THREAD_DECLARE(two,procNE())

THREAD_DECLARE(three,procCH())

THREAD_DECLARE(four,procNE())

THREAD_DECLARE(five,procNE())

#define THREAD_CREATE(num) {thread_t threadID_##num; pthread_create(&threadID_##num, NULL,thread_##num, NULL);}

int main(int argc, const char * argv[])

{

    THREAD_CREATE(one)

    THREAD_CREATE(two)

    THREAD_CREATE(three)

    THREAD_CREATE(four)

    THREAD_CREATE(five)

    sleep(-1);

    return 0;

}
```

# App9 - 堆内存模式

## 构建
```bash
gcc main.c -pthread -static -o App9
```

## 代码
```c
// main.c

// App9 - 堆内存模式

//

// Copyright (c) 2015 - 2022 Software Diagnostics Services. 保留所有。

// Build:

//

// gcc main.c -pthread -static -o App9

//

#include <stdio.h>

#include <pthread.h>

#include <unistd.h>

#include <string.h>

#include <stdlib.h>

void procD() {

}

typedef void (**PFUNC)();

void procC(int iter) {

    for (int i = 0; i < iter; ++i) {

        char *p = malloc(256);

        strcpy(p, "allocated memory");

        *(PFUNC)(p + 32) = &procC;

    }

}

void procB() {

    procC(250000);

    sleep(300);

    procC(250000);

    sleep(-1);

}

void procA() {

    procC(5000);

    sleep(300);

    procB();

}

#define THREAD_DECLARE(num,func) void bar##num()

{

    func;

}

void foo##num()\

{

    bar##num();

}

void * thread##num(void *arg)

{

    foo##num();

    return 0;

}

THREAD_DECLARE(one,sleep(-1))

THREAD_DECLARE(two,procA())

THREAD_DECLARE(three,sleep(-1))

THREAD_DECLARE(four,sleep(-1))

THREAD_DECLARE(five,sleep(-1))

#define THREAD_CREATE(num) {thread_t threadID_##num; pthread_create(&threadID_##num, NULL,thread_##num, NULL);}

int main(int argc, const char * argv[])

{

    THREAD_CREATE(one)

    THREAD_CREATE(two)

    THREAD_CREATE(three)

    THREAD_CREATE(four)

    THREAD_CREATE(five)

    sleep(-1);

    return 0;

}
```

# App10 - 堆损坏、堆竞争、关键区域、等待链、自诊断模式

## 构建
```bash
gcc main.c -pthread -static -o App10
```

## 代码
```c
// main.c

// App10 - 堆损坏、堆竞争、关键区域、等待链、自诊断模式

// Copyright (c) 2015 - 2022 Software Diagnostics Services. 保留所有。

// Build:

//

//     gcc main.c -pthread -static -o App10

#include <stdio.h>

#include <pthread.h>

#include <unistd.h>

#include <string.h>

#include <stdlib.h>

#define ARR_SIZE 10000

char *pAllocBuf[ARR_SIZE] = {0};

void proc() {

    while (1) {

        int idx = rand()%ARR_SIZE;

        int malloc_size = rand()%ARR_SIZE;

        if (pAllocBuf[idx]) {

            free(pAllocBuf[idx]);

            pAllocBuf[idx] = 0;

        }

        pAllocBuf[idx] = malloc(malloc_size);

    }

}

#define THREAD_DECLARE(num,func) void bar_##num()

{

    func();

}

void foo_##num()\

{

    bar_##num();

}

void *thread_##num(void *arg)

{

    foo_##num();

    return 0;

}

THREAD_DECLARE(one,proc())

THREAD_DECLARE(two,proc())

THREAD_DECLARE(three,proc())

THREAD_DECLARE(four,proc())

THREAD_DECLARE(five,proc())
```

# App11 - 等锁链、死锁、已处理异常模式

## 构建
```bash
# 构建 (App11):
g++ main.cpp -pthread -static -o App11

# 构建 (App12):
g++ main.cpp -g -pthread -static -o App12

cp App12 App12.debug

objcopy strip-debug App12
```

## 代码
```cpp
//
// main.c
// App11 - 等锁链、死锁、已处理异常模式
// Copyright (c) 2015 - 2022 Software Diagnostics Services. All rights reserved.
//
// 构建 (App11):
//
g++ main.cpp -pthread -static -o App11
//
// 构建 (App12):
//
g++ main.cpp -g -pthread -static -o App12
//
cp App12 App12.debug
//
objcopy strip-debug App12

#include <stdio.h>
#include <pthread.h>
#include <unistd.h>
#include <string.h>
#include <stdlib.h>

thread_mutex_t mutexA, mutexB;

void procC()
{
    throw 0;
}

void procA()
{
    try
    {
        thread_mutex_lock(&mutexA);
        procC();
        thread_mutex_unlock(&mutexA);
    } catch(...)
    {
        sleep(20);
        thread_mutex_lock(&mutexB);
        thread_mutex_unlock(&mutexB);
    }
}

void procB()
{
    thread_mutex_lock(&mutexB);
    thread_mutex_lock(&mutexA);
    sleep(30);
    thread_mutex_unlock(&mutexA);
    thread_mutex_unlock(&mutexB);
}
```

```cpp
#define THREAD_DECLARE(num,func) void bar_##num()\n{\nfunc()\n}\nvoid foo##num()\n{\nbar_##num();\n}\nvoid * thread##num (void *arg)\n{\nfoo##num();\n\nreturn 0;\n}
```

```cpp
THREAD_DECLARE(one,sleep(-1))
THREAD_DECLARE(two,procA)
THREAD_DECLARE(three,sleep(-1))
THREAD_DECLARE(four,procB())
THREAD_DECLARE(five,sleep(-1))
```

```cpp
#define THREAD_CREATE(num) {pthread_t threadID_##num; pthread_create(&threadID_##num, NULL, thread_##num, NULL);}

int main(int argc, const char *argv[])
{
    pthread_mutex_init(&mutexA, NULL);
    pthread_mutex_init(&mutexB, NULL);

    THREAD_CREATE(one)
    THREAD_CREATE(two)
    sleep(10);
    THREAD_CREATE(three)
    THREAD_CREATE(four)
    THREAD_CREATE(five)

    sleep(-1);
    return 0;
}
```

# App12 - 内核空间中的 NULL 指针（数据）内存分析模式

## 代码
```cpp
// mod_a.c
// 内核空间中的 NULL 指针（数据）内存分析模式
//
// Copyright (c) 2022 Software Diagnostics Services. All rights reserved.
//
#include <linux/module.h>

void foo(void);
void bar(void);

int init_module(void)
{
    foo();
    return 0;
}

void bar(void)
{
    int *pi = NULL;
    *pi = 1;
}

void foo(void)
{
    bar();
}

MODULE_LICENSE("GPL");
```

# K3

## 代码
```cpp
// mod_b.c
// 内核空间中的空指针（代码）内存分析模式
//
// Copyright (c) 2022 Software Diagnostics Services. All rights reserved.
//
#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/kthread.h>
#include <linux/sched.h>
#include <linux/delay.h>
```

```cpp
void foo(void);

int kthread_f(void *arg)
{
    msleep(10000);

    foo();

    return 0;
}
```

```cpp
int init_module(void)
{
    struct task_struct *ts;

    ts = kthread_run(kthread_f, NULL, "mod_b thread");

    if (IS_ERR(ts))
    {
        return PTR_ERR(ts);
    }

    return 0;
}
```

```cpp
// foo.c
// MODULE_LICENSE("GPL");

#include <linux/module.h>

void bar(void);

void foo(void)
{
    bar();
}

// bar.c
// MODULE_LICENSE("GPL");

#include <linux/module.h>
#include <linux/kernel.h>

void bar(void)
{
    int (*pf)(void) = NULL;
    pf();
}

MODULE_LICENSE("GPL");
```

# App13 - 内核空间中的尖峰线程（Spiking Thread）分析模式

## 代码
```cpp
// mod_c.c
// 内核空间中的尖峰线程（Spiking Thread）分析模式
//
// Copyright (c) 2022 Software Diagnostics Services. All rights reserved.
//
#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/kthread.h>
#include <linux/sched.h>
#include <linux/delay.h>
```

```cpp
void foo(void);

int kthread_f(void *arg)
{
    msleep(10000);

    foo();

    return 0;
}

int init_module(void)
{
    struct task_struct *ts;

    ts = kthread_run(kthread_f, NULL, "mod_c thread");

    if (IS_ERR(ts))
    {
        return PTR_ERR(ts);
    }

    return 0;
}
```

```cpp
// foo.c
// MODULE_LICENSE("GPL");

#include <linux/module.h>

void foo(void)
{
    while (1);
}
MODULE_LICENSE("GPL");
```
