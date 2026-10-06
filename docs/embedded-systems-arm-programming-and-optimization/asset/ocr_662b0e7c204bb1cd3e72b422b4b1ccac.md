# 180 CHAPTER 4 Memory Optimization and Video Processing

```
int capture_frame (struct v4l2_buffer *buf) {
    fd_set fds;
    int ret;
    struct timeval tv;
```

The Linux select() system can synchronize the software with the frame capture rate of the camera. select() is used to block a program's execution until new data is ready to be read. It is often used when using the Sockets API to wait for incoming network data.

Make sure you open the framebuffer after opening the capture device to ensure the capture device's file descriptor has a value greater than the framebuffer. Otherwise, the select() will call fail.

```
tv.tv_sec=0;
tv.tv_usec=0;

FD_ZERO(&fds);
FD_SET(fd1,&fds);

ret = select(fd1+1, &fds, NULL, NULL, &tv);
if(ret == -1) {
    perror("waiting for frame");
    return 1;
}
```

The next IO control will dequeue a frame buffer from Video4Lux and then enqueue another request for the buffer.

```
if(ioctl(fd1, VIODOC_DQBUF, buf) == -1) {
    perror("retrieving frame");
    return 1;
}

if(ioctl(fd1, VIODOC_QBUF, buf) == -1) {
    perror("queuing buffer");
    return 0;
}
```