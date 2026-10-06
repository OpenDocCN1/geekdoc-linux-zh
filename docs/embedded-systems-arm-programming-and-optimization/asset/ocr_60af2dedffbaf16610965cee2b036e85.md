# 270 APPENDIX C OpenCL

source code every time the program is executed, adding performance over-head that degrades the overall benefit from coprocessor acceleration.

```
cl_program clCreateProgramWithBinary(cl_context context,

cl_uint num_devices,
const cl_device_id *device_list,
const size_t *lengths,
const unsigned char **binaries,
cl_int *binary_status,
cl_int *errcode_ret)
```

Creates a program object for a context, and loads specified binary data into the program object.

This function allows the loading of pre-compiled kernels. Many OpenCL platform implementations don't offer a standalone (offline) compiler. In this case, the programmer needs to write or her own program that compiles the kernel, extract the binary using clGetProgramInfo(), and save it to a file.

```
cl_program clCreateProgramWithBuiltKernels(cl_context context,

cl_uint num_devices,
const cl_device_id *device_list,
const char *kernel_names,
cl_int *errcode_ret)
```

Creates a program object for a context, and loads the information related to the built-in kernels into a program object.

This function allows vendors to offer pre-made kernels to programmers.

```
cl_int clRetainProgram(cl_program program)
```

Increments the program reference count.

This function prevents a program object from being deleted by the runtime.

```
cl_int clReleaseProgram(cl_program program)
```