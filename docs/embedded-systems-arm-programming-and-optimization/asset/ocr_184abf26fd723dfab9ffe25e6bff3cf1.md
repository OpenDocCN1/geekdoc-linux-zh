# 198 CHAPTER 5 Embedded Heterogeneous Programming with OpenCL

```
cl_device_id *devices,
cl_uint *num_devices;
```

Obtain the list of devices available on a platform.

```
cl_int clGetDeviceInfo(cl_device_id,
cl_device_info param_name,
size_t param_value_size,
void *param_value,
size_t *param_value_size_ret
```

Get information about an OpenCL device.

Required Declarations:

```
cl_device_id devices;
```

Example Code:

```
ret = clGetDeviceIds(platform_ids[0], CL_DEVICE_TYPE_ALL,0,0,
&num_devices);
```

```
CHECK_STATUS(ret);
printf("Number of devices for platform 0: %d\n",num_devices);
for(i=0;i<num_devices;i++) {
```

```
ret =
clGetDeviceIds(platform_ids[0]),
CL_DEVICE_TYPE_ALL,num_devices,&device[i],0);
CHECK_STATUS(ret);
```

```
for(i=0;i<num_devices;i++) {
ret = clGetDeviceInfo(device[i], CL_DEVICE_NAME, 0, 0,
&length);
CHECK_STATUS(ret);
```

```
ret=clGetDeviceInfo(device[i],
CL_DEVICE_NAME,
length>1024?1024:length.
```