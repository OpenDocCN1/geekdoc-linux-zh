
## 8.1 Event infrastructure 147

Table 8.6 Values for perf_event_attr.sample_type
(Gleixner Molnar, 2014)

| Value | Records |
|---|---|
| PERF_SAMPLE_IP | Instruction pointer |
| PERF_SAMPLE_TID | Thread id |
| PERF_SAMPLE_TIME | Timestamp |
| PERF_SAMPLE_ADDR | Address |
| PERF_SAMPLE_READ | Counter values |
| PERF_SAMPLE_CALLCHAIN | Stacktrace |
| PERF_SAMPLE_ID | Unique id for group leader |
| PERF_SAMPLE_CPU | CPU number |
| PERF_SAMPLE_PERIOD | Sampling period. |
| PERF_SAMPLE_STREAM_ID | Unique id for opened event |
| PERF_SAMPLE_RAW | Additional data (depends on event) |
| PERF_SAMPLE_BRANCH_STACK | Record of recent branches |
| PERF_SAMPLE_REGS_USER | Userspace registers |
| PERF_SAMPLE_STACK_USER | Userspace stack |
| PERF_SAMPLE_WEIGHT | Hardware weight for cost of event |
| PERF_SAMPLE_DATA_SRC | Data source in hierarchy |

Another important configuration is the frequency of events controlled. This is controlled with either perf_event_attr.sample_period or perf_event_attr.sample_freq fields. The perf_event_attr.sample_period is the same interface described in Chapter 6, where the counter is set to (unsigned)-j perf_event_attr.sample_period, generating an interrupt every sample_period events.

On the other hand with perf_event_attr.sample_freq, the kernel will adjust the sampling period to receive the requested rate.

### 8.1.4 ENABLING, DISABLING, AND RESETTING COUNTERS

Event counts can be controlled by performing ioctl(2) on the associated file descriptor. Modifications can be per event or per group. To modify an individual descriptor, the ioctl(2) is invoked on the event's file descriptor and uses 0 as the last argument. On the other hand, the full event count can be modified by invoking the ioctl(2) on the group leader's file descriptor and using PERF_IOC_FLAG_GROUP as the last argument.

The PER_EVENT_IOC_ENABLE and PER_EVENT_IOC_DISABLE ioctls enable and disable the counters, respectively. This does not change the counter values.

The PER_EVENT_IOC_RESET ioctl resets the counter to 0. However, any other data associated with the event counter, as the time_enabled or time_running values, are not reset.

## CHAPTER 8 Perf

### 8.1.5 READING COUNT EVENTS

As mentioned earlier, event counts can be accessed by invoking read(2) on the event file descriptor. Additionally, all event counts within a group can be obtained together, via read(2) on the group leader's file descriptor, if the PER_FORMAT_GROUP flag was specified as part of perf_event_attr.read_format.

Consider the example in Listing 8.2. In this example, branch hardware events, retired and misses, are measured for a trivial workload that alternates between and two branches. Notice that in order to prevent the compiler from optimizing the workload of the executable, the termination condition is dependent on user input and the results are printed.

On lines 61 and 65, the two descriptors are created, with the PER_COUNT_HW_BRANCH_INSTRUCTIONS as the group leader. In this example, the predefined events of type PER_TYPE_HARDWARE are used. This is because branch counts, branch retired and branch misses are retired, architectural events. If desired, these events could also be encoded using the PER_TYPE_RAW event type. This would require changing the value of perf_attr.type on line 22, and then setting perf_attr.config to 0xCC4 and 0x0C5 for PER_COUNT_HW_BRANCH_INSTRUCTIONS and PER_COUNT_HW_BRANCH_MISSES respectively.

On line 25, the perf_event_attr.read_format field is set to report both event counts together in the same read(2) call, which occurs on line 99. Additionally, it is also set to report the time the counters were enabled and run, in order to monitor multiplexing.

Then, the counters are prepared to begin measurement. First, the counters are reset, line 69, to ensure the starting values are known. Secondly, the counters are enabled, line 75, since they were created, line 28. Notice that ioctl(2) affects both counters in the group, because of the PER_IOC_FLAG_GROUP flag.

The trivial microbenchmark, lines 81 to 91, is designed to determine whether the branch predictor will correctly identify this pattern. The advantage of such a simple workload for this example is easy validating results. For each iteration, two branches occur. The first branch checks whether the loop index, i, has exceeded the limit. The second branch checks whether the loop index is even or odd. Therefore, the total number of branches is (2*)1 or simply 93 + 1.

