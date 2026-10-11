To use these macros, pass the `st_mode` member of the `stat` structure as the `mode` argument to the listed macros. The sample program that follows illustrates their usage.

# *Example*

![](bbox=[0.04, 0.15, 0.15, 0.19])

# ### Example

To run this program, pass it the name of the file that interests you.

```
""" 
/*
 * mstat.c = Naive stat(1) program
*/
#include <unistd.h>
#include <sys/stat.h>
#include <stdlib.h>
#include <stdio.h>

int main(int argc, char **argv)
{
  struct stat buf;
  mode_t mode;
  char type[80];
  if(argc != 2) {
    puts("USAGE: mstat FILENAME");
    exit(EXIT_FAILURE);
  }

  if((lstat(argv[1], &buf)) < 0) {
    perror("lstat");
    exit(EXIT_FAILURE);
  }
  mode = buf.st_mode;
  printf("   FILE: %s\n", argv[1]);
  printf("   INODE: %d\n", buf.st_ino);
  printf("   DEVICE: %d, %d\n",
         major(buf.st_dev), minor(buf.st_dev));

  printf(" MODE: %o\n", buf.st_mode & ~(S_IFMT));

  printf("   LINKS: %d\n", buf.st_nlink);
  printf("   UID: %d\n", buf.st_uid);
  printf("   GID: %d\n", buf.st_gid);"""
```