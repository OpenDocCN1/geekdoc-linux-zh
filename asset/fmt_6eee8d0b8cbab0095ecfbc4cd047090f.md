
每个 `callout` 条目由一个 `callout` 结构表示，它们通过 `ct_idhash[]` 和 `ct_lbhash[]` 数组链接到某张 `callout` 表，其中每个数组元素要么为 `null`，要么是指向 `callout` 结构的指针。`callout` 条目存储在这两个数组中；一个数组按 `callout` ID 进行散列，另一个按 `lbolt` 值进行散列。在初始化时，内核还会为每张 `callout` 表创建两个 `callout` 线程。当 `callout_schedule()` 函数执行时（由时钟处理程序调用），如果有定时器已到期的函数需要执行，就会通过条件变量通知这些 `callout` 线程。

正如我们前面提到的，`timeout(9F)` 函数对 `callout` 表条目进行的插入和删除，在运行中的 Solaris 系统上是一种常见且频繁的操作。将条目放入 `callout` 队列的算法如下（即 `timeout(9F)` 的流程）。

- `timeout(function_pointer, argument_pointer, time value (delta))` 进入 `timeout_common()`，携带传给 `timeout(9F)` 的所有参数，以及一个用于 `callout_table` 数组的下标。该下标的推导基于 CPU 的 `cpu_seqid`（顺序 ID）字段以及 `callout` 类型，其中普通 `callout` 放置在数组位置 8 到 15 之间索引的表上（实时 `callout` 为 0 到 7）。

    基本上，随着 CPU ID 递增，该算法会让 `callout` 条目在索引 8 到 15 之间循环；同一个 CPU 每次都会引用同一个索引位置。

- `timeout_common()` 会从 `ct_freelist` 中获取一个 `callout` 结构（如果有可用的话），否则由内核内存分配器分配一个新的结构。

- 在 `callout` 结构中设置 `c_func` 和 `c_arg` 字段，并将 `c_runtime` 字段设置为当前 `lbolt` 值与传入的定时器值之和。

- `timeout_common()` 在 `callout` 表结构中建立 ID，设置 `ct_short_id` 或 `ct_long_id`（如果定时器值大于 16,384，则为长 ID）。

    我们之前看到，这些 ID 字段在引导时被初始化。随着 `callout` 条目的不断添加，该算法基本上是向上计数，直到回绕并重新开始。这个过程导致了我们刚刚讨论过的重用问题，这也是我们区分短期和长期 ID 的原因。

- `callout` 结构中的 `c_xid` 被设置为与 `callout` 表 ID 相同的值。

- 该算法将 `callout` 条目（`callout` 结构）插入 `callout` 表时，会同时把该条目添加到 `callout` 表中的 `ct_idhash[]` 和 `ct_lbhash[]` 数组。对于 `ct_idhash[]` 的放置，它通过对 ID 进行散列来推导数组下标；对于通过 `ct_lbhash[]` 找到的条目，则对 `callout` 结构中设置的 `c_runtime` 值进行散列来推导数组下标。如果该数组下标已经有一个指针，算法会通过 `next` 和 `prev` 指针将 `callout` 结构链接起来。

至此，`callout` 条目已建立在 `callout` 表上，`timeout(9F)` 将该 ID 返回给调用函数。`realtime_timeout()` 的事件序列与此相同。

当时钟中断处理程序调用 `callout_schedule()` 时，其工作基本上通过多个循环完成。外层循环遍历所有 `callout` 表，内层循环遍历表中的 `callout` 条目。

- 一个被设置为当前 `lbolt` 值的局部函数变量用于进入内层循环，`callout` 条目的 `c_runtime` 值决定了这些 `callout` 是否到期需要执行。

- 如果 `callout` 未到期或已在运行中，代码会继续处理下一个条目。否则，就该执行 `callout` 条目中的函数了。

- 对于普通 `callout` 类型，会设置一个条件变量信号函数，以唤醒一个 `callout` 线程来执行该函数。对于实时 `callout`，内核会调用 `softcall()` 函数来产生一个软件中断，该中断会打断某个处理器，从而使函数无需经过调度器即可执行。

