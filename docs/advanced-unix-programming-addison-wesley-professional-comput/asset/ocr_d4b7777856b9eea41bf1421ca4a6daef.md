The following program, which is very specific to FreeBSD's implementation of FFS, shows one way to access the superblock and an i-node by reading the disk device /dev/ad0slg, which is a raw disk device that happens to contain the /usr directory tree. That this is so can be seen by executing the mount command (which knows FFS as type "ufs"):

```
$ mount
/dev/ad0sla on / (ufs, NFS exported, local)
/dev/ad0slf on /tmp (ufs, local, soft-updates)
/dev/ad0slg on /usr (ufs, local, soft-updates)
/dev/ad0sle on /var (ufs, local, soft-updates)
procfs on /proc (procfs, local)
```

# Here's the program:

```
```c
#ifdef FREEBSD
#error "Program is for FreeBSD only."
#endif

#include "defs.h"
#include <sys/param.h>
#include <ufs/ffs/fs.h>
#include <ufs/ufs/dinode.h>

#define DEVICE "/dev/ad0slg"

int main(int argc, char *argv[])
{
int fd;
long inumber;
char sb_buf[(sizeof(struct fs) / DEV_BSIZE) + 1] * DEV_BSIZE];
struct fs *superblock = (struct fs *)sb_buf;
struct dinode *d;
ssize_t nread;
off_t fsbo, fsba;
char *inode_buf;
size_t inode_buf_size;

if (argc < 2) {
printf("Usage: inode n\n");
exit(EXIT_FAILURE);
}
inumber = atol(argv[1]);
```
```