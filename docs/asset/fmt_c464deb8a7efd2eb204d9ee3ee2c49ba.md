
```c
void createsem(int *sid, key_t key, int members)
{
  int cntr;
  union semmpts;
  if(members > SEMMSL) {
    printf("Sorry, max number of semaphores in a set is %d\n", SEMMSL);
    exit(1);
  }
  printf("Attempting to create new semaphore set with %d members\n", members);

  if(*sid = semget(key, members, IPC_CREATE|IPC_EXCL|0666)) == -1) {
    fprintf(stderr, "Semaphore set already exists!\n");
    exit(1);
  }

  semopts.val = SEM_RESOURCE_MAX;

  /* 初始化所有成员（可以使用 SETALL 完成） */
  for(cntr=0; centr<members; centr++)
    semctl(*sid, centr, SETVAL, &semopts);
}
```

```c
void locksem(int sid, int member)
{
    struct sembuf sem_lock={ 0, -1, IPC_NOWAIT};
    if(member<0 || member>get_member_count(sid)-1)
    {
        fprintf(stderr, "semaphore member %d out of range\n", member);
        return;
    }

    /* 尝试锁定信号量集 */
    if(!getlock(sid, member)) {
        fprintf(stderr, "Semaphore resources exhausted (no lock)!\n");
        exit(1);
    }

    sem_lock.sem_num = member;

    if((semop(sid, &sem_lock, 1)) == -1) {
        fprintf(stderr, "Lock failed\n");
        exit(1);
    }
    else
        printf("Semaphore resources decremented by one (locked)\n");

    dispval(sid, member);
}

void unlocksem(int sid, int member)
{
    struct sembuf sem_unlock={ member, 1, IPC_NOWAIT};
    int semval;

    if(member<0 || member>get_member_count(sid)-1) {
        fprintf(stderr, "semaphore member %d out of range\n", member);
        return;
    }

    /* 信号量是否锁定？ */
    semval = getval(sid, member);
    if(semval == SEM_RESOURCE_MAX) {
        fprintf(stderr, "Semaphore not locked!\n");
        exit(1);
    }

    sem_unlock.sem_num = member;

    /* 尝试锁定信号量集 */
    if(semop(sid, &sem_unlock, 1) == -1) {
        fprintf(stderr, "Unlock failed\n");
        exit(1);
    }
    else
        printf("Semaphore resources incremented by one (unlocked)\n");

    dispval(sid, member);
}
```

```c
void removesem(int sid)
{
    semctl(sid, 0, IPC_RMID, 0);
    printf("Semaphore removed\n");
}
```

```c
unsigned short get_member_count(int sid)
{
    union semun semopts;
    struct semid_ds myds;

    semopts.buf = &myds;

    /* 返回信号量集中的成员数量 */
    return(semopts.buf->sem_num);
}
```

```c
int getval(int sid, int member)
{
  int semval;

  semval = semctl(sid, member, GETVAL, 0);
  return(semval);
}
```

```c
void changemode(int sid, char *mode)
{
  int rc;
  union semun semopts;
  struct semid_ds myds;

  /* 获取内部结构的当前值 */
  semopts.buf = &myds;

  rc = semctl(sid, 0, IPC_STAT, &semopts);
  if (rc == -1) {
    perror("semctl");
    exit(1);
  }

  printf("Old permissions were %o\n", semopts.buf->perm.mode);

  /* 修改信号量的权限 */
  sscanf(mode, "%o", &semopts.buf->perm.mode);

  /* 更新信号量集 */
  semctl(sid, 0, IPC_SET, &semopts);

  printf("Updated: %d\n", rc);
}
```

```c
void dispval(int sid, int member)
{
  int semval;

  semval = semctl(sid, member, GETVAL, 0);
  printf("semval for member %d is %d\n", member, semval);
}
```

```c
void usage(void)
{
  fprintf(stderr, "semtool - 一个用于操作信号量的工具\n");
  fprintf(stderr, "USAGE: semtool <create>\n");
  fprintf(stderr, "lock <sem>\n");
  fprintf(stderr, "unlock <sem>\n");
  fprintf(stderr, "delete\n");
  fprintf(stderr, "mode <mode>\n");
  exit(0);
}
```

## `semstat`: `semtool`

作为额外奖励，提供了一个名为 `semstat` 的辅助程序。`semstat` 显示了由 `semtool` 创建的信号量的值。

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

摘自《Linux 程序员指南》第 6 章

(C) 1994-1995, Scott Burkett

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

模块：`semstat.c`

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

`semtool` 的配套工具。`semstat` 显示了由 `semtool` 创建的所有信号量的当前值。
