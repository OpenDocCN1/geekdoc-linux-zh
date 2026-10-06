# 62 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

Also note the shorthand notation for the parallel region, in which the "omp parallel" and "omp sections" directives are combined into a single directive "omp parallel sections." Thread groups within each parallel section are numbered starting at 0. As a result, in this example, omp_get_thread_num() function would return 0 in each thread constants in each differentiate the behavior of each thread.

The final state of variables *a* and *b* in each thread are 10, 11, 12, respectively, demonstrating the initialization of the variable *a*. The printed value of *b* is 12, assigned in the last section.

Four threads are spawned in the second parallel region. The final state of *c* in each thread are 0, 1, 2, and 3. Because *c* is marked as a summation reduction variable, the printed value of *c* is 11, as the sum of these values as well as the initial value of *c*.

```
int a=10,b=1,c=5;
#pragma omp parallel sections firstprivate(a) lastprivate(b)
{
    #pragma omp section
    b=0+a;
    #pragma omp section
    b=1+a;
    #pragma omp section
    b=2+a;
}
```

```
#pragma omp parallel num_threads(4) reduction(+:c)
c=omp_get_thread_num();
printf("a=%d, b=%d, c=%d\n",a,b,c); // a=10, b=12, c=11

```

# 2.4.3 Other OpenMP directives

Nested pragmas are also used when a section within a parallel block must be executed in a special way, such as when a section must be executed in sequential order among the threads (the **ordered** pragma), when a section must be executed only on the master thread (the master pragma), when a section must be executed atomically (the **atomic** pragma), when a section