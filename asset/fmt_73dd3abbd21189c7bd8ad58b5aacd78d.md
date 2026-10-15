
**This appendix is intended only as a quick reference; it provides only a brief summary of relevant information.** For a more thorough description of any feature, the reader should refer to the official OpenCL documentation. Much of this information is from the Khronos Group, available at https://www.khronos.org.

# C OpenCL Reference

## C.1 PLATFORM LAYER

The platform layer includes a set of functions called by the host to query coprocessor communications and instantiate device channels. This section lists the most commonly used:

```c
cl_int GetPlatformIDs (cl_uint num_entries,
                         cl_platform_id *platform,
                         cl_uint *num_platforms);
```

Obtain the list of available platforms.

*This function retrieves the number of available platforms (if `platforms` is NULL) or retrieves handles to the actual platforms themselves (if `num_platforms` contains a value).*

```c
cl_int GetPlatformInfo (cl_platform_id platform,
                         cl_platform_info param_name,
                         size_t *param_value_size);
```

```c
void *param_value,
size_t *param_value_ret)
```

`param_name`: `CL_PLATFORM_(PROFILE, VERSION)`

Get information about the OpenCL platform.

This function retrieves information regarding the available platform(s), such as the OpenCL version and set of supported extensions. This is most useful for writing portable OpenCL applications, allowing the application to adapt to the capabilities of available platforms.

```c
cl_int GetDeviceIDs (cl_platform_id platform,
                      cl_device_type device_type,
                      cl_uint num_entries,
                      cl_device_id *devices,
                      cl_uint *num_devices)
```

`device_type`: `CL_DEVICE_TYPE_(ACCELERATOR, ALL, CPU, CUSTOM, DEFAULT, GPU)`

Obtain the list of devices available on a platform.

This function retrieves device handles. Every OpenCL application must call this function to access a device.

```c
cl_int GetDeviceInfo (cl_device_id device,
                      cl_device_info param_name,
                      size_t *param_value_size,
                      void *param_value,
                      size_t *param_value_ret)
```

`param_name`: `CL_DEVICE_(NAME, VENDOR, PROFILE, TYPE)`
`CL_DEVICE_NATIVE_VECTOR_WIDTH_(CHAR, INT)`
`CL_DEVICE_NATIVE_VECTOR_WIDTH_(LONG, SHORT)`
`CL_DEVICE_NATIVE_VECTOR_WIDTH_(DOUBLE, HALF)`
`CL_DEVICE_NATIVE_VECTOR_WIDTH_FLOAT`,

## C.1 Platform Layer

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
```

## C.2 内存类型

表 C.1 从主机（host）和内核（kernel）角度的 OpenCL 缓冲区类型

| 全局 (Global) | 常量 (Constant) | 局部 (Local) | 私有 (Private) |
| --- | --- | --- | --- |
| 主机 (Host) | 动态分配，读写访问 | 动态分配，读写访问 | 动态分配，无访问 | 无分配，无访问 |
| 内核 (Kernel) | 无分配，读写访问 | 静态分配，只读 | 静态分配，读写访问 | 静态分配，读写访问 |

所有函数局部变量默认使用私有内存，通常用于标量，例如循环迭代器和索引计算的临时变量。
