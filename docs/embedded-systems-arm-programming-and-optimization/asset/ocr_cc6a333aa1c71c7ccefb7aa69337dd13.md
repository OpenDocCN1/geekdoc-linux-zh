# 194 CHAPTER 5 Embedded Heterogeneous Programming with OpenCL

```
__LINE__ ,_\nopencl_error_to_str(status):\nnexit(0);\
```

This chapter's example code will invoke this macro after every call to an OpenCL platform function.

# 5.3.3 Platform layer: Initializing the platforms

OpenCL platform functions begin with "c1" followed by a capital letter, for example:clGetDeviceIdsAndclFinish().

In practice, calls to the OpenCL platform functions serve one of the following purposes:

+   - querying the OpenCL runtime for device-specific or kernel-specific information (e.g., determining how many devices are present or determining the maximum number of work-items allowed for a device);
- device memory management (e.g., allocating memory on a device);
- sending commands to the device (e.g., initiating kernel execution on a device).

This section describes how to obtain a handle to the platforms and query them for information.

# In Practice:

Some OpenCL functions require that the host call them twice: once to obtain the size of the requested data structure and again to obtain its data.

The initialization section of the example host code calls clGetPlatformIDs() to obtain the number of available platforms. Using the returned number of platforms, it allocates a correspondingly sized array of cl_platform_id and calls the function again to obtain a list of platform handles.

For example, a theoretical embedded SoC may contain CPUs, GPUs, and an FPGA fabric. In this case, the OpenCL platform layer would include one platform corresponding to the GPU, another platform corresponding to the FPGA fabric, and potentially a third platform to allow OpenCL kernels to execute on the CPU cores. However, in practice most embedded SoCs today only have one platform.