Once the workload has finished, the counters are disabled, and the results are read into the results structure. Remember that the format of this buffer differs on the values set in perf_event_attr.read_format. Changing one of those values may require rearranging the structure. Due to the usage of PER_FORMAT_GROUP, only one read(2) is called to return both counter values. Otherwise, a separate read be necessary for each file descriptor.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
```

```c
#include <types.h>

#include <unistd.h>
#include <sys/syscall.h>
#include <linux/event.h>

int _perf_event_open(struct perf_event_attr *attr, pid_t pid, int cpu,
    int group_fd, unsigned long flags)
{
    return syscall(NR_perf_event_open, attr, pid, cpu, group_fd, flags);
}
static int setup_cnt(int const fd, uint64_t event, int leader) {
    struct perf_event_attr *attr;

    memset(&attr, 0, sizeof(struct perf_event_attr));
    attr.type = PERF_TYPE_HARDWARE;
    attr.config = event;
    attr.size = sizeof(struct perf_event_attr);
    attr.read_format = PERF_FORMAT_GROUP |
        PERF_FORMAT_TOTAL_TIME_ENABLED |
        PERF_FORMAT_TOTAL_TIME_RUNNING;

    attr.disabled = 1;
    attr.exclude_kernel = 1;

    *fd = _perf_event_open(&attr, 0, -1, leader, 0);
    if (*fd < 0)
        perror("perf_event_open");
    return (*fd < 0);
}

#define NUM_EVENTS 2
enum { TOTAL = 0, MISS = 1 };

struct read_format {
    uint64_t nr;
    uint64_t time_enabled;
    uint64_t time_running;
    uint64_t value[NUM_EVENTS];
};

int main(int argc, char **argv) {
    int brh_fd[NUM_EVENTS], ret, iter, max;
```

```c
51      struct read_format result;
52
53      ret = EXIT_FAILURE;
54
55      if (argc != 2) {
56          fprintf(stderr, "Usage: %s <num>\n", argv[0]);
57          goto done;
58      }
59      max = atoi(argv[1]);
60
61      if (setup_cnt(&brh_fd[0], PERF_COUNT_HW_BRANCH_INSTRUCTIONS, -1)) {
62          goto done;
63      }
64      if (setup_cnt(&brh_fd[1], PERF_COUNT_HW_BRANCH_MISSES, brh_fd[0])) {
65          goto done;
66      }
67
68      if (ioctl(brh_fd[0], PERF_EVENT_IOC_RESET | PERF_IOC_FLAG_GROUP, 0) < 0) {
69          perror("PERF_EVENT_IOC_RESET)");
70          goto done_1;
71      }
72
73      if (ioctl(brh_fd[0], PERF_EVENT_IOC_ENABLE | PERF_IOC_FLAG_GROUP, 0) < 0) {
74          perror("PERF_EVENT_IOC_ENABLE)");
75          goto done_1;
76      }
77
78      iter = 0;
79      /* simple branch test: alternating or odd */
80      int i = 0;
81      while (i < max) {
82          if (i & 1)
83              i++;
84          else
85              i += 3;
86          iter++;
87      }
88
89
90      if (ioctl(brh_fd[0], PERF_EVENT_IOC_DISABLE | PERF_IOC_FLAG_GROUP, 0) < 0) {
91          perror("PERF_EVENT_IOC_DISABLE)");
92          goto done_1;
93      }
```

```c
98  read(brh_fd[0], &result, sizeof(struct read_format));
99  printf("%d / %d branches mispredicted\n",
100 result.value[MISS], result.value[TOTAL]);
101 printf("%d\n", iter);
102
103 ret = EXIT_SUCCESS;
104 done_1:
105     close(brh_fd[1]);
106 done_0:
107     close(brh_fd[0]);
108 done:
109     return ret;
110 }
111 )
```

## 8.1 Event infrastructure 149

## LISTING 8.2

Example using read(2) to access hardware counters.

When the author runs the application in Listing 8.2, the following results were produced:

```
$ ./read 100
6 / 133 branches mispredicted
50
$ ./read 100
7 / 133 branches mispredicted
50
$ ./read 100
7 / 133 branches mispredicted
50
$ ./read 100
5 / 133 branches mispredicted
50
```

When performing counters, these sorts of discrepancies are common. Remember that PMU events measure the behavior of the processor's internals. In other words, what is counted toward an event and when it is counted, depends on the specific hardware implementation. This is especially problematic when using lower level events, because these events rely upon internal core state state than higher level
