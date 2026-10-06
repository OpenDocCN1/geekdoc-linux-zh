# 2.4 Using Multiple Cores: OpenMP 57

![](bbox=[0.218, 0.146, 0.574, 0.269])

**FIGURE 2.2** OpenMP thread creation. per_event tracks performance counter events only within the master thread (solid line).

The most commonly used OpenMP directive is the *parallel* directive, which specifies the start of a *parallel region*:

```
#pragma omp parallel <directive options>
```

As shown in Figure 2.2, in the OpenMP programming model, all programs begin their execution as a single thread called the master thread. Some point the master thread will encounter a parallel region, which will create *worker threads*. Together with the master thread, these worker threads will execute the code inside the parallel region concurrently. The number of worker threads created when the processor encounters a parallel region will have previously been determined by the programmer using any of the following in decreasing order of precedence:

+   - in the *num_threads()* directive option, e.g., `#pragma omp num_threads(4)*`

+   - through a call to OpenMP function `omp_set_number_threads()`, e.g., `omp_set_number_threads(4)*`, or

+   - through the value of the OMP_NUM_THREADS environment variable at program launch.

Since the master thread counts toward the total number of threads, the parallel region will cause the OpenMP runtime to create *one less* than the number specified by the programmer. Often, the program will be structured such that the master thread and worker threads execute exactly the same code. In this case their behavior will only differ in the ranges of input and output data processed (i.e., their array indices are specified as a function of their thread ID).

In other cases each thread will branch off to code sections. In other cases the worker threads will execute the same code while the master thread performs special functions. OpenMP includes a directive that allows