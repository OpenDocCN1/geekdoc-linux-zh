# 5.4 Kernel Workload Distribution 219

```
const cl_event *event_wait_list,
cl_event *event)
```

Enqueue commands to read from a buffer object to host memory.

```
cl_int clFinish(cl_command_queue command_queue)
```

Blocks until all previously queued OpenCL commands in a command queue are issued to the associated device and have completed.

```
cl_int clGetEventProfilingInfo(cl_event event),
cl_profiling_info param_name,
size_t param_value_size,
void *param_value,
size_t *param_value_size_ret
```

Returns profiling information for the command associated with event if profiling is enabled.

Required Definitions/Declarations:

The following definitions will provide the input size (in bytes), the kernel vector size, the work group size (assuming 1D workgroups), the number of workgroups (assuming 1D array of workgroups), and the device number.

In this example, the number of workgroups is maximized by setting N/(4 × VS × WGS). This will cause each work item to perform only one loop iteration.

```
#define N 1024*1024
#define VS 4
#define WGS 256
#define NWG N/(4*VS*WGS)
#define DEVICE 1
```

localSize and globalSize are 1D arrays that specify the workgroup size and number of workgroups to the platform layer.

localSize directly determines the workgroup size, while globalSize determines the total number of work-items. The number of workgroups is thus implied as globalSize/localSize.