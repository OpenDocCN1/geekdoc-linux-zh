
# 354 GNU/Linux 应用程序编程

```c
1: #include <stdio.h>
2: #include <sys/sh.h>
3: #include <sys/sem.h>
4: #include <string.h>
5: #include <stdlib.h>
6: #include <unistd.h>
7: #include "common.h"
8: 
9: #define MAX_STRING 5000
10: 
11: typedef struct {
12:     int semID;
13:     int counter;
14:     char string[MAX_STRING+1];
15: } MY_T;
16: 
17: int main(int argc, char *argv[])
18:     
19:     int shmid, ret, i;
20:     MY_BLOCK_T *block;
21:     struct sem sb;
22:     char user;
23: 
24:     /* 确保有参数 */
25:     if (argc >= 2) {
26: 
27:         /* 如果命令是 "create" */
28:         */
29:         if (!strncmp(argv[1], "create", 6)) {
30:             printf("Creating shared memory\n");
31: 
32:             /* 创建共享内存 */
33:             shmid = shmget(MY_SHM_ID, sizeof(MY_BLOCK_T), IPC_CREAT | 0666);
34: 
35:             /* 挂载段 */
36:             block = (MY_BLOCK_T *)shmat(shmid, (void *)0, 0);
37: 
38:             /* 初始化指针 */
39:             block->counter = 0;
40: 
41:             /* 创建信号量 */
42:             block->semID = shmget(MY_SEM_ID, sizeof(struct sem), IPC_CREAT | 0666);
43: 
44:             /* 初始化信号量 */
45:             sb.sem_num = 0;
46:             sb.op = 1;
47:             sb.sem_flg = 0;
48:             semop(block->semID, &sb, 1);
49: 
50:             /* 我们完成了，取消映射共享内存段。 */
51:             shmdt((void *)block);
52:         } 
53:         else if (!strncmp(argv[1], "use", 3)) {
54: 
55:             /* 指定一个字符（写入缓冲区） */
56:             if (argc < 3) exit(-1);
57: 
58:             user = argv[2][0];
59: 
60:             /* 获取共享内存段 */
61:             shmid = shmget(MY_SHM_ID, 0, 0);
62: 
63:             /* 挂载它 */
64:             block = (MY_BLOCK_T *)shmat(shmid, (void *)0, 0);
65: 
66:             for (i = 0; i < 2500; i++) {
67: 
68:                 /* 暂时让 CPU */
69:                 sleep(0);
70: 
71:                 /* 获取信号量 */
72:                 sb.sem_num = 0;
73:                 sb.op = -1;
74:                 sb.sem_flg = 0;
75:                 if (semop(block->semID, &sb, 1) != -1) {
76: 
77:                     /* 将我们的字符写入段缓冲区
78:                      *（只有当我们拥有信号量时）。这是
79:                      * 我们的临界区。 */
80:                     block->string[block->counter++] = user;
81: 
82:                     /* 释放信号量 */
83:                     sb.sem_num = 0;
84:                     sb.op = 1;
85:                     sb.sem_flg = 0;
86:                     if (semop(block->semID, &sb, 1) == -1) {
87: 
88:                         printf("Failed to release the semaphore\n");
89:                     }
90:                 }
91:             } else {
92: 
93:                 printf("Failed to acquire the semaphore\n");
94:             }
95:         }
96:         }
97: 
98:         /* 我们完成了，取消映射共享内存段。 */
99:         ret = shmdt((void *)block);
100:    } 
101:    else if (!strcmp(argv[1], "read", 6)) {
102: 
103:        /* 在这里，我们将读取共享段中的缓冲区 */
104:        
105:        shmid = shmget(MY_SHM_ID, 0, 0);
106: 
107:        block = (MY_BLOCK_T *)shmat(shmid, (void *)0, 0);
108: 
109:        for (i = 0; i < block->counter; i++) {
110:            printf("%c", block->string[i]);
111:        }
112:        printf("\n");
113: 
114:        shmdt((void *)block);
115:    } 
116:    return 0;
117:}
```
