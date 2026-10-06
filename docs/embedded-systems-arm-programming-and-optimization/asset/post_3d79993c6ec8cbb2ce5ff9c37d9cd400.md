
# 64 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

Compile this example with the option "fopenmp". When executed, the master thread, thread 0, always reaches the critical section first but the worker threads reach the print in different orderings each run. Also notice that the print statement that is immediately after the parallel section will print after all worker threads finish.

Run 1:

```
thread 0 finished in position 1
thread 2 finished in position 2
thread 3 finished in position 3
thread 1 finished in position 4
parallel region ended
```

Run 2:

```
thread 0 finished in position 1
thread 3 finished in position 2
thread 2 finished in position 3
thread 1 finished in position 4
parallel region ended
```

Run 3:

```
thread 0 finished in position 1
thread 1 finished in position 2
thread 3 finished in position 3
thread 2 finished in position 4
parallel region ended
```

## 4.4.4.2 Locks

Locks provide a similar functionality as critical sections. Locks are specified as functions, so the programmer would call omp_set_lock() to mark the beginning of a critical section and omp_unset_lock() to mark its end. Locks have an associated handle that the programmer must declare and initialize in the master thread before use.

For example:

```
int a=0;

omp_lock_t mylock;
omp_init_lock(&mylock);

#pragma omp parallel num_threads(4)
{
omp_set_lock(&mylock);

a++;
```

## 2.4 Using Multiple Cores: OpenMP 65

```
omp_unset_lock(&mylock);
```

```
}
printf("%d\n",a); // printed value is always 4
```

## 2.4.4.3 Barriers

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

## 2.4.4.4 Atomic sections

An atomic operation is guaranteed to be performed on one thread at any given moment in time. In this sense they are indivisible, much like actual atoms. In concept they are identical to critical sections, but atomic sections can only ensure exclusivity for a single assignment operation, so they are used only for single statements. Their advantage is that they have lower overhead than critical sections.

Atomic operations are specified as pragmas, for example:

```
int a=0;
#pragma omp parallel num_threads(4)
{
    #pragma omp atomic
a++;
}
printf("%d\n",a); // printed value is always 4
}
```

## 2.4.5 Debugging OpenMP code

There are a few things to note when debugging OpenMP programs with GNU Debugger (GDB). GNU Compiler Collection (GCC) "outline" the parallel regions, meaning that it encapsulates the parallel code block into a function, which is called from the host function within each thread. Shared variables are copied into a container before being passed by reference to this function. Private variables are declared as local variables include the outlined function.

In the previous example, OpenMP would generate a container type:

```
struct .omp_data_s {
int place;
};
```

The outlined function would look similar to the following, without including the critical section:

```
void main._omp_fn.0(struct omp_data_s* omp_data_i) {
    printf("thread %d finished in\nposition%d\n",omp_get_thread_num(),omp_data_i->place);
}
```

GCC replaces the parallel region in main() with

```
struct omp_data_s omp_data_o;
omp_data_o.place=place;
__builtin_GOMP_parallel_start(main._omp_fn.0,
&omp_data_o, 2);
main._omp_fn.0 (&omp_data_o);
__builtin_GOMP_parallel_end();
place = omp_data_o.place;
```

## 2.4 Using Multiple Cores: OpenMP 67

Re-compile the example with the debug (-g) option and execute within GDB:

```
gcc omp_test.c -fopenmp -g

gdb a.out
```

Set a breakpoint on the line containing the #pragma omp parallel for and step once:

```
(gdb) b11
Breakpoint 1 at 0x8600: /share/reconfig/arm_code/omp_test.c:11. (2 locations)

(gdb) r
...
Breakpoint 1, main () at omp_test.c:11
11		#pragma omp parallel shared(place)

(gdb) s
[New Thread 0xb66b1430 (LWP 23388)]
[New Thread 0x5beb1430 (LWP 23389)]
[New Thread 0x5b6b1430 (LWP 23390)]
[Switching to Thread 0x5beb1430 (LWP 23389)]
Breakpoint 1, main__omp_fn () at omp_test.c:15
15			place++;
```

Notice how after stepping past the #pragma line, GDB shows that the program created three new workers. By default the debugging session remains in the master thread. The programmer can view the list of active threads using the "info threads" command, and switch the debugging session to another thread, for example, the "thread 1" command to switch to thread 1.

Also notice that the current function is now main__omp_fn (). Since the debugging session is no longer in the main function, the user cannot access the local variables.

Unfortunately, GCC does not generate debug information for locals within the parallel region. Later in this chapter you may need to use "info registers".

## 2.4.6 The OpenMP parallel for pragma

Kernels are usually comprised of a for-loop containing nested loops. OpenMP offers a simple way to automatically distribute the iterations of a for-loop to multiple threads using the for directive. The directive can be written as

```
#pragma omp parallel
#pragma omp for
for (...)
```

or as a shortcut:

```
#pragma omp parallel for
for (...)
```

The parallel for directive requires that the termination condition be a single less-than, less-than-equal, greater-than, or greater-than-or-equal comparison with the loop variable, the increment operation must not be dependent on code in the loop body, and not break, goto, or throw statements are allowed in the loop body.

By default the loop variable is treated as private. This is important since each thread will be simultaneously working on a different set of loop iterations and so the value of each thread's i variable will have different values at the same time.

Consider the following example:

```
#pragma omp parallel for
for (i=0;i<12;i++) {
    printf("iteration %d, thread %d\n",
    i,omp_get_thread_num());
}
```

When executed the new code will produce the following output:

+   iteration 0, thread 0
iteration 1, thread 0
iteration 2, thread 0
iteration 9, thread 3
iteration 10, thread 3
iteration 11, thread 3