- 在内层循环处理完一张 `callout` 表后，外层循环会将代码移到下一张 `callout` 表。在内层循环中会获取互斥锁（`ct_lock`），以防止另一个处理器同时处理同一个 `callout` 表。当内层循环完成对该 `callout` 表的处理后，互斥锁被释放。

- 初始化时创建的 `callout` 线程（每张 `callout` 表两个）随后进入循环，等待 `ct_threadpool` 条件变量。当普通 `callout` 条目到期需要执行时（如上所述），会通过条件变量通知它们，此时它们会调用 `callout_execute()` 函数。`callout_execute()` 也会通过 `softcall()` 中断函数被调用来运行由 `realtime_timeout()` 放置在 `callout` 表上的函数。

需要重申的是，普通 `callout` 可能会面临一些额外的延迟，因为 `callout` 线程在被条件变量通知后需要被调度。而 `softcall()` 方法会通过中断设施，迫使某个处理器更早地进入 `callout_execute()` 函数。

- `callout_execute()` 会再次遍历 `callout` 表，检查函数执行的条件。在函数调用与锁释放之间，另一个处理器可能已经处理了相关事项，因此内核在实际执行函数之前，会检查表中条目的时间值和运行标志。

- 假设确实到了运行时间，`callout_execute()` 会在 `callout` 条目的 `c_xid` 字段中设置 `CALLOUT_EXECUTING` 标志，然后调用该函数。

- 随后，`callout` 条目会从 `callout` 表中移除，`callout` 结构被放入空闲列表（`ct_freelist`），如果有任何线程正在 `c_done` 条件变量上休眠，则会广播该条件变量。这个条件变量是 `callout` 条目的一部分，它提供了一种生成通知的方法，用于通知放在 `callout` 表上的函数已经执行完毕。

内核还提供了 `untimeout(9F)` 接口，用于移除 `callout`。调用 `untimeout(9F)` 时需要传入 ID（该 ID 是函数被放入 `callout` 表时由 `timeout(9F)` 返回的）。通过 `ct_idhash[]` 数组定位该条目并将其移除，同时将 `callout` 结构添加到空闲列表中。由 `realtime_timeout(9F)` 添加的 `callout` 条目也可以使用 `untimeout(9F)` 移除。移除实时 `callout` 没有单独的函数。

## 2.5.2 Solaris 2.5.1 的 Callout 表

Solaris 2.5.1 中的 `callout` 表在功能上与我们在 Solaris 2.6 和 Solaris 7 中描述的完全相同；只是实现方式不同。Solaris 2.5.1 维护两张 `callout` 表——一张用于普通 `callout`，一张用于实时 `callout`——它们都在引导时初始化。Solaris 2.5.1 中 `callout` 表的总体结构如图 2.11 所示。

如你所见，许多结构字段在名称（和功能）上与之前描述的完全相同。每张 `callout` 表通过一个 `callout_state` 指针（普通 `callout` 表）和一个 `rt_callout_state` 指针（实时 `callout` 表，图中未显示，但结构相同）进行链接。这两张表实现了一个包含 256 个桶（`bucket`）的数组；每个桶链接到一个 `callout` 结构，并维护该条目的 ID。

初始化过程发生在引导时，分为两个不同的设置阶段：一个用于普通 `callout` 表，一个用于实时 `callout` 表。`callout_state` 结构（实际上就是 `callout` 表）的 `cs_bucket[]` 数组实现为一个循环单链表。在初始化时，`b_first` 指针被设置为指向自身；随着 `callout` 被添加到桶中，最后一个 `callout` 的 `c_next` 会引用该桶中的第一个条目。与 Solaris 2.6 和 7 的实现一样，这些 ID 字段表示长 ID 和短 ID 两个命名空间。在初始化阶段，这些字段会在每个桶头中被设置为初始值。

![](img/220ae4af07df2fe8e5be69d27f885d1b_93_0.png)

每个 `callout` 条目中的 `c_xid`（扩展 ID）字段具有多重作用：它标识 `callout` 条目、`callout` 表（普通或实时）、桶 ID，以及一个标志（用于指示是否为长期 `callout`）。
