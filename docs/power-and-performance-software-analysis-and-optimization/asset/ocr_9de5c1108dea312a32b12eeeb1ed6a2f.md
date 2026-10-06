# 8.1 Event infrastructure 151

```
98
99  read(brh_fd[TOTAL], &result, sizeof(struct read_format));
100  printf("%d / %d branches mispredicted\n",
101  result.value[MISS], result.value[TOTAL]);
102  printf("%d\n", iter);\n103
104      ret = EXIT_SUCCESS;
105  done_1:
106      close(brh_fd[MISS]);
107  done_0:
108      close(brh_fd[TOTAL]);
109  done:
110      return ret;
111 )
```

# LISTING 8.2

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

Earlier, the number of branches during the workload had been calculated as opposed to max+1, and we would expect 101 branches for our workload, Looking at the code, another return value for the ioctl(2) to enable the performance counters. Others can be accounted for by the glibc wrapper for ioctl(2), that is, the validation code to check the ioctl(2) that various arguments are correct, or perhaps to the return path from the ioctl(2) that enables the counters. Additionally, the discrepancy could be caused by a nuance of the specific event counter.

When performing counters, these sorts of discrepancies are common. Remember that PMU events measure the behavior of the processor's internals. In other words, what is counted toward an event and when it is counted, depends on the specific hardware implementation. This is especially problematic when using lower level events, because these events rely upon internal core state state than higher level