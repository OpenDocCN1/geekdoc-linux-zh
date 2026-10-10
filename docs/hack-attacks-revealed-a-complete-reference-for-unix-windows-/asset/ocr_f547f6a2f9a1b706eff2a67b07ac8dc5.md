```
```
}
return NULL;
}
return XMSBuf;
}
```
```

**The following example puts the extended memory functions together:**

```
```
/* A sequential table of variable length records in XMS */
#include <dos.h>
#include <stdio.h>
#include <stdlib.h>
#include <alloc.h>
#include <string.h>

#define TRUE 1
#define FALSE 0

/*
BLOCKSIZE will be the size of our real-memory buffer that
we'll swap XMS through (must be a multiple of 1024, since
XMS is allocated in 1K chunks.)
*/

#ifdef __SMALL__
#define BLOCKSIZE (16L * 1024L)
#endif

#ifdef __MEDIUM__
#define BLOCKSIZE (16L * 1024L)
#endif

#ifdef __COMPACT__
#define BLOCKSIZE (64L * 1024L)
#endif

#ifdef __LARGE__
#define BLOCKSIZE (64L * 1024L)
#endif

/*
XMSParms is a structure for copying information to and from
real-mode memory to XMS memory
*/
struct parmstruct
{
/* blocklength is the size in bytes of block to copy
*/
unsigned long blockLength;
```
```