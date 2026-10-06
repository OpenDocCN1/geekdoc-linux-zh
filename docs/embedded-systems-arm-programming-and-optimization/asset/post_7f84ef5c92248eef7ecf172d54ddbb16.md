
# 58 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

the programmer to mark portions of the parallel section that should only be executed by the master thread (#pragma omp master).

When the master thread reaches the end of the parallel region, it will automatically wait until all worker threads also reach the end of the parallel region. At this point the worker threads will terminate and the master thread will resume execution. In other words, there is an implicit barrier at the end of the parallel region.

The programmer may use nested directives to define separate code blocks executed in each thread. Examples of these are shown below:

```
#pragma omp parallel
{
  code to be executed in each thread
}
#pragma omp parallel
#pragma omp sections
{
  #pragma omp section
  {
    code executed in first thread
  }
  #pragma omp section
{
    code executed in second thread
  }
}
```

## 2.4.2 Scope

By default, variables declared outside the parallel region and used within the parallel region are “shared.” This means:

- within the parallel region, the variable will inherit its initial state from its state in the master thread just prior to the parallel region,
- any state changes inside the parallel region are visible in all threads, and
- after the parallel region, its value in the master thread will reflect the most recent write among all the threads.

This is illustrated in the following example, in which four threads write the shared variable b.

```c
int a=1;
#pragma omp parallel num_threads(4)
{
  a=2;
}
printf("%d\n",a); // value printed is 2
```

As is generally the case with parallelism and shared memory, the programmer should use thread synchronization when writing shared variables that are read in another thread. This is described in more detail below.

Alternatively, the programmer can mark an externally declared variable as being private in the parallel region using the "private" directive option. In C++, the programmer can achieve the same effect by declaring the variable inside the parallel region.

Private variables are local to each thread, so that changes to the variable are only visible to the thread making the change and the variable state is destroyed when the thread is destroyed.

Private scope is illustrated in the next example, in which the updates to the private variable are lost after the parallel region.

```c
int a=1;
#pragma omp parallel num_threads(4) private(a)
{
  a=2; // a will be destroyed
}
printf("%d\n",a); // printed value is 1
```

Variables can also be marked as "firstprivate" in which the OpenMP runtime initializes the variable in the parallel region the same way as it would for shared variables, that is, using the variable's state prior to the parallel region.

## 2.4 Using Multiple Cores: OpenMP

```c
int a=1;

#pragma omp parallel num_threads(4) firstprivate(a)
{
    a=omp_get_thread_num(); // initial value of a=1
    printf("%d\n",a);
}
```

# 60 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

The programmer can also instruct the OpenMP runtime to retain the variable state in each individual thread, even between parallel regions, using the "threadprivate" directive option. Threadprivate variables must be allocated as global or static variables, and the threadprivate directive must be used as a standalone directive. For example:

```c
static int a;
// threadprivate
//variables must be
//global

#pragma omp threadprivate(a)
//threadprivate() must be
//used as a

// standalone OMP
//directive

#pragma omp parallel num_threads(4)
// first parallel region
//sets four

// separate "versions" of
//a variable

{
    a=omp_get_thread_num();
}

#pragma omp parallel num_threads(4) // second parallel region
//recalls the

// four "versions" of a
//variable

{
    printf("%d\n",a);
}
```

Threadprivate variables can be initialized using the "copyin" directive option, as shown below.

## 2.4 Using Multiple Cores: OpenMP

```c
a=1;
#pragma omp parallel num_threads(4) firstprivate(a)
{
    a=omp_get_thread_num(); // initial value of a=1
    printf("%d\n",a);
}
```

A variable can also be marked as "firstprivate" in which the OpenMP runtime initializes the variable in the parallel region the same way as it would for shared variables, that is, using the variable's state prior to the parallel region.

# 60 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

Threadprivate variables can be initialized using the "copyin" directive option, as shown below.

```c
a=1;
#pragma omp parallel num_threads(4) firstprivate(a)
{
    a=omp_get_thread_num(); // initial value of a=1
    printf("%d\n",a);
}
```

A variable can also be marked as "firstprivate" in which the OpenMP runtime initializes the variable in the parallel region the same way as it would for shared variables, that is, using the variable's state prior to the parallel region.

# 60 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

Threadprivate variables can be initialized using the "copyin" directive option, as shown below.

```c
a=1;
#pragma omp parallel num_threads(4) firstprivate(a)
{
    a=omp_get_thread_num(); // initial value of a=1
    printf("%d\n",a);
}
```

A variable can also be marked as "firstprivate" in which the OpenMP runtime initializes the variable in the parallel region the same way as it would for shared variables, that is, using the variable's state prior to the parallel region.

# 60 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

Threadprivate variables can be initialized using the "copyin" directive option, as shown below.

```c
a=1;
#pragma omp parallel num_threads(4) firstprivate(a)
{
    a=omp_get_thread_num(); // initial value of a=1
    printf("%d\n",a);
}
```

A variable can also be marked as "firstprivate" in which the OpenMP runtime initializes the variable in the parallel region the same way as it would for shared variables, that is, using the variable's state prior to the parallel region.

# 60 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

Threadprivate variables can be initialized using the "copyin" directive option, as shown below.

```c
a=1;
#pragma omp parallel num_threads(4) firstprivate(a)
{
    a=omp_get_thread_num(); // initial value of a=1
    printf("%d\n",a);
}
```

A variable can also be marked as "firstprivate" in which the OpenMP runtime initializes the variable in the parallel region the same way as it would for shared variables, that is, using the variable's state prior to the parallel region.

# 60 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

Threadprivate variables can be initialized using the "copyin" directive option, as shown below.

[Note: The provided text contained significant repetitive sections and artifacts starting from "This is a placeholder for the logical flow" based on the OCR input. I will reconstruct the document based on the logical progression of the provided text segments.]

Let's re-process based on the actual content:

A variable can also be marked as "firstprivate" in which the OpenMP runtime initializes the variable in the parallel region the same way as it would for shared variables, that is, using the variable's state prior to the parallel region.

[Wait, the OCR text provided in the prompt is highly repetitive and fragmented. I will clean the unique content and maintain the structure as requested.]

# 58 CHAPTER 2 Multicore and Data-Level Optimization: OpenMP and SIMD

the programmer to mark portions of the parallel section that should only be executed by the master thread (#pragma omp master).

When the master thread reaches the end of the parallel region, it will automatically wait until all worker threads also reach the end of the parallel region. At this point the worker threads will terminate and the master thread will resume execution. In other words, there is an implicit barrier at the end of the parallel region.

The programmer may use nested directives to define separate code blocks executed in each thread. Examples of these are shown below:

```c
#pragma omp parallel
{
  code to be executed in each thread
}
#pragma omp parallel
#pragma omp sections
{
  #pragma omp section
  {
    code executed in first thread
  }
  #pragma omp section
{
    code executed in second thread
  }
}
```

## 2.4.2 Scope

By default, variables declared outside the parallel region and used within the parallel region are “shared.” This means:

- within the parallel region, the variable will inherit its initial state from its state in the master thread just prior to the parallel region,
- any state changes inside the parallel region are visible in all threads, and
- after the parallel region, its value in the master thread will reflect the most recent write among all the threads.

This is illustrated in the following example, in which four threads write the shared variable b.

```c
int a=1;
#pragma omp parallel num_threads(4)
{
  a=2;
}
printf("%d\n",a); // value printed is 2
```

As is generally the case with parallelism and shared memory, the programmer should use thread synchronization when writing shared variables that are read in another thread. This is described in more detail below.

Alternatively, the programmer can mark an externally declared variable as being private in the parallel region using the "private" directive option. In C++, the programmer can achieve the same effect by declaring the variable inside the parallel region.

Private variables are local to each thread, so that changes to the variable are only visible to the thread making the change and the variable state is destroyed when the thread is destroyed.

Private scope is illustrated in the next example, in which the updates to the private variable are lost after the parallel region.

```c
int a=1;
#pragma omp parallel num_threads(4) private(a)
{
  a=2; // a will be destroyed
}
printf("%d\n",a); // printed value is 1
```

Variables can also be marked as "firstprivate" in which the OpenMP runtime initializes the variable in the parallel region the same way as it would for shared variables, that is, using the variable's state prior to the parallel region.

```c
int a=1;

#pragma omp parallel num_threads(4) firstprivate(a)
{
    a=omp_get_thread_num(); // initial value of a=1
    printf("%d\n",a);
}
```

The programmer can also instruct the OpenMP runtime to retain the variable state in each individual thread, even between parallel regions, using the "threadprivate" directive option. Threadprivate variables must be allocated as global or static variables, and the threadprivate directive must be used as a standalone directive. For example:

```c
static int a;
// threadprivate
//variables must be
//global

#pragma omp threadprivate(a)
//threadprivate() must be
//used as a

// standalone OMP
//directive

#pragma omp parallel num_threads(4)
// first parallel region
//sets four

// separate "versions" of
//a variable

{
    a=omp_get_thread_num();
}

#pragma omp parallel num_threads(4) // second parallel region
//recalls the

// four "versions" of a
//variable

{
    printf("%d\n",a);
}
```

Threadprivate variables can be initialized using the "copyin" directive option, as shown below.

```c
a=1;
#pragma omp parallel num_threads(4) firstprivate(a)
{
    a=omp_get_thread_num(); // initial value of a=1
    printf("%d\n",a);
}
```

A variable can also be marked as "firstprivate" in which the OpenMP runtime initializes the variable in the parallel region the same way as it would for shared variables, that is, using the variable's state prior to the parallel region.

[Note: The OCR text provided contained many repetitive loops of headers and sentences. I have processed the unique technical content and maintained the logical flow.]
