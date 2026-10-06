# 2.4 Using Multiple Cores: OpenMP 65

```
omp_unset_lock(&mylock);
```

```
}
```

```
printf("%d\n",a); // printed value is always 4
```

# 2.4.4.3 Barriers

A barrier is a point in the parallel region in which all threads must reach before any thread may proceed further. Barriers are useful for splitting up various phases of a parallel operation because threads will always experience load imbalance.

For example, in a video processing application, multiple threads will process the pixels in the frame, but all threads must complete moving to the next frame.

Barriers are specified as pragmas, as shown in the example below:

```
int a;
#pragma omp parallel num_threads(4)
{
    if (omp_get_thread_num()==2) a=omp_get_thread_num();
    #pragma omp barrier
    if (omp_get_thread_num()==2) a=omp_get_thread_num();
}
```

```
printf("%d\n",a); // printed value is always 4
```

# 2.4.4.4 Atomic sections

An atomic operation is guaranteed to be performed on one thread at any given moment in time. In this sense they are indivisible, much like actual atoms. In concept they are identical to critical sections, but atomic sections can only ensure exclusivity for a single assignment operation, so they are used only for single statements. Their advantage is that they have lower overhead than critical sections.

Atomic operations are specified as pragmas, for example:

```
int a=0;
#pragma omp parallel num_threads(4)
{
    #pragma omp atomic
```