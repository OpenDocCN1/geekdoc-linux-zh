# 2.4 Using Multiple Cores:OpenMP 59

+   - any state changes inside the parallel region are visible in all threads, and
- after the parallel region, its value in the master thread will reflect the
most recent write among all the threads.

This is illustrated in the following example, in which four threads write the
shared variable b.

```
int a=1;
#pragma omp parallel num_threads(4)
{
  a=2;
}
printf("%d\n",a); // value printed is 2
```

As is generally the case with parallelism and shared memory, the program-mer should use thread synchronization when writing shared variables that
read in another thread. This is described in more detail below.

Alternatively, the programmer can mark an externally declared variable as
being private in the parallel region using the "private" directive option. In
C++, the programmer can achieve the same effect by declaring the variable
inside the parallel region.

Private variables are local to each thread, so that changes to the variable
are only visible to the thread making the change and the variable state is
destroyed when the thread is destroyed.

Private scope is illustrated in the next example, in which the updates to the
private variable are lost after the parallel region.

```
int a=1;
#pragma omp parallel num_threads(4) private(a)
{
  a=2; // a will be destroyed
}
printf("%d\n",a); // printed value is 1
```

Variables can also be marked as "firstprivate" in which the OpenMP
runtime initializes the variable in the parallel region the same way as it
would for shared variables, that is, using the variable'9s state prior to the
parallel region.