# 5.3 OpenCL Programming Model, Idioms, and Abstractions 203

Creates a program object for a context, and loads the source code specified by the text strings in the strings array into the program object.

```
cl_int clBuildProgram(cl_program_program,
    cl_uint num_devices,
    const cl_device_id *device_list,
    const char *options,
    void (*pfn_notify)(cl_program, void *user_data),
    void *user_data)
```

Builds (compiles and links) a program executable from the program source or binary.

```
cl_kernel clCreateKernel(cl_program_program,
    const char *kernel_name,
    cl_int *errcode_ret)
```

Creates a kernel object.

cl_int clReleaseKernel(cl_kernel kernel)

Decrements the kernel reference count.

```
cl_int clProgramBuildInfo(cl_program_program,
    cl_device_id device,
    cl_program_build_info param_name,
    size_t param_value_size,
    void *param_value,
    size_t *param_value_size_ret)
```

Returns build information for each device in the program object.

```
cl_int clReleaseProgram(cl_program_program)
```

Decrements the program reference count.

Required Declarations:

```
cl_program_program;
cl_kernel kernel;
FILE *myFile;
```