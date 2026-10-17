
每当一个线程想要访问 `$R_j$` 时（j 为 1 或 2）。

然而，假设一个线程 `$p_i$` 需要访问两个资源。很容易想象，`$p_i$` 在两个信号量上嵌套了 `$p_j$`，如图 9.3(a) 所示，而 `$p_j$` 在相同的两个信号量上以相反顺序嵌套了 `$p_i$`，如图 9.3(b) 所示。某些执行序列会导致死锁。假设 `$p_i$` 获得了 `mutex`，与此同时，`$p_j$` 也获取了 `mutex`。在这种情况下，`$p_j$` 持有 `mutex` 并阻塞等待 `mutex_2`，而 `$p_i$` 持有 `mutex` 并阻塞等待 `mutex`。问题的出现是因为，有时只需要使用信号量中的一个，而有时需要使用另一个信号量，而有时两个都应该被使用。不幸的是，不同的程序员可以编写不同的程序以任何顺序获取信号量。

假设可以使用一个简单的抽象 `P` 来一次性获取所有所需的信号量，或者一个都不获取。当任何一个信号量无法获取时，该操作将阻塞调用线程。这种同步 `P` 或 `AND` 同步具有如下形式：

`$P_{simultaneous}(S_1, \dots, S_n)$`

### 图 9.3 嵌套信号量操作

不同的程序员可能会编写程序以不同的顺序请求两个信号量：例如，`p1` 可能会尝试在获取 `mutex2` 之前获取 `mutex1`，而 `p2` 尝试在获取 `mutex1` 之前获取 `mutex2`。这可能导致死锁。

| p1,P Order | p2,P Order |
| :--- | :--- |
| `P(mutex1);` | `P(mutex2);` |
| `P(mutex2);` | `P(mutex1);` |
| `<access R1>;` | `<access R2>;` |
| `V(mutex2);` | `V(mutex1);` |
| `V(mutex1);` | `V(mutex2);` |

同步操作定义如下 [Maekawa, et al., 1987]:

```c
P_simultaneous(S1, ..., Sn) {
  for (i=1; i<=n; i++) {
    P(Si);
  }
}

V_simultaneous(S1, ..., Sn) {
  for (i=1; i<=n; i++) {
    V(Si);
  }
}
```

### 图 9.4 同步信号量

同步（AND 样式）信号量可以使用由调用线程内部执行的信号量来实现。进程阻塞在 `P.sim` 操作上，直到它同时获取 `S` 和 `R`。

```c
int R_num = 0, S_num = 0;
Queue R_wait, S_wait;
Semaphore mutex = 1;
P_sim(PID callingThread, semaphore R, semaphore S) {
L1: P(mutex)
  if(R.val>0&&S.val>0) {
    P(R); P(S);
    V(mutex)
  } else {
    if(R.val==0) {
      R_num++;
      enqueue(callingThread, R_wait);
      V(mutex);
      goto L1;
    } else {
      S_num++;
      enqueue(callingThread, S_wait);
      V(mutex);
      goto L1;
    }
  }
}

V_sim(semaphore R, semaphore S) {
  P(mutex);
  V(R); V(S);
  if(R_num>0) {
    R_num--;
    dequeue(R_wait); // Release a thread
  }
  if(S_num>0) {
    S_num--;
    dequeue(S_wait); // Release a thread
  }
  V(mutex);
}
```

实现这一操作是棘手的，因为它需要一个“第三方”来入队调用线程（线程不能自己让自己释放临界区）。在监视器的讨论中，图 9.4 展示了第三方在 `n=2` 时执行的代码。与本章描述的其他机制一样，同步信号量机制是否被认为是原语，取决于它是如何实现的。如果是使用类似于图 9.4 的技术实现的，那么它是在库运行时实现的抽象。如果是在操作系统中实现的（例如通过使用 `TS` 指令的代码），那么它可以被认为是一种同步原语。

# 使用 AND 同步解决哲学家就餐问题

让我们重新考虑图 9.1 所示的哲学家就餐问题。这里我们使用 `AND` 同步（针对 `n=2`）来解决该问题。

