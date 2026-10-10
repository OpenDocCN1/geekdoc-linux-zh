
# 354 GNU/Linux 编程

```c
/* 挂载它 */
block = (MY_BLOCK_T *)shmat(shmid, (const void *)0, 0);
```

```c
for (i = 0; i < 2500; i++) {
  /* 暂时放弃 CPU */
  sleep(0);
  /* 获取信号量 */
  sb.sem_num = 0;
  sb.sem_op = -1;
  sb.sem_flg = 0;
  if (semop(block->semID, &sb, 1) != -1) {
    /* 将我们的字母写入段缓冲区
      *（仅在我们拥有信号量时）。这
      * 是我们的临界区。
    */
    block->string[block->counter++] = user;
    /* 信号量 */
    sb.sem_num = 0;
    sb.sem_op = 1;
    sb.sem_flg = 0;
    if (semop(block->semID, &sb, 1) == -1) {
      printf("Failed to release the semaphore\n");
    }
  } else {
    printf("Failed to acquire the semaphore\n");
  }
}
/* 我们已完成，取消映射共享内存段。 */
ret = shmdt((void*)block);
} else if (!strcmp(argv[1], "read", 6)) {
  /* 在这里，我们将读取共享段中的缓冲区 */
  shmid = shmget(MY_SHM_ID, 0, 0);
```

# 360 GNU/Linux 应用程序编程

通过 `stat` 信息，你特别使用 `st_mode` 字段来确定文件类型。该字段是文件类型的编码，但 GNU C 库提供了一组宏，用于测试给定的文件类型（如果文件是定义的类型则返回 1，否则返回 0）。这些宏在表 19.1 所示。

表 19.1 用于 stat 的文件测试宏

| 宏 | 描述（如果文件是该类型则返回 1） |
| --- | --- |
| `S_ISREG` | 普通文件 |
| `S_ISDIR` | 目录 |
| `S_ISCHR` | 特殊字符文件 |
| `S_ISBLK` | 特殊块文件 |
| `S_ISLNK` | 符号链接 |
| `S_ISFIFO` | 特殊 FIFO 文件 |
| `S_ISSOCK` | 套接字 |

要使用 `stat`，你通过一个代表要捕信息的结构的缓冲区来调用它。列表 19.1 提供了一个简单的应用程序，它使用提供的文件名作为参数，然后使用 `stat` 和文件测试宏来确定文件类型。

列表 19.1 使用文件测试宏确定文件类型（位于 CD-ROM 的 `/source/ch19/ftype.c` 中）

```c
int main( int argc, char *argv[]) 
{
    struct stat statbuf;
    /* 检查是否提供了文件名 */
    if (argc < 2) {
        printf("specify a file to test\n");
        return 1;
    }
    /* 获取文件的 stat 信息 */
    if (stat(argv[1], &statbuf) == -1) {
        printf("Can't stat file\n");
        return 1;
    }
}
printf("%s ", argv[1]);
/* 从 st_mode 确定文件类型 */
if (S_ISDIR(statbuf.st_mode)) {
  printf("is a directory\n");
} else if (S_ISCHR(statbuf.st_mode)) {
  printf("is a character file\n");
} else if (S_ISBLK(statbuf.st_mode)) {
  printf("is a block special file\n");
} else if (S_ISREG(statbuf.st_mode)) {
  printf("is a regular file\n");
} else if (S_ISFIFO(statbuf.st_mode)) {
  printf("is a FIFO file\n");
} else if (S_ISSOCK(statbuf.st_mode)) {
  printf("is a socket\n");
} else {
  printf("is unknown\n");
}
return 0;
}
```

```c
if (shmid != -1) {
  block = (MY_BLOCK_T*)shmat(shmid, (const void*)0, 0);
  /* 终止缓冲区 */
  block->string[block->counter+1] = 0;
  printf("%s\n", block->string);
  printf("length %d\n", block->counter);
  ret = shmdt((void*)block);
} else {
  printf("Unable to read segment.\n");
}
} else if (!strncmp(argv[1], "remove", 6)) {
  shmid = shmget(MY_SHM_ID, 0, 0);
  if (shmid != -1) {
    block = (MY_BLOCK_T*)shmat(shmid, (const void*)0, 0);
    /* 移除信号量 */
    ret = semctl(block->semID, 0, IPC_RMID);
    /* 移除共享段 */
    ret = semctl(shmid, IPC_RMID, 0);
    if (ret == 0) {
      printf("Successfully removed\n");
    }
  } else {
    printf("Failed to remove\n");
  }
}
```
