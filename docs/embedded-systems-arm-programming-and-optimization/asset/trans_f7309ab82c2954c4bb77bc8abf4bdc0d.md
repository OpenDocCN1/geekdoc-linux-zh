

# 196 第5章 使用 OpenCL 的嵌入式异构编程

```c
// 查询每个平台
for (i = 0; i < num_platforms; i++) {
    ret = clGetPlatformInfo(platform_ids[i],
        CL_PLATFORM_PROFILE, 0, 0, &length);
    CHECK_STATUS(ret);
    ret = clGetPlatformInfo(platform_ids[i],
        CL_PLATFORM_PROFILE,
        length > 1024 ? 1024 : length, &str[0], 0);
    CHECK_STATUS(ret);
    printf("CL_PLATFORM_PROFILE: %s\n", str);
    // 显示平台版本
    ret = clGetPlatformInfo(platform_ids[i],
        CL_PLATFORM_VERSION,
        0.0, &length);
    CHECK_STATUS(ret);
    ret = clGetPlatformInfo(platform_ids[i],
        CL_PLATFORM_VERSION,
        length > 1024 ? 1024 : length, &str[0], 0);
    CHECK_STATUS(ret);
    printf("CL_PLATFORM_VERSION: %s\n", str);
    ret = clGetPlatformInfo(platform_ids[i],
        CL_PLATFORM_NAME, 0.0, &length);
    CHECK_STATUS(ret);
    ret = clGetPlatformInfo(platform_ids[i],
        CL_PLATFORM_NAME, length > 1024 ? 1024 : length,
        &str[0], 0);
    CHECK_STATUS(ret);
    printf("CL_PLATFORM_NAME: %s\n", str);
    ret = clGetPlatformInfo(platform_ids[i],
        CL_PLATFORM_VENDOR, 0, 0, &length);
```

## 5.3 OpenCL 编程模型、惯用法与抽象

```c
CHECK_STATUS(ret);
ret = clGetPlatformInfo(platform_ids[i],
    CL_PLATFORM_VENDOR,
    length > 1024 ? 1024 : length,
    &str[0], 0);
CHECK_STATUS(ret);
printf("CL_PLATFORM_VENDOR: %s\n", str);
ret = clGetPlatformInfo(platform_ids[i],
    CL_PLATFORM_EXTENSIONS,
    0.0, &length);
CHECK_STATUS(ret);
ret = clGetPlatformInfo(platform_ids[i],
    CL_PLATFORM_EXTENSIONS,
    length > 1024 ? 1024 : length,
    &str[0], 0);
CHECK_STATUS(ret);
printf("CL_PLATFORM_EXTENSIONS: %s\n", str);
```

### 5.3.4 平台层：初始化设备

本节描述了平台层中特定于设备的函数。

**实践中：**

一旦主机（host）获取了平台的句柄，它必须获取设备的句柄。可选情况下，它可以查询设备的信息。

示例代码调用了 `clGetDeviceIds()` 和 `clDeviceInfo()` 来获取与每个平台关联的设备句柄。

**相关函数：**

```c
cl_int clGetDeviceIds(cl_platform_id platform,
    cl_device_type device_type,
    cl_uint num_entries,
    cl_device_id *devices,
    cl_uint *num_devices);
```

# 198 第5章 使用 OpenCL 的嵌入式异构编程

```c
cl_int clGetDeviceInfo(cl_device_id device,
    cl_device_info param_name,
    size_t param_value_size,
    void *param_value,
    size_t *param_value_size_ret);
```

获取有关 OpenCL 设备的信息。

**必要的声明：**

```c
cl_device_id devices;
```

**示例代码：**

```c
ret = clGetDeviceIds(platform_ids[0], CL_DEVICE_TYPE_ALL, 0, 0,
    &num_devices);

CHECK_STATUS(ret);
printf("Number of devices for platform 0: %d\n", num_devices);
for(i=0; i<num_devices; i++) {
    ret = clGetDeviceIds(platform_ids[0],
    CL_DEVICE_TYPE_ALL, 0, num_devices, &device[i]);
    CHECK_STATUS(ret);
}

for(i=0; i<num_devices; i++) {
    ret = clDeviceInfo(device[i],
    CL_DEVICE_NAME, 0, 0, &length);
    CHECK_STATUS(ret);
    ret = clDeviceInfo(device[i],
    CL_DEVICE_NAME, length>1024:length,
    &str[0], 0);
    printf("Device NAME: %s\n", str);
}
```

# 5.3 OpenCL 编程模型、惯用法与抽象 199

5.3.5 平台层：初始化上下文

上下文（context）是主机上的一个抽象，用于管理主机与设备之间的交互。每个与设备交互的 OpenCL 函数都需要上下文。

**实践中：**

在获取平台和设备的句柄后，主机调用 `clCreateContext` 或 `clCreateContextFromType` 来获取与设备关联的上下文句柄。

