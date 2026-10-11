
### Reader-Writer Spin Lock Methods (continued)

| Method | Description |
| :--- | :--- |
| write_unlock_irqrestore() | Releases given lock and restores local interrupts to given previous state |
| write_trylock() | Tries to acquire given lock for writing; if unavailable, returns nonzero |
| rwlock_init() | Initializes given rwlock_t |

A final important consideration in using the Linux reader-writer spin locks is that they favor readers over writers. If the read lock is held and a writer is waiting for exclusive access, readers that attempt to acquire the lock continue to succeed. The spinning writer does not acquire the lock until all readers release the lock. Therefore, a sufficient number of readers can starve pending writers. This is important to keep in mind when designing your locking. Sometimes this behavior is beneficial; sometimes it is catastrophic.

Spin locks provide a quick and simple lock. The spinning behavior is optimal for short hold times and code that cannot sleep (interrupt handlers, for example). In cases where the sleep time might be long or you potentially need to sleep while holding the lock, the semaphore is a solution.

## Semaphores

Semaphores in Linux are sleeping locks. When a task attempts to acquire a semaphore that is unavailable, the semaphore places the task onto a wait queue and puts the task to sleep. The processor is then free to execute other code. When the semaphore becomes available, one of the tasks on the wait queue is awakened so that it can then acquire the semaphore.

Let's jump back to the door and key analogy. When a person reaches the door, he can grab the key and enter the room. The big difference lies in what happens when another dude reaches the door and the key is not available. In this case, instead of spinning, the fellow puts his name on a list and takes a number. When the person inside the room leaves, he checks the list at the door. If anyone's name is on the list, he goes over to the first name and gives him a playful jab in the chest, waking him up and allowing him to enter the room. In this manner, the key (read: semaphore) continues to ensure that there is only one person (read: thread of execution) inside the room (read: critical region) at one time. This provides better processor utilization than spin locks because there is no time spent busy looping, but semaphores have much greater overhead than spin locks. Life is always a trade-off.

You can draw some interesting conclusions from the sleeping behavior of semaphores:
- Because the contending tasks sleep while waiting for the lock to become available, semaphores are well suited to locks that are held for a long time.
- Conversely, semaphores are not optimal for locks that are held for short periods because the overhead of sleeping, maintaining the wait queue, and waking back up can easily outweigh the total lock hold time.
- Because a thread of execution sleeps on lock contention, semaphores must be obtained only in process context because interrupt context is not schedulable.
- You can (although you might not want to) sleep while holding a semaphore because you will not deadlock when another process acquires the same semaphore. (It will just go to sleep and eventually let you continue.)
- You cannot hold a spin lock while you acquire a semaphore, because you might have to sleep while waiting for the semaphore, and you cannot sleep while holding a spin lock.

These facts highlight the uses of semaphores versus spin locks. In most uses of semaphores, there is little choice as to what lock to use. If your code needs to sleep, which is often the case when synchronizing with user-space, semaphores are the sole solution. It is often easier, if not necessary, to use semaphores because they allow you the flexibility of sleeping. When you do have a choice, the decision between semaphore and spin lock should be based on lock hold time. Ideally, all your locks should be held as briefly as possible. With semaphores, however, longer lock hold times are more acceptable. Additionally, unlike spin locks, semaphores do not disable kernel preemption and, consequently, code holding a semaphore can be preempted. This means semaphores do not adversely affect scheduling latency.

## Counting and Binary Semaphores

A final useful feature of semaphores is that they can allow for an arbitrary number of simultaneous lock holders. Whereas spin locks permit at most one task to hold the lock at a time, the number of permissible simultaneous holders of semaphores can be set at declaration time. This value is called the usage count or simply the count. The most common value is to allow, like spin locks, only one lock holder at a time. In this case, the count is equal to one, and the semaphore is called either a binary semaphore (because it is either held by one task or not held at all) or a mutex (because it enforces mutual exclusion). Alternatively, the count can be initialized to a nonzero value greater than one. In this case, the semaphore is called a counting semaphore, and it enables at most count holders of the lock at a time. Counting semaphores are not used to enforce mutual exclusion because they enable multiple threads of execution in the critical region at once. Instead, they are used to enforce limits in certain code. They are not used much in the kernel. If you use a semaphore, you almost assuredly want to use a mutex (a semaphore with a count of one).

