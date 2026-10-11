```
*/*

```c
*/*
#include <fcntl.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>

int main(void)
{
  int fdsrc, fdnull, fdtmp, nbytes;
  char fname[] = "fread.c";
  char buf[10];

  /* open the source file, /dev/null, and /tmp/foo.bar */
  if((fdsrc = open(fname, O_RDONLY)) < 0) {
    perror("open fdsrc");
    exit(EXIT_FAILURE);
  }
  if((fdnull = open("/dev/null", O_WRONLY)) < 0) {
    perror("open fdnull");
    close(fdsrc); /* close this since we've opened it */
    exit(EXIT_FAILURE);
  }
  if((fdtmp = open("/tmp/foo.bar",
    O_CREAT | O_TRUNC | O_WRONLY,
    0644)) < 0) {
    perror("open fdtmp");
    close(fdsrc); /* have to close both of these now */
    close(fdnull);
    exit(EXIT_FAILURE);
  }

  /* read up to 10 bytes, write up to 10 bytes */
  while((nbytes = read(fdsrc, buf, 10)) != 0) {
    if(write(fdnull, buf, 10) < 0) /* the null device */
      perror("write /dev/null");
    if(write(fdtmp, buf, nbytes) < 0) /* a temporary file in /tmp */
      perror("write /tmp/foo.bar");
  }
}
```
```