这两个函数相似，`clCreateContext()` 返回一个带有设备句柄的上下文，而 `clCreateContextFromType()` 返回一个与给定设备类型（如 GPU）关联的上下文。这两个函数都通过引用返回上下文。回调函数 `pfn_notify` 和关联的 `user_data` 用于运行时异步报告错误，但如果不需要这种行为，程序员可以设置为 NULL。示例代码使用 `clCreateContextFromType()` 为类型为 `CL_DEVICE_TYPE_GPU` 的设备请求上下文句柄，然后使用该句柄来发现内核构建并确定工作组大小。

**相关函数：**

```c
cl_context clCreateContext(cl_context_properties *properties,
    cl_int num_devices,
    cl_device_id *devices,
    void (*pfn_notify)(const char *errinfo,
    const void *private_info,
    size_t cb,
    void *user_data),
    cl_int *errcode_ret);

cl_context clCreateContextFromType(cl_context_properties *properties,
    cl_device_type device_type,
    void (*pfn_notify)(const char *errinfo,
    const void *private_info,
    size_t cb,
    void *user_data,
    cl_int *errcode_ret);

cl_int clReleaseContext(cl_context context);
```

创建一个 OpenCL 上文（从指定的设备）。从设备类型创建 OpenCL 上文。减少引用计数。当计数达到零时，OpenCL 运行时从内存中卸载上下文。

**必要的定义/声明：**

```c
#define DEVICE 0
cl_context context;
cl_context_properties context_props[] = {
    CL_CONTEXT_PLATFORM, (cl_context_properties)platform_ids[0], 0
};
```

**示例代码：**

```c
context = clCreateContextFromType(context_props,
    CL_DEVICE_TYPE_GPU, 0, 0, &ret);
CHECK_STATUS(ret);
ret = clGetContextInfo(context, CL_CONTEXT_DEVICES,
    0, NULL, &deviceBufferSize);

CHECK_STATUS(ret);
ret = clGetContextInfo(context, CL_CONTEXT_DEVICES,
    deviceBufferSize, &device[DEVICE], NULL);
CHECK_STATUS(ret);
```

### 5.3.6 平台层：内核控制

主机与设备之间的所有通信通过命令队列（command queue）处理。程序员使用命令队列设置内核数据集并向内核发送输入。

**实践中：**

程序通过将关联的上下文传递给 `clCreateCommandQueue()` 获取命令队列句柄。调用 `clCreateCommandQueue()` 时，指定 `CL_QUEUE_PROFILING_ENABLE` 选项，这将允许主机收集运行时信息。

**相关函数：**

```c
cl_command_queue clCreateCommandQueue(cl_context context,
    cl_device_id device,
    cl_command_queue_properties properties,
    cl_int *errcode_ret);
```

在特定设备上创建命令队列。

```c
cl_int clReleaseCommandQueue(cl_command_queue command_queue);
```

减少命令队列的引用计数。

**必要的声明：**

```c
cl_command_queue queue;
```

**示例代码：**

```c
queue = clCreateCommandQueue(context, device,
    CL_QUEUE_PROFILING_ENABLE, &ret);
CHECK_STATUS(ret);
```

# 202 第5章 使用 OpenCL 的嵌入式异构编程

### 5.3.7 平台层：内核编译

OpenCL 内核代码通常由主机程序在运行时编译。因此，OpenCL 使用的是即时编译（JIT）方法，而内核不是与主机代码一起编译（如在 NVIDIA 的 CUDA 框架中那样），主机代码必须包含一系列操作来读取内核代码并使用 API 调用对其进行编译。

**实践中：**

编译内核源码的平台层函数并不接收可能预期的源文件路径，而是接收一个指向零终止字符数组（C 字符串）的指针，其中包含了源代码。因此，程序员在调用编译函数之前必须使用标准系统将内核源码读取到字符串中。

要做到这一点，打开文件（使用 `fopen()`），确定其大小（使用 `fseek()`、`fell()`、`fseek()`），为字符串分配内存（使用 `malloc()`），然后将文件内容读取到字符串中（使用 `fread()`）。在将字符串传递给编译函数之前，确保为字符串分配额外的字符以进行零终止。

要编译程序，调用 `CreateProgramWithSource()` 获取程序句柄，调用 `clBuildProgram()` 编译程序，并使用 `clCreateKernel()` 创建内核实例。

构建时，程序可以传递存储在选项字符串中的编译器选项。此示例使用了“cl-fast-relaxed-math”。这些选项允许 GPU 执行不 100% 符合 IEEE 754 标准的浮点运算，但比保证合规时具有更高的吞吐量。

由于程序员（通常）无法在 OpenCL主机 API 之外编译任何 OpenCL 内核，程序员需要一种方法来识别内核源码中的任何语法或语义错误。对于此程序，可以使用 `clGetProgramBuildInfo()` 结合协处理器的设备 ID。

