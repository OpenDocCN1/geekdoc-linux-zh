# 108 CHAPTER 3 Arithmetic Optimization and the Linux Framebuffer

```
screensize = vinfo.xres * vinfo.yres * vinfo.bits_per_pixel / 8
row_size = vinfo.xres * vinfo.bits_per_pixel / 8
```

Now map the framebuffer itself to a block of virtual memory within our program's:

```
char *fbp;

fbp 5 (char *)mmap(0, screensize, PROT_READ | PROT_WRITE,
MAP_SHARED, fd, 0);

if ((int)fbp 5 -1) err("Error: failed to map framebuffer \
device to memory");
```

The program can now paint pixels by writing data to the region of memory pointed to by the fbp pointer. The code that draws pixels depends on the pixel size. For example, for 16-bit pixels (which the most significant 5 bits are red intensity, the least significant 5 bits are blue, and the middle 6 bits are the green intensity):

+   **((unsigned short *)(fbp + i*(row_size) + j*2) =
  (red << 11) | (green << 5) | blue);

The Linux framebuffer is a zero-copy framebuffer, meaning that a single write from the program updates the pixel on the monitor. The upper bound for our frames per second (fps) using the write memory bandwidth experiment from Chapter 1.

For example, the Raspberry Pi has a write bandwidth of 325 MB/s, while a $1920 \times 1080 \times 16$ frame is comprised of $4,147,200$ bytes, so the program can achieve $1/(4,147,200/325 \times 20) = 82$ fps.

Once you are finished with the framebuffer you should unmap the memory and close the file:

```
munmap(fbp, screensize);
close(fd);
```

# 3.2 AFFINE IMAGE TRANSFORMATIONS

Anyone who has played a video game, flipped through virtual covers on their personal media device, or used image editing software is familiar with the idea of image transformations. An image transformation describes an operation that changes or distorts an image. A linear image transformation, in particular, can be used to do things such as rotate, scale, shear, reflect, or project an image.