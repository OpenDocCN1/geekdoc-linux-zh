```
size_t image_height,
size_t image_depth,
size_t image_row_pitch,
size_t image_slice_pitch,
void *host_ptr,
cl_int *errcode_ret
```

Creates a 3D image object. [OpenCL 1.1 only]

This function creates an image object. This was replaced in OpenCL 1.2 withclCreateImage().

# C4 PROGRAMS AND COMPILING

OpenCL kernels can be compiled at runtime using CreateProgramWithSource() and BuildProgram(or clCompileProgram() and clLinkProgram()) or offline using CreateProgramWithBinary().

Either way, the kernel code is stored in separate file from the host object code, so the host must explicitly read the kernel code before dispatching it onto the device for execution.

After this, the program is associated with a kernel using a function such as clCreateKernel(), arguments are set using SetKernelArg(), and invoked by a function such as EnqueueNDRangeKernel().

```
cl_program createProgramWithSource(cl_context context,
cl_uint count,
const char **strings,
const size_t *lengths,
cl_int *errcode_ret
```

Creates a program object for a context, and loads the source code specified by the text in the strings array into the program object.

Using this function as part of a "just-in-time" compilation method is perhaps the most common method to compile a kernel in OpenCL. Since different devices often have different binary interfaces, this approach provides an obvious advantage in portability. Its drawback is that it compiles the kernel