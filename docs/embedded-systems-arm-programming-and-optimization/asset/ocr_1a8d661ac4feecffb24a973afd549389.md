# 262 APPENDIX C OpenCL Reference

```
cl_uint_num_events_in_wait_list,
const cl_event *event_wait_list,
cl_event *event
```

Enqueue commands to read from a buffer object to host memory.

The name of this function can potentially be confusing. “Read” is from the perspective of the host, so this function is normally applied to an output array of the kernel. In other words, the programmer refers to the output array as a read buffer, since it will be eventually read by the host.

```
cl_int clEnqueueBufferRect(cl_command_queue command_queue,
cl_mem buffer,
cl_bool blocking_read,
const size_t *buffer_origin,
const size_t *host_origin,
const size_t *region,
size_t buffer_row_pitch,
size_t buffer_slice_pitch,
size_t host_row_pitch,
size_t host_slice_pitch,
void *ptr,
cl_uint *num_events_in_wait_list,
const cl_event **event_wait_list,
cl_event *event)
```

Enqueue commands to read from a rectangular region from a buffer object to host memory.

This function is necessary for copying a subregion of a 2D array to the host. This isn't necessary when copying an entire 2D array having the elements of its major dimension stored consecutively since such an array occupies a contiguous block of memory and can be copied with clEnqueueRead-Buffer().

```
cl_int clEnqueueBuffer(cl_command_queue command_queue,
cl_mem buffer.)
```