
此图中的代码仅显示了设备驱动程序软件和硬件控制器的同步行为，而不是设备驱动程序和控制器的所有功能行为。例如，如果该方案是实现的基础，它会导致调用进程阻塞——而实际实现并不会这样做。在模型中，`busy` 和 `done` 初始化为 0，因此当设备控制器启动时，它会进入一个无限循环，通过测试 `busy` 标志来与软件同步其操作。如果 `busy` 为 0（初始状态），控制器将阻塞并等待驱动程序的信号。应用程序每当想要执行 I/O 操作时就会调用驱动程序。在准备操作后（例如，通过设置控制器寄存器、设备状态表条目等），它通过对 `busy` 信号量执行 `V` 操作来向硬件发送信号。`V` 操作解锁控制器，并在 `done` 信号量上阻塞驱动程序。当设备完成操作时，它通过对 `done` 标志执行 `V` 操作向驱动程序发送信号。

# 有界缓冲区（生产者-消费者）问题

有界缓冲区问题经常出现在并发软件中。在图 5.11 中，我们看到了“纯净循环水公司”是如何说明如何使用忙碌缓冲区的。Dijkstra 使用这个问题来演示了信号量在同一个问题中的不同用途 [Dijkstra, 1968]。假设系统包含两个单线程（经典）进程，其中一个产生信息（生产者进程），另一个使用信息（消费者进程）。这两个进程通过从空缓冲区池获取一个空缓冲区、向其填充信息，并将其放入满缓冲区池来通信。消费者通过从满池中取回缓冲区、从缓冲区中复制信息并将缓冲区放入空池进行回收来获取信息。生产者和消费者使用固定有限的 N 个缓冲区在它们之间传递任意数量的信息。该解决方案使用缓冲区来保持生产者和消费者同步。

图 8.18 是生产者和消费者进程的程序方案。`empty` 和 `full` 信号量说明了一种新类型的信号量，称为通用信号量（也称为计数信号量）。二进制信号量仅取 0 和 1 的值，而对于 N 缓冲区问题，计数信号量可以取 0 到 N 的值。在解决方案中，计数信号量具有双重作用：它们记录空缓冲区和满缓冲区的数量。它们还用于同步进程操作，即在没有空缓冲区时阻塞生产者，在没有满缓冲区时阻塞消费者。

缓冲区是逻辑上分成 N 部分的内存块。每个缓冲区必须包含链接空间以将该缓冲区与其他空或满缓冲区关联，以及用于数据本身的空间。由于生产者和消费者都操作这些链接，因此操作缓冲区池的代码必须被视为临界区。互斥（`mutex`）信号量保护对两个缓冲区的访问，确保一次时间只有一个进程取或放缓冲区。`V()` 操作信号将缓冲区释放到空缓冲区池或满缓冲区池。

互斥信号量用于保护与操作缓冲区相关的临界区（例如列表插入/删除操作）。如果没有空缓冲区，`P(empty)` 操作将阻塞生产者。同样，如果没有满缓冲区，`P(full)` 操作将阻塞消费者。

## 图 8.18 有界缓冲区

该解决方案使用了三个信号量：`mutex` 是一个二进制信号量，`full` 和 `empty` 是通用信号量（取值范围从 0 到 N）。`mutex` 保护与操作缓冲区相关的临界区（例如列表插入/删除操作）。如果没有空缓冲区，`P(empty)` 操作将阻塞生产者。同样，如果没有满缓冲区，`P(full)` 操作将阻塞消费者。

## 图 8.20 协调读者和写者的第一种策略

在这一策略中，读者的优先级高于写者。这是因为一旦某个读者获取了共享资源的控制权，一连串读者就可以无限期阻塞任何写者。

```
reader() {

  while(TRUE) {

    <other computing>;

    P(mutex);

    readCount = readCount+1;

    if (readCount == 1)
      P(writeBlock);
    /* Critical section */
    access(resource);
    V(mutex);

    readCount = readCount-1;
    if (readCount == 0)
      V(writeBlock);
    V(mutex);
  }

}

writer() {

  while(TRUE) {

    <other computing>
    P(writeBlock);
    /* Critical section */
    access(resource);
    V(writeBlock);

  }

}
```

```
resourceType *resource;
int readCount = 0;
semaphore mutex = 1;
semaphore writeBlock = 1;
/* 启动读者和写者 */
fork(reader, 0); /* 可以有很多个 */
fork(writer, 0); /* 可以有很多个 */
```

实现第二种策略的算法如图 8.21 所示。该策略仍然允许一连串读者进入临界区，直到写者到达。一旦写者到达，它将优先于所有后续读者，但已经访问共享资源的读者外。当第一个写者到达时，它将获得 `readBlock` 信号量。然后它会在 `writeBlock` 信号量上阻塞，等待所有读者离开临界区。下一个到达的写者将获得 `writePending` 信号量，然后在 `writeBlock` 信号量上阻塞。假设此时又有另一个写者到达，它将一直阻塞直到第一个写者进入临界区。如果第二个写者到达，它将在 `writePending` 信号量上阻塞。第二个及随后的写者被阻塞在 `writeBlock` 上，且没有读者在信号量上阻塞，写者将主导资源。当所有写者完成后，读者才被允许使用资源。

这个例子突出了一个新问题。信号量将硬件级同步抽象为用于解决简单问题的软件机制，但像读者-写者问题这样复杂的问题要困难得多。我们如何知道像读者-写者这样的解决方案是正确的？我们剩下两条路：

- 创建一个更高层次的抽象（你将在第 9 章中学习更多内容）。
- 证明你的同步程序是正确的。也就是说，信号量并没有消除对证明的需求，但它们使我们能够编写出比没有它们时更复杂的场景的程序。

## 图 8.21 协调读者和写者的第二种策略

第二种读者-写者策略赋予了写者优先级。即使有读者正在使用共享资源，当写者到达时，它将在任何其他读者被访问之前获取资源的权限。

```
reader() {

  while (TRUE) {

    <other computing>
    P(pending);
    P(readBlock);
    P(mutex1);
      readCount = readCount+1;
      if (readCount == 1)
        P(writeBlock);
    V(mutex1);
    V(readBlock);
    V(pending);
    access(resource);
    P(mutex1);
      readCount = readCount-1;
      if (readCount == 0)
        V(writeBlock);
    V(mutex1);

  }

}

writer() {

  while (TRUE) {

    <other computing>
    P(mutex2);
    writeCount=writeCount+1;
    if (writeCount==1)
      P(readBlock);
    V(mutex2);
    P(writeBlock);
    access(resource);
    V(writeBlock);
    P(mutex2);
      writeCount=writeCount-1;
      if (writeCount==0)
        V(readBlock);
    V(mutex2);

  }

}
```

```
resourceType *resource;
int readCount = 0, writeCount = 0;
semaphore mutex1 = 1, mutex2 = 1;
semaphore readBlock = 1;
semaphore writePending = 1;
semaphore writeBlock = 1;
/* 启动读者和写者 */ /* 可以有很多个 */
fork(reader, 0); /* 可以有很多个 * */
fork(writer, 0); /* 可以有很多个 * */
```
