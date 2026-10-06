
# 252 APPENDIX B NEON Intrinsic

* l specifies 64-bit input width but generates a 128-bit output width.
* hn stores the high half of each result element.
* q specifies 128-bit input and output width.
* l specifies 64-bit input width but generates a 128-bit output width.
* w allows the operation to accept one 128-bit operand and a second 64-bit operand and generate a 128-bit result.
* hn stores the high half of each result element.

## B.5.4 Operand type and width

operand width is:

* s8, s16, s32: signed integer
* u8, u16, u32: unsigned integer
* p8: integer
* f16, f32: floating point

# OpenCL reference

This appendix provides a reference for the most common features of OpenCL versions 1.1 and 1.2. These are older versions but are most likely to be supported on embedded GPUs at the time of writing.

**This appendix is intended only as a quick reference; it provides only a brief summary of relevant information.** For a more thorough description of any feature, the reader should refer to the official OpenCL documentation. Much of this information is from the Khronos Group, available at https://www.khronos.org.

## C.1 PLATFORM LAYER

The platform layer includes a set of functions called by the host to query coprocessor communications and instantiate device channels. This section lists the most commonly used:

```c
cl_int GetPlatformIDs (cl_uint num_entries,
                         cl_platform_id *platform,
                         cl_uint *num_platforms);
```

Obtain the list of available platforms.

*This function retrieves the number of available platforms (if platforms is NULL) or retrieves handles to the actual platforms themselves (if num_platforms contains a value).*

```c
cl_int GetPlatformInfo (cl_platform_id platform,
                         cl_platform_info param_name,
                         size_t *param_value_size);

# C OpenCL Reference

```c
void *param_value,
size_t *param_value_ret)
```

param_name: CL_PLATFORM_(PROFILE, VERSION)

Get information about the OpenCL platform.

This function retrieves information regarding the available platform(s), such as the OpenCL version and set of supported extensions. This is most useful for writing portable OpenCL applications, allowing the application to adapt to the capabilities of available platforms.

```c
cl_int GetDeviceIDs (cl_platform_id platform,
                      cl_device_type device_type,
                      cl_uint num_entries,
                      cl_device_id *devices,
                      cl_uint *num_devices)
```

device_type: CL_DEVICE_TYPE_(ACCELERATOR, ALL, CPU, CUSTOM, DEFAULT, GPU)

Obtain the list of devices available on a platform.

This function retrieves device handles. Every OpenCL application must call this function to access a device.

```c
cl_int GetDeviceInfo (cl_device_id device,
                      cl_device_info param_name,
                      size_t *param_value_size,
                      void *param_value,
                      size_t *param_value_ret)
```

param_name: CL_DEVICE_(NAME, VENDOR, PROFILE, TYPE)
CL_DEVICE_NATIVE_VECTOR_WIDTH_(CHAR, INT)
CL_DEVICE_NATIVE_VECTOR_WIDTH_(LONG, SHORT)
CL_DEVICE_NATIVE_VECTOR_WIDTH_(DOUBLE, HALF)
CL_DEVICE_NATIVE_VECTOR_WIDTH_FLOAT,

# C.1 Platform Layer

```c
CL_DEVICE_PREFERRED_VECTOR_WIDTH_(CHAR, INT),
CL_DEVICE_PREFERRED_VECTOR_WIDTH_(LONG, SHORT),
CL_DEVICE_PREFERRED_VECTOR_WIDTH_(DOUBLE, HALF),
CL_DEVICE_PREFERRED_VECTOR_WIDTH_FLOAT,
CL_DEVICE_PREFERRED_INTEROP_USER_SYNC,
CL_DEVICE_ADDRESS_BITS,
CL_DEVICE_AVAILABLE,
CL_DEVICE_BUILT_KERNELS,
CL_DEVICE_COMPILER_AVAILABLE,
CL_DEVICE_(DOUBLE, HALF)_FP_CONFIG,
CL_DEVICE_ENDIAN_LITTLE,
CL_DEVICE_EXTENSIONS,
CL_DEVICE_ERROR_SUPPORT,
CL_DEVICE_EXECUTION_CAPABILITIES,
CL_DEVICE_GLOBAL_MEM_CACHE_(SIZE, TYPE),
CL_DEVICE_GLOBAL_MEM_(CACHELINE_SIZE),
CL_DEVICE_HOST_UNIFIED_MEMORY,
CL_DEVICE_IMAGE_MAX_(ARRAY, BUFFER)_SIZE,
CL_DEVICE_IMAGE_SUPPORT,
CL_DEVICE_IMAGE2D_MAX_(WIDTH, HEIGHT),
CL_DEVICE_IMAGE3D_MAX_(WIDTH, HEIGHT, DEPTH),
CL_DEVICE_LOCAL_MEM_(TYPE, SIZE),
CL_DEVICE_MAX_(READ, WRITE)_IMAGE_ARGS,
CL_DEVICE_MAX_CLOCK_FREQUENCY,
CL_DEVICE_MAX_COMPUTE_UNITS,
CL_DEVICE_MAX_CONSTANT_(ARGS, BUFFER_SIZE),
CL_DEVICE_MAX_(MEM_ALLOC, PARAMETER)_SIZE,
CL_DEVICE_MAX_SAMPLERS,
CL_DEVICE_MAX_WORK_GROUP_SIZE,
CL_DEVICE_MAX_WORK_ITEM(DIMENSIONS, SIZES),
CL_DEVICE_MEM_BASE_ADDR_ALIGN,
CL_DEVICE_OPENCL_VERSION,
CL_DEVICE_PARENT_DEVICE,