Semaphores were formalized by Edsger Wybe Dijkstra³ in 1968 as a generalized locking mechanism. A semaphore supports two atomic operations, P() and V(), named after the Dutch word Proberen, to test (literally, to probe), and the Dutch word Verhogen, to increment. Later systems called these methods down() and up(), respectively, and so does Linux. The down() method is used to acquire a semaphore by decrementing the count by one. If the new count is zero or greater, the lock is acquired and the task can enter the critical region. If the count is negative, the task is placed on a wait queue, and the processor moves on to something else. These names are used as verbs: You down a semaphore to acquire it. The up() method is used to release a semaphore upon completion of a critical region. This is called upping the semaphore. The method increments the count value; if the semaphore’s wait queue is not empty, one of the waiting tasks is awakened and allowed to acquire the semaphore.

## Creating and Initializing Semaphores

The semaphore implementation is architecture-dependent and defined in <asm/semaphore.h>. The struct semaphore type represents semaphores. Statically declared semaphores are created via the following, where name is the variable’s name and count is the usage count of the semaphore:

```c
struct semaphore name;
sema_init(&name, count);
```

As a shortcut to create the more common mutex, use the following, where, again, name is the variable name of the binary semaphore:

```c
static DECLARE_MUTEX(name);
```

More frequently, semaphores are created dynamically, often as part of a larger structure. In this case, to initialize a dynamically created semaphore to which you have only an indirect pointer reference, just call sema_init(), where sem is a pointer and count is the usage count of the semaphore:

```c
sema_init(sem, count);
```

Similarly, to initialize a dynamically created mutex, you can use

```c
init_MUTEX(sem);
```

Dr. Dijkstra (1930–2002) is one of the most accomplished computer scientists in the (admittedly brief) history of computer scientists. His numerous contributions include work in OS design, algorithm theory, and the concept of semaphores. He was born in Rotterdam, The Netherlands, and taught at the University of Texas for 25 years. He would probably not be happy with the large number of GOTO statements in the Linux kernel, however.

I do not know why the "mutex" in init_MUTEX() is capitalized or why the "init" comes first here but second in sema_init(). I suspect that after you read Chapter 8, the inconsistency is not surprising.

## Using Semaphores

The function down_interruptible() attempts to acquire the given semaphore. If the semaphore is unavailable, it places the calling process to sleep in the TASK_INTERRUPTIBLE state. Recall from Chapter 3 that this process state implies that a task can be awakened with a signal, which is generally a good thing. If the task receives a signal while waiting for the semaphore, it is awakened and down_interruptible() returns -EINTR. Alternatively, the function down() places the task in the TASK_UNINTERRUPTIBLE state when it sleeps. You most likely do not want this because the process waiting for the semaphore does not respond to signals. Therefore, use of down_interruptible() is much more common (and correct) than down(). Yes, again, the naming is not ideal.

You can use down_trylock() to try to acquire the given semaphore without blocking. If the semaphore is already held, the function immediately returns nonzero. Otherwise, it returns zero and you successfully hold the lock.

To release a given semaphore, call up(). Consider an example:

```c
/* define and declare a semaphore, named mr_sem, with a count of one */
static DECLARE_MUTEX(mr_sem);

/* attempt to acquire the semaphore ... */
if (down_interruptible(&mr_sem)) {
    /* signal received, semaphore not acquired ... */
}

/* critical region ... */

/* release the given semaphore */
up(&mr_sem);
```

A complete listing of the semaphore methods is in Table 10.6.

### Semaphore Methods

| Method | Description |
| :--- | :--- |
| sema_init(struct semaphore *, int) | Initializes the dynamically created semaphore to the given count |
| init_MUTEX(struct semaphore *) | Initializes the dynamically created semaphore with a count of one |
| init_MUTEX_LOCKED(struct semaphore *) | Initializes the dynamically created semaphore with a count of zero (so it is initially locked) |
