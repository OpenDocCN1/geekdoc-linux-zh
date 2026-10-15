
`pthread_cond_timedwait` 阻塞线程，直到指定的超时时间到达，或者它被唤醒。如果超时到达，`pthread_cond_timedwait` 会返回 `ETIMEDOUT`。

使用绝对时间的优势是，`pthread_cond_timedwait` 可以在多个线程之间共享超时，而相对时间必须在每次调用时都重新计算。
