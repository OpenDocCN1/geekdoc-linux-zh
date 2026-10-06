+   - Number of workgroups (referred to as “NWG")

For most GPUs, the unit of workload assigned to processor cores is the workgroup. This means that the programmer must instantiate at least many workgroup as cores in order to take advantage of multicore parallelism. As described above, the workgroup also has implications for the memory system, since only work-items within the same workgroup can share on-chip memory. Having too many workgroups will limit data sharing and also add overhead.

+   - Workgroup size (referred to as “WGS")

The workgroup size, or number of work-items per workgroup, affects the number of instructions executed per work-item invocation. Having too few work-items may limit the number of work-items the GPU can run on parallel SIMD lanes and limit the pool of work-items available to hide the latency of other work-items. Having too many work-items might result in work-items executing so instructions that their dispatch overhead outweighs their performance benefit. The workgroup size has an upper limit determined by the hardware but can be further limited by register and shared memory usage

+   - Work-item vector size (referred to as “VS")

The programmer can explicitly vectorize the OpenCL kernel, much like as described in Chapter 2 for ARM NEON instructions. This is less necessary for desktop and server GPUs since they are more effective at abstracting the vectorization from the programmer, while embedded GPUs may still benefit from this.

For a simple kernel like the Horner example, the product of NWG × WGS × VS determines the minimal number of elements processed by the kernel. If this number is less than the dataset, the kernel will need a loop.

The programmer can get hints for setting these parameters by invoking certain queries to the platform layer.

For example, the programmer can use getDeviceInfo() to report the maximum number of work items supported by the hardware in each of the three workgroup size dimensions (x, y, z):

```
ret = getDeviceInfo(device[DEVICE]);

CL_DEVICE_MAX_WORK_ITEM_SIZES,
3*sizeof(size_t),
```