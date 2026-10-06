# 5.4 Kernel Workload Distribution 217

the host. To reconcile this difference, the host will send the kernel reference to each corresponding cl_mem object.

In other words, the host calls clSetKernelArg() for each of the kernel's corresponding arguments. Some of these may be scalars, but for each argument the host will pass its corresponding cl_mem object. Note that the host must pass each argument to clSetKernelArg() by reference as a void pointer, but the kernel receives a de-referenced version of each argument. Also note that clSetKernelArg() assigns each actual argument value to the kernel's formal arguments according to the order in which the formal arguments are listed in the kernel function (which specifies the formal argument by its relative position in the kernel's argument list.

For example, the arguments kernel prototype:

```
kernel void example_kernel(global float* invals,

    global float* outvals, int n)
```

...could be assigned on the host:

```
clSetKernelArg(my_kernel, 0, sizeof(cl_mem),

    (void*)&inval_buffer);
clSetKernelArg(my_kernel, 1, sizeof(cl_mem),

    (void*)outval_buffer);
clSetKernelArg(my_kernel, 2, sizeof(cl_mem),

    (void*)&n);
```

...where inval_buffer and outval_buffer are declared as cl_mem objects and n is declared as int.

To dispatch the kernel, the host calls clEnqueueNDRangeKernel(), whose arguments specify the workgroup size and number of workloads.

After the kernel completes execution, the host must call clEnqueueReadBuffer() to transfer the kernel's output arrays back to the host.

# Related Functions:

```
cl_int clSetKernelArg(cl_kernel kernel,

    cl_uint arg_index,

    size_t arg_size,

    const void *arg_value)
```

Used to set the argument value for a specific argument of a kernel.