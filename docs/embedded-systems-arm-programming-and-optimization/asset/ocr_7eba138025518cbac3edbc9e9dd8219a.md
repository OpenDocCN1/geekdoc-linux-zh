# 5.3 Open Programming Model, Idioms, and Abstractions 195

Once the host obtains the platform handles, it can query them for information such as name, OpenCL version (profile), etc.

Related Functions:

```
cl_int clGetPlatformIDs(cl_uint num_entries,
```

```
cl_platform_id *platforms,
```

```
cl_uint *num_platforms)
```

Obtain the list of platforms available. Set the platforms argument to NULL to obtain the number of platforms.

```
cl_int clGetPlatformInfo(cl_platform_id platform_id,
```

```
cl_platform_info param_name,
```

```
size_t param_value_size,
```

```
void *param_value,
```

```
size_t *param_value_size_ret)
```

Get specific information about the OpenCL platform.

Required Declarations:

```
cl_platform_id platform_ids[8];
```

```
cl_int ret;
```

```
size_t length;
```

```
char str[1024];
```

Example Code:

```
// query clGetPlatformIDs(0,0,&num_platforms);
```

```
ret = clGetPlatformIDs(0,0,&num_platforms);
```

```
CHECK_STATUS(ret);
```

```
printf("Number of available platforms: %u\n", num_platforms);
```

```
// retrieve handle to platforms, limit to 8
```

```
ret = clGetPlatformIDs(num_platforms > 8 ? 8 :
```

```
num_platforms.platform_ids,0);
```

```
CHECK_STATUS(ret);
```