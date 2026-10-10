
```c
int cnts_open(int *event_attr, struct *attr) {
    memset(&attr, 0, sizeof(attr));
    attr.type = PERF_TYPE_HARDWARE;
    attr.size = sizeof(struct perf_event_attr);
    attr.read_format =
        PER_FORMAT_TOTAL_TIME_ENABLED|
        PER_FORMAT_TOTAL_TIME_RUNNING;
    attr.config = PERF_COUNT_EVENT_HW_CPU_CYCLES;
    fd[CYCLES] = perf_event_open(&attr, 0, -1, -1, 0);
    if (fd[CYCLES] == -1) 
        perror("cannot open perf_counter for cycles"); exit(0);
    attr.config = PERF_COUNT_HW_INSTRUCTIONS;
    fd[INSTRUCTIONS] = perf_event_open(&attr, 0, -1, -1, 0);
    if (fd[INSTRUCTIONS] == -1) 
        perror("cannot open perf_counter for instructions"); exit(0);
#ifdef ARM11
    attr.type = PERF_TYPE_RAW;
    attr.config = 0x9;
    fd[CACHFS] = perf_event_open(&attr, 0, -1, -1, 0);
    if (fd[CACHFS] == -1) 
        perror("cannot open perf_counter for cache refs"); exit(0);
    attr.config = 0x8;
    fd[CACHES] = perf_event_open(&attr, 0, -1, -1, 0);
    if (fd[CACHES] == -1)
        perror("cannot open perf_counter for cache misses"); exit(0);
#else
    attr.config = PERF_COUNT_HW_REFERENCES;
    fd[CACHFS] = perf_event_open(&attr, 0, -1, -1, 0);
    if (fd[CACHFS] == -1) 
        perror("cannot open perf_counter for cache refs"); exit(0);
    attr.config = PERF_COUNT_HW_MISSES;
    fd[CACHES] = perf_event_open(&attr, 0, -1, -1, 0);
    if (fd[CACHES] == -1)
        perror("cannot open perf_counter for cache misses"); exit(0);
#endif
}
```

添加 `tick` 和 `clock` 函数，它们可以在代码执行前后后调用：

```c
void cnts_tick(int *fd) {
    int i, ret;
    cnts_open(fd);
    for (i=0; i<4; i++) {
        ret = ioctl(fd[i], PERF_EVENT_IOC_RESET);
        if (ret==-1) perror("ioctl in cnts_tick() failed");
    }
}

void cnts_clock(int *fd, unsigned long long cnts[]) {
    int i, ret;
    for (i=0; i<4; i++) {
        ret = read(fd[i], cnts[i], sizeof(cnts[i]));
        if (ret!=8) perror("read in cnts_clock() failed");
    }
}
```

```c
void cnts_close(int *fd) {
  int i;
  for (i=0; i<4; i++) close(fd[i]);
}
```

## 1.10 测量带宽

为了开始使用 `perf_event`，让我们使用它来测量处理器写入连续块和读取连续块所需的时间。这种测试还允许我们测量内存带宽，读和写的情况通常不同。程序员可以使用这些值计算性能上限。

编写一个打印性能结果并计算带宽的打印程序：

```c
void cnts_dump(unsigned long long cnts[][3]) {
    float time, memb;
    time = ((float)cnts[CYCLES])/CLOCK_RATE;
    membw = (float)SIZE/time/(1024.0*1024.0);
    printf("[%perf_event] cycles = %llu (%0.0f us)\n",
           cnts[CYCLES],
           (float)cnts[CYCLES]/(CLOCK_RATE/1.0E-6));
    printf("[%perf_event] instructions = %llu (CPI=%0.2f)\n",
           cnts[INSTRUCTIONS],
           (float)cnts[INSTRUCTIONS])/(float)cnts[CYCLES]);
    printf("[%perf_event] misses = %llu, references = %llu\n"
           "(miss rate=%0.4f)\n",
           cnts[CACHES],
           cnts[CACHFS],
           (float)cnts[CACHES]/(float)cnts[CACHFS]);
}
```

接下来添加定义来指定拷贝的内存块大小（以字为单位）以及处理器频率。

```c
#define SIZE 128<<20 // 128MB

#if ARM11
#define CLOCK_RATE 700.0e6
#elif A9
#define CLOCK_RATE 666.0e6
#elif A15
#define CLOCK_RATE 2230.5e6
#endif
```
