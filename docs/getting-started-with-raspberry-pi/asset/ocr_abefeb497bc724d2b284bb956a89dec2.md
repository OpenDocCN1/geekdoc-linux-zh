Listing 12.1 is a simple application that works over the frame buffer API. The program clears the screen by operating on `/dev/fb0`, the frame buffer device node corresponding to the display. It first decipheres the visible resolutions and the *bits per pixel* in a hardware-independent manner using the frame buffer API, `FBIOGET_VSCREENINFO`. This interface command gleans the display's variable parameters by operating on the `fb_var_screeninfo` structure. The program then goes on to `mmap()` the frame buffer memory and clears each constituent pixel bit.

# Listing 12.1. Clear the Display in a Hardware-Independent Manner

```
Code View:

```c
#include <stdio.h>
#include <fcntl.h>
#include <linux/fb.h>
#include <sys/mman.h>
#include <stdlib.h>

struct fb_var_screeninfo vinfo;

int
main(int argc, char *argv[])
{
    int fbfd, fbsize, i;
    unsigned char *fbbuf;

    /* Open video memory */
    if ((fbfd = open("/dev/fb0", O_RDWR)) < 0) {
        exit(1);
    }

    /* Get variable display parameters */
    if (ioctl(fbfd, FBIOGET_VSCREENINFO, &vinfo)) {
        printf("Bad vscreeninfo ioctl\n");
        exit(2);
    }

    /* Size of frame buffer =
       (X-resolution * Y-resolution * bytes per pixel) */
    fbsize = vinfo.xres*vinfo.yres*(vinfo.bits_per_pixel/8);

    /* Map video memory */
    if ((fbbuf = mmap(0, fbsize, PROT_READ|PROT_WRITE,
                      MAP_SHARED, fbfd, 0)) == (void *)-1){
        exit(3);
    }

    /* Clear the screen */
    for (i=0; i<fbsize; i++) {
        *(fbbuf+i) = 0x00;
    }

    munmap(fbbuf, fbsize);
    close(fbfd);
}
```
```