```c
philosopher(int i){
  while (TRUE) {
    // 思考
    // 吃
    P.sim(fork[i], fork[i+1 mod 5]);
    eat();
    V.sim(fork[i], fork[i+1 mod 5]);
  }
}

semaphore fork[5];
fork[0] = fork[1] = fork[2] = fork[3] = fork[4] = 1;
fork(philosopher, 1, 0);
fork(philosopher, 1, 1);
fork(philosopher, 1, 2);
fork(philosopher, 1, 3);
fork(philosopher, 1, 4);
```

# 第九章 高级同步与进程间通信

# 事件

事件（Events）是信号量操作的抽象。它们特别适用于信号量的信号传递（与互斥锁的排除用法不同）。事件可以用于向一组进程通信某些条件的发生情况。如果一个进程需要根据事件的发生来同步其操作，它可以阻塞自己，直到系统中的某个元素引发（发布）该事件。因此，事件类似于信号量，等待事件等同于 `P` 操作，发布事件的发生等同于 `V` 操作。

不同的操作系统中事件有略有不同的变体，尽管它们都建立在相同的基本概念之上。事件由一个称为事件描述符（event descriptor，或事件控制块或其他类似结构）的系统数据结构表示。进程可以等待事件，这导致它们被放置在相应事件描述符的进程列表中。当进程发布事件时，系统使用事件描述符来激活一个或多个被阻塞的进程。

不同系统之间的事件的精确语义有所不同。以下是一组常用的语义：事件名称（或引用）通常定义在全局地址空间中，所有现代进程中的所有线程都可以使用。事件有三个函数：

- `wait(event)` 操作阻塞调用线程，直到另一个线程执行 `signal(event)` 操作。
- `signal(event)` 操作如果有任何线程通过 `wait(event)` 挂起在事件上，则将恰好预留一个等待线程。如果在发出 `signal(event)` 时没有线程在等待，则它会被忽略。
- `queue(event)` 操作返回当前等待某个事件的进程数量。

# 使用通用事件

事件与信号量之间的主要区别是，如果在信号时没有线程在等待，则 `signal()` 操作的结果不会被保存，它的发生将没有任何影响。这些语义的原理是，信号应该代表事件刚刚发生的情况，而不是它在过去某个时候发生的。如果另一个线程在稍后的任意时间检测到这种发生情况（正如被动信号量操作那样），则 `signal()` 和 `wait()` 函数调用之间的因果关系将会丢失。这些语义在 9.2 节的监视器讨论中会被重新考虑。

假设声明了一个事件 `topOfHour`（整点）。那么：

```c
topOfHour.signal();
```

意味着一个进程为 `topOfHour` 事件调用 `signal()` 过程。另一个使用 `topOfHour` 事件的进程可以通过如下调用在事件上阻塞：

```c
topOfHour.wait();
```

现在假设几个进程希望挂起自己直到某个特定时间（例如，精确的整点，如 5:00:00，如第 8 章中的间谍示例所示）。每个进程 `topOfHour.wait()` 会在事件上次发生后（4:00 之后）到下一次发生前（5:00 之前）挂起。这导致所有进程都进入 `topOfHour` 事件的队列。同时，另一个如图 9.5 所示的进程到达了定义的时刻（示例中的整点）。当读取时钟的进程检测到时间正确时，它信号所有入队列的进程并发执行。（当然，调度策略将影响此方案的准确性，尽管其意图是它们在事件发生后尽快运行。）

*在事件上同步*

这里的 `topOfHour` 事件被表示为一个类。进程通过 `wait()` 调用等待事件的发生，在这种情况下，另一个进程轮询时钟以确定何时整点。

```cpp
class Event {
  public:
    void signal();
    void wait();
    int queue();
}
```

![](img/65fa32f8b1eb09c8c688a77a880941bf_378_0.png)

```cpp
shared Event topOfHour;
// 等到整点
// 后继续
// topOfHour.wait();
// 到整点了...
```
