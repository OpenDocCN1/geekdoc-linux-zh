# 2.4 Using Multiple Cores: OpenMP 69

a for-loop to multiple threads using the for directive. The directive can be
written as

```
#pragma omp parallel
#pragma omp for
for (...)"
```

or as a shortcut:

```
#pragma omp parallel for
for (...)
```

The parallel for directive requires that the termination condition be a single
less-than, less-than-equal, greater-than, or greater-than-or-equal compar-
ison with the loop variable, the increment operation must not be dependent
on code in the loop body, and not break, goto, or throw statements are
allowed in the loop body.

By default the loop variable is treated as private. This is important since each
thread will be simultaneously working on a different set of loop iterations
and so the value of each thread's i variable will have different values at
the same time.

Consider the following example:

```
#pragma omp parallel for
for (i=0;i<12;i++) {
    printf("iteration %d, thread %d\n",
    i.omp_get_thread_num());
}
```

When executed the new code will produce the following output:

+   iteration 0, thread 0
iteration 1, thread 0
iteration 2, thread 0
iteration 9, thread 3
iteration 10, thread 3
iteration 11, thread 3