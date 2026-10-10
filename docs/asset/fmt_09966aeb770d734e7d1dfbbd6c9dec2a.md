
现在是时候查看一些信号量数组操作的示例。列表 17.8 展示了使用 `semctl` 的 `SETVAL` 和 `GETVAL`。在这个示例中，你创建了一个包含 10 个信号量的信号量数组。信号量数组的创建是在第 20-21 行使用 `semget` 函数完成的。注意，由于你将在此函数内部创建并移除信号量数组，你没有使用键，而是使用了 `IPC_PRIVATE`。`MAX_SEMAPH` 定义了信号量的数量。

## `semctl`

`semctl` API provides a number of control operations on semaphores or semaphore arrays. Examples of functionality range from setting the value of the semaphore (as shown in Listing 17.6) to removing a semaphore or semaphore array (see Listing 17.7). You get a chance to see these and other examples in this section. The function prototype for the `semctl` call is as follows:

```
