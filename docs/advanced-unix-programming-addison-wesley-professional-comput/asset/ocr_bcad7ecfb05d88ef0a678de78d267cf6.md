![](bbox=[0.24, 0.15, 0.75, 0.4])

Figure 7.3 Server sharing memory with two clients.

We'll take advantage of one of the features of System V semaphores and use one semaphore set of two semaphores for each shared-memory segment. Semaphore 0 is the read semaphore, and 1 is the write semaphore. Here are some macros for those numbers and for the `semwait` and `sempost` operations on them:

```
#define SEMI_READ    0
#define SEMI_WRITE   1
#define SEMI_POST    1
#define SEMI_WAIT    -1
```

Given a semaphore, the function `op_semi` operates on it. For example, to post the write semaphore for a segment, you execute:

```
ec_negl( op_semi(semid_receiver, SEMI_WRITE, SEMI_POST) )
```

Here's the code for `op_semi`:

```
static int op_semi(int semid, int sem_num, int sem_op)
{
   struct sembuf sbuf;
   int r;

   sbuf.sem_num = sem_num;
   sbuf.sem_op = sem_op;
   sbuf.sem_flg = 0;
   ec_negl( r = semop(semid, &sbuf, 1) )
   return r;
```