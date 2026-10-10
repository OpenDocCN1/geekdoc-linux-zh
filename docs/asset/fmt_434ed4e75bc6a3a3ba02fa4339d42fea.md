
`int semctl(int semid, int semnum, int cmd, ...)`

# Chapter 17 Synchronization with Semaphores 317

The first argument defines the semaphore identifier, the second defines the semaphore number of interest, the third defines the command to be applied, and then potentially another argument (usually defined as a union). The operations that can be performed are shown in Table 17.4.

## TABLE 17.4 Operations That Can Be Performed Using semctl

| Command | Description | Fourth Argument |
| --- | --- | --- |
| GETVAL | Return the semaphore value. | |
| SETVAL | Set the semaphore value. | int |
| GETPID | Return the process ID that last operated on the semaphore (`semop`). | |
| GETNCNT | Return the number of processes awaiting the semaphore to increase in value. | int |
| GETZCNT | Return the number of processes awaiting the semaphore to become zero. | int |
| GETALL | Return the value of each semaphore in a semaphore array. | `u_short*` |
| SETALL | Set the value of each semaphore in a semaphore array. | `u_short*` |
| IPC_STAT | Return the effective user, group, and permissions for a semaphore. | `struct semid_ds*` |
| IPC_SET | Set the effective user, group, and permissions for a semaphore. | `struct semid_ds*` |
| IPC_RMID | Remove the semaphore or semaphore array. | |

Now it's time to look at some examples of each of these operations in `semctl`, focusing on semaphore array examples where applicable. The first example illustrates the setting of a semaphore value and then returning its value. In this example, you first set the value of the semaphore to 10 (using the command `SETVAL`) and then read it back out using `GETVAL`. Note that the second argument (argument 2) defines an individual semaphore. Later on, you can take look at the semaphore array case with `GETALL` and `SETALL`.

```
int semid, ret, value;

...
/* Set the semaphore to 10 */
ret = semctl(semid, 0, SETVAL, 10);
...
/* Read the semaphore value (return value) */
value = semctl(semid, 0, GETVAL);
```

The `GETPID` command allows you to identify the last process that performed `semop` on the semaphore. The process identifier is the return value, and argument 4 is not used in this case.

```
int semid, pid;
pid = semctl(semid, 0, GETPID);
```

If no `semop` has been performed on the semaphore, the return value is zero. To identify the number of processes awaiting the semaphore to increase in value, you can use the `GETCNT` command. You can also identify the number of processes awaiting the semaphore to become zero using `GETCNT`. Both of these commands are illustrated in the following for the semaphore zero:

```
int semid, count;
```

```
/* How many processes are awaiting this semaphore to increase */
count = semctl(semid, 0, GETCNT);
```

```
/* How many processes are awaiting this semaphore to become zero */
count = semctl(semid, 0, GETCNT);
```

Now is time to look at example of some semaphore array operations. Listing 17.8 illustrates both `SETVAL` and `GETVAL` with `semctl`. In this example, you create a semaphore array of 10 semaphores. The creation of the semaphore array is performed at lines 20–21 using the `semget` function. Note that because you are going to create and remove the semaphore array within this function, you use no key and instead use `IPC_PRIVATE`. The `MAX_SEMAPH` defines the number of semaphores.

# 316 GNU/Linux 应用程序编程

在 `semget` 的最后一个示例中，你简单地获取一个已存在信号量的标识符。在这个示例中，你指定了键值但没有指定任何命令：

```
semid = semget(0x222, 0, 0);
if (semid == -1) {
    printf("Semaphore does not exist...\n");
}
```

关于信号量的最后一点说明是，就像消息队列一样，信号量在创建时会为它提供一组默认值。定义的参数如表 17.3 所示。在随后对 `semctl` 的讨论中，你可以看到如何更改某些参数。

## 表格 17.3 信号量内部值

| 参数 | 默认值 |
|---|---|
| `sem_perm.cuid` | 调用进程（创建者）的有效用户 ID |
| `sem_perm.uid` | 调用进程（所有者）的有效用户 ID |
| `sem_perm.cgid` | 调用进程（创建者）的有效组 ID |
| `sem_perm.gid` | 调用进程（所有者）的有效组 ID |
| `sem_perm.mode` | 权限（`semflg` 的低 9 位） |
| `sem_nms` | 设置为 `nsems` 的值 |
| `sem_otime` | 设置为零（上一次 `semop` 时间） |
| `sem_ctime` | 设置为当前时间（创建时间） |

进程可以覆盖这些参数中的某些。你将在后后对 `semctl` 的讨论中探索这一点。
